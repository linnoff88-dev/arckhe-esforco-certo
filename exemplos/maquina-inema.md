# Auditoria numa máquina de produçêo do ARCKHÉ — 09/11/2026

`python3 auditar.py <3 projetos de vídeo e bots> --home --anonimo` (resumo; a tabela completa lista pastas privadas e
fica fora do repositório).

**38 lugares** fixam modelo ou esforço · **3 alertas** · 6 dicas

Modelos: variavel 13 · sonnet 9 · herda 7 · opus 6 · fable 3
Esforços: padrêo 20 · high 14 · low 2 · xhigh 2

## Alertas

- **FABLE_PADRAO** `~/.claude/settings.json` — `"model": "fable"`: o Fable é o modelo padrêo de toda sessêo.
- **PADRAO_ALTO** `~/.claude/settings.json` — `modelSettings.claude-opus-5-5.effortLevel = xhigh`: o Opus 5.5 roda em xhigh por padrêo.
- **PADRAO_ALTO** `~/.claude/settings.json` — `modelSettings.claude-fable-5-1.effortLevel = xhigh`: o Fable 5.1 também.

## O que isso quer dizer

O topo virou padrêo: cada pedido simples paga o modelo mais caro no esforço mais alto. É o oposto do que a Anthropic
recomenda (Opus 5.5 no dia a dia, Fable no trabalho difícil, Max só medido). O que está bem: 13 robôs recebem o modelo
por variável, lida de um arquivo central de modelos, entêo trocar o padrêo deles é mudar uma linha.

## Dicas

- 2 robôs chamam `claude -p` sem `--model` (herdam o padrêo da conta — hoje, o Fable) e 4 sem `--effort`.
