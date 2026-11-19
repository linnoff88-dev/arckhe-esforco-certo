# esforÃ§o certo

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


[![esforÃ§o certo](guia/assets/banner.jpg)](https://inematds.github.io/esforco-certo/guia/)

**ðŸ‡§ðŸ‡· [PortuguÃªs](README.md) Â· ðŸ‡ºðŸ‡¸ [English](README.en.md) Â· ðŸ‡ªðŸ‡¸ [EspaÃ±ol](README.es.md)**

## O que Ã©

O esforÃ§o certo Ã© um kit gratuito para quem usa o Claude Code em projetos e robÃ´s. Ele lÃª as configuraÃ§Ãµes, os agentes e os scripts do seu projeto e mostra em que modelo (Fable, Opus, Sonnet, Haiku) e em que esforÃ§o cada coisa roda â€” esforÃ§o Ã© quanto o modelo pensa antes de responder, de `low` a `max`. Ele aponta o que estÃ¡ caro sem precisar, traz uma regra pronta para colar no seu CLAUDE.md e um teste que roda o mesmo trabalho em dois esforÃ§os, pela sua assinatura, para vocÃª comparar. Precisa de Python 3 e, para o teste, do Claude Code; a auditoria nÃ£o usa internet nem API.

## ðŸ“– Guia de uso

Guia completo (landing + passo a passo): **https://inematds.github.io/esforco-certo/guia/**

## Por quÃª

Na pÃ¡gina de lanÃ§amento do Claude Fable 5.2 (09/11/2026), a Anthropic recomenda comeÃ§ar no **Opus 5.5** para a maioria do
cÃ³digo e do trabalho do dia a dia, e subir para o Fable sÃ³ no trabalho mais difÃ­cil. No grÃ¡fico de custo por tarefa do
teste FrontierCode 2.0 da mesma pÃ¡gina:

| CombinaÃ§Ã£o | Nota | Custo por tarefa (lido no grÃ¡fico) |
|---|---|---|
| Fable 5.2 Â· high | 45,3% | ~US$ 7 |
| Opus 5.5 Â· melhor | 45,5% | ~US$ 13 |
| Fable 5.2 Â· xhigh | 49,1% | ~US$ 15 |
| Fable 5.2 Â· max | ~45,7% | ~US$ 45 |

O Max fez menos que o Xhigh e custou cerca de 3Ã—. Em outro teste (desenho de hardware) o melhor veio no Max â€” por isso a
regra Ã© **Max nÃ£o Ã© padrÃ£o; meÃ§a**. E a tabela de notas Ã© sempre no esforÃ§o mais alto, enquanto o Claude Code vem no
medium por padrÃ£o.

## ComeÃ§o rÃ¡pido

```bash
git clone https://github.com/inematds/esforco-certo.git
cd esforco-certo
python3 auditar.py ~/meu-projeto --home          # quem roda em qual modelo/esforÃ§o, e o que estÃ¡ caro
cat politica/CLAUDE-esforco.md >> ~/meu-projeto/CLAUDE.md
./ab.sh "Revise src/ e liste os 5 riscos mais graves" --dir ~/meu-projeto   # mesmo trabalho, 3 combinaÃ§Ãµes
```

## ConteÃºdo

| Arquivo | O que faz |
|---|---|
| `auditar.py` | LÃª `.claude/settings*.json` (`model`, `effortLevel`, `modelSettings.<modelo>.effortLevel`), agentes, skills, comandos, scripts, timers e cÃ³digo que chama a API. Alertas: `MAX`, `PADRAO_ALTO`, `FABLE_PADRAO`. OpÃ§Ãµes: `--home`, `--json`, `--estrito` (CI), `--anonimo`, `--docs`. |
| `ab.sh` | Roda o mesmo pedido com `claude -p` em 2+ combinaÃ§Ãµes `modelo:esforÃ§o` (padrÃ£o `opus:high fable:medium fable:high`). SÃ³ leitura por padrÃ£o; `--editar` usa uma git worktree do Ãºltimo commit por combinaÃ§Ã£o (commite antes; ela vem sem `node_modules`/`.venv`) e `--checar "<cmd>"` roda o seu teste â€” instale as dependÃªncias nele, ex.: `--checar "npm ci && npm test"`. Quadro com tempo, tokens, custo equivalente e o modelo que rodou de verdade. Usa a assinatura (tira `ANTHROPIC_API_KEY` do ambiente). |
| `politica/CLAUDE-esforco.md` | Bloco pronto para o CLAUDE.md/AGENTS.md. |
| `politica/comparar-modelos.md` | Protocolo para comparar dois modelos sem se enganar: separa capacidade, interpretaÃ§Ã£o e esforÃ§o em 3 experimentos (mesmo orÃ§amento, melhor esforÃ§o, mesmo resultado) + ficha de avaliaÃ§Ã£o Ã s cegas. |
| `agentes/` | `dia-a-dia` (Opus, medium), `trabalho-longo` (Fable, high), `mecanico` (Haiku, low). |
| `resets.md` | Roteiro para gastar os resets do Fable (promoÃ§Ã£o atÃ© 16/11/2026) num trabalho longo. |
| `exemplos/` | RelatÃ³rio do projeto de teste e o resumo de uma mÃ¡quina de produÃ§Ã£o. |
| `tests/` | 19 testes sem rede: `python3 -m unittest discover tests`. |

## O processo, do inÃ­cio ao fim

| # | Passo | Comando | Quem |
|---|---|---|---|
| 1 | Baixar o kit | `git clone https://github.com/inematds/esforco-certo.git` | ðŸ§  vocÃª |
| 2 | Auditar o projeto | `python3 auditar.py <pasta> --home` | âš™ï¸ script |
| 3 | Decidir o padrÃ£o com os alertas | ler o relatÃ³rio; mudar `model`/`effortLevel` Ã  mÃ£o | ðŸ§  vocÃª |
| 4 | Colar a regra e os agentes | `cat politica/CLAUDE-esforco.md >> CLAUDE.md` Â· `cp agentes/*.md .claude/agents/` + `git commit` | ðŸ§  vocÃª |
| 5 | Medir no seu trabalho (para comparar modelos: os 3 experimentos de `politica/comparar-modelos.md`) | `./ab.sh "<tarefa>" --dir <pasta> [--editar --checar "<teste>"]` | ðŸ¤– `claude -p` |
| 6 | Travar no CI | `cp auditar.py <projeto>/tools/` Â· no CI: `python3 tools/auditar.py . --estrito` | âš™ï¸ script |
| 7 | Gastar os resets num trabalho longo | seguir `resets.md` | ðŸ§  vocÃª + ðŸ¤– |

## Limites

- A auditoria acha o que estÃ¡ escrito; nÃ£o sabe o que um script decide em tempo de execuÃ§Ã£o (modelo vindo de variÃ¡vel aparece como `variavel`).
- O custo do `ab.sh` Ã© o que o Claude Code calcula pela tabela da API; na assinatura vocÃª paga em limite, nÃ£o em dÃ³lar.
- NÃºmeros do Fable 5.2 e do Opus 5.5: testes da prÃ³pria Anthropic, lidos em 09/11/2026.

Projetos e cursos gratuitos: https://inema.club

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>