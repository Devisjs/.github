# Devis

**Pattern-matching microservices for Node.js.** Register handlers under plain-object patterns, then call them in the same process or over TCP, Unix sockets, named pipes or RabbitMQ, with the same calling code.

```javascript
// math.js
const devis = require("devis");
devis.push({ role: "math", cmd: "sum" }, async ({ left, right }) => left + right);
devis.listen({ host: "127.0.0.1", port: 3030 });
```

```javascript
// client.js
const devis = require("devis");
devis.connect({ id: "math", host: "127.0.0.1", port: 3030 }, async () => {
    console.log(await devis.call({ clientId: "math", role: "math", cmd: "sum" }, { left: 1, right: 2 })); // 3
    devis.close();
});
```

Async handlers, awaited calls, timeouts, parallel calls per connection, graceful shutdown and TypeScript types since Devis 4.

```bash
npm install devis   # Node.js 22 or later
```

## Packages

| Package | What it does | |
| --- | --- | --- |
| [devis](https://github.com/Devisjs/devis) | The framework: patterns, local calls, TCP, Unix sockets, named pipes | [![npm](https://img.shields.io/npm/v/devis.svg)](https://www.npmjs.com/package/devis) |
| [devisPattern](https://github.com/Devisjs/devisPattern) | The exact-match pattern matcher behind Devis | [![npm](https://img.shields.io/npm/v/devisPattern.svg)](https://www.npmjs.com/package/devisPattern) |
| [devis-mongo-client](https://github.com/Devisjs/devis-mongo-client) | MongoDB plugin | [![npm](https://img.shields.io/npm/v/devis-mongo-client.svg)](https://www.npmjs.com/package/devis-mongo-client) |
| [devis-pub_sub-redis](https://github.com/Devisjs/devis-pub_sub-redis) | Redis pub/sub plugin | [![npm](https://img.shields.io/npm/v/devis-pub_sub-redis.svg)](https://www.npmjs.com/package/devis-pub_sub-redis) |
| [devis_rabbitmq](https://github.com/Devisjs/devis_rabbitmq) | RabbitMQ transport with per-call RPC replies | [![npm](https://img.shields.io/npm/v/devis_rabbitmq.svg)](https://www.npmjs.com/package/devis_rabbitmq) |
| [generator-devis](https://github.com/Devisjs/generator-devis) | `yo devis`: scaffold a gateway and a microservice | [![npm](https://img.shields.io/npm/v/generator-devis.svg)](https://www.npmjs.com/package/generator-devis) |

## Get started

- Read the [devis README](https://github.com/Devisjs/devis#readme) for the API and recipes.
- Run the [examples](https://github.com/Devisjs/Devis-Examples): local calls, TCP, MongoDB, Redis, RabbitMQ.
- Scaffold a project: `npm install -g yo generator-devis && yo devis`.

All packages are MIT licensed and tested on Node.js 22 and 24.
