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
  - [first -> head](#first---head)
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

// `_.property``をショートハンドで書ける。そのため、以下のコードの処理はどちらも同じ。
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

## fill

## findIndex

## findLastIndex

## first -> head

## flatten

## flattenDeep

## flattenDepth

## fromPairs

## head

## indexOf

## initial

## intersection

## intersectionBy

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
