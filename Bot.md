---
date: 2025-04-17
hora: 22:59
tags:
---
O bot tem que ter:
compra parcial
	só executar venda parcial 
venda por estagnação



Adcionar
- [x] Saldo do USDC
- [x] Função de validação robusta
- [ ] melhorar o relatório diário
- [x] O modelo de ML deve usar RandomForest, o data.set deve ter mais de 100k entradas
- [ ] falar com o chatgpt sobre adicionar mais pares
	- [ ] Acho que eu vou me comprometer a adicionar mais pares depois da versão 10, refinar todas as funções base e depois aumentar o número de pares
- [ ] podia fazer uma análise macro, sobre ciclos de subida ou descida e coisas assim, mas não sei se faz sentido, ou se o negócio é deixar o 
- [x] ativos estagnados - fazer com que ele recomece a contar os 15 minutos caso o código seja reiniciado (talvez ele já esteja fazendo isso)
- [ ] adicionei o DOT e o HYPER na versão 11
- [ ] Agora o % máximo é 30%. Mas ainda não fica menos de 60 usdc na conta. Talvez deva mudar isso. PErguntar pro chat
- [ ] quero adicionar a cópia do csv para o dropbox
- [ ] O trailing dinamico parece estar vendendo frequentemente com prejuízo. Será que eu devo deixar ele um pouco mais sensível?


# Código
Estou rodando esse código, é um bot de trade de cripto que opera com 5 pares. ao iniciar o bot e depois de cada operação de compra e venda ele atualiza as posições abertas. Contudo, ele não está atualizando o saldo de USDC, que forma que o bot não vê o saldo disponível para fazer novas compras. Atualize isso. 
import time
import math
import traceback
import requests
import pandas as pd
import csv
import os
from datetime import datetime, timedelta
from binance.client import Client
from binance.exceptions import BinanceAPIException
import threading

## ========== CONFIGURAÇÃO ==========
API_KEY = ''
API_SECRET = ''

PAIRS = ["BTCUSDC", "ETHUSDC", "ADAUSDC", "SOLUSDC", "XRPUSDC"]
TIMEFRAME = Client.KLINE_INTERVAL_1MINUTE

USE_BALANCE_PERCENT = 0.15
MIN_USDC_TRADE = 5

MIN_TRADE_BY_PAIR = {
    "BTCUSDC": 15,
    "ETHUSDC": 5,
    "ADAUSDC": 2,
    "SOLUSDC": 3,
    "XRPUSDC": 2
}

ENABLE_TELEGRAM = True
TELEGRAM_TOKEN = ":"
TELEGRAM_CHAT_ID = ""

LOG_FILE = "registro_operacoes.csv"

client = Client(API_KEY, API_SECRET)
positions = {symbol: None for symbol in PAIRS}
position_times = {symbol: None for symbol in PAIRS}

def send_telegram_message(message: str):
    if ENABLE_TELEGRAM:
        try:
            url = f"https://api.telegram.org/bot{TELEGRAM_TOKEN}/sendMessage"
            params = {"chat_id": TELEGRAM_CHAT_ID, "text": message}
            requests.get(url, params=params, timeout=5)
        except Exception as e:
            print(f"Erro ao enviar mensagem Telegram: {e}")

def registrar_operacao(tipo: str, symbol: str, quantidade: float, preco: float, motivo: str):
    cabecalho = ["timestamp", "tipo", "par", "quantidade", "preco", "motivo"]
    if not os.path.exists(LOG_FILE):
        with open(LOG_FILE, mode="w", newline="", encoding="utf-8") as f:
            writer = csv.writer(f)
            writer.writerow(cabecalho)
    with open(LOG_FILE, mode="a", newline="", encoding="utf-8") as f:
        writer = csv.writer(f)
        writer.writerow([
            datetime.utcnow().strftime("%Y-%m-%d %H:%M:%S"),
            tipo,
            symbol,
            f"{quantidade:.6f}",
            f"{preco:.4f}",
            motivo
        ])
def verificar_vendas_por_estagnacao():
    now = datetime.utcnow()
    for symbol, pos in positions.items():
        if pos is not None:
            tempo_posicao = (now - position_times[symbol]).total_seconds() / 60
            if tempo_posicao >= 15:
                try:
                    qty = round(pos["quantity"], 6)
                    client.order_market_sell(symbol=symbol, quantity=qty)
                    registrar_operacao("VENDA", symbol, qty, pos["entry_price"], "Venda por estagnação (15min)")
                    send_telegram_message(f"[{symbol}] VENDA por estagnação: {qty:.6f} @ {pos['entry_price']:.4f} USDC após {tempo_posicao:.1f} min")
                    positions[symbol] = None
                    position_times[symbol] = None
                    atualizar_posicoes()
                except Exception as e:
                    print(f"[ERRO] Venda por estagnação falhou para {symbol}: {e}")


