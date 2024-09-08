### Javascript Object 

## assign()
// > Merging objects with same properties
const o1 = { a: 1, b: 1, c: 1 };
const o2 = { b: 2, c: 2 };
const o3 = { c: 3 };

const copiedObj = Object.assign({}, o1, o2, o3);
console.log(copiedObj); // { a: 1, b: 2, c: 3 }
// The properties are overwritten by other objects that have the same properties later in the parameters order.

// > Cloning an object
const obj = { a: 1 };
const copy = Object.assign({}, obj);
console.log(copy); // { a: 1 }

-- Object(o1, o2, o3) 를 선언, 할당하고 assign 메서드를 이용해 copiedObj를 생성한다.  
-- (o1, o2, o3)의 프로퍼티 값을 각각 수정하여도 서로에게 영향을 주지 않는다. 
-- 다만 객체 내부의 객체를 수정했을 때는 동시에 수정이 될 수 있다. (원시자료형인 경우 깊은 복사, 참조자료형인 경우 얕은 복사)

## create() 
const person = {
  isHuman: false,
  printIntroduction: function() {
    console.log(`My name is ${this.name}. Am I human? ${this.isHuman}`);
  }
};

const me = Object.create(person);

me.name = 'Matthew'; // "name" is a property set on "me", but not on "person"
me.isHuman = true; // Inherited properties can be overwritten

me.printIntroduction();
// Expected output: "My name is Matthew. Am I human? true"

-- 지정된 프로토타입 객체 및 속성을 갖는 새 객체를 만든다. 
  -- 매개변수 
    1) proto : 새로 만든 객체의 프로토타입이어야 할 객체 
    2) propertiesObject : 선택사항, 지정되고 undefined가 아니면 자신의 속성이 열거 가능한 객체는 해당 속성명으로 새로 만든 객체에 추가될 속성 설명자를 지정한다. 
-- 상속의 기능을 제대로 구현하기 위해서는 Object.create()를 활용한다. 

## entries()
// Array-like object
const obj = { 0: "a", 1: "b", 2: "c" };
console.log(Object.entries(obj)); // [ ['0', 'a'], ['1', 'b'], ['2', 'c'] ]

// Using for...of loop
const obj = { a: 5, b: 7, c: 9 };
for (const [key, value] of Object.entries(obj)) {
  console.log(`${key} ${value}`); // "a 5", "b 7", "c 9"
}

// Using array methods
Object.entries(obj).forEach(([key, value]) => {
  console.log(`${key} ${value}`); // "a 5", "b 7", "c 9"
});

-- 자바스크립트 객체를 배열로 변환해주는 메소드이다. 
-- 객체의 {key : value} 형식을 배열 형태의 [key, value]로 변환하여 준다. 
-- 주로 Object에서는 사용할 수 없는 자바스크립트 Array 메소드를 (forEach(), find(), filter()...등 ) 사용하고자 할 때 Object를 Array로 변환시키기에 유용하다. 


## fromEntries()
const entries = new Map([
  ['foo', 'bar'],
  ['baz', 42]
]);

const obj = Object.fromEntries(entries);

console.log(obj);
// Expected output: Object { foo: "bar", baz: 42 }

## hasOwnProperty()
const buz = {
  fog: "stack",
};

for (const name in buz) {
  if (buz.hasOwnProperty(name)) {
    console.log(`this is fog (${name}) for sure. Value: ${buz[name]}`);
  } else {
    console.log(name); // toString or something else
  }
}

## hasOwnProperty() (2)
var foo = {
  hasOwnProperty: function() {
    return false;
  },
  bar: 'Here be dragons'
};

foo.hasOwnProperty('bar'); // always returns false

// Use another Object's hasOwnProperty and call it with 'this' set to foo
({}).hasOwnProperty.call(foo, 'bar'); // true

// It's also possible to use the hasOwnProperty property from the Object prototype for this purpose
Object.prototype.hasOwnProperty.call(foo, 'bar'); // true


## keys()
const object1 = {
  a: 'somestring',
  b: 42,
  c: false
};

console.log(Object.keys(object1));
// Expected output: Array ["a", "b", "c"]

## values()
const object1 = {
  a: 'somestring',
  b: 42,
  c: false
};

console.log(Object.values(object1));
// Expected output: Array ["somestring", 42, false]