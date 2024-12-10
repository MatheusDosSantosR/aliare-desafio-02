# aliare-desafio-02

Para as consultas, em sql foi realizado os testes no site oneCompiler criando as tabelas adicionado valores e realizando as consultas para acessar clique [aqui](https://onecompiler.com/sqlserver/432p65vut)

## 1 - Elaboração dos casos de testes referentes aos requisitos especificados no anexo Documento de Requisitos.pdf

- Os casos de testes foram criados seguindo:
  - Pré-condição: Ações necessarias antes de realizar o testes, como configurações, login, etc...
  - Passos: Passos necessarios para realização do teste.
  - Resultado esperado: Resultado esperado ao concluir a pre-confição e passos.

### **Casos de Teste para [FA01] – Previsão de Entrega no Pedido de Venda (Fatu2022)**

#### Caso de Teste 1: Verificar exibição correta da data de previsão de entrega

- **Pré-condição**: A tela Fatu2022A deve estar acessível no módulo "Vendas e Faturamento".
- **Passos**:
  1. Acesse a tela Fatu2022A.
  2. Visualize a data de previsão de entrega.
- **Resultado Esperado**: A data de previsão de entrega deve ser exibida conforme o registro no banco de dados.

### Caso de Teste 2: Garantir que previsão "NÃO VALIDA" não é enviada à central

- **Pré-condição**: Configuração do campo "Confirmação da Previsão" como "NÃO VALIDA".
- **Passos**:
  1. Crie ou edite um pedido na tela Fatu2022A.
  2. Configure a previsão de entrega como "NÃO VALIDA".
  3. Envie o pedido.
- **Resultado Esperado**: A previsão de entrega não deve aparecer na central de pedidos.

---

### **Casos de Teste para [MD01] – Fatu2022A - Manutenção dos Itens do Pedido de Venda**

#### Caso de Teste 3: Validar inclusão do campo "Confirmação da Previsão"

- **Pré-condição**: A tela Fatu2022A deve estar funcional.
- **Passos**:
  1. Acesse a tela Fatu2022A.
  2. Verifique as opções disponíveis no campo "Confirmação da Previsão".
- **Resultado Esperado**: O campo deve exibir as opções: Vazio, NÃO VALIDA, PENDENTE, CONFIRMADO. "Vazio" deve ser o padrão.

#### Caso de Teste 4: Garantir que o rateio de 100% é levado para a central

- **Pré-condição**: Pedido com "Rateio de 100%".
- **Passos**:
  1. Acesse a tela Fatu2022A.
  2. Configure a previsão de entrega como "CONFIRMADO".
  3. Salve e envie o pedido.
- **Resultado Esperado**: O pedido deve aparecer na central com rateio de 100%.

---

### **Casos de Teste para [MD02] – Tela Previsão de Entrega**

#### Caso de Teste 5: Validar bloqueio de duplicação de data de previsão de entrega

- **Pré-condição**: Um pedido com uma data de previsão já registrada.
- **Passos**:
  1. Tente inserir a mesma data de previsão de entrega novamente.
- **Resultado Esperado**: O sistema deve bloquear a duplicação da data.

#### Caso de Teste 6: Validar obrigatoriedade do rateio total da quantidade

- **Pré-condição**: Pedido com quantidade de itens maior que 1.
- **Passos**:
  1. Tente salvar o pedido sem realizar o rateio completo.
- **Resultado Esperado**: O sistema deve exibir mensagem de erro solicitando o rateio total.

## 2 - Considerando o anexo Modelo Entidade Relacionamento.png devem ser desenvolvidas instruções SQL capazes de

### Consulta de parceiros de negócio

1. Consultas de parceiros de negócio:

    ```sql
    SELECT razao_social
        FROM parceiro
        WHERE ativo = 1;
    ```

2. Identificar o CEP, endereço e complemento de todas as propriedades do parceiro cuja razão social é 'PARCEIRO - AVALIAÇÃO ANALISTA DE TESTES':

    ```sql
    SELECT cep, endereco, complemento
        FROM propriedade
        WHERE parceiro_id = (
            SELECT id
            FROM parceiro
            WHERE razao_social = 'PARCEIRO - AVALIAÇÃO ANALISTA DE TESTES'
        );
    ```

### Consulta de pedidos

1. Identificar o número de todos os pedidos de venda da série '1' e a razão social do seu parceiro é 'PARCEIRO - AVALIAÇÃO ANALISTA DE TESTES':

   ```SQL
    SELECT pv.numero
        FROM pedido_venda pv
        JOIN parceiro p ON pv.parceiro_id = p.id
        WHERE pv.serie = 1 AND p.razao_social = 'PARCEIRO - AVALIAÇÃO ANALISTA DE TESTES';
   ```

2. Identificar todos os campos dos pedidos de venda do parceiro cuja razão social é 'PARCEIRO - AVALIAÇÃO ANALISTA DE TESTES':

    ```sql
    SELECT pv.*
        FROM pedido_venda pv
        JOIN parceiro p ON pv.parceiro_id = p.id
        WHERE p.razao_social = 'PARCEIRO - AVALIAÇÃO ANALISTA DE TESTES';
    ```

3. Identificar todos os pedidos de venda que foram criados entre as datas '01/11/2020' e '30/11/2020' cuja razão social do parceiro é 'PARCEIRO - AVALIAÇÃO ANALISTA DE TESTES':

    ```sql
    SELECT pv.*
        FROM pedido_venda pv
        JOIN parceiro p ON pv.parceiro_id = p.id
        WHERE p.razao_social = 'PARCEIRO - AVALIAÇÃO ANALISTA DE TESTES'
            AND pv.data_cadastro BETWEEN '2020-11-01' AND '2020-11-30';
    ```

4. Identificar todos os pedidos de venda que foram criados entre as datas '01/11/2020' e '30/11/2020' cuja razão social do parceiro é 'PARCEIRO - AVALIAÇÃO ANALISTA DE TESTES', e a cidade de sua propriedade é 'GOIÂNIA'. Os resultados devem ser ordenados de forma decrescente a partir da data de cadastro do pedido:

    ```sql
    SELECT pv.*
        FROM pedido_venda pv
        JOIN parceiro p ON pv.parceiro_id = p.id
        JOIN propriedade pr ON pr.parceiro_id = p.id
        JOIN cidade c ON pr.cidade_id = c.id
        WHERE p.razao_social = 'PARCEIRO - AVALIAÇÃO ANALISTA DE TESTES'
            AND c.nome = 'GOIÂNIA'
            AND pv.data_cadastro BETWEEN '2020-11-01' AND '2020-11-30'
        ORDER BY pv.data_cadastro DESC;
    ```
