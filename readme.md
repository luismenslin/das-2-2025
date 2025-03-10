## Bruto

Cache = Informação armazenada na memória com o intuito de ser mais rapida do que o HD


Banco de dados relacional tem um planejador de query

Banco de dados não relacional executam a query na chave ou no indice

Exemplo Site da Univille:
    Para superar as limitações da linguagem de programação e melhorar a experiencia dos usuários, precisamos de mais maquinas (PHP com o limite de Treads, Java com a instancia de objetos, etc) 
        Ganhar disponibilidade/Ganhar performance = Gastar mais dinheiro


Automatização de ambiente
    - Amazon Cloud Watch -> Monitora se a maquina está 

Terraform - Foda pra infraestrutura como código

Trade-offs
São as trocas e escolhas que acontecem durante a construção de uma arquitetura.

Consistência
Garantia de que os dados serão persistidos em uma transação.

Durabilidade
Fazer os dados persistirem e durarem.

Cache
Memória temporária de fácil acesso (Guarda dados na memória RAM).

Espaço
A Terceira Forma Normal (3FN) é uma técnica de normalização de bancos de dados que garante que cada atributo de uma tabela depende apenas da chave primária (Serve para reduzir redundância e diminuir espaço de armazenamento).

Banco de dados não relacionais
Banco de dados não relacionais não fazem normalização, abrem mão do espaço para aumentar performance.

Implementando escalabilidade
Aumento da disponibilidade

Melhora da experiência de usuário

Aumento dos gastos com as máquinas

Automatizando provisionamento de recursos: AWS Cloud Watch.

Iac - Infraestutura como Código
Provisionando sua infraestrutura computacional usando código (scripts) utilizando código ao invés de utilizar processos manuais. AWS possui o AWS CloudFormation para escrever os scripts
Tratar os recursos como descartáveis
Usar a vantagem oferecida pelo provisionamento dinâmica dos recursos.

## Resumo do Bruto
## Aula 27/02/2024

**Trade-offs**
São as trocas e escolhas que acontecem durante a construção de uma arquitetura. 

**Consistência**
Garantia de que os dados serão persistidos em uma transação.

**Durabilidade**
Fazer os dados persistirem e durarem.

**Cache**
Memória temporária de fácil acesso (Guarda dados na memória RAM).

**Espaço**
A Terceira Forma Normal (3FN) é uma técnica de normalização de bancos de dados que garante que cada atributo de uma tabela depende apenas da chave primária (Serve para reduzir redundância e diminuir espaço de armazenamento).

**Banco de dados não relacionais**
Banco de dados não relacionais não fazem normalização, abrem mão do espaço para aumentar performance.

**Implementando escalabilidade**
- Aumento da disponibilidade
- Melhora da experiência de usuário
- Aumento dos gastos com as máquinas

- Automatizando provisionamento de recursos: AWS Cloud Watch.

**Iac - Infraestutura como Código**
- Provisionando sua infraestrutura computacional usando código (scripts) utilizando código ao invés de utilizar processos manuais. AWS possui o AWS CloudFormation para escrever os scripts
- Terraform; Tofu

**Tratar os recursos como descartáveis**
- Usar a vantagem oferecida pelo provisionamento dinâmica dos recursos.

## Aula 06/03/2024

**Baixo Acoplamento**
- Ter pouca depêndencia entre os componentes do software para evitar falhas.
- Para ter alta disponibilidade é necessário ter redundância  (Várias istâncias de banco, load balancer etc)

**Arquiteturar serviços e não servidores**
- Não limitar a arquitetura aos servidores, considerar a utilização de container, serverless.

**Escolher a opção correta de banco**
- Banco de dados relacional: Problemas com escalabilidade horizontal.
- Chega um momento que a escalabilidade horizontal não dá conta da necessidade, pois muitas das cópias servem apenas para leitura.
    - Escalabilidade horizontal: aumentar instância (servidor).
    - Escalabilidade vertical: aumentar hardware.

- NoSQL: Facilmente escalavel, pois as instâncias não são apenas de leitura.

**Evitar pontos únicos de falha**
- Aumentar instâncias
- Assumir que tudo falha e se preparar para a falha.
 
**Otimizar o custo**
- Tirar vantagem da flexibilidade da nuvem para aumentar sua eficiência de custo.
- Evitar exageros de arquitetura, utilizar somente recursos que são necessários.

**Usar cash**
- Minimiza as operações de banco de dados ao busca-los de regiões de cash próximas do usuário 
- Amazon CloudFront interage como esse intermediador entre usuário --> internet --> Amazon CloudFront --> S3

**Segurança**
- Utilizar mais de uma ferramenta de segurança.
- Usar o princípio do privilégio mínimo.

