## Runtyped

TypeScript types disappear at runtime. Runtyped changes that, preserving types
at runtime via a fork of the TypeScript compiler. Define your types once and
use them everywhere for validation, serialization, JSON Schema generation and
full runtime reflection. No schema duplication. Just TypeScript.

Runtyped is framework-agnostic: it is concerned only with type reflection,
while staying flexible enough for framework-specific features to be built on
top of it.

### Packages

| Package | What it is | Repository |
| --- | --- | --- |
| [`@runtyped/typescript`](https://npm.im/@runtyped/typescript) | A fork of the official TypeScript 7.x compiler (written in Go) that emits type information as regular JavaScript values. Drop-in replacement for the `typescript` package, same CLI. | [runtyped/TypeScript](https://github.com/runtyped/TypeScript) |
| [`@runtyped/type`](https://npm.im/@runtyped/type) | The runtime library that consumes those values: `is`, `cast`, `validate`, `serialize`, `typeOf`, `toJsonSchema` and more. | [runtyped/runtyped](https://github.com/runtyped/runtyped) |

Both packages share a major version, which tracks the reflection format: any
`@runtyped/type` works with any `@runtyped/typescript` of the same major.

### Quick start

```sh
npm i --save-dev @runtyped/typescript
npm i --save @runtyped/type
```

```typescript
import { cast, validate, toJsonSchema } from '@runtyped/type';

interface User {
  id: number;
  registered: Date;
  username: string;
}

const user = cast<User>({ id: 1, registered: '2024-01-15T10:30:00Z', username: 'peter' });
user.registered instanceof Date; // true

validate<User>({ id: 'not a number' }); // [{ path: 'id', message: 'Not a number' }]

const schema = toJsonSchema<User>();
```

Then compile as usual with `tsc`.

### Learn more

- [Documentation](https://github.com/runtyped/runtyped/blob/main/docs/00-index.md)
- [Changelog and migration notes](https://github.com/runtyped/runtyped/blob/main/CHANGELOG.md)
- [Versioning scheme](https://github.com/runtyped/runtyped#versioning)
- [Examples](https://github.com/runtyped/runtyped/tree/main/examples)

> [!NOTE]
> `@runtyped/type-compiler` (the TypeScript ≤ 6.x transformer), `@runtyped/core`,
> `@runtyped/type-spec` and `@runtyped/expect` are deprecated as of 3.0.0. See
> [TypeScript 6.x and @runtyped/type-compiler](https://github.com/runtyped/runtyped#typescript-6x-and-runtypedtype-compiler).

### Origins

Runtyped started in 2026 as a selective fork of the runtime type modules of
the astounding [Deepkit] by Marc J. Schmidt. See [Relationship to Deepkit].

[Deepkit]: https://github.com/marcj/deepkit
[Relationship to Deepkit]: https://github.com/runtyped/runtyped#relationship-to-deepkit

### License

`@runtyped/type` is MIT-licensed. `@runtyped/typescript` is Apache 2.0, like
upstream TypeScript.
