Here's an edited version of your linked list README file with expanded explanations and descriptions, while maintaining the original structure. This version aims to provide a comprehensive overview of linked lists while following the conventions of a GitHub README file.

---

# Linked List

## Contents

*   [What is this?](#what-is-this)
*   [When should I use this?](#when-should-i-use-this)
*   [Installation](#installation)
*   [Usage](#usage)
*   [API](#api)
    *   [`List([items…])`](#listitems)
    *   [`Item()`](#item)
*   [Types](#types)
*   [Compatibility](#compatibility)
*   [Security](#security)
*   [Contributing](#contributing)
*   [License](#license)

## What is this?

This package provides a small, efficient implementation of a **doubly linked list**. In a linked list, each item (or node) contains references to both the next sibling (the item that follows it) and the previous sibling (the item that precedes it). This structure allows for efficient insertion and deletion operations from both ends of the list and anywhere in between.

### Key Features:
- **Doubly Linked**: Each item has references to both its next and previous items, making it easy to traverse in both directions.
- **Dynamic Size**: Unlike arrays, linked lists do not require a predefined size; they can grow or shrink as needed.

## When should I use this?

You should consider using this implementation of a linked list when you need a data structure that allows for:
- **Frequent insertions and deletions**: Linked lists are particularly useful when your application requires numerous insertions and deletions since these operations can be done in constant time.
- **Dynamic memory allocation**: When the size of the data structure is unpredictable, linked lists are preferable to arrays, which have a fixed size.
- **Bidirectional traversal**: If you need to traverse your data in both directions (forward and backward), a doubly linked list is ideal.

## Installation

This package is **ESM only** (ECMAScript Module). In Node.js (version 14.14+, 16.0+), you can install it using [npm][]:

```sh
npm install linked-list
```

In Deno, you can import it from [`esm.sh`][esmsh]:

```js
import {List, Item} from 'https://esm.sh/linked-list@3'
```

In browsers, you can use the same URL to import it:

```html
<script type="module">
  import {List, Item} from 'https://esm.sh/linked-list@3?bundle'
</script>
```

## Usage

Here’s a simple example of how to create and use a linked list:

```js
import {List, Item} from 'linked-list'

// Create items
const item1 = new Item();
const item2 = new Item();
const item3 = new Item();

// Initialize the list with items
const list = new List(item1, item2, item3);

// Accessing items
console.log(list.head); // => item1
console.log(list.head.next); // => item2
console.log(list.head.next.next); // => item3
console.log(list.head.next.prev); // => item1
console.log(list.tail); // => item3
console.log(list.tail.next); // => null
```

### Subclassing

You can extend the base `List` and `Item` classes to create your own specialized versions:

```js
import {List, Item} from 'linked-list'

// Custom List class for tokens
class Tokens extends List {
  /** @param {string} delimiter */
  join(delimiter) {
    return this.toArray().join(delimiter);
  }
}

// Custom Item class for tokens
class Token extends Item {
  /** @param {string} value */
  constructor(value) {
    super();
    this.value = value;
  }

  toString() {
    return this.value;
  }
}

// Create token instances
const dogs = new Token('dogs');
const and = new Token('&');
const cats = new Token('cats');

// Initialize Tokens list
const tokens = new Tokens(dogs, and, cats);

console.log(tokens.join(' ')); // => 'dogs & cats'

// Manipulating items
and.prepend(cats);
and.append(dogs);

console.log(tokens.join(' ') + '!'); // => 'cats & dogs!'
```

## API

This package exports two main identifiers: `List` and `Item`. There is no default export.

### `List([items…])`

Creates a new list from the given items.

```js
new List(); // Creates an empty list
new List(new Item(), new Item()); // Creates a list with provided items
```

#### `List.from([items])`

Creates a new list from the given array of items.

```js
List.from(); // Creates an empty list
List.from([]); // Creates an empty list
List.from([new Item(), new Item()]); // Creates a list from the provided array
```

#### `List.of([items…])`

Creates a new list from the given arguments.

```js
List.of(); // Creates an empty list
List.of(new Item(), new Item()); // Creates a list with provided items
```

### `List#append(item)`

Adds an item to the end of the list.

```js
const list = new List();
const item = new Item();

console.log(list.head === null); // => true
console.log(item.list === null); // => true

list.append(item);

console.log(list.head === item); // => true
console.log(item.list === list); // => true
```

### `List#prepend(item)`

Adds an item to the beginning of the list.

```js
const list = new List();
const item = new Item();

list.prepend(item);
```

### `List#toArray()`

Returns the items of the list as an array.

```js
const item1 = new Item();
const item2 = new Item();
const list = new List(item1, item2);
const array = list.toArray();

console.log(array[0] === item1); // => true
console.log(array[1] === item2); // => true
console.log(array[0].next === item2); // => true
console.log(array[1].prev === item1); // => true
```

### `List#head`

The first item in a list or `null` if the list is empty.

```js
const item = new Item();
const list = new List(item);

console.log(list.head === item); // => true
```

### `List#tail`

The last item in a list or `null` if the list is empty.

```js
const list = new List();
const item1 = new Item();
const item2 = new Item();

console.log(list.tail === null); // => true

list.append(item1);
console.log(list.tail === null); // => true, see note.

list.append(item2);
console.log(list.tail === item2); // => true
```

> 👉 **Note**: A list with only one item has **no tail**, only a head.

### `List#size`

The number of items in the list.

```js
const list = new List();
const item1 = new Item();
const item2 = new Item();

console.log(list.size === 0); // => true

list.append(item1);
console.log(list.size === 1); // => true

list.append(item2);
console.log(list.size === 2); // => true
```

### `Item()`

Creates a new linked list item.

```js
const item = new Item();
```

### `Item#append(item)`

Adds the given item **after** the operated-on item in a list.

```js
const item1 = new Item();
const item2 = new Item();

new List().append(item1);

console.log(item1.next === null); // => true

item1.append(item2);
console.log(item1.next === item2); // => true
```

### `Item#prepend(item)`

Adds the given item **before** the operated-on item in a list.

```js
const item1 = new Item();
const item2 = new Item();

new List().append(item1);

console.log(item1.prev === null); // => true

item1.prepend(item2);
console.log(item1.prev === item2); // => true
```

### `Item#detach()`

Removes the operated-on item from its parent list.

```js
const item = new Item();
const list = new List(item);

console.log(item.list === list); // => true

item.detach();
console.log(item.list === null); // => true
```

### `Item#next`

The following item or `null` if there is none.

```js
const item1 = new Item();
const item2 = new Item();

const list = new List(item1);

console.log(item1.next === null); // => true
console.log(item2.next === null); // => true

item1.append(item2);

console.log(item1.next === item2); // => true

item1.detach();

console.log(item1.next === null); // => true
```

### `Item#prev`

The preceding item or `null` if there is none.

```js
const item1 = new Item();
const item2 = new Item();

const list = new List(item1);

console.log(item1.prev === null); // => true
console.log(item2.prev === null); // => true

item1.append(item2);

console.log(item2.prev === item1); // => true

item2.detach();

console.log

(item2.prev === null); // => true
```

### `Item#list`

The list this item belongs to or `null` if detached.

```js
const item = new Item();
const list = new List();

console.log(item.list === null); // => true

list.append(item);

console.log(item.list === list); // => true

item.detach();

console.log(item.list === null); // => true
```

## Types

This package is fully typed with [TypeScript][typescript]. It exports no additional types beyond those defined.

## Compatibility

This package is compatible with all maintained versions of Node.js, specifically:
- Node.js 14.14+ 
- Node.js 16.0+ 

It also works seamlessly in Deno and modern browsers.

## Security

This package is designed with security in mind and has been tested for vulnerabilities. 

## Contributing

Contributions are welcome! Please see [How to Contribute to Open Source][contribute] for guidelines on how to get involved.

## License

[MIT][license] © [Titus Wormer][author]

<!-- Definitions -->

[build-badge]: https://github.com/wooorm/linked-list/workflows/main/badge.svg
[build]: https://github.com/wooorm/linked-list/actions
[coverage-badge]: https://img.shields.io/codecov/c/github/wooorm/linked-list.svg
[coverage]: https://codecov.io/github/wooorm/linked-list
[downloads-badge]: https://img.shields.io/npm/dm/linked-list.svg
[downloads]: https://www.npmjs.com/package/linked-list
[size-badge]: https://img.shields.io/bundlephobia/minzip/linked-list.svg
[size]: https://bundlephobia.com/result?p=linked-list
[npm]: https://docs.npmjs.com/cli/install
[esmsh]: https://esm.sh
[license]: license
[author]: https://wooorm.com
[esm]: https://gist.github.com/sindresorhus/a39789f98801d908bbc7ff3ecc99d99c
[typescript]: https://www.typescriptlang.org
[contribute]: https://opensource.guide/how-to-contribute/
[wiki]: https://wikipedia.org/wiki/Linked_list

---

Feel free to modify any sections further or ask for specific changes!
