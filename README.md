# Projeto de Testes Caixa Cinza em API de Autenticação utilizando Supabase e Postman

## 1. Introdução

O desenvolvimento de aplicações modernas depende diretamente da comunicação entre sistemas por meio de APIs (Application Programming Interfaces). Essas interfaces permitem a troca de informações entre diferentes aplicações, sendo amplamente utilizadas em processos de autenticação, armazenamento de dados e integração de serviços.

Nesse contexto, os testes de software desempenham um papel fundamental para garantir que os sistemas apresentem funcionamento adequado, segurança e confiabilidade.

Este projeto apresenta a aplicação de testes caixa cinza em uma API de autenticação utilizando a plataforma Supabase. Para a execução dos testes foi utilizada a ferramenta Postman Desktop, responsável pelo envio de requisições HTTP e análise das respostas retornadas pelo servidor.

A abordagem caixa cinza foi utilizada porque os testes foram realizados com conhecimento parcial da estrutura da API, incluindo endpoint, método HTTP, headers, parâmetros e estrutura do corpo das requisições.

## 2. Objetivo da Atividade

O objetivo principal desta atividade foi compreender e aplicar conceitos de testes caixa cinza em APIs de autenticação, utilizando ferramentas presentes no mercado de desenvolvimento de software.

Durante o desenvolvimento foram estabelecidos os seguintes objetivos específicos:

- Criar e configurar um ambiente de autenticação no Supabase.
- Habilitar a autenticação utilizando e-mail e senha.
- Criar um usuário destinado à execução dos testes.
- Compreender a estrutura e o funcionamento de requisições HTTP.
- Configurar variáveis de ambiente no Postman.
- Desenvolver requisições utilizando o método POST.
- Executar testes com credenciais válidas e inválidas.
- Analisar códigos de resposta HTTP e mensagens retornadas pela API.
- Documentar os resultados obtidos por meio de uma planilha e evidências visuais.

## 3. Configuração do Supabase

### 3.1 Criação do projeto

Inicialmente, foi criada uma conta na plataforma Supabase e posteriormente um novo projeto denominado `ProjetoAutenticacao`.

O Supabase foi escolhido por disponibilizar serviços de backend, incluindo autenticação de usuários, gerenciamento de sessões e integração por meio de APIs.

Durante a criação do projeto foram definidos seu nome, senha de banco de dados e região de hospedagem.

### 3.2 Configuração da autenticação

Após a criação do projeto, foi acessada a área Authentication, responsável pelo gerenciamento dos mecanismos de autenticação.

Foi habilitado o provedor Email, permitindo que os usuários realizassem autenticação utilizando endereço de e-mail e senha.

### 3.3 Criação do usuário de teste

Foi cadastrado um usuário específico para a realização dos testes funcionais.

Esse usuário foi utilizado como referência para o cenário de login válido, enquanto outros cenários utilizaram informações incorretas ou inexistentes.

### 3.4 Obtenção das credenciais

Para estabelecer a comunicação entre o Postman e o Supabase, foram obtidas as seguintes informações:

| Informação | Finalidade |
|---|---|
| Project URL | Identificar o endereço da API |
| Publishable Key | Permitir a comunicação com a API |

As credenciais foram armazenadas no ambiente do Postman, evitando a necessidade de inserir manualmente os valores em cada requisição.

**Evidências da configuração:**

Os registros visuais da criação do projeto, habilitação da autenticação, cadastro do usuário e obtenção das credenciais estão disponíveis na pasta `prints/`.

## 4. Configuração do Postman

### 4.1 Criação do Workspace

Foi utilizado o Postman Desktop para a elaboração e execução dos testes.

Inicialmente, foi criado um Workspace denominado `Testes API - Supabase`, destinado à organização das requisições relacionadas ao projeto.

### 4.2 Criação do Environment

Em seguida, foi criado um ambiente denominado `Supabase - Testes`.

