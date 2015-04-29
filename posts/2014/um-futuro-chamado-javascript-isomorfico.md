### *Search Engine Optimization, Desempenho, Manutenibilidade entre outras melhorias em sua aplicação JS*

---
Este é, certamente, um tema que tem chamado cada vez mais minha atenção e que, apesar de não ser uma ideia nova — já discutida entre desenvolvedores desde 2011, e desapraticada antes disso — até pouco tempo atrás via muitos desenvolvedores que ainda relutavam em aceitá-la ou então não entendiam a real necessidade de aplicações escritas em código isomórfico.

Algo que me motivou a escrever este post foi o fato de não ter encontrado muito conteúdo — principalmente em português — sobre o tema — até encontrei muitas artigos/documentação sobre frameworks/bibliotecas isomórficas, mas não sobre arquitetura isomórfica em si. Contudo esse post não será algo muito técnico nem fará uma abordagem muito detalhada.

Neste momento você, leitor, deve estar se perguntando “O que exatamente é esse tão falado Javascript isomórfico?” Bem, para ficar mais fácil de entender, eu gostaria de convidá-lo a se lembrar de como era o desenvolvimento web até um tempo atrás e como é hoje em dia.

Antigamente, na experiência de navegação ocorria algo assim: um navegador solicitava uma página em particular e, em seguida, um servidor web retornava uma página HTML hospedada para o solicitante. Isso funcionava bem porque as páginas HTML eram documentos simples, em sua maioria estáticos, e autossuficientes — e os navegadores não tinham de ser muito “poderosos” para que este processo desse certo.

O tempo passou e, depois de muitos avanços, a web tem rompido cada vez mais seus antigos limites — e navegadores web têm evoluído junto para acompanhá-la. Agora, a Web evoluiu para uma plataforma completa, onde fortes padrões HTML5 entre outras tecnologias permitem que os desenvolvedores criem aplicações ricas que antes só eram possíveis em plataformas nativas.

# A ascensão das Single Page Applications (SPAs)

No cenário descrito não demorou muito para que os desenvolvedores começassem a criar aplicações que rodassem inteiramente no navegador usando Javascript e aproveitando todas as evoluções descritas anteriormente. Então frameworks como Backbone.js, Ember.js e AngularJS — muitas vezes referidos como client-side MVC (Model-View-Controller), MVVM (Model-View-ViewModel) ou MVP (Model-View-Presenter) — entre outros nos levaram a uma espécie de boom de SPAs.

A lógica da aplicação passa a viver no cliente, que se comunica com uma API para obter dados. O servidor pode ser escrito em qualquer linguagem e serve uma página de que funciona como um “esqueleto inicial” em HTML. Uma vez que os arquivos Javascript são carregados pelo navegador, a aplicação então é inicializada, busca dados da API, e renderiza o resto da página HTML.

Aplicações agora podiam responder imediatamente às interações do usuário — não havendo mais a necessidade de toda uma “viagem de ida e volta” para o servidor apenas para processar uma nova página — e fornecer interfaces de usuário mais rápidas e interativas do que aplicações web tradicionais.

Isso também era ótimo para os desenvolvedores, pois as SPAs idealizadas tinham uma clara separação de preocupações entre os lados do cliente e o servidor, promovendo um fluxo de desenvolvimento agradável e evitando a necessidade de compartilhar muita lógica entre os dois — que são muitas vezes escritos em diferentes linguagens.

Servidor e cliente ficaram claramente separados. Desenvolvedores Front e Backend precisavam se preocupar cada vez menos um com o outro, e poderiam proceder separadamente. Por isso também não havia problema em escrever a aplicação do servidor e do cliente em diferentes linguagens. Tudo parecia tão perfeito — então por que mudar?

# Alguns problemas das Single Page Applications (SPAs)

## Desempenho

Com a renderização no lado do cliente, o usuário tem que esperar alguns segundos a mais do que teria caso a aplicação apenas solicitasse templates pré-renderizados a partir do servidor. Este efeito pode ser ainda pior em dispositivos móveis como smartphones e tablets — com especificações de hardware mais fracas. E existem vários estudos que mostram o efeito drástico que um site lento tem sobre os usuários — atrasos de apenas algumas centenas de milissegundos podem levar o usuário a deixar a página ou aplicativo.

## Search Engine Optimization (SEO)

