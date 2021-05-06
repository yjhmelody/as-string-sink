String Sink
===
[![Build Status](https://github.com/MaxGraey/as-string-sink/actions/workflows/test.yml/badge.svg?event=push)](https://github.com/MaxGraey/as-string-sink/actions/workflows/test.yml)

An efficient dynamically sized string buffer (aka **String Builder**) for AssemblyScript.

## Current status

_WIP_

## Interface

```ts
class StringSink {
  constructor(initial: string = "");

  get length(): i32;
  get capacity(): i32;

  write(str: string): void;
  writeLn(str: string): void;
  writeCodePoint(code: i32): void;

  shrink(): void;
  clear(): void;

  toString(): string;
}
```

## Usage

non efficient example:

```ts
function toList(arr: string[]): string {
  let res = "";
  for (let i = 0, len = arr.length; i < len; i++) {
    res += arr[i] + "\n";
  }
  return res;
}
```

efficient with `StringSink`:

```ts
function toList(arr: string[]): string {
  let res = new StringSink();
  for (let i = 0, len = arr.length; i < len; i++) {
    res.write(arr[i] + "\n");
  }
  return res.toString();
}
```

even more efficient:

```ts
function toList(arr: string[]): string {
  let res = new StringSink();
  for (let i = 0, len = arr.length; i < len; i++) {
    res.writeLn(arr[i]);
  }
  return res.toString();
}
```

## TODO

- add tests
- add "start" and "end" optional arguments for write / writeLn
