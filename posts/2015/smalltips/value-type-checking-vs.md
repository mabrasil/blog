Fala galera, essa é mais uma da série **#smalltips** e hoje falarei de dois operadores do Javascript: o *Operador de Igualdade* (`==`) e o *Operador de Identidade* (`===`).

Tive essa ideia quando navegava por alguns projetos no Github e vi que a opção `eqeqeq` do [JSHint](http://jshint.com) muitas vezes ainda é necessária para *"proibir o uso de `==` e `!=` no lugar de `===` e `!==`"* - como a própria documentação a descreve.

Mesmo pessoas que não são iniciantes com Javascript às vezes ficam confusas com situações assim:

```js
'1' == 1 // Retorna "true"
'1' === 1 // Retorna "false"
true == 1 // Retorna "true"
true === 1 // Retorna "false"
```

Mas relaxe, entender a diferença entre estes é algo bem trivial :)

## Operador de Igualdade (`==`)

O operador de igualdade basicamente faz um processo de conversão de tipo dos operandos, se estes não forem do mesmo tipo, **e somente então**, aplica a comparação estrita. Assim, temos que esse operador é bem **liberal**, pois valores são considerados iguais, mesmo sendo de tipos diferentes. Exemplo de uma expressão com a sua sintaxe:

```js
x == y
```

onde, por exemplo:

```js
1 == 1 // Retorna "true"
1 == "1" // Retorna "true"
1 == true // Retorna "true"
```

## Operador de Identidade/Igualdade Estrita (`===`)

O operador identidade é mais **rígido** e retorna `true` **somente se** os operandos forem rigorosamente iguais - mesmo valor e mesmo tipo. Assim, temos uma expressão da forma:

```js
x === y
```

onde o exemplo acima ficaria:

```js
1 === 1 // Retorna "true", pois ambos são do tipo "number"
1 === "1" // Retorna "false", pois temos um "number" e uma "string"
1 === true // Retorna "false", pois temos um "number" e um "boolean"
```

## Observações

1. O mesmo funciona para os operadores de Desigualdade (`!=`) e não-identidade (`!==`).
2. Se ambos os operandos forem objetos, então é feita uma comparação de referências internas, que são iguais quando os operandos se referem ao mesmo objeto na memória e diferentes quando estes se referem a objetos diferentes.

## Resumindo (mais ainda)

Para concluir, basta saber que operador de igualdade faz a coerção dos operandos antes de compará-los - o que pode levar a alguns resultados inesperados. Já o operador de identidade não faz qualquer coerção - por isso é mais seguro e faz o uso do primeiro *não recomendado*.
