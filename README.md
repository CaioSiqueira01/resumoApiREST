# Api REST e RESTFul

Uma API REST (Representational State Transfer) é um conjuto de padrões de arquitetura que definem como os aplicativos ou dispositivos podem realizar uma conexão ou comunicação uns com os outros. Ela é uma API que utiliza os princípios do protocolo HTTP para criação de serviços web e execução de funções padrões como o CRUD (Create, Reade, Update e Delete) com as solicitações GET, POST, PUT e DELETE. Já uma API RESTFul ela segue padrões de comunicação de software seguros, confiáveis e eficientes para realizar trocas de informações pela internet.

## Diferenças entre REST e RESTFul

A principal diferença entre elas é que a API RESTFul segue rigorosamente os princípios REST. Embora o REST simplifique a integração, desafios como segurança, autenticação e autorização precisam ser tratados de maneira adequada.

### Exemplo de implementação REST em Node.js

```javascript
const express = require('express');
const bodyParser = require('body-parser');

const app = express();
app.use(bodyParser.json());

const myData = [
    { id: 1, name: "Pedro Garcia" },
    { id: 2, name: "Maria Rosalva" },
    { id: 3, name: "Richard Stallman" },
    { id: 4, name: "Marcos Jesus" },
    { id: 5, name: "Joana Dark" }
];

/**
 * Lista os dados (GET)
 *
 */
app.get("/my-data", (req, res) => {
    res.json(myData);
});

/**
 * lista um determinado dado baseado 
 * no ID informado na requisição (GET)
 */
app.get("/my-data/:id", (req, res) => {
    const id = parseInt(req.params.id);
    const item = myData.find(item => item.id === id);
    if (item) {
        res.json(item);
    } else {
        res.status(404).json({ 
            message: 'Registro não encontrado!' 
        });
    }
});

const PORT = 3000;
app.listen(PORT, () => {
    console.log(`Servidor está rodando na porta ${PORT}`);
});
```
### Exemplo de serviço RESTFul em Node.js

```javascript
/**
 * Criar um novo registro (POST)
 */
app.post('/my-data', (req, res) => {
    const newItem = {
        id: items.length + 1,
        name: req.body.name,
    };
    myData.push(newItem);
    res.status(201).json(newItem);
});

/**
 * Atualizar um registro por ID (PUT)
 */
app.put('/my-data/:id', (req, res) => {
    const id = parseInt(req.params.id);
    const item = myData.find(item => item.id === id);

    if (item) {
        item.name = req.body.name;
        res.json(item);
    } else {
        res.status(404).json({ 
            message: 'Item não encontrado' 
        });
    }
});

/**
 * Excluir um registro por ID (DELETE)
 */
app.delete('/my-data/:id', (req, res) => {
    const id = parseInt(req.params.id);
    const itemIndex = myData.findIndex(item => item.id === id);

    if (itemIndex !== -1) {
        myData.splice(itemIndex, 1);
        res.sendStatus(204);
    } else {
        res.status(404).json({ 
            message: 'Item não encontrado' 
        });
    }
});
```

## HTTP verbs

Os métodos HTTP ou HTTP Verbs são responsáveis por indicar a ação a ser executada para um dado recurso. Os métodos incluem:

- **GET:** Método usado para recuperar dados de um recurso.
- **POST:** Método usado para enviar dados para serem processados por um recurso.
- **PUT:** Método usado para atualizar ou criar um recurso caso ele não exista.
- **DELETE:** Método usado para remover um recurso.
- **HEAD:** Método que solicita uma resposta de forma idêntica ao método GET, porém sem conter o corpo da resposta.
- **CONNECT:** Método que estabelece um túnel para o servidor identificado pelo recurso de destino.
- **OPTIONS:** Método que é usado para descrever as opções de comunicação com o recurso de destino.
- **TRACE:** Método que executa um teste de chamada loop-back junto com o caminho para o recurso de destino.
- **TRACE:** Método utilizado para aplicar modificações parciais em um recurso.

## HTTP Status Code

Os códigos de status são retornados como parte da resposta de uma solicitação feita a um servidor. Podem indicar falha ou sucesso de uma solicitação. Eles são agrupados em 5 categorias:

### 1xx (Informational)

Significa que a solicitação foi recebida e o processo continua.

- **100 Continue:** Apenas uma parte da solicitação foi recebida pelo servidor, mas enquanto não for rejeitada, o cliente deverá continuar com a solicitação.
- **101 Switching Protocols:** O servidor muda de protocolo.

### 2xx (Success)

