# Desafio-Processamento-de-Pagamento
Link da API de Validaçäo: https://github.com/Viniciusalves16/PrePaymentAPI ✅

Link da API de Pagamento: https://github.com/Viniciusalves16/PagFlow ✅

Link da API de Enivo Notificaçao: https://github.com/Viniciusalves16/NotificationDispatcher ✅


![desenho desafio](https://github.com/user-attachments/assets/6c906037-d48b-4854-a541-6869befe98a4)      

Requisitos Funcionais:

Cadastro de Pagamento:
O cliente pode realizar um pagamento utilizando diferentes métodos (cartão de crédito, boleto bancário, transferência, etc.).
A API deve validar a entrada de dados do pagamento, como o valor, o método de pagamento e as informações do cliente.


Cadastro de Pagamento:
O cliente pode realizar um pagamento utilizando diferentes métodos (cartão de crédito, boleto bancário, transferência, etc.).
A API deve validar a entrada de dados do pagamento, como o valor, o método de pagamento e as informações do cliente.


Processamento Assíncrono de Pagamento:
O pagamento não deve bloquear a execução da aplicação. O processamento de pagamento será feito de forma assíncrona.
O status do pagamento (pendente, concluído, falhado) deve ser atualizado em tempo real, mas de forma não bloqueante.

Notificação de Pagamento:
Uma vez que o pagamento seja processado, a API deve notificar o cliente e outros sistemas sobre o status do pagamento via Kafka.
A notificação pode ser por email, SMS, ou webhook.


Controle de Threads:
Algumas operações, como o processamento de grandes volumes de dados (ex: atualização de status de pagamento para múltiplos clientes ou geração de relatórios), devem ser feitas em threads separadas para não bloquear a execução da API.
O uso de threads pode ser aplicado nas notificações, relatórios ou no processamento de grandes quantidades de pagamentos.



Persistência de Dados:
Os dados de pagamento devem ser armazenados em banco de dados relacional (MySQL, PostgreSQL, etc.).



Segurança:
A API deve usar autenticação baseada em JWT para proteger endpoints sensíveis.
O sistema de pagamento deve garantir a criptografia de dados sensíveis, como informações de cartão de crédito.




Requisitos Técnicos:
Java 17:
Utilizar os recursos mais recentes do Java 17 (ex.: sealed classes, record classes, etc.) para simplificar a estrutura do código e melhorar a manutenção.
Utilizar Project Loom ou CompletableFuture para implementar a execução de tarefas assíncronas (threads).

Spring Boot 2.x (com Java 17):
Utilizar o Spring Web para criar os endpoints RESTful.
Usar Spring Security para autenticação e autorização (JWT).
Usar Spring Data JPA para persistência de dados no banco relacional.



Kafka:
Usar o Spring Kafka para integração com Kafka, garantindo uma comunicação assíncrona e escalável.
O Kafka deve ser usado para enviar eventos de pagamento para outros sistemas ou serviços (ex: sistemas de notificação ou relatórios).


Threads (Execução Assíncrona):
Usar @Async ou CompletableFuture para implementar a execução assíncrona de tarefas como o processamento de pagamentos ou o envio de notificações.
Considerar o uso de Thread Pools para gerenciar as threads de forma eficiente e evitar problemas de escalabilidade.



Banco de Dados:
Usar um banco de dados relacional, como PostgreSQL ou MySQL, para armazenar as transações e dados relacionados aos pagamentos.
Utilizar Spring Data JPA para mapear as entidades de pagamento e garantir a persistência adequada dos dados.



Fluxo de Funcionamento da API de Pagamento:

Recebimento do Pagamento:
O cliente realiza uma requisição POST para a API com os detalhes do pagamento (valor, método de pagamento, etc.).
A API valida as informações e, se corretas, cria uma transação no banco de dados com status "Pendente".



Processamento Assíncrono:
A requisição é retornada rapidamente ao cliente, enquanto o processamento do pagamento ocorre de maneira assíncrona em uma thread separada (utilizando @Async ou CompletableFuture).
O status da transação é atualizado após o processamento do pagamento (pode ser "Concluído", "Falhado", etc.).



Envio de Notificação:
Após o processamento do pagamento, um evento é enviado para uma fila do Kafka.
Outro sistema escuta o tópico do Kafka e envia uma notificação ao cliente sobre o status do pagamento (via email, SMS, etc.).







