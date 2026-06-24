# Design System — Apresentações Eleven

Referência de apoio à skill. O motor (CSS + JS) já está pronto dentro de
`assets/template.html`; aqui está o mapa para editar com segurança.

## Tokens de cor da marca

```
--azul:   #3C679E      (azul institucional)
--verde:  #5B9559      (verde institucional)
--grad:       linear-gradient(100deg, #3C679E → #4A7E7E → #5B9559)
--grad-soft:  linear-gradient(100deg, #5A86BC → #79B86A)
--grad-dark:  linear-gradient(135deg, #102A42 → #1B3A5B → #27583F)  (fundos escuros)
vermelho de alerta (perda):  #C75D6E
```

Não introduza cores fora desta paleta. Para "bom" use verde, para "ruim/perda" use o
vermelho de alerta, para neutro/institucional o azul.

## Arquétipos de slide disponíveis

Cada um está marcado no template com `<!-- ===== SLIDE: ... ===== -->`.

| Arquétipo                   | Classe base                         | Quando usar                                                      |
| --------------------------- | ----------------------------------- | ---------------------------------------------------------------- |
| **Capa**                    | `.slide--cover`                     | Abertura: título, subtítulo, chips, rodapé.                      |
| **Divisória de seção**      | `.slide--dark`                      | Separar blocos do deck — só kicker + título grande.              |
| **Conteúdo com KPIs**       | `.slide--light` + `.kpi-row`        | 3–4 números-chave com rótulo.                                    |
| **Gráfico donut**           | `.slide--light` + `.donut`          | Proporção/participação entre 2–3 fatias.                         |
| **Comparativo**             | `.slide--light` + `.cmp-rows`       | Tabela A × B linha a linha.                                      |
| **Lista numerada / passos** | `.slide--dark` + `.vnum`            | Recomendações, etapas, veredito. Até 5 itens; 6 → `.verd.tight`. |
| **Blocos win/lose**         | `.slide--light` + `.frota win/lose` | Contrastar um resultado bom (verde) e um ruim (vermelho).        |
| **Fechamento**              | `.slide--dark`                      | Mensagem final + assinatura.                                     |

Duplique blocos internos (`.kpi`, `.cmp-row`, `.vrow`) para mais itens; remova para menos.
Apague arquétipos inteiros que o deck não usa.

## Donut — como mudar os valores

O SVG usa `stroke-dasharray: 439.8` (circunferência de `r=70`). Para uma fatia:
`stroke-dashoffset = 439.8 × (1 − fração)`. Ex.: 70% preenchido → offset `131.9`.
A animação dispara via regra `.is-active .panel-donut .d-*` no `<style>` — ajuste os
offsets lá. Há ainda a variante de **fatia única** `.donut2 .d-fatia` (vermelho) já incluída.

## Navegação e atalhos (já pronta no JS)

| Tecla                        | Ação                                                             |
| ---------------------------- | ---------------------------------------------------------------- |
| `← →` · espaço · PageUp/Down | Slide anterior / próximo                                         |
| `1`–`9`                      | Pular para o N-ésimo slide **visível**                           |
| `Home` / `End`               | Primeiro / último slide visível                                  |
| `F`                          | Tela cheia                                                       |
| `O`                          | **Overview** — grade de miniaturas (Esc ou `O` fecha)            |
| `H`                          | **Oculta/revela** o slide atual (persiste na sessão)             |
| `P`                          | **Apresentador** — 2ª janela com atual + próximo + notas + timer |

Também: clique nos pontos da navbar, swipe e scroll. Contador, pontos e barra de progresso são
gerados automaticamente das `<section class="slide">` — basta adicionar/remover slides.

**Botões na navbar** (à direita do contador): overview (grade), ocultar este slide (olho),
apresentador (monitor) e exportar PDF (impressora) — os mesmos atalhos, clicáveis. **Somem
automaticamente em tela cheia** (`F`), deixando a barra só com navegação. Os atalhos de
teclado continuam valendo em tela cheia.

## Ocultar / pular slides

Para apresentar um subconjunto sem apagar nada do arquivo:

- **No markup:** `<section class="slide ..." data-skip>` nasce oculto.
- **Pela URL:** `?skip=4,7` oculta esses; `?only=1,2,5` mostra **só** esses (1-based;
  `only` precede `skip`).
- **Ao vivo:** tecla `H` (ou o botão de olho) oculta/revela o slide atual; no overview, o botão
  de cada miniatura faz o mesmo. O estado fica salvo em `localStorage` por arquivo (sobrevive ao
  reload). Slides ocultos somem da navegação, dos pontos e do contador — mas continuam no `?audit`.

## Notas do apresentador + modo apresentador (`P`)

Adicione `<aside class="notes">…</aside>` dentro de qualquer `<section class="slide">`. Ele
**nunca** aparece no deck. A tecla `P` (ou o botão de monitor) abre uma 2ª janela com o slide
atual, o próximo, as notas do atual, um relógio e um cronômetro. Navegar em qualquer janela
sincroniza a outra. _(Permita pop-ups; em `file://` use o mesmo navegador para as duas.)_

## Orçamento de altura + auditoria de overflow

Cada `.slide` é uma **caixa fixa de 1280×720** e o palco tem `overflow:hidden` — conteúdo que
estoura **some sem aviso** (não rola). Área útil ~590px (descontando o padding de 64px topo/base).
Pense em cada slide como um pôster, não como página que rola.

**Orçamento seguro por arquétipo:** lista numerada `.vrow` = 5 itens (6 → `.verd.tight`; 7+ →
quebrar em 2 slides); tabela = 7 linhas; cartões 2×2/3 = até 4 bullets cada; KPIs = 4 cartões.
Mais que isso → **dividir o slide**, não encolher fonte.

**Antes de entregar, audite:** abra o deck com `?audit` na URL — qualquer slide que estoure os
720px ganha borda vermelha + badge `▲ +Npx`. Sem badge = tudo dentro da caixa.

## Exportar / imprimir todos os slides

- **PDF de todos os slides:** abra com `?print` (ou clique no botão de impressora) — todos os
  slides (respeitando os ocultos) viram páginas em paisagem, sem animação, e o diálogo de
  impressão abre sozinho. "Salvar como PDF".
- **Um slide congelado:** `?still` (estado final sem animação) — útil para screenshot.

## Acessibilidade

Slides inativos recebem `aria-hidden`; há `:focus-visible` nos controles; e
`prefers-reduced-motion` desliga animações e count-up automaticamente (mesmo efeito do `?still`).

## Logos

`assets/logo-colorida.png` (fundo claro) e `assets/logo-branca.png` (fundo escuro). Ao inserir
um logo num slide novo, **embuta em base64** — nunca referencie o arquivo externo, ou o deck
deixa de ser autocontido.
