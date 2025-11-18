# ✈️ Modelagem de Dados em Power BI: Análise de Viagens

## 📄 Visão Geral do Projeto

Este projeto é uma **atividade prática** do curso de **Power BI da EBAC** (Escola Britânica de Artes Criativas e Tecnologia).

Ele demonstra a importância da **Modelagem de Dados** no **Power BI** para garantir a integridade, a confiabilidade e o desempenho otimizado em análises de negócios. Utilizaremos dados transacionais (viagens) e dados descritivos (clientes, aeroportos, destinos) para construir um modelo **esquema *Star*** (Estrela), que é ideal para *Business Intelligence* (BI).

O cenário foca na análise de **viagens**, conectando clientes, aeroportos de origem e destino, e informações detalhadas sobre as transações.

---

## 💾 Conjuntos de Dados

Quatro arquivos CSV foram fornecidos para a atividade:

| Arquivo | Descrição | Colunas-Chave Principais | Tipo de Tabela |
| :--- | :--- | :--- | :--- |
| `airport.csv` | Lista de Aeroportos. | `airport_id` | Dimensão |
| `client.csv` | Lista de Clientes. | `id` | Dimensão |
| `destination.csv` | Destinos populares e informações adicionais. | `travel_id` | Dimensão |
| `travel.csv` | Dados das viagens compradas (Transações). | `travel_id` | Fato |

---

## 🚀 Passo a Passo da Atividade

### 1. Contextualização e Importância da Modelagem de Dados

* **Explicação:** A modelagem de dados é fundamental, pois define como as tabelas se conectam e como os dados devem ser agregados e filtrados.
* **Benefícios:** Uma boa modelagem, como a estrutura *Star Schema*, **otimiza o desempenho** (consultas mais rápidas), **melhora a confiabilidade** (cálculos corretos e sem duplicação) e **evita erros interpretativos**.
* **Cenário:** Conectar a **tabela Fato (Viagens)** com as **tabelas Dimensão (Clientes, Aeroportos)** permite análises cruzadas precisas, como o *Total Price* (Fato) pelo *Gender* (Dimensão Cliente).

---

### 2. Carregamento e Estabelecimento dos Relacionamentos

Após importar os arquivos CSV, os relacionamentos devem ser criados na *Visualização de Modelo* do Power BI.

**Modelo de Relacionamento (Esquema Estrela):**


* **Viagens $\leftrightarrow$ Clientes:**
    * Chaves: `travel.client_id` **$\rightarrow$** `client.id`
* **Viagens $\leftrightarrow$ Aeroportos (Origem):**
    * Chaves: `travel.airport_origin` **$\rightarrow$** `airport.airport_id`
* **Viagens $\leftrightarrow$ Aeroportos (Destino):**
    * Chaves: `travel.airport_destination` **$\rightarrow$** `airport.airport_id`
    * *Nota: O relacionamento de Destino será criado, mas mantido **Inativo** para evitar ambiguidade (caminhos múltiplos).*
* **Viagens $\leftrightarrow$ Destinos Populares (Opcional):**
    * Chaves: `travel.travel_id` **$\rightarrow$** `destination.travel_id`

---

### 3. Definição das Cardinalidades e Direção

A cardinalidade correta é crucial para a precisão dos cálculos.

<img width="693" height="144" alt="image" src="https://github.com/user-attachments/assets/1f6c51ab-8107-4720-a52b-fd8af685fe60" />
---
### 4. Gerenciamento dos Relacionamentos e Identificação de Tabelas

<img width="701" height="217" alt="image" src="https://github.com/user-attachments/assets/0fd98bd8-b885-46fb-9fce-4650d51619dd" />

## 4.1 Configurações de Relacionamento
Resolução de Ambiguidade (Aeroportos):
* A tabela airport será usada para Origem e Destino.
* O relacionamento airport $\leftrightarrow$ travel para Origem deve estar Ativo.
* O relacionamento airport $\leftrightarrow$ travel para Destino deve ser criado, mas Inativo.
* Para analisar o destino, será necessário usar a função USERELATIONSHIP no DAX.
Chaves: Garanta que as colunas de chave primária (airport_id, id) estejam conectadas às chaves estrangeiras (airport_origin, client_id).

