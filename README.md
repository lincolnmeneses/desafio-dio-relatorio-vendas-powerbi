# 📊 Relatório de Vendas Elegante com Power BI

Desafio de projeto da trilha **Primeiros Passos em Power BI** (DIO): criar um relatório de vendas mais elaborado, com base na amostra **Financial Sample** da Microsoft.

Base de dados fornecida pela especialista: [julianazanelatto/power_bi_analyst](https://github.com/julianazanelatto/power_bi_analyst) (`Módulo 2/Desafio de Projeto/Financial Sample.xlsx`).

---

## 🎯 O que o desafio pedia e como foi atendido

| Requisito do desafio | Como foi implementado |
| --- | --- |
| Estrutura definida | Layout fixo em 1280×720 com barra lateral de navegação, cabeçalho com título e filtros, linha de cartões (KPIs) e área de gráficos em painéis brancos com cantos arredondados |
| Botões de navegação | Menu lateral **Vendas / Lucro**, seta de próxima página / voltar e logo da DIO clicável que volta para a página inicial |
| Segmentadores e botões com imagem associada | Segmentadores de **Período**, **Segmento**, **Ano** e **País**, e um botão **Limpar filtros** com a imagem de uma borracha |
| Indicadores e botões para alternar visuais sobre o mesmo assunto | Botões **Barras / Rosca** (Vendas por Segmento) e **Treemap / Barras** (Vendas por País), cada um ligado a um indicador |
| Segunda página do relatório | Página **Análise de Lucro**, com árvore de decomposição, gráfico de cascata e análises de lucro por produto e segmento |
| Publicação no Power BI Service | Ver a seção [Publicação](#-publicação-no-power-bi-service) |

---

## 🗂️ Páginas do relatório

### 1. Visão de Vendas
- **Cartões:** Total de Vendas, Lucro Total, Margem de Lucro, Unidades Vendidas e Total de Descontos
- **Gráfico de área:** evolução mensal de Vendas e Lucro
- **Vendas por Segmento:** barras ↔ rosca (alternados por indicadores)
- **Vendas por Produto:** colunas
- **Vendas por País:** treemap ↔ barras (alternados por indicadores)
- **Filtros:** Período (intervalo de datas) e Segmento

### 2. Análise de Lucro
- **Cartões:** Lucro Total, Margem de Lucro, Custo dos Produtos (COGS) e % de Desconto
- **Árvore de decomposição:** lucro detalhado por Ano → País → Segmento → Produto
- **Gráfico de cascata:** variação do lucro por trimestre
- **Lucro por Produto** (barras) e **Lucro por Segmento** (rosca)
- **Filtros:** Ano (botões) e País

---

## 🧱 Modelo de dados

```
dCalendario (1) ──────< (*) financials
Medidas (tabela só de medidas)
```

- **financials**: tabela fato importada do Excel. No Power Query, os tipos de dados foram ajustados e a coluna `" Sales"` (que vem com um espaço no início) foi renomeada para `Sales`.
- **dCalendario**: tabela de datas criada no Power Query a partir da menor e da maior data de vendas, com Ano, Mês, Trimestre, "Ano Trimestre" e "Mês Ano" (ordenada corretamente). Está marcada como tabela de datas.
- **Medidas**: tabela dedicada às medidas DAX, que deixa o painel de campos organizado.

### Medidas DAX

```DAX
Total Vendas      = SUM ( financials[Sales] )
Vendas Brutas     = SUM ( financials[Gross Sales] )
Total Descontos   = SUM ( financials[Discounts] )
% Desconto        = DIVIDE ( [Total Descontos], [Vendas Brutas] )
Unidades Vendidas = SUM ( financials[Units Sold] )
Custo (COGS)      = SUM ( financials[COGS] )
Lucro Total       = SUM ( financials[Profit] )
Margem de Lucro   = DIVIDE ( [Lucro Total], [Total Vendas] )
```

---

## 📁 Estrutura do repositório

```
├── dados/
│   └── Financial Sample.xlsx           # base de dados do desafio
├── RelatorioVendas.pbip                # abre o projeto no Power BI Desktop
├── RelatorioVendas.Report/             # definição do relatório (páginas, visuais, indicadores, imagens)
└── RelatorioVendas.SemanticModel/      # modelo de dados em TMDL (tabelas, Power Query, medidas, relacionamentos)
```

O projeto está salvo no formato **Power BI Project (.pbip)**, que guarda o relatório e o modelo como arquivos de texto. Assim dá para versionar no GitHub e ver cada alteração.

## ▶️ Como abrir

1. Instale o [Power BI Desktop](https://powerbi.microsoft.com/desktop/).
2. Abra o arquivo `RelatorioVendas.pbip`.
3. Clique em **Página Inicial → Atualizar** para carregar os dados.
4. Se você clonou o repositório em outra pasta, ajuste o parâmetro **CaminhoArquivo** em **Transformar dados → Editar parâmetros** para o caminho do arquivo `dados/Financial Sample.xlsx` no seu computador.

> Dica: no Power BI Desktop, use **Ctrl + clique** nos botões para testá-los no modo de edição.

## ☁️ Publicação no Power BI Service

Relatório publicado em: _adicione aqui o link do relatório no Power BI Service_

---

## 🛠️ Tecnologias
- Power BI Desktop (Power Query, DAX, indicadores e botões)
- Power BI Service
- Git e GitHub
