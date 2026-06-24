---
name: apresentacoes-eleven
description: Cria apresentações institucionais da Eleven Proteção Veicular como slide deck HTML autocontido (um único arquivo, zero dependências externas) no design system oficial da marca. Use quando o usuário pedir uma apresentação, deck, slides ou pitch da Eleven, ou quando precisar transformar uma análise/relatório em slides no padrão visual da Eleven. NÃO use Marp nem PowerPoint para decks de cliente — este é o padrão.
---

# Apresentações Eleven

Gera decks **HTML autocontidos** (um arquivo só, sem build, abre direto no navegador) no
design system da Eleven Proteção Veicular: fontes Sora + Inter embutidas em base64, logo
embutido, motor de navegação em JS puro (teclado, swipe, barra de progresso, contador).

## Quando usar esta skill

- O usuário pede uma "apresentação", "deck", "slides" ou "pitch" da Eleven.
- Precisa transformar uma análise, número ou relatório em slides apresentáveis.
- Qualquer entrega visual institucional da Eleven para cliente, liderança ou equipe.

Para rascunho interno descartável, Marp serve. Para **qualquer coisa que alguém vai ver**,
use este template.

## Como criar um deck (workflow)

1. **Duplique o template.** Ele está em `assets/template.html` (dentro desta skill).
   Copie para onde o deck final deve morar e renomeie de forma descritiva, ex.:
   `Eleven-NomeDoTema.html`. Se o usuário tiver a estrutura de workspace, o destino padrão
   é `~/Documents/Workspace/Apresentações/`; senão, salve no diretório de trabalho atual.

2. **Entenda o conteúdo antes de editar.** Pergunte ou colete: tema, público, números-chave,
   a mensagem central e o call-to-action. Um deck bom tem uma tese, não só slides.

3. **Edite os slides.** Cada arquétipo no template está marcado com um comentário
   `<!-- ===== SLIDE: <nome> — <como usar> ===== -->`. Troque os placeholders `{{...}}`
   pelo conteúdo real. Duplique ou remova blocos (`.kpi`, `.cmp-row`, `.vrow`) conforme a
   quantidade de itens. Remova arquétipos que o deck não precisa — não deixe placeholder cru.

4. **Respeite o design system.** Use só os tokens de cor da marca e os arquétipos prontos.
   Não invente cores nem layouts fora do padrão. Detalhes em `reference/design-system.md`.

5. **Não há build.** É HTML standalone — basta abrir no navegador (duplo clique). Para gerar
   PDF de **todos os slides**, abra a URL com `?print` (monta uma página por slide e abre o
   diálogo de impressão); para um slide congelado sem animação, use `?still`.

6. **Audite antes de entregar.** Cada slide é uma caixa fixa de 1280×720 que **corta o overflow
   sem aviso**. Abra o deck com `?audit`: slide que estoura ganha borda vermelha + badge
   `▲ +Npx`. Respeite o orçamento de altura (lista numerada = 5 itens, tabela = 7 linhas…; ver
   `reference/design-system.md`) — se não couber, **divida em dois slides**, não encolha a fonte.

## Modos de apresentação (motor já pronto)

O template traz, além da navegação básica: **`O`** overview (grade de miniaturas), **`H`**
ocultar/revelar o slide atual, **`P`** modo apresentador (2ª janela com atual + próximo + notas

- timer). Ocultar slides também via `data-skip`, `?skip=4,7` ou `?only=1,2,5`. Notas do
  apresentador via `<aside class="notes">` (some do deck). A navbar tem botões clicáveis para
  tudo isso, que **somem em tela cheia**. Detalhes em `reference/design-system.md`.

## Regras de ouro

- **Autocontido sempre.** Zero refs externas: fontes e imagens vão embutidas em base64.
  Se inserir um logo novo ou imagem, converta para base64 e cole inline — nunca referencie
  arquivo externo, ou o deck quebra na máquina de outra pessoa.
- **Logos oficiais.** Use os de `assets/`: `logo-colorida.png` (fundo claro) e
  `logo-branca.png` (fundo escuro). O template já traz o logo embutido na capa/rodapé.
- **Evite emoji** nos slides — fora do design system e vira imagem externa em alguns renders.
- **Um número por vez.** KPIs são para destaque; não empilhe 8 métricas num slide. Corte.
- **Português do Brasil**, tom direto e institucional.

## Números animados (count-up)

Para um número que sobe na entrada do slide:
`<span class="count" data-to="4150" data-format="int">0</span>` (inteiro) ou `data-dec="1"`
(1 casa decimal). O `<i>` ao lado vira sufixo (`%`, `M`).

## Referência completa

`reference/design-system.md` — tokens de cor, tabela de arquétipos de slide, como ajustar o
gráfico donut (offsets do SVG) e navegação.
