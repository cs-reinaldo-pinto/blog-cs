**Meu primeiro Lambda AWS**
======
![tag1](./imagens/img01.jpeg)

Olá pessoal, objetivo do post, é auxiliar novos usuários da AWS que tem dúvidas sobre o Lambda.

#### Que tal começarmos explicando “O que é Lambda?!""

Para resumir, é uma plataforma "Server-less" da AWS que executa funções de código, sem a necessidade de ter uma infraestrutura, seu código só executado quando invocado. Chamamos de "Função do Lambda", quando o Lambda for invocado, isso quer dizer que seu código foi executado. Usado como serviço stateless. No blog tem outros posts sobre Lambda que pode enriquecer o conhecimento sobre Lambda [clique aqui.](http://www.concretesolutions.com.br/?s=lambda&post_type=post)

#### Ta bom! Mas, quando usar?

No caso de uma arquitetura baseada em micro-serviços será o ideal.

Mas uma recomendação verifique se seu código está coeso, atende aos requisitos mínimo de patterns e modularização, nossa agora complicou né, haha. 😅

Calma, resumindo podemos quebrar nossa aplicação e colocarmos algum modulo no Lambda, por exemplo: A granularidade pode separar o modulo de login, será que é necessário este serviço rodar 24x7x360 em uma VM ?! Isso é desperdício de recurso, dinheiro gasto sem necessidade. Para resolver isso podemos usar um Lambda. Mas lembre-se devemos tratar o Lambda como serviço stateless.

Por se tratar de um serviço gerenciado pela AWS, usamos quando não queremos se preocupar com a infraestrutura e escalabilidade. Sem esquentar com atualização de Sistema Operacional, bugs e etc. Você so precisa determinar a quantidade de memória e o Lambda cuida do resto, CPU, Disco e IO.

Obs, obtenha métricas ou levante todos requisitos necessários para determinar a melhor arquitetura.

Dois exemplos simples de um arquitetura usando Lambda:

![tag2](./imagens/arqaws01)

![tag2](./imagens/arqaws003)


Alguns cases de sucesso [clique aqui.](https://aws.amazon.com/pt/solutions/case-studies/all/)

#### E o custo?

Isso é o mais interessante, muitas vezes esse serviço sera gratuito. Serio? Sim, a AWS disponibiliza para alguns serviços um "nível gratuito", no caso do Lambda até 1 milhão de execuções (invocação) e 400.000 GB/segundo de tempo de memória usada por mês.
Excedendo o nível gratuito, você só paga pelo tempo de execução, o tempo de execução não conta o tempo de iniciar a "instância", e sim a partir do momento que seu código inicia e termina, isso é demais.
Mas lembre-se seu código teve ficar armazenado em algum lugar! O Lambda armazena no s3, e isso pode gerar um custo baixo. Para detalhes [clique aqui.](https://aws.amazon.com/pt/lambda/pricing/)

#### Nossa marotão 😎 haha!!! Mas o que eu preciso para criar um Lambda?

Aqui tem uma parte chatinha, mas muito importante, você deve criar policies e associar a uma role, com os níveis de permissões necessário, garantindo ainda mais segurança e deixando uma arquitetura muito mais justa. Para detalhes [clique aqui.](http://docs.aws.amazon.com/pt_br/lambda/latest/dg/access-control-identity-based.html)

#### Como nada é perfeito, vejamos alguns pros:

- Não tem suporte para todas linguagens.
- Não esta disponível em todas regiões da AWS.
- Possui limite de memória, isso pode implicar na performance dependendo da sua aplicação.

---
Criando meu primeiro Lambda
========
Acesse o console da AWS e localize o serviço Lambda:

![tag3](./imagens/img001.png)

A AWS fornece "blueprint", templates para auxiliar.
Selecione "Blank Function":

![tag4](./imagens/img002.png)

O Lambda trabalha com triggers, muito útil com integrações com outros serviços da AWS, por exemplo o S3. No nosso blog tem alguns exemplos [clique aqui.](http://www.concretesolutions.com.br/?s=lambda&post_type=post)
Mas nesse momento não vamos associar uma trigger:

![tag5](./imagens/img003.png)

Adicione as configurações necessárias, conforme exemplo abaixo:

![tag6](./imagens/img004.png)

Coloque o código conforme exemplo, repositório [clique aqui.](exemplo):

![tag7](./imagens/img008.png)

Na ultima release da AWS, o Lambda recebeu algumas funcionalidades, uma delas é variável de ambiente.
Selecione a Role (criada para o Lambda), quantidade de memória e tempo para execução do código, com limite até 5 minutos, exemplo:

![tag7](./imagens/img005.png)

"DLQ Resource", voce pode usar para caso de falha seja encaminhado para uma fila e ser reprocessado mais tarde ou enviar uma notificação por e-mail.



Network, selecione a VPC criada para exibir as subnets. É recomendado adicionar duas subnets sendo elas privadas e de zona de disponibilidade diferentes. Também é importante lembrar que o Lambda é um recurso usado em backend, por isso não é necessário adicionar subnet pública.
Selecione um ou mais "Security Groups":

![tag8](./imagens/img006.png)

Integração com KMS, é possível criptografar as variáveis de ambiente. Você pode associar um KMS em uso na conta.
Finalizado a configuração, aperte "Next":

![tag9](./imagens/img007.png)

Valide as configurações e selecione "Create Function":

![tag10](./imagens/img0012.png)

Após criado, podemos testar nosso código.
Na opção "Actions", selecione "Configure test event":


![tag10](./imagens/img009.png)

Coloque os dados abaixo e selecione a opção "Save and test":

![tag10](./imagens/img0010.png)

Resultado do teste:

![tag10](./imagens/img0011.png)

Faça outro teste com seu nome e sobre nome e verifique o retorno. 😆
_______
Espero que o post ajude os iniciantes no mundo de cloud computing com o Lambda AWS.

##### Feedbacks são bem-vindo!!! Abraços 😘!!
