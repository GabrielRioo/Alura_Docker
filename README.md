# Alura_Docker

### CONTAINER
* Contem toda a aplicação
* Funciona junto com SO base (divide rede, kernel...)
* Um SO para varias aplicações
* Não tem custo de manter multiplos SO
* Mais rápido de subir (segundos)

#### Ganhos:
* Melhor controle sobre o uso de cada recurso (CPU, Disco, Rede...)
* Agilidade na hora de cirar ou remover um container
* Maior facilidade de trabalhar com diversas versões de linguagens e bibliotecas
* Mais leves que as VMs

### DOCKER
* Criado pela `DotClound`
* Intermediário entre o SO e a aplicação, permite criar containers
* `Docker Engine` - Hosteia os containers, plataforma, host com Sistema Operacional
* `Docker Compose` - Um jeito mais facil de definir e orquestrar múltiplos containers
* `Docker Swarm` - Uma ferramenta para colocar multiplos Docker Gosts para trabalharem juntos em cluster
* `Docker Hub` - [Docker Hub](https://hub.docker.com/) - Repositorio com mais de 250mil imagens diferentes para os containers
* `Docker Machine` - Uma ferramenta que nos permite instalar e configurar em host virtuais
<br>
* As imagens são read-only sempre
* Um container é uma instância de uma imagem
* Para guardar as alterações a docker engine cria uma nova layer em cima da última layer da imagem

#### Download Docker: 
* Caso Windows seja o Pro 64 bits: [Docker CE For Windows](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* Caso contrario: [Docker Tool Box](https://docs.docker.com/docker-for-windows/docker-toolbox/) ou [tutorial](https://www.mundodocker.com.br/docker-toolbox/)
   * Docker Engine
   * Docker Compose
   * Docker Machine
   * Docker Kinematic 
* **DEVE UTILIZAR O DOCKER MACHINE, NÃO É POSSIVEL USAR O CMD**
<br>
* [Play With Docker](https://labs.play-with-docker.com/) : Terminal do docker para testes

#### Volumes:
* Local onde salva os dados dos containers.
* É criada dentro do proprio container
* A pasta de _Volume de Dados_ aponta para uma pasta no **Docker Host**

#### Montar Imagens:
* No projeto, criar um arquivo chamado: `Dockerfile`(padrao) ou `nome.dockerfile`
   * `FROM node:latest` - da imagem base do node
   * `LABEL Gabriel Rio` - quem está mantendo a imagem
   * `ENV NODE_ENV=production` - Variaveis de ambiente
   * `COPY . /var/www ` - copia tudo que tem dentro da projeto para pasta que esta dentro do container
   * `WORKDIR /var/www` - Work director (pasta que vai ser executada)
   * `RUN npm install` - instalar as dependencias do projeto
   * `ENTRYPOINT [ "npm", "start" ]` - quando container for startado, rodar o comando npm start
   * `EXPOSE 3000` - especificar a porta
* `docker build -f Dockerfile -t gabrielrio/node .` - constrói e nomeia uma imagem não-oficial informando o caminho para o Dockerfile. - _Precisa esta dentro da pasta do projeto para buildar_
* Sempre que alterar o `dockerfile`, tem que buildar novamente.
* `docker login` - Fazer login na conta do Docker
   * `docker push <imagem a subir>` - subir a imagem para o docker hub
   * `docker pull <imagem nome>` - pegar imagem do docker hub

#### Comandos:
* `docker run <container>` - vai até o **Docker Hub** baixa a imagem e executa e cria um container
* `docker ps` - lista os containers que estao ativos no momento
* `docker ps -a` - lista todos os containers ja criados, inclusive os **parados**
* `docker ps -q` - lista apenas os IDs dos containers ativos
* `docker run -it <container>` - atrela o terminal que esta sendo utilizado com o da imagem (ubuntu por exemplo)
* `docker start <ID container>` - deixar o container ativo
* `docker start -a -i`
* `docker stop <ID container>` - deixar o container desativaddo
* `docker stop -t 0 <ID container>` - tempo para desativar o container
* `docker stop $(docker ps -q)` - executa o comando que esta entre "()"
* `docker rm <ID container>` - remover um container especifico
* `docker container prune` - remover todos containers inativos
* `docker images` - mostra todas imagens
* `docker rmi <container>` - remove uma imagem especifica
* `docker run -d <container>` - nao trava o terminal, roda em background
* `docker run -d -P <container>` - atribua portas aleatorios
* `docker run -d -p 12345:80 <container>` - informa a porta desejada para rodar
* `docker run -d -P -e AUTHOR="Gabriel" <container>` - variaveis de ambiente
* `docker run -d -P --name <nome> <container>` - adiciona um nome ao container
* `docker run -v "var/www" <imagem>` - cria um **volume**
* `docker run -it -v "C:\Users\gabri\Desktop:/var/www" ubuntu` - Direciona o volume para pasta especificada e acessa o volume com terminal da imagem 
* `docker run -p 8080:3000 -v "C:\Users\gabri\Desktop\volume-exemplo:/var/www" -w "/var/www" node npm start` - cria um volume, na pasta especifica, e jogar essa pasta para dentro de "/var/www", localizar a pasta onde deve rodar, e rodar `npm start` quandoo startar esse container
* `docker run -d -p 8080:3000 -v "$(pwd):/var/www" -w "/var/www" node npm start` - simplificando o comando acima
* `docker port <ID conntainer>` - mostra as postas 
* `docker inspect <ID container>`
* `docker login` - Fazer login na conta do Docker
   * `docker push <imagem a subir>` - subir a imagem para o docker hub
   * `docker pull <imagem nome>` - pegar imagem do docker hub

#### Docker Compose
* Sem o docker compose, as chances de erro sao maiores:
   * Muitas flags, muito manual, **o banco de dados deve subir antes da aplicação**... 
* Orquestra os containers
* Criar o arquivo `docker-compose.yml` no projeto.
   *  Arquivo para conter o build completo dos containers
   *  A tabulação é feita somente com `TAB`
      * `version: '3'` - versão
      * `services:` - listar os serviços
      * `nginx` - serviço exemplo
      * `build: ./docker/nginx.dockerfile` - contruido a partir desse caminho
      * `context: .`
      * `image: nomeImagem` - nome da imagem
      * `container_name: nginx`
      * `ports: - 80:80` - definir a porta padrao
      * `networks: - production-network` - rede a qual vai ser associado
      * `depends_on: - "node1"` - depende do container especificado construido para ser buildado.
   * `docker-compose build` - builda o arquivo `.yml` se nao tiver nenhum erro.
   * `docker-compose up` - executa a os serviços, abre as portas.. do arquivo `yml` **(precisa estar na pasta do projeto `yml`)**
   * `docker-compose up -d` - libera o terminal e deixa o container executando. **(precisa estar na pasta do projeto `yml`)**
   * `docker-compose down` - para os containers **(precisa estar na pasta do projeto `yml`)**
   * `docker-compose ps` - listar os containers rodando
   * `docker-compose restart` - reinicia todos os serviços

#### Criando a propria Rede Id
* Os containers para conversarem entre si, devem estar na mesma rede
* `docker network create --driver bridge minha-rede` - cria a rede
* `docker run -it --name meu-container-ubuntu --network minha-rede ubuntu` - criando container em uma rede EXISTENTE
* `docker network ls` - listar todos os nomes das redes criadas

#### Terminal Ubuntu:
* `hostname -i` - ip da rede deafault

#### Lista de comandos do curso Alura:
##### Comandos relacionados às informações
* `docker version` - exibe a versão do docker que está instalada.
* `docker inspect ID_CONTAINER` - retorna diversas informações sobre o container.
* `docker ps` - exibe todos os containers em execução no momento.
* `docker ps -a` - exibe todos os containers, independentemente de estarem em execução ou não.
##### Comandos relacionados à execução
* `docker run NOME_DA_IMAGEM` - cria um container com a respectiva imagem passada como parâmetro.
* `docker run -it NOME_DA_IMAGEM` - conecta o terminal que estamos utilizando com o do container.
* `docker run -d -P --name NOME dockersamples/static-site` - ao executar, dá um nome ao container e define uma porta aleatória.
* `docker run -d -p 12345:80 dockersamples/static-site` - define uma porta específica para ser atribuída à porta 80 do container, neste caso 12345.
* `docker run -v "CAMINHO_VOLUME" NOME_DA_IMAGEM` - cria um volume no respectivo caminho do container.
* `docker run -it --name NOME_CONTAINER --network NOME_DA_REDE NOME_IMAGEM` - cria um container especificando seu nome e qual rede deverá ser usada.
##### Comandos relacionados à inicialização/interrupção
* `docker start ID_CONTAINER` - inicia o container com id em questão.
* `docker start -a -i ID_CONTAINER` - inicia o container com id em questão e integra os terminais, além de permitir interação entre ambos.
* `docker stop ID_CONTAINER` - interrompe o container com id em questão.
##### Comandos relacionados à remoção
* `docker rm ID_CONTAINER` - remove o container com id em questão.
* `docker container prune` - remove todos os containers que estão parados.
* `docker rmi NOME_DA_IMAGEM` - remove a imagem passada como parâmetro.
##### Comandos relacionados à construção de Dockerfile
* `docker build -f Dockerfile` - cria uma imagem a partir de um Dockerfile.
* `docker build -f Dockerfile -t NOME_USUARIO/NOME_IMAGEM` - constrói e nomeia uma imagem não-oficial.
* `docker build -f Dockerfile -t NOME_USUARIO/NOME_IMAGEM` CAMINHO_DOCKERFILE - constrói e nomeia uma imagem não-oficial informando o caminho para o Dockerfile.
##### Comandos relacionados ao Docker Hub
* `docker login` - inicia o processo de login no Docker Hub.
* `docker push NOME_USUARIO/NOME_IMAGEM` - envia a imagem criada para o Docker Hub.
* `docker pull NOME_USUARIO/NOME_IMAGEM` - baixa a imagem desejada do Docker Hub.
##### Comandos relacionados à rede
* `hostname -i` - mostra o ip atribuído ao container pelo docker (funciona apenas dentro do container).
* `docker network create --driver bridge NOME_DA_REDE` - cria uma rede especificando o driver desejado.
##### Comandos relacionados ao docker-compose
* `docker-compose build` - Realiza o build dos serviços relacionados ao arquivo docker-compose.yml, assim como verifica a sua sintaxe.
* `docker-compose up` - Sobe todos os containers relacionados ao docker-compose, desde que o build já tenha sido executado.
* `docker-compose down` - Para todos os serviços em execução que estejam relacionados ao arquivo docker-compose.yml.
