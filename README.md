# roi
Node - Introdução
O Node.js é um ambiente que permite executar JavaScript no
lado do servidor, indo além do tradicional uso no navegador.
JavaScript no servidor:
Agora podemos utilizar JavaScript para criar aplicações no
servidor, expandindo nossas capacidades de desenvolvimento.
Construído sobre a engine V8 do Google Chrome:
O Node.js se baseia na mesma engine poderosa que o Google
Chrome utiliza para executar JavaScript rapidamente.
Node - Vantagens
Desempenho rápido:
Graças ao seu modelo assíncrono e ao conceito de Event Loop (um
componente crucial que permite a execução assíncrona e não bloqueante de
operações), o Node.js oferece desempenho rápido para lidar com várias
tarefas simultaneamente.
Escalabilidade:
A capacidade de lidar com um grande número de conexões simultâneas
torna o Node.js escalável, ideal para aplicações em tempo real.
Modelo de E/S não bloqueante:
No Node.js, o modelo não bloqueante significa que, em vez de esperar que
uma operação de E/S seja concluída antes de passar para a próxima tarefa,
o Node.js delega essas operações a um mecanismo assíncrono. Isso
permite que o código continue a ser executado, lidando com outras
operações enquanto a operação de E/S está em andamento.
Node - Quem usa?
Instalando o node
LinkedIn
Netflix
Walmart

Node - Rotas
Cada rota é associada a um manipulador de função (ou
call back) que é executado quando a solicitação corresponde à
rota específica. Essa função de callback é responsável por
processar a solicitação do cliente e enviar a resposta de volta.
A ideia central das rotas é organizar o código da sua aplicação
de forma a lidar com diferentes solicitações de maneira modular.
Por exemplo, você pode ter uma rota para a página inicial (/),
outra rota para a página de perfil (/perfil), e assim por diante.


Node - Criando uma WebService
Simples
Um webservice é um serviço online que permite a comunicação
entre sistemas computacionais pela internet, seguindo padrões
como SOAP ou REST, para trocar dados e funcionalidades de
maneira interoperável.
Um webservice é um tipo específico de API que segue padrões
específicos para comunicação na web, enquanto API é um termo
mais amplo que engloba qualquer conjunto de regras que
permitem a interação entre sistemas. Um webservice pode ser
uma forma de implementar uma API, mas nem toda API é um
webservice.

Node - Filtrando dados de um JSON
Usando Express
É um framework para facilitar a criação de aplicativos web com
Node.js. Ele fornece uma estrutura organizada para desenvolver
suas aplicações, ajudando a lidar com coisas como roteamento
(determinar qual parte do código lidará com qual solicitação),
manipulação de solicitações e respostas, e a configuração geral
do servidor.
Isso significa que "Node.js com Express" geralmente se refere a
usar o JavaScript no lado do servidor com a ajuda do framework
Express para construir aplicações web de maneira mais fácil e
eficiente.
Revisão para Prova - Node.js
1. O que é Node.js e por que é usado?
Node.js é um ambiente de execução JavaScript fora do navegador. Permite criar servidores e APIs com
JavaScript. É rápido, assíncrono e leve, ideal para aplicações em tempo real.
2. Como ler um JSON em Node.js?
Use o módulo 'fs' e JSON.parse():
const fs = require('fs');
const dados = fs.readFileSync('arquivo.json');
const obj = JSON.parse(dados);
3. Função de JSON.stringify()
Converte objeto em string JSON:
const json = JSON.stringify({ nome: 'Ana', idade: 25 });
4. Como escrever JSON em arquivo?
Use fs.writeFileSync:
fs.writeFileSync('saida.json', JSON.stringify(dados, null, 2));
5. fs.readFileSync() vs fs.readFile()
readFileSync: síncrono, bloqueia código.
readFile: assíncrono, ideal para apps web.
6. O que é um módulo em Node.js?
Arquivo com funcionalidades exportadas. Use módulos com 'require'.
Exemplo: npm install moment
7. Outras tarefas com JSON
Comunicação com APIs, manipulação de configs, resposta em APIs Express.
8. Por que usar JSON em apps web?
Formato leve e ideal para troca de dados cliente-servidor, bancos NoSQL.
9. Como validar JSON?
Verifique tipos manualmente ou use bibliotecas como 'ajv'.
10. Lendo JSON grande eficientemente
Use fs.createReadStream() ao invés de readFileSync.
11. JSON.parse() vs JSON.stringify()
parse: string -> objeto
stringify: objeto -> string
12. Atualizações em tempo real
Use WebSocket (ex: socket.io), fs.watch() ou bancos com eventos.
13. O que é npm?
Gerenciador de pacotes. Use para instalar módulos como 'lowdb' para manipular JSON.


