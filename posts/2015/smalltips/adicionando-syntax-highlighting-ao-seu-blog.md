Fala galera! Esse post inaugura ~~outra seção que não manterei~~ mais uma *hashtag* aqui no blog: **#smalltips**, onde pretendendo, como o nome sugere, trazer dicas curtas e bem rápidas mesmo ~~(diferente dos longos e entediantes posts de sempre)~~.

A ideia do post de hoje surgiu quando pedi feedback sobre um post aqui do blog a um amigo meu e, para minha surpresa, um dos principais pontos que ele destacou não dizia respeito ao conteúdo do post em si, mas para um aspecto presente no blog: **a falta de syntax highlighting nos snippets de código**. Sim, eu tinha deixado passar esse detalhe. ~~*"Que burro, dá zero pra ele."*~~

Enfim, vamos ao que interessa! No caso do meu blog, este é feito com [Ghost](https://github.com/tryghost/Ghost), e muitos temas disponíveis não acompanham *syntax highlighting* - inclusive o que eu escolhi de base pra fazer o meu em cima. Caso sua *blog engine* ou *static generator*, e o tema que você usa no seu blog, já tenha suporte a *syntax highlighting*, não há nada para se fazer além de marcações corretas ao se incluir um snippet de código em seu post. Caso não, este post é pra você.

Em geral, incluir uma biblioteca para fazer *syntax highlighting* em si é um trabalho do seu tema. Como estamos assumindo que este não o fez, faremos nós mesmos :)

Para isso, precisamos de uma biblioteca de *syntax highlighting*. Há várias opções boas, incluindo [prism.js](http://prismjs.com/), [SyntaxHighlighter](http://alexgorbatchev.com/SyntaxHighlighter/), [Rainbow](https://craig.is/making/rainbows) e o [highlightjs](https://highlightjs.org/). Por motivos ligados princpalmente ao número de linguagens (~125) e estilos (~63) suportados, acabei optando por usar o *highlightjs*.

Incluí-lo no seu blog se resume a quatro simples passos. Dentro do blog, vá para a pasta onde fica o seu tema - no meu caso `ghost/content/themes/...` - e procure algum template *default* - no meu caso: `default.hbs`. Dentro desse arquivo, precisamos:

- Incluir um arquivo CSS do tema que você gosta:

```html
<link rel="stylesheet" type="text/css" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/8.2/styles/meu_tema_favorito">
```
Uma lista completa de temas e linguagens suportados - e seus links - pode ser encontrada [aqui](http://cdnjs.com/libraries/highlight.js/).

- Incluir a biblioteca do HighlightJs:

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/8.6/highlight.min.js"></script>
```

- Inicializar a biblioteca do HighlightJs:

```html
<script>hljs.initHighlightingOnLoad();</script>
```

==Nesse momento==, dentro de seu *head*, devemos ter algo assim:

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/8.6/styles/monokai_sublime.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/8.6/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>
```

- Usar nos posts :)

Para usá-lo, basta adicionar a marcação correta (de acordo com a linguagem desejada) em cada snippet de código, com uma algo como

```html
<pre ><code class="html"> Seu código aqui </code></pre>
```
Bem amigos, por hoje é isso. Caso tenha alguma dúvida, sugestão de melhoria ou correção para este post - ou outro - é só comentar :)
