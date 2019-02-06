# Collection

- \_.countBy
- \_.every
- \_.filter
- \_.find
- \_.findLast
- \_.flatMap
- \_.flatMapDeep
- \_.flatMapDepth
- \_.forEach
- \_.forEachRight
- \_.groupBy
- \_.includes
- \_.invokeMap
- \_.keyBy
- \_.map
- \_.orderBy
- \_.partition
- \_.reduce
- \_.reduceRight
- \_.reject
- \_.sample
- \_.sampleSize
- \_.shuffle
- \_.size
- \_.some
- \_.sortBy

## \_.countBy

```js
_.countBy(collection, [(iteratee = _.identity)]);
```

繰り返し処理で返される値をキーにしたオブジェクトを生成する。

各キーに対応する値は、そのキーになる値を生成した回数。

```js
_.countBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': 1, '6': 2 }
// [6.1, 4.2, 6.3] に対して Math.floor を実行すると
// [6, 4, 6] になる。 6 が２つで 4が１つなので、最終的な出力は
// { '4': 1, '6': 2 } になる
```

```js
_.countBy([1, 2, 5, 8, 42, 12], num => (num % 2 == 0 ? 'even' : 'odd'));
// => Object {odd: 2, even: 4}
```

## \_.every

```js
_.every(collection, [(predicate = _.identity)]);
```

繰り返し処理が全て`true`を返す場合、`true`を返す。

```js
_.every([1, 2, 3, 4], n => n % 2 == 0); // => false
_.every([2, 4, 6], n => n % 2 == 0); // => true

const users = [
  { user: 'barney', age: 36, active: false },
  { user: 'fred', age: 40, active: false }
];

_.every(users, user => user.age > 35); // => true
_.every(users, user => user.age >= 40); // => false

// `_.matches`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.every(users, _.matches({ user: 'barney', active: false }));
_.every(users, { user: 'barney', active: false });
// => false

// `_.matchesProperty`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.every(users, _.matchesProperty('active', false));
_.every(users, ['active', false]);
// => true

// `_.property`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.every(users, _.property('active'));
_.every(users, 'active');
// => false
```

## \_.filter

<!-- 大体の人は理解していると思うので一旦飛ばす -->

## \_.find

```js
_.find(collection, [(predicate = _.identity)], [(fromIndex = 0)]);
```

繰り返し処理で最初に`true`を返す要素を返す。第３引数で数値を渡すと、渡した数値のインデックスから検索を開始する。

```js
_.find([1, 2, 3, 4], n => n % 2 == 1); // => 1

// 第３引数で1を渡しているため、インデックスの1から検索を開始する
_.find([1, 2, 3, 4], n => n % 2 == 1, 1); // => 3

const users = [
  { user: 'barney', age: 36, active: true },
  { user: 'fred', age: 40, active: false },
  { user: 'pebbles', age: 1, active: true }
];

_.find(users, user => user.age < 40);
// => {user: "barney", age: 36, active: true}

// `_.matches`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.find(users, _.matches({ age: 1, active: true }));
_.find(users, { age: 1, active: true });
// => {user: "pebbles", age: 1, active: true}

// `_.matchesProperty`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.find(users, _.matchesProperty('active', false));
_.find(users, ['active', false]);
// => {user: "fred", age: 40, active: false}

// `_.property`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.find(users, _.property('active'));
_.find(users, 'active');
// => {user: "barney", age: 36, active: true}
```

## \_.findLast

```js
_.findLast(
  collection,
  [(predicate = _.identity)],
  [(fromIndex = collection.length - 1)]
);
```

繰り返し処理で最後に`true`を返す要素を返す。

```js
_.findLast([1, 2, 3, 4], n => n % 2 == 1); // => 3

const users = [
  { user: 'barney', age: 36, active: true },
  { user: 'fred', age: 40, active: false },
  { user: 'pebbles', age: 1, active: true }
];

_.findLast(users, user => user.age < 40);
// => {user: "pebbles", age: 1, active: true}
```

`_.find`と同様で`_.matches`、`_.matchesProperty`、`_.property`をショートハンドでも書ける。

## \_.flatMap

```js
_.flatMap(collection, [(iteratee = _.identity)]);
```

繰り返し処理でマッピングされた結果を平坦化した配列を返す。

