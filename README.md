
# 📚 API RESTful para Gerenciamento de Alunos

Este projeto utiliza **Express.js** para desenvolver uma API RESTful de gerenciamento de alunos, permitindo criar, listar, buscar, atualizar e excluir registros. Vamos configurar o projeto, criar o servidor Express, implementar as rotas e manipular os dados da entidade **Aluno**.

---

## 🛠️ 1. Configurando o Ambiente

### Passo 1: Instale o Node.js
Certifique-se de que você tem o Node.js instalado. Verifique com os comandos:
```bash
node -v
npm -v
```

Passo 2: Crie a Pasta do Projeto
No terminal, crie e navegue para a pasta do projeto:
```bash
mkdir api-alunos
cd api-alunos
```

Passo 3: Inicialize o Projeto Node.js
Inicie o projeto Node.js com o comando:
```bash
npm init -y
```
📦 2. Instalando Dependências
Passo 4: Instale o Express e o Body-Parser
Execute o seguinte comando para instalar o Express.js e o body-parser:
```bash
npm install express body-parser   
```

📂 3. Estrutura do Projeto
Passo 5: Crie a Estrutura de Pastas
Na pasta do projeto, crie a estrutura básica:
```bash
mkdir src
touch src/index.js
```


📝 4. Implementando a API
Passo 6: Código do Servidor
Abra o arquivo src/index.js e insira o seguinte código:
```bash
const express = require('express');
const bodyParser = require('body-parser');

const app = express();
const port = 3000;

// Middleware
app.use(bodyParser.json());

// Dados fictícios para simular um banco de dados
let alunos = [];
let idCounter = 1;

// Criar um novo aluno (POST)
app.post('/alunos', (req, res) => {
    const { nome, email, nome_curso } = req.body;
    const novoAluno = { id: idCounter++, nome, email, nome_curso };
    alunos.push(novoAluno);
    res.status(201).json(novoAluno);
});

// Listar todos os alunos (GET)
app.get('/alunos', (req, res) => {
    res.json(alunos);
});

// Buscar um aluno específico (GET)
app.get('/alunos/:id', (req, res) => {
    const aluno = alunos.find(a => a.id === parseInt(req.params.id));
    if (!aluno) return res.status(404).send('Aluno não encontrado.');
    res.json(aluno);
});

// Atualizar um aluno existente (PUT)
app.put('/alunos/:id', (req, res) => {
    const aluno = alunos.find(a => a.id === parseInt(req.params.id));
    if (!aluno) return res.status(404).send('Aluno não encontrado.');

    const { nome, email, nome_curso } = req.body;
    aluno.nome = nome;
    aluno.email = email;
    aluno.nome_curso = nome_curso;

    res.json(aluno);
});

// Excluir um aluno (DELETE)
app.delete('/alunos/:id', (req, res) => {
    const alunoIndex = alunos.findIndex(a => a.id === parseInt(req.params.id));
    if (alunoIndex === -1) return res.status(404).send('Aluno não encontrado.');

    alunos.splice(alunoIndex, 1);
    res.status(204).send(); // No Content
});

// Iniciar o servidor
app.listen(port, () => {
    console.log(`🚀 Servidor rodando em http://localhost:${port}`);
});
        
```


▶️ 5. Executando a API
Passo 7: Inicie o Servidor
No terminal, execute o servidor:
```bash
node src/index.js  
```


🔎 6. Testando a API
Você pode usar ferramentas como Postman ou cURL para testar as rotas da API. Abaixo estão alguns exemplos:

Criar um novo aluno (POST)
URL: POST http://localhost:3000/alunos
Corpo da Requisição:
```bash
{
    "nome": "Daniel Silva",
    "email": "dsdezessete@gmail.com",
    "nome_curso": "Análise e Desenvolvimento de Sistemas"
}
        
```

Listar todos os alunos (GET)
URL: GET http://localhost:3000/alunos

Buscar um aluno específico (GET)
URL: GET http://localhost:3000/alunos/1

Atualizar um aluno existente (PUT)
URL: PUT http://localhost:3000/alunos/1

Corpo da Requisição:
```bash
{
    "nome": "Daniel Silva",
    "email": "dsdezessete@gmail.com",
    "nome_curso": "Análise e Desenvolvimento de Sistemas"
}
```

Excluir um aluno (DELETE)
URL: DELETE http://localhost:3000/alunos/1
