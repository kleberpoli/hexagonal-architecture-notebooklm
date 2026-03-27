# Arquitetura Hexagonal com NotebookLM

## Contexto

Este projeto foi desenvolvido como parte de um desafio da DIO com o objetivo de utilizar Inteligência Artificial (NotebookLM) como ferramenta de aprendizagem ativa.

O tema escolhido foi **Arquitetura Hexagonal (Ports and Adapters)**, uma abordagem arquitetural que promove desacoplamento, testabilidade e independência de frameworks.

## Objetivos

- Compreender os fundamentos da Arquitetura Hexagonal
- Identificar seus principais componentes (Core, Ports e Adapters)
- Comparar com outras arquiteturas (MVC, Clean Architecture)
- Aplicar o conceito em cenários reais de backend
- Construir um material de referência reutilizável

## Curadoria de Fontes

As fontes abaixo foram utilizadas no NotebookLM para geração de insights e resumos:

### Artigos e Documentação

1. https://engsoftmoderna.info/artigos/arquitetura-hexagonal.html
2. https://alistair.cockburn.us/hexagonal-architecture/
3. https://medium.com/@marcio.kgr/arquitetura-hexagonal-8958fb3e5507
4. https://docs.aws.amazon.com/pt_br/prescriptive-guidance/latest/cloud-design-patterns/hexagonal-architecture.html
5. https://www.thoughtworks.com/insights/blog/architecture/demystify-software-architecture-patterns
6. https://medium.com/netflix-techblog/ready-for-changes-with-hexagonal-architecture-b315ec967749
7. https://scalastic-io.translate.goog/en/hexagonal-architecture/?_x_tr_sl=en&_x_tr_tl=pt&_x_tr_hl=pt&_x_tr_pto=tc

### Vídeos (YouTube)

1. https://www.youtube.com/watch?v=bDWApqAUjEI
2. https://www.youtube.com/watch?v=yDzQsXM8aSM
3. https://www.youtube.com/watch?v=JubdZIdLQ4M
4. https://www.youtube.com/watch?v=7SaA3HCOc4c
5. https://www.youtube.com/watch?v=92eWCQrcsvQ
6. https://www.youtube.com/watch?v=1PMCPgRIqNE

## Uso do NotebookLM

### Estrutura do Notebook

- Tema: Hexagonal Architecture: Mastering Ports and Adapters
- Fontes carregadas: artigos e vídeos acima
- Objetivo: sintetizar conhecimento e gerar explicações aplicáveis

## Engenharia de Prompts

### Prompt 1 — Conceito

**Pergunta:** O que é Arquitetura Hexagonal e quais são seus principais componentes?

**Resposta:**

A Arquitetura Hexagonal, também conhecida como Ports and Adapters (Portas e Adaptadores), é um padrão de arquitetura de software criado por Alistair Cockburn em 2005. Seu objetivo principal é desacoplar a lógica de negócio central da aplicação de componentes externos, como interfaces de usuário (UI), bancos de dados e frameworks. Nesse modelo, a aplicação é visualizada como um hexágono onde o "interior" contém a lógica pura de negócio, protegida de mudanças tecnológicas no "exterior". Isso permite que o sistema seja testado de forma isolada e que tecnologias externas sejam trocadas com baixo impacto no código principal.

Os principais componentes desta arquitetura são:

1. Domínio ou Core (O interior do Hexágono)
É o coração da aplicação, onde residem as regras de negócio, entidades e casos de uso. O domínio deve ser totalmente independente de tecnologia, não contendo anotações de frameworks ou referências a bancos de dados específicos. Ele define como o sistema funciona, independentemente de como ele é acessado.

2. Portas (Ports)
As portas são interfaces que definem o contrato de comunicação entre o domínio e o mundo externo. Elas são independentes de tecnologia e ficam localizadas no limite do hexágono interno.
Existem dois tipos:
- Portas de Entrada (Driving/Primary): Definem os serviços que a aplicação oferece ao mundo exterior. São chamadas por atores externos para iniciar uma ação no sistema (ex: uma interface de API).
- Portas de Saída (Driven/Secondary): Definem os serviços que a aplicação precisa do mundo exterior para funcionar, como persistência de dados ou envio de e-mails.

3. Adaptadores (Adapters)
São classes concretas que implementam as portas ou as utilizam para traduzir conversas técnicas em chamadas que a aplicação entende.
- Adaptadores Primários (Driving): Convertem requisições externas (como um JSON de uma API REST ou um comando de console) em chamadas para as portas de entrada do domínio.
- Adaptadores Secundários (Driven): Implementam as interfaces das portas de saída para interagir com tecnologias específicas, como um banco de dados SQL, um sistema de arquivos ou um serviço de mensageria.