//1
// Importa o módulo HTTP nativo do Node.js
const http = require('http');

// Cria o servidor HTTP
const servidor = http.createServer((req, res) => {
  // Rota principal (home)
  if (req.url === '/') {
    res.writeHead(200, { 'content-type': 'text/plain' });
    res.end('bem-vindo ao meu servidor node.js!');
  } 
  
  // Rota para alunos
  else if (req.url === '/aluno') {
    res.writeHead(200, { 'content-type': 'text/plain' });
    res.end('alunos');
  } 
  
  // Rota para professores
  else if (req.url === '/professor') {
    res.writeHead(200, { 'content-type': 'text/plain' });
    res.end('professores.');
  } 
  
  // Qualquer outra rota
  else {
    res.writeHead(404, { 'content-type': 'text/plain' });
    res.end('rota não encontrada!');
  }
});

// Define a porta onde o servidor vai rodar
const porta = 3000;
servidor.listen(porta, () => {
  console.log(`servidor rodando em http://localhost:${porta}`);
});



//2
// Importa os módulos necessários
const http = require('http');
const url = require('url');
const fs = require('fs');

// Função que lê um arquivo e envia o conteúdo como resposta
function lerArquivo(res, arquivo) {
  fs.readFile(arquivo, (err, dados) => {
    res.end(dados);
  });
}

// Função principal que trata as requisições
function callback(req, res) {
  // Define o tipo da resposta como JSON
  res.writeHead(200, { 'content-type': 'application/json; charset=utf-8' });

  // Pega o caminho da URL
  const caminho = url.parse(req.url).pathname;

  // Verifica qual rota foi acessada e responde com o JSON correspondente
  if (caminho === '/carros/classicos') {
    lerArquivo(res, 'carros_classicos.json');
  } else if (caminho === '/carros/esportivos') {
    lerArquivo(res, 'carros_esportivos.json');
  } else if (caminho === '/carros/luxo') {
    lerArquivo(res, 'carros_luxo.json');
  } else {
    res.end(`path não mapeado: ${caminho}`);
  }
}

// Cria o servidor e inicia na porta 3000
const servidor = http.createServer(callback);
servidor.listen(3000, () => {
  console.log('servidor iniciado em http://localhost:3000/');
});


//3
// Importa os módulos necessários
const fs = require('fs');
const path = require('path');
const express = require('express');

// Inicializa o app Express
const app = express();
const porta = 3000;

// Caminho do arquivo JSON com os carros
const caminhoJson = path.join(__dirname, 'carros.json');

// Configura para aceitar JSON e dados de formulário
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// Lê os dados do arquivo JSON
let carros = JSON.parse(fs.readFileSync(caminhoJson, 'utf-8'));

// Função para salvar os dados atualizados no arquivo JSON
function salvarDados() {
  fs.writeFileSync(caminhoJson, JSON.stringify(carros, null, 2));
}

// Rota para exibir o formulário HTML para adicionar carro
app.get('/adicionar-carro', (req, res) => {
  res.sendFile(path.join(__dirname, 'adicionarcarronovo.html'));
});

// Rota para processar o formulário de adição de carro
app.post('/adicionar-carro', (req, res) => {
  const novoCarro = req.body;

  // Verifica se já existe carro com o mesmo nome (case insensitive)
  if (carros.find(c => c.nome.toLowerCase() === novoCarro.nome.toLowerCase())) {
    res.send('<h1>carro já existe. não é possível adicionar duplicatas.</h1>');
    return;
  }

  // Adiciona o novo carro ao array
  carros.push(novoCarro);

  // Salva os dados no arquivo
  salvarDados();

  // Retorna resposta de sucesso
  res.send('<h1>carro adicionado com sucesso!</h1>');
});

// Inicia o servidor
app.listen(porta, () => {
  console.log(`servidor iniciado em http://localhost:${porta}`);
});


//4
// Importando os módulos necessários do Node.js
const fs = require('fs');         // Manipulação de arquivos
const path = require('path');     // Manipulação de caminhos
const express = require('express'); // Criação de servidores web

// Criando uma instância do Express
const app = express();

// Definindo a porta do servidor
const port = 3000;

// Caminho do arquivo JSON com os dados dos carros
const carrosPath = path.join(__dirname, 'carros.json');

