# Tech Challenge Fase 1 — Case NPS Preditivo

**FIAP PosTech | Ciência de Dados e Inteligência Artificial**

---

## Objetivo do Projeto

Uma empresa de e-commerce enfrenta alta variabilidade no NPS (Net Promoter Score) entre diferentes perfis de clientes. Como o NPS é coletado apenas após o encerramento da jornada de compra, a empresa não consegue agir preventivamente sobre clientes em risco de insatisfação.

O objetivo deste projeto é **identificar, a partir de dados operacionais, quais fatores influenciam a satisfação do cliente e propor uma estratégia preditiva** capaz de antecipar problemas antes da pesquisa de NPS ser aplicada — permitindo intervenções proativas como contato do atendimento, compensações ou pesquisas antecipadas.

O projeto cobre três frentes:

1. **Entendimento do negócio** — contexto, importância do NPS e áreas beneficiadas
2. **Definição da variável alvo** — escolha e justificativa do target preditivo
3. **Análise Exploratória dos Dados (EDA)** — identificação dos principais drivers de (in)satisfação

---

## Descrição da Base de Dados

**Arquivo:** `data/desafio_nps_fase_1.csv`
**Registros:** 2.500 | **Colunas:** 19 | **Valores ausentes:** nenhum | **Duplicatas:** nenhuma

### Dicionário de Dados

| Coluna | Tipo | Descrição |
|---|---|---|
| `customer_id` | int | Identificador único do cliente |
| `order_id` | int | Identificador único do pedido |
| `customer_age` | int | Idade do cliente |
| `customer_region` | str | Região geográfica (Sul, Sudeste, Norte, Nordeste, Centro-Oeste) |
| `customer_tenure_months` | int | Tempo de relacionamento com a empresa (meses) |
| `order_value` | float | Valor total do pedido (R$) |
| `items_quantity` | int | Quantidade de itens no pedido |
| `discount_value` | float | Valor de desconto aplicado (R$) |
| `payment_installments` | int | Número de parcelas do pagamento |
| `delivery_time_days` | int | Tempo total de entrega (dias) |
| `delivery_delay_days` | int | Dias de atraso em relação ao prazo prometido |
| `freight_value` | float | Valor do frete (R$) |
| `delivery_attempts` | int | Número de tentativas de entrega |
| `customer_service_contacts` | int | Número de contatos com o atendimento |
| `resolution_time_days` | int | Tempo para resolução do problema (dias) |
| `nps_score` | float | Nota de satisfação do cliente (0–10) — **variável alvo** |
| `repeat_purchase_30d` | int | Recompra em 30 dias (0 = não, 1 = sim) |
| `complaints_count` | int | Número de reclamações registradas |
| `csat_internal_score` | float | Score interno de satisfação (0–10) |

---

## Metodologia

### 1. Análise Exploratória (EDA)

- Distribuição do NPS e composição por categoria (Detrator / Passivo / Promotor)
- Análise logística: impacto de atraso, prazo e tentativas de entrega
- Análise de atendimento: contatos, reclamações e tempo de resolução
- Perfil do cliente: faixa etária, tempo de relacionamento e recompra
- Matriz de correlação de Pearson entre todas as variáveis numéricas
- Identificação de pontos de ruptura operacionais
- Análise do CSAT interno e sua relação com o NPS

**Principais achados:**

| Variável | Correlação com NPS | Relevância |
|---|---|---|
| `delivery_delay_days` | r = −0,60 | Alta — driver mais forte |
| `complaints_count` | r = −0,50 | Alta |
| `customer_service_contacts` | r = −0,35 | Moderada |
| `resolution_time_days` | r = −0,19 | Moderada |
| `delivery_time_days` | r ≈ 0,00 | Nenhuma |
| `delivery_attempts` | r = +0,03 | Nenhuma |

> **Achado crítico:** O grande motivador encontrado para baixo NPS é o atraso nas entregas, porém o NPS está abaixo de 7 mesmo em pedidos com zero dias de atraso e zero contatos com atendimento — indicando um problema estrutural que vai além de falhas operacionais pontuais.

---

## Como Reproduzir os Resultados

### Pré-requisitos

Python 3.8+ com as seguintes bibliotecas:

```
pandas
numpy
matplotlib
seaborn
scipy
```

Instalação:

```bash
pip install pandas numpy matplotlib seaborn scipy scikit-learn
```

### Estrutura de Arquivos

```
TechChallenge_1/
├── data/
│   └── desafio_nps_fase_1.csv
├── notebooks/
│   └── TechChallenge_1.ipynb
└── README.md
```

### Execução

1. Clone ou baixe o repositório
2. Certifique-se de que o arquivo `desafio_nps_fase_1.csv` está em `data/`
3. Abra o notebook em `notebooks/TechChallenge_1.ipynb`
4. Execute todas as células em ordem (Kernel > Restart & Run All)

O notebook lê o CSV com caminho relativo `'../data/desafio_nps_fase_1.csv'` — **não é necessário nenhuma configuração adicional**, desde que a estrutura de pastas acima seja mantida.

---

*FIAP PosTech — Ciência de Dados e Inteligência Artificial | Fase 1*
