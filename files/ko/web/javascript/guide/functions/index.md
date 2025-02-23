---
title: 함수
slug: Web/JavaScript/Guide/Functions
translation_of: Web/JavaScript/Guide/Functions
original_slug: Web/JavaScript/Guide/함수
---
{{jsSidebar("JavaScript Guide")}} {{PreviousNext("Web/JavaScript/Guide/Loops_and_iteration", "Web/JavaScript/Guide/Expressions_and_Operators")}}

함수는 JavaScript에서 기본적인 구성 블록 중의 하나입니다. 함수는 작업을 수행하거나 값을 계산하는 문장 집합 같은 자바스크립트 절차입니다. 함수를 사용하려면 함수를 호출하고자 하는 범위 내에서 함수를 정의해야만 합니다.

세부 사항에 대해서는 [exhaustive reference chapter about JavaScript functions](/ko/docs/Web/JavaScript/Reference/Functions)를 참조하세요.

## 함수 정의

### 함수 선언

함수 정의(또는 함수 선언)는 다음과 같은 [`함수`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/function "function") 키워드로 구성되어 있습니다:

- 함수의 이름
- 괄호 안에서 쉼표로 분리된 함수의 매개변수 목록
- 중괄호 `{ }` 안에서 함수를 정의하는 자바스크립트 표현

예를 들어, 다음의 코드는 `square`라는 간단한 함수를 정의하였습니다:

```js
function square(number) {
  return number * number;
}
```

함수 `square`은 `number`라는 하나의 매개변수를 가집니다. 이 함수는 인수 (즉, `number`) 자체를 곱하여 반환하는 하나의 문장으로 구성되어 있습니다. [`return`](/en-US/docs/Web/JavaScript/Reference/Statements/return "return") 문은 함수에 의해 반환된 값을 지정합니다.

```js
return number * number;
```

기본 자료형인 매개변수(number와 같은)는 **값으로** 함수에 전달됩니다; 즉, 값이 함수로 전달됩니다. 그러나 함수가 매개변수의 값을 바꾸더라도 이는 **전역적으로 또는 함수를 호출하는 곳에는 반영되지 않습니다**.

만약 여러분이 매개변수로 (예: {{jsxref("Array")}}이나 사용자가 정의한 객체와 같이 기본 자료형이 아닌 경우)를 전달하거나 함수가 객체의 속성을 변하게 하는 경우, 다음의 예처럼 그 변화는 함수 외부에서 볼 수 있습니다:

```js
function myFunc(theObject) {
  theObject.make = "Toyota";
}

var mycar = {make: "Honda", model: "Accord", year: 1998};
var x, y;

x = mycar.make; // x 의 값은 "Honda" 입니다.

myFunc(mycar);
y = mycar.make; // y 의 값은 "Toyota" 입니다.
                // (make 속성은 myFunc에서 변경되었습니다.)
```

### 함수 표현식

위에서 함수 선언은 구문적인 문(statement)이지만, **함수 표현식(** [function expression](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/function)**)**에 의해서 함수가 만들어 질 수도 있습니다. 이 같은 함수를 **익명**이라고 합니다. 이 말은 모든 함수가 이름을 가질 필요는 없다는 것을 뜻합니다. 예를 들어, 함수 `square`은 다음과 같이 정의 될 수도 있습니다:

```js
var square = function(number) { return number * number };
var x = square(4) // x 의 값은 16 입니다.
```

하지만, 함수 표현식에서 함수의 이름을 지정 할 수 있으며, 함수내에서 자신을 참조하는데 사용되거나, 디버거 내 스택 추적에서 함수를 식별하는 데 사용될 수 있습니다.

```js
var factorial = function fac(n) { return n<2 ? 1 : n*fac(n-1) };

console.log(factorial(3));
```

함수 표현식은 함수를 다른 함수의 매개변수로 전달할 때 편리합니다. 다음 예는 첫 번째 인자로로 함수를, 두 번째 인자로 배열을 받는 `map` 함수를 보여줍니다.

```js
function map(f,a) {
  var result = [], // Create a new Array
      i;
  for (i = 0; i != a.length; i++)
    result[i] = f(a[i]);
  return result;
}
```

다음 코드에서, 함수 표현식으로 정의된 함수를 인자로 받아, 2번 째 인자인 배열의 모든 요소에 대해 그 함수를 실행합니다.