O Environment permite armazenar informações reutilizáveis durante a execução das requisições, facilitando a manutenção e organização dos testes.

Foram configuradas quatro variáveis:

| Variável | Descrição |
|---|---|
| base_url | Endereço principal da API Supabase |
| api_key | Publishable Key do projeto |
| email | E-mail do usuário cadastrado |
| password | Senha do usuário cadastrado |

A utilização dessas variáveis possibilitou a substituição automática dos valores durante o envio das requisições.

As informações confidenciais não devem ser publicadas no repositório GitHub.

## 5. Configuração das Requisições

### 5.1 Método HTTP

Para a realização dos testes foi utilizado o método POST, responsável pelo envio de informações ao servidor.

O endpoint utilizado foi:

`{{base_url}}/auth/v1/token?grant_type=password`

O parâmetro `grant_type=password` indica que a autenticação será realizada utilizando credenciais de e-mail e senha.

### 5.2 Headers

Foram configurados os seguintes cabeçalhos HTTP:

| Header | Valor |
|---|---|
| apikey | {{api_key}} |
| Authorization | Bearer {{api_key}} |
| Content-Type | application/json |

O cabeçalho `apikey` identifica a chave utilizada na comunicação com o Supabase.

O cabeçalho `Authorization` informa a credencial utilizada na requisição, enquanto `Content-Type` especifica que os dados enviados estão no formato JSON.

### 5.3 Body JSON

O corpo da requisição foi configurado no formato JSON, contendo as informações necessárias para autenticação.

```json
{
  "email": "{{email}}",
  "password": "{{password}}"
}
```

A estrutura permite enviar os dados do usuário de forma organizada para que o serviço de autenticação possa validar as credenciais.

### 5.4 Funcionamento da requisição

Após a configuração dos parâmetros, a requisição foi enviada por meio do botão Send do Postman.

O servidor processou as informações recebidas e retornou uma resposta contendo o código HTTP e um objeto JSON.

Nos casos de autenticação válida, foi retornado um access token, utilizado para identificar a sessão autenticada do usuário.

Nos casos inválidos, a API retornou mensagens indicando a rejeição da tentativa de autenticação.

## 6. Execução dos Testes

### 6.1 Metodologia

Os testes foram realizados utilizando a abordagem caixa cinza, na qual existe conhecimento parcial sobre a estrutura e o funcionamento do sistema.

Foram analisados o endpoint de autenticação, o método HTTP, os headers e a estrutura do JSON enviado.

A partir dessas informações foram elaborados cinco cenários, contemplando situações de sucesso e falha.

### 6.2 Cenário CT01 — Login válido

Foi realizada uma tentativa de autenticação utilizando o e-mail e a senha cadastrados no Supabase.

**Resultado obtido:** HTTP 200 OK.

A resposta apresentou os dados da sessão e o campo `access_token`, demonstrando que a autenticação ocorreu corretamente.

### 6.3 Cenário CT02 — Senha incorreta

Foi mantido o e-mail válido, porém a senha foi substituída por uma informação incorreta.

**Resultado obtido:** HTTP 400 Bad Request.

A API retornou uma resposta indicando falha nas credenciais, impedindo a autenticação do usuário.

### 6.4 Cenário CT03 — Usuário inexistente

Foi realizada uma tentativa de autenticação utilizando um endereço de e-mail que não estava cadastrado no Supabase.

**Resultado obtido:** HTTP 400 Bad Request.

A resposta JSON apresentou o código `invalid_credentials` e a mensagem `Invalid login credentials`.

### 6.5 Cenário CT04 — Campos vazios

Foi enviada uma requisição contendo os campos de e-mail e senha vazios.

**Resultado obtido:** HTTP 400 Bad Request.

A API retornou o código `validation_failed` e a mensagem `missing email or phone`, demonstrando que a ausência de informações obrigatórias foi identificada.

### 6.6 Cenário CT05 — Credenciais inválidas

