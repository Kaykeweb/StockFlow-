# StockFlow

Sistema web de gerenciamento de produtos, categorias e movimentações,
desenvolvido como trabalho acadêmico sobre **Sistemas Distribuídos**.

## 1. Visão geral

O StockFlow é uma aplicação web desenvolvida com React e TypeScript. O
frontend consome serviços HTTP por meio de uma API REST e troca
informações no formato JSON.

O projeto demonstra arquitetura cliente-servidor, comunicação REST,
integração com serviço de dados NoSQL por meio da API Technoworks e
interface web responsiva.

> **Arquitetura de dados:** o StockFlow acessa os dados pela API
> Technoworks. O projeto não configura nem acessa diretamente um projeto
> Firebase próprio do aluno. A persistência é disponibilizada pelo
> serviço externo, conforme a documentação da atividade.

## 2. Tecnologias e padrões

-   React e TypeScript
-   HTTP e API REST
-   JSON
-   Serviço de dados NoSQL disponibilizado pela Technoworks

Consulte o `package.json` para conferir as versões exatas das
dependências e os scripts disponíveis.

## 3. Arquitetura

``` text
Usuário / Navegador
        |
        v
StockFlow (React + TypeScript)
        |
        | HTTP / JSON
        v
API REST Technoworks
        |
        v
Serviço de persistência NoSQL
```

O navegador executa o frontend. Nas operações, o frontend envia
requisições HTTP à API. A API processa cada solicitação e retorna
respostas JSON para a aplicação.

## 4. Funcionalidades

### Dashboard

-   Indicadores calculados a partir dos produtos retornados pela API.
-   Total de produtos, valor total e preço médio.
-   Produtos cadastrados recentemente e gráficos.

### Produtos

Integração com a API principal para listar, cadastrar, consultar por ID,
substituir, atualizar parcialmente e excluir produtos. Também oferece
pesquisa, ordenação, validação e confirmação antes da exclusão.

### Categorias

-   Cadastro e listagem de categorias no Banco do Aluno.
-   Identificação pelo ID gerado pela API.
-   Atualização da listagem após o cadastro.

Exemplo de objeto:

``` json
{
  "tipo": "categoria",
  "nome": "Informática",
  "descricao": "Itens básicos de informática",
  "ativo": true
}
```

### Movimentações

-   Registro de entradas e saídas associados a produtos pelo ID.
-   Histórico em tabela responsiva.
-   Identificação visual de entradas e saídas.
-   Indicadores de entradas, saídas e quantidade de movimentações.
-   Saldo derivado do histórico disponível.
-   Validação de saídas quando há informação suficiente para determinar
    o saldo.
-   Atualização automática após cadastro e atualização manual.

Exemplo de objeto:

``` json
{
  "tipo": "movimentacao",
  "produtoId": "ID_REAL_DO_PRODUTO",
  "produtoNome": "Notebook Dell",
  "operacao": "entrada",
  "quantidade": 5,
  "observacao": "Reposição de estoque"
}
```

**Observação sobre o saldo:** o saldo derivado é calculado a partir das
entradas e saídas registradas. Sem saldo inicial conhecido e sem
histórico completo, o resultado não comprova a quantidade física
disponível.

### Relatórios

-   Consolidação dos dados disponíveis de produtos.
-   Valor total dos produtos cadastrados.
-   Quantidade de categorias e movimentações.
-   Resumo de entradas e saídas.
-   Impressão e exportação CSV, conforme implementado na aplicação.

### Configurações

-   Identificação do sistema e RA utilizado.
-   Endereços das APIs.
-   Teste e indicação do estado de conexão.
-   Informações sobre a arquitetura distribuída.

## 5. Endpoints utilizados

### Produtos

Base URL: `https://technoworks.com.br/api/items`

  Método   Endpoint            Finalidade
  -------- ------------------- ---------------------------
  GET      `/api/items`        Listar produtos
  POST     `/api/items`        Cadastrar produto
  GET      `/api/items/{id}`   Consultar produto pelo ID
  PUT      `/api/items/{id}`   Substituir produto
  PATCH    `/api/items/{id}`   Atualizar parcialmente
  DELETE   `/api/items/{id}`   Excluir produto

Exemplo de cadastro:

``` json
{
  "titulo": "Notebook Dell",
  "descricao": "Notebook i5 8GB",
  "preco": 3500
}
```

O ID é gerado pelo serviço. Os campos `criadoEm` e `atualizadoEm` são
administrados pela API.

### Banco do Aluno

RA utilizado: `3126103464`

-   Consulta: `GET https://technoworks.com.br/rest/3126103464?limite=20`
-   Cadastro: `POST https://technoworks.com.br/rest/3126103464`

O Banco do Aluno aceita objetos JSON com estrutura livre. Campos
iniciados por `_` são reservados pelo sistema. A aplicação utiliza os
tipos `categoria` e `movimentacao` para distinguir os registros.

A implementação descrita utiliza GET e POST no Banco do Aluno. Não se
deve presumir a existência de PUT, PATCH ou DELETE nessa rota sem
confirmação na documentação oficial.

## 6. Como executar

1.  Instale uma versão do Node.js compatível com o projeto.
2.  Abra a pasta do projeto no terminal.
3.  Instale as dependências:

``` bash
npm install
```

4.  Inicie o ambiente de desenvolvimento:

``` bash
npm run dev
```

5.  Abra no navegador o endereço local informado pelo terminal.

Os comandos acima são usuais em projetos Vite. Confira os scripts
efetivamente definidos no `package.json`.

## 7. Como verificar os dados

-   Produtos: https://technoworks.com.br/api/items
-   Banco do Aluno: https://technoworks.com.br/rest/3126103464?limite=20
-   Documentação: https://technoworks.com.br/apidoc

## 8. Verificações e testes

Conforme o relatório de implementação: - `tsc --noEmit` foi executado
sem erros. - `vite build` foi executado com sucesso. - As operações CRUD
de produtos foram verificadas diretamente contra a API. - A consulta do
Banco do Aluno foi verificada. - Os cadastros POST de categoria e
movimentação devem ser conferidos na interface, pois criam registros
persistentes.

Antes da entrega, recomenda-se executar novamente a aplicação e testar
manualmente as telas e operações principais.

## 9. Limitações e observações

-   O acesso aos dados é realizado pela API Technoworks; não há
    comprovação de acesso direto ao console Firebase de um projeto
    próprio do aluno.
-   O Banco do Aluno utiliza o RA para identificar os registros do
    estudante.
-   O saldo derivado depende do histórico disponível e não substitui um
    inventário físico ou saldo inicial confirmado.
-   Não apresentar dados fictícios como registros reais.
-   Preservar os IDs retornados pela API nas referências entre
    registros.

## 10. Identificação acadêmica

-   **Projeto:** StockFlow
-   **Aluno:** Kayke
-   **RA:** 3126103464
-   **Tema:** Sistemas Distribuídos
-   **Tipo:** Aplicação web cliente de serviços REST
-   **Comunicação:** HTTP e JSON
-   **Persistência:** serviço NoSQL disponibilizado pela API Technoworks

------------------------------------------------------------------------

Desenvolvido para fins acadêmicos.
