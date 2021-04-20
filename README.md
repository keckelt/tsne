# tSNE

Updated implementation of [tSNEJS](https://github.com/karpathy/tsnejs) in TypeScript.
Published it on NPM: `npm install @keckelt/tsne`.

## Usage

```ts
import {TSNE} from '@keckelt/tsne-js';

const data = [...];

// TODO one hot encoding, normalization, ...

const opt = {
  epsilon: 10, // epsilon is learning rate (10 = default)
  perplexity: data.length ** 0.5, // roughly how many neighbors each point influences (30 = default)
  dim: 2 // dimensionality of the embedding (2 = default)
};

const tsne = new TSNE(opt);
tsne.initDataRaw(data);

const iterations = 500;
for(let i = 0; i < iterations; i++) {
  tsne.step(); // every time you call this, solution gets better
}

var Y = tsne.getSolution(); // Y is an array of 2-D points that you can plot
```


### Worker

You can use [Comlink](https://github.com/GoogleChromeLabs/comlink), for example, to wrap the TSNE class and have the code executed in a worker thread:

```ts
import * as Comlink from 'comlink';
import { TSNE } from '@keckelt/tsne-js';

Comlink.expose(TSNE);
```
