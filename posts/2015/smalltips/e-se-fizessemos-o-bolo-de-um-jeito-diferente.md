Fala galera! Mais um post da *hashtag* **#smalltips**! Na verdade, esse post tá nessa seção mais pelo *small* do que pelo *tips* em si.

Bem, o assunto do post de hoje não é novo, e a ideia surgiu no início deste semestre, quando comecei a cursar a cadeira de *"lógica de programação"* - sim, entre aspas mesmo!

Vejo muito sendo ventilado a novatos na programação que devemos sempre *"estudar lógica primeiro e então optarmos por uma linguagem X, de preferência C, C++ ou Java"* - eu mesmo já ouvi muito disso.

O pior é que, isso não é algo exclusivo de "conselhos para principiantes" - muitas vezes isso acaba nos sendo imposto pelos sistemas: seja em cursos técnicos, de nível superior etc., o que observo é sempre um grande processo de doutrinação a tecnologias ou métodos específicos, como se estes fossem **a única opção das galáxias** - sendo que muitas vezes estes estão longes de ser, ao menos, **a melhor opção**.

Os casos são muitos, inclusive eu e o [Felipe Sousa](http://felipesousa.github.io/), já chegamos a discutir sobre muitas experiências envolvendo doutrinação *Java/OO* - sim amigos, eu acredito que existem muitas linguagens mais adequadas para se aprender *Orientação a Objetos pura*, assim como descrita inicialmente por [Alan Kay](https://pt.wikipedia.org/wiki/Alan_Kay) e outros cientistas, do que Java - mas esse caso específico não é o ponto do post.

Vamos falar de *lógica*: Em geral, a *"lógica de programação"* que aprendemos é algo como uma sequencia lógica de instruções ~~sério, Matheus?!~~ a serem executadas com um objetivo - em geral, algo como a sequencia de condicionais (If...Then...Else...), loops (for, while...) etc. de nosso programa. Professores, apostilas, outros programadores etc. nos dão como exemplo a clássica **receita de bolo** - daí o título do post :)

Assim, a nossa clássica receita básica de bolo, imperativa, orientada a objetos, ficaria algo assim:

```
// Definimos onde assaremos
FormaDeAssar recipiente

// Adicionamos cada ingrediente ao recipiente
Recipiente.Adicionar (500 farinha)
Recipiente.Adicionar(3 ovos)
Recipiente.Adicionar(150ml leite)

// Preparando a massa
Recipiente.Bater(15 minutos)

// Cozinhando
Recipiente.Cozinhar(40 minutos,180°)
```

O problema é que muita gente por aí "enfia" tal modelo em nossa cabeça sem nos mostrar que isso ocorre assim em [linguagens com implementações imperativas](http://en.wikipedia.org/wiki/Imperative_programming) - como, por exemplo: C, C++, Java, PHP, Ruby, Python, JavaScript etc. - ou seja, linguagens que expressam uma sequencia lógica de instruções - apesar de algumas também implementarem outros paradigmas.

Mas o que nem sempre nos é mostrado é que há outras formas de pensarmos; incluindo as [linguagens funcionais](https://pt.wikipedia.org/wiki/Programa%C3%A7%C3%A3o_funcional), que não nos dizem *como* fazer algo, e sim *o quê* deve ser feito - por meio de funções matemáticas.

Então... E se tivéssemos uma receita assim:

```
// Uma função para definir o que vai ser batido
Let batedeira = 500g farinha + 3 ovos + 150ml leite

// Uma função para definir o que vai ser feito com a massa resultante
Let massa =  bater por 15 minutos

// Uma função para definir o que vai ser assado
Let bolo = assar massa por 40 minutos a 180°
```

Algo um tanto quanto diferente - e que não soaria *normal* pra nenhum cozinheiro, inclusive.

Esse é o ponto: por mais que você entenda a lógica imperativa e domine muitas linguagens entre os exemplos dados, provavelmente teria uma certa dificuldade em aprender uma linguagem funcional como [Haskell](https://www.haskell.org/), [Clojure](http://clojure.org/), [Scala](http://www.scala-lang.org/), [Erlang](http://www.erlang.org/), [Elixir](http://elixir-lang.org/) etc. - ou até mesmo em entender implementações funcionais de linguagens que não são *puramente funcionais*. Assim, a *"lógica de programação"* que você aprendeu na faculdade seria um tanto desnecessária em ~~presentes divinos~~ linguagens assim, pois você não pode pensar de forma imperativa, você precisa **pensar de forma funcional**.

Assim, muitas pessoas acabam por não *simpatizar* muito com linguagens funcionais; porque não conseguem entendê-las facilmente, uma vez que estão acostumadas com o pensamento imperativo (*"lógica de programação"*).

Aí alguém pode se questionar: *"Quem usa isso?!"*. Bem, responder essa pergunta envolve explicar a importância cada vez maior que a programação funcional tem tomado. Mas, eu acabaria fugindo muito do assunto - e a [Ju Gonçalves](http://jugoncalv.es/) já fez isso muito bem [nesse post](https://medium.com/@jugoncalves/functional-programming-should-be-your-1-priority-for-2015-47dd4641d6b9).

Esse era o objetivo do post: apenas tentar abrir um pouco a mente para a ideia de que *lógica de programação* como nos é passada, **pode ser sim importante**, mas não é a única, uma vez que não existem apenas linguagens imperativas.

Então, se seu professor mandou você *fazer o bolo* da forma tradicional, seja *punk* e mostre que, como já dizia sua mãe, **"Você nao é todo mundo!"**, e não tem de ser mais um a apenas engolir *verdades*: estude sempre novos paradigmas,novas linguagens, e **faça o bolo de um jeito diferente!**

*Lembrem-se:* eu não sou nenhum “dono da verdade”: se você tem alguma opinião sobre isso (concordando, discordando, complementando) sinta-se livre para compartilhá-la - só por favor, não me xingue muito :)
