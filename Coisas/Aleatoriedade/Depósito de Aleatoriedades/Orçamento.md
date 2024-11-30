---
date: 2024-11-25
tags:
---

|          |       |     |
| -------- | ----- | --- |
| Aluguel  | -200  |     |
| Academia | -40   |     |
| Telefone | -20   |     |
| Zotero   | -1.70 |     |
| Contas   | -45   |     |
| Terapia  | -80   |     |
| Reserva  | 1     |     |
| Carro    | 1     |     |
| Proteina | -15   |     |
| Spotify  | -5    |     |
<!-- TBLFM: @I$>..@8$>=sum($2..$-1) -->
<!-- TBLFM: @>$2=sum(@I..@-1) -->


```dataviewjs
const gastos = [
    { item: "Aluguel", valor: -200 },
    { item: "Academia", valor: -40 },
    { item: "Telefone", valor: -20 },
    { item: "Zotero", valor: -1.70 },
    { item: "Contas", valor: -45 },
    { item: "Terapia", valor: -80 },
    { item: "Reserva", valor: 1 },
    { item: "Carro", valor: 1 },
    { item: "Proteína", valor: -15 },
    { item: "Spotify", valor: -5 },
];

let total = gastos.reduce((acc, gasto) => acc + gasto.valor, 0);

dv.table(["Descrição", "Valor"], gastos.map(gasto => [gasto.item, gasto.valor]));
dv.paragraph(`**Total:** ${total}`);
```

```dataviewjs
const gastos = [
    { item: "Aluguel", valor: -200 },
    { item: "Academia", valor: -40 },
    { item: "Telefone", valor: -20 },
    { item: "Zotero", valor: -1.70 },
    { item: "Contas", valor: -45 },
    { item: "Terapia", valor: -80 },
    { item: "Reserva", valor: 1 },
    { item: "Carro", valor: 1 },
    { item: "Proteína", valor: -15 },
    { item: "Spotify", valor: -5 },
];

let total = gastos.reduce((acc, gasto) => acc + gasto.valor, 0);

dv.table(["Descrição", "Valor"], gastos.map(gasto => [gasto.item, gasto.valor]));
dv.paragraph(`**Total:** ${total}`);
```


```dataviewjs
// Defina a taxa de câmbio atual de BRL para EUR
const taxaCambioBRLparaEUR = 1 / 6; // 1 BRL = aproximadamente 0,1666667 EUR

const gastos = [
    { item: "Aluguel", valor: -200, moeda: 'EUR' },
    { item: "Academia", valor: -40, moeda: 'EUR' },
    { item: "Telefone", valor: -20, moeda: 'EUR' },
    { item: "Zotero", valor: -1.70, moeda: 'EUR' },
    { item: "Contas", valor: -45, moeda: 'EUR' },
    { item: "Terapia", valor: -80, moeda: 'EUR' },
    { item: "Reserva", valor: 1, moeda: 'EUR' },
    { item: "Carro", valor: 1, moeda: 'EUR' },
    { item: "Proteína", valor: -15, moeda: 'EUR' },
    { item: "Spotify", valor: -25, moeda: 'BRL' }, // Valor em reais
];

let total = gastos.reduce((acumulador, gasto) => {
    let valorEmEUR = gasto.moeda === 'BRL'
        ? parseFloat((gasto.valor * taxaCambioBRLparaEUR).toFixed(2))
        : gasto.valor;
    return acumulador + valorEmEUR;
}, 0);

dv.table(
    ["Descrição", "Valor Original", "Valor em EUR"],
    gastos.map(gasto => {
        let valorEmEUR = gasto.moeda === 'BRL'
            ? parseFloat((gasto.valor * taxaCambioBRLparaEUR).toFixed(2))
            : gasto.valor;
        return [
            gasto.item,
            gasto.valor.toLocaleString('pt-PT', { style: 'currency', currency: gasto.moeda }),
            valorEmEUR.toLocaleString('pt-PT', { style: 'currency', currency: 'EUR' })
        ];
    })
);

dv.paragraph(`**Total:** ${total.toLocaleString('pt-PT', { style: 'currency', currency: 'EUR' })}`);
```


