---
date: 2024-11-28
hora: 17:44
tags:
---

```dataviewjs
// Defina a taxa de câmbio atual de BRL para EUR
const taxaCambioBRLparaEUR = 6; // 1 EUR = 6 BRL

const transacoes = [
    { item: "Salário", valor: 1125, moeda: 'EUR', tipo: 'Salário' },
    { item: "Aluguel", valor: 1500, moeda: 'BRL', tipo: 'Salário' },
    { item: "Paitrocínio", valor: 5000, moeda: 'BRL', tipo: 'Salário' }, // Caso esteja presente
    { item: "Academia", valor: -40, moeda: 'EUR', tipo: 'Gasto' },
    { item: "Telefone", valor: -20, moeda: 'EUR', tipo: 'Gasto' },
    { item: "Zotero", valor: -1.70, moeda: 'EUR', tipo: 'Gasto' },
    { item: "Conta energia", valor: -30, moeda: 'EUR', tipo: 'Gasto' },
    { item: "Terapia", valor: -80, moeda: 'EUR', tipo: 'Gasto' },
    { item: "Spotify", valor: -32, moeda: 'BRL', tipo: 'Gasto' }, // Valor em reais
    { item: "Bitcoin", valor: -80, moeda: 'BRL', tipo: 'Investimento' },
    { item: "Reserva Emergência", valor: -480, moeda: 'BRL', tipo: 'Investimento' },
    { item: "Ethereum", valor: -60, moeda: 'BRL', tipo: 'Investimento' },
    { item: "Reserva do Carro", valor: -555, moeda: 'BRL', tipo: 'Investimento' },
    { item: "Revolut", valor: -0, moeda: 'EUR', tipo: 'Investimento' },
    { item: "Dona Isabel", valor: -16, moeda: 'EUR', tipo: 'Gasto' },
    { item: "Exemplo Investimento", valor: -0, moeda: 'EUR', tipo: 'Investimento' },
    { item: "Exemplo Gasto", valor: -0, moeda: 'EUR', tipo: 'Gasto' },
   { item: "Dinheiro do BR", valor: -650, moeda: 'BRL', tipo: 'Gasto' },
   { item: "Mercado Semana 1", valor: -11, moeda: 'EUR', tipo: 'Gasto' },
   { item: "Mercado Semana 2", valor: -45, moeda: 'EUR', tipo: 'Gasto' },
   { item: "Acumpultura", valor: -90, moeda: 'EUR', tipo: 'Gasto' },
   { item: "Aliexpress", valor: -80, moeda: 'EUR', tipo: 'Gasto' },
   { item: "Compras natalinas", valor: -100, moeda: 'EUR', tipo: 'Gasto' },
    
];

let totalGastos = 0;
let totalInvestimentos = 0;
let totalSalario = 0;

let totalGastosEmEUR = 0;
let totalInvestimentosEmEUR = 0;
let valorAluguel = 0;
let valorPaitrocinio = 0;

transacoes.forEach(transacao => {
    let valorEmEUR = transacao.moeda === 'BRL'
        ? parseFloat((transacao.valor / taxaCambioBRLparaEUR).toFixed(2))
        : transacao.valor;

    // Identificar e armazenar os valores de Aluguel e Paitrocínio
    if (transacao.item === 'Aluguel') {
        valorAluguel = valorEmEUR;
    }
    if (transacao.item === 'Paitrocínio') {
        valorPaitrocinio = valorEmEUR;
    }

    if (transacao.tipo === 'Gasto') {
        totalGastos += valorEmEUR;

        // Somar gastos em EUR, excluindo Aluguel e Paitrocínio
        if (transacao.moeda === 'EUR' && transacao.item !== 'Aluguel' && transacao.item !== 'Paitrocínio') {
            totalGastosEmEUR += valorEmEUR;
        }
    } else if (transacao.tipo === 'Investimento') {
        totalInvestimentos += valorEmEUR;

        // Somar investimentos em EUR
        if (transacao.moeda === 'EUR') {
            totalInvestimentosEmEUR += valorEmEUR;
        }
    } else if (transacao.tipo === 'Salário') {
        totalSalario += valorEmEUR;
    }
});

let totalLiquido = totalSalario + totalGastos + totalInvestimentos;

// Cálculo do Restante do Salário
let restanteSalario = totalSalario - valorAluguel - valorPaitrocinio + totalGastosEmEUR + totalInvestimentosEmEUR;

dv.table(
    ["Descrição", "Valor em EUR", " "],
    transacoes.map(transacao => {
        let valorEmEUR = transacao.moeda === 'BRL'
            ? parseFloat((transacao.valor / taxaCambioBRLparaEUR).toFixed(2))
            : transacao.valor;
        let emojiTipo = '';
        if (transacao.tipo === 'Gasto') {
            emojiTipo = '💸';
        } else if (transacao.tipo === 'Investimento') {
            emojiTipo = '📈';
        } else if (transacao.tipo === 'Salário') {
            emojiTipo = '💰';
        }
        return [
            transacao.item,
            valorEmEUR.toLocaleString('pt-PT', { style: 'currency', currency: 'EUR' }),
            emojiTipo
        ];
    })
);

dv.paragraph(`**Restante do Salário:** ${restanteSalario.toLocaleString('pt-PT', { style: 'currency', currency: 'EUR' })}`);
dv.paragraph(`**Total de Gastos:** ${totalGastos.toLocaleString('pt-PT', { style: 'currency', currency: 'EUR' })}`);
dv.paragraph(`**Total de Investimentos:** ${totalInvestimentos.toLocaleString('pt-PT', { style: 'currency', currency: 'EUR' })}`);
dv.paragraph(`**Total Líquido:** ${totalLiquido.toLocaleString('pt-PT', { style: 'currency', currency: 'EUR' })}`);

```

# Gastos Previstos
- [ ] comprar minoxidil - 60 eur
- [x] Acumpultura
- [ ] presentes de natal
	- [x] Bel - terapia + camisetinha + alguma coisa fofa
	- [ ] Gírio - Camiseta do Benfica
	- [x] Celso - Cult of the lamb + ficções https://www.wook.pt/livro/ficcoes-jorge-luis-borges/24074498?gad_source=1 
	- [x] Jardim - Babel
	- [ ] Pai - Veias abertas da américa latina em alemão - https://www.ebay.com/itm/386382228985?_trkparms=amclksrc%3DITM%26aid%3D1110006%26algo%3DHOMESPLICE.SIM%26ao%3D1%26asc%3D264183%26meid%3Db914780b6fd14784869e9bb1349d9280%26pid%3D101224%26rk%3D2%26rkt%3D5%26sd%3D235261729100%26itm%3D386382228985%26pmt%3D1%26noa%3D1%26pg%3D2332490%26algv%3DDefaultOrganicWebV9BertRefreshRankerWithCassiniEmbRecall&_trksid=p2332490.c101224.m-1
- [x] Coisas no aliexpress
	- [x] potinhos
	- [x] capa do kobo
	- [x] um fidget
	- [x] suporte do monitor
	- [x] pano de chão
	- [x] toalha de microfibra academia
	- [x] necessairezinha
	- [x] capa do fone
	- [x] presente fátima
	- [x] coisinha de contar apertos
- [ ] bolsa da uniqlo
- [x] Mercado - Semana 3
	- [x] 2 latas de feijão
	- [x] dois pacotes de brocolis
	- [ ] 