def calculate_indicators(df: pd.DataFrame):
    close = df["close"]
    delta = close.diff()
    up = delta.clip(lower=0)
    down = (-delta).clip(lower=0)
    avg_gain = up.rolling(window=14, min_periods=14).mean()
    avg_loss = down.rolling(window=14, min_periods=14).mean()
    rs = avg_gain / avg_loss
    rsi = 100 - (100 / (1 + rs))
    ema12 = close.ewm(span=12, adjust=False).mean()
    ema26 = close.ewm(span=26, adjust=False).mean()
    macd_line = ema12 - ema26
    signal_line = macd_line.ewm(span=9, adjust=False).mean()
    ema9 = close.ewm(span=9, adjust=False).mean()
    return {
        "close": close.iloc[-1],
        "rsi": rsi.iloc[-1],
        "macd": macd_line.iloc[-1],
        "prev_macd": macd_line.iloc[-2],
        "signal": signal_line.iloc[-1],
        "prev_signal": signal_line.iloc[-2],
        "ema9": ema9.iloc[-1]
    }

def obter_min_lot_size(symbol):
    try:
        exchange_info = client.get_symbol_info(symbol)
        for f in exchange_info["filters"]:
            if f["filterType"] == "LOT_SIZE":
                return float(f["minQty"])
    except Exception as e:
        print(f"[ERRO] Falha ao obter minQty de {symbol}: {e}")
    return None

def atualizar_posicoes():
    for symbol in PAIRS:
        try:
            base_asset = symbol.replace("USDC", "")
            balance = client.get_asset_balance(asset=base_asset)
            if balance and float(balance["free"]) > 0:
                qty = float(balance["free"])
                ticker = client.get_symbol_ticker(symbol=symbol)
                entry_price = float(ticker["price"])
                positions[symbol] = {
                    "entry_price": entry_price,
                    "quantity": qty,
                    "peak_price": entry_price,
                    "partial_sold": False
                }
                position_times[symbol] = datetime.utcnow()
                print(f"[INFO] Posição detectada em {symbol}: {qty} unidades a {entry_price}.")
        except Exception as e:
            print(f"Erro ao atualizar posição para {symbol}: {e}")

def enviar_relatorio_diario():
    if not os.path.exists(LOG_FILE):
        return
    hoje = datetime.utcnow().date()
    df = pd.read_csv(LOG_FILE)
    df["timestamp"] = pd.to_datetime(df["timestamp"])
    df_dia = df[df["timestamp"].dt.date == hoje]
    total = len(df_dia)
    saldo = 0
    if not df_dia.empty:
        compras = df_dia[df_dia["tipo"] == "COMPRA"]["preco"].astype(float).sum()
        vendas = df_dia[df_dia["tipo"] == "VENDA"]["preco"].astype(float).sum()
        saldo = vendas - compras
    msg = f"\U0001F4CA Relatório diário ({hoje}):\nOperações: {total}\nResultado líquido: {saldo:.2f} USDC"
    send_telegram_message(msg)

def agendar_relatorio():
    while True:
        agora = datetime.utcnow()
        alvo = datetime.combine(agora.date(), datetime.strptime("16:00", "%H:%M").time()) - timedelta(hours=1)
        if agora > alvo:
            alvo += timedelta(days=1)
        espera = (alvo - agora).total_seconds()
        time.sleep(espera)
        enviar_relatorio_diario()

threading.Thread(target=agendar_relatorio, daemon=True).start()
send_telegram_message("Bot de trading iniciado e monitorando pares.")
print("Bot de trading iniciado. Monitorando pares:", PAIRS)
print("-" * 60)
atualizar_posicoes()

