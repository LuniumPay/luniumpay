<p align="center"><strong>LuniumPay · Developers</strong><br/>Pix ⇄ stablecoin no Brasil, por API. Chave de produção em uma chamada, sem aprovação humana.</p>

---

## Comece em 60 segundos

```bash
# 1. chave de teste (o e-mail recebe o manual uma única vez)
curl -X POST https://api.luniumpay.com/keys/sandbox -H 'Content-Type: application/json' -d '{"email":"voce@empresa.com"}'

# 2. cobrança Pix com entrega em USDT (sandbox: dinheiro fictício)
curl -X POST https://api.luniumpay.com/cashin/charge -H "X-API-Key: $LUNIUM_API_KEY" -H 'Content-Type: application/json' \
  -d '{"amount_cents":10000,"payer_tax_number":"12345678909","destino":"cripto","asset":"USDT","chain":"polygon","payout_address":"0xSUA_CARTEIRA","external_id":"pedido-1","sandbox_scenario":"success"}'

# 3. chave de produção, na hora
curl -X POST https://api.luniumpay.com/keys -H 'Content-Type: application/json' -d '{"name":"Minha Empresa","email":"voce@empresa.com"}'
```

Mesmo contrato no sandbox e em produção: troque só a variável de ambiente.

## Programa com IA? Instale a skill

```bash
npx skills add LuniumPay/lunium-agent-skills
```

Funciona em Claude Code, Cursor, Codex, Gemini CLI e qualquer agente que leia o padrão Agent Skills. Depois peça: *"quero receber Pix e cair em USDT na minha carteira"*. O agente cria a chave, escreve o backend na sua stack, mostra o QR da API, configura o webhook e prova tudo no sandbox. Página: https://docs.luniumpay.com/skill

## Repositórios

| Repositório | O que é |
|---|---|
| [lunium-agent-skills](https://github.com/LuniumPay/lunium-agent-skills) | 7 skills para agentes de código: receber Pix em USDT ou saldo, custódia, webhooks, pagar Pix com cripto, carteira USDT, verificar Pix. Receitas Next.js, Express, FastAPI, Supabase; scripts de sandbox. |
| [lunium-examples](https://github.com/LuniumPay/lunium-examples) | Exemplos executáveis em Python e Node, coleção Postman, agentes de exemplo. |

## O que a API faz

| Produto | Em uma linha | Endpoints |
|---|---|---|
| **Receber Pix → cripto** | Cliente paga Pix; você recebe USDT/USDC (ou outro ativo do catálogo) na carteira | `POST /cashin/charge` destino `cripto` |
| **Receber Pix → saldo** | Saldo em reais sem carteira, subcontas por cliente, saque em cripto quando quiser | destino `saldo`, `/saldo/*`, `/saldo/sacar-cripto` |
| **Pagar Pix com saldo** | Pix para fornecedores e clientes com o saldo recebido | `POST /payouts` |
| **Cripto → Pix** | Cliente envia USDT; o Pix sai com comprovante do Banco Central | `POST /cash-outs` |
| **Carteira USDT** | Saldo em stablecoin e Pix pago com ele, por chave ou copia e cola | `/carteira-usdt/*` |
| **Verificar Pix** | Prova pública de liquidação pelo E2E, sem chave | `GET /v1/verificar/{e2e}` |

## Fonte de verdade

- OpenAPI 3.1: https://docs.luniumpay.com/openapi.json
- Contrato para máquina (LLMs): https://docs.luniumpay.com/llms.txt
- Jornadas estruturadas: https://docs.luniumpay.com/integration.json
- Sandbox e cenários de falha: https://docs.luniumpay.com/sandbox
- Manual: https://docs.luniumpay.com/manual · Começar: https://docs.luniumpay.com/comecar
- MCP: `https://api.luniumpay.com/mcp` (descritor em `/.well-known/mcp.json`)
- Status: https://docs.luniumpay.com/status

## Regras que valem para todo integrador

1. Dinheiro é estado, não HTTP 200: libere com `status=paid` **e** `settlement_status=sent`.
2. `external_id` em toda criação, gravado antes de chamar; retry com o mesmo id e o mesmo corpo.
3. Cash-in e saldo em centavos inteiros; cash-out e carteira USDT em decimais string.
4. Webhook: corpo cru, HMAC `X-Lunium-Signature`, `event_id` único, 2xx rápido, status relido antes de liberar.
5. Segredos só em variável de ambiente do servidor.
6. Taxas, mínimos e rotas lidos em tempo de execução. Nada gravado no código.

## Suporte

contato@luniumpay.com · [WhatsApp](https://wa.me/27722944340) · [Lunium Partners no Telegram](https://t.me/+FerOZMRRP_g5MDk5) (comunidade oficial de integradores, recomendada).

---

<sub><strong>EN</strong> · Brazilian Pix ↔ stablecoin API. Production key in one call, no human approval. Same contract in sandbox and production. Coding agents: <code>npx skills add LuniumPay/lunium-agent-skills</code>. Source of truth: <a href="https://docs.luniumpay.com/openapi.json">openapi.json</a> · <a href="https://docs.luniumpay.com/llms.txt">llms.txt</a>.</sub>
