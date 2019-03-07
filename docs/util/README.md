# Util

- [Util](#Util)
  - [attempt](#attempt)
  - [bindAll](#bindAll)
  - [cond](#cond)
  - [conforms](#conforms)
  - [constant](#constant)
  - [defaultTo](#defaultTo)
  - [flow](#flow)
  - [flowRight](#flowRight)
  - [identity](#identity)
  - [iteratee](#iteratee)
  - [matches](#matches)
  - [matchesProperty](#matchesProperty)
  - [method](#method)
  - [methodOf](#methodOf)
  - [mixin](#mixin)
  - [noConflict](#noConflict)
  - [noop](#noop)
  - [nthArg](#nthArg)
  - [over](#over)
  - [overEvery](#overEvery)
  - [overSome](#overSome)
  - [property](#property)
  - [propertyOf](#propertyOf)
  - [range](#range)
  - [rangeRight](#rangeRight)
  - [runInContext](#runInContext)
  - [stubArray](#stubArray)
  - [stubFalse](#stubFalse)
  - [stubObject](#stubObject)
  - [stubString](#stubString)
  - [stubTrue](#stubTrue)
  - [times](#times)
  - [toPath](#toPath)
  - [uniqueId](#uniqueId)

## identity

```js
_.identity(value);
```

受け取った第１引数を返す。

```js
const object = { a: 1 };
const object2 = { b: 1 };

console.log(_.identity(object, object2));
// => {a: 1}
console.log(_.identity(object, object2) === object);
// => true
```

## iteratee

```js
_.iteratee([(func = _.identity)]);
```

引数の種類に応じた関数を返す。

```js
// 関数を渡せば、渡した関数を実行する関数を返す
const cl = _.iteratee(v => console.log(v));
cl('soarflat'); // => 'soarflat'

const users = [
  { user: 'barney', age: 36, active: true },
  { user: 'fred', age: 40, active: false }
];

// オブジェクトを渡すと`_.matches`を実行する関数を返す
// 以下の記述はどちらも同じ出力
_.iteratee({ user: 'barney' })({ user: 'barney', age: 36, active: true });
_.matches({ user: 'barney' })({ user: 'barney', age: 36, active: true });
// => true
// 以下の記述もどれも同じ出力
_.filter(users, _.iteratee({ user: 'barney' }));
_.filter(users, _.iteratee(v => _.matches(v))({ user: 'barney' }));
_.filter(users, _.matches({ user: 'barney' }));
// => [{ user: 'barney', age: 36, active: true }]

// 配列を渡すと`_.matchesProperty`を実行する関数を返す
// 以下の記述はどちらも同じ出力
_.iteratee(['user', 'fred'])({ user: 'fred', age: 40, active: false });
_.matchesProperty('user', 'fred')({ user: 'fred', age: 40, active: false });
// => true
// 以下の記述もどれも同じ出力
_.filter(users, _.iteratee(['user', 'fred']));
_.filter(
  users,
  _.iteratee((v, v2) => _.matchesProperty(v, v2))('user', 'fred')
);
_.filter(users, _.matchesProperty('user', 'fred'));
// => [{ user: 'fred', age: 40, active: false }]

// 上記に該当しないものを渡すと`_.property`を実行する関数を返す
// 以下の記述はどちらも同じ出力
_.iteratee('user')({ user: 'fred', age: 40, active: false });
_.property('user')({ user: 'fred', age: 40, active: false });
// => 'fred'
// 以下の記述もどれも同じ出力
_.map(users, _.iteratee('user'));
_.map(users, _.iteratee(v => _.property(v))('user'));
_.map(users, _.property('user'));
// => ['barney', 'fred']
```
