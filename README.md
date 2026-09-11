# Controle de Processos e Prazos — Landing Page

Landing page de vendas em HTML/CSS/JS puro (arquivo único, sem frameworks) para o
infoproduto **"Controle de Processos e Prazos"** — planilha de Excel/Google Sheets
para advogados autônomos e pequenos escritórios controlarem prazos processuais.

## Arquivos

- [index.html](index.html) — a landing page completa (HTML + CSS + JS inline, sem dependências externas além das fontes do Google Fonts).
- [assets/](assets/) — os 3 prints reais da planilha (`painel.png`, `processos.png`, `prazos.png`) usados como prova visual na página.

## Antes de publicar — troque estas variáveis

Tudo o que precisa de ajuste fica no topo do `<head>` de [index.html](index.html), num bloco `<script>` comentado:

```js
window.CHECKOUT_URL = "https://pay.kiwify.com.br/Uxjv9X5"; // link real da Kiwify (já preenchido)
window.PRICE_DISPLAY = "R$ 19,90";   // preço exibido
window.PRICE_OLD_DISPLAY = "R$ 37";  // preço "de" (âncora), opcional
```

Logo abaixo fica o **Meta Pixel Code** (código oficial gerado pelo Gerenciador de
Eventos do Facebook), já com o ID real `1048049571165967` disparando `PageView` no
carregamento. Todos os botões de compra também disparam `InitiateCheckout` ao serem
clicados (isso é feito à parte, no script do final do arquivo). Se um dia precisar
trocar de pixel, o ID aparece em **dois** lugares dentro do bloco `<!-- Meta Pixel
Code -->`: na chamada `fbq('init', ...)` e no `<noscript>` logo abaixo — troque nos
dois.

O botão principal de compra tem `id="checkout-btn"`; todos os botões de compra
(inclusive esse) usam a classe `.btn-buy-link`, que recebe o link da Kiwify via JS
a partir de `CHECKOUT_URL`.

## Rodar localmente

É um HTML estático — a forma mais simples é abrir [index.html](index.html) direto
no navegador (duplo clique). Para servir por `http://localhost`, use o que tiver
instalado:

```bash
# com Python
python -m http.server 8000

# ou com Node.js
npx serve .
```

## Subir para o GitHub

Este repositório já está inicializado e com todos os commits prontos na branch
`main`. Falta só criar o repositório vazio no GitHub e apontar para ele:

```bash
git remote add origin https://github.com/<seu-usuario>/<seu-repo>.git
git push -u origin main
```

## Publicar no GitHub Pages

1. Depois do push, vá em **Settings → Pages** no repositório.
2. Em "Source", selecione a branch `main` e a pasta raiz (`/`).
3. A página fica disponível em `https://<seu-usuario>.github.io/<repo>/`.

## Decisões de design

Identidade visual minimalista clara: fundo cinza-claro/off-white, tipografia
Inter, botões pill pretos, cards com borda fina. A prova visual do produto são
os 3 prints reais em [assets/](assets/) (não mockups recriados) — no hero eles
aparecem num seletor de abas clicável (Painel/Processos/Prazos), e reaparecem
nas seções "Como funciona" e "Todos os processos, num lugar só".
