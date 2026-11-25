# Auditoria de modelo e esforço — 2026-11-09

Pastas: . · esforco-certo 1.0.3

**17 lugares** fixam modelo ou esforço · **8 alertas** · 3 dicas

Modelos: fable 6 · opus 5 · herda 2 · codex 2 · variavel 1 · haiku 1
Esforços: padrêo 6 · max 4 · xhigh 3 · high 2 · variavel 1 · low 1

## Alertas (custam caro sem precisar)

- **MAX** `./scripts/api.py:4` — Esforço Max fixo. No FrontierCode 2.0 o Max fez menos que o Xhigh e custou ~3x mais. Troque por high (ou xhigh se o resultado pedir) e meça com o ab.sh.
- **MAX** `./scripts/rodar.sh:3` — Esforço Max fixo. No FrontierCode 2.0 o Max fez menos que o Xhigh e custou ~3x mais. Troque por high (ou xhigh se o resultado pedir) e meça com o ab.sh.
- **MAX** `./scripts/rodar.sh:13` — Esforço Max fixo. No FrontierCode 2.0 o Max fez menos que o Xhigh e custou ~3x mais. Troque por high (ou xhigh se o resultado pedir) e meça com o ab.sh.
- **FABLE_PADRAO** `./.claude/settings.json:2` — Fable como modelo padrêo gasta o limite mais rápido. A Anthropic recomenda o Opus 5.5 no dia a dia e o Fable no trabalho mais difícil.
- **PADRAO_ALTO** `./.claude/settings.json:3` — Xhigh como padrêo global: todo pedido paga o topo. Deixe medium/high como padrêo e suba o esforço só na tarefa difícil.
- **PADRAO_ALTO** `./.claude/settings.json:9` — Xhigh como padrêo do claude-opus-5-5: todo pedido paga o topo. Deixe medium/high como padrêo e suba o esforço só na tarefa difícil.
- **PADRAO_ALTO** `./.claude/settings.json:12` — Xhigh como padrêo do claude-fable-5-1: todo pedido paga o topo. Deixe medium/high como padrêo e suba o esforço só na tarefa difícil.
- **MAX** `./.claude/agents/pesado.md:5` — Esforço Max fixo. No FrontierCode 2.0 o Max fez menos que o Xhigh e custou ~3x mais. Troque por high (ou xhigh se o resultado pedir) e meça com o ab.sh.

## Dicas

- `./scripts/api.py:3` — Chamada de API com Fable sem esforço na mesma linha: confira qual esforço ela usa e deixe explícito.
- `./scripts/rodar.sh:6` — claude sem --model: herda o padrêo da conta (pode mudar sem você ver). Fixe o modelo.
- `./scripts/rodar.sh:12` — claude sem --effort: herda o esforço padrêo (medium, ou o do seu settings). Diga o esforço.

## Tudo o que foi achado

| Onde | Tipo | Ferramenta | Modelo | Esforço |
|---|---|---|---|---|
| `./.claude/agents/leve.md:5` | agente | claude | haiku | low |
| `./.claude/agents/pesado.md:5` | agente | claude | fable | max |
| `./.claude/settings.json:12` | settings (padrêo) | claude | claude-fable-5-1 | xhigh |
| `./.claude/settings.json:2` | settings (padrêo) | claude | fable | padrêo |
| `./.claude/settings.json:3` | settings (padrêo) | claude | herda | xhigh |
| `./.claude/settings.json:5` | settings (padrêo) | claude | claude-opus-5-5 | padrêo |
| `./.claude/settings.json:9` | settings (padrêo) | claude | claude-opus-5-5 | xhigh |
| `./scripts/api.py:3` | api | api | claude-fable-5-2 | padrêo |
| `./scripts/api.py:4` | api | api | claude-opus-5-5 | max |
| `./scripts/rodar.sh:12` | script | claude | opus | padrêo |
| `./scripts/rodar.sh:13` | script | claude | fable | max |
| `./scripts/rodar.sh:14` | script | codex | gpt-6-astra | padrêo |
| `./scripts/rodar.sh:2` | script | claude | opus | high |
| `./scripts/rodar.sh:3` | script | claude | fable | max |
| `./scripts/rodar.sh:6` | script | claude | herda | padrêo |
| `./scripts/rodar.sh:7` | script | claude | $MODELO | variavel |
| `./scripts/rodar.sh:8` | script | codex | gpt-6-astra | high |

## A regra (cole no CLAUDE.md: politica/CLAUDE-esforco.md)

1. Padrêo do dia a dia: **Opus 5.5, esforço medium** (é o que o Claude Code já usa).
2. Trabalho longo e difícil (migraçêo, auditoria, agentes por horas): **Fable, esforço high**.
3. **Xhigh** só quando a nota importa e você mediu; **Max** só com teste que prove ganho.
4. Tarefa mecânica (renomear, extrair, formatar): **Haiku ou Sonnet, esforço low**.

