# CRM_Insight

## Tabelas e Relacionamentos

O banco de dados consiste em três tabelas principais:

1. **UDR_CRM_CAMPANHAS**: Armazena informações sobre campanhas de marketing.
   - `CAMPANHA_ID` (NUMBER): Chave primária que identifica exclusivamente cada campanha.
   - `NOME` (VARCHAR2): Nome da campanha.
   - `DATA_INICIO` (DATE): Data de início da campanha.
   - `DATA_FIM` (DATE): Data de término da campanha.
   - `ORCAMENTO` (NUMBER): Orçamento alocado para a campanha.

2. **UDR_CRM_CLIENTES**: Armazena informações sobre clientes.
   - `CLIENTE_ID` (NUMBER): Chave primária que identifica exclusivamente cada cliente.
   - `NOME` (VARCHAR2): Nome do cliente.
   - `EMAIL` (VARCHAR2): Endereço de e-mail do cliente.
   - `TELEFONE` (VARCHAR2): Número de telefone do cliente.
   - `DATA_CADASTRO` (DATE): Data em que o cliente foi cadastrado.

3. **UDR_CRM_INTERACOES**: Armazena informações sobre as interações dos clientes com as campanhas.
   - `INTERACAO_ID` (NUMBER): Chave primária que identifica exclusivamente cada interação.
   - `CLIENTE_ID` (NUMBER): Chave estrangeira que referencia a tabela UDR_CRM_CLIENTES.
   - `CAMPANHA_ID` (NUMBER): Chave estrangeira que referencia a tabela UDR_CRM_CAMPANHAS.
   - `DATA_INTERACAO` (DATE): Data em que a interação ocorreu.
   - `TIPO` (VARCHAR2): Tipo de interação (ex.: 'Visualização', 'Clique', 'Compra').
   - `METRICA` (VARCHAR2): Métrica associada à interação (ex.: 'Tempo na Página', 'Taxa de Cliques', 'Receita').
   - `VALOR` (NUMBER): Valor da métrica.

A tabela UDR_CRM_INTERACOES possui duas chaves estrangeiras:
- `CLIENTE_ID` referencia a tabela UDR_CRM_CLIENTES, indicando qual cliente está associado a cada interação.
- `CAMPANHA_ID` referencia a tabela UDR_CRM_CAMPANHAS, indicando a qual campanha cada interação pertence.

## Objetivo do Banco de Dados

O objetivo do banco de dados CRM_Insight é fornecer uma estrutura para armazenar e analisar dados sobre campanhas de marketing, clientes e suas interações. Ele permite:

- Acompanhar campanhas de marketing, incluindo seus nomes, datas e orçamentos.
- Armazenar informações sobre clientes, como nomes, detalhes de contato e datas de cadastro.
- Registrar interações dos clientes com campanhas, incluindo o tipo de interação, métricas e valores associados.

Ao centralizar esses dados, o CRM_Insight permite análises para entender melhor o comportamento do cliente, medir a eficácia da campanha e tomar decisões baseadas em dados para otimizar os esforços de marketing.

## Executando os Scripts SQL

Para configurar e popular o banco de dados CRM_Insight, você precisará executar dois scripts SQL:

1. **estrutura.sql**: Este script cria as tabelas e restrições necessárias. Para executá-lo no SQL*Plus, use:

```bash
SQL> @/caminho/para/estrutura.sql
```

Para executar no SQL Developer, abra o arquivo e clique no botão "Executar Script".

2. **dados.sql**: Este script insere dados de amostra nas tabelas. Para executá-lo no SQL*Plus, use:

```bash
SQL> @/caminho/para/dados.sql
```

Após executar esses scripts, você pode consultar as tabelas para verificar se os dados foram inseridos corretamente:

```sql
SELECT * FROM UDR_CRM_CAMPANHAS;
SELECT * FROM UDR_CRM_CLIENTES;
SELECT * FROM UDR_CRM_INTERACOES;
```

## Executando Consultas

Após executar os scripts `estrutura.sql` e `dados.sql`, você pode executar consultas para analisar os dados. Por exemplo:

```sql
SELECT c.nome AS cliente, ca.nome AS campanha, i.tipo, i.metrica, i.valor
FROM UDR_CRM_INTERACOES i
JOIN UDR_CRM_CLIENTES c ON i.cliente_id = c.cliente_id
JOIN UDR_CRM_CAMPANHAS ca ON i.campanha_id = ca.campanha_id;
```

Isso mostrará as interações com os nomes dos clientes e campanhas relacionados, como mostrado na captura de tela abaixo:

![Resultado da Consulta](/crm_insight_screenshot.png)

## Membros
- Nikolas Santana: 180632
- Julia Santos Souza: 180442
