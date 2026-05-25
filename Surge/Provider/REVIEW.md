# Provider Review Queue

This file tracks source rules that were not automatically merged into the active
provider lists.

## Not Auto-Merged

### Auto

`Auto/` appears to be an older split profile, not a current provider source. The
following files need manual review before any future merge:

- `Auto/DIRECT.conf`: old domestic/direct rules. Some overlap with `China.list`,
  but it also contains local-network, SMTP, BT, and behavior rules.
- `Auto/PROXY.conf`: old proxy rules. Some entries overlap with current
  `Proxy.list`, but it may reintroduce services that were intentionally removed
  or moved.
- `Auto/REJECT.conf`: not merged. Keep reject behavior isolated and do not move
  these rules into routing provider lists without explicit review.
- `Auto/Header Rewrite.conf`, `Auto/URL Rewrite.conf`, `Auto/Script.conf`,
  `Auto/Hostname.conf`: rewrite, script, and MITM support files, not provider
  routing rules.
- `Auto/HOST.conf`: empty.

Only clear Apple direct rules from `Auto/Apple.conf` were merged into
`Apple Microsoft.list`.

### 2025/Home_IP_Only.list

This file mixes AI, developer tools, cloud services, and app-specific rules. It
was not merged wholesale.

Already covered by the active `AI.list`:

- `openai.com`, `chatgpt.com`, `oaiusercontent.com`
- `anthropic.com`, `claude.ai`, `claudeusercontent.com`
- `api.anthropic.com` is covered by `anthropic.com`
- `cdn.oaistatic.com` is covered by `oaistatic.com`

Needs manual routing decision:

- Augment: `augment.com`, `augmentcode.com`
- Cloudflare AI Gateway: `gateway.ai.cloudflare.com`
- GitHub Copilot: `githubcopilot.com`, `api.github.com`
- Microsoft Copilot and Bing AI domains
- Cursor, Codeium, Windsurf
- Dify, xAI/Grok, Groq, Jasper, Clipdrop
- Meta AI and Llama domains
- Perplexity domains
- Poe, You.com, Phind, Hugging Face, Replicate
- Stability AI, Midjourney, Runway, Suno, ElevenLabs
- Replit, Lovable, v0, Bolt, Supabase, Railway, Vercel, Netlify

### 2025/Global.list

This file is a broad global proxy list. It overlaps heavily with current
`Proxy.list`, `Apple Microsoft.list`, and `China.list`. It was not merged as a
whole because it would blur the route ownership model.

### 2025/block_udp443.list

Contains:

```text
AND,((PROTOCOL,UDP),(DEST-PORT,443)),REJECT-NO-DROP
```

This is a behavior rule for blocking QUIC/UDP 443, not a provider domain list.
Keep it for main-config or module review.
