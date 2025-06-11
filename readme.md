## DAS 2

Luis Felipe Menslin

## 27/02/2025
Trade-offs

Resultado da escolha de ferramentas necessarias para um projeto;

Exemplo:

 Durabilidade
    Dados duraveis, garantia de permanencia de informação;
    Caracteristicas de sistemas transacionais;

 Cache
    Memoria temporaria, guardar informações em memória para mais rapidez  na busca dos dados

Escalabilidade

Assegurar que uma aplicação consiga se manter mesmo em altos niveis de demandas

Exemplo:

 Servidor local
    Maior rentabilidade no sentido de gerenciamento fixo

 Servidor Clound
    Maior segurança e flexibilidade na garantia de escalabilidade

Automatização

Automatizar processos e recursos de um sistema 

Exemplo:

 Aplicação que monitora o estado de servidores para criar alertas;
 Sistema responsável por recriar maquinas virtuais sozinha;
 Aplicar recursos necessários para colocar a aplicação online novamente;

IaC

Infraestrutura em forma de codigo

 Reduz falhas por configuração manual;
 Propaga mudanças e atualizações de forma uniforme;
 Agilidade na execução e manutenção de aplicações;

Recursos Descartaveis

Tratar recursos todos como descartaveis

 Recursos que podem ser facilmente substituidos;
 Substituição de recursos mais antigos automaticamente devido a descartabilidade

## 06/03 

automatizar o provisionamento das máquinas, infra como código.
não tratar dados como algo único sempre, manter opções de backup para restabekecer o sistema mais rapimento.
uma coisa altamente acoplada algo que não pode ser substituita por outra de forma rapida.
quando se trata de banco de bados geralmente é muito acoplano, mas pode ser usado um ELB um balanceador de carga e varias copias do banco.
half check
sempre tenha redundancia incluse no ELB (elastic load balancing)

escolhar a opção de banco correta, temos 2 grandes mundos
relacional mais tradicional o problema dele ele é fixo, ele tem um limite escalabilidade horizontal, criar replicas do banco mas é de leitura não consegue escalar
infinitamente o banco se torna lento

noSQL pensado para escalar horizontal, perfomance extrema e quando não se consegue modelar a tabala do banco de dados

aws procura sempre ser eficiente no custos, para o cliente gastar apenas o que precisa
não se criar coisas complicadas para tarefas simples

Use cache
minimizar as operações de requisições de dados.
segurança usar serviços gerenciados AWS que tem a responsabilidade (S3)
muitas empresas não tem uma boa segurança, tem apenas um firewall e um antivivus e acham que estão seguros
semore use o principio do privilégio minimo. cada um tem o acesso que precisa de nada mais.

infraestrutura global da AWS

36 regiões no mundo , 114 zonas de disponibilidasde 700 ROPS prontos de presença
pensar nas regiões que os clientes precisam de acesso, quanto mais perto mais rapido é .
conexão entre as AZ totalmente redundante entre delas rede propria rede privada da AWS
local zone rodar serviços computacionais aonde não tem regiões AWS
pequenas AZs dentro de outros lugares. 

WAVELength 5g rodar serviços da AWS em operadoras de telefonia evitando gargalos nas redes normais de internet
colado no 5g

## 10/03 

todas as regiões da aws tem 3 azs algumas tem mais, Az são datacenters

Az serve para alta disponibilidade
local zone extrutua parecida com uma az mas ela é menor n precisa deu uma região, ( argentina tem 1 em buenos aires). serviços computacionais
conteudos rapidos, exemplo o spam do netflix usam locals zones Edge locastion 700 pontos espalhaados pelo mundo, eles buscam as informação de forma intermediario reginal cache.
buscando da região.

Segurança de acesso. 
modelo d responsabilidasde compartilhada quando vc roda sua infra vc é o responsavel
quando vc roda  outro a responsabilidade é compartilhada  IaaS/EC2  servidor  infraestrutura com serviço
responsabilidade da aws região zonas livres e edge locastlion a infra 
eles passam apenas o link de acesso o resto da resposabilidade é sua

