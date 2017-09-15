# docker-lnmp
Stack LNMP (Linux, Nginx, MySQL, PHP7) utilizando Docker

**Importante:** O Docker deve ser instalado previamente.

## Stack de Desenvolvimento

`Atenção:` Nenhum tipo de configuração de segurança foi aplicada nesta Stack!

Esta configuração lhe permite rodar uma Stack LNMP (Linux, Nginx, MySQL, PHP7), utilizando a Engine do Docker, em modo de Desenvolvimento.

Esta Stack possui uma particularidade, que é a utilização de um único Servidor MySQL para todos os projetos, centralizando assim, todas as bases de dados em uma única imagem Docker (um só local).

### Configuração

Siga os passos abaixo, para criar uma única Rede para as sua Imagens Docker.

Assim que esta rede for criada, você irá criar também, um único Servidor MySQL.

### Criando uma única Rede para as sua Imagens

Acesse o terminal e execute o seguinte comando:

    docker network create rede-local-docker
    
Onde **rede-local-docker** é o nome da sua rede. 

Mantenha este nome, para que você não precise editar os arquivos de configuração!

### Criando um único Servidor MySQL

Acesse o terminal e execute o comando abaixo, para rodar um container com MySQL na Rede previamente criada:
    
    docker run --name servidor-mysql --network=rede-local-docker -v ˜/projetos/mysql/data/db:/var/lib/mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -d mysql/mysql-server:5.7

Onde **˜/projetos/mysql/data/db** é uma estrutura de diretórios, onde as bases de dados serão salvas.

Altere este caminho de acordo com a sua necessidade!

Lembre-se, quando precisar rodar o servidor MySQL novamente, bastará que você execute o seguinte comando:

    docker start servidor-mysql
    
### Copiando e Rodando

Agora, para rodar o seu projeto, bastará copiar os arquivos necessários para a raiz do seu projeto.

Para isto, basta que você copie os seguintes arquivos:
- app.docker
- docker-compose.yml
- host.conf
- web.docker

Acesse o diretório do seu projeto através do terminal e execute o seguinte comando:

    docker-compose up

Visualize o projeto pelo browser em:

    localhost
