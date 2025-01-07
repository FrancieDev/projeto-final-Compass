# ☁️ Projeto Final do Programa de Bolsas Compass UOL
___

<div align="center">
  <img src="/assets/LogoCompassUol.png" width="340px">
</div>


### 👥 Integrantes do Grupo:
* Francie Lima
* Leonardo Pereira

**🔎 CONTEXTO:**

Nós somos da empresa "Fast Engineering S/A" e gostaríamos de uma solução dos senhores(as), que fazem parte da empresa terceira "TI SOLUÇÕES INCRÍVEIS".

Nosso eCommerce está crescendo e a solução atual não está atendendo mais a alta demanda de acessos e compras que estamos tendo.

Atualmente usamos:
* 01 servidor para Banco de Dados Mysql (500GB de dados, 10Gb de RAM, 3 Core CPU);
* 01 servidor para a aplicação utilizando REACT – frontend (5GB de dados, 2Gb de RAM, 1 Core CPU);
* 01 servidor de backend com 3 APIs, com o Nginx servindo de balanceador de carga e que armazena estáticos como fotos e links. (5GB de dados, 4Gb de RAM, 2 Core CPU);

<div align="center">
  <img src="/assets/ArquiteturaAtual.png" width="400px">
   <p><em>Arquitetura atual da Fast Engineering S/A</em></p>
</div>

Queremos modernizar esse sistema para a AWS, precisamos seguir as melhores práticas arquitetura em Cloud AWS, a nova arquitetura deve seguir as seguintes diretrizes:

* Ambiente Kubernetes;
* Banco de dados gerenciado (PaaS e Multi AZ);
* Backup de dados;
* Sistema para persistência de objetos (imagens, vídeos etc.);•
* Segurança;

Porém antes da migração acontecer para a nova estrutura, precisamos fazer uma migração “lift-and-shift” ou “as-is”, o mais rápido possível, só depois que iremos promover a modificação para a nova estrutura em Kubernetes.

**ETAPA 1: Migração "AS-IS"**

ATIVIDADES NECESSÁRIAS PARA A MIGRAÇÃO

1. Definição dos pré-requisitos
2. Criação do usuário do AWS Identity and Access Management (IAM)
3. Acesso ao console do AWS MGN
4. Definição do modelo de configurações de replicação
5. Instalação do AWS Replication Agent
6. Definição das configurações de execução
7. Execução de uma instância de teste
8. Execução de uma instância de substituição
9. Limpeza após a substituição final

**ETAPA: Modernização/Kubernetes**

### **Arquitetura da solução proposta**

A solução planejada na AWS é construída com base em serviços gerenciados que simplificam a gestão de infraestrutura e permitem à equipe de desenvolvimento focar no aprimoramento dos serviços oferecidos aos clientes. Essa abordagem reduz significativamente o esforço necessário para tarefas operacionais, como provisionamento de servidores e escalabilidade manual, direcionando os recursos para a entrega de novas funcionalidades e melhorias.

Com uma infraestrutura gerenciada pela AWS, garantimos alta disponibilidade, segurança e desempenho, proporcionando uma experiência consistente para os usuários finais. Além disso, a adoção de práticas modernas, como integração e entrega contínuas (CI/CD), reforça a eficiência do desenvolvimento, assegurando que as aplicações atendam às expectativas de confiabilidade e agilidade no mercado.

<div align="center">
  <img src="/assets/ArquiteturaFinal.png">
   <p><em>Arquitetura final sugerida</em></p>
</div>

### **🧰 Serviços e Recursos Usados na Arquitetura**

#### Amazon Cognito
O Amazon Cognito oferece um armazenamento de identidade que pode ser dimensionado para milhões de usuários, oferece suporte à federação de identidades sociais e corporativas e oferece recursos avançados de segurança para proteger seus consumidores e negócios. 
- Uso: Com o Amazon Cognito, será possível adicionar recursos de inscrição e login de usuários e controlar o acesso às aplicações. 

#### Amazon Route 53 
O Amazon Route 53 é um serviço DNS que permite registrar e gerenciar domínios com roteamento de tráfego para recursos AWS, como ELB e CloudFront. Facilita o roteamento de tráfego eficiente e garante alta disponibilidade, direcionando acessos para instâncias e serviços AWS.  
- Uso: A requisição do cliente é enviada para o Amazon Route 53, que direciona o tráfego para o CloudFront apropriado com base no tipo de conteúdo solicitado (conteúdo estático, frontend ou API).

