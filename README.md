

# 🚀 Como rodar

## Pré-requisitos

Antes de executar o projeto, certifique-se de ter instalado:

- **Node.js 20+**
- **JDK 21**
- **Docker Desktop** (opcional, para execução com PostgreSQL)

---

## 💻 Opção 1 · Um clique (recomendada) — Windows

A maneira mais simples de executar o projeto é utilizando o script de inicialização.

1. Extraia o projeto.
2. Abra a pasta `portal-do-instrutor`.
3. Execute o arquivo `rodar.bat` com duplo clique.

Ou, pelo terminal PowerShell:

```powershell
.\rodar.ps1.\rodar.ps1
```

O script instala as dependências do frontend, gera o build e inicia o backend utilizando o banco **H2 local**, sem necessidade de instalar PostgreSQL.

Após a inicialização, o navegador será aberto automaticamente em:

**[http://localhost:8080](http://localhost:8080)**

> Na primeira execução, o processo pode levar alguns minutos para baixar as dependências e preparar o ambiente.

---

## 🐳 Opção 2 · Docker Compose (PostgreSQL)

Caso prefira executar o projeto utilizando Docker:

```bash
# 1. Crie o arquivo de ambiente
cp .env.example .env

# 2. Inicie o banco e a aplicação
docker compose up --build
```

O Docker Compose iniciará o PostgreSQL e a aplicação automaticamente.

Acesse:

**[http://localhost:8080](http://localhost:8080)**

Para encerrar:

```bash
docker compose down
```

Para encerrar e apagar também os dados do banco:

```bash
docker compose down -v
```

> ⚠️ O comando `docker compose down -v` remove o volume do PostgreSQL e apaga os dados persistidos.

---

## 🛠️ Opção 3 · Execução manual

### 1. Frontend

Entre na pasta `mobile`:

```bash
cd mobile
npm ci
npm run build
```

O comando `npm run build` gera os arquivos estáticos que serão servidos pelo backend.

### 2. Backend

Entre na pasta `backend`:

```bash
cd ../backend
```

Para executar utilizando o perfil local com H2:

```bash
./gradlew bootRun --args='--spring.profiles.active=local'
```

No Windows:

```powershell
.\gradlew.bat bootRun --args='--spring.profiles.active=local'
```

A aplicação estará disponível em:

**[http://localhost:8080](http://localhost:8080)**

---

## 🔄 Desenvolvimento com hot reload

Para desenvolver o frontend sem precisar gerar o build a cada alteração:

```bash
cd mobile
npm ci
npm run dev
```

O frontend será iniciado na porta `5173`.

Acesse:

**[http://localhost:5173](http://localhost:5173)**

> O backend deve permanecer rodando em paralelo na porta `8080`, pois as requisições da API são encaminhadas para ele.

---

## 🔑 Acesso de demonstração

Quando a variável `SEED_SENHA` estiver configurada, o sistema poderá criar automaticamente um usuário de demonstração.

| Campo   | Valor                          |
| ------- | ------------------------------ |
| Usuário | `instrutor`                    |
| E-mail  | `instrutor@senac.br`           |
| Senha   | Valor definido em `SEED_SENHA` |

Exemplo:

```env
SEED_SENHA=senac123
```

A senha deve possuir pelo menos 8 caracteres.

> ⚠️ O usuário de demonstração deve ser utilizado apenas para desenvolvimento e testes.

---

## ⚠️ Observações

- O modo `local` utiliza H2 e dispensa a instalação do PostgreSQL.
- O modo `dev` utiliza PostgreSQL.
- O Docker Compose configura automaticamente o banco de dados.
- Para desenvolvimento local, recomenda-se utilizar o script `rodar.bat`.
- Para produção, utilize o perfil `prod` e configure corretamente as variáveis de ambiente.