<pre class="brush: js line-numbers language-js"><code class="language-js">function map(f, a) {
  var result = []; // Create a new Array
  var i; // Declare variable
  for (i = 0; i != a.length; i++)
    result[i] = f(a[i]);
      return result;
}
var f = function(x) {
   return x * x * x;
}
var numbers = [0, 1, 2, 5, 10];
var cube = map(f,numbers);
console.log(cube);</code></pre>

함수는 \[0, 1, 8, 125, 1000] 을 반환합니다.

JavaScript에서 함수는 조건에 의해 정의될 수 있습니다. 예를 들어, 다음 함수 정의는 오직 `num`이 0일 때 경우에 만 `myFunc`을 정의합니다.

```js
var myFunc;
if (num == 0){
  myFunc = function(theObject) {
    theObject.make = "Toyota"
  }
}
```

여기에 기술된 바와 같이 함수를 정의하는것에 더하여 {{jsxref("eval", "eval()")}} 과 같이 런타임에 문자열에서 함수들을 만들기위해 {{jsxref("Function")}} 생성자를 사용할 수 있습니다.

객체내의 한 속성이 함수인 경우 **메서드**라고 합니다. [Working with objects](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Working_with_Objects "en-US/docs/JavaScript/Guide/Working with Objects")에서 객체와 방법에 대해 자세히 알아보세요.

## 함수 호출

함수를 정의하는 것은 함수를 실행하는 것이 아닙니다. 함수를 정의하는 것은 간단히 함수의 이름을 지어주고, 함수가 호출될 때 무엇을 할지 지정 해주는 것입니다. 사실 함수를 **호출**하는 것은 나타나있는 매개변수를 가지고 지정된 행위를 수행하는 것입니다. 예를 들어, 만약 여러분이 함수 `square`를 정의한다면, 함수를 다음과 같이 호출할 수 있습니다.

```js
square(5);
```

위의 문장은 5라는 인수를 가지고 함수를 호출합니다. 함수는 이 함수의 실행문을 실행하고 값 25를 반환합니다.

함수는 호출될 때 범위 내에 있어야 합니다. 그러나 함수의 선언은 이 예에서와 같이, 호이스팅 될 수 있습니다. (코드에서 호출 아래에 선언문이 있습니다.):

```js
console.log(square(5));
/* ... */
function square(n) { return n*n }
```

함수의 범위는 함수가 선언된 곳이거나, 전체 프로그램 에서의 최상위 레벨(전역)에 선언된 곳입니다.

<div class="note"><p><strong>비고:</strong> 위에 구문을 사용하여 함수를 정의하는 경우에만 작동합니다 (즉, <code>function funcName(){}</code> ). 아래와 같은 코드는 작동되지 않습니다. 이것이 의미하는 바는, 함수 호이스팅은 오직 함수 선언과 함께 작동하고, 함수 표현식에서는 동작하지 않습니다.</p></div>

```js example-bad
console.log(square);   // square는 초기값으로 undefined를 가지고 호이스트된다.
console.log(square(5));  // TypeError: square는 함수가 아니다.
square = function (n) {
  return n * n;
}
```