```js
function duplicate(n) {
  return [n, n];
}

_.flatMap([1, 2], duplicate);
// => [1, 1, 2, 2]
// 要は [[1, 1], [2, 2]] -> [1, 1, 2, 2]
```

## \_.flatMapDeep

```js
_.flatMapDeep(collection, [(iteratee = _.identity)]);
```

繰り返し処理でマッピングされた結果を再帰的に平坦化した配列を返す。

```js
function duplicate(n) {
  return [[[n, n]]];
}

_.flatMapDeep([1, 2], duplicate);
// => [1, 1, 2, 2]
// 要は [[[1, 1]], [[2, 2]]] -> [1, 1, 2, 2]
```

## \_.flatMapDepth

```js
_.flatMapDepth(collection, [(iteratee = _.identity)], [(depth = 1)]);
```

繰り返し処理でマッピングされた結果を、指定した深度（デフォルトは 1）で再帰的に平坦化した配列を返す。

```js
function duplicate(n) {
  return [[[n, n]]];
}

_.flatMapDepth([1, 2], duplicate);
// => [[[1, 1]], [[2, 2]]]
_.flatMapDepth([1, 2], duplicate, 2);
// => [[1, 1], [2, 2]]
_.flatMapDepth([1, 2], duplicate, 3);
// => [1, 1, 2, 2]
```

## \_.forEach

<!-- 大体の人は理解していると思うので一旦飛ばす -->

## \_.forEachRight

```js
_.forEachRight(collection, [(iteratee = _.identity)]);
```

コレクションの要素を右から左に繰り返し処理をする（`_.forEach`は左から右）。

```js
_.forEachRight([1, 2, 3], value => {
  console.log(value);
});
// => `3`
// => `2`
// => `1`
```

## \_.groupBy

```js
_.groupBy(collection, [(iteratee = _.identity)]);
```

繰り返し処理で返される値をキーにしたオブジェクトを生成する。

各キーに対応する値は、そのキーになる値を生成する要素をまとめた配列。

---

```js
_.groupBy([6.1, 4.2, 6.3], Math.floor);
// => { 4: [4.2], 6: [6.1, 6.3] }
// [6.1, 4.2, 6.3] に対して Math.floor を実行すると
// [6, 4, 6] になる。`6`を返す要素が`6.1`と`6.3`で
// `4`を返す要素は`4.2`のため、最終的な出力は
// { 4: [4.2], 6: [6.1, 6.3] } になる

// `_.property`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.groupBy(['one', 'two', 'three'], _.property('length'));
_.groupBy(['one', 'two', 'three'], 'length');
// => { '3': ['one', 'two'], '5': ['three'] }
```

## \_.includes

```js
_.includes(collection, value, [(fromIndex = 0)]);
```

値がコレクション内にあるかチェックする。第３引数で数値を渡すと、渡した数値のインデックスからチェックをする。

```js
_.includes([1, 2, 3], 1);

// 第３引数で1を渡しているため、インデックスの1から検索を開始する
_.includes([1, 2, 3], 1, 1); // => false

_.includes({ a: 1, b: '2' }, '2'); // => true

_.includes('abcd', 'bc'); // => true
```

## \_.invokeMap

```js
_.invokeMap(collection, path, [args]);
```

コレクション内の各要素のメソッドを呼び出し、呼び出されたメソッドの結果を配列で返す。

追加の引数は、呼び出された各メソッドに提供されます。 path が関数の場合、コレクション内の各要素に対して呼び出され、それにバインドされます。

```js
// `toUpperCase`を渡しているため、`'a'.toUpperCase()`のようにそれぞれの
// 要素（`'a', 'b', 'c'`）で`toUpperCase`が実行されている
_.invokeMap(['a', 'b', 'c'], 'toUpperCase'); // => ["A", "B", "C"]
// つまり、処理結果は以下と同じ
_.map(['a', 'b', 'c'], v => v.toUpperCase()); // => ["A", "B", "C"]

_.invokeMap([['a', 'b'], ['c', 'd']], 'join', ''); // => ['ab', 'cd']
// 処理結果は以下と同じ
_.map([['a', 'b'], ['c', 'd']], v => v.join('')); // => ["A", "B", "C"]
```

## \_.keyBy

```js
_.keyBy(collection, [(iteratee = _.identity)]);
```

繰り返し処理で返される値をキーにして、処理される要素を値にしたオブジェクトを生成する。

