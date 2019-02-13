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

引数の数値の長さで要素を分割した配列を生成する。

```js
_.chunk(['a', 'b', 'c', 'd'], 2);
// => [['a', 'b'], ['c', 'd']]

_.chunk(['a', 'b', 'c', 'd', 'e'], 2);
// => [['a', 'b'], ['c', 'd'], ['e']]
```

## compact

```js
_.compact(array);
```

引数の配列の要素から`false`、`null`、`0`、`""`、`undefined`、`NaN`を削除した配列を生成する。

```js
_.compact([0, 1, false, 2, '', 3]);
// => [1, 2, 3]
```

## concat

```js
_.concat(array, [values]);
```

引数の値を連結した配列を生成する。

```js
const array = [1];
_.concat(array, 2, [3], [[4]], { name: 'soarflat' });
// => [1, 2, 3, [4], {name: "soarflat"}]
```

## difference

```js
_.difference(array, [values]);
```

第一引数の配列から、第二引数以降の配列に含まれない値を抜き出した配列を生成する。

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

第一引数の配列と、第二引数以降の配列の値に対して反復処理を実行し、結果が等価にならない値（その結果を計算するために利用した値）を抜き出した配列を生成する。

```js
_.differenceBy([2.1, 1.2], [2.3, 3.4], Math.floor);
// [2.1, 1.2], [2.3, 3.4] に Math.floor を実行すると
// [2, 1], [2, 3] になる。結果が等価にならないのは`1`であり
// この`1`を計算するために Math.floor に渡していたのは`1.2`のため、最終的な出力は
// => [1.2]

// `_.property`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.differenceBy([{ x: 2 }, { x: 1 }], [{ x: 1 }], _.property('x'));
_.differenceBy([{ x: 2 }, { x: 1 }], [{ x: 1 }], 'x');
// => [{ 'x': 2 }]
```

## differenceWith

## drop

```js
_.drop(array, [(n = 1)]);
```

配列の先頭から指定した数の要素を削除した配列を生成する。

```js
// デフォルトは1なので、最初の要素だけ削除される
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

配列の末尾から指定した数の要素を削除した配列を生成する。

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

配列の末尾の要素から反復処理を実行し、`false`を返すまでの要素を削除した配列を生成する。

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

// `_.matches`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。.
_.dropRightWhile(users, _.matches({ user: 'pebbles', active: false }));
_.dropRightWhile(users, { user: 'pebbles', active: false });
// => [{ user: 'fred', active: false }, {user: "barney", active: true}]

// `_.matchesProperty`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。.
_.dropRightWhile(users, _.matchesProperty('active', false));
_.dropRightWhile(users, ['active', false]);
// => [{user: "barney", active: true}]

// `_.property`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。.
_.dropRightWhile(users, _.property('active'));
_.dropRightWhile(users, 'active');
// => [{user: "barney", active: true}, { user: 'fred', active: false }, { user: 'pebbles', active: false }]
```

## dropWhile

```js
_.dropWhile(array, [(predicate = _.identity)]);
```

配列の先頭の要素から反復処理を実行し、`false`を返すまでの要素を削除した配列を生成する。

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

// `_.matches`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。.
_.dropWhile(users, _.matches({ user: 'barney', active: false }));
_.dropWhile(users, { user: 'barney', active: false });
// => [{ user: 'fred', active: false }, { user: 'pebbles', active: false }]

// `_.matchesProperty`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。.
_.dropWhile(users, _.matchesProperty('active', false));
_.dropWhile(users, ['active', false]);
// => [{ user: 'pebbles', active: true }]

// `_.property`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。.
_.dropWhile(users, _.property('active'));
_.dropWhile(users, 'active');
// => [{ user: 'barney', active: false }, { user: 'fred', active: false }, { user: 'pebbles', active: true }]
```

## fill

```js
_.fill(array, value, [(start = 0)], [(end = array.length)]);
```

配列の要素を指定した値で埋める（置き換える）。

第二引数で値を埋める開始位置を、第三引数で終了位置を指定する（終了位置は値が埋められない）。

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

反復処理で最初に`true`を返す要素のインデックスを返す。

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

要素を右から左に反復処理し、最初に`true`を返す要素のインデックスを返す。

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

配列を深さレベル１で平坦化した配列を生成する。

```js
_.flatten([1, [2, [3, [4]], 5]]);
// => [1, 2, [3, [4]], 5]
```

## flattenDeep

```js
_.flattenDeep(array);
```

配列を再帰的に平坦化した配列を生成する。

```js
_.flattenDeep([1, [2, [3, [4]], 5]]);
// => [1, 2, 3, 4, 5]
```

## flattenDepth

```js
_.flattenDepth(array, [(depth = 1)]);
```

配列を指定した深さレベルで平坦化した配列を生成する。

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

配列の要素をキーと値にしたオブジェクトを生成する。

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

配列の最初の要素を取得する。

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

引数の値と等価になる要素のインデックスを返す。

第三引数で検索を開始するインデックスを指定できる。

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

配列の最後の要素を取り除いた配列を生成する。

```js
_.initial([1, 2, 3]);
// => [1, 2]
```

## intersection

```js
_.intersection([arrays]);
```

全ての配列に含まれる値が格納された配列を生成する。

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

全ての配列に対して反復処理を実行し、その結果が全ての配列に含まれる場合、結果を計算するために利用した要素を格納した配列を生成する。

結果は同じだが、利用する値が配列によって異なる場合、格納される値は最初の配列の値になる。

```js
_.intersectionBy([2.1, 1.2], [2.3, 3.4], Math.floor);
// [2.1, 1.2], [2.3, 3.4] に Math.floor を実行すると
// [2, 1], [2, 3] になる。全ての配列に含まれる結果は`2`であり、
// この`2`を計算するために Math.floor に渡していた要素は`2.1`と`2.3`である。
// そして、最初の配列の要素は`2.1`のため、最終的な出力は
// => [2.1]

// `_.property`をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
_.intersectionBy([{ x: 1 }], [{ x: 2 }, { x: 1 }], _.property('x'));
_.intersectionBy([{ x: 1 }], [{ x: 2 }, { x: 1 }], 'x');
// => [{ 'x': 1 }]
```

## intersectionWith

## join

## last

## lastIndexOf

## nth

## pull

## pullAll

## pullAllBy

## pullAllWith

## pullAt

## remove

## reverse

## slice

## sortedIndex

## sortedIndexBy

## sortedIndexOf

## sortedLastIndex

## sortedLastIndexBy

## sortedLastIndexOf

## sortedUniq

## sortedUniqBy

## tail

## take

## takeRight

## takeRightWhile

## takeWhile

## union

## unionBy

## unionWith

## uniq

## uniqBy

## uniqWith

## unzip

## unzipWith

## without

## xor

## xorBy

## xorWith

## zip

## zipObject

## zipObjectDeep

## zipWith
