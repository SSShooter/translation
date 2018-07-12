
# 可迭代对象（Iterables）

*可迭代对象*是数组的泛化（generalization of arrays）。这个概念使对象可以在 `for..of` 循环中使用。

数组本身就是可迭代的。但不止数组，字符串以及很多内建对象都是可迭代的。

可迭代对象在 JavaScript 实现中广泛使用，很多操作和内建方法都依赖于可迭代对象。

## Symbol.iterator

为了理解可迭代对象这个概念，我们可以尝试自己写一个。

例如，下面这个对象，不是数组，但是看起来适用于 `for..of`，`range` 对象代表一组数字的区间：

```js
let range = {
  from: 1,
  to: 5
};

// We want for..of to work:
// for(let num of range) ... num=1,2,3,4,5
```

要让 `range` 可迭代（自然就能用于 `for..of`），我们需要给这个对象加一个名为 `Symbol.iterator`（一个专用的内建 symbol）的方法。

- 当 `for..of` 开始就会调用此方法（没有的话就会报错）。
- 这个方法必定返回一个 *迭代器（iterator）*（一个有 `next` 方法的对象）。
- `for..of` 获取下一个值时调用 `next`。
- `next()` 返回的必定是这个格式 `{done: Boolean, value: any}`，`done=true` 时意味着迭代结束，非则 `value` 为下一个值。

以下是 `range` 的完整实现：

```js run
let range = {
  from: 1,
  to: 5
};

// 1. call to for..of initially calls this
range[Symbol.iterator] = function() {

  // 2. ...it returns the iterator:
  return {
    current: this.from, // start at "range.from",
    last: this.to,      // end at "range.to"

    // 3. next() is called on each iteration by for..of
    next() {
      if (this.current <= this.last) {
        // 4. it should return the value as an object {done:.., value :...}
        return { done: false, value: this.current++ };
      } else {
        return { done: true };
      }
    }
  };
};

for (let num of range) {
  alert(num); // 1, then 2, 3, 4, 5
}
```

这段代码包含了分离关注点的思想：

- `range` 本身没有 `next()` 方法。
- 调用 `range[Symbol.iterator]()` 生成的“迭代器”主导迭代过程。

所以迭代器和对象本身是分离的。

从技术上讲，可以合并他们，使用 `range` 本身作为迭代器，使代码更简洁（但这有个缺点）：

```js run
let range = {
  from: 1,
  to: 5,

  [Symbol.iterator]() {
    this.current = this.from;
    return this;
  },

  next() {
    if (this.current <= this.to) {
      return { done: false, value: this.current++ };
    } else {
      return { done: true };
    }
  }
};

for (let num of range) {
  alert(num); // 1, then 2, 3, 4, 5
}
```

现在 `range[Symbol.iterator]()` 返回 `range` 对象本身，也有自己的 `next()` 方法。注意，当前迭代器使用的是 `this.current`。这或许可以正常运作，但是当两个 `for..of` 循环同时对这个对象操作：他们将会共享一个迭代器状态，因为这里面只有一个迭代器——对象本身。

```smart header="无限迭代器"
无限迭代器也是可行的。例如把例子改为 `range.to = Infinity`，或者写一个可迭代对象无限生成伪随机数，这个做法挺实用。

`next` 是无限制的，它可以返回无数的值。

当然，`for..of` 循环会因此变成无限循环，我们需要用 `break` 来停止循环。
```


## 字符串也可迭代

数组和字符串是使用得最多得内建可迭代对象。

`for..of` 循环一个字符串的字符：

```js run
for(let char of "test") {
  alert( char ); // t, then e, then s, then t
}
```

对组合字符（surrogate pairs）也正常工作！

```js run
let str = '𝒳😂';
for(let char of str) {
    alert(char); // 𝒳, and then 😂
}
```

## 显式调用迭代器

可迭代对象通常只与 `for..of` 循环合作，但是要深入理解这个玩意，我们还是要了解一下如何显式创建一个迭代器。我们可以直接调用它，实现 `for..of` 一样的效果。

一个例子，获取字符串的迭代器，手动调用它：

```js run
let str = "Hello";

// does the same as
// for (let char of str) alert(char);

let iterator = str[Symbol.iterator]();

while(true) {
  let result = iterator.next();
  if (result.done) break;
  alert(result.value); // outputs characters one by one
}
```

