# 📊 Projeto de Análise de Viagens — Power BI

Este projeto tem como objetivo analisar dados de viagens utilizando o Power BI, aplicando boas práticas de modelagem de dados, relacionamento entre tabelas e criação de métricas e visualizações que permitam entender o comportamento dos clientes, aeroportos e destinos.

---

## 🚀 Objetivo do Projeto

O propósito principal é transformar uma base de dados bruta (Mockaroo) em um modelo analítico consistente, permitindo:

- Análises claras sobre viagens, clientes e aeroportos.  
- Métricas de desempenho confiáveis.  
- Visualizações intuitivas e estruturadas.  
- Um modelo de dados robusto e escalável.

---

## 🧩 Conjuntos de Dados Utilizados

Os arquivos utilizados foram gerados no **Mockaroo** e importados para o Power BI:

### **1. airport.csv**  
Contém a lista de aeroportos:  
- airport_id  
- airport_name  
- airport_city  
- airport_country  
- latitude  
- longitude  

### **2. client.csv**  
Lista de clientes:  
- id  
- client_name  
- gender  
- city  
- country  

### **3. destination.csv**  
Lista de destinos populares:  
- travel_id  
- airport  
- cat
### **4. travel.csv**  
Dados das viagens realizadas:  
- travel_id  
- airport_origin  
- airport_destination  
- purchase_date  
- travel_date  
- payment_method  
- total_price  
- currency_name  
- client_id  

---

## 🛠️ Como Replicar o Projeto

### **1️⃣ Faça o download dos arquivos .csv**

Coloque todos os arquivos em uma mesma pasta:  
* airport.csv
* client.csv
* destination.csv
* travel.csv


### **2️⃣ Abra o Power BI Desktop**  
Vá em:  
**Página Inicial → Obter Dados → Texto/CSV**

Importe cada um dos arquivos.

### **3️⃣ Organize e nomeie as tabelas**  
Recomenda-se manter os nomes:  
- *Aeroportos*  
- *Clientes*  
- *Destinos*  
- *Viagens*  

### **4️⃣ Configure os relacionamentos**  
Após carregar tudo, abra **Modelagem → Exibição de Modelo** para montar o diagrama conforme descrito abaixo.

---

## 🧱 Modelagem de Dados

A modelagem segue o padrão **estrela (Star Schema)**, garantindo clareza, performance e consistência nas análises.

### **🔹 Tabela Fato**

**Fato_Viagens**  
Contém todos os eventos das viagens realizadas (transações).

### **🔸 Tabelas Dimensão**

- **Dim_Clientes**  
- **Dim_Aeroportos**  
- **Dim_Destinos**  

---

## 🔗 Relacionamentos Criados

### ✔ Viagens → Clientes  
**Muitos para Um**  
Chave: `client_id`  
> Um cliente pode fazer várias viagens.

### ✔ Viagens → Aeroportos (Origem e Destino)  
**Muitos para Um**  
Chave: `airport_id`  
> Várias viagens podem partir/chegar ao mesmo aeroporto.

### ✔ Aeroportos → Destinos (Opcional)  
**Muitos para Um**  
Chave: Cidade/País (dependendo da granularidade)  
> Relacionamento auxiliar para análises geográficas.

---

## ⚠️ Importância da Cardinalidade Correta

Cardinalidades erradas podem causar:

- **Duplicação de valores**  
- **Filtros comportando-se incorretamente**  
- **Medidas com cálculos distorcidos**  
- **Resultados inconsistentes nos dashboards**

A configuração correta garante:

- Propagação adequada de filtros  
- Relações claras entre entidades  
- Desempenho superior no Power BI  

---

## 📏 Métricas Criadas

As principais métricas desenvolvidas incluem:

- **Total de Viagens**  
```DAX
Total Viagens = COUNT(Fato_Viagens[travel_id])
```
* Total de Receita
```DAX
Receita Total = SUM(Fato_Viagens[total_price])
```
* Ticket Médio
```DAX
Ticket Médio = DIVIDE([Receita Total], [Total Viagens])
```

* Qtd. Clientes Ativos
```DAX
Clientes Ativos = DISTINCTCOUNT(Fato_Viagens[client_id])
```

* Viagens por Origem/Destino
```DAX
Viagens por Origem = COUNT(Fato_Viagens[airport_origin])
```
## 🔍 Principais Insights Obtidos

- Identificação dos aeroportos mais movimentados (origem e destino).

- Análise do comportamento de compra dos clientes: datas, métodos de pagamento, sazonalidade.

- Mapa com concentração geográfica dos aeroportos.

- Categorias e destinos mais buscados no dataset.

- Impacto da modelagem no desempenho e precisão das análises.

## 📁 Estrutura do Repositório

Projeto-Analise_de_Viagens/
│
├── dataset/
│   ├── airport.csv
│   ├── client.csv
│   ├── destination.csv
│   └── travel.csv
│
├── modelo_de_dados.png   # Captura do diagrama
├── dashboard.png         # Print do relatório
└── Projeto_Analise_Viagens.pbix
