# AGENTS.md

This file is the operating guide for coding agents working in the public Leadping TypeScript SDK repository. Follow it together with `CONTRIBUTING.md`, `SECURITY.md`, `package.json`, and the project’s TypeScript configuration.

## Repository purpose

This repository contains the official TypeScript client for the Leadping API. Microsoft Kiota generates the client from Leadping’s OpenAPI contract. Applications provide the fetch request adapter, authentication provider, credential storage, retry behavior, and logging policy.

Authoritative public resources:

- API contract: <https://leadping.ai/docs/openapi.json>
- API documentation: <https://leadping.ai/docs/api-reference>
- Authentication discovery: <https://leadping.ai/auth.md>
- Security reporting: `SECURITY.md`

## Understand the change before editing

Endpoint paths, schemas, required fields, and response behavior belong in the upstream API/OpenAPI contract. Generated request builders, models, serializers, parsers, and `leadpingOpenApiClient.ts` should be regenerated from the corrected contract. Documentation, examples, npm metadata, workflows, and contributor files are maintained here.

If correct OpenAPI produces invalid TypeScript, identify the Kiota generator issue and keep any temporary workaround narrow and documented. Avoid unrelated regeneration, mass formatting, dependency upgrades, or lockfile churn.

## TypeScript conventions

- Preserve ESM output, strict typing, exports, and the compiler settings in `tsconfig.json`.
- Preserve Kiota request-adapter, authentication, parse-node, serialization, and error-mapping conventions.
- Do not introduce a second fetch wrapper or model serialization system.
- Avoid `any` when the generated model or a safe narrowing is available.
- Treat exported names, module paths, runtime behavior, and package exports as compatibility-sensitive.
- Do not edit `dist` directly; rebuild it from the TypeScript sources.

## Authentication and examples

Send Leadping credentials as `Authorization: Bearer <credential>`. Never commit or log real user tokens, WorkOS agent assertions or refresh tokens, organization API keys, or source keys. Examples must use nonfunctional values, inject credentials outside source control, and not imply that the SDK stores or refreshes credentials.

## Validation

For TypeScript, dependency, or package metadata changes, run:

```bash
npm ci
npm run build
```

Run relevant tests if a test suite is introduced. Documentation-only changes normally need link, spelling, and example review rather than dependency installation.

Before handing off, inspect `git diff` and the lockfile, explain OpenAPI or Kiota changes, update documentation when usage changes, and report checks run plus anything not validated.

## Releases and security

Do not change package versions, create tags, alter provenance or publishing workflows, or publish to npm unless explicitly authorized. Follow `SECURITY.md` for private vulnerability reporting.
