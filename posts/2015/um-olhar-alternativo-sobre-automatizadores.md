### *Ferramentas como Gulp podem ser incríveis, mas realmente precisamos delas?*

---
Tarefas como desenvolvimento e implantação/publicação de Single-Page Applications (SPAs) e módulos Node, por exemplo, podem demandar um número considerável de ferramentas: quando trabalho em uma Single-Page Application, eu preciso de alguma forma realizar o gerenciamento de assets, pré-processamento e compilação de estilos, preparação para testes e ainda concatenação, minificação e compressão de arquivos Javascript — tudo isso para produção, e mantendo-as como são para desenvolvimento. E ainda, eu preciso poder fazer redeploy contínuo a cada alteração feita no código.

Se você trabalha com desenvolvimento de aplicações modernas em Javascript, muito provavelmente sabe do que estou falando — e há boas chances de ter usado ferramentas de automação em Javascript. Se não, vamos primeiramente relembrar o que são automatizadores — e conhecer alguns deles.

# O que são automatizadores?

A definição mais simples que eu posso pensar de automatizadores é que eles são um conjunto de ferramentas para tornar tarefas como compilação “limpas e bem documentadas”. Eles fornecem meios para gerenciar as operações no sistema de arquivos do projeto — através da linha de comando. Em outras palavras, eles são algo como “a nova geração de Makefiles”.

# Quais ferramentas temos?

Eu gostaria de mencionar apenas algumas das quais julgo serem as mais populares do momento: Grunt, Gulp e Broccoli. Os pesos pesados são realmente o Grunt e o Gulp, embora muitos outros existam.

## Grunt
Eu diria que este é o task runner mais popular do mundo Node. O número de downloads feitos no npm — algo em torno de 30.000 downloads quase todos os dias — ainda é o maior. Seu processo de build é baseado em um Gruntfile localizado na raiz do seu projeto e a maioria dos recursos exige a instalação de um plugin específico.

Os plugins são baseados na configuração via um objeto Javascript. A menos que você queira escrever seu próprio plugin, você provavelmente não precisará escrever lógica no código.

A comunidade do Grunt é muito ativa e há um considerável número de recursos sobre o assunto.

## Gulp
Assim como o Grunt, o Gulp trabalha com um Gulpfile + plugins; mas tende a tornar as coisas mais simples, baseando-se em uma lógica de código de pipes. A ideia por trás dele é que seu código é uma lista de arquivos que exigem uma série de operações a serem aplicadas. O resultado de cada operação é canalizado (“piped”) para a próxima.

O código se torna mais flexível do que com Grunt, menos código é necessário e você também tem um monte de plugins para tornar a sua vida mais fácil.

## Broccoli
O Broccoli segue o mesmo princípio do Gulp: tarefas baseadas em lógica de código e sistema de plugins — mas sem nenhuma noção de pipes: apenas filtros que se aplicam a uma árvore de arquivos. Ele também se baseia mais na linha de comando para os parâmetros.

# Os problemas

Nas últimas semanas eu comecei a refletir sobre a possiblidade de muitas destas ferramentas estarem resolvendo mal o problema mencionado . Se você prestar atenção aos task runners citados, podemos ver que ferramentas como Gulp tentam resolver os problemas do Grunt; e o Broccoli tenta resolver os problemas do Gulp — ou seja, resolver os problemas/insuficiências da ferramenta anterior, mas trazendo à tona seus próprios.

Estas são algumas das razões pelas quais eu acho que essas ferramentas podem às vezes ser más escolhas — ou pelo menos as menos adequadas:

## Dependência de plugins

Salvo enganos, nenhuma das ferramentas de automação que temos pode trabalhar sem plugins. E o pior: se você encontrar uma nova ferramenta que você gostaria de aplicar em seu processo de build, você provavelmente vai ter que esperar até que alguém escreva um wrapper para o task runner que você utiliza — ou escrevê-lo você mesmo. Ao invés de apenas aprender comandos básicos para a ferramenta que deseja usar, agora você tem que aprender mais sobre a API desta e também a API da sua ferramenta de automação.

E se você, por exemplo, para certas tarefas, precisa usar o Grunt, e para outras, o Gulp — ou mesmo Brunch -, você vai acabar **usando automatizadores para gerenciar seus automatizadores**.

## Comportamentos Inesperados

Há muitos relatos de maus comportamentos observados com o Gulp, por exemplo: já vi casos em que o JSHint não falhou em um experimento onde certa quantidade de erros foram propositadamente escritos para fazê-lo falhar. Eu li o mesmo tipo de relatório com o plugin Mocha do Gulp: mesmo quando encontrado um erro, o Gulp apresentou um código de saída 0— o que significa que, caso colocássemos isso em um ambiente de integração contínua, como Travis, ele iria apresentar tais falhas e, em seguida, passar, uma vez que o serviço de CI apenas vê a saída do log e um código de saída “amigável” e assume que tudo ocorreu bem.