4. Atores
Embora externos ao hexágono, os atores interagem com ele.
- Atores Primários: Aqueles que "dirigem" a aplicação, como usuários humanos ou scripts de teste automatizados.
- Atores Secundários: Aqueles que são "dirigidos" pela aplicação para obter respostas ou notificações, como servidores de banco de dados.

---

### Prompt 2 — Comparação

**Pergunta:** Compare Arquitetura Hexagonal com Clean Architecture e MVC, destacando vantagens e desvantagens

**Resposta:**

A comparação entre a Arquitetura Hexagonal, a Clean Architecture e o padrão MVC revela diferentes níveis de abstração e complexidade, embora todas busquem organizar o código para facilitar o desenvolvimento.

1. Arquitetura Hexagonal vs. Clean Architecture
A Clean Architecture (Arquitetura Limpa) é frequentemente descrita como uma evolução ou especialização da Arquitetura Hexagonal. Ambas compartilham o princípio fundamental de isolar a lógica de negócio no centro, com as dependências apontando sempre para dentro.

- Diferenças de Estrutura: Enquanto a Arquitetura Hexagonal foca na separação entre o "dentro" (domínio) e o "fora" (infraestrutura) através de portas e adaptadores, a Clean Architecture é mais prescritiva, definindo camadas específicas com nomes como "Entidades", "Casos de Uso" e "Adaptadores de Interface".
- Complexidade: A Clean Architecture tende a ser mais complexa por exigir uma separação de preocupações ainda mais explícita (como a distinção entre regras de negócio corporativas e da aplicação), o que a torna conhecida como "Screaming Architecture" por deixar sua intenção evidente. A Hexagonal é vista como mais simples e flexível por não impor nomes rígidos às camadas.

2. Arquitetura Hexagonal vs. MVC
O MVC (Model-View-Controller) é um padrão tradicional focado na separação de componentes para interface de usuário, enquanto a Arquitetura Hexagonal foca no isolamento total da lógica de negócio.
- Ponto de Foco: No MVC, a lógica muitas vezes acaba "vazando" para o Controller ou para a View, gerando alto acoplamento. Na Hexagonal, o domínio é o centro e não conhece nada sobre a interface (View) ou o banco de dados (Model tradicional), protegendo-o de mudanças técnicas.
- Simetria: O MVC é assimétrico (focado no usuário), enquanto a Hexagonal trata todos os atores externos (usuários, bancos de dados, testes) de forma simétrica através de portas e adaptadores.

3. Vantagens e Desvantagens

| Arquitetura       | Vantagens        | Desvantagens        |
|-------------------|------------------|---------------------|
| Hexagonal         | Testabilidade isolada sem DB/UI; flexibilidade para trocar tecnologias (ex: mudar SQL para NoSQL); baixo acoplamento. | Complexidade inicial elevada; excesso de código (boilers) e pacotes para projetos simples; potencial latência devido às camadas. |
| Clean             | Limites claros e explícitos; alta manutenibilidade a longo prazo; segue rigorosamente os princípios SOLID. | Curva de aprendizado íngreme; pode ser um overkill para microserviços pequenos ou funções serverless. |
| MVC               | Simplicidade de implementação inicial; padrão amplamente conhecido e suportado por frameworks. | Risco de acoplamento forte; difícil de testar a lógica sem a infraestrutura; lógica de negócio espalhada por várias camadas. |

Em resumo, a escolha depende do contexto: para aplicações pequenas, o MVC ou uma abordagem simples pode bastar; para sistemas complexos onde a lógica de negócio deve ser protegida de mudanças tecnológicas e testada exaustivamente, a Hexagonal ou a Clean Architecture são preferíveis.

---

### Prompt 3 — Aplicação Prática

**Pergunta:** Como aplicar Arquitetura Hexagonal em um projeto de backend usando Java ou Node.js?

**Resposta:**

Para aplicar a Arquitetura Hexagonal (ou Ports and Adapters) de forma objetiva em Java ou Node.js, o foco deve ser o isolamento da lógica de negócio e a garantia de que as dependências apontem sempre para o "interior" do sistema.