Significa que a solicitação foi recebida, compreendida e aceita com sucesso.

- **200 OK:** O pedido está OK.
- **201 Created:** A solicitação é concluída e um novo recurso é criado.
- **202 Accepted:** A solicitação é aceita para processamento, mas o processamento não é concluído.
- **203 Non-authoritative Information:** As informações no cabeçalho da entidade são de uma cópia local ou de terceiros, e não do servidor original.
- **204 No Content:** Um código de status e um cabeçalho são fornecidos na resposta, mas não há corpo de entidade na resposta.
- **205 Reset Content:** O navegador deve limpar o formulário usado para esta transação para entrada adicional.
- **206 Partial Content:** O servidor está retornando dados parciais do tamanho solicitado. Usado em resposta a uma solicitação especificando um cabeçalho Range. O servidor deve especificar o intervalo incluído na resposta com o cabeçalho Content-Range.

### 3xx (Redirection)

Significa que mais ações são necessárias para completar a solicitação

- **300 Multiple Choices:** Uma lista de links. O usuário pode selecionar um link e ir para esse local. Máximo de cinco endereços.
- **301 Moved Permanently:** A página solicitada foi movida para um novo URL.
- **302 Found:** A página solicitada foi movida temporariamente para um novo URL.
- **303 See Other:** A página solicitada pode ser encontrada em um URL diferente.
- **304 Not Modified:** Este é o código de resposta para um cabeçalho If-Modified-Since ou If-None-Match, onde o URL não foi modificado desde a data especificada.
- **305 Use Proxy:** A URL solicitada deve ser acessada através do proxy mencionado no cabeçalho Location.
- **306 Unused:** Este código foi usado em uma versão anterior. Não é mais usado, mas o código está reservado.
- **307 Temporary Redirect:** A página solicitada foi movida temporariamente para um novo URL.

### 4xx (Client Error)

Significa que a solicitação contém sintaxe incorreta ou não pode ser cumprida.

- **400 Bad Request:** O servidor não entendeu a solicitação.
- **401 Unauthorized:** A página solicitada precisa de um nome de usuário e uma senha.
- **402 Payment Required:** Você não pode usar este código ainda.
- **403 Forbidden:** É proibido o acesso à página solicitada.
- **404 Not Found:** O servidor não consegue encontrar a página solicitada.
- **405 Method Not Allowed:** O método especificado na solicitação não é permitido.
- **406 Not Acceptable:** O servidor só pode gerar uma resposta que não seja aceita pelo cliente.
- **407 Proxy Authentication Required:** Você deve se autenticar com um servidor proxy antes que essa solicitação possa ser atendida.
- **408 Request Timeout:** A solicitação demorou mais do que o servidor estava preparado para esperar.
- **409 Conflict:** A solicitação não pôde ser concluída devido a um conflito.
- **410 Gone:** A página solicitada não está mais disponível.
- **411 Length Required:** O "Content-Length" não está definido. O servidor não aceitará a solicitação sem ele
- **412 Precondition Failed:** A pré-condição fornecida na solicitação avaliada como falsa pelo servidor.
- **413 Request Entity Too Large:** O servidor não aceitará a solicitação porque a entidade solicitada é muito grande.
- **414 Request-url Too Long:** O servidor não aceitará a solicitação porque a URL é muito longa. Ocorre quando você converte uma solicitação "post" em uma solicitação "get" com informações de consulta longas.
- **415 Unsupported Media Type:** O servidor não aceitará a solicitação porque o tipo de mídia não é compatível.
- **416 Requested Range Not Satisfiable:** O intervalo de bytes solicitado não está disponível e está fora dos limites.
- **417 Expectation Failed:** A expectativa fornecida em um campo de cabeçalho de solicitação Expect não pôde ser atendida por este servidor.

### 5xx (Server Error)

Significa que o servidor falhou em cumprir uma solicitação aparentemente válida.

- **500 Internal Server Error:** A solicitação não foi concluída. O servidor atendeu a uma condição inesperada.
- **501 Not Implemented:** A solicitação não foi concluída. O servidor não suportava a funcionalidade necessária.
- **502 Bad Gateway:** A solicitação não foi concluída. O servidor recebeu uma resposta inválida do servidor upstream.
- **503 Service Unavailable:** A solicitação não foi concluída. O servidor está temporariamente sobrecarregado ou inativo.
- **504 Gateway Timeout:** O gateway expirou.
- **505 HTTP Version Not Supported:** O servidor não suporta a versão "protocolo http".

---

**Autor do resumo:** Caio Henrique Soares Siqueira - 01509846
