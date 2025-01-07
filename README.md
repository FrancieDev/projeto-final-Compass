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