1. Organize o projeto em camadas claras
Divida o código para separar o que é regra de negócio do que é tecnologia externa:
- Domínio (Core): Contém as entidades e regras de negócio puras. Não deve possuir dependências ou anotações de frameworks (como JPA, Spring ou Express).
- Aplicação: Define os Casos de Uso (orquestração da lógica) e as Portas.
- Infraestrutura: Onde residem os Adaptadores técnicos (banco de dados, APIs externas, configuração).

2. Defina Portas (Interfaces) no centro
As portas são interfaces que definem o contrato de comunicação entre o domínio e o mundo externo:
- Portas de Entrada (Driving): Interfaces que expõem as funcionalidades do sistema (ex: CriarProdutoPort).
- Portas de Saída (Driven): Interfaces que o sistema usa para interagir com o exterior (ex: ProdutoRepositoryPort).

3. Implemente os Adaptadores na periferia
Os adaptadores traduzem requisições tecnológicas para as portas do domínio:
- Adaptadores de Entrada: Controladores REST (Spring @RestController em Java ou rotas Express em Node.js) chamam as portas de entrada.
- Adaptadores de Saída: Classes que implementam as interfaces de saída para persistência (ex: usando JPA/Hibernate ou repositórios em memória).

4. Gerencie a Injeção de Dependências
Como o domínio é isolado de frameworks, a injeção deve ser configurada externamente:
- Em Java/Spring: Use uma classe @Configuration para instanciar manualmente as classes do domínio como Beans, injetando nelas os adaptadores de infraestrutura.
- Em Node.js: Injete manualmente as instâncias dos repositórios ou serviços de infraestrutura no construtor dos casos de uso ao iniciar a aplicação.

Principais Benefícios Práticos
- Testabilidade: Você pode testar toda a lógica de negócio de forma isolada usando Mocks para as portas de saída, sem precisar de banco de dados ou servidores ativos.
- Flexibilidade: Permite trocar o banco de dados (ex: de SQL para MongoDB) apenas criando um novo adaptador de saída, sem tocar em uma única linha da regra de negócio.

---

### Prompt 4 — Erros Comuns

**Pergunta:** Quais são os erros comuns ao implementar Arquitetura Hexagonal e como evitá-los?

**Resposta:** 

Ao implementar a Arquitetura Hexagonal, os desenvolvedores frequentemente enfrentam desafios que podem comprometer os benefícios de desacoplamento e testabilidade do sistema. Abaixo estão os erros mais comuns e as estratégias para evitá-los:

1. Infiltração de Lógica de Negócio em Camadas Externas
Um dos erros mais clássicos é permitir que a lógica de negócio "vaze" para os adaptadores de interface de usuário (UI) ou de persistência. Isso ocorre quando regras de decisão são colocadas em controladores REST ou em procedimentos armazenados no banco de dados.
Como evitar: Garanta que todas as regras de negócio residam exclusivamente no hexágono interno (domínio). Utilize testes de regressão automatizados para detectar se novas funcionalidades estão quebrando esse isolamento e forçando a lógica para a periferia.

2. Dependência de Frameworks e Tecnologias no Domínio
É comum encontrar anotações de frameworks (como @Service do Spring) ou de persistência (como @Entity do JPA) dentro das classes de domínio. Isso acopla o coração da aplicação a uma tecnologia específica, dificultando trocas futuras e testes isolados.
Como evitar: Mantenha o domínio como código puro (Plain Old Objects), sem dependências externas. Para persistência, crie uma entidade de banco de dados separada do modelo de domínio e use adaptadores para converter um no outro. Para injeção de dependência, utilize uma classe de configuração externa para instanciar os beans do domínio.

3. Casos de Uso Acoplados à Tecnologia
Escrever casos de uso que contêm detalhes íntimos da tecnologia externa (como formatos de mensagens específicos ou nomes de tabelas) torna o sistema rígido e difícil de manter.
Como evitar: Escreva os casos de uso na fronteira da aplicação (hexágono interno), focando apenas no propósito da conversa e nos eventos suportados, independentemente da tecnologia que os dispara.

4. Overengineering em Projetos Simples (Overkill)
Aplicar a complexidade de portas e adaptadores em aplicações muito pequenas, como funções serverless simples, pode gerar uma sobrecarga de manutenção desnecessária e excesso de pacotes.
Como evitar: Avalie a complexidade e a estabilidade das regras de negócio. Se a aplicação for pequena ou se as regras forem triviais, arquiteturas mais simples podem ser preferíveis. A Arquitetura Hexagonal brilha quando a lógica de negócio é complexa e precisa ser protegida de mudanças técnicas frequentes.