这种做法不常用，但给我们更多的操作自由。例如我们可以迭代部分，停止，处理其他任务，然后继续这个迭代。

## 可迭代对象与类数组对象

这两个名词初看或者有点相似，其实十分不同。

- *可迭代对象*是如上所述实现了 `Symbol.iterator` 方法的对象。
- *类数组对象*是拥有索引和 `length` 的对象，看起来像数组。

当然，两者也可以组合起来，例如字符串，就同时符合两者条件。

但是可迭代对象不一定是类数组对象，反之亦然。

上面的 `range` 是可迭代对象，但它没有索引和 `length`,所以并非类数组对象。

下例中是一个类数组对象，但不是可迭代对象：

```js run
let arrayLike = { // has indexes and length => array-like
  0: "Hello",
  1: "World",
  length: 2
};


// Error (no Symbol.iterator)
for(let item of arrayLike) {}

```

共同点是，他们通常**不是数组**，没有 `push`、`pop`等功能。当我们希望这个对象可以像数组一样操作的时候，就很不方便。

## Array.from

这里有一个通用方法 [Array.from](mdn:js/Array/from) 把他们组合到一块。它接受一个可迭代对象或类数组对象，返回一个真正的数组，这样我们就能对其进行数组操作。

例子：

```js run
let arrayLike = {
  0: "Hello",
  1: "World",
  length: 2
};


let arr = Array.from(arrayLike); // (*)

alert(arr.pop()); // World (method works)
```

`(*)` 标注的行中 `Array.from` 接受一个对象，检测它是否符合可迭代对象或者类数组对象，然后复制器内容返回一个新数组。

对于可迭代对象：

```js
// assuming that range is taken from the example above
let arr = Array.from(range);
alert(arr); // 1,2,3,4,5 (array toString conversion works)
```

`Array.from` 的完整语法中，可以提供映射函数：
```js
Array.from(obj[, mapFn, thisArg])
```

第二个参数 `mapFn` 函数在处理每一个元素后再放入新的数组，`thisArg` 参数可以设定它的 `this`。

例子：

```js
// assuming that range is taken from the example above

// square each number
let arr = Array.from(range, num => num * num);

alert(arr); // 1,4,9,16,25
```

也可以用 `Array.from` 处理字符串：

```js run
let str = '𝒳😂';

// splits str into array of characters
let chars = Array.from(str);

alert(chars[0]); // 𝒳
alert(chars[1]); // 😂
alert(chars.length); // 2
```

不同于 `str.split`，它依赖于字符串的可迭代性，可以像 `for..of` 一样正确分离组合字符。

用 `for..of` 实现相同效果：

```js run
let str = '𝒳😂';

let chars = []; // Array.from internally does the same loop
for(let char of str) {
  chars.push(char);
}

alert(chars);
```

...显然 `Array.from` 简单多了    

甚至可以实现组合字符的截取：

```js run
function slice(str, start, end) {
  return Array.from(str).slice(start, end).join('');
}

let str = '𝒳😂𩷶';

alert( slice(str, 1, 3) ); // 😂𩷶

// native method does not support surrogate pairs
alert( str.slice(1, 3) ); // garbage (two pieces from different surrogate pairs)
```


## 总结

可以用于 `for..of` 的对象称为*可迭代对象*。

- 可迭代对象必须实现一个 `Symbol.iterator` 方法。
    - `obj[Symbol.iterator]` 返回一个*迭代器*，用于处理后续迭代。
    - 迭代器必须有 `next()` 方法，返回一个 `{done: Boolean, value: any}`，`done:true` 时代表迭代结束，否则 `value` 成为下一次迭代的值。
- `Symbol.iterator` 方法在 `for..of` 中自动被调用，但也可以手动调用。
- 内建可迭代对象如字符串、数组，也实现了 `Symbol.iterator`。
- 字符串迭代器可以识别组合字符（surrogate pairs）。


拥有索引和 `length` 属性的对象被称为*类数组对象*。这类对象可以拥有其他属性和方法，但缺少数组的内建方法。

如果深入研究规范，我们可以看到内建方法大多假设他们是对可迭代对象或类数组对象作处理（而不是真正的数组），因为那更抽象。

`Array.from(obj[, mapFn, thisArg])` 用可迭代对象或类数组对象制作真数组，`mapFn` 和 `thisArg` 函数应用于其中的每一个元素。