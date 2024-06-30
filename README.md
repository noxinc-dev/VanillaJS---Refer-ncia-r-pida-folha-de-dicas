## Referência Rápida de JavaScript / CheatSheet

[Original em inglês](https://gist.github.com/thegitfather/9c9f1a927cd57df14a59c268f118ce86).

[Traduzido Llama-3-portuguese-Tom-cat-8b-instruct](https://huggingface.co/noxinc/Llama-3-portuguese-Tom-cat-8b-instruct-Q8_0-GGUF-PTBR).

Recentemente foi migrado de Codepen.io para markdown. Créditos para [David Conner](https://github.com/davidicus).


| Trabalhando com DOM | Trabalhando com JS | Trabalhando com Funções |
| ---------------------|---------------------|------------------------ |
| [Acessando Elementos do DOM](#acessando-elementos-do-dom)| [Adicionar/Remover Item do Array](#adicionarremover-item-do-array) | [Adicionar Parâmetros Padrão a uma Função](#adicionar-parâmetros-padrão-a-uma-função) |
| [Capturar Filhos/Pai de Nós](#capturar-filhos-pai-de-nós)| [Adicionar/Remover Propriedades do Objeto](#adicionarremover-propriedades-do-objeto) | [Acoplar ou Desacoplar Chama de Funções](#acoplar-ou-desacoplar-chama-de-funcões-calls) |
| [Criar Elementos do DOM](#criar-novos-elementos-do-dom)| [Condicional](#condicional) | |
| [Adicionar Elementos ao DOM](#adicionar-elementos-ao-dom)| [Laços](#laços) | |
| [Adicionar/Remover/Trocar/Verificar Classes](#adicionar-elementos-ao-dom-cont)| [Eventos](#eventos) | |
| | [Timers](#timers) | |
| | [Verificação de Tipo](#verificação-de-tipo) | |



#### Acessando Elementos do DOM

```javascript
// Retorna uma referência ao elemento pelo seu ID.
document.getElementById('someid');

// Retorna um objeto array-like de todos os elementos filho que têm todas as classes especificadas.
document.getElementsByClassName('someclass');

// Retorna uma coleção HTML de elementos com o nome de tag especificado.
document.getElementsByTagName('LI');

// Retorna o primeiro elemento dentro do documento que matches o grupo de seletores especificado.
document.querySelector('.someclass');

// Retorna uma lista de elementos dentro do documento (usando profundidade-first pre-order traversal das nodes do documento)
// que matches o grupo de seletores especificado.
document.querySelectorAll('div.note, div.alert');
```

#### Capturar Filhos/Pai de Nós

```javascript
// Pega nós filho
var stored = document.getElementById('someid');
var children = stored.childNodes;

// Pega pai de nível superior
var parental = children.parentNode;
```

#### Criar Novos Elementos do DOM

```javascript
// Crie novos elementos
var newHeading = document.createElement('h1');
var newParagraph = document.createElement('p');

// Crie nós de texto para novos elementos
var h1Text= document.createTextNode('This is a nice header text!');
var pText= document.createTextNode('This is a nice paragraph text!');

// Afixe novos nós de texto a novos elementos
newHeading.appendChild(h1Text);
newParagraph.appendChild(pText);

// Elementos agora estão criados e prontos para ser adicionados ao DOM.
```

#### Adicionar Elementos ao DOM

```javascript
// Pegue elemento na página que deseja adicionar conteúdo
var firstHeading = document.getElementById('firstHeading');

// Adicione ambos os novos elementos à página como filhos do elemento armazenado em firstHeading.
firstHeading.appendChild(newHeading);
firstHeading.appendChild(newParagraph);

// Ou pode-se inserir antes da seguinte maneira

// Obtenha pai de firstHeading
var parent = firstHeading.parentNode;

// Insira newHeading antes de FirstHeading
parent.insertBefore(newHeading, firstHeading);
```

#### Adicionar Elementos ao DOM (continuação)

Suponha que você tenha o seguinte HTML:
```html
<div id='box1'>
<p>Some example text</p>
</div>
<div id='box2'>
<p>Some example text</p>
</div>
```

Você pode inserir outro snippet de HTML entre #box1 e #box2:

```javascript
var box2 = document.getElementById('box2');
box2.insertAdjacentHTML('beforebegin', '<div><p>This gets inserted.</p></div>');

// beforebegin - O HTML seria colocado imediatamente antes do elemento, como irmão.
// afterbegin - O HTML seria colocado dentro do elemento, antes de seu primeiro filho.
// beforeend - O HTML seria colocado dentro do elemento, após seu último filho.
// afterend - O HTML seria colocado imediatamente após o elemento, como irmão.
```

#### Adicionar/Remover/Trocar/Verificar Classes

```javascript
// Pegue elemento na página que deseja usar
var firstHeading = document.getElementById('firstHeading');

// Removerá foo se ele for uma classe do firstHeading
firstHeading.classList.remove('foo');

// Adicionará a classe 'anotherClass' se ela não existir
firstHeading.classList.add('anotherclass');

// Adicionar ou remover múltiplas classes
firstHeading.classList.add('foo', 'bar');
firstHeading.classList.remove('foo', 'bar');

// Se a classe 'visible' estiver definida, removê-la; caso contrário, adicione-a
firstHeading.classList.toggle('visible');

// Retorna true se tiver classe 'foo' ou false se não tiver
firstHeading.classList.contains('foo');
```

#### Adicionar/Remover Item do Array

```javascript
// Crie um array vazio
var myArray = [];

// Crie um array com itens. Pode armazenar qualquer tipo
var myOtherArray = [myArray, true, 'a random string'];

// Chame valor específico em um array
myOtherArray[0];
// retornará myArray

// Altere valor para este item
myOtherArray[0] = false;
// agora retorna false


// Adicione ao final do array
myOtherArray[myOtherArray.length] = 'new stuff';
// retornará o novo item 'new stuff'

// Ou pode-se usar push()
myOtherArray.push('new stuff');
// retornará o novo comprimento do array

// pode remover esse último item usando pop()
myOtherArray.pop();
// retornará o último item do array e removerá ele de myOtherArray

// shift e unshift farão o mesmo no início do Array
myOtherArray.shift();
// removerá e retornará o primeiro item do array

myOtherArray.unshift(1,2);
// adicionará 1 e 2 ao início do array e retornará o novo comprimento
```

#### Adicionar/Remover Propriedades do Objeto

```javascript
// Crie um objeto
var newObject = {};

// Adicione uma propriedade ao objeto
newObject.newPropName = 'super slick';

// Ou outro sintaxe
newObject['other new prop name'] = 'mildly slick';

// Agora newObject.newPropName retornará 'super slick'
newObject.newPropName;

// Agora para deletar
delete newObject.newPropName;
```

#### Condicionais

```javascript
// Se Else Statements
var a = 1;
var b = 2;

if (a < b) {
console.log('the if is true!');
} else {
console.log('the if is false!');
}


// Multi If Else Statements
var a = 1;
var b = 2;
var c = 3;

if (a > b) {
console.log('a is bigger than b');
} else if (a > c) {
console.log('but a is bigger than c');
} else {
console.log('a is the smallest');
}


// Operadores Ternários. Mesmo que If Else
var a = 1;
var b = 2;

a === b ? console.log('The statement is true') : console.log('The statement is false');

// Switch Statements
var a = 4;
switch (a) {
case 'Oranges':
console.log('Orange? really?');
break;
case 1:
console.log('a is equal to 1.');
break;
case 2:
console.log('a is equal to 2.');
break;
case 3:
console.log('a is equal to 3.');
break;
case 4:
console.log('a is equal to 4.');
break;
default:
console.log('I run if no one else is true.');
}
```

#### Laços

```javascript
// Loop While
var i = 0;
while (i < 10) {
console.log(i);
i += 1
}


// Do While Loop
var i = 0;
do {
console.log(i);
i += 1
} while (i < 10)


// Loop For
for (var i = 0; i < 10; i++) {
console.log(i);
}

// For In Statements
var obj = {a:1, b:2, c:3};

for (var prop in obj) {
// Verifique se a propriedade é herdada ou não
if (obj.hasOwnProperty(prop)) {
console.log('obj.' + prop + ' = ' + obj[prop]);
}
}
```

#### Eventos ([MDN Event Reference](https://developer.mozilla.org/en-US/docs/Web/Events))

```javascript
var newElement = document.getElementsByTagName('h1');

newElement.onclick = function() {
console.log('clicked');
};

var logEventType = function(e) {
console.log('event type:', e.type);
};

newElement.addEventListener('focus', logEventType, false);
newElement.removeEventListener('focus', logEventType, false);

window.onload = function() {
console.log('Im loaded');
};
```

#### Timers

```javascript
function simpleMessage() {
alert('This is just a simple alert');
}

// Set Timeout
window.setTimeout(simpleMessage, 5000);

// Se você quiser limpar o timer.
var timer = window.setTimeout(simpleMessage, 5000);
window.clearTimeout(timer);

// Set Interval. Repetirá todos os 5000ms
window.setInterval(simpleMessage, 5000);

// Se você quiser limpar os intervalos.

var intervalHandler = window.setInterval(simpleMessage, 5000);
window.clearInterval(intervalHandle);
```

#### Verificação de Tipo

```javascript
var myNumber = 1;
var myString = 'some Text';
var bools = true;
var myArray = [];
var myObj = {};
var notNumber = NaN;
var nullified = null;
var undef;

typeof myNumber;
// retorna 'number'

typeof myString;
// retorna 'string'

typeof bools;
// retorna 'boolean'

typeof myArray;
// retorna 'object'.

// Não é muito útil, então deve verificar se tem propriedade de comprimento para ver se é um array.
typeof myArray === 'object' && myArray.hasOwnProperty('length');
// retorna true

typeof myObj;
// retorna 'object'. Deve fazer o mesmo teste acima, mas esperar falso de volta da verificação.

typeof notNumber;
// retorna 'number'. Isso é confuso, pois retorna isso porque NaN é parte do objeto global Number.

// Deve verificar se isNaN()
typeof notNumber === 'number' && isNaN(notNumber);
// retorna true se tipo for 'number' e ainda seja NaN

typeof undef;
// retorna 'undefined'

undef === undefined && typeof undef === 'undefined';
// retorna 'true'

notDeclared === undefined;
// -> Uncaught ReferenceError: notDeclared is not defined
```

#### Adicionar Parâmetros Padrão a uma Função

```javascript
var myFunc = function (arg1='default argument one', arg2='default argument two') {
console.log(arg1 + " & " + arg2);
};

myFunc(undefined, 'and a new value'); // logs 'default argument one & and a new value'
```

#### Acoplar ou Desacoplar Chama de Funções

```javascript
var helpers = {
/**
* debouncing, executes the function if there was no new event in $wait milliseconds
* @param func
* @param wait
* @param scope
* @returns {Function}
*/
debounce: function(func, wait, scope) {
var timeout;
return function() {
var context = scope || this, args = arguments;
var later = function() {
timeout = null;
func.apply(context, args);
};
clearTimeout(timeout);
timeout = setTimeout(later, wait);
};
},

/**
* In case of a "storm of events", this executes once every $threshold
* @param fn
* @param threshold
* @param scope
* @returns {Function}
*/
throttle: function(fn, threshold, scope) {
threshold || (threshold = 250);
var last, deferTimer;

return function() {
var context = scope || this;
var now = +new Date, args = arguments;

if (last && now < last + threshold) {
// Hold on to it
clearTimeout(deferTimer);
deferTimer = setTimeout(function() {
last = now;
fn.apply(context, args);
}, threshold);
} else {
last = now;
fn.apply(context, args);
}
};
}
};

var resizeHandler = function(){
console.log('do stuff');
};

// Debounce by waiting 0.25s (250ms) with "this" context
window.addEventListener('resize', helpers.debounce(resizeHandler, 250, this));
```
