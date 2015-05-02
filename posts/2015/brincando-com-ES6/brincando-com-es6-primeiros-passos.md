Bem amigos, muitos de vocês, desenvolvedores, sabem que o Javascript tem chamado cada vez mais atenção nos últimos anos - inclusive de empresas como [Microsoft, IBM e Linux Foundation, que anunciaram apoio ao Node.js](http://venturebeat.com/2015/02/10/joyent-joins-with-ibm-microsoft-the-linux-foundation-to-form-the-node-js-foundation/), recentemente. 

E, muitos de vocês também devem devem ter ouvido falar da [última versão do JavaScript](http://tc39wiki.calculist.org/es6/), conhecida também como ECMAScript 6 ou apenas ES6, que, em meio a um constante avanço do JavaScript, busca trazer recursos cada vez mais modernos para o mesmo.

Como gosto de sempre estudar e evangelizar coisas legais, então decidi criar essa nova série de posts onde, ao longo das próximas semanas, estaremos fazendo uma introdução ao padrão ES6.

Ao longo dos posts serão apresentados recursos utilizados em sites como o [ES6 Fiddle](http://www.es6fiddle.net/). Eu particularmente recomendo que você procure ao máximo *brincar* com eles para ter certa noção de um *futuro que já não é tão futuro assim*.

Estes são alguns dos conceitos/recursos que serão explorados ao longo da série - não necessariamente nessa ordem:

- Arrow Functions; 
- `let` keyword e Block Scoping
- Destructured Arrays & Objects
- Promises; Rest parameters; Sets
- Classes e hierarquia; parâmetros default
- Generators; Iterators; Maps
- **Muitas** outras coisas legais :)

<iframe src="//giphy.com/embed/7pZSFcwBv3Bde?html5=true" width="480" height="384" frameBorder="0" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>

Queira você já tenha certo conhecimento sobre ES6, ou queira você nem sequer faça ideia do que seja ECMAScript, essa série de posts é pra você!

Sei que você deve estar bem ansioso pra ver todas essas coisas legais ~~ou não~~, mas como a série de posts visa a tratar desde o bem básico, vamos começar entendendo a especificação ECMA, algumas considerações importantes antes de decidir por ES6, e como usar ES6 **hoje**.

# O que é ECMAScript?

Bem, o ECMAScript 6 (ES6, muitas vezes referido como *Harmony*) é o sexto grande release da especificação da linguagem ECMAScript. ECMAScript é o nome *apropriado* para a linguagem que conhecemos por JavaScript (<3).

O [projeto da especificação](https://people.mozilla.org/~jorendorff/es6-draft.html) ES6 é atualizado regularmente e é uma ótima maneira de se familiarizar com os detalhes da linguagem. Se você estiver interessado em saber que rumos a especificação está tomando, há lugares bem interessantes, como o [ES Wiki](http://wiki.ecmascript.org/doku.php).


# Considerações antes de optar por ES6

Antes de você decidir usar ES6 em sua aplicação - em produção, e sem ser apenas para fins de estudo -, há dois *questionamentos-chave* que penso eu serem importantes:

## *Há uma preocupação com as constantes mudanças na especificação ES6?*

Temos que trabalhar com fatos: a especificação ES6 ainda não está completamente concluída, e por isso, o funcionamento/comportamento de certas características podem mudar facilmente. Isto significa que as ferramentas que você utiliza para fazer com que determinadas features do ES6 funcionem na versão atual do JavaScript também podem mudar - e quebrar seu código existente. Se você pensa que possíveis mudanças na especificação - e respectivamente, quebra de código, sejam uma preocupação importante em sua aplicação, recomendo que pense um pouco mais antes de usar ES6 em produção.

## *Quais são as plataformas que almejo? Há uma necessidade de manter compatibilidade com dispositivos e navegadores mais antigos?*

As plataformas que sua aplicação visa a atingir - dispositivos, navegadores etc. - devem ser levadas em conta ao decidir pelo uso de ES6. Se você é um ~~pobre coitado, sofredor, frustado~~ desenvolvedor que **ainda** tem de lidar com navegadores como IE6 ou IE7, então você pode acabar tendo de usar apenas um subset de recursos ES6. 

E outro ponto: usar ES6 requer um *transpiler* ou um *shim* (abordaremos com mais detalhes mais adiante). Se você precisa usar um transpiler, ele vai afetar tanto a sua capacidade de depurar o código quanto seu próprio desempenho. Mais aprofundadamente: 

### Depuração

Se você usa um *transpiler*, este irá gerar arquivos JS compilados que, às vezes, podem ser consideravelmente difíceis de se entender - o que pode tornar dificultar um pouco a depuração. 

Felizmente, navegadores modernos suportam *source maps* - o que significa que você, em teoria, não precisaria se preocupar com esse aspecto, uma vez que o *source map* permite com que você veja o código ES6 original, em vez do código compilado para ES5. 

Porém, se você almeja plataformas - ou browsers - mais antigas, isso pode ser um problema - uma vez que elas podem não suportar *source maps*. Muitos navegadores mais antigos até suportam a especificação ES5 muito bem - e o código gerado vai funcionar neles, mas se você precisar depurar nestes, pode vir a ter dores de cabeça.

### Desempenho

Os transpilers ES6 em geral não fazem otimizações de desempenho com base no navegador a executar o código. Em alguns casos, isto pode resultar em código que não executa tão bem em alguns navegadores. Se você está trabalhando em algo que precisa ter um desempenho muito elevado, tais como jogos, o JavaScript *padrão* pode ser a melhor opção. No entanto, isto não significa que você não deve usar ES6 em tudo: você pode muito bem simplesmente evitar o uso de recursos ES6 em determinadas partes do seu código que podem ser consideradas *críticas*.

# Transpilers? Shims?

<iframe src="//giphy.com/embed/PrAMyghZaYjm?html5=true" width="480" height="281" frameBorder="0" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>

Então, após se questionar as perguntas anteriores, você optou por usar ES6. *Mas por onde começar?* Bem, você precisa fazer uma escolha: quais recursos do ES6 quer usar? A ES6 fornece tanto uma nova sintaxe, como o `let` e o sistema de módulos, mas também nos fornece recursos como novos objetos e funções adicionais, tais como *promises*. Antes de prosseguir, quero apenas lembrar que: keep calm, a maioria desses recursos serão explorados na série :)

Se você quiser usar a nova sintaxe, você precisa de um *transpiler*. Se você só quer usar os objetos e os recursos mencionados antes, então você pode usar um *shim*. *Shims* são mais simples e fáceis de se trabalhar com, como você só precisa incluí-lo em sua página ou aplicação Node antes de outros scripts. **Relembrando**: um *shim* não pode suportar recursos sintáticos. Se você quiser estes, você precisa então de um *transpiler*.

Vamos ver um pouco sobre cada um deles:

## Shims

Para nossos exemplos com *shims*, usaremos o [ES6 Shim](https://github.com/paulmillr/es6-shim/).

### Configurando o ES6 Shim no servidor

Configurar o ES6 Shim no `node.js`, `io.js`, ou outro workflow que seja gerenciado pelo npm é um processo muito simples: rode o comando `npm install es6-shim` e inclua `require('es6-shim');` em seus scripts.

### Configurando o ES6 Shim no navegador

O ES6 Shim tem um suporte a navegadores razoavelmente grande - algumas features estão disponíveis até para anteriores ao IE8! A maneira mais simples para começar no navegador é apenas incluir uma tag de script em sua página referenciando para o caminho onde está o arquivo principal do shim - que pode ser encontrado no [repositório oficial](https://github.com/paulmillr/es6-shim/):

`<script src="/es6-shim.js"></script>`

Se você usa o [Bower](http://bower.io/) como gerenciador de pacotes, também pode ser uma boa opção: `bower install es6-shim`. 

Em ambos os casos (servidor e navegador) sua maior preocupção é certificar-se de que o shim é carregado antes de quaisquer scripts que dependem dos recursos do ES6 - o mesmo para uso em produção ;)

## Transpilers

Para nossos exemplos com *transpilers*, usaremos principalmente o [Traceur](https://github.com/google/traceur-compiler/), que é um projeto do Google que visa pegar código ES6 e compilar para código ES5 compatível com os navegadores modernos em suas configurações padrão (as configurações de seus usuários terão). O Traceur é um projeto muito ativo e seus recursos são atualizados regularmente.

Porém, é válido lembrar que há uma série de outras [opções de transpilers](https://github.com/addyosmani/es6-tools#transpilers). Inclusive, o [Babel (ou 6to5)](https://github.com/babel/babel), possui boas vantagens frente ao Traceur - mas não se preocupe: teremos exemplos com ele também :) 

Antes de passarmos para configuração, é importante lembrar que há duas maneiras de se usar o Traceur:

- Incluir o compilador do Traceur em sua página ou aplicação Node, o que acaba sendo bom para testar features de maneira rápida - mas que traz problemas de desempenho, uma vez que o código é compilado em tempo real na página.

- Pré-compilar o código no servidor, o que é mais recomendado, principalmente se o alvo da sua aplicação é o navegador.

### Configurando o Traceur no servidor

Antes de tudo, precisamos do módulo do Traceur: `npm install traceur`. Contudo, temos dois *cenários* de uso do ES6 no Node:

#### Carregar a aplicação inteira usando módulos ES6

Se sua aplicação é escrita primordialmente em ES6, este pode provavelmente ser o melhor método - e você ainda pode usar o `require` do Node, se necessário. Neste método, você escreve um bootstrap para sua aplicação - como um módulo Node normal - onde você carrega um arquivo ES6, que inicializa sua aplicação. Primeiro, vamos criar o arquivo de inicialização (`bootstrap.js`):

```js
export function run() {
  console.log('Hello, World');
}
```

Em seguida, criamos o arquivo que será propriamente executado pelo Node (`app.js`):

```js
var traceur = require('traceur');
// Faz com que o require do Traceur sobrescreva o do Node
traceur.require.makeDefault(function(file) {
  // Certifica-se de que o Traceur não roda arquivos da pasta node_modules
  return file.indexOf('node_modules') == -1;
});
 
require('./bootstrap.js').run();
```

Um ponto interessante é que podemos usar tanto a o `require` quanto a sintaxe de importação de módulos do ES6.

*Como assim, Matheus?* 

Usando o `require`, nosso `bootstrap.js` ficaria assim:

```js
var express = require('express');
 
export function run() {
  console.log('Hello, World');
 
  var app = express();
}
```

Usando a sintaxe de módulos do ES6, teríamos o mesmo `bootstrap.js` assim:

```js
import * as express from 'express';
 
export function run() {
  console.log('Hello, World');
 
  var app = express();
}
```

#### Misturando módulos ES6 e Node

Esta abordagem é mais recomendada se você tiver uma aplicação existente onde você quer começar a usar módulos ES6. Assim, nós apenas incluímos o Traceur dentro do nosso módulo e usamos o `require` diretamente dele, por exemplo:

```
var traceur = require('traceur'); 
var exemplo = traceur.require('./exemplo.js');
 
//exemplo.js é um módulo ES6, podemos usá-lo normalmente:
exemplo.whatever();
```

### Configurando o Traceur no navegador

Convenhamos, no browser as coisas ficam um pouco mais complicadas. Mas vamos lá:

1. Nós precisamos ter o Traceur instalado como uma CLI. Para isso, fazemos: `npm install -g traceur`. Depois disso, você terá o comando `traceur`.

2. Uma vez instalado o Traceur, você também precisará do `traceur-runtime.js`, que pode ser achado em seu diretório npm (geralmente em `/usr/local/lib/node_modules/traceur/bin/traceur-runtime.js`).

3. Copie o arquivo para que você possa incluí-lo dentro de sua página HTML.

#### Configurando um módulo ES6 em sua página

Vamos imaginar uma estrutura de projeto simples, onde os arquivos de código-fonte estão em `src/`, e os arquivos de saídas (compilados) estarão em `build/`. O arquivo `traceur-runtime.js` deve estar em `lib/`. Primeiro, vamos criar um arquivo de exemplo simples (`app.js`):

```js
export function run() {
  console.log('Hello, World');
}
```

Em seguida, podemos usar o Traceur para convertê-lo em ES5: `traceur --out build/bundle.js src/app.js`. Por meio do flag `--out`, estamos dizendo ao Traceur para agrupar todas as dependências de nosso `app.js` para o arquivo `bundle.js`. Nosso HTML ficaria algo assim:

```js
<!DOCTYPE html>
<html>
  <head>
    <script src="lib/traceur-runtime.js"></script>
    <script src="build/bundle.js"></script>
 
    <script>
      var m = System.get('src/app.js');
 
      //m é o nosso exemplo de módulo ES6, com tudo exportado
      m.run();
    </script>
  </head>
 
  <body>
  </body>
</html>
```

Precisamos incluir ambos o `traceur-runtime.js` e nosso `bundle.js`. Em seguida, usamos o loader do sistema de módulos ES6 para obter acesso ao módulo, e inovacamos a função `run` que havíamos exportado.

#### Usando *imports* e outras bibliotecas

Se você está fazendo build de vários módulos ES6, essa configuração pode ser interessante. Nosso `app.js` ficaria:

```javascript
import * as foo from 'foo';
 
export function run() {
  console.log('Hello, World');
}
```

Você pode importar qualquer módulo ES6 como faria normalmente: o Traceur saberá lidar com as dependências e uní-las em nosso arquivo de saída (`bundle.js`). O uso de outras bibliotecas, como jQuery, funciona exatamente como seria sem ES6:

```js
<script src="/jquery.js"></script>
<script src="lib/traceur-runtime.js"></script>
<script src="build/bundle.js"></script>
 
<script>
  var m = System.get('src/app.js');
  m.run();
</script>
```

E o nosso `app.js`:

```js
export function run() {
  $(() => {
    $(document.body).html('Hello, World');
  });
}
```

Você simplesmente inclui todas as bibliotecas que você quer antes de seus scripts, e os globais que estas fornecem estarão disponíveeis em seus módulos ES6 também :)

### Não pode facilitar?

<iframe src="//giphy.com/embed/zjQrmdlR9ZCM?html5=true" width="480" height="253" frameBorder="0" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>

**Sim!** Como tinha prometido há umas linhas atrás, agora vamos usar o [Babel](https://github.com/babel/babel) de exemplo. Como dito também, o Babel possui algumas vantagens, como por exemplo a falta da necessidade de *runtimes*, o que o torna mais performático. Porém, discutir qual transpiler é melhor não é mérito deste post - quem sabe de um futuro. 

Apesar de nos seguintes exemplos usarmos um transpiler diferente, a *chave* para facilitar o processo será o **uso de automatizadores**. 

Nesta [lista](https://github.com/addyosmani/es6-tools) curada pelo nada pouco conhecido [Addy Osmani](https://github.com/addyosmani), podemos achar, entre outras diversas ferramentas para uso de ES6, uma série de plugins - grande parte feita pelo [Sindre Sorhus](https://github.com/sindresorhus) -  para trabalhar com a maioria dos automatizadores que temos (incluindo Grunt, Gulp e Broccoli).

Sem mais delongas, vamos ao exemplo onde usamos *Babel + Gulp* para compilarmos os arquivos da pasta `src` para ES6. Nosso `gulpfile.js` ficaria assim:

```js
 var gulp = require('gulp');
 var to5 = require('gulp-6to5');

  gulp.task('build', function () {
    var paths = [
      'lib/*.js',
      'src/**/*.js',
      '!lib/es6-transformer.js'
    ];

    gulp.src(paths)
      .pipe(to5())
      .pipe(gulp.dest('compiled'));
  });
```
Melhorou bastante, não?!

# Conclusão

Bem, confesso que, ao decidir escrever uma série de posts sobre ES6, um questionamento me veio a cabeça: se deveria começar expondo as features e, somente ao final da série expor maneiras de usá-las hoje em dia ou fazer o oposto: mostrar como ser adepto das novas especificações logo no primeiro post para que, a medida que a série avançasse, você mesmo fosse fazendo suas implementações e experimentos com as features e já vendo elas na prática :)

Acabei optando pela segunda, e o objetivo deste primeiro post passou a ser, além de esclarecer do que se trata ES6, mostrar que, com as ferramentas certas, já podemos começar a tirar proveito de recursos bastante interessantes - e que promovem reais melhorias para o desenvolvedor - disponíveis em versões futuras do JavaScript, hoje mesmo. 

Uma pergunta permanece: *Quando poderemos parar de usar shims e transipilers?* Esta é uma difícil de se responder; embora a previsão seja de junho de 2015, eu pessoalmente acho que levará um pouco mais de tempo. Uma recomendação é sempre acompanhar tabelas como [esta](http://kangax.github.io/compat-table/es6/) onde você pode verificar o suporte de algum navegador ou plataforma a características específicas. 

Por fim, espero que, mesmo este post tendo saído um pouco mais ~~cansativo~~ *"completo"* do que eu havia planejado, espero que tenha sido suficiente para despertar o interesse de vocês pelo novos recursos legais que estão aí - e que exploraremos ao longo da série :)