#### Amazon CloudFront  
O Amazon CloudFront é um serviço de Content Delivery Network (CDN) oferecido pela AWS. Sua principal função é acelerar a entrega de conteúdo estático e dinâmico, como páginas web, imagens, vídeos, scripts e outros arquivos multimídia aos usuários finais com baixa latência e alta disponibilidade.  
- Uso: Se o conteúdo solicitado for estático (imagens, CSS, JavaScript), o CloudFront o recupera do S3 e o entrega diretamente ao cliente com baixa latência e alta disponibilidade.  
    Se o conteúdo solicitado for o frontend da aplicação web, o CloudFront o recupera do S3 e o entrega ao navegador do cliente.  
    Se o conteúdo solicitado for uma API, o CloudFront o direciona para o Application Load Balancer.

#### Amazon Simple Storage Service
O Amazon S3 utiliza Buckets para armazenar e distribuir conteúdo estático, incluindo imagens, vídeos e arquivos, integrando-se ao CloudFront para uma entrega eficiente. Oferece armazenamento seguro e escalável para imagens, vídeos e arquivos.
- Uso: Armazenamento dos arquivos estáticos e de frontend da aplicação.

#### AWS WAF
O AWS Web Application Firewall é um serviço de firewall projetado para proteger aplicações web contra ataques comuns, proporcionando proteção avançada contra ameaças, garantindo a segurança de aplicativos da web.
- Uso: O WAF oferece uma ampla gama de recursos de segurança, como filtragem de IP, regras de bloqueio de URL e proteção contra DDoS. Ele é posicionado antes do Application Load Balancer, assim filtra o tráfego malicioso antes que chegue aos clusters do EKS.  
Essa configuração oferece a melhor proteção para sua aplicação web com o mínimo de impacto no desempenho e na complexidade.

#### Amazon VPC
O Virtual Private Cloud isola a infraestrutura na nuvem e fornece controle granular sobre a rede, criando uma rede privada virtual. Cria uma rede VPC, melhorando o controle de tráfego e a segurança da infraestrutura.
- Uso: Cria um ambiente de rede isolado e seguro na AWS, permitindo o controle granular do tráfego de rede e a segmentação de recursos. A VPC é dividida em sub-redes públicas e privadas, segregando recursos sensíveis (como bancos de dados) da internet pública.

#### Amazon ALB
Application Load Balancer é um serviço que distribui o tráfego entre várias instâncias ou recursos para garantir a alta disponibilidade e a escalabilidade de aplicativos.  
- Uso: O Application Load Balancer distribui o tráfego entre os clusters do EKS que executam o backend da aplicação web.

#### Amazon EKS
O Elastic Kubernetes Service atua como a base da arquitetura, oferecendo orquestração de contêineres por meio do Kubernetes. Proporciona orquestração de contêineres escalável, permitindo a expansão dinâmica e alta disponibilidade da aplicação.
- Uso: O EKS é responsável pelo gerenciamento do ciclo de vida dos conteinêres, incluindo provisionamento, escalonamento e reinicialização em caso de falhas.

#### Amazon Fargate
O Amazon Fargate é um serviço de computação sem servidor da AWS projetado para executar contêineres. Ele permite que você execute aplicativos em contêineres sem precisar provisionar e gerenciar servidores, o que significa que você não precisa se preocupar com a infraestrutura subjacente.
- Uso: Os conteinêres do Fargate executam o backend da aplicação web e se comunicam com o banco de dados RDS MySQL para recuperar ou armazenar dados e retornam as respostas ao cliente.

#### Amazon RDS MySQL 
O Amazon RDS é um serviço de banco de dados relacional oferecido pela AWS. Ele foi projetado para simplificar a administração, operação e escalabilidade de bancos de dados relacionais, permitindo que os desenvolvedores se concentrem em suas aplicações sem se preocupar com a gestão do banco de dados subjacente.
- Uso: O banco de dados RDS MySQL armazena os dados da aplicação web, como produtos, pedidos, usuários e informações de pagamento.