```dataviewjs
// Defina a taxa de câmbio atual de BRL para EUR
const taxaCambioBRLparaEUR = 1 / 6; // 1 BRL = aproximadamente 0,1667 EUR

const gastos = [
    { item: "Aluguel", valor: -200, moeda: 'EUR' },
    { item: "Academia", valor: -40, moeda: 'EUR' },
    { item: "Telefone", valor: -20, moeda: 'EUR' },
    { item: "Zotero", valor: -1.70, moeda: 'EUR' },
    { item: "Contas", valor: -45, moeda: 'EUR' },
    { item: "Terapia", valor: -80, moeda: 'EUR' },
    { item: "Reserva", valor: 1, moeda: 'EUR' },
    { item: "Carro", valor: 1, moeda: 'EUR' },
    { item: "Proteína", valor: -15, moeda: 'EUR' },
    { item: "Spotify", valor: -25, moeda: 'BRL' }, // Valor em reais
];

let total = gastos.reduce((acumulador, gasto) => {
    let valorEmEUR = gasto.moeda === 'BRL'
        ? parseFloat((gasto.valor * taxaCambioBRLparaEUR).toFixed(2))
        : gasto.valor;
    return acumulador + valorEmEUR;
}, 0);

dv.table(
    ["Descrição", "Valor em EUR"],
    gastos.map(gasto => {
        let valorEmEUR = gasto.moeda === 'BRL'
            ? parseFloat((gasto.valor * taxaCambioBRLparaEUR).toFixed(2))
            : gasto.valor;
        return [
            gasto.item,
            valorEmEUR.toLocaleString('pt-PT', { style: 'currency', currency: 'EUR' })
        ];
    })
);

dv.paragraph(`**Total:** ${total.toLocaleString('pt-PT', { style: 'currency', currency: 'EUR' })}`);
```


```dataviewjs
// Defina a taxa de câmbio atual de BRL para EUR
const taxaCambioBRLparaEUR = 1 / 6; // 1 BRL = aproximadamente 0,1667 EUR

const gastos = [
    { item: "Salário", valor: 1125, moeda: 'EUR', tipo: 'Salario' },
    { item: "Aluguel", valor: -200, moeda: 'EUR', tipo: 'Despesa' },
    { item: "Academia", valor: -40, moeda: 'EUR', tipo: 'Despesa' },
    { item: "Telefone", valor: -20, moeda: 'EUR', tipo: 'Despesa' },
    { item: "Zotero", valor: -1.70, moeda: 'EUR', tipo: 'Despesa' },
    { item: "Contas", valor: -45, moeda: 'EUR', tipo: 'Despesa' },
    { item: "Terapia", valor: -80, moeda: 'EUR', tipo: 'Despesa' },
    { item: "Reserva", valor: 450, moeda: 'BRL', tipo: 'Economia' },
    { item: "Carro", valor: 450, moeda: 'BRL', tipo: 'Economia' },
    { item: "Proteína", valor: -15, moeda: 'EUR', tipo: 'Despesa' },
    { item: "Spotify", valor: -32, moeda: 'BRL', tipo: 'Despesa' }, // Valor em reais
    { item: "Bitcoin", valor: -80, moeda: 'BRL', tipo: 'Investimento' },
    { item: "Mês passado", valor: 0, moeda: 'EUR', tipo: 'Economia' },
    { item: "Mês passado", valor: 0, moeda: 'EUR', tipo: 'Economia' },
];

let totalDespesas = 0;
let totalInvestimentos = 0;
let totalEconomias = 0;
let totalSalario = 0;

gastos.forEach(gasto => {
    let valorEmEUR = gasto.moeda === 'BRL'
        ? parseFloat((gasto.valor * taxaCambioBRLparaEUR).toFixed(2))
        : gasto.valor;

    if (gasto.tipo === 'Despesa') {
        totalDespesas += valorEmEUR;
    } else if (gasto.tipo === 'Investimento') {
        totalInvestimentos += valorEmEUR;
    } else if (gasto.tipo === 'Economia') {
        totalEconomias += valorEmEUR;
    } else if (gasto.tipo === 'Salario') {
        totalSalario += valorEmEUR;
        
    }
});

let totalGeral = totalDespesas + totalSalario;

dv.table(
    ["Descrição", "Valor em EUR", "Tipo"],
    gastos.map(gasto => {
        let valorEmEUR = gasto.moeda === 'BRL'
            ? parseFloat((gasto.valor * taxaCambioBRLparaEUR).toFixed(2))
            : gasto.valor;
        return [
            gasto.item,
            valorEmEUR.toLocaleString('pt-PT', { style: 'currency', currency: 'EUR' }),
            gasto.tipo
        ];
    })
);

dv.paragraph(`**Total Geral:** ${totalGeral.toLocaleString('pt-PT', { style: 'currency', currency: 'EUR' })}`);
dv.paragraph(`**Total de Despesas:** ${totalDespesas.toLocaleString('pt-PT', { style: 'currency', currency: 'EUR' })}`);
dv.paragraph(`**Total de Investimentos:** ${totalInvestimentos.toLocaleString('pt-PT', { style: 'currency', currency: 'EUR' })}`);
dv.paragraph(`**Total de Economias:** ${totalEconomias.toLocaleString('pt-PT', { style: 'currency', currency: 'EUR' })}`);

```



