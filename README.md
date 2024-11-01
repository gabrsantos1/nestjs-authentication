# Sistema de Autenticação JWT com NestJS

Este projeto é um sistema básico de autenticação JWT utilizando NestJS. Ele permite que usuários façam login e obtenham um token JWT para acessar rotas protegidas.

## 🚀 Requisitos

- **Node.js** >= 14.x
- **Docker** (opcional, para banco de dados MySQL)
- **Postman** ou outro cliente HTTP (para testar as rotas)

## 📦 Instalação

1. **Clone o repositório**:

   ```bash
   git clone <URL do repositório>
   cd <nome do diretório>
   ```

2. **Instale as dependências**:

   ```bash
   npm install
   ```

3. **Configure o ambiente**:

   Crie um arquivo `.env` na raiz do projeto e adicione as variáveis de ambiente:

   ```dotenv
   JWT_SECRET=sua_chave_secreta
   MYSQL_HOST=localhost
   MYSQL_PORT=3306
   MYSQL_USER=seu_usuario
   MYSQL_PASSWORD=sua_senha
   MYSQL_DATABASE=seu_banco_de_dados
   ```

4. **Inicie o Docker** (opcional):

   Se você estiver usando Docker para o banco de dados MySQL, use o `docker-compose.yaml` incluído no projeto. Certifique-se de que as variáveis de ambiente do banco de dados no `.env` correspondam às do `docker-compose.yaml`.

   ```bash
   docker-compose up -d
   ```

5. **Compile e inicie o projeto**:

   ```bash
   npm run start:dev
   ```

## 🔑 Uso

### 1. Login e Obtenção de Token JWT

Faça uma requisição `POST` para `http://localhost:<porta>/auth/login` com o seguinte corpo JSON:

```json
{
  "username": "test",
  "password": "password"
}
```

Se as credenciais forem válidas, você receberá um token JWT no formato:

```json
{
  "access_token": "<token_jwt>"
}
```

### 2. Acessar Rotas Protegidas

Para acessar uma rota protegida, inclua o token JWT no cabeçalho `Authorization` como `Bearer <token_jwt>`.

**Exemplo**:

```
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InRlc3QiLCJpYXQiOjE3MzA0OTQ2OTksImV4cCI6MTczMDQ5ODI5OX0.FYscnrXa3xslP9SSHr4gi_jJhwJRgKohuQO2bmB-x-o
```

#### Exemplo de Requisição para uma Rota Protegida

Supondo que exista uma rota protegida em `http://localhost:<porta>/profile`, você pode acessá-la com:

```bash
curl -H "Authorization: Bearer <token_jwt>" http://localhost:<porta>/profile
```

## 📂 Estrutura do Projeto

- **AuthModule**: Módulo responsável pelo sistema de autenticação.
- **AuthService**: Serviço que valida o usuário e gera tokens JWT.
- **AuthController**: Controlador que expõe a rota `/auth/login` para autenticação.
- **JwtAuthGuard**: Guard responsável por proteger rotas com autenticação JWT.

## 🧪 Testes

Para rodar os testes:

```bash
npm test
```

## 🛠️ Configuração de Produção

Em produção, certifique-se de:

- Definir `JWT_SECRET` como uma variável de ambiente segura.
- Desativar `synchronize` nas configurações do TypeORM para evitar alterações indesejadas no banco de dados.

## 📜 Licença

Este projeto é distribuído sob a licença MIT.

---

Feito com 💻 por [Pedro Toscano](https://github.com/pedro12u) e [Gabriel Santos](https://github.com/gabrsantos1) 😊