Outro ponto que eu penso que mereça ser abordado a favor da renderização do lado do servidor — que eu considero quase tão importante quanto problemas o desempenho — é SEO. Um aplicativo que só pode ser executado no lado do cliente não pode servir HTML para alguns crawlers, uma vez que alguns desses bots não executam Javascript — eles trabalham fazendo uma solicitação para o servidor web e interpretando o resultado. Assim, se o servidor retorna uma página em branco, esta não é de muito valor.

Isso faz com que sua página web tenha naturalmente uma má SEO e, dependendo do caso, até mesmo seja ignorado por motores de busca como o Bing ou Yahoo — com relação ao Google, isso já mudou uma vez que o seu crawler já é capaz de executar Javascript e aplicar CSS.

## Manutenibilidade

Por último, mas não menos importante, temos a manutenibilidade: enquanto o modelo ideal de SPAs pode levar a uma boa — e livre de preocupações — separação entre cliente e servidor, inevitavelmente, parte da aplicação acaba duplicada entre cliente e servidor, muitas vezes em diferentes linguagens. Podemos citar como exemplo disso a formatação de data e moeda, validações de formulários e ainda a lógica de roteamento. Caso não seja bem trabalhado, isso pode acabar tornando com que a manutenção seja mais trabalhosa, especialmente em aplicações mais complexas e que precisam ser escaláveis.

# E como seria uma abordagem Isomórfica?

Em resumo, queremos um híbrido de novas e antigas abordagens: queremos servir HTML totalmente formado a partir do servidor, devido ao desempenho e SEO, mas queremos que a velocidade e flexibilidade que temos com a lógica da aplicação do lado do cliente. Se criássemos as abstrações apropriadas, poderíamos escrever a nossa lógica de aplicação de tal forma que esta seja executada no servidor e no cliente — que é a definição de Javascript isomórfico.

Imagine pelo menos parte da lógica de sua aplicação sendo executada no servidor e no cliente. Pode parecer que não, mas isso abre várias portas: otimizações em desempenho, melhor manutenção, SEO-by-default, entre outras. Mas, para isso, temos importantes conceitos/práticas envolvidos. E aqui estão, resumidamente, alguns que considero mais importantes.

## Abstração

O cliente e o servidor são ambientes muito diferentes, e por isso temos de criar um conjunto de abstrações que possam dissociar nossa lógica de aplicação das implementações subjacentes, para que possamos ter uma única API.

## Renderização de views

Independentemente de optarmos por manipular diretamente o DOM, ficar com templates HTML baseados em strings, ou ainda optar por uma biblioteca de componentes de interface do usuário com uma abstração de DOM, é preciso que a marcação seja gerada isomorficamente. Devemos poder renderizar qualquer view seja no servidor ou no cliente, dependendo das necessidades da nossa aplicação.

## Routing

Em nossa aplicação isomórfica, queremos um único conjunto de rotas que mapeiam padrões URI para manipuladores de rota. Os nossos manipuladores de rota precisam ter acesso a HTTP headers, cookies e informações de URI, além de especificar redirecionamentos sem acessar diretamente window.location (no cliente / browser) ou req/res (no servidor / Node.js).

## Obtenção e persistência de dados

Queremos descrever os recursos necessários para renderizar uma determinada página ou componente independentemente do mecanismo de obtenção de dados. O recurso pode ser um simples URI, que aponte para um endpoint JSON ou, para aplicações maiores, pode ser útil encapsular recursos em modelos e coleções e especificar uma classe modelo e chave primária que, em algum momento, iria ser traduzido para um URI.

# As ferramentas que temos

Nesta seção cito apenas algumas das mais populares bibliotecas e frameworks isomórficas — mas há muitos outros que merecem a sua atenção — e até mesmo algumas horas de estudo.

## Mojito

O Mojito foi o primeiro framework isomórfico de código aberto a receber destaque — e esta é uma das razões que me faz pensar que ele merece um lugar nesta lista. É um framework avançado, full-stack e baseado em Node.js. Destaque para o fato de o Yahoo ter feito um bom trabalho de estender a YUI para lidar com a maior parte do trabalho no lado do servidor —que por outro lado acabou não sendo algo tão vantajoso, uma vez que a sua dependência do YUI e outras especificações do Yahoo levaram a não ter uma popularidade muito boa na comunidade Javascript, desde que seu código foi aberto que em Abril de 2012.

## Rendr

O Rendr é uma pequena biblioteca desenvolvida pelos engenheiros da Airbnb que permite que você execute suas aplicações em Backbone.js sem problemas em ambos o cliente e o servidor (com Node.js). Com ele, você serve páginas HTML completamente renderizadas no servidor, sem perder os benefícios de um client-side feito em Backbone.js.

