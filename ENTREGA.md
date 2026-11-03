# Kapon — pacote de entrega do site

Site institucional do Kapon (app de compras locais), feito para ser entregue a um desenvolvedor
ou publicado em qualquer hospedagem.

---

## 1. O que enviar

| Arquivo | Para que serve |
|---|---|
| `public/kapon-site.html` | **Site completo em um único arquivo.** Abre em qualquer navegador, sem instalação, sem build. É o arquivo principal da entrega. |
| `ENTREGA.md` | Este guia: seções, cores, fontes, textos e pendências. |
| Pasta `src/` | Versão em React + Tailwind (é o código que roda nesta plataforma). |

O `kapon-site.html` é a referência visual fiel: quem for portar o site para WordPress, Webflow,
Next.js ou o sistema próprio da empresa pode copiar estrutura e estilos dali.

---

## 2. Estrutura da página (ordem das seções)

1. **Cabeçalho fixo** — wordmark `kapon.` à esquerda, 4 links de navegação, botão "Baixar o app".
   Ganha fundo desfocado ao rolar a página.
2. **Hero** — título, subtítulo, dois botões (baixar / quero vender) e mockup do app
   (tela de mapa desenhada em CSS, não é imagem).
3. **Faixa rolante** — categorias de produtos em movimento contínuo.
4. **Como funciona** — 3 passos numerados.
5. **Para quem compra** — foto + 4 benefícios.
6. **Para quem vende** — seção em fundo claro (contraste), foto da loja + 4 benefícios + CTA.
7. **Perguntas frequentes** — 6 perguntas em acordeão.
8. **CTA final** — bloco vermelho de conversão para a Play Store.
9. **Rodapé** — wordmark, 2 colunas de links, contato, copyright.

Âncoras internas: `#top`, `#como-funciona`, `#comprar`, `#vender`, `#duvidas`.

---

## 3. Identidade visual

### Cores

| Token | Valor | Uso |
|---|---|---|
| `--bg` | `#0A0A0B` | Fundo principal (quase preto) |
| `--fg` | `#EDEAE3` | Texto principal (branco quente) |
| `--muted` | `#A3A09A` | Texto secundário |
| `--primary` | `#ED1C24` | Vermelho Kapon — botões, destaques, palavras-chave |
| `--line` | `rgba(255,255,255,.10)` | Bordas e divisórias |
| `--sand` | `#F7F4F0` | Fundo da seção "Para quem vende" |
| `--ink` | `#12100F` | Texto sobre o fundo claro |

Contraste: texto principal sobre fundo escuro passa de 15:1 e o branco sobre o vermelho
fica em ~4.6:1 — acima do mínimo AA para texto grande. Em textos pequenos sobre o vermelho,
usar `rgba(255,255,255,.8)` ou maior.

### Tipografia

- **Display / títulos:** `Bricolage Grotesque` (600–800), `letter-spacing` entre `-0.04em` e `-0.055em`.
- **Texto:** `Inter` (300–600).
- **Corpo:** 18px base, entrelinha 1.6.
- **H1:** `clamp(2.6rem, 6.4vw, 5rem)` · **H2:** `clamp(2rem, 4.2vw, 3.4rem)`.

### Medidas

- Largura máxima do conteúdo: **1152px**, margem lateral de 24px.
- Raio: 16px (cards) / 24–32px (blocos e fotos) / 999px (botões e pílulas).
- Respiro vertical das seções: 96px no celular, 128px no desktop.
- Grade: 12 colunas; nos blocos de duas colunas, `1.08fr / 0.92fr` (hero) e `1fr / 1fr` (conteúdo).

---

## 4. Textos (copy)

Todo o texto está em português e já dentro do HTML. Pontos de atenção:

- **Título:** "O que você precisa já está aqui do lado."
- **Subtítulo:** "O Kapon mostra no mapa os produtos que estão sendo vendidos perto de você.
  Encontre, converse com o vendedor e combine a compra — tudo pelo app."
- **Link do app (usado 6 vezes):**
  `https://play.google.com/store/apps/details?id=com.kapon.app&hl=pt-BR`

Para trocar textos, use o próprio HTML como fonte da verdade.

---

## 5. Imagens

Três fotos, hospedadas em `media.base44.com` (URLs públicas, já dentro do HTML):

| Onde aparece | URL |
|---|---|
| Fundo do hero | `.../d01410db9_generated_49374e55.png` |
| Seção "Para quem compra" | `.../becd55169_generated_9b852761.png` |
| Seção "Para quem vende" | `.../577f088fb_generated_bae6e9f4.png` |

Recomendação: baixar essas fotos e servir do próprio servidor, em WebP, com largura
máxima de 1600px. O mockup do celular **não é imagem** — é HTML/CSS, então escala sem perder
qualidade e pode ser trocado por um print real do app quando quiserem.

---

## 6. Pendências antes de publicar

1. **Contato real** — o site atual não divulga e-mail/telefone; o rodapé está com
   "atendimento pelo app". Trocar por e-mail, WhatsApp e CNPJ da empresa.
2. **Política de privacidade e termos de uso** — páginas obrigatórias para app publicado em loja;
   os links ainda não existem no rodapé.
3. **Favicon e imagem de compartilhamento** (og:image) — usar o "K" vermelho da marca.
4. **Botão da App Store** — hoje o app é só Android; se lançarem para iOS, adicionar o segundo botão.
5. **Domínio** — o site deve ir para `www.kapon.com.br` com HTTPS e redirecionar `kapon.com.br` → `www`.

---

## 7. Versão React (código da plataforma)

Se o desenvolvedor preferir trabalhar no código atual:

```
src/pages/Home.jsx                 → monta a página inteira
src/components/kapon/
  SiteHeader.jsx                   → cabeçalho fixo
  Hero.jsx                         → seção de abertura
  PhoneMockup.jsx / MapScreen.jsx  → mockup do celular
  CategoryMarquee.jsx              → faixa rolante
  HowItWorks.jsx                   → 3 passos
  ForBuyers.jsx                    → bloco de quem compra
  ForSellers.jsx                   → bloco de quem vende
  Faq.jsx                          → perguntas frequentes
  FinalCta.jsx                     → bloco vermelho final
  SiteFooter.jsx                   → rodapé
  PlayStoreButton.jsx              → botão + URL da Play Store (fonte única do link)
  Wordmark.jsx                     → logotipo em texto
src/index.css                      → tokens de cor e tipografia
tailwind.config.js                 → mapeamento dos tokens
```

Rodando localmente: `npm install` e `npm run dev`.

Para baixar o projeto inteiro como pasta/repositório: no topo do editor, em
**More actions → GitHub connection**, conecte a conta do GitHub e baixe o repositório em ZIP.