---
date: {{date:YYYY-MM-DD}}
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
    { item: "Contas", valor: -45, moeda: 'EUR', tipo: 'Gasto' },
    { item: "Terapia", valor: -80, moeda: 'EUR', tipo: 'Gasto' },
    { item: "Proteína", valor: -15, moeda: 'EUR', tipo: 'Gasto' },
    { item: "Spotify", valor: -32, moeda: 'BRL', tipo: 'Gasto' }, // Valor em reais
    { item: "Bitcoin", valor: -80, moeda: 'BRL', tipo: 'Investimento' },
    { item: "Reserva Emergência", valor: -480, moeda: 'BRL', tipo: 'Investimento' },
    { item: "Ethereum", valor: -60, moeda: 'BRL', tipo: 'Investimento' },
    { item: "Reserva do Carro", valor: -555, moeda: 'BRL', tipo: 'Investimento' },
    { item: "Revolut", valor: -200, moeda: 'EUR', tipo: 'Investimento' },
    { item: "Exemplo Gasto", valor: -0, moeda: 'EUR', tipo: 'Gasto' },
    { item: "Exemplo Investimento", valor: -0, moeda: 'EUR', tipo: 'Investimento' },
   
    
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
- [ ] 