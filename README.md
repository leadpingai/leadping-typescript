# Leadping TypeScript SDK

Typed TypeScript client source for the Leadping API, generated from the public Leadping OpenAPI document with Microsoft Kiota.

This SDK gives TypeScript applications a fluent, strongly typed way to call Leadping API resources such as leads, conversations, SMS, phone numbers, automations, reports, billing, and users.

## At a glance

| Item             | Value                            |
| ---------------- | -------------------------------- |
| Repository       | `leadpingai/leadping-typescript` |
| Package name     | `@leadpingai/leadping`           |
| Main factory     | `createLeadpingOpenApiClient`    |
| Main client type | `LeadpingOpenApiClient`          |
| Default API host | `https://api.leadping.ai`        |
| OpenAPI source   | `leadpingai/openapi`             |
| Generator        | Microsoft Kiota `1.32.2`         |

## Status

This repository contains generated SDK source plus npm package metadata. The `Publish TypeScript SDK` GitHub Actions workflow builds the package, publishes it to npm, publishes it to GitHub Packages, tags the commit, and creates a GitHub release with the npm tarball.

The generated source is refreshed from `leadpingai/openapi`. Do not hand-edit generated `.ts` files; update the OpenAPI document and regenerate the SDK instead. This README is intended to be preserved across regenerations.

## Install

Install from npm after a version is published:

```bash
npm install @leadpingai/leadping
```

To install from GitHub Packages, configure the Leadping scope first:

```bash
npm config set @leadpingai:registry https://npm.pkg.github.com
npm install @leadpingai/leadping
```

The package includes the Kiota abstractions and serialization dependencies required by the generated client. Applications still choose their own Kiota request adapter and authentication provider. For the standard fetch adapter used in the quick start:

```bash
npm install @microsoft/kiota-http-fetchlibrary
```

Recommended `tsconfig.json` settings for Kiota-generated clients:

```json
{
  "compilerOptions": {
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true,
    "lib": ["es2020", "dom"],
    "module": "NodeNext",
    "moduleResolution": "NodeNext",
    "target": "es2020"
  }
}
```

Set ESM mode in `package.json`:

```json
{
  "type": "module"
}
```

## Quick start

```ts
import { FetchRequestAdapter } from "@microsoft/kiota-http-fetchlibrary";
import type {
  AuthenticationProvider,
  RequestInformation,
} from "@microsoft/kiota-abstractions";

import { createLeadpingOpenApiClient } from "@leadpingai/leadping";

class BearerTokenAuthenticationProvider implements AuthenticationProvider {
  public constructor(private readonly token: string) {}

  public authenticateRequest = async (
    request: RequestInformation,
    _additionalAuthenticationContext?: Record<string, unknown>,
  ): Promise<void> => {
    request.headers.add("Authorization", `Bearer ${this.token}`);
  };
}

const token = process.env.LEADPING_API_TOKEN;
if (!token) {
  throw new Error("LEADPING_API_TOKEN is required.");
}

const adapter = new FetchRequestAdapter(
  new BearerTokenAuthenticationProvider(token),
);
adapter.baseUrl = "https://api.leadping.ai";

const client = createLeadpingOpenApiClient(adapter);
const me = await client.users.me.get();

console.log(me?.email);
```

For production applications, use an authentication provider that matches your Leadping credential flow and refreshes credentials as needed.

## Common entry points

The client exposes request builders for the main Leadping API areas:

| Area              | Builder                                                                          |
| ----------------- | -------------------------------------------------------------------------------- |
| Leads             | `client.leads`                                                                   |
| Conversations     | `client.conversations`                                                           |
| SMS               | `client.sms`                                                                     |
| Phone numbers     | `client.phoneNumbers`                                                            |
| Automations       | `client.automations`                                                             |
| Sources           | `client.sources`                                                                 |
| Reports           | `client.reports`                                                                 |
| Users             | `client.users`                                                                   |
| Businesses        | `client.businesses`                                                              |
| Usage and billing | `client.usage`, `client.wallets`, `client.transactions`, `client.paymentMethods` |

Each builder mirrors the OpenAPI path structure and provides typed request and response models from `models/index.ts`.

## Regenerating

This SDK is regenerated by the Leadping GitHub workflow from the canonical OpenAPI repository:

```bash
kiota generate \
  --openapi ../openapi/openapi.json \
  --language TypeScript \
  --output . \
  --class-name LeadpingOpenApiClient \
  --namespace-name leadping \
  --exclude-backward-compatible
```

## Support

Use the Leadping API documentation and the OpenAPI document as the source of truth for routes, schemas, authentication requirements, and response shapes.

Useful links:

- Leadping API host: <https://api.leadping.ai>
- OpenAPI repository: <https://github.com/leadpingai/openapi>
- Kiota documentation: <https://learn.microsoft.com/openapi/kiota/>
