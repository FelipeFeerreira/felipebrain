# AGENTS.md — felipebrain-pages (site publicado)

Este repositório é **saída de build**, não fonte. Quem edita aqui edita o que o próximo
build apaga. A fonte é `~/Documents/felipebrain-site` (Quartz) + o vault `~/Documents/FelipeBrain`.

## Padrão obrigatório

Seguir `30-Projetos/portfolio/padrao-de-vitrine.md` no vault (`~/Documents/FelipeBrain/30-Projetos/portfolio/padrao-de-vitrine.md`):
escala mínima (corpo 16 px, h1 48 desktop / 30 celular, alvo de toque 44 px, contraste 4,5:1),
uma cor de ação, imagem de verdade, e aceite = print a 390 e 1280 + medidas tiradas do CSS publicado.

## Referência visual deste site

- **Site**: https://felipefeerreira.github.io/felipebrain/ — referência é a própria home atual.
- O que copiar: home de leitura (título grande, um parágrafo curto, lista de notas), busca no
  topo da barra lateral, largura de conteúdo ~750 px no desktop, sidebar com árvore de pastas.
- O que não copiar: nada de hero de tela cheia, caixa alta com tracking, header que não fixa.

## Paleta e fontes reais (as do CSS publicado, 23/11)

| Token | Claro | Escuro | Uso |
|---|---|---|---|
| `--light` / fundo | `#fcfbf9` | `#161618` | fundo da página |
| `--dark` / texto | `#3e3a35` | `#e8e6e3` | corpo |
| `--darkgray` / título | `#201e1c` | — | título do artigo |
| `--gray` | `#6b655e` (5,59:1) | `#a8a49c` | secundário, rótulo da busca |

Fontes: `Inter` (corpo), `Fraunces` (títulos), `JetBrains Mono` (código).
Cor de ação: **nenhuma** hoje — este site não tem CTA; se entrar botão, ele usa uma única cor (`--acao`).

Ajustes de escala/contraste/alvo vivem em `~/Documents/felipebrain-site/quartz/styles/custom.scss`
(blocos comentados com o defeito e o número antes/depois). Não editar os `component-*.css` daqui.

## Build

```bash
cd ~/Documents/felipebrain-site
node quartz/bootstrap-cli.mjs build     # gera public/ (13–22 html, canonical em todas)
# ./publicar.sh também funciona; em 23/11 ele quebrou no npx quartz — o node direto é o caminho seguro
```

Cópia para este repo (só com OK do Felipe; é publicação):

```bash
cd ~/Documents/felipebrain-site && ./deploy.sh
# = publicar.sh + touch .nojekyll + rsync -a --delete --exclude .git public/ ../felipebrain-pages/
```

## Print e medição

```bash
cd /tmp/opencode/preview && python3 -m http.server 8099    # serve preview/felipebrain = public/
# com Playwright MCP: browser_resize 390x844 ou 1280x900 + browser_take_screenshot
# ou: npx playwright screenshot --viewport-size=390,844 http://localhost:8099/felipebrain/index.html antes-390.png
```

Medir sempre no build local (`localhost`) **e** conferir o publicado; os números do publicado podem
estar atrás (publicar é decisão do Felipe).

Checagem mínima aceita:

```js
document.documentElement.scrollWidth - innerWidth   // 0 = sem overflow lateral
[...document.querySelectorAll('footer a,.sidebar a')].filter(a => a.getBoundingClientRect().height < 44 && a.getBoundingClientRect().height > 0).length // 0
```

## Regras

- Não commitar `main` nem publicar sem o OK do Felipe.
- Não apagar página sem conferir se alguém linka para ela (a pasta `40-IA/` maiúscula foi rename; redirects foram criados de propósito).
- Notas do vault são de outros donos: `90-sistema/` aqui é espelho, não fonte.
