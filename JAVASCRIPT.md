## Indentação

A unidade de recuo é ** 4 espaços **. Nunca misture espaços e tabs.

```javascript
// Good
while (condition) {
    statements
}

// Bad
while (condition) {
  statements
}
```

## Comprimento da linha

Evite linhas maiores que ** 100 caracteres **. Quando uma instrução não cabe em uma única linha, pode ser necessário quebrá-la. Coloque a quebra depois de um operador, idealmente depois de uma vírgula. A próxima linha deve ser recuada ** 4 espaços **.

```javascript
// Good
YUI().use('aui-module-a', 'aui-module-b', 'aui-module-c', 'aui-module-d',
    'aui-module-e', 'aui-module-f');

// Bad
YUI().use('aui-module-a', 'aui-module-b', 'aui-module-c', 'aui-module-d', 'aui-module-e', 'aui-module-f');
```

## Ponto e vírgula

```javascript
// Good
a = b + c;
test();

// Bad
a = b + c
test()
```

## Variáveis

Todas as variáveis devem ser declaradas ** antes ** de serem utilizadas. Evite usar declarações repetidas de `var`.

```javascript
// bad
const obj = {
  id: 5,
  name: 'San Francisco',
};
obj[getKey('enabled')] = true;

// good
const obj = {
  id: 5,
  name: 'San Francisco',
  [getKey('enabled')]: true,
};
```

```javascript
// Good
var foo = '',
    bar = '';

// Bad
var foo = '';
var bar = '';
```

Constantes (variáveis com valores permanentes) são escritas em ** maiúsculo **.

```javascript
// Good
var FOO = 'foo';

// Bad
var foo = 'foo';
```

Javascript ES6
```javascript
// bad
var a = 1;
var b = 2;

// good
const A = 1;
const B = 2;
```

Javascript ES6 prefira usar `let` no lugar de `var`
```javascript
var count = 1;
if (true) {
  count += 1;
}

// good, use the let.
let count = 1;
if (true) {
  count += 1;
}
```

## Strings

Prefira aspas simples e dentro da string aspas duplas.

```javascript
// Good
var string = '<p class="foo">Lorem Ipsum</p>';

// Bad
var string = "<p class='foo'>Lorem Ipsum</p>";
```

As cores hexadecimais são escritas ** maiúsculas **.

Tanto no Javascript quanto no CSS.

```css
// Good
.class {
  color: #D96AB6;
}

// Bad
.class {
  color: #d96ab6;
}
```

```javascript
// Good
var color = '#D96AB6';

// Bad
var color = '#d96ab6';
```

## Novas linhas

Parênteses `()` e vírgulas `,` ** não ** são definição de recuo ou de novas linhas.

```javascript
// Good
YUI().use('aui-module', function (Y) {
    statements
});

// Bad
YUI().use(
    'aui-module',
    function (Y) {
        statements
    }
);
```

As chaves `{}` são seguidos por ** novas linhas ** e recuam as definições filhas.

```javascript
// Good
if (condition) {
    statements
} else {
    statements
}

// Bad
if (condition) {
    statements
}
else {
    statements
}
```

## Espaço em branco

Adicione espaços entre ** operadores ** ( `=`, `>`, `*`, etc).

```javascript
// Good
for (i = 0; i < 10; i++) {
    statements
}

// Bad
for (i=0;i<10;i++) {
    statements
}
```

As expressões de função e declarações de função ** não ** têm um espaço entre o nome da função e os parentêses.

```javascript
// Bom
var foo = function() {
    statements
};

// Ruim
var foo = function () {
    statements
};

// Bom
function bar() {
    statements
}

// Ruim
function bar () {
    statements
}
```

Adicione espaços ** fora ** de parênteses `()`, mas evite dentro.

```javascript
// Good
if (x > 10) {
    statements
}

// Bad
if( x > 10 ){
    statements
}
```

As linhas vazias não têm espaços à direita.

## Condições

Evite condições inline. Cada condicional (com instruções simples ou múltiplas) devem usar ** colchetes ** `{}`. A única exceção a esta regra é o `else if`.

```javascript
// Good
if (condition) {
    statements
} else if (condition) {
    statements
} else {
    statements
}

// Bad
if (condition) statement;
else if (condition) statement;
else statement;
```

## Equaldade

As verificações de igualdade de Strings devem ser usado `===` no lugar de `==`.

```javascript
// Bom
if (foo === 'foo') {
    statement
}

// Ruim
if (foo == 'foo') {
    statement
}

// Good
if (bar !== 'bar') {
    statement
}

// Bad
if (bar != 'bar') {
    statement
}
```

## Loops

Evite inline loops. Cada loop (com instruções únicas ou múltiplas) deve usar ** chaves ** `{}`.

```javascript
// Good
for (initialization; condition; expression) {
    statements
}

// Bad
for (initialization; condition; expression) statement;
```
