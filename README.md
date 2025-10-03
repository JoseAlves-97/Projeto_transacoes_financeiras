Projeto Final - SQL 🚀

Descrição
Este projeto consolida transações financeiras (PIX, transferências de entrada e saída) em uma única tabela chamada **`total_transfers`**.  
O objetivo é criar uma visão unificada das transações **concluídas no ano de 2020**, permitindo análises posteriores como:  
- Volume de transações por cliente  
- Valores movimentados por tipo de operação  
- Distribuição mensal das transferências  

Estrutura do Projeto
- **`total_transfers.sql`** → Script responsável pela criação da tabela final consolidada.  
- **`README.md`** → Documentação do projeto.  

Tabelas Utilizadas
O script utiliza dados de diferentes tabelas do projeto **`Projeto_Final`** no BigQuery:

1. **`pix_movements`**
   - Campos principais: `id`, `pix_amount`, `status`, `account_id`, `pix_completed_at`.

2. **`transfer_ins`**
   - Campos principais: `id`, `amount`, `status`, `account_id`, `transaction_completed_at`.

3. **`transfer_outs`**
   - Campos principais: `id`, `amount`, `status`, `account_id`, `transaction_completed_at`.

4. **`accounts`**
   - Relaciona contas com clientes.

5. **`customers`**
   - Informações de clientes (`first_name`, `last_name`).

6. **`time`**
   - Utilizada para obter a data de conclusão.

Lógica Implementada
- União das três fontes de dados (`pix_movements`, `transfer_ins`, `transfer_outs`) via `UNION ALL`.
- Filtro de transações com **status = 'completed'**.  
- Período considerado: **01/01/2020 até 31/12/2020**.  
- Criação de campo **`month`** a partir da data de conclusão.  
- Identificação do tipo de transação:
  - `pix_movements` → conforme `in_or_out`.  
  - `transfer_ins` → `'transfer_ins'`.  
  - `transfer_outs` → `'transfer_outs'`.  

Resultado Esperado
Tabela consolidada **`curso-sql-eba-471019.Projeto_Final.total_transfers`**, com os seguintes campos:

| Coluna           | Descrição                                  |
|------------------|---------------------------------------------|
| transaction_id   | ID da transação                             |
| customer_id      | ID do cliente                               |
| full_name        | Nome completo do cliente                    |
| account_id       | ID da conta                                 |
| amount           | Valor da transação                          |
| status           | Status da transação (`completed`)           |
| type_transaction | Tipo da transação (`pix`, `transfer_ins`, `transfer_outs`) |
| date_completed   | Data da conclusão da transação              |
| month            | Mês de referência (extraído da data)        |

---

## 🚀 Como Usar
1. Abra o **BigQuery**.  
2. Copie o conteúdo de `total_transfers.sql`.  
3. Execute o script para criar/atualizar a tabela **`total_transfers`**.  

---

👨‍💻 Autor: Jose Alves Pedrosa Filho 
📅 Projeto desenvolvido como exercício final do curso de SQL EBA Analista 
