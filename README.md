# NumPy file parsing and serialization for TensorFlow.js

[![test](https://github.com/MaximeKjaer/tfjs-npy/actions/workflows/test.yml/badge.svg)](https://github.com/MaximeKjaer/tfjs-npy/actions/workflows/test.yml)
![npm (scoped)](https://img.shields.io/npm/v/@maximekjaer/tfjs-npy)

This is a fork of [tfjs-npy](https://github.com/propelml/tfjs-npy), which adds:

- New synchronous APIs
- `.npz` parsing and serialization
- Loading and saving files from disk

Note that because of support for `.npz` (which uses zlib for zipping), and for loading and saving files, this library is meant to be used in Node.js, not in the browser.

See https://docs.scipy.org/doc/numpy/neps/npy-format.html for more information about the file format.

API:

```ts
import * as tf from "@tensorflow/tfjs-core";
import { npy, npz } from "@maximekjaer/tfjs-npy";

////////////////
// .npy files //
////////////////

// Load a Tensor from a .npy file:
const tensor1: tf.Tensor = await npy.load("file.npy");

// Parse a Tensor from an ArrayBuffer containing the bytes of a .npy file:
const npyArrayBuffer: ArrayBuffer = getArrayBufferFromSomewhere();
const tensor2: tf.Tensor = npy.parse(npyArrayBuffer);

// Save a tensor to a .npy file:
await npy.save("file2.npy", tensor2);

// Serialize a tensor to an ArrayBuffer containing the bytes of the .npy file:
const npyArrayBuffer2: ArrayBuffer = await npy.serialize(tensor1);
const npyArrayBuffer3: ArrayBuffer = npy.serializeSync(tensor2);

////////////////
// .npz files //
////////////////

// Load a Tensor from a .npy file:
const tensors1: tf.Tensor[] = await npz.load("file.npz");

// Parse a Tensor from an ArrayBuffer containing the bytes of a .npy file:
const npzArrayBuffer: ArrayBuffer = getArrayBufferFromSomewhere();
const tensors2: tf.Tensor[] = npz.parse(npyArrayBuffer);

// Save a tensor to a .npy file:
await npz.save("file2.npz", tensors2);

// Serialize a tensor to an ArrayBuffer containing the bytes of the .npy file:
const npzArrayBuffer2: ArrayBuffer = await npz.serialize(tensors1);
const npzArrayBuffer3: ArrayBuffer = npz.serializeSync(tensors2);
```
