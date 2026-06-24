# Apresentações Eleven — Skill para Claude Code

Skill do [Claude Code](https://claude.com/claude-code) que cria **apresentações institucionais
da Eleven Proteção Veicular** como slide deck **HTML autocontido**: um único arquivo, zero
dependências externas, no design system oficial da marca (fontes embutidas, logo embutido,
navegação por teclado/swipe). Abre direto no navegador — sem build, sem PowerPoint.

Depois de instalada, é só pedir ao seu Claude Code:

> "Crie uma apresentação da Eleven sobre \[tema\]"

e ele monta o deck no padrão da marca usando o template incluído aqui.

---

## Instalação (1 comando)

Cole no terminal:

```bash
git clone https://github.com/alexpaivadev/apresentacoes-eleven.git ~/.claude/skills/apresentacoes-eleven
```

Reinicie o Claude Code (ou abra uma nova sessão). Pronto — a skill `apresentacoes-eleven`
fica disponível automaticamente.

**Não tem git ou prefere que o Claude faça?** Abra o Claude Code e cole:

> Instale a skill deste repositório no meu Claude Code:
> https://github.com/alexpaivadev/apresentacoes-eleven
> Clone para `~/.claude/skills/apresentacoes-eleven` e confirme que ficou disponível.

### Atualizar

```bash
cd ~/.claude/skills/apresentacoes-eleven && git pull
```

### Verificar se instalou

No Claude Code, rode `/help` ou simplesmente peça uma apresentação da Eleven — a skill é
acionada sozinha pela descrição. Os arquivos devem estar em
`~/.claude/skills/apresentacoes-eleven/`.

---

## O que vem na skill

```
apresentacoes-eleven/
├── SKILL.md                    # instruções que o Claude segue para montar o deck
├── assets/
│   ├── template.html           # o template autocontido (duplicar e editar)
│   ├── logo-colorida.png       # logo oficial Eleven (fundo claro)
│   └── logo-branca.png         # logo oficial Eleven (fundo escuro)
└── reference/
    └── design-system.md        # tokens de cor, arquétipos de slide, donut, navegação
```

## Design system (resumo)

- **Cores:** azul institucional `#3C679E`, verde institucional `#5B9559`, vermelho de alerta
  `#C75D6E`, mais gradientes da marca.
- **8 arquétipos de slide prontos:** capa, divisória de seção, KPIs, gráfico donut, comparativo
  A × B, lista numerada/passos, blocos win/lose, fechamento.
- **Navegação inclusa:** setas, números `1–9`, swipe, tela cheia (`F`), barra de progresso e
  contador automáticos.
- **Exporta PDF:** Chrome → Imprimir → Salvar como PDF (paisagem). Use `?still` na URL para o
  print sem animação.

Detalhes completos em [`reference/design-system.md`](reference/design-system.md).

## Como usar depois de instalada

1. Peça ao Claude Code uma apresentação da Eleven sobre o tema desejado.
2. Forneça os números, a mensagem central e o público.
3. O Claude duplica o template, preenche os arquétipos certos e entrega um `.html` pronto.
4. Abra no navegador. Exporte PDF se precisar.

---

> Padrão oficial de decks da Eleven Proteção Veicular. **Não use Marp nem PowerPoint** para
> apresentações de cliente — este template é o padrão.
