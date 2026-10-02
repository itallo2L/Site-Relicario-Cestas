# Relicário Cestas — site

Site estático (HTML + CSS + JS, sem build). Abra com um servidor local:

```bash
python -m http.server 5173
```

## Estrutura

```
index.html                 página (seções: header, hero, destaques, depoimentos, vitrine, rodapé)
css/styles.css             tokens de cor/tema + componentes (mobile-first)
js/main.js                 tema claro/escuro, menu, WhatsApp, carrossel, animações
assets/img/placeholders/   imagens provisórias (substituir)
```

## Cores e temas

- Paleta oficial em `:root` (`--brand-*`) no topo de `css/styles.css`: verde-sálvia e creme, tirados do logo. Os nomes das variáveis vieram do site anterior; os comentários ao lado dizem a cor atual.
- Tema claro e escuro em `[data-theme="light"]` / `[data-theme="dark"]` (tokens `--color-*`, `--btn-*`, `--wa-*`).
- Tema inicial segue o sistema do visitante; a escolha manual fica salva no navegador.

## WhatsApp

Número central em `js/main.js` → `CONFIG.whatsapp`. Cada link com `data-wa="mensagem"` abre o WhatsApp com a mensagem já preenchida.

## Logo

- `assets/img/logo.webp`: logo oficial (fundo creme, 443×443). Uma versão maior (900×900 ou mais) deixaria o banner do início mais nítido.
- `favicon.ico`, `assets/img/favicon-32.png`, `assets/img/apple-touch-icon.png`: galho do logo em creme sobre círculo verde-sálvia (legível em tamanho pequeno).

## Árvore de fundo

- `assets/img/arvore-clara.webp` / `arvore-escura.webp`: silhueta de árvore (fundo transparente), em verde-oliva no tema claro e sálvia clara no escuro.
- Aplicada como fundo fixo em `body::before` no CSS; imagem e intensidade vêm dos tokens `--tree-image` e `--tree-opacity` de cada tema.
- Não usa `mask-image` de propósito: o Chrome bloqueia máscaras ao abrir o site direto do arquivo (`file://`).

## Produtos

- 11 cestas em 3 categorias no `#vitrine` do `index.html`: Cestas, Bandejas e Boxes. As 3 primeiras dos destaques ficam em `#destaques`.
- Fotos em `assets/img/produtos/` (WebP 600×800, proporção 3:4, nome igual ao do produto: `cesta-dengo.webp`…).
- Sem preço no site: o valor é combinado pelo WhatsApp. Cada botão "Encomendar" abre a conversa com "Olá! Gostaria de encomendar: <nome>."
- Os itens de cada cesta ficam em `<details class="items">` ("O que vem"), que abre e fecha sem JavaScript.
- Para mais de uma foto num produto, use `class="product-card__media gallery" data-gallery` com um `.gallery__track` contendo as `<img>`. Bolinhas e setas são criadas pelo `js/main.js`.
- Ao alterar CSS/JS, aumente o `?v=` nos links do `index.html` para evitar cache antigo.

## Depoimentos (carrossel)

A seção `#depoimentos` é um carrossel: o 1º slide mostra a presença no Instagram ("+4 mil seguidores" e temas que mais encantam); os seguintes são mensagens de clientes no WhatsApp, recriadas em HTML como balões do app (texto real: nítido em qualquer tela e lido pelo Google).
Para adicionar um depoimento, copie um bloco `<figure class="testimonials__slide testimonial testimonial--chat">` dentro de `.testimonials__track` e troque os balões: `chat__msg--in` é a mensagem do cliente (branca), `chat__msg--out` é a resposta da Relicário (verde) e `chat__msg--tail` vai só na primeira mensagem de cada sequência. Transcreva o texto como foi escrito. As bolinhas são geradas automaticamente.
Atualize o número de seguidores no `index.html` quando mudar.

## Contato

Atendimento exclusivo pelo WhatsApp (sem endereço físico no site). Instagram: [@relicariocestas](https://www.instagram.com/relicariocestas/).

As imagens usam `object-fit: cover` e `aspect-ratio` fixo: basta trocar o `src` (e o `alt`) que o layout não quebra.
