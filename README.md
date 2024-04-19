# docker-lnmp
Stack LNMP (Linux, Nginx, MySQL, PHP) utilizando Docker

`Importante:` O Docker deve ser instalado previamente.


## Stack de Desenvolvimento

`Atenção:` Nenhum tipo de configuração de segurança foi aplicada nesta Stack!

Esta configuração lhe permite rodar uma Stack LNMP (Linux, Nginx, MySQL, PHP), utilizando a Engine do Docker, em modo de Desenvolvimento.

Esta Stack possui uma particularidade, que é a utilização de um único Servidor MySQL para todos os projetos, centralizando assim, todas as bases de dados em uma única imagem Docker (um só local).


### Versões das ferramentas que compõem a Stack

As seguintes versões das ferramentas que compõem a Stack estão sendo atualmente utilizadas:

| Ferramenta | Versão  |
|:----------:|:--------|
| Nginx      | 1.25.4  |
| MySQL      | 8.0.32  |
| PHP        | 8.2     |


### Configuração

Siga os passos abaixo, para criar uma única Rede para os seus containers Docker.

Assim que esta rede for criada, você irá criar também, um único Servidor MySQL.


### Criando uma única Rede para os seus containers

Acesse o terminal e execute o seguinte comando:

    docker network create rede-local-docker

Onde **rede-local-docker** é o nome da sua rede.

`Dica:` Mantenha este nome, para que não seja necessário editar os arquivos de configuração!


### Criando um único Servidor MySQL

Acesse o terminal e execute o comando abaixo, para rodar um container com MySQL na Rede previamente criada:

    docker run -d --restart=always --name servidor-mysql-8 --network=rede-local-docker -v ˜/projetos/mysql8/data/db:/var/lib/mysql -p 3306:3306 -e MYSQL_ALLOW_EMPTY_PASSWORD=yes -e MYSQL_ROOT_HOST=% mysql/mysql-server:8.0.32


docker run -d --restart=always --name servidor-mysql-8 --network=rede-local-docker -v /Users/maiconschmitz/projetos/mysql8/data/db:/var/lib/mysql -p 3306:3306 -e MYSQL_ALLOW_EMPTY_PASSWORD=yes -e MYSQL_ROOT_HOST=% mysql/mysql-server:8.0.32

Onde **/projetos/mysql8/data/db** é uma estrutura de diretórios, onde as bases de dados serão salvas.

Altere o caminho acima, de acordo com a sua necessidade.

É importante notar que este servidor MySQL não possui senha de acesso!

Lembre-se, quando desejar manipular o servidor MySQL, bastará que você execute os comandos, utilizando o nome da imagem **servidor-mysql-8**:

Para rodar:

    docker start servidor-mysql-8

Para rodar:

    docker stop servidor-mysql-8


### Copiando e Rodando

Agora, para rodar o seu projeto, bastará copiar os arquivos necessários para a raiz do mesmo.

Para isto, copie os seguintes arquivos:
- app.docker
- docker-compose.yml
- host.conf
- web.docker

Acesse o diretório do seu projeto através do terminal e execute o seguinte comando:

    docker-compose up

Visualize o projeto pelo browser em:

    localhost