while True:
    agora = time.time()
    espera = 60 - (agora % 60)
    time.sleep(espera)

    try:
        for symbol in PAIRS:
            try:
                klines = client.get_klines(symbol=symbol, interval=TIMEFRAME, limit=100)
            except Exception as e:
                print(f"[ERRO] Falha ao obter dados de {symbol}: {e}")
                continue

            df = pd.DataFrame(klines, columns=["open_time", "open", "high", "low", "close", "volume",
                                               "close_time", "quote_vol", "trades", "taker_base_vol",
                                               "taker_quote_vol", "ignore"])
            df["close"] = pd.to_numeric(df["close"], errors='coerce')
            if df["close"].isnull().any() or len(df) < 26:
                continue

            indicators = calculate_indicators(df)
            price = indicators["close"]
            rsi = indicators["rsi"]
            macd = indicators["macd"]
            prev_macd = indicators["prev_macd"]
            prev_signal = indicators["prev_signal"]
            signal = indicators["signal"]
            ema9 = indicators["ema9"]

            print(f"{symbol} -> Preço: {price:.4f}, RSI: {rsi:.2f}, MACD: {macd:.4f}, Signal: {signal:.4f}, EMA9: {ema9:.4f}")

            if positions[symbol] is None:
                if rsi < 50 and macd > signal and price <= ema9 * 1.005:
                    try:
                        balance = client.get_asset_balance(asset="USDC")
                        usdc_free = float(balance["free"]) if balance else 0.0
                        amount_usdc = usdc_free * USE_BALANCE_PERCENT
                        min_trade = MIN_TRADE_BY_PAIR.get(symbol, MIN_USDC_TRADE)

                        if amount_usdc < min_trade:
                            continue

                        order = client.order_market_buy(symbol=symbol, quoteOrderQty=round(amount_usdc, 2))
                        qty = sum(float(fill["qty"]) for fill in order["fills"])
                        entry_price = sum(float(fill["price"]) * float(fill["qty"]) for fill in order["fills"]) / qty

                        positions[symbol] = {
                            "entry_price": entry_price,
                            "quantity": qty,
                            "peak_price": entry_price,
                            "partial_sold": False
                        }
                        position_times[symbol] = datetime.utcnow()

                        registrar_operacao("COMPRA", symbol, qty, entry_price, "Sinal técnico agressivo")
                        send_telegram_message(f"Comprado {symbol}: {qty:.6f} @ {entry_price:.4f} USDC")
                        atualizar_posicoes()
                    except Exception as e:
                        print(f"[ERRO] Falha na compra: {e}")
            else:
                pos = positions[symbol]
                entry_price = pos["entry_price"]
                qty = pos["quantity"]
                peak_price = pos["peak_price"]
                partial_sold = pos["partial_sold"]

                if price > peak_price:
                    positions[symbol]["peak_price"] = price

                sell_reason = None
                now = datetime.utcnow()
                tempo_posicao = (now - position_times[symbol]).total_seconds() / 60

                if not partial_sold and price >= entry_price * 1.004:
                    sell_qty = qty * 0.5
                    min_lot = obter_min_lot_size(symbol)
                    if min_lot and sell_qty >= min_lot:
                        try:
                            client.order_market_sell(symbol=symbol, quantity=round(sell_qty, 6))
                            registrar_operacao("VENDA", symbol, sell_qty, price, "Venda parcial 0.4% lucro")
                            send_telegram_message(f"Venda parcial de {symbol}: {sell_qty:.6f} @ {price:.4f} USDC")
                            positions[symbol]["quantity"] = qty - sell_qty
                            positions[symbol]["partial_sold"] = True
                        except Exception as e:
                            print(f"[ERRO] Venda parcial falhou: {e}")
                    else:
                        print(f"[AVISO] Venda parcial ignorada: {sell_qty:.8f} < min LOT_SIZE ({min_lot})")
                elif tempo_posicao >= 15:
                    sell_reason = "Ativo estagnado 15min"
                elif price >= entry_price * 1.008:
                    sell_reason = "Lucro total 0.8%"
                elif price <= entry_price * 0.99:
                    sell_reason = "Stop loss 1%"
                elif peak_price > entry_price and price <= peak_price * 0.996:
                    sell_reason = "Trailing Stop 0.4%"
                elif (
                    rsi > 60 and  # RSI realmente alto
                    prev_macd > prev_signal and  # MACD cruzou de cima para baixo
                    macd < signal and  # MACD está abaixo da linha de sinal agora
                    price > entry_price * 1.002  # lucro de pelo menos 0.2%
                ):
                    sell_reason = "RSI alto + cruzamento descendente do MACD com lucro"
                elif (rsi > 60 and  # RSI realmente alto
                    prev_macd > prev_signal and  # MACD cruzou de cima para baixo
                    macd < signal and  # MACD está abaixo da linha de sinal agora
                    price > entry_price * 1.002  # lucro de pelo menos 0.2%
                ):
                    sell_reason = "RSI alto + cruzamento descendente do MACD com lucro"
                elif rsi > 55 and prev_macd > signal and macd < signal:
                    sell_reason = "RSI > 55 e MACD cruzando"

                if sell_reason:
                    try:
                        client.order_market_sell(symbol=symbol, quantity=round(positions[symbol]["quantity"], 6))
                        registrar_operacao("VENDA", symbol, positions[symbol]["quantity"], price, sell_reason)
                        send_telegram_message(f"VENDA {symbol}: {positions[symbol]['quantity']:.6f} @ {price:.4f} USDC -- {sell_reason}")
                        positions[symbol] = None
                        position_times[symbol] = None
                        atualizar_posicoes()
                    except Exception as e:
                        print(f"[ERRO] Venda falhou: {e}")

    except Exception as e:
        print(f"[ERRO GERAL]: {e}")
    verificar_vendas_por_estagnacao()
