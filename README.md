# Leadping TypeScript SDK

Typed TypeScript client for the Leadping API, generated from `leadpingai/openapi` with Kiota.

## Install

```bash
npm install @leadpingai/leadping
```

Use a Kiota request adapter, such as:

```bash
npm install @microsoft/kiota-http-fetchlibrary
```

For GitHub Packages:

```bash
npm config set @leadpingai:registry https://npm.pkg.github.com
npm install @leadpingai/leadping
```

## Use

```ts
import { createLeadpingOpenApiClient } from "@leadpingai/leadping";

const adapter = createLeadpingRequestAdapter();
adapter.baseUrl = "https://api.leadping.ai";

const client = createLeadpingOpenApiClient(adapter);
const me = await client.users.me.get();
```

`createLeadpingRequestAdapter` should return a Kiota request adapter configured with your Leadping authentication.

## Release

Publishing is handled by this repository's `Publish TypeScript SDK` workflow. npm uses trusted publishing, so configure an npm trusted publisher for `leadpingai/leadping-typescript` and workflow file `publish.yml`.

## Notes

- Generated code comes from `leadpingai/openapi`; update the OpenAPI spec instead of hand-editing generated files.
- Package name: `@leadpingai/leadping`
- License: see `LICENSE`