// Lendo e convertendo os dados do JSON para objeto JavaScript
const carrosData = fs.readFileSync(carrosPath, 'utf-8');
const carros = JSON.parse(carrosData);

// Função para buscar um carro pelo nome
function buscarCarroPorNome(nome) {
    return carros.find(carro =>
        carro.nome.toLowerCase() === nome.toLowerCase()
    );
}

// Rota para buscar e exibir um carro pelo nome (GET)
app.get('/buscar-carro/:nome', (req, res) => {
    const nomeDoCarroBuscado = req.params.nome;
    const carroEncontrado = buscarCarroPorNome(nomeDoCarroBuscado);

    if (carroEncontrado) {
        // Retorna os dados do carro formatados
        res.send(`<h1>Carro encontrado:</h1><pre>${JSON.stringify(carroEncontrado, null, 2)}</pre>`);
    } else {
        res.send('<h1>Carro não encontrado.</h1>');
    }
});

// Inicia o servidor
app.listen(port, () => {
    console.log(`Servidor iniciado em http://localhost:${port}`);
});


//5
const fs = require('fs');
const path = require('path');
const express = require('express');

const app = express();
const port = 3000;

// Caminho do arquivo JSON
const carrosPath = path.join(__dirname, 'carros.json');

// Middlewares para processar JSON e dados do formulário
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// Lendo os dados do JSON
let carrosData = fs.readFileSync(carrosPath, 'utf-8');
let carros = JSON.parse(carrosData);

// Função para salvar os dados atualizados no JSON
function salvarDados() {
    fs.writeFileSync(carrosPath, JSON.stringify(carros, null, 2));
}

// Rota para exibir o formulário HTML
app.get('/adicionar-carro', (req, res) => {
    res.sendFile(path.join(__dirname, 'adicionarcarro.html'));
});

// Rota para processar a adição do carro (POST)
app.post('/adicionar-carro', (req, res) => {
    const novoCarro = req.body;

    // Verifica se o carro já existe pelo nome
    if (carros.find(carro => carro.nome.toLowerCase() === novoCarro.nome.toLowerCase())) {
        res.send('<h1>Carro já existe. Não é possível adicionar duplicatas.</h1>');
        return;
    }

    // Adiciona o novo carro e salva no arquivo
    carros.push(novoCarro);
    salvarDados();

    res.send('<h1>Carro adicionado com sucesso!</h1>');
});

// Inicia o servidor
app.listen(port, () => {
    console.log(`Servidor iniciado em http://localhost:${port}`);
});

//6
const fs = require('fs');
const path = require('path');
const express = require('express');

const app = express();
const port = 3001;

const carrosPath = path.join(__dirname, 'carros.json');

app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// Função para salvar dados atualizados
function salvarDados(carros) {
    fs.writeFileSync(carrosPath, JSON.stringify(carros, null, 2));
}

// Rota para exibir o formulário de atualização
app.get('/atualizar-carro', (req, res) => {
    res.sendFile(path.join(__dirname, 'atualizarcarro.html'));
});

// Rota para processar atualização dos dados do carro
app.post('/atualizar-carro', (req, res) => {
    const { nome, novaDescricao, novaUrlInfo, novaUrlFoto, novaUrlVideo } = req.body;

    let carrosData = fs.readFileSync(carrosPath, 'utf-8');
    let carros = JSON.parse(carrosData);

    // Busca o carro pelo nome
    const carroIndex = carros.findIndex(carro => carro.nome.toLowerCase() === nome.toLowerCase());

    // Verifica se o carro existe
    if (carroIndex === -1) {
        res.send('<h1>Carro não encontrado.</h1>');
        return;
    }

    // Atualiza os dados do carro
    carros[carroIndex].desc = novaDescricao;
    carros[carroIndex].url_info = novaUrlInfo;
    carros[carroIndex].url_foto = novaUrlFoto;
    carros[carroIndex].url_video = novaUrlVideo;

    salvarDados(carros);

    res.send('<h1>Dados do carro atualizados com sucesso!</h1>');
});

// Inicia o servidor
app.listen(port, () => {
    console.log(`Servidor iniciado em http://localhost:${port}`);
});