#### NAT Gateway
Um gateway NAT é um serviço de Network Address Translation (NAT – Conversão de endereços de rede). Você pode usar um gateway NAT para que as instâncias em uma sub-rede privada possam se conectar a serviços fora da VPC, mas os serviços externos não podem iniciar uma conexão com essas instâncias.
- Uso: O NAT Gateway permite que os conteinêres do Fargate nas sub-redes privadas se comuniquem com a internet e com outros serviços da AWS de forma segura.

#### Internet Gateway
Um gateway da Internet é um componente da VPC horizontalmente dimensionado, redundante e altamente disponível que permite a comunicação entre a VPC e a Internet. Ele oferece suporte para tráfego IPv4 e IPv6. Não causa riscos de disponibilidade ou restrições de largura de banda no tráfego de rede.
- Uso: O Internet Gateway habilita recursos nas sub-redes públicas para estabelecer conexão com a Internet.

#### Network ACL
A Network Access Control List é uma lista com camadas adicionais de segurança que controlam o tráfego de entrada e saída de sub-redes em sua VPC.
- Uso: Recurso de segurança que permite controlar o tráfego de entrada e saída das sub-redes dentro da VPC. 

#### AWS IAM
O AWS Identity and Access Management é um serviço que ajuda você a controlar o acesso aos recursos da AWS de forma segura. Com o IAM, é possível gerenciar, de maneira centralizada, permissões que controlam quais recursos da AWS os usuários poderão acessar. Você usa o IAM para controlar quem é autenticado (fez login) e autorizado (tem permissões) a usar os recursos.
- Uso: A IAM Role dentro do Fargate assume um papel crucial na atribuição de permissões e no controle de acesso para os conteinêres em execução. Ela funciona como uma identidade digital para os conteinêres, permitindo que eles acessem recursos específicos da AWS e realizem tarefas necessárias para a sua operação, como por exemplo permitindo a conexão com o banco de dados RDS.

#### Amazon CloudWatch
O Amazon CloudWatch é um serviço de monitoramento dos recursos da AWS e as aplicações executadas na AWS em tempo real. Você pode usar o CloudWatch para coletar e monitorar métricas, que são as variáveis que é possível medir para avaliar seus recursos e suas aplicações.
- Uso: Monitora a infraestrutura e a aplicação, fornecendo insights sobre desempenho, segurança e eventos, permitindo a prevenção, detecção e resolução rápida de problemas.

#### Amazon Backup
O AWS Backup é um serviço totalmente gerenciado que facilita a centralização e a automatização da proteção de dados em todos os serviços da AWS, na nuvem e no local garantindo uma maior granularidade e controle em relação às políticas de backup.

- Uso: O Amazon Backup será responsável pela garantia de políticas que estejam em total acordo com as normas de backup pré-estabelecidas pela empresa.

#### AWS Certificate Manager
O Gerenciador de Certificados da AWS é uma ferramenta essencial para garantir a segurança e a confiabilidade da sua infraestrutura e aplicações na nuvem. Ele oferece uma solução centralizada para gerenciar todo o ciclo de vida dos seus certificados digitais, desde a solicitação e emissão até a renovação e revogação.

- Uso: O AWS Certificate Manager será responsável pela guarda, garantia e segurança dos certificados digitais como SSL/TLS para garantir a comunicação criptografada de ponta a ponta utilizando o protocolo HTTPS.


#### AWS Database Migration Service
O AWS DMS é um serviço de replicação e migração gerenciado que ajuda a mover workloads analíticos e bancos de dados para a AWS rapidamente, de forma segura e com o mínimo possível de inatividade e zero perda de dados.
- Uso: Permite migrar os dados do banco de dados on-premises para a AWS.

### Migração dos dados

Propomos a migração segura e eficiente do servidor MySQL on-premises para o Amazon RDS na nuvem utilizando o AWS Database Migration Service (DMS). O DMS garante replicação contínua dos dados durante a migração, assegurando integridade e consistência. 
O DMS facilita o processo com uma interface amigável para configuração e gerenciamento, além de oferecer monitoramento completo da migração. Com o AWS DMS e o RDS, garantimos uma migração tranquila, segura e eficiente para a nuvem e ao mesmo tempo, será possível desfrutar de escalabilidade sob demanda, confiabilidade e segurança robusta, redução de custos e alto desempenho.