5. Falta de Compreensão do Domínio antes da Codificação
Tentar isolar a lógica de negócio sem entender profundamente os atores, casos de uso e regras pode levar a erros custosos de modelagem.
Como evitar: Antes de codificar, identifique claramente os atores primários (quem inicia a ação) e secundários (quem é acionado pelo sistema), definindo bem os contratos (portas) para cada interação necessária.

6. Problemas de Latência e Performance
O uso excessivo de camadas, portas e adaptadores, especialmente se cada hexágono se comunicar via rede ou APIs, pode introduzir latência no sistema.
Como evitar: Seja criterioso ao dividir a aplicação em múltiplos hexágonos (microserviços). Agrupe funcionalidades que pertencem ao mesmo domínio para evitar chamadas de rede desnecessárias e use o padrão apenas onde a flexibilidade tecnológica for realmente um requisito.

---

## Cicatrizes (Aprendizados)

Durante o uso do NotebookLM, não foram identificados erros críticos, mas sim limitações relacionadas à qualidade das respostas geradas a partir dos prompts iniciais.

### Principais pontos observados:

- Respostas excessivamente conceituais e extensas
- Baixa presença de exemplos práticos aplicáveis
- Explicações pouco objetivas para uso em contexto real de desenvolvimento

### Diagnóstico

O principal fator identificado foi a **falta de especificidade nos prompts**, o que levou a respostas mais genéricas e acadêmicas.

### Soluções aplicadas

- Refinamento dos prompts para maior direcionamento, incluindo:
  - Solicitação de respostas mais objetivas e resumidas
  - Pedido explícito por exemplos práticos
  - Uso de analogias para facilitar entendimento
  - Contextualização técnica (ex: backend, APIs REST)

### Exemplo de melhoria de prompt

**Antes:**

> O que é Arquitetura Hexagonal e quais são seus principais componentes?

**Depois:**

> Explique de forma objetiva o que é Arquitetura Hexagonal, destacando seus principais componentes (Domínio, Portas e Adaptadores) e forneça um exemplo prático de como eles se relacionam em um cenário de backend (API Rest em Java).

### Insight chave

A qualidade das respostas geradas por IA está diretamente ligada à clareza, contexto e restrições definidas no prompt.

Prompts bem estruturados resultam em respostas mais úteis, aplicáveis e alinhadas ao contexto profissional.

## Miniguia de Estudo

### Resumo Estruturado

A Arquitetura Hexagonal (Ports and Adapters) é um modelo que separa o núcleo da aplicação das dependências externas, garantindo desacoplamento e maior testabilidade.

**Principais componentes:**
- **Core:** regras de negócio puras
- **Ports:** interfaces que definem comunicação
- **Adapters:** implementações externas (banco, APIs, UI)

**Fluxo:**
`Entrada → Adapter → Port → Core → Port → Adapter → Saída`

**Quando usar:**
- Sistemas complexos
- Necessidade de testes isolados
- Alto desacoplamento de infraestrutura

### Glossário

- **Arquitetura Hexagonal:** modelo que isola o domínio das dependências externas  
- **Port:** interface que define entrada/saída do sistema  
- **Adapter:** implementação concreta de um port  
- **Core (Domínio):** lógica de negócio independente  
- **Dependency Inversion:** dependências apontam para o núcleo, não para fora  
- **MVC (Model-View-Controller):** Padrão arquitetural que separa a aplicação em três camadas: Model (dados), View (interface) e Controller (lógica de controle), facilitando organização e manutenção.
- **Clean Architecture:** Abordagem arquitetural que organiza o sistema em camadas independentes, onde regras de negócio são isoladas de frameworks e detalhes externos, seguindo o princípio de inversão de dependência.
- **Node.js:** Ambiente de execução JavaScript no lado do servidor, baseado em eventos e orientado a I/O assíncrono, amplamente utilizado para APIs e aplicações escaláveis.
- **Java:** Linguagem de programação orientada a objetos, fortemente tipada, amplamente utilizada em aplicações corporativas, backend e sistemas distribuídos.

### Prompts Reutilizáveis

- Explique `[conceito]` de forma objetiva com exemplo prático em backend
- Compare `[X]` vs `[Y]` destacando vantagens, desvantagens e quando usar
- Liste erros comuns ao aplicar `[tecnologia]` e como evitá-los
- Gere um exemplo simples usando `[linguagem/framework]`
- Explique como aplicar `[conceito]` em uma API REST