```dataviewjs
// Defina a taxa de câmbio atual de BRL para EUR
const taxaCambioBRLparaEUR = 1 / 6; // 1 BRL = aproximadamente 0,1667 EUR

const transacoes = [
    { item: "Salário", valor: 1125, moeda: 'EUR', tipo: 'Salário' },
    { item: "Aluguel", valor: 1500, moeda: 'BRl', tipo: 'Salário' },
    { item: "Paitrocínio", valor: 5000, moeda: 'BRl', tipo: 'Salário' },
    { item: "Renda", valor: -200, moeda: 'EUR', tipo: 'Gasto' },
    { item: "Academia", valor: -40, moeda: 'EUR', tipo: 'Gasto' },
    { item: "Telefone", valor: -20, moeda: 'EUR', tipo: 'Gasto' },
    { item: "Zotero", valor: -1.70, moeda: 'EUR', tipo: 'Gasto' },
    { item: "Contas", valor: -45, moeda: 'EUR', tipo: 'Gasto' },
    { item: "Terapia", valor: -80, moeda: 'EUR', tipo: 'Gasto' },
    { item: "Proteína", valor: -15, moeda: 'EUR', tipo: 'Gasto' },
    { item: "Spotify", valor: -32, moeda: 'BRL', tipo: 'Gasto' }, // Valor em reais
    { item: "Bitcoin", valor: -80, moeda: 'BRl', tipo: 'Investimento' },
    { item: "Reserva de Emergência", valor: -450, moeda: 'BRl', tipo: 'Investimento' },
    { item: "Reserva do Carro", valor: -450, moeda: 'BRl', tipo: 'Investimento' },
];

let totalGastos = 0;
let totalInvestimentos = 0;
let totalSalario = 0;

transacoes.forEach(transacao => {
    let valorEmEUR = transacao.moeda === 'BRL'
        ? parseFloat((transacao.valor * taxaCambioBRLparaEUR).toFixed(2))
        : transacao.valor;

    if (transacao.tipo === 'Gasto') {
        totalGastos += valorEmEUR;
    } else if (transacao.tipo === 'Investimento') {
        totalInvestimentos += valorEmEUR;
    } else if (transacao.tipo === 'Salário') {
        totalSalario += valorEmEUR;
    }
});

let totalLiquido = totalSalario + totalGastos + totalInvestimentos;

dv.table(
    ["Descrição", "Valor em EUR", " "],
    transacoes.map(transacao => {
        let valorEmEUR = transacao.moeda === 'BRL'
            ? parseFloat((transacao.valor * taxaCambioBRLparaEUR).toFixed(2))
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

dv.paragraph(`**Total de Gastos:** ${totalGastos.toLocaleString('pt-PT', { style: 'currency', currency: 'EUR' })}`);
dv.paragraph(`**Total de Investimentos:** ${totalInvestimentos.toLocaleString('pt-PT', { style: 'currency', currency: 'EUR' })}`);
dv.paragraph(`**Total Líquido:** ${totalLiquido.toLocaleString('pt-PT', { style: 'currency', currency: 'EUR' })}`);
```



