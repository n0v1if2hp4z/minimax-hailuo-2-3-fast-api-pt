# MiniMax Hailuo 2.3 Fast API (`MiniMax-Hailuo-2.3-Fast`)

<!-- conv-kit:v1 -->

<p align="center">
  <img src="assets/badges/price.svg" alt="observed unit price"> <img src="assets/badges/billing.svg" alt="billing model"> <img src="assets/badges/compat.svg" alt="OpenAI-compatible endpoint">
</p>

<p align="center">
  <img src="assets/01-product-ad-ceramic-mug-thumb.jpg" width="820" alt="Sample video frame generated through APIMart">
</p>

> **from $0.0248 per second** on the APIMart route — um único endpoint compatível com OpenAI em `https://api.apimart.ai/v1`, sem plano mensal. *(observado em 2026-10-12)*

**[Obter uma chave de API](https://go.apimart.ai/k-1ca2fb)** · **[Preços ao vivo](https://go.apimart.ai/k-4eaecf)** · **[Página do modelo](https://go.apimart.ai/k-937e23)** · [⚡ Início rápido em 60 segundos](#quickstart)

**Por que os times usam MiniMax Hailuo 2.3 Fast (`MiniMax-Hailuo-2.3-Fast`) via APIMart**

- **Uma chave, o catálogo inteiro.** A mesma base URL `https://api.apimart.ai/v1` e o mesmo cabeçalho `Authorization` alcançam MiniMax Hailuo 2.3 Fast (`MiniMax-Hailuo-2.3-Fast`) e mais de 300 modelos de imagem, vídeo e linguagem — troque o campo `model`, não o seu cliente.
- **Mínimo de $1, pague conforme o uso.** Sem assinatura e sem plano pré-pago para dimensionar antes: recarregue a partir de $1 e gaste em chamadas.
- **A cobrança volta na resposta.** Toda tarefa concluída informa o valor cobrado (`cost` / `credits_cost`); uma tarefa marcada como `failed` é reembolsada.
- **Assíncrono por design.** Envie, pegue o `task_id`, consulte `GET /v1/tasks/{id}` — batching e retries são trabalho comum de fila, não uma integração sob medida.

<!-- /conv-kit:v1 -->



MiniMax Hailuo 2.3 Fast on APIMart is the latest generation AI video model, offering superior visual quality, high motion coherence, and professional-grade performance. This page uses MiniMax-Hailuo-2.3-Fast for image-to-video generation and requires a first-frame image.

## Model id and routes

| Route | `model` value | Billing | Notes |
| --- | --- | --- | --- |
| Text-to-video / image-to-video | `MiniMax-Hailuo-2.3-Fast` | per generated second, by resolution | see the [model page](https://go.apimart.ai/k-937e23) for the exact tiers |

Endpoint: `POST https://api.apimart.ai/v1/videos/generations`, then poll `GET /v1/tasks/{task_id}`.

## Pricing

<!-- pricing:model:start -->
| Resolution | List price | Effective price |
| --- | --- | --- |
| default | 0.031 | 0.0248 |


<!-- pricing:model:end -->

Prices are a snapshot; the [pricing page](https://go.apimart.ai/k-4eaecf) and [`data/model.json`](data/model.json) are refreshed by CI, and a completed task reports the exact amount in its `cost` field.

## Request parameters

| Field | Type | Default | Notes |
| --- | --- | --- | --- |
| `model` | string | required | the model id shown in the route table above |
| `prompt` | string | required | the shot description; camera and subject motion belong here |
| `duration` | integer | route default | clip length in seconds — billing is per generated second |
| `resolution` | string | route default | 480P / 720P / 1080P or the route’s own tiers |
| `size` / `aspect_ratio` | string | `16:9` | output framing |
| `image_urls` | string[] | — | first frame, first + last frame, or style references, where supported |
| `seed` | integer | — | fix the seed to reproduce a take |

The table lists the fields accepted by the APIMart `videos/generations` endpoint. Check the [model page](https://go.apimart.ai/k-937e23) for anything this model adds on top.

## Quickstart

```bash
curl --request POST --url https://api.apimart.ai/v1/videos/generations \
  --header "Authorization: Bearer $APIMART_API_KEY" --header 'Content-Type: application/json' \
  -d '{"model":"MiniMax-Hailuo-2.3-Fast","prompt":"A bamboo forest at sunrise, slow push-in","duration":5,"resolution":"720P","size":"16:9"}'
```

```python
import os, time, requests

BASE = "https://api.apimart.ai/v1"
HEADERS = {"Authorization": f"Bearer {os.environ['APIMART_API_KEY']}", "Content-Type": "application/json"}

created = requests.post(f"{BASE}/videos/generations", headers=HEADERS, timeout=60, json={
    "model": "MiniMax-Hailuo-2.3-Fast", "prompt": "A bamboo forest at sunrise, slow push-in", "duration": 5,
}).json()
task_id = created["data"]["id"]

while True:
    task = requests.get(f"{BASE}/tasks/{task_id}", headers=HEADERS, timeout=60).json()["data"]
    if task["status"] in ("completed", "failed"):
        break
    time.sleep(5)
print(task.get("cost"), task["result"]["videos"][0]["url"])
```

Runnable versions: [`examples/`](examples). The task lifecycle is `pending → processing → completed | failed`.

## FAQ

**Qual é o id do modelo MiniMax Hailuo 2.3 Fast?**

`MiniMax-Hailuo-2.3-Fast`. Veja a tabela de rotas acima.

**Como é a cobrança?**

**from $0.0248 per second** on the APIMart route. A tarefa concluída informa o valor exato no campo `cost`; uma tarefa com falha é reembolsada.

**How do I get a key?**

Use the [Get an API key](https://go.apimart.ai/k-1ca2fb) link — $1 minimum top-up, no plan required.

<!-- related-repos:auto -->
## Related repositories

- **Same model, this language** — the other half of this pair: [minimax-hailuo-2-3-fast-prompts-pt](https://github.com/n0v1if2hp4z/minimax-hailuo-2-3-fast-prompts-pt)
- **Same model, other languages** — 10 more language builds: English [minimax-hailuo-2-3-fast-api](https://github.com/sutsndi4k8j/minimax-hailuo-2-3-fast-api) · 中文 [minimax-hailuo-2-3-fast-api-cn](https://github.com/ggucz6z3g9v3w/minimax-hailuo-2-3-fast-api-cn) · Deutsch [minimax-hailuo-2-3-fast-api-de](https://github.com/lqzftxffi/minimax-hailuo-2-3-fast-api-de) · Español [minimax-hailuo-2-3-fast-api-es](https://github.com/g06zqtyckwv13h/minimax-hailuo-2-3-fast-api-es) · Français [minimax-hailuo-2-3-fast-api-fr](https://github.com/x7iiodjlo8vxk8/minimax-hailuo-2-3-fast-api-fr) · Relay/gateway `minimax-hailuo-2-3-fast-api-gateway` · Bahasa `minimax-hailuo-2-3-fast-api-id` · 日本語 [minimax-hailuo-2-3-fast-api-ja](https://github.com/ee8d3uqmm/minimax-hailuo-2-3-fast-api-ja) · 한국어 [minimax-hailuo-2-3-fast-api-ko](https://github.com/j20pyxt/minimax-hailuo-2-3-fast-api-ko) · Русский `minimax-hailuo-2-3-fast-api-ru`
- **More models in this language** — [midjourney-api-pt](https://github.com/l-ca0/midjourney-api-pt) · [gemini-2-5-flash-image-preview-api-pt](https://github.com/ycx8l0/gemini-2-5-flash-image-preview-api-pt) · [nano-banana-api-pt](https://github.com/erujt71i1lx/nano-banana-api-pt) · [gemini-3-1-flash-image-preview-api-pt](https://github.com/hutjwux0nt9h/gemini-3-1-flash-image-preview-api-pt) · [nano-banana-2-api-pt](https://github.com/ydkd8kdkl8n/nano-banana-2-api-pt) · [gemini-3-pro-image-preview-api-pt](https://github.com/qss2d-66qb2n7/gemini-3-pro-image-preview-api-pt)
- **Topic hubs** — every build of this model, all languages: [minimax-hailuo-2-3-fast](https://github.com/topics/minimax-hailuo-2-3-fast) · [minimax-hailuo-2-3-fast-api](https://github.com/topics/minimax-hailuo-2-3-fast-api)

This repository is one build in a cross-linked set of API guides for the same model family; each language build links back to the others.
<!-- /related-repos:auto -->

## Attributed links (how this repository is measured)

| Purpose | Attributed link | Target |
| --- | --- | --- |
| Model page | <https://go.apimart.ai/k-937e23> | `apimart.ai/pt/model/minimax-hailuo-2-3-fast` |
| Live pricing | <https://go.apimart.ai/k-4eaecf> | `apimart.ai/pt/pricing` |
| Get an API key | <https://go.apimart.ai/k-1ca2fb> | `apimart.ai/pt/keys` |

Outbound APIMart links are minted through the promo link API; hand-made tracking parameters are rejected by
`tools/check_links.py` in CI.

## Disclosure

MiniMax Hailuo 2.3 Fast is a third-party model served through APIMart; this repository documents how to call it and publishes
model ids and prices, and does not claim official status. Model names, prices and documentation belong to their
respective owners.

## License

MIT — see [LICENSE](LICENSE).