S3 ( serviço de software as A serviço / PaaS 
cria um balde gamha um endereço de inter poem e a tira arquivos um DROPBOX
servidor rede fiwrewall responsabilidade aws

principaus pilares da segurança
tem que ter unm provedor de identidade forte ( não ter sistemas que guardam usuarios e senhas dentro do banco de dados ( usar soft que guardam  as credenciais exemplo keycloak).

proteger dados em transito e em descanso ( SSL TLS HTTPS, trafegar as semha criptogradas ) 
criptografia em descanso quando esta gravada em disco um bucket s3 HD do servidor

aplicar segurança em todas as camadas ( antivirus, firewall, 

Manter os dados logne das pessoas( não dar acesso direito ao banco de dados, precisam passar por autenticação

Ter rastreabilidade vc saber quando um usuario logou e qo que fez no sistema
O que aconteceu na nuvem, 

Se preparar para eventos de segurança, ter uma equipe de segurança caçando problemas.

automatizar as meelhores praticas de segurança, evitar coisas manuais, evitando problemas de brechas de segurança.

CONCEITO DE NUVEM
autenticação mostrar que o usuario realmente é vc no casos 2 fatores de autenticação, ( login e senha ) e biometria ( autenticação pelo celular ou gerador de senha)
Autorização o que ele pode ter acesso, pode mecher em baldes s3 mas não no banco de dados, é dito o que cada usuario pode ou não mecher.  (IAM identiti proviber aws)
principio do privilegio minimo

sempre use criptografia entre as contas

## 13/03 

Modelo de responsabilidade compartilhada
Principio de Privilegio minimo
Autenticação
Autorização
Identify and Acess Management
Usuarios
Acesso pela console / programatico

IAM ele cuida de usaurios grupos de usuarios roles voices
usuario é uma credencial  pode ser um software tb
Sempre que criar uma conta deve pensar no tempo de duração dela. caso algum funcionario saia vc deve removoela do IAM
credenciais acess key e acess passoword são de longas duração a menos que alguem remova e cria novas, ficam nas maquinas.
usuario ROOT não tem limite do que pode fazer. 
Roles: são mudanças de autorização e negação de outras para acesso em outras partes do sistema

## 17/03

RBAC  ROle base acess Control são mecanimos de controle, permissões de banco.
polices de itendidade são dadas pelo Root feito pelo IAM
polices de recursos feito pelo S3 criando um balde ( bucket),  
ARN é um identificador unico, permitindo que qualquer usuario tenha acesso ao  seu bucket.
é um recurso aonde vc vai na AWS e escreve que vc da permissão de acesso.
recurso tem principal identificar quem é o usuario.

sistemas de arquivos blocados eles são no meio do arquivo ( EBS)
file share são redes compartilhadas de computadores para troca de arquivos dentro do servidor (EFS) FXs
armazenamento de objeto é um tipo de armazenamento da internet que salva o binario do arquivo e meta dados (dados de dados sobre os dados ), o Dono é tal pessoas. (S3)
s3 é virtualmente ilimitado n tem numero max de armazenamento.
limite de 5 t por objeto/arquivo
todo objeto s3 tem uma URL global e unica.

policy de identidade

## 24/03

pessoas que lhedam com s3 precisa de preocuiiapr com limite de espaço. Lifecycle
impactando no custo pq os clientes precisam ter espaço, jeitos de economizar apagar o que precisa ou ajustar as classes de armazenamento ( que tb é pago)
pode ser criadas regras para apagar arquivos com tempo de validade  presscritos pelas regras da empresa, transcionar interclasses ou expirar um arquivo
ele sempre nascew com versionamento desligado, mas se habilitar não da mais para desabilitar o que pode ser feito é pausar.
cada versão é uma copia inteira do objeto
não é possível editar um arquivo dentro do s3.

o que é cors
validação proteção pros seus arquivos no s3

## 27/03
cuidar para não expor bucket para internet
uso de criptografia
SSE-S3
são envelopes com chaves criptografadas
ele quando é feito vem todo privado só o dono tem acesso,
vc pode tornar parcialmente acessível, usuarios que vc determianr podem acessar
ou vc pode tornar totalmente publico exemplo um site.

batch operation vc faz copia de arquivos para outro balde escolhendo quais vc quer ver, pois pode haver muitos arquivos para listar de uma unica vez


## 03/04
EC2
ma nuvem vc tem multiplas maneira de ordar algo dentro dela, pode usar o ec2 para rodar uma maquina direta no hardware
ELastic COmpute Cloud, é o segundo serviço da AWS, servidores para rodar na nuvem
todo servidor fisico, mas o sistema não tem contado direto com o hardware, ele tem contado com o hypervisor, no caso um geremnciador vai admnistar o hardware CPU memoria etc, 
atraves das placa de rede é acessado a internet outros servidores e serviços da AWS, no caso um s3 tb pode ser conecatado, e geralmente para guarda o servidor é usado o EBS ( Amazon elastic Block Store 
armazenamento ephemewral é tipo um flash  armazenamento persistente é o que fica quando desliga maquina etc
para criar um servidor aws tem um passo a passo, escolher a aamazon machine imagem que via ser usada no caso o sistema operaciona, seja linux wins ou mac, (AMI) 
tornar o ambiente repetitivel, reutilizavel e recuperavel. 
a imagem vive em uma região da aws, mas pode ser copiada caso não possua na sua regiao
existe um conjunto de imagnes que a propria aws te dar caso não queira criar do zero
e existe o AWS marketplace mas pode haver algum soft a mais embutido
community AMIs use por sua conta e risco nada é testado pela aws é publico.
faz o launche no caso cria a maquina estado de pendente depois estadao de running, pode rebootar a maquima, pode desligar a maquima, e pode terminar no caso apagar ela.
e pode ser hibernada.
vc precisa saber as familias na escolha da maquina ( 1 caracter familia, depois numero a geração, letreas complementarem ( gn graviton  ARM) tamanho da maquina.
computer optimizer é feito para ver se a maquina esta sobrando ou faltando overprovisioned ou underrovivisioned
EBS não é fileshare, 
s3 não é sistema de arquivos
File Share EFS ou FSX 
EFS sistema de file share  LINUX. por causa do protocolo v4
pago apenas pelo que se usa de armazenamento
FSX pode ser usado com o wins por causa do protolo suportado dele.

## 07/04
EBS hd do servidor

Regiões são compostas por Az ao menos 3, HPC seria uma solução aonde as maquinas ficam super juntas no caso um Cluster para processar coisas pesadas, se possivuel na mesma maquina
ou no mesmo hack fisico a fim de reduzir a latencia, alta disponibilidade, 
Spread é espalhando criando alta disponobilidade mas reduz latencia e velocidade
partition - apacbe kafka , cassandra, spark, todas elas fazedm processamento de dados ou streamer, sharding os dados n ficam em um unico servidor, a ferrramenta espalha em varios
servidores, mas que eles fiquem proximos, meio termo entre o cluster e o spread, usando um dos soft ja listado no exemplo.
EC2

on-demand paga por hora usada
reserved insta eu digo o que vou usuar e uso só aquilo, uma forma de compromisso, exemplo servidor tal masquina tal sistema etc mas apenas isso por um tempo determinado.
se pagar adiantado tem muito mais descontos
Saving plans - 

amazon ec2 Spot leilão de maquinas comprar partes ociosas de maquinas afin de procurar um desconto bem grande, mas pode acontecer a qualquer momento aws pode vir atras e mandar para de usar
2 minutos geralmente.

nAo se pode depender de invervenção manual para proteção das maquinas. ( segurança)

## 10/04

BANCO DE DADOS 
escalabilidade de um banco sempre é um desafio
quanto de espaço eu preciso
modelo de dados que vai ser utilziado e latencia
precisa que suporte qualquer modelo de dados, ja que o banco de dados relacional não tem total suporte 
na aws tem um serviço chamado RDS feito para subir banco de dados na aws, inclusive pode subir uma maquina e vc mesmo instalar o banco ( serviço não gerenciado) 
Mas pode ser feito gerenciados tb mundo relacional
na parte não relacional DynamoDB aonde roda amazon.com
amazon netpune blockchains são exenmplos disso
amazon elastic cache copias do banco para resposta mais rapida
escalabilidade vertical aumenta a maqyina poder
vertical hozizontal copias do banco

## Aula 17/04/2025
Connection pooling: melhora a escalabilidade por meio de um rds proxy entre a aplicação e o BD, evitando a exaustão do servidor devivo às várias conexões
Backups no RDS: automatizado (faz a cada 5 dias, retenção de 7 a 35 dias), snapshot (manual, retenção perpétua)
KMS: key management system, cofre de chaves
Chave simétrica: a mesma chave que criptografa é a que descriptografa
Chave assimétrica: as chaves que criptografam e descriptografam são diferentes
DynamoDB: BD NoSQL, serverless, performance de um dígito de milisegundo. Ideal para arquitetura baseada em eventos. Ativo/ativo. Critpografia automática padrão, usa IAM roles para autenticar acesso
Redshift: BD para data warehouse, para pesquisas pesadas e históricas
Outros DBs disponibilizados na AWS: DocumentDB, Keyspaces, MemoryDB Neptune, Timestream, Quantum Ledger

## Aula 05/05/2025
- Início do 2º Bimestre e do módulo de redes na AWS.

- **Amazon VPC (Virtual Private Cloud)**:  
  Solução de rede virtual baseada em SDN (Software Defined Network) na AWS.  
  - **Isolamento**: O primeiro nível de isolamento é a conta AWS; o segundo, a rede (VPC).
  - Permite criar sub-redes, grupos de segurança, ACLs, e controlar todo o tráfego.
  - Redes em regiões diferentes não se comunicam por padrão.
  - Cada VPC é restrita à sua região de criação.
  - **Customização**: CIDR, sub-redes, rotas, ACLs, grupos de segurança, etc.
  - **VLAN x Sub-rede**:  
    - VLAN: conecta máquinas em uma mesma rede virtual local.  
    - Sub-rede: segmento da VPC, conecta máquinas em uma mesma sub-rede.
  - **Subnet pública**:  
    - Possui acesso à internet via Internet Gateway.
    - Recursos podem se comunicar com a internet (entrada e saída).
    - Exemplos: servidores web, servidores de aplicação.
    - Internet Gateway: conecta a VPC à internet, vincula-se à tabela de rotas e exige IP público nos recursos.

## Aula 19/05/2025
- **VPC Peering**:  
  - Solução simples para conectar duas VPCs (na mesma ou em diferentes regiões).
  - Permite comunicação direta entre VPCs.
  - Não exige Transit Gateway.
  - Limitação: não conecta VPCs em regiões diferentes.
- **AWS Site-To-Site VPN**:  
  - Serviço para criar conexão segura entre rede local e VPC.
  - Utiliza criptografia IPsec.
  - Principais componentes: Customer Gateway (CGW) e Virtual Private Gateway (VGW).
  - Alta disponibilidade: dois túneis VPN.
  - Uso comum: integração de redes corporativas com a nuvem.
  - Fácil configuração e manutenção.
  - Baixo custo, pois utiliza a internet pública.
- **AWS Direct Connect**:  
  - Conexão dedicada entre data center/local físico e AWS.
  - Indicado para grandes volumes de dados e integração híbrida.
  - Cobrança baseada na velocidade da porta e volume de dados transferidos.

## Aula 26/05/2025
- Início do módulo de segurança na AWS.
- **IAM Groups**:  
  - Organiza usuários IAM em grupos com permissões semelhantes.
  - Facilita o gerenciamento de permissões em larga escala.
  - Ideal para equipes, projetos ou departamentos.
  - Criação envolve definir políticas e adicionar membros.
  - Serviço gratuito, parte do IAM.
- **AWS IAM Roles**:  
  - Identidades com permissões temporárias para acesso seguro a recursos AWS.
  - Usadas por serviços AWS (EC2, Lambda) ou aplicações externas.
  - Evita compartilhamento de credenciais permanentes.
- **AWS Cognito**:  
  - Gerencia autenticação e autorização de usuários em aplicações web e mobile.
  - Recursos: registro, login, MFA, integração com provedores sociais.
  - Indicado para apps que exigem autenticação de usuários.
  - Segurança: criptografia de dados e suporte a MFA.
  - Configuração: criação de user pool, definição de políticas e provedores.
  - Cobrança baseada em usuários ativos mensais e operações.

## Aula 29/05/2025
- Continuação do módulo de segurança.
- **Teorema CAP**:  
  - Consistência: todos os nós têm a mesma visão dos dados.
  - Disponibilidade: todos os nós respondem a requisições.
  - Tolerância a partições: sistema opera mesmo com falhas de rede.
  - Não é possível garantir os três ao mesmo tempo; é preciso priorizar dois.
  - Exemplo: bancos relacionais priorizam consistência e disponibilidade; NoSQL, disponibilidade e tolerância a partições.
- **Amazon Inspector**:  
  - Avalia a segurança de instâncias EC2 e contêineres.
  - Realiza varreduras de vulnerabilidades e gera relatórios.
  - Sugere correções e pode ser integrado ao AWS Security Hub.
- **Amazon Detective**:  
  - Analisa e investiga eventos de segurança.
  - Identifica padrões suspeitos na conta AWS.
- **AWS Security Hub**:  
  - Centraliza informações de segurança de vários serviços AWS.
  - Permite visualização e gerenciamento centralizados.
  - Integra-se com outros serviços de segurança (GuardDuty, Inspector, etc.).
  - Permite criação de painéis personalizados.

## Aula 02/06/2025
- Início do módulo de monitoramento.
- **Monitoramento de aplicações**:
  - **Objetivos**:
    - Garantir saúde operacional dos serviços.
    - Monitorar desempenho e uso eficiente dos recursos.
    - Avaliar performance e tempo de resposta das aplicações.
    - Verificar aspectos de segurança operacional.
  - **Amazon CloudWatch**:
    - Serviço de monitoramento para coleta e visualização de métricas e logs.
    - Métricas: gráficos de desempenho (CPU, memória, disco, etc.).
    - Logs são cobrados à parte.
    - Possibilidade de criar métricas personalizadas (serviço pago).
    - Permite configurar alarmes para eventos específicos.
  - **Event Bridge**:
    - Serviço de eventos para criar regras e acionar ações automáticas.
    - Integração com Lambda, SNS, SQS e outros serviços AWS.
    - Permite automação baseada em eventos e métricas.
