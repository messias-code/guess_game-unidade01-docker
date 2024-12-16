# Guia de Inicialização do Projeto 🎮🚀🛠️

Este README fornece instruções detalhadas e técnicas para iniciar, operar e gerenciar o ambiente de desenvolvimento deste projeto, além de contextualizar a lógica de programação e as funcionalidades do jogo de adivinhação. 

---

## Requisitos do Sistema 🖥️🐳📥

O projeto faz uso de **Docker** e **Docker Compose** para gerenciar os containers necessários. Antes de prosseguir, assegure-se de que ambas as ferramentas estão devidamente instaladas no sistema.

### Instalação do Docker e Docker Compose

- Consulte o guia oficial do Docker para instalação: [Instalar Docker](https://docs.docker.com/get-docker/)
- Verifique se o Docker Compose já está integrado à sua versão do Docker. Caso contrário, siga as instruções específicas: [Instalar Docker Compose](https://docs.docker.com/compose/install/)

---

## Como Iniciar o Projeto 🛠️📦✨

1. Clone o repositório localmente:

   ```bash
   git clone https://github.com/messias-code/guess_game-unidade01-docker.git
   cd guess_game-unidade01-docker
   ```

2. Construa e inicie os containers com:

   ```bash
   docker compose up --build
   ```

   - Este comando cria todas as imagens necessárias e inicializa os serviços.
   - Após a inicialização, o projeto estará disponível em [http://localhost](http://localhost).

---

## Como Finalizar e Limpar o Projeto ❌🧹📂

### Encerrando o Ambiente de Forma Segura

Para remover os volumes associados e limpar os dados persistentes:

```bash
docker compose down --volumes
```

### Limpeza Completa e Restauração de Recursos

Para um reset total, incluindo remoção de imagens e dados armazenados:

```bash
# Excluir volumes persistentes
docker compose down --volumes

# Excluir imagens Docker
docker rmi $(docker images -aq)

# Limpar o sistema Docker
docker system prune -a -f

# Verificar espaço em disco ocupado
docker system df
```

> **Nota:** Esses comandos eliminam **todos os dados e configurações** armazenados no Docker. Execute com cautela.

---

## Sobre o Projeto 🧩🏗️💡

### Decisões de Design
O projeto é estruturado utilizando containers Docker para maximizar modularidade, isolamento e escalabilidade. Seus principais componentes são:

#### Docker Compose
O Docker Compose foi utilizado para facilitar a orquestração de múltiplos containers (backend, frontend e banco de dados). Ele garante que todos os serviços sejam configurados e executados de maneira eficiente, sem necessidade de configuração manual.

#### Backend
O backend é configurado com Flask, e a aplicação é executada em um container isolado.
- Desenvolvido em Python utilizando o framework Flask.
- Responsável pela lógica do jogo e gestão de dados de usuários e jogos.
- Integra-se ao banco de dados PostgreSQL para persistência.

#### Frontend
O frontend é um container Node.v18 executado de forma isolada
- Construído em React para fornecer uma interface interativa ao usuário.
- Servido pelo NGINX, que também atua como proxy reverso para o backend.

#### NGINX
O NGINX foi escolhido para atuar como proxy reverso e balanceador de carga, permitindo que múltiplas instâncias do backend sejam escaladas conforme a demanda.
- Faz parte do frontend

#### PostgreSQL
O banco de dados foi configurado para garantir persistência de dados, mesmo com a reinicialização dos containers.
- Configurado para armazenar de forma segura os dados críticos, incluindo frases secretas e tentativas.
- Também atua de forma isolada em um container dedicado.

### Lógica do Jogo

O jogo implementa uma mecânica colaborativa com dois papéis principais:

1. **Criador**:
   - Define a frase secreta e inicia um novo jogo.
2. **Quebrador**:
   - Recebe o identificador do jogo e tenta adivinhar a frase secreta baseada em suas tentativas.

Cada jogo possui um identificador único (`game_id`), utilizado para associar as tentativas ao jogo correto no backend.

---

## Como Jogar o Jogo de Adivinhação 🎯🤔✨

1. **Criar um Novo Jogo:**

   - Acesse o frontend em [http://localhost](http://localhost).
   - Insira uma frase secreta no campo indicado e envie.
   - Guarde o **game_id** gerado para compartilhar com o Quebrador.

2. **Adivinhar a Frase:**

   - Navegue até [http://localhost](http://localhost).
   - Acesse a página **Breaker** (Quebrador).
   - Insira o **game_id** fornecido pelo Criador.
   - Proponha suas tentativas para desvendar a frase secreta.

---

## Informações Adicionais 📝🛠️🔍

### Logs e Depuração

- O backend fornece logs detalhados no console do container. Para acessá-los:
  ```bash
  docker logs <nome_do_container>
  ```

### Acesso ao Banco de Dados

- Caso seja necessário explorar o banco diretamente, utilize qualquer cliente PostgreSQL com as credenciais padrão:
  - **Usuário:** postgres
  - **Senha:** secretpass
  - **Host:** localhost
  - **Porta:** 5432

---

## Resumo dos Arquivos de Configuração 📂📜🔧

### Estrutura do Projeto — Arquivos Principais

```bash
guess_game-unidade01-docker/
├── backend/
│   └── Dockerfile         # Configuração do container para o backend em Flask
├── frontend/
│   ├── Dockerfile         # Configuração do container para o frontend em React
│   └── nginx.conf         # Arquivo de configuração do NGINX para servir o frontend e atuar como proxy reverso
└── docker-compose.yml     # Orquestração dos containers para backend, frontend e banco de dados
```

Para aprofundar a compreensão do projeto, os principais arquivos de configuração são descritos a seguir:
### docker-compose.yml
- Define os serviços de backend, frontend e banco de dados.
- Configura redes, volumes e mapeamento de portas.
- Inclui verificações de saúde para dependências entre os serviços.

### Dockerfile (Backend)
- Baseado no Python 3.10.
- Configura dependências e variáveis de ambiente para o Flask.
- Especifica o comando de inicialização do backend.

### Dockerfile (Frontend)
- Usa Node.js para construir o aplicativo React e NGINX para servir os arquivos estáticos.
- Configura a variável `REACT_APP_BACKEND_URL` para conexão com o backend.
- Substitui as configurações padrão do NGINX pelo build do React.

### nginx.conf
- Configura o proxy reverso para o backend Flask.
- Define o upstream `flask` e redireciona requisições ao endpoint `/api/`.
- Ajusta cabeçalhos para compatibilidade com o proxy.

Com essas definições, é possível compreender como os serviços se interconectam e são gerenciados no ambiente Docker. 🎯🌐📁

## 🎒🏫📝 Aluno PUC

CONTEINERIZAÇÃO E ORQUESTRAÇÃO

- Nome: Ihan Messias Nascimento dos Santos
- Matrícula: 218214
- E-mail: 1568414@sga.pucminas.br