```dataviewjs
// Defina a taxa de câmbio atual de BRL para EUR
const taxaCambioBRLparaEUR = 6; // 1 EUR = 6 BRL

const transacoes = [
    { item: "Salário", valor: 1125, moeda: 'EUR', tipo: 'Salário' },
    { item: "Paitrocínio", valor: 5000, moeda: 'BRL', tipo: 'Salário' },
    { item: "Aluguel", valor: 1500, moeda: 'BRL', tipo: 'Salário' },
    { item: "Renda", valor: -200, moeda: 'EUR', tipo: 'Gasto' },
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
    { item: "Porchat", valor: -25, moeda: 'EUR', tipo: 'Gasto' },
    { item: "Sushi + Bel", valor: -66, moeda: 'EUR', tipo: 'Investimento' },
    { item: "Hospedagem Fátima", valor: -50, moeda: 'EUR', tipo: 'Gasto' },
    { item: "Alimentação Fátima", valor: -65, moeda: 'EUR', tipo: 'Gasto' },
    { item: "Fone", valor: -30, moeda: 'EUR', tipo: 'Investimento' },
    
    
];

let totalGastos = 0;
let totalInvestimentos = 0;
let totalSalario = 0;

transacoes.forEach(transacao => {
    let valorEmEUR = transacao.moeda === 'BRL'
        ? parseFloat((transacao.valor / taxaCambioBRLparaEUR).toFixed(2))
        : transacao.valor;

    if (transacao.tipo === 'Gasto') {
        totalGastos += valorEmEUR;
    } else if (transacao.tipo === 'Investimento') {
        totalInvestimentos += valorEmEUR;
    } else if (transacao.tipo === 'Salário') {
        totalSalario += valorEmEUR;
    }
});

let totalLiquido = totalSalario + totalGastos + totalInvestimentos;

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

dv.paragraph(`**Total de Gastos:** ${totalGastos.toLocaleString('pt-PT', { style: 'currency', currency: 'EUR' })}`);
dv.paragraph(`**Total de Investimentos:** ${totalInvestimentos.toLocaleString('pt-PT', { style: 'currency', currency: 'EUR' })}`);
dv.paragraph(`**Total Líquido:** ${totalLiquido.toLocaleString('pt-PT', { style: 'currency', currency: 'EUR' })}`);
```




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
    { item: "Porchat", valor: -25, moeda: 'EUR', tipo: 'Gasto' },
    { item: "Sushi + Bel", valor: -66, moeda: 'EUR', tipo: 'Investimento' },
    { item: "Hospedagem Fátima", valor: -50, moeda: 'EUR', tipo: 'Gasto' },
    { item: "Alimentação Fátima", valor: -65, moeda: 'EUR', tipo: 'Gasto' },
    { item: "Fone", valor: -30, moeda: 'EUR', tipo: 'Gasto' },
    { item: "SASUC", valor: -10, moeda: 'EUR', tipo: 'Gasto' },
    
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


