# Portfólio — Julia Brazolim

Site gerado com [Hugo](https://gohugo.io).

**O que mudou em relação ao HTML puro:** nav, footer e CTA agora são componentes reutilizáveis (partials). Cada case novo é um arquivo `.md` — você escreve só o conteúdo, o Hugo monta o HTML completo na hora do deploy.

---

## Conceitos rápidos (para quem vem do front-end)

| Hugo | Equivalente front-end |
|---|---|
| `layouts/` | Templates HTML com variáveis |
| `partials/` | Componentes reutilizáveis (como includes) |
| `content/*.md` | Os "dados" de cada página |
| `static/` | A pasta `public/` — CSS, imagens, fontes |
| `front matter` | As variáveis da página (bloco `---` no topo do `.md`) |
| `hugo server` | Servidor de desenvolvimento com live reload |
| `hugo --minify` | Build de produção — gera a pasta `public/` |

O front matter funciona como variáveis que o template lê. Exemplo:

```markdown
---
title: "Meu Projeto"   ← vira {{ .Title }} no template
cover: "img/capa.png"  ← vira {{ .Params.cover }} no template
---
```

---

## Rodar localmente

Com o Hugo instalado, dentro da pasta do projeto:

```bash
hugo server
```

Acesse `http://localhost:1313`. O site atualiza ao salvar qualquer arquivo.

> **Hugo não está instalado?**
> No Windows: `winget install Hugo.Hugo.Extended`

---

## Publicar alterações

Todo push para `master` dispara o deploy automático via GitHub Actions (~1 min).

```bash
git add .
git commit -m "descrição da alteração"
git push origin main:master
```

---

## Criar um novo case

1. Crie `content/cases/nome-do-case.md`
2. Preencha o front matter e o texto
3. Coloque as imagens em `static/img/nome-do-case/`
4. Faça push

O case aparece automaticamente na listagem e no carrossel da home.

### Modelo completo

```markdown
---
title: "Nome do Projeto"
subtitle: "Descrição curta · Cliente · Ano"
overline: "Product Designer"
year: "2024"
cover: "img/nome-do-case/capa.png"

tags:
  - UI Design
  - UX Research
  - Prototipagem

highlights:
  - icon: "🎯"
    title: "Título do destaque"
    text: "Texto explicativo."
  - icon: "✨"
    title: "Outro destaque"
    text: "Mais um texto."

steps_title: "Título da seção de processo"
steps:
  - number: "1."
    image: "img/nome-do-case/passo1.png"
    title: "Título do passo"
    text: "Descrição do que foi feito."
  - number: "2."
    title: "Próximo passo (sem imagem)"
    text: "Só omita o campo image."

result:
  - "Primeiro parágrafo do resultado."
  - "Segundo parágrafo, se necessário."

gallery:
  - wide: true
    image: "img/nome-do-case/destaque.png"
    alt: "Descrição"
  - image: "img/nome-do-case/detalhe1.png"
    alt: "Descrição"
  - image: "img/nome-do-case/detalhe2.png"
    alt: "Descrição"
---

## Título da introdução

Texto de apresentação do case. Markdown normal: **negrito**, *itálico*, parágrafos separados por linha em branco.
```

### Campos opcionais — o que acontece se omitir

| Campo | Se omitir |
|---|---|
| `cover` | Sem imagem no carrossel da home |
| `highlights` | Seção "Por que este projeto?" não aparece |
| `steps` | Seção de processo não aparece |
| `result` | Seção de resultado não aparece |
| `gallery` | Grade de imagens não aparece |
| `overline` | Usa "Product Designer" como padrão |

---

## Adicionar imagens

1. Coloque em `static/img/nome-do-case/`
2. Referencie **sem barra inicial**: `"img/nome-do-case/arquivo.png"`

> ⚠️ Não use `/img/...` (com barra no início) — quebra os caminhos no deploy.

**Tamanhos recomendados:**
- Capa (`cover`): proporção 16:9, ~1200px de largura
- Imagens de processo: ~600px
- Galeria wide: ~1400px | galeria normal: ~700px

---

## Editar conteúdo existente

| O que editar | Arquivo |
|---|---|
| Texto e dados de um case | `content/cases/nome-do-case.md` |
| Texto do hero da home | `layouts/index.html` — linha com "Oi oi oi" |
| Cards de serviços | `layouts/index.html` — seção `<!-- SERVICES -->` |
| Links das redes sociais | `layouts/partials/footer-home.html` e `footer-case.html` |
| CTA da home | `layouts/partials/cta-home.html` |
| CTA dos cases | `layouts/partials/cta-case.html` |
| CSS da home | `static/style.css` e `static/home-extra.css` |
| CSS dos cases | `static/cases.css` |

---

## Estrutura de pastas

```
content/
└── cases/
    └── chafe.md        ← um arquivo por case

static/
├── img/                ← todas as imagens do site
├── style.css           ← CSS da home (inclui animação SVG)
├── home-extra.css      ← reset, variáveis CSS, hero
└── cases.css           ← estilos das páginas de case

layouts/
├── index.html                  ← template da home
├── cases/
│   ├── list.html               ← página de listagem do portfólio
│   └── single.html             ← template de cada case
└── partials/
    ├── hero-svg.html           ← ilustração animada da Julinha
    ├── nav-home.html           ← nav dark (home)
    ├── nav-case.html           ← nav light (cases)
    ├── footer-home.html        ← footer dark (home)
    ├── footer-case.html        ← footer light (cases)
    ├── cta-home.html           ← CTA da home
    └── cta-case.html           ← CTA dos cases
```
