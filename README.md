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
window.PRICE_DISPLAY = "R$ 19,90";    // preço exibido
window.PRICE_OLD_DISPLAY = "R$ 39,90"; // preço "de" (âncora de preço de lançamento)
```

Logo abaixo fica o **Meta Pixel Code** (código oficial gerado pelo Gerenciador de
Eventos do Facebook), já com o ID real `1048049571165967` disparando `PageView` no
carregamento. Todos os botões de compra também disparam `InitiateCheckout` ao serem
clicados (isso é feito à parte, no script do final do arquivo). Se um dia precisar
trocar de pixel, o ID aparece em **dois** lugares dentro do bloco `<!-- Meta Pixel
Code -->`: na chamada `fbq('init', ...)` e no `<noscript>` logo abaixo — troque nos
dois.

O botão principal de compra (no hero) tem `id="checkout-btn"`; os demais CTAs
(comparativo de preço, oferta final, barra fixa no rodapé) têm ids próprios só
pra referência. Todos usam a classe `.btn-buy-link`, que recebe o link da
Kiwify via JS a partir de `CHECKOUT_URL`.

Se o preço de lançamento subir, troque só `PRICE_DISPLAY`/`PRICE_OLD_DISPLAY`:
o valor se propaga sozinho pro hero, pelo comparativo de preço, pela oferta
final e pela barra fixa.

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

## Estrutura da página

Layout minimalista monocromático (fundo cinza claro, cards brancos de borda
fina, botões pretos em pílula), no estilo de landing page de SaaS:

1. **Nav** fixa no topo: logo, links de seção e botão preto "Comprar".
2. **Hero**: título grande centralizado, subtítulo, dois CTAs (compra e "ver
   por dentro") e o print da aba Prazos numa moldura com fundo pontilhado.
3. **Visão geral**: grid de 6 cards (Processos, Prazos, Painel, Cor
   automática, Instruções, Excel e Sheets). Cada card tem texto à esquerda e
   um mini mockup em HTML à direita — nenhum é imagem.
4. **Três seções alternadas** (texto + painel de mockup): Prazos (a régua
   VENCIDO/HOJE/ESTA SEMANA/OK), Processos (fase de cada caso) e Painel
   (contadores do dia).
5. **Dentro da planilha**: bento com os 3 prints reais de [assets/](assets/).
6. **4 abas. Um arquivo só.**: 4 cards com checklist do que cada aba faz.
7. **Preço**: card central com preço ancorado, CTA preto e 4 selos, seguido
   do card de garantia de 7 dias.
8. **FAQ**: acordeão de linhas finas, com a primeira pergunta já aberta.
9. **CTA final** + **rodapé** em 4 colunas + **barra fixa** no rodapé da tela
   (aparece ao rolar além do hero, com preço e CTA sempre visíveis).

Sem nenhuma seção de depoimento, review ou citação de cliente, por decisão
deliberada.

## Decisões de design

Paleta monocromática: fundo `#f4f4f4`, superfícies brancas, linhas `#e7e7e7`,
preto `#0b0b0b` nos títulos e nos botões. Tipografia Inter com tracking
negativo (`-0.035em`) nos títulos. Cor só aparece dentro dos mockups, nas
situações de prazo (`--st-vencido`, `--st-hoje`, `--st-semana`, `--st-ok`),
que são as mesmas cores da planilha.

Os mockups das seções são HTML/CSS, não imagens — carregam junto com a página
e continuam nítidos em qualquer tela. A prova visual do produto continua sendo
os 3 prints reais em [assets/](assets/), agrupados na seção "Dentro da
planilha".

## Deploy

A página está publicada na Vercel, ligada a este repositório:
<https://landingpageplanilhaprazoseprocessos.vercel.app/>. Todo push na branch
`main` republica o site automaticamente.
