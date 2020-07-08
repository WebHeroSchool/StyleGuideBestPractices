# 1. Объекты и Массивы
Для создания объекта или массива используйте литеральную нотацию
``` js
// плохой пример:
const item = new Object();
const items = new Array();

// хороший пример:
const item = {};
const items = [];
```
# 2. Функции
 Используйте функциональные выражения вместо объявлений функций.
``` js
// плохой пример:
function foo() {
  // ...
}

const foo = function () {
  // ...
};

// хороший пример:
const foo = function uniqueMoreDescriptiveLexicalFoo() {
  // ...
};
```
# 3. Классы и конструкторы
Всегда используйте class. Избегайте прямых манипуляций с prototype
``` js
// плохой пример:
function Queue(contents = []) {
  this.queue = [...contents];
}
Queue.prototype.pop = function () {
  const value = this.queue[0];
  this.queue.splice(0, 1);
  return value;
};

// хороший пример:
class Queue {
  constructor(contents = []) {
    this.queue = [...contents];
  }
  pop() {
    const value = this.queue[0];
    this.queue.splice(0, 1);
    return value;
  }
}
```
# 4. Свойства
+ Используйте точечную нотацию для доступа к свойствам.
``` js
const luke = {
  jedi: true,
  age: 28,
};

// плохой пример:
const isJedi = luke['jedi'];

// хороший пример:
const isJedi = luke.jedi;
```
+ Используйте скобочную нотацию [], когда название свойства хранится в переменной.
``` js
const luke = {
  jedi: true,
  age: 28,
};

function getProp(prop) {
  return luke[prop];
}

const isJedi = getProp('jedi');
```
# 5. Избегайте использования унарных инкрементов и декрементов (++, --)
Согласно документации, унарные инкремент и декремент автоматически вставляют точку с запятой, что может стать причиной трудноуловимых ошибок при инкрементировании и декрементировании значений. Также нагляднее изменять ваши значения таким образом num += 1 вместо num++ или num ++. 
``` js
// плохой пример:
const array = [1, 2, 3];
let num = 1;
num++;
--num;

let sum = 0;
let truthyCount = 0;
for (let i = 0; i < array.length; i++) {
  let value = array[i];
  sum += value;
  if (value) {
    truthyCount++;
  }
}

// хороший пример:
const array = [1, 2, 3];
let num = 1;
num += 1;
num -= 1;

const sum = array.reduce((a, b) => a + b, 0);
const truthyCount = array.filter(Boolean).length;
```
# 6. Используйте === и !== вместо == и !=. Используйте сокращения для булевских типов, а для строк и чисел применяйте явное сравнение.
``` js
// плохой пример:
if (isValid === true) {
  // ...
}

if (name) {
  // ...
}

if (collection.length) {
  // ...
}

// хороший пример:
if (isValid) {
  // ...
}

if (name !== '') {
  // ...
}

if (collection.length > 0) {
  // ...
}
```
# 7. Блоки
+ Используйте фигурные скобки, когда блок кода занимает несколько строк
``` js
// плохой пример:
if (test)
  return false;

function foo() { return false; }

// хороший пример:
if (test) return false;

if (test) {
  return false;
}
```
+ Если блоки кода в условии if и else занимают несколько строк, расположите оператор else на той же строчке, где находится закрывающая фигурная скобка блока if.
``` js
// плохой пример:
if (test) {
  thing1();
  thing2();
}
else {
  thing3();
}

// хороший пример:
if (test) {
  thing1();
  thing2();
} else {
  thing3();
}
```
+ Если в блоке if всегда выполняется оператор return, последующий блок else не нужен.
``` js
// плохой пример:
function foo() {
  if (x) {
    return x;
  } else {
    return y;
  }
}

// хороший пример:
function foo() {
  if (x) {
    return x;
  }

  return y;
}
```
# 8. Управляющие операторы
Если ваш управляющий оператор (if, while и т.д.) слишком длинный или превышает максимальную длину строки, то каждое (сгруппированное) условие можно поместить на новую строку. Логический оператор должен располагаться в начале строки.
``` js
// плохой пример:
if ((foo === 123 || bar === 'abc') && doesItLookGoodWhenItBecomesThatLong() && isThisReallyHappening()) {
  thing1();
}

if (foo === 123 &&
  bar === 'abc') {
  thing1();
}

if (foo === 123
  && bar === 'abc') {
  thing1();
}

if (
  foo === 123 &&
  bar === 'abc'
) {
  thing1();
}

// хороший пример:
if (
  foo === 123
  && bar === 'abc'
) {
  thing1();
}

if (
  (foo === 123 || bar === 'abc')
  && doesItLookGoodWhenItBecomesThatLong()
  && isThisReallyHappening()
) {
  thing1();
}

if (foo === 123 && bar === 'abc') {
  thing1();
}
```
# 9. Комментарии
+ Используйте конструкцию /** ... */ для многострочных комментариев.
``` js
// плохой пример:

// make() возвращает новый элемент
// соответствующий переданному названию тега
//
// @param {String} tag
// @return {Element} element
function make(tag) {

  // ...

  return element;
}

// хороший пример:

/**
 * make() возвращает новый элемент
 * соответствующий переданному названию тега
 */
function make(tag) {

  // ...

  return element;
}
```
+  Используйте двойной слеш // для однострочных комментариев. Располагайте такие комментарии отдельной строкой над кодом, который хотите пояснить. Если комментарий не является первой строкой блока, добавьте сверху пустую строку.
``` js
// плохой пример:

const active = true;  // это текущая вкладка

function getType() {
  console.log('fetching type...');
  // установить по умолчанию тип 'no type'
  const type = this.type || 'no type';

  return type;
}

// хороший пример:

// это текущая вкладка
const active = true;

/ хорошо
function getType() {
  console.log('fetching type...');

  // установить по умолчанию тип 'no type'
  const type = this.type || 'no type';

  return type;
}
```
+ Начинайте все комментарии с пробела, так их проще читать
``` js
// плохой пример:

//это текущая вкладка
const active = true;

// хороший пример:

// это текущая вкладка
const active = true;
```
# 10. Соглашение об именовании
+ Избегайте названий из одной буквы. Имя должно быть наглядным.
``` js
// плохой пример:
function q() {
  // ...
}

// хороший пример:
function query() {
  // ...
}
```
+ Используйте camelCase для именования объектов, функций и экземпляров. 
``` js
// плохой пример:
const OBJEcttsssss = {};
const this_is_my_object = {};
function c() {}

// хороший пример:
const thisIsMyObject = {};
function thisIsMyFunction() {}
```
+ Используйте PascalCase только для именования конструкторов и классов. 
``` js
// плохой пример:
function user(options) {
  this.name = options.name;
}

const bad = new user({
  name: 'nope',
});

// хороший пример:
class User {
  constructor(options) {
    this.name = options.name;
  }
}

const good = new User({
  name: 'yup',
});
```
+ Не сохраняйте ссылку на this. Используйте стрелочные функции или метод bind().
``` js
// плохой пример:
function foo() {
  const self = this;
  return function () {
    console.log(self);
  };
}

// хороший пример:
function foo() {
  return () => {
    console.log(this);
  };
}
```
