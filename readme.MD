## Why

The Gemini API is [free](https://ai.google.dev/pricing "limits applied!"), but there are many tools that work exclusively with the OpenAI API.

This project provides a personal OpenAI-compatible endpoint for free.

## Serverless?

Although it runs in the cloud, it does not require server maintenance.
It can be easily deployed to various providers for free (with generous limits suitable for personal use).

> [!TIP]  
> Running the proxy endpoint locally is also an option, though it's more appropriate for development use.

## How to start

You will need a personal Google [API key](https://makersuite.google.com/app/apikey).

Even if you are located outside of the [supported regions](https://ai.google.dev/available_regions#available_regions) (e.g., in Europe), it is still possible to acquire one using a VPN.

Then deploy the project to one of the providers, using the instructions below. You will need to set up an account there (and on Github).

### Deploy With Vercel

- [![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/PublicAffairs/openai-gemini&repository-name=my-openai-gemini)
- Alternatively can be deployed with [cli](https://vercel.com/docs/cli):
  `vercel deploy`
- Serve locally: `vercel dev`

### Deploy to Netlify

- [![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/PublicAffairs/openai-gemini&integrationName=integrationName&integrationSlug=integrationSlug&integrationDescription=integrationDescription)
- Alternatively can be deployed with [cli](https://docs.netlify.com/cli/get-started/):
  `netlify deploy`
- Serve locally: `netlify dev`

### Deploy to Cloudflare

https://developers.cloudflare.com/workers/tutorials/deploy-button/

- [![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/PublicAffairs/openai-gemini)
- Alternatively can be deployed manually pasting content of `src/worker.mjs` to https://workers.cloudflare.com/playground (see there `Deploy` button).
- Alternatively can be deployed with [cli](https://developers.cloudflare.com/workers/wrangler/):
  `wrangler deploy`
- Serve locally: `wrangler dev`

## How to use

> [!WARNING]  
> Not all tools allows overriding the OpenAI endpoint, but many do (however these settings can sometimes be deeply hidden).

Use the endpoint address wherever you can specify it. The relevant field may be labeled as "OpenAI proxy". You might need to look under "Advanced settings" or similar sections. Or in some sonfig file.

For some command-line tools, you may need to set an env variable, _e.g._:  
`set OPENAI_BASE_URL=https://my-super-proxy.vercel.app/v1`  
_..or_:  
`set OPENAI_API_BASE=https://my-super-proxy.vercel.app/v1`


---

## Possible further development

- [x] `chat/completions`
    Currently, most of the parameters that make sense for both APIs are implemented, except for function calls.
    <details>

    - [x] messages
        - [x] content
        - [x] role
            - [x] system (=>user)
            - [x] user
            - [x] assistant
            - [ ] tool (v1beta)
        - [ ] name
        - [ ] tool_calls
    - [x] model _(value ignored, autoselect "gemini-pro", or "-vision" for "gpt-4-vision-preview" request)_
    - [ ] frequency_penalty
    - [ ] logit_bias
    - [ ] logprobs
    - [ ] top_logprobs
    - [x] max_tokens
    - [x] n (candidateCount <8) _n.b.: atm api does not accept >1_
    - [ ] presence_penalty
    - [ ] response_format
    - [ ] seed
    - [x] stop: string|array (stopSequences [1,5])
    - [x] stream
    - [x] temperature (0.0..1.0)
        - [ ] <0, >1..2
    - [x] top_p
    - [ ] tools (v1beta)
    - [ ] tool_choice (v1beta)
    - [ ] user

    </details>
- [ ] `completions`
- [ ] `embeddings`
- [ ] `models`
