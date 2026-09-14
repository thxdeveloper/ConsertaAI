# 🔧 Conserta Aí

**Manutenção caseira sem gastar com técnico.**

App web que usa IA para diagnosticar problemas domésticos e te dar o passo a passo para resolver em casa — com lista de ferramentas, peças e vídeos tutoriais do YouTube embutidos.

---

## ✨ Funcionalidades

- **Diagnóstico por IA** — descreva o problema ou mande uma foto
- **Categorias** — Automotivo, Elétrica, Hidráulica, Eletrodomésticos, Móveis, Eletrônicos
- **Nível de risco** — aviso claro quando o reparo é perigoso e deve ser feito por profissional
- **Passo a passo** — instruções didáticas para quem nunca fez o reparo antes
- **Player de vídeo embutido** — assista tutoriais do YouTube direto no app, sem sair da página
- **Vídeos da comunidade** — usuários podem votar e indicar vídeos que funcionaram
- **Busca de vídeos via Tavily** — depois do diagnóstico, o app busca tutoriais reais no YouTube usando a API da Tavily (free tier, sem custo por busca na Anthropic)

---

## 🚀 Como usar

### Opção 1 — GitHub Pages (recomendado)

1. Faça fork ou clone este repositório
2. Vá em **Settings → Pages**
3. Em **Source**, selecione `main` / `root`
4. Aguarde o deploy — o app estará em `https://seu-usuario.github.io/conserta-ai/`

### Opção 2 — Qualquer servidor estático

Basta servir os arquivos com qualquer servidor HTTP (Netlify, Vercel, Cloudflare Pages, etc.).

> ⚠️ **Não abre como arquivo local (`file://`)** — o navegador bloqueia chamadas à API e embeds do YouTube por segurança. Sempre use um servidor HTTP.

---

## 🔑 API Keys

O app usa duas APIs diretamente do browser:

1. **[Anthropic](https://console.anthropic.com/)** — gera o diagnóstico (texto/foto → JSON estruturado). Procure no `index.html` por `SUA_CHAVE_AQUI` (dentro de `const API_KEY`) e cole sua chave.
2. **[Tavily](https://app.tavily.com)** — busca os vídeos reais no YouTube depois do diagnóstico (free tier: ~1.000 buscas/mês por conta, sem cartão de crédito). Procure por `TAVILY_API_KEYS` no `index.html` e cole uma ou mais chaves na lista — se a primeira estourar a cota, expirar ou falhar, o app tenta automaticamente a próxima da lista antes de desistir (e, se nenhuma funcionar, o diagnóstico continua normalmente, só sem vídeos).

> ⚠️ **Atenção:** as duas chaves ficam visíveis para qualquer um que inspecionar o código, por estarem no frontend. Para uso público, crie um backend (ex: Cloudflare Worker) que repasse as chamadas sem expor as chaves.

---

## 🗃️ Banco de dados

Os votos e sugestões de vídeo da comunidade são salvos no **storage persistente dos Artifacts da Anthropic** (via `window.storage`), que funciona automaticamente no ambiente Claude.ai.

Se você hospedar fora do Claude.ai, esse storage não estará disponível — os votos simplesmente não serão salvos (o resto do app funciona normalmente). Para persistência externa, substitua as chamadas `window.storage` por qualquer solução como Firebase, Supabase ou um JSON no próprio GitHub (via GitHub API).

---

## 🛠️ Stack

- HTML + CSS + JavaScript puro (zero dependências, zero build)
- [Anthropic Messages API](https://docs.anthropic.com/en/api/messages) com `claude-sonnet-4-6` (diagnóstico)
- [Tavily Search API](https://tavily.com) (busca de vídeos reais no YouTube)
- YouTube embed via `youtube-nocookie.com`
- Google Fonts (Space Grotesk + Inter)

---

## 📁 Estrutura

```
conserta-ai/
├── index.html   # app completo (single file)
└── README.md
```

---

## 📋 Roadmap de ideias

- [ ] Histórico local dos últimos diagnósticos
- [ ] Estimativa de custo das peças
- [ ] Compartilhar diagnóstico via WhatsApp
- [ ] Modo PWA (instalável no celular)
- [ ] Backend proxy para proteger a API key
- [ ] Avaliação do vídeo assistido direto no modal

---

## ⚖️ Aviso

O diagnóstico é gerado por IA e serve como orientação inicial. Em caso de dúvida sobre segurança, procure sempre um profissional qualificado. O app nunca incentiva reparos que envolvam risco de vida.
