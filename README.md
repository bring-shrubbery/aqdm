# aqdm

Simple terminal progress indicator __that works__

- ✅ Simple API to show progress of a loop
- 🫡 Both CommonJS and ESM imports are supported
- 🔥 Examples of usage provided below
- 🥳 Written in TypeScript

## Installation

```sh
npm install aqdm
```

## Usage

### With iterable objects

```js
import aqdm from 'aqdm'

// Array, Generator, etc..
const arr = [...Array(1000)]

for(const v of aqdm(arr)) {
	// do something
}
```

Results:

```sh
  4.70% [=====>                                                            ] 00:00:04 00:01:37 [1923.72 iter/sec]
```

### Specify times of iteration instead of iterables

```js
for(const i of aqdm(300)) {
	// do something
}
```

Results:

```sh
  4.70% [=====>                                                            ] 00:00:04 00:01:37 [1923.72 iter/sec]
```

### Manualy process

```js
const prgrs = aqdm()
while(true) {
	prgrs.process()
}
```

Results:

```sh
  327 [=============================================================================] 00:00:04 [2089.72 iter/sec]
```

## Options

### `length`

You can manually specify total length of items when you works with iterable objects without `length` property. (Typically for generators.)

```js
function* gen(num) {
	for (let i = 0; i < num; i++) {
		yield i
	}
}

const g = gen(100)

for(const v of aqdm(g, {length: 100})){
	// do something
}
```

### `dest`

Choose where to write progress indicator ('stdout' or 'stderr'), another value will be ignored.  
Defaults to be 'stdout'.

```js
for(const v of aqdm(arr, {dest: 'stderr'})) {
	// now aqdm will write the progress into process.stderr
}
```

### `callback`

You can define your own callback function being called per iteration.

```js
const cb = ({current, total, ratio, elapsed, remain, perSec}) => {
	console.log({current, total, ratio, elapsed, remain, perSec})
}

for(const v of aqdm(arr, {callback: cb})) {
	// do something
}

```

### `silent`

`aqdm` will display nothing when set this option to true. (designed to use with callback function.)

```js
for(const v of aqdm(arr, {silent: true})) {
	// now aqdm displays nothing.
}
```
