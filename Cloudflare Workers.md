---
alias: Cloudflare Workers
---

- Serverless functions that run on Cloudflare's global edge network.
- Utilize the V8 JavaScript engine and operate similar to Node.js.
- Used to build and deploy code closer to users for better speed and reliability.
- Common use cases for Cloudflare Workers:
    - edge caching, 
    - image optimization, 
    - redirects, and
    - rate limiting.

## Examples

### Simple Web Page

```ts
export default {
    async fetch(request: Request) {
        const html = `<!DOCTYPE html>
            <html>
                <body>
                    <h1>Hello, World!</h1>
                </body>
            </html>`;

        return new Response(html, {
            headers: {
                "content-type": "text/html;charset=UTF-8",
            },
        });
    },
} satisfies ExportedHandler;
```

### Redirect Service

```ts
export default {
    async fetch(request: Request) {
        const to = "https://minch.dev";
        
        return Response.redirect(to, 301);
    },
} satisfies ExportedHandler;
```

### AI Text Generation

```ts
import { Ai } from "@cloudflare/ai";

export interface Env {
  AI: Ai;
}

export default {
    async fetch(request: Request, env: Env) {
        const ai = new Ai(env.AI);
        const genAiModel = "@cf/meta/llama-2-7b-chat-fp16";
        
        const url = new URL(request.url);
        const input = url.searchParams.get("query");

        if (!input.trim()) {
            input = "What is Cloudflare Workers?";
        }
        
        const messages = [
            { role: "system", content: "You are a friendly assistant" },
            { role: "user", content: input },
        ];
        
        const stream = await ai.run(genAiModel, {
            messages,
            stream: true,
        });
        
        return new Response(stream, {
            headers: { "content-type": "text/event-stream" },
        });
    },
};
```
