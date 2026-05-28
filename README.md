# Fio de Sonho — Site

Site vitrine (página única) para o crochê artesanal **Fio de Sonho**.
Estático, leve e sem dependências de servidor. Toda venda acontece via **WhatsApp**.

## Estrutura

```
site/
├── index.html              # o site inteiro (HTML + CSS + JS num arquivo só)
└── assets/img/
    ├── logo.png            # fada + nome (fundo transparente) — usada no hero
    ├── logo-divulgacao.png # logo completa refinada (post pro Instagram)
    ├── favicon.png         # ícone da aba do navegador
    ├── produto-coelho.png  # lembrancinhas
    ├── produto-chocalho.png# chocalhos de bebê
    ├── produto-dragao.png  # amigurumis
    └── produto-bolsa.png   # bolsas/acessórios
```

## Como editar o essencial

Abra `index.html` num editor de texto:

- **Número do WhatsApp**: linha com `const WHATSAPP = "5534999182686";`
  (formato internacional, só dígitos: 55 + DDD + número)
- **@ do Instagram**: procure por `fio_de_sonho` e troque se mudar o handle.
- **Textos das peças**: cada peça está num bloco `<article class="card">`.
- **Trocar foto de uma peça**: substitua o arquivo em `assets/img/` mantendo o mesmo nome,
  ou aponte o `src` da `<img>` para o novo arquivo.

## Deploy no Cloudflare Pages (gratuito)

### Opção 1 — arrastar e soltar (mais rápido)
1. Crie conta em https://dash.cloudflare.com
2. Workers & Pages → Create → Pages → **Upload assets**
3. Arraste a pasta `site/` inteira.
4. Pronto: sai um endereço `*.pages.dev`. Depois é só apontar o domínio próprio.

### Opção 2 — via Git (recomendado, integra com seu GitLab)
1. Suba a pasta `site/` num repositório.
2. No Cloudflare Pages → Connect to Git → selecione o repo.
3. Build settings: **sem build command**, output directory = `/` (ou a pasta do site).
4. Cada `git push` na branch principal publica automaticamente.

> Cloudflare Pages não conecta direto no GitLab self-hosted. Caminho prático:
> espelhar (mirror) o repo do GitLab para GitHub e conectar o Pages ao GitHub,
> **ou** usar a action `cloudflare/pages-action` num CI que roda `wrangler pages deploy`.

## Domínio próprio
Comprar algo como `fiodesonho.com.br` (registro.br) deixa muito mais profissional.
No Cloudflare Pages → Custom domains → adicionar e seguir o apontamento de DNS.

## Observações técnicas
- Fontes vêm do Google Fonts (Parisienne, Cormorant Garamond, Montserrat) via `<link>`.
  Precisa de internet do lado do visitante (sempre tem). Para 100% offline,
  baixar os .ttf e servir localmente com `@font-face`.
- Não há backend, banco nem cookies. Performance e privacidade altas por padrão.
- Os botões de WhatsApp usam `wa.me` com mensagem pré-preenchida por contexto.
