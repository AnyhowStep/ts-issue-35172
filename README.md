### Repro

1. `npm install`
1. `npm run build`

https://github.com/microsoft/TypeScript/issues/35172

Expected, compiles (because `type-mapping` compiled successfully)

Actual, crashes.

-----

The commit on `type-mapping` is this,
https://github.com/AnyhowStep/type-mapping/commit/cb420b8e14dda4de5bf017bcc4a3ab3f35e71de5#diff-f84343d86daf9a112cfa32bdb89c7cdaR2

-----

### Output

```
../node_modules/@types/node/index.d.ts:823:11 - error TS2430: Interface 'NodeBuffer' incorrectly extends interface 'Uint8Array'.
  Types of property 'slice' are incompatible.
    Type '(start?: number, end?: number) => Buffer' is not assignable to type '(start?: number, end?: number) => Uint8Array'.
      Type 'Buffer' is not assignable to type 'Uint8Array'.
        Types of property 'slice' are incompatible.
          Type '(begin: number, end?: number) => ArrayBuffer' is not assignable to type '(start?: number, end?: number) => Uint8Array'.
            Type 'ArrayBuffer' is missing the following properties from type 'Uint8Array': BYTES_PER_ELEMENT, buffer, byteOffset, copyWithin, and 18 more.

823 interface NodeBuffer extends Uint8Array {
              ~~~~~~~~~~

node_modules/type-mapping/src/buffer.d.ts:2:11 - error TS2320: Interface 'Buffer' cannot simultaneously extend types 'ArrayBuffer' and 'NodeBuffer'.
  Named property 'slice' of types 'ArrayBuffer' and 'NodeBuffer' are not identical.

2 interface Buffer extends ArrayBufferLike {
            ~~~~~~


```