Penso que seja válido mencionar que superar esses tipos de obstáculos — quando tudo que você quer fazer é apenas configurar uma simples ferramenta — pode ser uma experiência um tanto desagradável.

## Falsas Promessas

O Gulp promete ter uma API muito simples, mas o que não percebemos é que essa API simples esconde a complexidade do utilitário de gerenciamento de arquivos do Gulp — VinylFS — e seu framework de automação — o Orchestrator. Assim, você pode acabar tendo de ler também as documentações e código destes.

Além disso, o Gulp também proclama a presença de dois conceitos-chave: streaming e assincronismo — ao contrário do Grunt, onde tudo acontece de forma síncrona. Mas acontece que um dos principais benefícios pretendidos do Gulp — sua capacidade de streaming — na verdade não funciona com todos os plugins disponíveis.

## Complicações desnecessárias

O que eu noto é que todos esses task runners tentam abstrair algum tipo de paradigma de tarefas em seu próprio “jeito ideal”. Por exemplo, o Gulp, como dito antes, usa arquivos de configuração e plugins que permitem usar suas ferramentas favoritas para trabalhar com o seu código. Se quiséssemos um Gulpfile que simplesmente rodasse o JSHint, teríamos algo parecido com isto:

```js
var jshint = require(‘gulp-jshint’); 
var gulp = require(‘gulp’); 
gulp.task(‘jshint’, function() { 
  return gulp.src(‘**.js’) 
    .pipe(jshint()) 
    .pipe(jshint.reporter(‘default’)); 
});
```
Tudo isso é feito para abstrair as dificuldades de rodar o JSHint diretamente de seu terminal.

É claro que, para fazer com que isso funcionasse você ainda teria que rodar `gulp jshint` no terminal, o que, como se vê, é um comando apenas um pouco mais curto do que apenas: `jshint **.js`.

A mesma coisa ocorre com o Grunt — com algumas linhas de código a mais, obviamente— , mas ainda precisamos de duas dependências (grunt e grunt-contrib-jshint). E isso não acontece apenas com o Grunt e o Gulp: Jake, Broccoli, Brunch e Mimosa; todos exigem plugins, o que significa que ao usar qualquer um desses task runners, você está apenas instalando mais uma dependência (o próprio task runner).

E agora você deve estar pensando: “Se nenhuma dessas complexas ferramentas de automação resolve realmente o problema, o que resolve?” E esta pergunta nos leva ao próximo tópico:

# A solução

Em minha opinião, a solução seria algo como uma ferramenta que possa executar scripts de build, assumir valores de configuração, seja streaming, tenha uma API relativamente simples — e ainda seja fornecida gratuitamente com cada instalação Node.js. Pode soar estranho, mas se você acha que eu estou lhe dizendo que o npm é a melhor solução, você está certo.

Se olharmos para o nosso arquivo package.json — o que significa que você não tem nem que adicionar novos arquivos ao seu projeto— , vamos ver o objeto scripts do npm. Suas propriedades são os nomes de tarefas; e os valores, são os comandos.

Vamos relembrar o exemplo de uso do JSHint (da secção “Complicações Desnecessárias”) e “portá-lo” para o npm:

```js
“devDependencies”: { 
  “jshint”: “latest”, 
}, 
“scripts”: { 
  “lint”: “jshint **.js” 
}
```
Tudo que você tem de fazer é introduzir uma dependência extra e uma linha de código, rodar `npm run lint ` e pronto!

#Conclusão

No final das contas, se dermos uma olhada no nosso package.json, vamos ver que o que fazemos são chamadas via CLI para os pacotes Node.js que nós temos instalados como dependências de desenvolvimento e, em seguida, canalizando as chamadas de um para o outro — o mesmo que fazemos com o Gulp, mas com menos código, muito mais simplicidade e mais facilidade de manutenção.

Eu não estou dizendo que o Gulp — ou o task runner do momento — nunca será necessário: eu compreendo que pode haver um — ou mais — caso(s) de uso válido(s) para ferramentas de build. Mas, para muitos casos, nós podemos apenas usar o próprio npm. Eu penso que se você considerar fazer isso em seu próximo projeto, os resultados podem surpreendê-lo positivamente.

A propósito, é sempre bom lembrar que eu não sou nenhum tipo de “dono verdade”: se você tem alguma opinião sobre isso (concordando, discordando, complementando) sinta-se livre para compartilhá-la.

*Originalmente postado em [Um olhar alternativo sobre automatizadores](https://medium.com/pensamentos-js/um-olhar-alternativo-sobre-automadores-339d0df6a4cc).*