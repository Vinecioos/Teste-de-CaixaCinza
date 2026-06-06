# Teste-de-CaixaCinza

---

# Introdução

Este repositório contém a documentação e evidências da atividade prática de testes de caixa cinza aplicados em uma API de autenticação. A atividade foi desenvolvida utilizando Supabase como backend de autenticação, Postman Desktop para execução das requisições HTTP e GitHub para versionamento e entrega.

---

# Objetivo da Atividade

O objetivo desta atividade é compreender e aplicar testes de caixa cinza em APIs de autenticação, utilizando ferramentas modernas de mercado. Durante a atividade foram realizadas as seguintes tarefas:

- Configuração de um ambiente de autenticação utilizando Supabase
- Criação de usuários para testes
- Compreensão do funcionamento de requisições HTTP
- Utilização do Postman para execução de testes
- Validação de respostas de autenticação
- Documentação técnica de todo o processo realizado

---

# Configuração do Supabase

## Como o projeto foi criado

O projeto foi criado na plataforma Supabase (supabase.com) através do botão "New Project". Foi definido um nome para o projeto, uma senha de banco de dados e a região mais próxima. Após a criação, o projeto ficou disponível com um endpoint de API pronto para uso.

## Tipo de autenticação utilizada

Foi utilizada autenticação por **e-mail e senha**, recurso nativo do Supabase que já vem habilitado por padrão no projeto. Esse método permite que usuários se autentiquem enviando suas credenciais via requisição HTTP POST.

## Como o usuário foi criado

O usuário de teste foi criado diretamente pelo painel do Supabase em **Authentication → Users → Add user → Create new user**, preenchendo e-mail e senha. Esse método já cria o usuário com status "Confirmed", permitindo login imediato.

## Objetivo da configuração

A configuração do Supabase teve como objetivo criar um ambiente real de autenticação para que os testes pudessem ser executados contra uma API funcional, simulando um cenário próximo ao de produção.

## Evidências

<img width="1230" height="517" alt="image" src="https://github.com/user-attachments/assets/69969814-bf0e-41a8-9bb1-b147ebb2d3f6" />

<img width="1047" height="161" alt="image" src="https://github.com/user-attachments/assets/a10bebf9-3e5d-4492-9b69-bbdedeb25436" />

<img width="894" height="186" alt="image" src="https://github.com/user-attachments/assets/06f76a43-dff9-4152-a323-f2ef78236e40" />


---

# Configuração do Postman

## Como o Workspace foi criado

O Workspace foi criado no Postman Desktop através do menu **Workspaces → Create Workspace**, sendo nomeado de acordo com a atividade. O Workspace serve para organizar todas as requisições e configurações relacionadas ao projeto.

## Como o Environment foi configurado

O Environment foi criado em **Environments → "+"** dentro do Workspace. Foram adicionadas as variáveis necessárias para que as requisições pudessem ser reutilizadas sem precisar alterar valores manualmente a cada teste.

## Finalidade das variáveis

| Variável | Descrição |
|---|---|
| `base_url` | URL base da API do Supabase (Project URL) |
| `api_key` | Chave de acesso anon/public do projeto Supabase |
| `email` | E-mail do usuário criado para testes |
| `senha` | Senha do usuário criado para testes |

## Como o Postman será utilizado nos testes

O Postman foi utilizado para enviar requisições HTTP para a API do Supabase, simulando diferentes cenários de autenticação. Cada cenário foi executado alterando os dados enviados no Body da requisição e analisando a resposta retornada pelo servidor.

## Evidências

<img width="1031" height="239" alt="image" src="https://github.com/user-attachments/assets/fc62e88f-3444-46ba-b448-e4646d8693ac" />

<img width="992" height="192" alt="image" src="https://github.com/user-attachments/assets/27d7f6ec-9b70-4d60-a203-33289e8e5ba8" />

<img width="1356" height="699" alt="image" src="https://github.com/user-attachments/assets/f1fd17f3-58da-424b-8554-c1838e733153" />


---

# Configuração das Requisições

## Endpoint utilizado

```
POST {{base_url}}/auth/v1/token?grant_type=password
```

## Método HTTP utilizado

**POST** — utilizado para enviar dados ao servidor. Neste caso, envia as credenciais do usuário para que o Supabase valide e retorne um token de acesso.

## Headers utilizados

| Header | Valor |
|---|---|
| `apikey` | `{{api_key}}` |
| `Authorization` | `Bearer {{api_key}}` |
| `Content-Type` | `application/json` |

## Body JSON utilizado

```json
{
  "email": "usuario@email.com",
  "password": "123456"
}
```

## Finalidade da requisição

A requisição tem como objetivo enviar as credenciais de um usuário para a API de autenticação do Supabase e receber em resposta um `access_token`, que comprova que o login foi realizado com sucesso.

## Evidências

<img width="1008" height="254" alt="image" src="https://github.com/user-attachments/assets/5af1d368-5b87-4c57-a295-31459cd92b5b" />

