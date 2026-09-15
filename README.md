# 🔧 Conserta Aí

**Manutenção caseira sem gastar com técnico.**

App web que usa IA para diagnosticar problemas domésticos e te dar o passo a passo para resolver em casa — com lista de ferramentas, peças e vídeos tutoriais do YouTube embutidos.

---

## ✨ Funcionalidades

- **Diagnóstico por IA** — descreva o problema ou mande uma foto
- **Categorias** — Automotivo, Elétrica, Hidráulica, Eletrodomésticos, Móveis, Eletrônicos
- **Nível de risco** — aviso claro quando o reparo é perigoso
- **Passo a passo** — instruções didáticas para leigos
- **Player de vídeo embutido** — tutoriais do YouTube direto no app
- **Vídeos da comunidade** — usuários votam nos vídeos que funcionaram
- **Sem API key da IA** — usa Puter.js, zero configuração obrigatória

---

## 🚀 Como usar

### GitHub Pages (recomendado)

1. Faça fork deste repositório
2. Vá em **Settings → Pages → Source: main / root**
3. Aguarde o deploy — estará em `https://seu-usuario.github.io/conserta-ai/`

> ⚠️ **Não abre como arquivo local (`file://`)** — hospede sempre num servidor HTTP.

---

## 🔑 APIs usadas

### IA — Puter.js (obrigatória, sem chave)

O diagnóstico usa [Puter.js](https://developer.puter.com) com **Claude Sonnet**. Na primeira vez que o usuário acessar, abre um popup rápido para criar ou entrar na conta Puter (gratuita). Depois fica salvo no navegador — transparente.

**Não tem nenhuma API key no código.** O custo de uso da IA fica na conta Puter do próprio usuário (modelo "User-Pays"). A cota gratuita do Puter cobre bem o uso casual.

### Busca de vídeos — Tavily (opcional, chave do usuário)

Para sugestões de vídeos do YouTube, o usuário pode configurar sua própria chave da [Tavily](https://app.tavily.com) (plano gratuito: 1.000 buscas/mês). O app funciona normalmente sem ela — só não sugere vídeos automaticamente.

A chave fica salva só no navegador do usuário (`localStorage`), nunca passa por servidor nenhum.

---

## 🗃️ Banco de dados / votos

Os votos da comunidade nos vídeos são salvos via `window.storage` (Puter.js) — compartilhado entre usuários logados no Puter. Funciona automaticamente sem nenhuma configuração extra.

---

## 🛠️ Stack

- HTML + CSS + JavaScript puro (zero dependências, zero build)
- [Puter.js](https://js.puter.com/v2/) — IA sem API key (Claude Sonnet via Puter)
- [Tavily API](https://tavily.com) — busca de vídeos (chave do usuário, opcional)
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

## 📋 Roadmap

- [ ] Histórico local dos últimos diagnósticos
- [ ] Estimativa de custo das peças
- [ ] Compartilhar diagnóstico via WhatsApp
- [ ] Modo PWA (instalável no celular)
- [ ] Avaliação do vídeo assistido direto no modal

---

## ⚖️ Aviso

Diagnóstico gerado por IA como orientação inicial. Em caso de dúvida sobre segurança, procure um profissional qualificado. O app nunca incentiva reparos que envolvam risco de vida.