各キーに対応する値は、そのキーになる値を生成する際に処理される要素。

```js
const array = [{ dir: 'left', code: 97 }, { dir: 'right', code: 100 }];

_.keyBy(array, o => String.fromCharCode(o.code);
// => { 'a': { 'dir': 'left', 'code': 97 }, 'd': { 'dir': 'right', 'code': 100 } }
// `97`と`100` に対して String.fromCharCode を実行すると
// `'a'`と`'d'`になる。それがキーになり、処理される要素が値になるため、最終的な出力は
// { 'a': { 'dir': 'left', 'code': 97 }, 'd': { 'dir': 'right', 'code': 100 } } になる

// `_.property`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.keyBy(array, _.property('dir'));
_.keyBy(array, 'dir');
// => { 'left': { 'dir': 'left', 'code': 97 }, 'right': { 'dir': 'right', 'code': 100 } }
```

## \_.map

<!-- 大体の人は理解していると思うので一旦飛ばす -->

## \_.orderBy

```js
_.orderBy(collection, [(iteratees = [_.identity])], [orders]);
```

コレクションの要素を指定したソート順でソートする。

降順の場合は`'desc'`、昇順の場合は`'asc'`を指定する。指定がない場合は全て昇順でソートされる。

```js
const users = [
  { user: 'fred', age: 48 },
  { user: 'barney', age: 34 },
  { user: 'fred', age: 40 },
  { user: 'barney', age: 36 }
];

// `user`を昇順、`age`を降順でソートする
_.orderBy(users, ['user', 'age'], ['asc', 'desc']);
// => [{ user: "fred", age: 48 }, { user: "fred", age: 40 }, { user: "barney", age: 36 }, { user: "barney", age: 34 }]
```

## \_.partition

```js
_.partition(collection, [(predicate = _.identity)]);
```

繰り返し処理で`true`を返す要素をまとめた配列と、`false`を返す要素でまとめた配列を返す。

```js
var users = [
  { user: 'barney', age: 36, active: false },
  { user: 'fred', age: 40, active: true },
  { user: 'pebbles', age: 1, active: false }
];

_.partition(users, o => o.active);
// =>
// [
//   [{ user: 'fred', age: 40, active: true }],
//   [{ user: 'barney', age: 36, active: false }, { user: 'pebbles', age: 1, active: false }]
// ];

// `_.matches`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.partition(users, _.matches({ age: 1, active: false }));
_.partition(users, { age: 1, active: false });
// =>
// [
//   [{ user: 'pebbles', age: 1, active: false }],
//   [{ user: 'barney', age: 36, active: false }, { user: 'fred', age: 40, active: true }]
// ];

// `_.matchesProperty`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.partition(users, _.matchesProperty('active', false));
_.partition(users, ['active', false]);
// =>
// [
//   [{ user: 'barney', age: 36, active: false }, { user: 'pebbles', age: 1, active: false }],
//   [{ user: 'fred', age: 40, active: true }]
// ];

// `_.property`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.partition(users, _.property('active'));
_.partition(users, 'active');
// =>
// [
//   [{ user: 'fred', age: 40, active: true }],
//   [{ user: 'barney', age: 36, active: false }, { user: 'pebbles', age: 1, active: false }]
// ];
```

## \_.reduce

<!-- 大体の人は理解していると思うので一旦飛ばす -->

## \_.reduceRight

```js
_.reduceRight(collection, [(iteratee = _.identity)], [accumulator]);
```

機能は`_.reduce`と同じだが、要素を右から反復処理をする。

```js
const array = [[0, 1], [2, 3], [4, 5]];

_.reduceRight(array, (acc, v) => acc.concat(v), []);
// => [4, 5, 2, 3, 0, 1]
```

## \_.reject

```js
_.reject(collection, [(predicate = _.identity)]);
```

`false`を返す要素をまとめた配列を返す。`_.filter`の逆。

```js
const users = [
  { user: 'barney', age: 36, active: false },
  { user: 'fred', age: 40, active: true }
];

_.reject(users, user => user.active);
// => [{ user: 'barney', age: 36, active: false }]
```

## \_.sample

```js
_.sample(collection);
```

コレクションからランダムな要素を取得する。

```js
_.sample([1, 2, 3, 4]);
// => 1、2、3、4のいずれかを返す
```
