# Functions y scope | Ejercicio de identificación

Identificar las funciones globales, locales, funciones de callback, function expressions, function statements, closure, scope, contextos de ejecución, qué funciones forman parte de la pila de ejecución (execution stack) y qué funciones forman parte de la cola de eventos (event queue).

## Funciones globales

> Son las funciones que no se encuentran dentro de otra función.

En este caso, `$(document).ready()`, en la línea 1, sería la única función global.

## Funciones locales

> Son aquellas que se encuentran dentro de una función.

En este documento, las siguientes funciones se existen dentro del scope de la función global `$(document).ready()`: 

- `console.log()` (línea 3)
- Función vinculada al evento `input` (línea 14)
- Función `activeButton()` (línea 19)
- Función `desactivButton()` (línea 24)
- Función `longitud(input)` (linea 29)
- Función `soloNumeros(input)` (línea 36)
- Función `isValidCreditCard(numberCard)` (línea 44)

## Funciones de callback

> Son las funciones que son pasadas como argumentos de otra función.

Se encuentran funciones de callback:

- Función vinculada al evento `input` (línea 14)
- Función `longitud` utilizada como argumento de la función `soloNumeros` (línea 45)

## Function expression

> Asigna el resultado de una función como expresión a la variable y puede ser llamada a través de esa variable.

```js
// Sintaxis
var add = function(x, y) {
  return x + y;
};
```

## Function statements

> Declara una nueva variable, crea una función de un objeto y asigna la función a la variable.

```js
// Sintaxis
function add(x, y) {
  return x + y;
}
```

En app.js se encuentran las siguientes `function statement`:

- `function activeButton()` (línea 19)
- `function desactiveButton()` (línea 24)
- `function longitud(input)` (línea 29)
- `function soloNumeros(input)` (línea 36)
- `function isValidCreditCard(numberCard)` (línea 44)

## Closure

> Es la habilidad que tienen las funciones para recordar el contexto en que fueron creadas, incluso cuando se les invoca en un contexto diferente.

Por ejemplo, La función `isValidCreditCard(numberCard)` fue creada en el scope de la función `$(document).ready()`. Luego es invocada en la línea 15, dentro de la función vinculada al evento `input` asignado a la variable `$inputCard` y se le pasa como parámetro la variable `$(this)`, que en este caso hace referencia a la variable `$inputCard`. `$inputCard` no fue creada dentro de la función en la que `isValidCreditCard` fue invocada, pero sí en el scope de la fución `$(document).ready()` al igual que `isValidCreditCard(numberCard)`, por lo que , gracias al closure, est función recuerda a la variable y puede utilizarla.

Igualmente las funciones `activeButton()` y `desactiveButton()` son invocadas en el scope de la función `isValidCreditCard(numberCard)`, pero utilizan la variable  `$buttonNext`, que fue creada en el mismo contexto que ellas, en el scope de la función `$(document).ready()`.

## Execution stack

Funciones que forman parte de la pila de ejecución.

- `console.log()`
- `$(document).ready()`

## Event Queue

Funciones que forman parte de la cola de eventos.

- Event handler vinculado a la variable `$inputCard`
- Función `isValidCreditCard()`
- Función `soloNumeros()`
- Función `longitud()`
- Función `activeButton()` || `desactiveButton()`