## Derby.js

O Derby foi projetado para criar SPAs com constante re-renderização de páginas. Para isso, o Derby entende que, se a página é solicitada a partir do servidor, esta tem de ser gerada lá e servida totalmente renderizada — exemplo claro de Javascript isomórfico.

Um ponto negativo que eu encontrei no Derby.js foi a pouca informação sobre este: a documentação não é muito abrangente e eu não encontrei muitos artigos.

## React

O React.js é uma biblioteca Javascript para a construção de interfaces de usuário e, embora hoje em dia seja open source, foi desenvolvida originalmente no Facebook para fins internos. Depois de um tempo, os engenheiros do Facebook perceberam que eles tinham criado algo lindo e decidiram compartilhar o código.

Em minha opinião, existem muitas razões que tornam o React.js uma boa opção como, por exemplo, a capacidade de criar seus próprios componentes, que mais tarde você pode reutilizar e combinar — evitando desgastantes operações de DOM e assim, ganhando eficiência — , e o JSX, que lhe permite misturar HTML com Javascript de uma maneira bem interessante.

Como casos de uso, temos muitos projetos internos do próprio Facebook e, salvo engano meu, o Instagram — que, depois de comprado pelo Facebook, teve sua versão web e sua lógica do lado do servidor reconstruídas em cima do React.js.

## Meteor

O Meteor é, provavelmente, o projeto isomórfico mais conhecido hoje em dia. Ele foi construído para suportar aplicações em tempo real, e a sua equipe — muito bem composta, por sinal — está construindo todo um ecossistema em torno de seu próprio gerenciador de pacotes e suas ferramentas de deploy.

Apesar de sua robustez, é um framework com uma ótima curva de aprendizado — independentemente de se você é leigo ou um “ninja”. E outro ponto a ser destacado é o fato de o Meteor ser voltado à rápida prototipagem — assim, projetos que levariam meses para serem feitos com outras ferramentas, podem ser realizados em bem menos tempo.

Se você é um desenvolvedor Front-End e quer construir uma aplicação web com Node, o Meteor pode ser a resposta para você. Com a template engine do Meteor — conhecida por Blaze — e suas APIs super simples que você pode construir sua aplicação facilmente e em pouco tempo.

Se você já é um “ninja” ou algo do tipo com Node.js e Javascript em geral, o Meteor também pode ser o framework para você. Você pode alterar qualquer parte de sua aplicação em Meteor da maneira que desejar — seja definindo um sistema personalizado de builds ou alterando o seu comportamento em aplicações real-time, o Meteor conta com ótimas APIs.

# Conclusão

Escrever aplicações de grande porte é um trabalho sempre complicado. Encapsular e reutilizar componentes dessas aplicações em ambos o cliente e o servidor torna isso uma tarefa ainda mais complicada. Contudo, aplicações que requerem um alto nível de desempenho, com alta taxa de usabilidade simultânea, têm se tornado cada vez mais comuns e a combinação de renderização em ambos o cliente e o servidor está ganhando cada vez mais espaço como uma solução a tal demanda — o que se fortalece ainda mais à medida que mais organizações de grande porte passam a se sentir “confortáveis” em rodar Node.js em produção.

Ainda assim é importante lembrar que Javascript isomórfico continua algo relativo: pode começar apenas com compartilhamento de templates, passando por toda a camada de interação da aplicação até toda a lógica de negócios da mesma. A maneira como esse compartilhamento de código deve ser feita, e o que do código Javascript de sua aplicação é compartilhado entre o cliente e o servidor, depende inteiramente desta e de seu específico conjunto de requisitos/restrições.

Por fim, gostaria de ressaltar que não penso que esses frameworks venham a substituir os atuais — e de certa forma consolidados — frameworks de SPAs — nem que estes devam ser substituídos. Porém, devido a algumas vantagens que este modelo apresenta e aos avanços em direção a versões estáveis dos frameworks mais “badalados” do universo isomórfico — e as comunidades destes terem crescido cada vez mais —, penso ser inevitável que mais e mais aplicações web comecem a compartilhar código entre seu cliente e servidor — e vejo isto com bons olhos.

*Originalmente postado em [Um futuro chamado Javascript Isomórfico](https://medium.com/pensamentos-js/um-futuro-chamado-javascript-isomorfico-fa43af60d132).*
