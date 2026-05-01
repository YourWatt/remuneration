# 💰 Calculadora de Remuneração — YourWatt

Ferramenta interna de simulação de remuneração para os sócios **Gabriel** e **Matheus**, com suporte a múltiplos regimes tributários, bônus por indicação de leads e participação de lucros.

## 🔗 Acesso

**[yourwatt.github.io/remuneration](https://yourwatt.github.io/remuneration)**

---

## 📋 Modos de uso

### 🎯 Meta de Gabriel
Informe a **meta mensal de remuneração** de Gabriel e a calculadora determina o faturamento necessário para atingi-la em cada regime tributário. Útil para planejamento e definição de metas comerciais.

### 📋 Faturamento Real por Projeto
Cadastre os **projetos do mês individualmente**, com valor e o sócio que trouxe o lead. A calculadora distribui automaticamente os pools, bônus e lucros com base no faturamento real.

---

## ⚙️ Parâmetros configuráveis

| Parâmetro | Descrição |
|-----------|-----------|
| **Meta de Gabriel** | Remuneração líquida mensal desejada (modo Meta) |
| **% bônus por indicação** | Percentual do valor do projeto pago ao sócio que trouxe o lead |
| **Pool de funcionários** | % do faturamento destinado ao pool de remuneração variável |
| **Prêmio CEO / CTO / CFO** | % do pool reservado ao prêmio executivo de Matheus |
| **Total de lucros** | % do faturamento distribuído como participação de lucros (dividendos) |
| **Número de sócios** | Divisor igualitário para a participação de lucros |

---

## 🧮 Lógica de cálculo

### Pool de funcionários
```
Pool total = poolPct × faturamento
Pool executivo = (CEO% + CTO% + CFO%) × pool total       → Matheus
Pool de projeto = restante do pool total
  └─ Gabriel:  85,5% do pool de projeto
  └─ Matheus:  14,5% do pool de projeto
```

### Regimes tributários de Gabriel
| Regime | Encargo | Observação |
|--------|---------|------------|
| **Pro-labore** | 11% patronal + 11% INSS pessoal | Regime padrão de sócio |
| **PJ · MEI** | DAS 1,5% | Limite de faturamento MEI aplica-se |
| **PJ · Simples AN. III** | ~6% efetivo | Para operações acima do teto MEI |

### Regime de Matheus (modo Faturamento Real)
| Regime | Cálculo |
|--------|---------|
| **Pro-labore** | custo ÷ 1,11 = bruto → bruto × 0,89 = líquido |
| **PJ AN.III** | custo × 0,94 = líquido (sem encargos patronais) |

### Bônus por indicação de lead
No modo Faturamento Real, cada projeto tem um responsável pelo lead. O bônus (`% × valor do projeto`) é calculado individualmente por projeto e pago ao sócio indicador — com dedução conforme seu regime de recebimento (Pro-labore ou PJ AN.III). MEI disponível apenas para Gabriel.

### Participação de lucros
```
Total lucros = lucroPct × faturamento
Por sócio   = total lucros ÷ nSócios
```
Distribuído igualmente entre os 6 sócios (incluindo Lucas). Isento de INSS e IRPF como dividendo.

---

## 👥 Sócios

| Sócio | Papel | Remuneração variável |
|-------|-------|---------------------|
| **Gabriel** | Engenheiro / Comercial | Pool de projeto (85,5%) + bônus leads + lucros |
| **Matheus** | CEO · CTO · CFO / Adm | Pool executivo + projeto (14,5%) + lucros |
| **Renio** | Comercial B2B | Bônus leads (se aplicável) + lucros |
| **Rodrigo** | Comercial | Bônus leads (se aplicável) + lucros |
| **Aquiles** | Comercial | Bônus leads (se aplicável) + lucros |
| **Lucas** | Sócio | Lucros |

---

## 🗂️ Estrutura do repositório

```
remuneration/
└── index.html   # Calculadora completa (HTML/CSS/JS — single file)
└── README.md    # Este arquivo
```

A calculadora é um **single-file app** sem dependências externas — funciona diretamente no browser sem servidor.

---

*YourWatt Energia Solar · Uso interno*
