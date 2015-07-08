Na **#smalltip** de hoje, veremos algumas coisas **bem básicas** relacionadas a manipular valores numéricos em Javascript, incluindo operações de aritmética e alguns métodos do objeto *Math*.

## Operadores básicos de Aritmética

---

### Adição (`+`)

**Sintaxe**: `x + y`

**O que faz:** Nos retorna a soma dos operandos.

**Exemplo:** `4 + 5;  // 9`

### Subtração (`-`)

**Sintaxe**: `x - y`

**O que faz:** Nos retorna a diferença de dois operandos.

**Exemplo:** `5 - 4;  // Retorna 1`

### Multiplicação (`*`)

**Sintaxe**: `x * y`

**O que faz:** Nos retorna o produto de dois operandos.

**Exemplo:** `4 * 5;  // Retorna 20`

### Divisão (`/`)

**Sintaxe**: `x / y`

**O que faz:** Nos retorna o quociente da divisão do primeiro operando pelo segundo.

**Exemplo:** `20 / 5; // Retorna 4`

### Resto/Modulus Operator (`%`)

**Sintaxe**: `x % y`

**O que faz:** Nos retorna o resto da divisão do primeiro operando pelo segundo.

**Exemplo:** `14 % 9 // Retorna 5`

### Em resumo...

Trabalhar com operações aritméticas básicas é algo simples assim:

```js
5 + 5; // Retorna 10
5 * 5; // Retorna 25
5 - 5; // Retorna 0
5 / 5; // Retorna 1
5 % 5; // Retorna 0
```

### Operadores de Incremento/Decremento

Estes se dividem em:

#### Prefix increment/decrement operators

**Sintaxe**:
```js
--x   // Decremento
++x   // Incremento
```

**O que fazem:** São operadores que primeiro aumentam (incremento) ou diminuem (decremento) o valor de uma expressão / variável por 1 e, em seguida, retornam este valor reduzido/incrementado.

**Exemplo:**
```js
var x = 16;
var y = ++x;
// O valor de x (16) é primeiro acrescido de 1 e então associado a y
console.log(y); // Retorna 17
```

#### Postfix increment/decrement operators

**Sintaxe**:
```js
x--  // Decremento
x++   // Incremento
```

**O que fazem:** São operadores que primeiro retornam o valor de uma expressão / variável e então aumentam (incremento) ou diminuem (decremento) este em 1.

**Exemplo:**
```js
var x = 16;
var y = x++;
// O valor de x (16) é primeiro associado a y e então acrescido de 1
console.log(y); //15
console.log(x); //16
```

## O objeto `Math`

---

O objeto `Math` nos permite execute algumas operações matemáticas, apenas acessando seus métodos/propriedades sem a necessidade de criá-lo - uma vez que este não é um construtor. Vamos ver alguns métodos:

### random

**Sintaxe**: `Math.random()`

**O que faz:** Retorna um número aleatório entre 0 e 1.

**Exemplo:** `Math.random(); // Retorna um número aleatório entre 0 e 1.`

### floor


**Sintaxe**: `Math.floor(x)`

**O que faz:** Retorna o *maior* número inteiro *menor que* ou *igual* a um número dado.

**Exemplo:** `Math.floor(9.99); // Retorna 9`

### ceil


**Sintaxe**: `Math.ceil(x)`

**O que faz:** Retorna o *menor* número inteiro *maior que* ou *igual* a um número dado.

**Exemplo:** `Math.ceil(9.99); // Retorna 10`

### pow

**Sintaxe**: `Math.pow(x, y)`

**O que faz:** Retorna a *base*(x) elevada ao *expoente*(y).

**Exemplo:** `Math.pow(2,4); // Retorna 16`

### sqrt

**Sintaxe**: `Math.sqrt(x)`

**O que faz:** Retorna a raiz quadrada de um número.

**Exemplo:** `Math.sqrt(5+4); // Retorna 3`

### PI

**Sintaxe**: `Math.PI`

**O que faz:** Retorna o valor de *pi (π)* - aproximadamente *3,14159*. Lembre-se que este não se trata de uma função - por isso, temos `Math.PI` e não `Math.PI()`.

**Exemplo:** `Math.ceil(Math.PI); // Retorna 4`

---

Basicamente, é isso pessoal, fiquem atentos aos próximos posts, onde veremos muitas coisas bacanas da API de Javascript.