함수의 인수는 문자열과 숫자에 제한되지 않습니다. 여러분은 함수에 전체 객체를 전달할 수 있습니다. `show_props()` 함수([Working with objects](/en-US/docs/Web/JavaScript/Guide/Working_with_Objects#Objects_and_Properties "https://developer.mozilla.org/en-US/docs/JavaScript/Guide/Working_with_Objects#Objects_and_Properties")에서 정의된)는 인수로 객체를 취하는 함수의 예입니다.

함수는 자신을 호출할 수 있습니다. 예를 들어, 팩토리얼을 재귀적으로 계산하는 함수가 있습니다:

```js
function factorial(n){
  if ((n == 0) || (n == 1))
    return 1;
  else
    return (n * factorial(n - 1));
}
```

여러분은 다음과 같이 1부터 5까지의 팩토리얼을 계산할 수 있습니다.

```js
var a, b, c, d, e;
a = factorial(1); // a gets the value 1
b = factorial(2); // b gets the value 2
c = factorial(3); // c gets the value 6
d = factorial(4); // d gets the value 24
e = factorial(5); // e gets the value 120
```

함수를 호출하는 다른 방법들이 있습니다. 함수를 동적 호출해야 하거나, 함수의 인수의 수가 달라져야 하거나, 함수 호출의 맥락이 런타임에서 결정된 특정한 객체로 설정될 필요가 있는 경우가 자주 있습니다. 함수가 그 자체로 객체이고 이들 객체는 차례로 메서드를({{jsxref("Function")}} 객체를 참조) 가지고 있습니다. 이들 중 하나인 {{jsxref("Function.apply", "apply()")}} 메서드는 이러한 목표를 달성하기 위해 사용될 수 있습니다.

<h2 class="deki-transform" id="함수의_범위">함수의 범위</h2>

함수 내에서 정의된 변수는 변수가 함수의 범위에서만 정의되어 있기 때문에, 함수 외부의 어느 곳에서든 액세스할 수 없습니다. 그러나, 함수가 정의된 범위 내에서 정의된 모든 변수나 함수는 액세스할 수 있습니다. 즉, 전역함수는 모든 전역 변수를 액세스할 수 있습니다. 다른 함수 내에서 정의 된 함수는 부모 함수와 부모 함수가 액세스 할 수 있는 다른 변수에 정의된 모든 변수를 액세스할 수 있습니다.

```js
// The following variables are defined in the global scope
var num1 = 20,
    num2 = 3,
    name = "Chamahk";

// This function is defined in the global scope
function multiply() {
  return num1 * num2;
}

multiply(); // Returns 60

// A nested function example
function getScore () {
  var num1 = 2,
      num2 = 3;

  function add() {
    return name + " scored " + (num1 + num2);
  }

  return add();
}

getScore(); // Returns "Chamahk scored 5"
```

## 범위와 함수 스택

### 재귀

함수는 자신을 참조하고 호출할 수 있습니다. 함수가 자신을 참조하는 방법은 세 가지가 있습니다.

1.  함수의 이름
2.  [`arguments.callee`](/ko/docs/Web/JavaScript/Reference/Functions/arguments/callee)
3.  함수를 참조하는 범위 내 변수

예를 들어, 다음 함수의 정의를 고려해보세요.

```js
var foo = function bar() {
   // statements go here
};
```

함수 본문 내에서 다음은 모두 동일합니다.

1.  `bar()`
2.  `arguments.callee()`
3.  `foo()`

자신을 호출하는 함수를 *재귀 함수*라고 합니다. 어떤 면에서, 재귀는 루프와 유사합니다. 둘 다 동일한 코드를 여러 번 실행하고, 조건(무한 루프를 방지하거나, 이 경우에는 오히려 무한 재귀하는)을 요구합니다. 예를 들어, 다음 루프는:

```js
var x = 0;
while (x < 10) { // "x < 10" is the loop condition
   // do stuff
   x++;
}
```

아래와 같이 재귀 함수와 그 함수에 대한 호출로 변환될 수 있습니다.

```js
function loop(x) {
  if (x >= 10) // "x >= 10" 는 탈출 조건 ("!(x < 10)"와 동등)
    return;
  // do stuff
  loop(x + 1); // the recursive call
}
loop(0);
```

그러나 일부 알고리즘은 단순 재귀 루프로 변환할 수 없습니다. 예를 들어, 트리 구조(가령, [DOM](/en-US/docs/DOM))의 모든 노드를 얻는 것은 재귀를 사용하여 보다 쉽게 할 수 있습니다:

```js
function walkTree(node) {
  if (node == null) //
    return;
  // do something with node
  for (var i = 0; i < node.childNodes.length; i++) {
    walkTree(node.childNodes[i]);
  }
}
```

함수 `loop` 와 비교하여, 각 재귀 호출 자체는 여기에 많은 재귀 호출을 만듭니다.

재귀적 알고리즘은 비 재귀적인 알고리즘으로 변환 할 수 있습니다. 그러나 변환된 알고리즘이 훨씬 더 복잡하며 그렇게 함으로써 스택의 사용을 요구합니다. 사실, 재귀 자체가 함수 스택을 사용 합니다.

스택형 동작은 다음의 예에서 볼 수 있습니다:

```js
function foo(i) {
  if (i < 0)
    return;
  console.log('begin:' + i);
  foo(i - 1);
  console.log('end:' + i);
}
foo(3);

// Output:

// begin:3
// begin:2
// begin:1
// begin:0
// end:0
// end:1
// end:2
// end:3
```

### 중첩된 함수와 클로저

여러분은 함수 내에 함수를 끼워 넣을 수 있습니다. 중첩 된 (내부) 함수는 그것을 포함하는 (외부) 함수와 별개입니다. 그것은 또한 *클로저*를 형성합니다. 클로저는 그 변수(“폐쇄”라는 표현)를 결합하는 환경을 자유롭게 변수와 함께 가질 수 있는 표현(전형적인 함수)입니다.

중첩 함수는 클로저이므로, 중첩된 함수는 그것을 포함하는 함수의 인수와 변수를 “상속”할 수 있는 것을 의미합니다. 즉, 내부 함수는 외부 함수의 범위를 포함합니다.

요약하면:

- 내부 함수는 외부 함수의 명령문에서만 액세스할 수 있습니다.

<!---->

- 내부 함수는 클로저를 형성합니다: 외부 함수는 내부 함수의 인수와 변수를 사용할 수 없는 반면에, 내부 함수는 외부 함수의 인수와 변수를 사용할 수 있습니다.

다음 예는 중첩된 함수를 보여줍니다:

```js
function addSquares(a,b) {
  function square(x) {
    return x * x;
  }
  return square(a) + square(b);
}
a = addSquares(2,3); // returns 13
b = addSquares(3,4); // returns 25
c = addSquares(4,5); // returns 41
```

내부 함수는 클로저를 형성하기 때문에, 여러분은 외부 함수를 호출하고, 외부 및 내부 함수 모두에 인수를 지정할 수 있습니다.

```js
function outside(x) {
  function inside(y) {
    return x + y;
  }
  return inside;
}
fn_inside = outside(3); // Think of it like: give me a function that adds 3 to whatever you give it
result = fn_inside(5); // returns 8

result1 = outside(3)(5); // returns 8
```

### 변수의 보존

중첩된 내부 함수가 반환될 때 외부 함수의 인수 `x`가 보존된다는 점을 알 수 있습니다. 클로저는 그것을 참조하는 모든 범위에서 인수와 변수를 보존해두어야 합니다. 매번 호출될 때마다 잠재적으로 다른 인수를 제공할 수 있기 때문에, 클로저는 외부 함수에 대하여 매번 새로 생성됩니다. 메모리는 그 무엇도 내부 함수에 접근하지 않을 때만 해제됩니다.

변수의 보존은 일반 객체에서 참조를 저장해두는 것과 다르지 않지만, 사용자가 직접 참조를 설정하는 것이 아니고 자세히 들여다볼 수 없어서 종종 명확하지 않습니다.

<h3 id="Multiply-nested_functions" name="Multiply-nested_functions">다중 중첩 함수</h3>

함수는 다중 중첩될 수 있습니다. 즉, 함수 (C)를 포함하는 함수 (B)를 포함하는 함수 (A). 여기에서 두 함수 B와 C는 모두 클로저를 형성합니다. 그래서 B는 A를 엑세스할 수 있고, C는 B를 액세스 할 수 있습니다. 이와 같이, 클로저는 다중 범위를 포함 할 수 있습니다; 그들은 재귀적으로 그것을 포함하는 함수의 범위를 포함합니다. 이것을 *범위 체이닝*이라 합니다.(그것을 “체이닝”이라 하는 이유는 추후에 설명할 것입니다.)

다음 예를 살펴 보겠습니다:

```js
function A(x) {
  function B(y) {
    function C(z) {
      console.log(x + y + z);
    }
    C(3);
  }
  B(2);
}
A(1); // logs 6 (1 + 2 + 3)
```

이 예에서, C는 B의 y와 A의 x를 엑세스 합니다. 이 때문에 수행할 수 있습니다:

1.  B는 A를 포함하는 클로저를 형성합니다. 즉, B는 A의 인수와 변수를 엑세스할 수 있습니다.
2.  C는 B를 포함하는 클로저를 형성합니다.
3.  B의 클로저는 A를 포함하고, C의 클로저는 A를 포함하기 때문에, C는 B와 A의 인수와 변수를 엑세스할 수 있습니다. 즉, 순서대로 C는 A와 B의 범위를 체이닝합니다.

그러나 역은 사실이 아닙니다. A는 C에 접근 할 수 없습니다. 왜냐하면 A는 B의 인수와 변수(C는 B변수)에 접근할수 없기 때문입니다. 그래서 C는 B에게만 사적으로 남게됩니다.

### 이름 충돌

클로저의 범위에서 두 개의 인수 또는 변수의 이름이 같은 경우, *이름 충돌*이 있습니다. 더 안쪽 범위가 우선순위를 갖습니다. 그래서 가장 바깥 범위는 우선순위가 가장 낮은 반면에, 가장 안쪽 범위는 가장 높은 우선순위를 갖습니다. 이것이 범위 체인(scope chaini)입니다. 체인에서 첫번째는 가장 안쪽 범위이고, 마지막은 가장 바깥 쪽의 범위입니다. 다음 사항을 고려하세요:

```js
function outside() {
  var x = 10;
  function inside(x) {
    return x;
  }
  return inside;
}
result = outside()(20); // returns 20 instead of 10
```

이름 충돌이 x를 반환하는 문과 내부의 매개 변수 x와 외부 변수 x 사이에서 발생합니다. 여기에서 범위 체이닝은 {내부, 외부, 전역 객체}입니다. 따라서 내부의 x는 외부의 x보다 높은 우선순위를 갖게 되고, 20(내부의 x)이 10(외부의 x) 대신에 반환됩니다.

## 클로저

클로저는 자바스크립트의 강력한 기능 중 하나입니다. 자바스크립트는 함수의 중첩(함수 안에 함수를 정의하는것)을 허용하고, 내부함수가 외부 함수 안에서 정의된 모든 변수와 함수들을 완전하게 접근 할 수 있도록 승인해줍니다.(그리고 외부함수가 접근할수 있는 모든 다른 변수와 함수들까지) 그러나 외부 함수는 내부 함수 안에서 정의된 변수와 함수들에 접근 할 수 없습니다. 이는 내부 함수의 변수에 대한 일종의 캡슐화를 제공합니다. 또한, 내부함수는 외부함수의 범위에 접근할 수 있기 때문에, 내부 함수가 외부 함수의 수명을 초과하여 생존하는 경우, 외부함수에서 선언된 변수나 함수는 외부함수의 실행 기간보다 오래갑니다. 클로저는 내부 함수가 어떻게든 외부 함수 범위 밖의 모든 범위에서 사용 가능해지면 생성됩니다.

```js
var pet = function(name) {   // 외부 함수는 'name'이라 불리는 변수를 정의합니다.
  var getName = function() {
    return name;             // 내부 함수는 외부 함수의 'name' 변수에 접근합니다.
  }
  return getName;            // 내부 함수를 리턴함으로써, 외부 범위에 노출됩니다.
},
myPet = pet("Vivie");

myPet();                     // "Vivie"로 리턴합니다.
```

클로저는 위 코드보다 더 복잡해 질 수도 있습니다. 외부 함수의 내부 변수를 다루는 메서드를 포함한 객체도 반환될 수도 있습니다.

```js
var createPet = function(name) {
  var sex;

  return {
    setName: function(newName) {
      name = newName;
    },

    getName: function() {
      return name;
    },

    getSex: function() {
      return sex;
    },

    setSex: function(newSex) {
      if(typeof newSex == "string" && (newSex.toLowerCase() == "male" || newSex.toLowerCase() == "female")) {
        sex = newSex;
      }
    }
  }
}

var pet = createPet("Vivie");
pet.getName();                  // Vivie

pet.setName("Oliver");
pet.setSex("male");
pet.getSex();                   // male
pet.getName();                  // Oliver
```

위 코드에서, 외부 함수의 'name' 이란 변수는 내부 함수에서 접근이 가능합니다. 그리고 그 내장 함수를 통하는 방법 말고는 내부 변수로 접근할 수 없습니다. 내부 함수의 내부 변수는 외부 인수와 변수를 안전하게 저장합니다. 내부 변수는 내부 함수가 작동하기 위해 '지속적'이고 '캡슐화된' 데이터를 보유합니다. 함수는 변수로 할당되거나, 이름을 가질 필요가 없습니다.

```js
var getCode = (function(){
  var secureCode = "0]Eal(eh&2";    // A code we do not want outsiders to be able to modify...

  return function () {
    return secureCode;
  };
})();

getCode();    // Returns the secureCode
```

그러나 클로저를 쓰면서 조심해야 할 위험이 많이 있습니다. 만약 내부 함수가 외부 함수의 범위에 있는 이름과 같은 변수를 정의하였을 경우, 다시는 외부 함수 범위의 변수를 참조(접근)할 방법이 없습니다.

```js
var createPet = function(name) {  // 외부 함수가 "name" 이라는 변수를 정의하였다
  return {
    setName: function(name) {    // 내부 함수 또한 "name" 이라는 변수를 정의하였다
      name = name;               // ??? 어떻게 우리는 외부 함수에 정의된 "name"에 접근할까???
    }
  }
}
```

## 인수(arguments) 객체 사용하기

함수의 인수는 배열과 비슷한 객체로 처리가 됩니다. 함수 내에서는, 전달 된 인수를 다음과 같이 다룰 수 있습니다. :

```js
arguments[i]
```

i 는 0 으로 시작하는 순서 번호입니다. 따라서 함수에 전달된 첫 번째 인수는 `arguments[0]` 입니다. 총 인수의 개수는 `arguments.length` 에서 얻을 수 있습니다.

인수(`arguments`) 객체를 이용하면, 보통 함수에 정의된 개수보다 많은 인수를 넘겨주면서 함수를 호출할 수 있습니다. 이것은 얼마나 많은 인수가 함수로 넘겨질지 모르는 상황에서 유용합니다. `arguments.length`를 함수에 실제로 넘겨받은 인수의 수를 알아낼 때 사용할 수 있고 , 각각의 인수에 인수(`arguments`) 객체를 이용하여 접근 할 수 있습니다.

예를 들어, 몇 개의 문자열을 연결하는 함수를 생각해 봅시다. 이 함수의 유일한 형식 인수는 각 문자열을 구분해주는 문자를 나타내는 문자열입니다 . 이 함수는 다음과 같이 정의됩니다:

```js
function myConcat(separator) {
   var result = ""; // 리스트를 초기화한다
   var i;
   // arguments를 이용하여 반복한다
   for (i = 1; i < arguments.length; i++) {
      result += arguments[i] + separator;
   }
   return result;
}
```

어떤 개수의 인수도 이 함수로 넘겨줄 수 있고, 이 함수는 각각의 인수를 하나의 문자열 "리스트" 로 연결합니다. :

```js
// returns "red, orange, blue, "
myConcat(", ", "red", "orange", "blue");

// returns "elephant; giraffe; lion; cheetah; "
myConcat("; ", "elephant", "giraffe", "lion", "cheetah");

// returns "sage. basil. oregano. pepper. parsley. "
myConcat(". ", "sage", "basil", "oregano", "pepper", "parsley");
```

> **참고:** 인수(arguments) 객체는 배열과 닮은 것이지 배열이 아닙니다. 인수(arguments) 객체는 번호 붙여진 인덱스와 길이 속성을 가지고 있다는 점에서 배열과 닮은 것입니다. 인수(arguments) 객체는 배열을 다루는 모든 메서드를 가지고 있지 않습니다.

더 자세한 정보를 얻고 싶으면 자바스크립트 참조문의 {{jsxref("Function")}}객체에 대하여 보세요.

## 함수의 매개변수

ECMAScript 2015와 함께 시작된,두 종류의 매개변수가 있습니다 : 디폴트 매개변수 , 나머지 매개변수.

### 디폴트 매개변수

자바스크립트에서, 함수의 매개변수는 `undefined` 가 기본으로 설정됩니다. 그러나, 어떤 상황에서는 다른 값을 기본값으로 가진 것이 유용할 때가 있습니다. 이때가 디폴트 매개변수가 도움을 줄 수 있는 상황입니다.

옛날엔, 기본값을 설정하는 보편적인 전략은 함수의 본문에서 매개변수 값을 테스트하여 그 값이 `undefined` 인 경우에 값을 할당하는 것이었습니다. 다음과 같은 예제에서, 함수호출 시 `b` 매개변수에 아무 값을 주지 않으면, `a*b` 계산 시 `b` 매개변수의 값은 `undefined` 일 것이므로 `multiply` 함수 호출은 `NaN`을 리턴할 것입니다. 그러나 이런 것은 이 예제의 2번째 줄에서 걸립니다:

```js
function multiply(a, b) {
  b = typeof b !== 'undefined' ?  b : 1;

  return a*b;
}

multiply(5); // 5
```

디폴트 매개변수와 함께라면, 함수 본문에서 검사하는 부분은 필요가 없습니다. 이제 , 함수 머리에서 `b` 의 기본값에 간단히 1을 넣어주면 됩니다:

```js
function multiply(a, b = 1) {
  return a*b;
}

multiply(5); // 5
```

더 자세한 내용을 보고 싶으시면, [default parameters](/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters) 문서를 참조하세요.

### 나머지 매개변수

[나머지 매개변수](/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters) 구문을 사용하면 배열로 불확실한 개수의 인수를 나타낼 수 있습니다. 이 예제에서, 우리는 나머지 매개변수를 2번째 인수부터 마지막 인수까지 얻기 위하여 사용하였습니다. 그리고 우리는 첫번째 값으로 나머지 매개변수에 곱하였습니다. 이 예제는 다음 섹션에서 소개할 화살표(arrow) 함수 입니다.

```js
function multiply(multiplier, ...theArgs) {
  return theArgs.map(x => multiplier * x);
}

var arr = multiply(2, 1, 2, 3);
console.log(arr); // [2, 4, 6]
```

## 화살표 함수

[화살표 함수 표현](/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) (**뚱뚱한 화살표(fat arrow) 함수라고 알려진**)은 함수 표현과 비교하였을때 짧은 문법을 가지고 있고 사전적으로 this 값을 묶습니다. 화살표 함수는 언제나 익명입니다. hacks.mozilla.org 블로그 포스트 "[ES6 In Depth: Arrow functions](https://hacks.mozilla.org/2015/06/es6-in-depth-arrow-functions/)" 를 참조하세요.

화살표 함수 소개에 영향을 주는 두 요소: 더 짧은 함수와 바인딩 되지않은 `this`.

### 더 짧은 함수

어떤 함수적 패턴에서는, 더 짧은 함수가 환영받습니다. 다음을 비교해 보세요:

```js
var a = [
  "Hydrogen",
  "Helium",
  "Lithium",
  "Beryl­lium"
];

var a2 = a.map(function(s){ return s.length });

console.log(a2); // logs [8, 6, 7, 9]

var a3 = a.map( s => s.length );

console.log(a3); // logs [8, 6, 7, 9]
```

### 사전적 `this`

화살표 함수에서, 모든 new함수들은 그들의 [this](/en-US/docs/Web/JavaScript/Reference/Operators/this) 값을 정의합니다 (생성자로서의 새로운 객체, 정의되지 않은 [strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)의 함수 호출, 함수가 "object method"로 호출했을때의 context object ,등등.). 이런 것은 객체지향 프로그래밍 스타일에서 짜증을 불러 일으킵니다.

```js
function Person() {
  // The Person() constructor defines `this` as itself.
  this.age = 0;

  setInterval(function growUp() {
    // In nonstrict mode, the growUp() function defines `this`
    // as the global object, which is different from the `this`
    // defined by the Person() constructor.
    this.age++;
  }, 1000);
}

var p = new Person();
```

IECMAScript 3/5 에서는, 이 문제는 `this` 안의 값을 뒤덮을 수 있는변수에 할당하면서 고쳐졌습니다.

```js
function Person() {
  var self = this; // Some choose `that` instead of `self`.
                   // Choose one and be consistent.
  self.age = 0;

  setInterval(function growUp() {
    // The callback refers to the `self` variable of which
    // the value is the expected object.
    self.age++;
  }, 1000);
}
```

또는, 적절한 `this` 값이 `growUp()` 함수에 전달되도록, [바인딩된 함수](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)가 생성될 수 있습니다.

화살표 함수에는 `this;`가 없습니다. 화살표 함수를 포함하는 객체 값이 사용됩니다. 따라서 다음 코드에서 setInterval에 전달 된 함수 내의 this 값은 화살표 함수를 둘러싼 함수의 this와 같은 값을 갖습니다.

```javascript
function Person() {
  this.age = 0;

  setInterval(() => {
    this.age++; // |this| properly refers to the person object
  }, 1000);
}

var p = new Person();
```

## 미리 정의된 함수들

자바스크립트에는 최고 등급의 몇가지 내장함수가 있습니다:

- {{jsxref("Global_Objects/eval", "eval()")}}
  - : **`eval()`** 메소드는 문자열로 표현된 자바스크립트 코드를 수행합니다.
- {{jsxref("Global_Objects/uneval", "uneval()")}} {{non-standard_inline}}
  - : **`uneval()`** 메소드는 {{jsxref("Object")}}의 소스코드를 표현하는 문자열을 만듭니다.
- {{jsxref("Global_Objects/isFinite", "isFinite()")}}
  - : 전역 **`isFinite()`** 함수는 전달받은 값이 유한한지 결정합니다. 만약 필요하다면, 매개변수는 첫번째로 숫자로 변환됩니다.
- {{jsxref("Global_Objects/isNaN", "isNaN()")}}
  - : **`isNaN()`** 함수는 {{jsxref("Global_Objects/NaN", "NaN")}}인지 아닌지 결정합니다. Note: `isNaN` 함수 안의 강제 변환은 [흥미로운](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/isNaN#Description) 규칙을 가지고 있습니다; {{jsxref("Number.isNaN()")}}을 대신 사용하고 싶을것입니다, ECMAScript 6 에서 정의된,또는 값이 숫자값이 아닐때, [`typeof`](/en-US/docs/Web/JavaScript/Reference/Operators/typeof) 를 사용할 수도 있습니다 .
- {{jsxref("Global_Objects/parseFloat", "parseFloat()")}}
  - : **`parseFloat()`** 함수는 문자열 인수 값을 해석하여 부동소숫점 수를 반환합니다.
- {{jsxref("Global_Objects/parseInt", "parseInt()")}}
  - : **`parseInt()`** 함수는 문자열 인수 값을 해석하여 특정한 진법의 정수를 반환합니다 (수학적 수 체계를 기반으로 해서).
- {{jsxref("Global_Objects/decodeURI", "decodeURI()")}}
  - : **`decodeURI()`** 함수는 사전에 {{jsxref("Global_Objects/encodeURI", "encodeURI")}}을 통해 만들어지거나 비슷한 과정을 통해 만들어진 URI(Uniform Resource Identifier) 를 해독합니다.
- {{jsxref("Global_Objects/decodeURIComponent", "decodeURIComponent()")}}
  - : **`decodeURIComponent()`** 메소드는 사전에{{jsxref("Global_Objects/encodeURIComponent", "encodeURIComponent")}}를 통하여 만들어 지거나 또는 비슷한 과정을 통해 만들어진 URI (Uniform Resource Identifier) 컴포넌트를 해독합니다.
- {{jsxref("Global_Objects/encodeURI", "encodeURI()")}}
  - : **`encodeURI()`** 메소드는 URI(Uniform Resource Identifier)를 각 인스턴스의 특정한 문자를 한개, 두개,세개, 또는 네개의 UTF-8인코딩으로 나타내어지는 연속된 확장문자들과 바꾸는 방법으로 부호화 합니다 .(두"surrogate"문자로 구성된 문자들은 오직 네개의 연속된 확장문자 입니다. ).
- {{jsxref("Global_Objects/encodeURIComponent", "encodeURIComponent()")}}
  - : **`encodeURIComponent()`** 메소드는 URI(Uniform Resource Identifier) 컴포넌트를 각 인스턴스의 특정한 문자를 한개, 두개,세개, 또는 네개의 UTF-8인코딩으로 나타내어지는 연속된 확장문자들과 바꾸는 방법으로 부호화 합니다 .(두"surrogate"문자로 구성된 문자들은 오직 네개의 연속된 확장문자 입니다. ).).
- {{jsxref("Global_Objects/escape", "escape()")}} {{deprecated_inline}}
  - : 곧 사라질 **`escape()`** 메소드는 한 문자열에서 특정 문자들이 16진 확장 비트열로 바뀌어진 문자열로 계산합니다. {{jsxref("Global_Objects/encodeURI", "encodeURI")}} 또는 {{jsxref("Global_Objects/encodeURIComponent", "encodeURIComponent")}} 를 사용하세요.
- {{jsxref("Global_Objects/unescape", "unescape()")}} {{deprecated_inline}}
  - : 곧 사라질 **`unescape()`** 메소드는 문자열에서 확장 비트열이 확장 비트열이 나타내는 문자로 바뀌어진 문자열로 계산합니다. {{jsxref("Global_Objects/escape", "escape")}}에서 확장 비트열이 소개될 것입니다. `unescape()` 메소드가 곧 사라지기 때문에, {{jsxref("Global_Objects/decodeURI", "decodeURI()")}} or {{jsxref("Global_Objects/decodeURIComponent", "decodeURIComponent")}} 를 대신 사용하세요.

{{PreviousNext("Web/JavaScript/Guide/Loops_and_iteration", "Web/JavaScript/Guide/Expressions_and_Operators")}}