<img width="1003" height="215" alt="image" src="https://github.com/user-attachments/assets/5dca46d8-0b54-4150-896b-ea54dfebc3d6" />

---

# Execução dos Testes

## Cenários executados

### 01 — Login válido

- **Entrada:** e-mail e senha corretos
- **Resultado esperado:** Status 200 + access_token retornado
- **Resultado obtido:** Status 200 — autenticação realizada com sucesso
- **Status:** ✅ OK

<img width="1006" height="367" alt="image" src="https://github.com/user-attachments/assets/e9926aa6-571d-4259-b94d-34ccca87b10a" />

---

### 02 — Senha incorreta

- **Entrada:** e-mail correto + senha errada
- **Resultado esperado:** Erro de autenticação (status 400)
- **Resultado obtido:** Status 400 — credenciais inválidas, acesso negado
- **Status:** ✅ OK

<img width="996" height="288" alt="image" src="https://github.com/user-attachments/assets/480c76de-6240-4269-b32c-aa2f4b33085e" />

---

### 03 — Usuário inexistente

- **Entrada:** e-mail que não existe no sistema
- **Resultado esperado:** Acesso negado (status 400)
- **Resultado obtido:** Status 400 — usuário não encontrado, acesso negado
- **Status:** ✅ OK

<img width="1004" height="277" alt="image" src="https://github.com/user-attachments/assets/cabe1849-3f0a-4f3a-a4eb-fef4d8cd98bc" />

---

### 04 — Campos vazios

- **Entrada:** Body enviado sem e-mail ou sem senha
- **Resultado esperado:** Erro de validação
- **Resultado obtido:** Status 400 — campo obrigatório vazio, requisição rejeitada
- **Status:** ✅ OK

<img width="969" height="242" alt="image" src="https://github.com/user-attachments/assets/95a3065c-e348-4439-b13f-7f0db82eef1f" />

---

### 05 — Credenciais inválidas

- **Entrada:** e-mail e senha em formato inválido (ex: sem @ no e-mail)
- **Resultado esperado:** Mensagem de erro
- **Resultado obtido:** Status 400 — formato de e-mail inválido, requisição rejeitada.
- **Status:** ✅ OK

<img width="970" height="265" alt="image" src="https://github.com/user-attachments/assets/8c86b357-785c-46dd-8bda-520449da0ef9" />

---

## Tabela de Cenários

| Cenário | Entrada Utilizada | Resultado Esperado | Resultado Obtido | Status |
|---|---|---|---|---|
| Login válido | E-mail e senha corretos | Status 200 + access_token | Sucesso | ✅ OK |
| Senha incorreta | Senha errada | Erro 400 | {preencher} | ✅ OK |
| Usuário inexistente | E-mail não cadastrado | Erro 400 | {preencher} | ✅ OK |
| Campos vazios | Body sem e-mail/senha | Erro de validação | {preencher} | ✅ OK |
| Credenciais inválidas | Formato inválido | Mensagem de erro | {preencher} | ✅ OK |

---

# Registro dos Testes

## Como os testes foram registrados

Os testes foram registrados em uma planilha contendo ID, cenário, entrada utilizada, resultado esperado, resultado obtido, status e observações. A planilha está disponível na pasta `/planilha/` deste repositório.


## Evidências

<img width="1300" height="122" alt="image" src="https://github.com/user-attachments/assets/65d6aadc-e978-4aed-9e7c-2b3eeee6c062" />

---

# Resultados Obtidos

Durante a execução dos testes, todos os cenários obrigatórios foram executados e validados. A API do Supabase respondeu corretamente em todos os casos:

- Retornou **status 200** e um `access_token` válido quando as credenciais estavam corretas
- Retornou **status 400** com mensagem de erro quando as credenciais estavam incorretas ou ausentes
- O comportamento da API foi consistente e previsível em todos os cenários testados

---

# Conclusão

## Os testes foram executados corretamente?

Sim, todos os 5 cenários obrigatórios foram executados com sucesso utilizando o Postman Desktop.

## A autenticação funcionou?

Sim, a autenticação via Supabase funcionou corretamente. O endpoint `/auth/v1/token?grant_type=password` retornou o `access_token` esperado para credenciais válidas e mensagens de erro adequadas para credenciais inválidas.

## Dificuldades encontradas

Dificuldade na identificação dos locais de acesso e a localização da anon key

## Melhorias que poderiam ser implementadas

- Implementar testes automatizados com scripts no Postman para validar as respostas automaticamente
- Adicionar mais cenários de teste, como limite de tentativas de login
- Configurar variáveis de ambiente separadas para desenvolvimento e produção

## Importância dos testes caixa cinza em APIs

Os testes de caixa cinza são importantes pois combinam o conhecimento parcial da estrutura interna do sistema com a perspectiva do usuário final. No contexto de APIs de autenticação, esse tipo de teste permite validar não apenas o caminho feliz (login bem-sucedido), mas também os comportamentos de erro, garantindo que o sistema seja seguro e robusto contra entradas inválidas ou maliciosas.
