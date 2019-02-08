# Collection

- [Collection](#collection)
  - [\_.countBy](#countby)
  - [\_.every](#every)
  - [\_.filter](#filter)
  - [\_.find](#find)
  - [\_.findLast](#findlast)
  - [\_.flatMap](#flatmap)
  - [\_.flatMapDeep](#flatmapdeep)
  - [\_.flatMapDepth](#flatmapdepth)
  - [\_.forEach](#foreach)
  - [\_.forEachRight](#foreachright)
  - [\_.groupBy](#groupby)
  - [\_.includes](#includes)
  - [\_.invokeMap](#invokemap)
  - [\_.keyBy](#keyby)
  - [\_.map](#map)
  - [\_.orderBy](#orderby)
  - [\_.partition](#partition)
  - [\_.reduce](#reduce)
  - [\_.reduceRight](#reduceright)
  - [\_.reject](#reject)
  - [\_.sample](#sample)
  - [\_.sampleSize](#samplesize)
  - [\_.shuffle](#shuffle)
  - [\_.size](#size)
  - [\_.some](#some)
  - [\_.sortBy](#sortby)

## \_.countBy

```js
_.countBy(collection, [(iteratee = _.identity)]);
```

反復処理で返される値をキーにしたオブジェクトを返す。

各キーに対応する値は、そのキーになる値を生成した回数。

```js
_.countBy([6.1, 4.2, 6.3], Math.floor);
// [6.1, 4.2, 6.3] に対して Math.floor を実行すると
// [6, 4, 6] になる。`6`が２つで `4`が１つなので、最終的な出力は
// => { '4': 1, '6': 2 }

_.countBy([1, 2, 5, 8, 42, 12], num => (num % 2 == 0 ? 'even' : 'odd'));
// => Object {odd: 2, even: 4}
```

## \_.every

```js
_.every(collection, [(predicate = _.identity)]);
```

反復処理が全て`true`を返す場合、`true`を返す。

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

```js
_.filter(collection, [(predicate = _.identity)]);
```

反復処理で`true`を返す要素をまとめた配列を返す。

```js
_.filter([1, 2, 3, 4, 5], num => num % 2 === 0);
// => [2, 4]

var users = [
  { user: 'barney', age: 36, active: true },
  { user: 'fred', age: 40, active: false }
];

_.filter(users, user => user.active);
// => [{user: "barney", age: 36, active: true}]

// `_.matches`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.filter(users, _.matches({ age: 36, active: true }));
_.filter(users, { age: 36, active: true });
// => [{user: "barney", age: 36, active: true}]

// `_.matchesProperty`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.filter(users, _.matchesProperty('active', false));
_.filter(users, ['active', false]);
// => objects for ['fred']

// `_.property`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.filter(users, 'active');
// => objects for ['barney']
```

## \_.find

```js
_.find(collection, [(predicate = _.identity)], [(fromIndex = 0)]);
```

反復処理で最初に`true`を返す要素を返す。

第３引数で数値を渡すと、渡した数値のインデックスから検索を開始する。

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

右から左の反復処理で最初に`true`を返す要素を返す。

第３引数で数値を渡すと、渡した数値のインデックスから検索を開始する。

```js
_.findLast([1, 2, 3, 4], n => n % 2 == 1); // => 3

// 第３引数で1を渡しているため、インデックスの1から検索を開始する。
// 右から左に反復処理されるため、[2, 1]の順番でチェックされる。
_.findLast([1, 2, 3, 4], n => n % 2 == 1, 1); // => 1

const users = [
  { user: 'barney', age: 36, active: true },
  { user: 'fred', age: 40, active: false },
  { user: 'pebbles', age: 1, active: true }
];

_.findLast(users, user => user.age < 40);
// => {user: "pebbles", age: 1, active: true}

// `_.matches`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.findLast(users, _.matches({ age: 1, active: true }));
_.findLast(users, { age: 1, active: true });
// => {user: "pebbles", age: 1, active: true}

// `_.matchesProperty`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.findLast(users, _.matchesProperty('active', false));
_.findLast(users, ['active', false]);
// => {user: "fred", age: 40, active: false}

// `_.property`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.findLast(users, _.property('active'));
_.findLast(users, 'active');
// => {user: "pebbles", age: 1, active: true}
```

## \_.flatMap

```js
_.flatMap(collection, [(iteratee = _.identity)]);
```

反復処理でマッピングされた結果（配列）を平坦化した配列を返す。

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

反復処理でマッピングされた結果（配列）を再帰的に平坦化した配列を返す。

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

反復処理でマッピングされた結果（配列）を、指定した深度（デフォルトは 1）で再帰的に平坦化した配列を返す。

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

```js
_.forEach(collection, [(iteratee = _.identity)]);
```

コレクションの要素を反復処理する。

```js
_.forEach([1, 2], value => {
  console.log(value);
});
// => `1`
// => `2`

_.forEach({ a: 1, b: 2 }, (value, key) => {
  console.log(value);
  console.log(key);
});
// => 1
// => a
// => 2
// => b
```

## \_.forEachRight

```js
_.forEachRight(collection, [(iteratee = _.identity)]);
```

コレクションの要素を右から左に反復処理する。

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

反復処理で返される値をキーにしたオブジェクトを返す。

各キーに対応する値は、そのキーになる値を生成する要素をまとめた配列。

```js
_.groupBy([6.1, 4.2, 6.3], Math.floor);
// [6.1, 4.2, 6.3] に対して Math.floor を実行すると
// [6, 4, 6] になる。`6`を返す要素が`6.1`と`6.3`で
// `4`を返す要素は`4.2`のため、最終的な出力は
// => { 4: [4.2], 6: [6.1, 6.3] }

// `_.property`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.groupBy(['one', 'two', 'three'], _.property('length'));
_.groupBy(['one', 'two', 'three'], 'length');
// => { '3': ['one', 'two'], '5': ['three'] }
```

## \_.includes

```js
_.includes(collection, value, [(fromIndex = 0)]);
```

値がコレクション内に存在すれば`true`を返す。

第３引数で数値を渡すと、渡した数値のインデックスからチェックを開始する。

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

追加の引数は、呼び出された各メソッド渡される。

```js
// `toUpperCase`を渡しているため、`'a'.toUpperCase()`のようにそれぞれの
// 要素（`'a', 'b', 'c'`）で`toUpperCase`が実行されている
_.invokeMap(['a', 'b', 'c'], 'toUpperCase'); // => ["A", "B", "C"]
// 処理結果は以下と同じ
_.map(['a', 'b', 'c'], v => v.toUpperCase()); // => ["A", "B", "C"]

_.invokeMap([['a', 'b'], ['c', 'd']], 'join', ''); // => ['ab', 'cd']
// 処理結果は以下と同じ
_.map([['a', 'b'], ['c', 'd']], v => v.join('')); // => ["A", "B", "C"]
```

## \_.keyBy

```js
_.keyBy(collection, [(iteratee = _.identity)]);
```

反復処理で返される値をキーにして、処理される要素を値にしたオブジェクトを返す。

各キーに対応する値は、そのキーになる値を生成する際に処理される要素。

```js
const array = [{ dir: 'left', code: 97 }, { dir: 'right', code: 100 }];

_.keyBy(array, o => String.fromCharCode(o.code);
// `97`と`100` に対して String.fromCharCode を実行すると
// `'a'`と`'d'`になる。それがキーになり、処理される要素が値になるため、最終的な出力は
// => { 'a': { 'dir': 'left', 'code': 97 }, 'd': { 'dir': 'right', 'code': 100 } }

// `_.property`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.keyBy(array, _.property('dir'));
_.keyBy(array, 'dir');
// => { 'left': { 'dir': 'left', 'code': 97 }, 'right': { 'dir': 'right', 'code': 100 } }
```

## \_.map

```js
_.map(collection, [(iteratee = _.identity)]);
```

反復処理の実行結果をまとめた配列を返す。

```js
function square(n) {
  return n * n;
}

_.map([4, 8], square);
// => [16, 64]

_.map({ a: 4, b: 8 }, square);
// => [16, 64]

const users = [{ user: 'barney' }, { user: 'fred' }];

// `_.property`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.map(users, _.property('user'));
_.map(users, 'user');
// => ['barney', 'fred']
```

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

反復処理で`true`を返す要素をまとめた配列と、`false`を返す要素でまとめた配列を返す。

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

```js
_.reduce(collection, [(iteratee = _.identity)], [accumulator]);
```

反復処理の結果を累積した値を返す。

反復処理が呼び出されるごとに、前の呼び出しの戻り値が渡される。

```js
_.reduce([1, 2, 3], (sum, num) => sum + num, 0);
// `sum + num`の戻り値が累積される。
// `sum`に累積された値が渡される。第3引数で初期値を指定するので、`sum`の初期値は`0`になる。
// 今回の処理の場合、以下のように値を加算して累積する。
// 1回目の反復処理では`sum`が`0`で`num`が`1`なので、`0 + 1`の戻り値である`1`を累積して次の反復処理へ
// 2回目の反復処理では`sum`が`1`で`num`が`2`なので、`1 + 2`の戻り値である`3`を累積して次の反復処理へ
// 3回目の反復処理では`sum`が`3`で`num`が`3`なので、`3 + 3`の戻り値である`6`を累積して値を返す。そのため、最終的な出力は
// =>  6

_.reduce(
  { a: 1, b: 2, c: 1 },
  (result, value, key) => {
    const obj = {};
    obj[key] = value * 2;
    return { ...result, ...obj };
  },
  {}
);
// => {a: 2, b: 4, c: 2}

_.reduce(['a', 'b', 'c'], (result, str) => result + str, '');
// => 'abc'
```

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
_.reject([1, 2, 3, 4, 5], num => num % 2 === 0);
// => [1, 3, 5]

const users = [
  { user: 'barney', age: 36, active: false },
  { user: 'fred', age: 40, active: true }
];

_.reject(users, user => user.active);
// => [{ user: 'barney', age: 36, active: false }]

// `_.matches`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.reject(users, _.matches({ age: 40, active: true }));
_.reject(users, { age: 40, active: true });
// => [{user: "barney", age: 36, active: false}]

// `_.matchesProperty`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.reject(users, _.matchesProperty('active', false));
_.reject(users, ['active', false]);
// => [{ user: 'fred', age: 40, active: true }]

// `_.property`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.reject(users, 'active');
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

## \_.sampleSize

```js
_.sampleSize(collection, [(n = 1)]);
```

コレクションからランダムな要素を指定した個数取得する。

```js
_.sampleSize([1, 2, 3], 2);
// => [3, 1]

// 要素数より大きな数を指定すると、全部の要素を取得する
_.sampleSize([1, 2, 3], 4);
// => [2, 3, 1]
```

## \_.shuffle

```js
_.sampleSize(collection, [(n = 1)]);
```

要素をシャッフルした配列を返す。

```js
_.shuffle([1, 2, 3, 4]);
// => [4, 1, 3, 2] などの要素がシャッフルされた配列
```

## \_.size

```js
_.size(collection);
```

コレクションの長さを返す。

- 配列: 配列の長さ
- オブジェクト: 文字列型のキープロパティの数
- 文字列: 文字列の長さ

```js
_.size([1, 2, 3]);
// => 3

_.size({ a: 1, b: 2 });
// => 2

_.size('pebbles');
// => 7
```

## \_.some

```js
_.some(collection, [(predicate = _.identity)]);
```

反復処理のいずれかが`true`を返す場合、`true`を返す。

```js
const users = [
  { user: 'barney', active: true },
  { user: 'fred', active: false }
];

// `_.matches`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.some(users, _.matches({ user: 'barney', active: false }));
_.some(users, { user: 'barney', active: false });
// => false

// `_.matchesProperty`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.some(users, _.matchesProperty('active', false));
_.some(users, ['active', false]);
// => true

// `_.property`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.some(users, _.property('active'));
_.some(users, 'active');
// => true
```

## \_.sortBy

```js
_.sortBy(collection, [(iteratees = [_.identity])]);
```

要素を反復処理の結果で昇順にソートした配列を返す。

```js
_.sortBy([2, 9, 5], num => 10 - num);
// それぞれの処理の結果は[8, 1, 5]になる。
// この結果を昇順にソートすると[1, 5, 8]
// そして、この結果を返す要素を返すため、最終的な出力は
// => [9, 5, 2]

const users = [
  { name: 'fred', age: 48 },
  { name: 'barney', age: 50 },
  { name: 'fred', age: 40 },
  { name: 'barney', age: 34 }
];

_.sortBy(users, user => user.name);
// =>
// [
//   { name: 'barney', age: 50 },
//   { name: 'barney', age: 34 },
//   { name: 'fred', age: 48 },
//   { name: 'fred', age: 40 }
// ];

_.sortBy(users, user => user.age);
// =>
// [
//   { name: 'barney', age: 34 },
//   { name: 'fred', age: 40 },
//   { name: 'fred', age: 48 },
//   { name: 'barney', age: 50 }
// ];

_.sortBy(users, ['name', 'age']);
// =>
// [
//   { name: 'barney', age: 34 },
//   { name: 'barney', age: 50 },
//   { name: 'fred', age: 40 },
//   { name: 'fred', age: 48 }
// ];
```
