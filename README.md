# aliare-desafio-02

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
