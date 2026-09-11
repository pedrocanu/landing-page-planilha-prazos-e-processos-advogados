# Controle de Processos e Prazos — Landing Page

Landing page de vendas em HTML/CSS/JS puro (arquivo único, sem frameworks) para o
infoproduto **"Controle de Processos e Prazos"** — planilha de Excel/Google Sheets
para advogados autônomos e pequenos escritórios controlarem prazos processuais.

## Arquivos

- [index.html](index.html) — a landing page completa (HTML + CSS + JS inline, sem dependências externas além das fontes do Google Fonts).

## Antes de publicar — troque estas variáveis

Tudo o que precisa de ajuste fica no topo do `<head>` de [index.html](index.html), num bloco `<script>` comentado:

```js
window.CHECKOUT_URL = "https://pay.kiwify.com.br/Uxjv9X5"; // link real da Kiwify (já preenchido)
window.PRICE_DISPLAY = "R$ 27";      // preço exibido
window.PRICE_OLD_DISPLAY = "R$ 47";  // preço "de" (âncora), opcional
window.FB_PIXEL_ID = "SEU_PIXEL_ID_AQUI"; // ID do Meta Pixel — troque pelo seu
```

O Pixel do Meta (Facebook Ads) está com o código base pronto (`PageView` +
`InitiateCheckout` disparado ao clicar em qualquer botão de compra), mas só funciona
de verdade depois que você substituir `SEU_PIXEL_ID_AQUI` pelo ID numérico do seu
pixel (Gerenciador de Eventos → seu Pixel → ID). Ele aparece em **dois** lugares no
arquivo: na variável `window.FB_PIXEL_ID` e no `<noscript>` logo abaixo — troque nos
dois.

O botão principal de compra tem `id="checkout-btn"`; todos os botões de compra
(inclusive esse) usam a classe `.btn-buy-link`, que recebe o link da Kiwify via JS
a partir de `CHECKOUT_URL`.

## Rodar localmente

É um HTML estático — basta abrir o arquivo direto no navegador, ou servir com
qualquer servidor simples:

```bash
python -m http.server 8000
# depois abra http://localhost:8000
```

## Publicar no GitHub Pages

1. Suba este repositório para o GitHub (veja abaixo).
2. Em **Settings → Pages**, selecione a branch `main` e a pasta raiz (`/`).
3. A página fica disponível em `https://<seu-usuario>.github.io/<repo>/`.

```bash
git remote add origin https://github.com/<seu-usuario>/<seu-repo>.git
git branch -M main
git push -u origin main
```

## Decisões de design

Identidade visual sóbria/editorial — preto, branco e creme, tipografia serifada
(Fraunces) para títulos e monoespaçada (IBM Plex Mono) para números de processo e
preços, remetendo a papelada de cartório/autos processuais. As "capturas de tela"
da planilha (Painel, Processos, Prazos) são recriadas em HTML/CSS — inclusive com
abas clicáveis — em vez de imagens estáticas, para carregar rápido, funcionar em
qualquer resolução e servir como prova real do produto (a lógica de cores
VENCIDO/HOJE/ESTA SEMANA/OK é a mesma da planilha de verdade).
