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

Reescrita focada em conversão (redesign a partir de análise de fricções):

1. **Hero**: headline testada em anúncio ("Vermelho é prazo vencido. Quantos
   você tem agora?"), preço ancorado (de/por), selo "pagamento único", CTA,
   selo de garantia de 7 dias e selos de confiança (compra segura, entrega
   por e-mail, nota fiscal).
2. **A dor**: 3 bullets curtos, sem parágrafo longo.
3. **Demonstração 1**: seletor de abas com os 3 prints reais (Painel,
   Processos, Prazos) + bullets resumindo as 4 abas.
4. **Demonstração 2**: seção isolada, em destaque (fundo escuro), focada só
   na régua de cores VENCIDO/HOJE/ESTA SEMANA/OK — o diferencial do produto.
5. **Comparação de preço**: sistema jurídico por assinatura vs. pagamento
   único, com checklist do que a pessoa recebe.
6. **FAQ**: ordenada da objeção mais comum pra mais rara. A pergunta sobre
   mensalidade não está mais aqui: virou selo de texto fixo abaixo do preço.
7. **Oferta final**: preço ancorado + CTA + garantia.
8. **Rodapé** + **barra fixa no rodapé da tela** (aparece ao rolar além do
   hero, com preço e CTA sempre visíveis).

Sem nenhuma seção de depoimento, review ou citação de cliente, por decisão
deliberada.

## Decisões de design

Identidade visual preto/branco/cinza com amarelo (`#f6c445`) como cor de
alerta e destaque, a mesma lógica de cores da própria planilha (navbar preta,
banner de atenção amarelo). A prova visual do produto são os 3 prints reais em
[assets/](assets/) — não mockups recriados.
