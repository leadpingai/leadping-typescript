# Leadping TypeScript SDK

Type-safe TypeScript client for the Leadping API.

## Install

```bash
npm install @leadping/sdk
```

The generated client uses a Kiota request adapter. Install the default fetch adapter:

```bash
npm install @microsoft/kiota-http-fetchlibrary
```

GitHub Packages is also available:

```bash
npm config set @leadpingai:registry https://npm.pkg.github.com
npm install @leadpingai/sdk
```

## Use

```ts
import { createLeadpingOpenApiClient } from "@leadping/sdk";

const adapter = createLeadpingRequestAdapter();
const client = createLeadpingOpenApiClient(adapter);

const me = await client.users.me.get();
```

`createLeadpingRequestAdapter` is application code. Configure it to send one of:

- `Authorization: Bearer <token>`
- `X-Leadping-Api-Key: <key>`

The client defaults to `https://api.leadping.ai` when the adapter does not already have a base URL.

## Links

- [API reference](https://leadping.ai/docs/api-reference)
- [License](LICENSE)