//6-2
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Atualizar Dados do Carro</title>
</head>
<body>
    <h1>Atualizar Dados do Carro</h1>
    <form action="/atualizar-carro" method="POST">
        <label for="nome">Nome do Carro:</label><br>
        <input type="text" id="nome" name="nome" required><br><br>

        <label for="novaDescricao">Nova Descrição:</label><br>
        <textarea id="novaDescricao" name="novaDescricao" required></textarea><br><br>

        <label for="novaUrlInfo">Nova URL de Informações:</label><br>
        <input type="url" id="novaUrlInfo" name="novaUrlInfo" required><br><br>

        <label for="novaUrlFoto">Nova URL da Foto:</label><br>
        <input type="url" id="novaUrlFoto" name="novaUrlFoto" required><br><br>

        <label for="novaUrlVideo">Nova URL do Vídeo:</label><br>
        <input type="url" id="novaUrlVideo" name="novaUrlVideo" required><br><br>

        <button type="submit">Atualizar Dados</button>
    </form>
</body>
</html>
//7
const fs = require('fs'); // Corrigido: 'fss' → 'fs'
const path = require('path'); // Corrigido: 'pat' → 'path'
const express = require('express'); // Corrigido: 'expre' → 'express'

const app = express();
const port = 3000; // Corrigido: 'tres mil' → número 3000

const carrosPath = path.join(__dirname, 'carro.json');

// Middlewares para tratar dados JSON e de formulário
app.use(express.json()); // Corrigido: 'jason' → 'json'
app.use(express.urlencoded({ extended: false }));

// Lendo o arquivo JSON
let carrosData = fs.readFileSync(carrosPath, 'utf-8'); // Corrigido: 'u-8' → 'utf-8'
let carros = JSON.parse(carrosData);

// Função para salvar os dados atualizados no arquivo
function saveDados() {
    fs.writeFileSync(carrosPath, JSON.stringify(carros, null, 4));
}

// Função para encontrar carro pelo nome
function ndCarroByName(name) {
    return carros.find(carro => carro.nome.toLowerCase() === name.toLowerCase()); // Corrigido: 'nd' → 'find', 'toLower' → 'toLowerCase'
}

// Rota: formulário de adição de carro
app.get('/add-car', (req, res) => {
    res.sendFile(path.join(__dirname, 'adicionar_carro.html'));
});

// Rota: adicionar novo carro
app.post('/add-car', (req, res) => {
    const newCarro = req.body;

    // Verifica se já existe um carro com o mesmo nome
    if (carros.find(car => car.nome.toLowerCase() === newCarro.nome.toLowerCase())) { // Corrigido: 'nd' → 'find'
        res.send('<h1>Car already exists. Cannot add duplicates.</h1>');
        return;
    }

    carros.push(newCarro);
    saveDados(); // Corrigido: adicionar parênteses para executar a função

    res.send('<h1>Car added successfully!</h1>');
});

// Rota: carros clássicos
app.get('/cars/classics', (req, res) => {
    fs.readFile(path.join(__dirname, 'carros_classicos.json'), 'utf-8', (err, data) => { // Corrigido: 'fss' → 'fs', 'u-8' → 'utf-8'
        if (err) {
            res.status(500).send('Error reading classic cars file.');
            return;
        }
        res.json(JSON.parse(data));
    });
});

// Rota: carros esportivos
app.get('/cars/sports', (req, res) => {
    fs.readFile(path.join(__dirname, 'carros_esportivos.json'), 'utf-8', (err, data) => { // Corrigido: 'lerArquivo' → 'readFile', 'u-8' → 'utf-8'
        if (err) {
            res.status(500).send('Error reading sports cars file.'); // Corrigido: 'statusCode(500)' → 'status(500)'
            return;
        }
        res.json(JSON.parse(data));
    });
});

// Rota: carros de luxo
app.get('/cars/luxury', (req, res) => {
    fs.readFile(path.join(__dirname, 'carros_luxo.json'), 'utf-8', (error, data) => { // Corrigido: 'u-8' → 'utf-8'
        if (error) {
            res.status(404).send('Error reading luxury cars file.');
            return;
        }
        res.json(JSON.parse(data)); // Corrigido: 'res.send' → 'res.json' para manter consistência
    });
});

// Rota: buscar carro por nome
app.get('/cars/:name', (req, res) => {
    const carName = req.params.name;
    const carroFound = ndCarroByName(carName);

    if (carroFound) {
        res.json(carroFound);
    } else {
        res.status(404).send('<h1>Car not found.</h1>'); // Corrigido: status 200 → 404
    }
});

// Inicialização do servidor
app.listen(port, () => {
    console.log(`Server started at http://localhost:${port}`); // Corrigido: 'hp://' → 'http://'
});
