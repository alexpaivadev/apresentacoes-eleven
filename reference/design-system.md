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

| Arquétipo                   | Classe base                         | Quando usar                                               |
| --------------------------- | ----------------------------------- | --------------------------------------------------------- |
| **Capa**                    | `.slide--cover`                     | Abertura: título, subtítulo, chips, rodapé.               |
| **Divisória de seção**      | `.slide--dark`                      | Separar blocos do deck — só kicker + título grande.       |
| **Conteúdo com KPIs**       | `.slide--light` + `.kpi-row`        | 3–4 números-chave com rótulo.                             |
| **Gráfico donut**           | `.slide--light` + `.donut`          | Proporção/participação entre 2–3 fatias.                  |
| **Comparativo**             | `.slide--light` + `.cmp-rows`       | Tabela A × B linha a linha.                               |
| **Lista numerada / passos** | `.slide--dark` + `.vnum`            | Recomendações, etapas, veredito (1, 2, 3).                |
| **Blocos win/lose**         | `.slide--light` + `.frota win/lose` | Contrastar um resultado bom (verde) e um ruim (vermelho). |
| **Fechamento**              | `.slide--dark`                      | Mensagem final + assinatura.                              |

Duplique blocos internos (`.kpi`, `.cmp-row`, `.vrow`) para mais itens; remova para menos.
Apague arquétipos inteiros que o deck não usa.

## Donut — como mudar os valores

O SVG usa `stroke-dasharray: 439.8` (circunferência de `r=70`). Para uma fatia:
`stroke-dashoffset = 439.8 × (1 − fração)`. Ex.: 70% preenchido → offset `131.9`.
A animação dispara via regra `.is-active .panel-donut .d-*` no `<style>` — ajuste os
offsets lá. Há ainda a variante de **fatia única** `.donut2 .d-fatia` (vermelho) já incluída.

## Navegação (já pronta no JS)

Setas `← →` (ou espaço / PageUp-Down), teclas `1–9` para pular, `Home`/`End`, `F` tela cheia,
clique nos pontos da navbar, swipe e scroll. O contador, os pontos e a barra de progresso são
gerados automaticamente a partir das `<section class="slide">` — basta adicionar/remover slides.

## Exportar para PDF

Abrir no Chrome → Imprimir → "Salvar como PDF", layout **paisagem**. Para o estado final
sem animação (melhor pro print), abra a URL com `?still`.

## Logos

`assets/logo-colorida.png` (fundo claro) e `assets/logo-branca.png` (fundo escuro). Ao inserir
um logo num slide novo, **embuta em base64** — nunca referencie o arquivo externo, ou o deck
deixa de ser autocontido.
