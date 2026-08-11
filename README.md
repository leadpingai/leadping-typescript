[![](https://img.shields.io/npm/v/@leadping/sdk.svg?style=for-the-badge)](https://www.npmjs.com/package/@leadping/sdk)
[![](https://img.shields.io/github/actions/workflow/status/leadpingai/leadping-typescript/publish.yml?style=for-the-badge)](https://github.com/leadpingai/leadping-typescript/actions/workflows/publish.yml)
[![](https://img.shields.io/npm/dt/@leadping/sdk.svg?style=for-the-badge)](https://www.npmjs.com/package/@leadping/sdk)
[![](https://img.shields.io/github/actions/workflow/status/leadpingai/leadping-typescript/codeql.yml?label=CodeQL&style=for-the-badge)](https://github.com/leadpingai/leadping-typescript/actions/workflows/codeql.yml)

# ![Leadping](https://leadping.ai/favicon.ico) Leadping TypeScript SDK

The official, type-safe TypeScript and JavaScript SDK for the Leadping API. Use it to integrate lead management, conversations, SMS and calling, automations, reporting, billing, and business settings into Node.js and server-side TypeScript applications.

The package is generated from the [Leadping OpenAPI specification](https://leadping.ai/docs/openapi.json) with Microsoft Kiota. It contains request builders and models; your application supplies the fetch request adapter, credentials, retry policy, and credential storage.

## Installation

Install the SDK and Kiota's fetch adapter:

```bash
npm install @leadping/sdk @microsoft/kiota-http-fetchlibrary
```

The SDK package is `@leadping/sdk`. The similarly named `@leadpingai/sdk` package is only used when consuming releases from GitHub Packages.

## Authentication

Set `LEADPING_API_KEY` to a WorkOS organization API key (`sk_...`). The SDK sends it as `Authorization: Bearer <credential>`. User access tokens are also supported when acting for a signed-in user; `lp_src_...` keys are only for lead-ingestion endpoints. See [API authentication](https://leadping.ai/docs/api-authentication). Do not expose organization or source keys in browser code.

## Create a client

Kiota's API-key authentication provider can place the complete Bearer value in the `Authorization` header:

```ts
import { createLeadpingOpenApiClient } from "@leadping/sdk";
import {
  ApiKeyAuthenticationProvider,
  ApiKeyLocation,
} from "@microsoft/kiota-abstractions";
import { FetchRequestAdapter } from "@microsoft/kiota-http-fetchlibrary";

const credential = process.env.LEADPING_API_KEY;
if (!credential) {
  throw new Error("LEADPING_API_KEY is not set.");
}

const authProvider = new ApiKeyAuthenticationProvider(
  `Bearer ${credential}`,
  "Authorization",
  ApiKeyLocation.Header,
  new Set(["api.leadping.ai"]),
);

const adapter = new FetchRequestAdapter(authProvider);
const client = createLeadpingOpenApiClient(adapter);

const lead = await client.leads.byId("lead-id").get();
console.log(lead?.id);
```

The client defaults to `https://api.leadping.ai`.

## Common operations

Request builders mirror the API path. Methods such as `byId()` select a resource; terminal methods send the request.

```ts
// Requires a user access token.
const currentUser = await client.users.me.get();

// Retrieve organization resources by ID.
const source = await client.sources.byId("source-id").get();
const lead = await client.leads.byId("lead-id").get();
```

Create and update operations accept generated request-body types exported by `@leadping/sdk`.

## Resources

- [Leadping introduction](https://leadping.ai/docs/introduction)
- [API authentication](https://leadping.ai/docs/api-authentication)
- [API reference](https://leadping.ai/docs/api-reference)
- [OpenAPI specification](https://leadping.ai/docs/openapi.json)
- [npm package](https://www.npmjs.com/package/@leadping/sdk)
- [License](LICENSE)
