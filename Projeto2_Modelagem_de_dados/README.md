# Projeto: Modelagem de Dados — Análise de Vendas (Power BI)

## 📝 Resumo
Este repositório contém a documentação da atividade de modelagem de dados para um projeto de análise de vendas de uma rede de lojas. Os dados vêm de arquivos CSV separados e precisam ser relacionados corretamente no Power BI para garantir análises consistentes e confiáveis.

---

## 📂 Arquivos fornecidos
- **Vendas.csv** — registros de vendas diárias.
  - Colunas: `VendaID`, `DataVenda`, `ProdutoID`, `Quantidade`, `ValorTotal`, `LojaID`, `VendedorID`
- **Metas.csv** — metas trimestrais por vendedor.
  - Colunas: `VendedorID`, `Trimestre`, `Venda`
- **Produto.csv** — catálogo de produtos.
  - Colunas: `ProdutoID`, `NomeProduto`

---

## 🎯 Objetivo
1. Explicar a importância da modelagem de dados no Power BI.
2. Importar os dados e estabelecer relacionamentos corretos.
3. Definir cardinalidades e justificar cada escolha.
4. Identificar tabelas de fato e de dimensão.

---

## 🛠️ Passo a passo
### 1. 🔽 Importação dos dados
- Power BI Desktop → **Obter dados** → **Texto/CSV**
- Importar os 3 arquivos.
- Verificar tipos de dados: datas, números e chaves.

### 2. 🧹 Limpeza no Power Query
- Padronizar nomes das colunas.
- Tratar nulos e duplicados.
- Confirmar formato da `DataVenda`.

### 3. 🔗 Modelagem — Relacionamentos
Relacionamentos criados:
- `Vendas[ProdutoID]` ➝ `Produto[ProdutoID]`
- `Vendas[VendedorID]` ➝ `Metas[VendedorID]`

<img width="797" height="138" alt="image" src="https://github.com/user-attachments/assets/2bc21004-9bb9-444f-bda5-b00d5c4cf4c8" />


#### 📌 Cardinalidade
- **Vendas → Produtos:** Muitos → Um
- **Vendas → Metas:** Muitos → Um

💬 *Justificativa:* Uma venda sempre se relaciona a apenas um produto e um vendedor, enquanto produtos e vendedores podem aparecer repetidas vezes em vendas.

💥 *Impacto de cardinalidades erradas:* valores duplicados, filtros incoerentes, gráficos inconsistentes.

### 4. 🎛️ Direção e comportamento dos relacionamentos
- Direção recomendada: **Dimensão → Fato**
- `Produto` e `Metas` = tabelas de início do filtro.
- `Vendas` = tabela final.
- Relacionamentos principais devem ser **ativos**.

### 5. 🌀 Problemas de ambiguidade
Se houver múltiplos caminhos entre tabelas:
- Criar tabela de datas (`DimData`).
- Desativar relacionamentos duplicados.
- Usar tabelas ponte quando necessário.

---

## 🏗️ Identificação das Tabelas
### 📊 Tabela de Fato
- **Vendas** — contém eventos transacionais (quantidade, valor, datas).

### 📁 Tabelas de Dimensão
- **Produto** — informações descritivas.
- **Metas** — contexto de metas por vendedor e trimestre.

---

## 🌈 Conclusão
A modelagem correta garante análises consistentes, visuais confiáveis e decisões mais seguras dentro do Power BI. 🎯✨

