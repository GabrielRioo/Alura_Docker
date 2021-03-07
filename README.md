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
* `Docker Hub` - Repositorio com mais de 250mil imagens diferentes para os containers
* `Docker Machine` - Uma ferramenta que nos permite instalar e configurar em host virtuais

#### Download Docker: 
* Caso Windows seja o Pro 64 bits: [Docker CE For Windows](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
* Caso contrario: [Docker Tool Box](https://docs.docker.com/docker-for-windows/docker-toolbox/) ou [tutorial](https://www.mundodocker.com.br/docker-toolbox/)
   * Docker Engine
   * Docker Compose
   * Docker Machine
   * Docker Kinematic 
* **DEVE UTILIZAR O DOCKER MACHINE, NÃO É POSSIVEL USAR O CMD**
