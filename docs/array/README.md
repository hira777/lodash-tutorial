# Array

- [Array](#array)

  - [chunk](#chunk)
  - [compact](#compact)
  - [concat](#concat)
  - [difference](#difference)
  - [differenceBy](#differenceby)
  - [differenceWith](#differencewith)
  - [drop](#drop)
  - [dropRight](#dropright)
  - [dropRightWhile](#droprightwhile)
  - [dropWhile](#dropwhile)
  - [fill](#fill)
  - [findIndex](#findindex)
  - [findLastIndex](#findlastindex)
  - [flatten](#flatten)
  - [flattenDeep](#flattendeep)
  - [flattenDepth](#flattendepth)
  - [fromPairs](#frompairs)
  - [head](#head)
  - [indexOf](#indexof)
  - [initial](#initial)
  - [intersection](#intersection)
  - [intersectionBy](#intersectionby)
  - [intersectionWith](#intersectionwith)
  - [join](#join)
  - [last](#last)
  - [lastIndexOf](#lastindexof)
  - [nth](#nth)
  - [pull](#pull)
  - [pullAll](#pullall)
  - [pullAllBy](#pullallby)
  - [pullAllWith](#pullallwith)
  - [pullAt](#pullat)
  - [remove](#remove)
  - [reverse](#reverse)
  - [slice](#slice)
  - [sortedIndex](#sortedindex)
  - [sortedIndexBy](#sortedindexby)
  - [sortedIndexOf](#sortedindexof)
  - [sortedLastIndex](#sortedlastindex)
  - [sortedLastIndexBy](#sortedlastindexby)
  - [sortedLastIndexOf](#sortedlastindexof)
  - [sortedUniq](#sorteduniq)
  - [sortedUniqBy](#sorteduniqby)
  - [tail](#tail)
  - [take](#take)
  - [takeRight](#takeright)
  - [takeRightWhile](#takerightwhile)
  - [takeWhile](#takewhile)
  - [union](#union)
  - [unionBy](#unionby)
  - [unionWith](#unionwith)
  - [uniq](#uniq)
  - [uniqBy](#uniqby)
  - [uniqWith](#uniqwith)
  - [unzip](#unzip)
  - [unzipWith](#unzipwith)
  - [without](#without)
  - [xor](#xor)
  - [xorBy](#xorby)
  - [xorWith](#xorwith)
  - [zip](#zip)
  - [zipObject](#zipobject)
  - [zipObjectDeep](#zipobjectdeep)
  - [zipWith](#zipwith)

## chunk

```js
_.chunk(array, [(size = 1)]);
```

`array`の要素を、`size`の長さ（デフォルトは`1`）で分割した配列を返す。

```js
_.chunk(['a', 'b', 'c', 'd']);
// => [['a'], ['b'], ['c'], ['d']]

_.chunk(['a', 'b', 'c', 'd'], 2);
// => [['a', 'b'], ['c', 'd']]

_.chunk(['a', 'b', 'c', 'd', 'e'], 2);
// => [['a', 'b'], ['c', 'd'], ['e']]
```

## compact

```js
_.compact(array);
```

`array`の要素から`false`、`null`、`0`、`""`、`undefined`、`NaN`を取り除いた配列を返す。

```js
_.compact([0, 1, false, 2, '', 3]);
// => [1, 2, 3]
```

## concat

```js
_.concat(array, [values]);
```

`array`に第`values`を連結した配列を返す。

```js
const array = [1];
_.concat(array, 2, [3], [[4]], { name: 'soarflat' });
// => [1, 2, 3, [4], {name: "soarflat"}]
```

## difference

```js
_.difference(array, [values]);
```

`array`の配列から、`values`に含まれない値を格納した配列を返す。

```js
_.difference([2, 1], [2, 3]);
// => [1]

_.difference([2, 1], [1, 2]);
// => []

_.difference([2, 1, 3, 4, 5], [2, 3], [5, 1]);
// => [4]
```

## differenceBy

```js
_.differenceBy(array, [values], [(iteratee = _.identity)]);
```

以下の処理で新たな配列を返す。

1. 第１引数の配列と、第２引数以降の配列に対して反復処理を実行する。
2. 第１引数の反復処理の戻り値が格納された配列と第２引数以降の反復処理の戻り値が格納された配列を比較する。
3. 第１引数の反復処理の戻り値が格納された配列に、第２引数以降の反復処理の戻り値が格納された配列に含まれない値があった場合、その値を返した反復処理の引数に渡されていた要素を格納した配列を返す。

言葉の説明だと非常にわかり辛いため、サンプルコードを見た方が理解しやすい。

```js
_.differenceBy([2.1, 1.2], [2.3, 3.4], [4.3], Math.floor);
// [2.1, 1.2], [2.3, 3.4], [4.3] に Math.floor を実行すると
// [2, 1], [2, 3], [4] になる。
// 第１引数の反復処理の結果である [2, 1] に
// 第２引数以降の反復処理の結果である [2.3, 3.4], [4.3] に含まれない値は`1`であり
// この`1`を計算するために Math.floor に渡していたのは`1.2`のため、最終的な出力は
// => [1.2]

// `_.property`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.differenceBy([{ x: 2 }, { x: 1 }], [{ x: 1 }], _.property('x'));
_.differenceBy([{ x: 2 }, { x: 1 }], [{ x: 1 }], 'x');
// => [{ 'x': 2 }]
```

## differenceWith

```js
_.differenceWith(array, [values], [comparator]);
```

`array`と`values`の要素を`comparator`で比較し、一致しない（`false`を返す）要素を格納した配列を返す。

言葉の説明だと非常にわかり辛いため、サンプルコードを見た方が理解しやすい。

```js
// comparator の第１引数の引数には、第１引数の配列の要素が渡され
// comparator の第２引数の引数には、第２引数以降の配列の要素が渡されるため、以下の処理が実行される
// 第２引数の配列の要素と比較
// _.isEqual({ x: 1, y: 2 }, { x: 1, y: 2 })
// => true なのでこの要素（{ x: 1, y: 2 }）は戻り値には格納されない
//
// 第２引数の配列の要素と比較
// _.isEqual({ x: 2, y: 1 }, { x: 1, y: 2 })
// => false
//
// 第３引数の配列の要素と比較
// _.isEqual({ x: 2, y: 1 }, { x: 2, y: 2 })
// => false 第２引数と第３引数の配列の要素と比較してどちらも false だったので
// { x: 2, y: 1 } は戻り値に格納される
//
// 第２引数の配列の要素と比較
// _.isEqual({ x: 2, y: 2 }, { x: 1, y: 2 }) => false
//
// 第３引数の配列の要素と比較
// _.isEqual({ x: 2, y: 2 }, { x: 2, y: 2 })
// => true なのでこの要素（{ x: 2, y: 2 }）は戻り値には格納されない
_.differenceWith(
  [{ x: 1, y: 2 }, { x: 2, y: 1 }, { x: 2, y: 2 }],
  [{ x: 1, y: 2 }],
  [{ x: 2, y: 2 }],
  _.isEqual
);
// => [{ x: 2, y: 1 }]
```

## drop

```js
_.drop(array, [(n = 1)]);
```

第１引数の配列の先頭から、第２引数で指定した長さ（デフォルトは`1`）の要素を削除した配列を返す。

```js
_.drop([1, 2, 3]);
// => [2, 3]

_.drop([1, 2, 3], 2);
// => [3]

_.drop([1, 2, 3], 5);
// => []

_.drop([1, 2, 3], 0);
// => [1, 2, 3]
```

## dropRight

```js
_.dropRight(array, [(n = 1)]);
```

第１引数の配列の末尾から、第２引数で指定した長さ（デフォルトは`1`）の要素を削除した配列を返す。

```js
_.dropRight([1, 2, 3]);
// => [1, 2]

_.dropRight([1, 2, 3], 2);
// => [1]

_.dropRight([1, 2, 3], 5);
// => []

_.dropRight([1, 2, 3], 0);
// => [1, 2, 3]
```

## dropRightWhile

```js
_.dropRightWhile(array, [(predicate = _.identity)]);
```

第１引数の配列の末尾の要素から反復処理を実行し、反復処理が`false`を返すまでの要素を削除した配列を返す。

```js
_.dropRightWhile([2, 4, 5, 6, 8, 10], num => num % 2 === 0);
// => [2, 4, 5]

const users = [
  { user: 'barney', active: true },
  { user: 'fred', active: false },
  { user: 'pebbles', active: false }
];
const users2 = [
  { user: 'fred', active: false },
  { user: 'barney', active: true },
  { user: 'pebbles', active: false }
];

_.dropRightWhile(users, user => !user.active);
// => [{user: "barney", active: true}]

_.dropRightWhile(users2, user => !user.active);
// => [{ user: 'fred', active: false }, {user: "barney", active: true}]

// `_.matches`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.dropRightWhile(users, _.matches({ user: 'pebbles', active: false }));
_.dropRightWhile(users, { user: 'pebbles', active: false });
// => [{ user: 'fred', active: false }, {user: "barney", active: true}]

// `_.matchesProperty`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.dropRightWhile(users, _.matchesProperty('active', false));
_.dropRightWhile(users, ['active', false]);
// => [{user: "barney", active: true}]

// `_.property`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.dropRightWhile(users, _.property('active'));
_.dropRightWhile(users, 'active');
// => [{user: "barney", active: true}, { user: 'fred', active: false }, { user: 'pebbles', active: false }]
```

## dropWhile

```js
_.dropWhile(array, [(predicate = _.identity)]);
```

第１引数の配列の先頭の要素から反復処理を実行し、反復処理が`false`を返すまでの要素を削除した配列を返す。

```js
_.dropWhile([2, 4, 5, 6, 8, 10], num => num % 2 === 0);
// => [5, 6, 8, 10]

const users = [
  { user: 'barney', active: false },
  { user: 'fred', active: false },
  { user: 'pebbles', active: true }
];
const users2 = [
  { user: 'barney', active: false },
  { user: 'pebbles', active: true },
  { user: 'fred', active: false }
];

_.dropWhile(users, user => !user.active);
// => [{ user: 'barney', active: true }]

_.dropWhile(users2, user => !user.active);
// => [{ user: 'fred', active: false }, {user: "barney", active: true}]

// `_.matches`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.dropWhile(users, _.matches({ user: 'barney', active: false }));
_.dropWhile(users, { user: 'barney', active: false });
// => [{ user: 'fred', active: false }, { user: 'pebbles', active: false }]

// `_.matchesProperty`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.dropWhile(users, _.matchesProperty('active', false));
_.dropWhile(users, ['active', false]);
// => [{ user: 'pebbles', active: true }]

// `_.property`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.dropWhile(users, _.property('active'));
_.dropWhile(users, 'active');
// => [{ user: 'barney', active: false }, { user: 'fred', active: false }, { user: 'pebbles', active: true }]
```

## fill

```js
_.fill(array, value, [(start = 0)], [(end = array.length)]);
```

第１引数の配列の要素を第２引数の値で埋める（置き換える）。

第３引数で値を埋める開始位置を、第４引数で終了位置を指定する（終了位置は値が埋められない）。

```js
const array = [1, 2, 3];

_.fill(array, 'a');
console.log(array);
// => ['a', 'a', 'a']

_.fill(Array(3), 2);
// => [2, 2, 2]

_.fill([4, 6, 8, 10], '*', 1, 3);
// => [4, '*', '*', 10]
```

## findIndex

```js
_.findIndex(array, [(predicate = _.identity)], [(fromIndex = 0)]);
```

第１引数の配列の要素に対して反復処理を実行し、反復処理が最初に`true`を返す要素のインデックスを返す。

```js
const users = [
  { user: 'barney', active: false },
  { user: 'fred', active: false },
  { user: 'pebbles', active: true }
];

_.findIndex(users, user => user.user == 'barney');
// => 0

// `_.matches`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.findIndex(users, _.matches({ user: 'fred', active: false }));
_.findIndex(users, { user: 'fred', active: false });
// => 1

// `_.matchesProperty`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.findIndex(users, _.matchesProperty('active', false));
_.findIndex(users, ['active', false]);
// => 0

// `_.property`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.findIndex(users, _.property('active'));
_.findIndex(users, 'active');
// => 2
```

## findLastIndex

```js
_.findLastIndex(
  array,
  [(predicate = _.identity)],
  [(fromIndex = array.length - 1)]
);
```

第１引数の配列の末尾から反復処理を実行し、反復処理が最初に`true`を返す要素のインデックスを返す。

```js
const users = [
  { user: 'pebbles', active: true },
  { user: 'barney', active: false },
  { user: 'fred', active: false }
];

_.findLastIndex(users, user => user.user == 'barney');
// => 1

// `_.matches`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.findLastIndex(users, _.matches({ user: 'fred', active: false }));
_.findLastIndex(users, { user: 'fred', active: false });
// => 2

// `_.matchesProperty`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.findLastIndex(users, _.matchesProperty('active', true));
_.findLastIndex(users, ['active', true]);
// => 0

// `_.property`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.findLastIndex(users, _.property('active'));
_.findLastIndex(users, 'active');
// => 0
```

## flatten

```js
_.flatten(array);
```

引数の配列を深さレベル１で平坦化した配列を返す。

```js
_.flatten([1, [2, [3, [4]], 5]]);
// => [1, 2, [3, [4]], 5]
```

## flattenDeep

```js
_.flattenDeep(array);
```

引数の配列を再帰的に平坦化した配列を返す。

```js
_.flattenDeep([1, [2, [3, [4]], 5]]);
// => [1, 2, 3, 4, 5]
```

## flattenDepth

```js
_.flattenDepth(array, [(depth = 1)]);
```

第１引数の配列を、第２引数で指定した深さレベルで平坦化した配列を返す。

```js
const array = [1, [2, [3, [4]], 5]];

_.flattenDepth(array, 1);
// => [1, 2, [3, [4]], 5]

_.flattenDepth(array, 2);
// => [1, 2, 3, [4], 5]

_.flattenDepth(array, 3);
// => [1, 2, 3, 4, 5]
```

## fromPairs

```js
_.fromPairs(pairs);
```

引数の配列の要素をキーと値にしたオブジェクトを返す。

```js
_.fromPairs([['a', 1], ['b', 2]]);
// => { 'a': 1, 'b': 2 }

_.fromPairs([['a', 1], ['a', 2]]);
// => { 'a': 2 }

_.fromPairs([['a', 1, 'A'], ['b', 2, 'B']]);
// => { 'a': 1, 'b': 2 }
```

## head

```js
_.head(array);
```

引数の配列の最初の要素を取得する。

```js
_.head([1, 2, 3]);
// => 1

_.head([]);
// => undefined
```

## indexOf

```js
_.indexOf(array, value, [(fromIndex = 0)]);
```

第１引数の配列から、第２引数の値と等価になる要素のインデックスを返す。

第３引数で検索を開始するインデックスを指定できる。

```js
_.indexOf([1, 2, 1, 2], 2);
// => 1

// インデックスの２から検索を開始する
_.indexOf([1, 2, 1, 2], 2, 2);
// => 3
```

## initial

```js
_.initial(array);
```

引数の配列の最後の要素を取り除いた配列を返す。

```js
_.initial([1, 2, 3]);
// => [1, 2]
```

## intersection

```js
_.intersection([arrays]);
```

引数の全ての配列に含まれる値が格納された配列を返す。

```js
_.intersection([2, 1], [2, 3]);
// => [2]

_.intersection([2, 1], [1, 2, 3], [1, 3]);
// => [1]
```

## intersectionBy

```js
_.intersectionBy([arrays], [(iteratee = _.identity)]);
```

以下の処理で新たな配列を返す。

1. 全ての配列に対して反復処理を実行する。
2. それぞれの反復処理の戻り値が格納された配列を比較する。
3. 全ての配列に同じ値が含まれる場合、その値を返した反復処理に渡されていた要素を格納した配列を返す。

言葉の説明だと非常にわかり辛いため、サンプルコードを見た方が理解しやすい。

```js
_.intersectionBy([2.1, 1.2], [2.3, 3.4], Math.floor);
// [2.1, 1.2], [2.3, 3.4] に Math.floor を実行すると
// [2, 1], [2, 3] になる。結果である全ての配列に含まれる値は`2`であり、
// この`2`を計算するために Math.floor に渡していた要素は`2.1`と`2.3`である。
// 格納される値は最初の配列の要素である`2.1`のため、最終的な出力は
// => [2.1]

// `_.property`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.intersectionBy([{ x: 1 }], [{ x: 2 }, { x: 1 }], _.property('x'));
_.intersectionBy([{ x: 1 }], [{ x: 2 }, { x: 1 }], 'x');
// => [{ 'x': 1 }]
```

## intersectionWith

```js
_.intersectionWith([arrays], [comparator]);
```

第１引数の配列と、第２引数以降の配列に対して comparator を実行し、全ての配列で一致する（`true`を返す）要素を格納した配列を返す。

言葉の説明だと非常にわかり辛いため、サンプルコードを見た方が理解しやすい。

```js
// comparator の第１引数の引数には、第１引数の配列の要素が渡され
// comparator の第２引数の引数には、第２引数以降の配列の要素が渡されるため、以下の処理が実行される
// 第２引数の配列の要素と比較
// _.isEqual({ x: 1, y: 2 }, { x: 1, y: 2 })
// => true
//
// 第３引数の配列の１つ目の要素と比較
// _.isEqual({ x: 1, y: 2 }, { x: 2, y: 2 })
// => false
//
// 第３引数の配列の２つ目の要素と比較
// _.isEqual({ x: 2, y: 1 }, { x: 1, y: 2 })
// => true 第２引数と第３引数の配列の要素と比較してどちらも true だったので
// { x: 1, y: 2 } は戻り値に格納される
//
// 第２引数の配列の要素と比較
// _.isEqual({ x: 2, y: 1 }, { x: 1, y: 2 })
// => false なので { x: 2, y: 1 } は戻り値に格納されない
//
// 第２引数の配列の要素と比較
// _.isEqual({ x: 2, y: 2 }, { x: 1, y: 2 })
// => false なので { x: 2, y: 2 } は戻り値に格納されない
//
_.intersectionWith(
  [{ x: 1, y: 2 }, { x: 2, y: 1 }, { x: 2, y: 2 }],
  [{ x: 1, y: 2 }],
  [{ x: 2, y: 2 }, { x: 1, y: 2 }],
  _.isEqual
);
// => [{ x: 1, y: 2 }]
```

## join

```js
_.join(array, [(separator = ',')]);
```

配列の要素を引数で渡した文字列で区切った文字列を返す。

```js
_.join(['a', 'b', 'c'], '~');
// => 'a~b~c'

_.join(['a', 'b', 'c'], '-');
// => 'a-b-c'
```

## last

```js
_.last(array);
```

配列の最後の要素を返す。

```js
_.last([1, 2, 3]);
// => 3
```

## lastIndexOf

```js
_.lastIndexOf(array, value, [(fromIndex = array.length - 1)]);
```

引数の値と等価になる要素のインデックスを返す。`_.indexOf`とは逆で右から左に検索をする。

第三引数で検索を開始するインデックスを指定できる。

```js
_.lastIndexOf([1, 2, 1, 2], 2);
// => 2

// インデックスの２から検索を開始する
_.lastIndexOf([1, 2, 1, 2], 2, 2);
// => 1
```

## nth

```js
_.nth(array, [(n = 0)]);
```

配列から指定したインデックスの要素を取得する。

負数の場合、末尾からインデックスの要素を取得する。。

```js
const array = ['a', 'b', 'c', 'd'];

_.nth(array, 1);
// => 'b'

_.nth(array, -2);
// => 'c';
```

## pull

```js
_.pull(array, [values]);
```

配列から指定した値を削除する。

`_.without`とは異なり、新しい配列を生成するのではなく、元の配列が変更される。

```js
const array = ['a', 'b', 'c', 'a', 'b', 'c'];

_.pull(array, 'a', 'c');
console.log(array);
// => ['b', 'b']
```

## pullAll

```js
_.pullAll(array, values);
```

配列から指定した配列の値を削除する。

`_.difference`とは異なり、新しい配列を生成するのではなく、元の配列が変更される。

```js
const array = ['a', 'b', 'c', 'a', 'b', 'c'];
const values = ['a', 'c'];

_.pullAll(array, values);
console.log(array);
// => ['b', 'b']
```

## pullAllBy

```js
_.pullAllBy(array, values, [(iteratee = _.identity)]);
```

1. 第１引数の配列と第 2 引数以降の配列に対して反復処理を実行する。
2. それぞれの反復処理の戻り値が格納された配列を比較する。
3. 等価となる値があった場合、その値を返した反復処理に渡されていた要素を第１引数の配列から削除する。

`_.differenceBy`とは異なり、新しい配列を生成するのではなく、元の配列が変更される。

言葉の説明だと非常にわかり辛いため、サンプルコードを見た方がわかりやすいと思う。

```js
const array = [2.1, 1.2];
const values = [2.3, 3.4];
_.pullAllBy(array, values, Math.floor);
// [2.1, 1.2], [2.3, 3.4] に Math.floor を実行すると
// [2, 1], [2, 3] になる。結果が等価になるのは`2`であり
// この`2`を計算するために Math.floor に渡していた`2.1`が削除される。
console.log(array);
// => [1.2]

const array2 = [{ x: 1 }, { x: 2 }, { x: 3 }, { x: 1 }];
// `_.property`をショートハンド（`_.property('x')` -> `x`）で書ける。
_.pullAllBy(array2, [{ x: 1 }, { x: 3 }], 'x');
// => [{ x: 2 }]
```

## pullAllWith

```js
_.pullAllWith(array, values, [comparator]);
```

`array`と`values`の要素を`comparator`で比較し、一致しない（`false`を返す）要素を格納した配列を返す。

`_.differenceWith`と異なり、新しい配列を生成するのではなく、引数で渡した配列が変更される。

言葉の説明だと非常にわかり辛いため、サンプルコードを見た方が理解しやすい

```js
const array = [{ x: 1, y: 2 }, { x: 3, y: 4 }, { x: 5, y: 6 }];

_.pullAllWith(array, [{ x: 3, y: 4 }], _.isEqual);
console.log(array);
// => [{ 'x': 1, 'y': 2 }, { 'x': 5, 'y': 6 }]
```

## pullAt

```js
_.pullAt(array, [indexes]);
```

指定したインデックスの要素を削除した配列を返す。

`_.at`とは異なり、新しい配列を生成するのではなく、引数で渡した配列が変更される。

```js
const array = ['a', 'b', 'c', 'd'];
const pulled = _.pullAt(array, [1, 3]);

console.log(array);
// => ['a', 'c']

console.log(pulled);
// => ['b', 'd']
```

## remove

反復処理で`true`を返す要素を削除した配列を返す。

`_.filter`とは異なり、新しい配列を生成するのではなく、元の配列も変更される。

```js
const array = [1, 2, 3, 4];
const evens = _.remove(array, n => n % 2 == 0);

console.log(array);
// => [1, 3]

console.log(evens);
// => [2, 4]
```

## reverse

```js
_.reverse(array);
```

配列の要素を反転する。

新しい配列を生成するのではなく、元の配列が変更される。

```js
const array = [1, 2, 3];

_.reverse(array);
// => [3, 2, 1]

console.log(array);
// => [3, 2, 1]
```

## slice

[Array.prototype.slice()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)

## sortedIndex

```js
_.sortedIndex(array, value);
```

第２引数の値を第１引数の配列のどのインデックスに追加すれば、配列のソート順が維持されるのかを返す。

```js
_.sortedIndex([30, 50], 40);
// `[30, 50]` に `40` を追加した場合、
// `[30, 40, 50]` にすればソート順が維持されるため、最終的な出力は
// => 1
```

## sortedIndexBy

第１引数と配列の要素と第２引数の値に対して反復処理を実行し、第２引数の反復処理の結果を第１引数の反復処理の結果である配列のどのインデックスに追加すれば、配列のソート順が維持されるのかを返す。

言葉の説明だと非常にわかりづらいため、サンプルコードを見た方が理解しやすい。

```js
_.sortedIndexBy([{ x: 4 }, { x: 6 }], { x: 5 }, o => o.x);
// `[{ x: 4 }, { x: 6 }]` と `{ x: 5 }` に対して
// `o => o.x` を実行すると　`[4, 6]` `5` になる。
// `[4, 6]` に `5` を追加した場合
// `[4, 5, 6]` にすればソート順が維持されるため、最終的な出力は
// => 1
```

## sortedIndexOf

```js
_.sortedIndexOf(array, value);
```

ソートされた`array`に対して二分探索を実行し、`value`にマッチするインデックスを返す。

```js
_.sortedIndexOf([4, 5, 5, 5, 6], 5);
// => 1
```

## sortedLastIndex

```js
_.sortedLastIndex(array, value);
```

ソートされた`array`に`value`を挿入しても、ソート順が維持される最大のインデックスを返す。

```js
_.sortedLastIndex([4, 5, 5, 5, 6], 5);
// => 4
```

## sortedLastIndexBy

```js
_.sortedLastIndexBy(array, value, [(iteratee = _.identity)]);
```

ソートされた`array`の要素と`value`を引数とした`iteratee`の戻り値をソートする。

そして、戻り値がソートされた配列から、`value`を引数とした`iteratee`の戻り値が存在するインデックスを返す。

```js
const objects = [{ x: 4 }, { x: 6 }];

// `objects`の要素と`{ x: 5 }`を引数とした`o => o.x`の戻り値は
// `[4, 6, 5]`であり、これらをソートすると`[4, 5, 6]`である
// ソートされた配列内で`5`（`{ x: 5 }`を引数とした`o => o.x`の戻り値）の
// インデックスは`1`のため、最終的な出力は`1`になる
_.sortedLastIndexBy(objects, { x: 5 }, o => o.x);
// => 1
_.sortedLastIndexBy(objects, { x: 7 }, o => o.x);
// => 2

// `_.property` のショートハンドを利用できる
_.sortedLastIndexBy(objects, { x: 5 }, 'x');
// => 1
```

## sortedLastIndexOf

```js
_.sortedLastIndexOf(array, value);
```

ソートされた`array`に対して二分探索を実行し、`value`にマッチする最大のインデックスを返す。

```js
_.sortedLastIndexOf(array, value);
```

## sortedUniq

```js
_.sortedUniq(array);
```

`_.uniq`と同様で`array`から値の重複を取り除いた配列を返す（重複した値は配列内で一番順番が早いものが残り、それ以外が取り除かれる）。

`_.uniq`とは異なり、ソートされた配列用に設計、最適化されている。

```js
_.sortedUniq([1, 1, 2]);
// => [1, 2]
```

## sortedUniqBy

```js
_.sortedUniqBy(array, [iteratee]);
```

`_.uniqBy`と同様で、`array`の要素を引数とした`iteratee`の戻り値が重複する場合、`array`から戻り値が重複した`iteratee`の引数に渡している要素を取り除いた配列を返す（重複の原因となる要素は配列内で一番順番が早いものが残り、それ以外が取り除かれる）。

`_.uniqBy`とは異なり、ソートされた配列用に設計、最適化されている。

```js
_.sortedUniqBy([1.1, 1.2, 2.3, 2.4], Math.floor);
// => [1.1, 2.3]
```

## tail

```js
_.tail(array);
```

`array`の最初の要素以外の要素を格納した配列を返す。

```js
_.tail([1, 2, 3]);
// => [2, 3]
```

## take

```js
_.take(array, [(n = 1)]);
```

`array`の先頭から`n`個の要素を格納した配列を返す。デフォルトの取得数は`1`。

```js
// デフォルトの取得数は`1`なので１つの要素を取得する。
_.take([1, 2, 3]);
// => [1]

_.take([1, 2, 3], 2);
// => [1, 2]

_.take([1, 2, 3], 5);
// => [1, 2, 3]

_.take([1, 2, 3], 0);
// => []
```

## takeRight

```js
_.takeRight(array, [(n = 1)]);
```

`array`の末尾から`n`個の要素を格納した配列を返す。デフォルトの取得数は`1`。

```js
// デフォルトの取得数は`1`なので１つの要素を取得する。
_.takeRight([1, 2, 3]);
// => [3]

_.takeRight([1, 2, 3], 2);
// => [2, 3]

_.takeRight([1, 2, 3], 5);
// => [1, 2, 3]

_.takeRight([1, 2, 3], 0);
// => []
```

## takeRightWhile

```js
_.takeRightWhile(array, [(predicate = _.identity)]);
```

`array`の末尾の要素から`predicate`を実行し、`false`を返すまでの要素を格納した配列を返す。

```js
_.takeRightWhile([5, 1, 3, 2, 9, 11, 13], num => num % 2 === 1);
// => [9, 11, 13]

const users = [
  { user: 'dom', active: false },
  { user: 'barney', active: true },
  { user: 'fred', active: false },
  { user: 'pebbles', active: false }
];

_.takeRightWhile(users, user => !user.active);
// => objects for ['fred', 'pebbles']

// `_.matches`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.takeRightWhile(users, _.matches({ user: 'pebbles', active: false }));
_.takeRightWhile(users, { user: 'pebbles', active: false });
// => objects for ['pebbles']

// `_.matchesProperty`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.takeRightWhile(users, _.matchesProperty('active', false));
_.takeRightWhile(users, ['active', false]);
// => objects for ['fred', 'pebbles']

// `_.property`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.takeRightWhile(users, _.property('active'));
_.takeRightWhile(users, 'active');
// => []
```

## takeWhile

```js
_.takeWhile(array, [(predicate = _.identity)]);
```

`array`の先頭の要素から`predicate`を実行し、`false`を返すまでの要素を格納した配列を返す。

```js
_.takeWhile([5, 1, 3, 2, 9, 11, 13], num => num % 2 === 1);
// => [5, 1, 3]
```

## union

```js
_.union([arrays]);
```

複数の配列から値の重複を取り除き、結合した配列を返す。

```js
_.union([2], [1, 2]);
// => [2, 1]
```

## unionBy

```js
_.unionBy([arrays], [(iteratee = _.identity)]);
```

`arrays`の要素を引数とした`iteratee`の戻り値が重複する場合、`arrays`から「戻り値が重複した`iteratee`の引数に渡している要素」を取り除き、結合した配列を返す（重複の原因となる要素は配列内で一番順番が早いものが残り、それ以外が取り除かれる）。

言葉の説明だと非常にわかりづらいため、サンプルコードを見た方が理解しやすいと思う。

```js
// [2.1], [1, 2.3] に`Math.floor`を実行すると
// [2], [1, 2] になる。そのため、重複する値は `2` 。
// この `2` を計算した `Math.floor` に渡されていた要素（重複の原因となる要素）は
// `2.1` と `2.3` であり、`2.1` の方が配列内の順番が早いため、
// `2.3` が取り除かれる。最終的な出力は
_.unionBy([2.1], [1.2, 2.3], Math.floor);
// => [2.1, 1.2]

// `_.property`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.unionBy([{ x: 1 }], [{ x: 2 }, { x: 1 }], _.property('x'));
_.unionBy([{ x: 1 }], [{ x: 2 }, { x: 1 }], 'x');
// => [{ 'x': 1 }, { 'x': 2 }]
```

## unionWith

```js
_.unionWith([arrays], [comparator]);
```

`arrays`の要素を`comparator`で比較し、重複した要素を取り除いて結合した配列を返す（重複の原因となる要素は配列内で一番順番が早いものが残り、それ以外が取り除かれる）。

`comparator`には 2 つの引数が渡される（以下のサンプルコードを参照）。

```js
const objects = [{ x: 1, y: 2 }, { x: 2, y: 1 }];
const others = [{ x: 1, y: 1 }, { x: 1, y: 2 }];

_.unionWith(objects, others, _.isEqual);
// 今回の場合、comparator である`_.isEqual`には以下の引数が渡されて実行される。
// _.isEqual({ x: 2, y: 1 }, { x: 1, y: 2 });
// _.isEqual({ x: 1, y: 1 }, { x: 1, y: 2 });
// _.isEqual({ x: 1, y: 1 }, { x: 2, y: 1 });
// _.isEqual({ x: 1, y: 2 }, { x: 1, y: 2 });
// => [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }, { 'x': 1, 'y': 1 }]
```

## uniq

```js
_.uniq(array);
```

配列から値の重複を取り除いた配列を返す。

重複した値は、配列内で一番順番が早いものが残り、それ以外が取り除かれる。

```js
_.uniq([2, 1, 2, 4, 5, 4]);
// => [2, 1, 4, 5]
```

## uniqBy

配列から「戻り値が重複する反復処理の引数に渡している要素」を取り除いた配列を返す。

言葉の説明だと非常にわかりづらいため、サンプルコードを見た方が理解しやすいと思う。

```js
_.uniqBy([2.1, 1.2, 2.3], Math.floor);
// `[2.1, 1.2, 2.3]` に `Math.floor` を実行すると
// `[2, 1, 2]` になる。そのため、重複する値は `2` 。
// この `2` を計算した `Math.floor` に渡されていた要素（重複の原因となる要素）は
// `2.1` と `2.3` であり、`2.1` の方が配列内の順番が早いため、
// `2.3` が取り除かれる。最終的な出力は
// => [2.1, 1.2]

// `_.property`のショートハンドが利用できるため
// `_.uniqBy([{ x: 1 }, { x: 2 }, { x: 1 }], _.property('x'))`
// を以下のように書ける。
_.uniqBy([{ x: 1 }, { x: 2 }, { x: 1 }], 'x');
// => [{ 'x': 1 }, { 'x': 2 }]
```

## uniqWith

```js
_.uniqWith(array, [comparator]);
```

`array`の要素を`comparator`で比較し、重複した要素を取り除いた配列を返す。

`comparator`には 2 つの引数が渡される（以下のサンプルコードを参照）。

```js
const objects = [{ x: 1, y: 2 }, { x: 2, y: 1 }, { x: 1, y: 2 }];

_.uniqWith(objects, _.isEqual);
// 今回の場合、comparator である`_.isEqual`には以下の引数が渡されて実行される。
// _.isEqual({x: 2, y: 1} {x: 1, y: 2})
// _.isEqual({x: 1, y: 2} {x: 1, y: 2})
// => [{ x: 1, y: 2 }, { x: 2, y: 1 }]
```

## unzip

```js
_.unzip(array);
```

`_.zip`でグループ化された`array`の構成を元に戻した配列を返す。

```js
const zipped = _.zip(['a', 'b'], [1, 2], [true, false]);
// => [['a', 1, true], ['b', 2, false]]

_.unzip(zipped);
// => [['a', 'b'], [1, 2], [true, false]]

_.unzip([['Pikachu', 'ELECTRIC'], ['Eevee', 'NORMAL'], ['Chikorita', 'CRASS']]);
// => [['Pikachu', 'Eevee', 'Chikorita'],['ELECTRIC', 'NORMAL', 'CRASS']]
```

## unzipWith

```js
_.unzipWith(array, [(iteratee = _.identity)]);
```

`_.zip`でグループ化された`array`の構成を元に戻し、その配列の要素を引数とした`iteratee`の戻り値が格納された配列を返す。

言葉の説明だと非常にわかり辛いため、サンプルコードを見た方がわかりやすいと思う。

```js
const zipped = _.zip([1, 2, 3], [10, 20, 30], [100, 200, 300]);
// => [[1, 10, 100], [2, 20, 200], [3, 30, 300]]

_.unzipWith(zipped, (a, b, c) => a + b + c);
// `a`、`b`、`c`にそれぞれの配列の要素が渡されるため、以下のような計算がされる
// 1 + 2 + 3 = 6
// 10 + 20 + 30 = 60
// 100 + 200 + 300 = 600
// => [6, 60, 600]

_.unzipWith(
  [['Pikachu', 'Eevee', 'Chikorita'], ['ELECTRIC', 'NORMAL', 'CRASS']],
  (name, type) => `Name: ${name} Type: ${type}`
);
// =>
// [
//   "Name: Pikachu Type: ELECTRIC",
//   "Name: Eevee Type: NORMAL",
//   "Name: Chikorita Type: CRASS"
// ]

// 引数の渡し方が異なるが `_.zipWith` でも同じことはできる。
_.zipWith([1, 10, 100], [2, 20, 200], [3, 30, 300], (a, b, c) => a + b + c);
// => [6, 60, 600]
```

## without

```js
_.without(array, [values]);
```

`array`から`values`を除外した配列を返す。

等価性の比較には[SameValueZero](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness#A_model_for_understanding_equality_comparisons)が利用される。

```js
_.without([2, 1, 2, 3], 1, 2);
// => [3]
```

## xor

```js
_.xor([arrays]);
```

`arrays`の対称差となる値を格納した配列を返す。

```js
_.xor([2, 1], [2, 3]);
// => [1, 3]
```

## xorBy

```js
_.xorBy([arrays], [(iteratee = _.identity)]);
```

1. 全ての配列に対して反復処理を実行する。
2. それぞれの反復処理の戻り値が格納された配列を比較する。
3. 対称差となる値があった場合、その値を返した反復処理に渡されていた要素を格納した配列を返す。

言葉の説明だと非常にわかり辛いため、サンプルコードを見た方がわかりやすいと思う。

```js
_.xorBy([2.1, 1.2], [2.3, 3.4], Math.floor);
// `[2.1, 1.2]`、`[2.3, 3.4]` に `Math.floor` を実行すると
// `[2, 1]`、`[2, 3]` になる。対称差となる値は `1` と `3` であり
// この `1` と `3` を返した `Math.floor` に渡されていた要素は
// `1.2` と `3.4` のため、最終的な出力は
// => [1.2, 3.4]

// `_.property`のショートハンドが利用できるため。以下のコードの処理はどちらも同じ。
_.xorBy([{ x: 1 }], [{ x: 2 }, { x: 1 }], 'x');
_.xorBy([{ x: 1 }], [{ x: 2 }, { x: 1 }], _.property('x'));
// => [{ x: 2 }]
```

## xorWith

```js
_.xorWith([arrays], [comparator]);
```

`arrays`の要素を`comparator`で比較し、対称差となる要素を格納した配列を返す。

`comparator`には 2 つの引数が渡される（以下のサンプルコードを参照）。

```js
const objects = [{ x: 1, y: 2 }, { x: 2, y: 1 }];
const objects2 = [{ x: 1, y: 1 }, { x: 1, y: 2 }];
const objects3 = [{ x: 1, y: 1 }, { x: 2, y: 2 }];

_.xorWith(objects, objects2, objects3, _.isEqual);
// 今回の場合、comparator である`_.isEqual`には以下の引数が渡されて実行される。
// _.isEqual({x: 1, y: 2} {x: 1, y: 1})
// _.isEqual({x: 1, y: 2} {x: 1, y: 2})
// _.isEqual({x: 2, y: 1} {x: 1, y: 1})
// _.isEqual({x: 2, y: 1} {x: 1, y: 2})
// _.isEqual({x: 2, y: 1} {x: 1, y: 1})
// _.isEqual({x: 2, y: 1} {x: 2, y: 2})
// _.isEqual({x: 1, y: 1} {x: 1, y: 2})
// _.isEqual({x: 1, y: 1} {x: 2, y: 1})
// _.isEqual({x: 1, y: 2} {x: 1, y: 2})
// _.isEqual({x: 1, y: 1} {x: 1, y: 1})
// _.isEqual({x: 1, y: 1} {x: 1, y: 2})
// _.isEqual({x: 1, y: 1} {x: 2, y: 1})
// _.isEqual({x: 2, y: 2} {x: 1, y: 2})
// _.isEqual({x: 2, y: 2} {x: 2, y: 1})
// _.isEqual({x: 1, y: 1} {x: 1, y: 1})
// _.isEqual({x: 2, y: 2} {x: 1, y: 1})
// _.isEqual({x: 2, y: 2} {x: 1, y: 2})
// _.isEqual({x: 2, y: 2} {x: 2, y: 1})
// => [{ x: 2, y: 1 }, {x: 2, y: 2}]
```

## zip

```js
_.zip([arrays]);
```

`arrays`の要素がグループ化された配列を返す。

````js
_.zip(['a', 'b'], [1, 2], [true, false]);
// => [['a', 1, true], ['b', 2, false]]
```

## zipObject

```js
_.zipObject([(props = [])], [(values = [])]);
````

第１引数の配列の要素をキーにして、第２引数の配列の要素を値にしたオブジェクトを返す。

```js
_.zipObject(['a', 'b'], [1, 2]);
// => { a: 1, b: 2 }
```

## zipObjectDeep

```js
_.zipObjectDeep([(props = [])], [(values = [])]);
```

第１引数の配列の要素をキーにして、第２引数の配列の要素を値にしたオブジェクトを返す。

zipObject とは異なり、property paths をサポートしているため、`a.b[0].c`のようなネストされたキーも指定できる。

```js
_.zipObjectDeep(['a.b[0].c', 'a.b[1].d'], [1, 2]);
// => { a: { b: [{ c: 1 }, { d: 2 }] } }
```

## zipWith

```js
_.zipWith([arrays], [(iteratee = _.identity)]);
```

`arrays`のそれぞれの要素を`iteratee`の引数として渡し、その`iteratee`の戻り値が格納された配列を返す。

```js
_.zipWith([1, 2], [10, 20], [100, 200], (a, b, c) => a + b + c);
// => [111, 222]
```