Foi realizada uma tentativa de autenticação utilizando um endereço de e-mail em formato inválido e uma senha preenchida.

**Resultado obtido:** HTTP 400 Bad Request.

A API retornou o código `invalid_credentials` e a mensagem `Invalid login credentials`, rejeitando a tentativa de autenticação.

## 7. Resultados Obtidos

Após a execução dos cinco cenários, foi possível observar o comportamento da API diante de diferentes condições de entrada.

### 7.1 Tabela de resultados

| ID | Cenário | Entrada utilizada | Resultado esperado | Resultado obtido | Status |
|---|---|---|---|---|---|
| CT01 | Login válido | E-mail e senha corretos | HTTP 200 + token | HTTP 200 OK + access_token | OK |
| CT02 | Senha Errada | E-mail correto e senha errada | Erro de autenticação | HTTP 400 | OK |
| CT03 | Usuário Inválido | E-mail não cadastrado | Acesso negado | HTTP 400 - invalid_credentials | OK |
| CT04 | Campos Sem Nada | E-mail e senha vazios | Erro de validação | HTTP 400 - validation_failed | OK |
| CT05 | Credenciais inválidas | E-mail em formato inválido | Erro de autenticação | HTTP 400 - invalid_credentials | OK |

### 7.2 Análise dos resultados

Os resultados demonstraram que a API apresentou comportamento adequado nos cenários executados.

No primeiro teste, a autenticação foi realizada com sucesso, comprovada pelo status HTTP 200 e pelo retorno do access token.

Nos demais cenários, as tentativas foram rejeitadas, impedindo o acesso com informações incorretas ou incompletas.

Também foi possível observar diferenças entre os tipos de erro retornados pela API. No cenário de campos vazios, ocorreu uma falha de validação, enquanto os cenários de senha incorreta, usuário inexistente e credenciais inválidas retornaram `invalid_credentials`.

Não foram identificadas falhas funcionais nos cinco cenários avaliados. Entretanto, os testes realizados não representam uma avaliação completa de segurança da API.

### 7.3 Registro dos testes

Os resultados foram organizados em uma planilha contendo os seguintes campos:

- ID do teste.
- Cenário executado.
- Dados de entrada.
- Resultado esperado.
- Resultado obtido.
- Status.
- Observações.
- Data da execução.

A planilha foi armazenada na pasta `planilha/`, enquanto os prints das execuções foram organizados na pasta `prints/`.

Essa organização facilita a consulta dos resultados e permite comprovar a execução dos cenários.

## 8. Conclusão

A realização desta atividade possibilitou compreender de maneira prática o funcionamento de uma API de autenticação e a importância dos testes caixa cinza para a qualidade dos sistemas.

Durante o desenvolvimento, foi possível configurar um ambiente de autenticação no Supabase, cadastrar um usuário de teste e estabelecer a comunicação entre a plataforma e o Postman Desktop.

A execução dos cinco cenários demonstrou que a API conseguiu autenticar corretamente o usuário válido e rejeitar as tentativas com informações incorretas ou incompletas.

Entre os principais aprendizados estão a compreensão dos métodos HTTP, a utilização de headers, a estruturação de requisições JSON e a interpretação dos códigos de resposta.

Como possíveis melhorias, poderiam ser implementados testes adicionais envolvendo recuperação de senha, expiração de tokens, renovação de sessões, tentativas consecutivas de autenticação e validações de segurança.

Conclui-se que os testes caixa cinza representam uma abordagem importante para avaliar o comportamento de APIs, pois permitem utilizar o conhecimento parcial da estrutura do sistema para elaborar cenários mais direcionados e identificar problemas de funcionamento.

## 9. Ferramentas utilizadas

- **Supabase:** configuração e gerenciamento da autenticação.
- **Postman Desktop:** elaboração e execução das requisições HTTP.
- **GitHub:** armazenamento e documentação do projeto.
