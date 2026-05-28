# 🔩 Cassandra Car Parts

Atividade avaliativa da disciplina **S202 - Banco de Dados II** do Inatel, explorando a integração entre **Python e Apache Cassandra** — um banco de dados NoSQL orientado a colunas — através de um sistema de estoque de peças automotivas.

## 📖 Contexto

Um fabricante de automóveis precisa de um sistema de banco de dados distribuído para suas linhas de montagem. Cada máquina da linha deve ser capaz de consultar o estoque e localizar as peças corretas para cada modelo de veículo.

O projeto explora os fundamentos do **CQL (Cassandra Query Language)**, a modelagem de dados orientada a consultas — característica central do Cassandra — e as diferenças práticas em relação a bancos relacionais tradicionais.

## 🛠️ Tecnologias

- Python 3.11
- [Apache Cassandra](https://cassandra.apache.org/) via [DataStax Astra](https://www.datastax.com/products/datastax-astra) (cloud)
- `cassandra-driver` para conexão Python ↔ Cassandra
- `pytest` para testes automatizados

> ⚠️ O banco é limpo automaticamente a cada nova conexão (`clean_database()`). Comente essa chamada em `get_session()` se quiser preservar os dados entre execuções.

## 📋 Questões

| # | Função | Descrição | Pontos |
|---|--------|-----------|--------|
| 1 | `create_table()` | Cria a tabela `parts` no Cassandra | 5 |
| 2 | `add_part()` | Insere uma peça no estoque | 5 |
| 3 | `get_shelf_parts()` | Busca nome, modelo e quantidade das peças de uma estante | 5 |
| 4 ⭐ | `get_car_parts()` | Busca peças de um determinado modelo de carro | 5 |
| 5 ⭐ | `get_shelves_stats()` | Retorna estatísticas (min, max, média) por estante | 5 |

## 🗂️ Modelagem

A tabela `parts` é modelada com `shelf` como **partition key**, o que permite consultas eficientes por estante sem `ALLOW FILTERING`:

```cql
CREATE TABLE parts (
    id INT,
    name TEXT,
    car_model TEXT,
    shelf INT,
    level INT,
    amount INT,
    PRIMARY KEY (shelf, level, id)
);
```

> 💡 No Cassandra, a modelagem é orientada às consultas — diferente do modelo relacional, onde se modela os dados e as queries se adaptam.
