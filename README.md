# Lodash Tutorial

雰囲気で利用している Lodash の理解を深める。

## Lodash とは？

> A modern JavaScript utility library delivering modularity, performance & extras.

様々なユーティリティー（汎用的で便利）関数を提供しているライブラリ。

### なぜ Lodash を利用するのか

配列、数値、オブジェクト、文字列などの操作が簡潔に書けるから。

そのため、自前でデータの変換や整形をする複雑なロジックを書いている場合、Lodash の利用を検討した方が良い。

大抵は Lodash を利用した方が簡潔に書ける。

### Ramda と比べてどうなのか

Lodash と似たような機能を提供する[Ramda](https://ramdajs.com/) というライブラリが存在する。

こちらは、より関数型プログラミングでコードを書けるライブラリのため、関数型プログラミングの考え方を知らないと有効に利用するのは難しい。

そのため、「関数型プログラミングでコードを書きたい」などの理由がなければ Lodash を使っておけばいいと思う。

## リファレンス

- Array
- [Collection](./docs/collection/)
- Data
- Function
- Lang
- Math
- Number
- Object
- Seq
- String
- Util
- Properties
- Methods

### リファレンスの読み方

リファレンスのそれぞれのメソッド（API）には以下のような式が記載されている。

```js
_.initial(array);
```

これは、`_.initial`の引数には`array`を渡して利用することを示している。

`array`は配列のことであり、実際には`_.initial([1, 2, 3]);`のように利用できる。

リファレンスには`array`のような配列以外にも様々な引数が存在するため、それぞれの引数が何を示しているのかを記載していく。

#### `collection`

配列かオブジェクト。

**リファレンス表記**

```js
_.shuffle(collection);
```

**実際の利用例**

```js
_.shuffle([1, 2, 3]);
_.shuffle({ a: 1, b: 2, c: 3 });
```

#### `array`

配列。

**リファレンス表記**

```js
_.initial(array);
```

**実際の利用例**

```js
_.initial([1, 2, 3]);
```

#### `[arrays]`

複数の配列。

**リファレンス表記**

```js
_.intersection([arrays]);
```

**実際の利用例**

```js
_.intersection([2, 1], [2, 3]);
```

#### `[iteratee = _.identity]`

反復処理で実行される関数。

**リファレンス表記**

```js
_.map(collection, [iteratee = _.identity]);
```

**実際の利用例**

```js
_.map([4, 8], val => val * val);
```

`iteratee`の引数に何が渡されるのかはメソッドによりけり。

#### `[predicate=_.identity]`

反復処理で実行される述語関数（真偽値を返す関数）。

**リファレンス表記**

```js
_.filter(collection, [predicate = _.identity]);
```

**実際の利用例**

```js
_.filter([1, 2, 3], val => val % 2 === 0);
```

`predicate`の引数に何が渡されるのかはメソッドによりけり。
