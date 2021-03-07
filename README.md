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
* `docker port <ID conntainer>` - mostra as postas 

