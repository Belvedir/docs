# Source: https://api.fractalresearch.ai/docs

# Documentation

Get started with Fractal in under 5 minutes.

## Getting Started

1. **1\. Create an instance**Sign in to the platform and create a new instance. You'll receive an API key starting with `fr_live_`. Save it somewhere secure — it won't be shown again.
2. **2\. Install the SDK**
 
 npm install @fractalresearch/loop
 
3. **3\. Initialize in your application**
 
 import { initialize } from "@fractalresearch/loop"; initialize({ apiKey: process.env.FRACTAL\_API\_KEY, baseUrl: "https://api.fractalresearch.ai", appName: "my-ai-app", });
 
 Call this once at your application's entry point, before any AI/LLM calls are made.
4. **4\. That's it**The SDK automatically instruments your LLM calls. Traces appear in your instance dashboard within seconds.

## Configuration

apiKey

Required. Your Fractal API key.

baseUrl

Fractal platform URL. Defaults to `https://api.fractalresearch.ai`

appName

Your application name. Used to label traces.

disableBatch

Send spans immediately instead of batching. Useful for testing.

## Supported Providers

The SDK auto-instruments these LLM providers with zero additional code:

- OpenAI
- Anthropic
- Cohere
- Azure OpenAI
- Amazon Bedrock
- Google Vertex AI
- Replicate
- HuggingFace

## How It Works

1. **Instrument** — The SDK hooks into your LLM client libraries and captures every call as an OpenTelemetry span.
2. **Collect** — Spans are batched and sent to your Fractal instance via the OTLP HTTP protocol.
3. **Analyze** — Fractal analyzes trace patterns against your improvement target using Claude.
4. **Improve** — Fractal opens GitHub PRs with suggested code changes to your codebase.

## API Reference

### POST /api/v1/traces

Receives OpenTelemetry trace data in OTLP JSON format. This is called automatically by the SDK.

Authorization — Bearer token with your API key, or use the `x-api-key` header.

Body — OTLP JSON with a `resourceSpans` array.

## Common Issues

### No traces appearing on Vercel

The Fractal SDK relies on OpenTelemetry, which requires the Node.js runtime. On Vercel, routes can default to the Edge runtime where the SDK silently skips initialization. Add the following to any API route that makes LLM calls:

export const runtime = 'nodejs'

### LLM clients created before SDK initializes

If you create OpenAI or Anthropic clients at module scope, make sure `initialize()` runs before the client instances are created. The SDK patches module prototypes, so imports can be hoisted above it — but `new OpenAI()` must come after. Call `initialize()` at the top of the module, before any client instantiation:

import { initialize } from "@fractalresearch/loop"; import OpenAI from "openai"; initialize({ apiKey: process.env.FRACTAL\_API\_KEY }); const openai = new OpenAI();

In Next.js, you can also use `instrumentation.ts` to run initialization at startup, but this may not work if route modules load before the instrumentation hook fires.

### Traces missing in development

Ensure your `FRACTAL_API_KEY` environment variable is set and that `initialize()` is called before any LLM client is created. Check your terminal for SDK warnings on startup.