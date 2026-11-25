# esforêÂ§o certo

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


[![esforêÂ§o certo](guia/assets/banner.jpg)](https://linnoff88-dev.github.io/

**ê°Å¸â¡Â§ê°Å¸â¡Â· [PortuguêÂªs](README.md) êÂ· ê°Å¸â¡Âºê°Å¸â¡Â¸ [English](README.en.md) êÂ· ê°Å¸â¡Âªê°Å¸â¡Â¸ [EspaêÂ±ol](README.es.md)**

## O que êÂ©

O esforêÂ§o certo êÂ© um kit gratuito para quem usa o Claude Code em projetos e robêÂ´s. Ele lêÂª as configuraêÂ§êÂµes, os agentes e os scripts do seu projeto e mostra em que modelo (Fable, Opus, Sonnet, Haiku) e em que esforêÂ§o cada coisa roda ê¢â¬â esforêÂ§o êÂ© quanto o modelo pensa antes de responder, de `low` a `max`. Ele aponta o que estêÂ¡ caro sem precisar, traz uma regra pronta para colar no seu CLAUDE.md e um teste que roda o mesmo trabalho em dois esforêÂ§os, pela sua assinatura, para vocêÂª comparar. Precisa de Python 3 e, para o teste, do Claude Code; a auditoria nêÂ£o usa internet nem API.

## ê°Å¸ââ Guia de uso

Guia completo (landing + passo a passo): **https://linnoff88-dev.github.io/

## Por quêÂª

Na pêÂ¡gina de lanêÂ§amento do Claude Fable 5.2 (09/11/2026), a Anthropic recomenda comeêÂ§ar no **Opus 5.5** para a maioria do
cêÂ³digo e do trabalho do dia a dia, e subir para o Fable sêÂ³ no trabalho mais difêÂ­cil. No grêÂ¡fico de custo por tarefa do
teste FrontierCode 2.0 da mesma pêÂ¡gina:

| CombinaêÂ§êÂ£o | Nota | Custo por tarefa (lido no grêÂ¡fico) |
|---|---|---|
| Fable 5.2 êÂ· high | 45,3% | ~US$ 7 |
| Opus 5.5 êÂ· melhor | 45,5% | ~US$ 13 |
| Fable 5.2 êÂ· xhigh | 49,1% | ~US$ 15 |
| Fable 5.2 êÂ· max | ~45,7% | ~US$ 45 |

O Max fez menos que o Xhigh e custou cerca de 3êâ. Em outro teste (desenho de hardware) o melhor veio no Max ê¢â¬â por isso a
regra êÂ© **Max nêÂ£o êÂ© padrêÂ£o; meêÂ§a**. E a tabela de notas êÂ© sempre no esforêÂ§o mais alto, enquanto o Claude Code vem no
medium por padrêÂ£o.

## ComeêÂ§o rêÂ¡pido

```bash
git clone https://github.com/linnoff88-dev/esforco-certo.git
cd esforco-certo
python3 auditar.py ~/meu-projeto --home          # quem roda em qual modelo/esforêÂ§o, e o que estêÂ¡ caro
cat politica/CLAUDE-esforco.md >> ~/meu-projeto/CLAUDE.md
./ab.sh "Revise src/ e liste os 5 riscos mais graves" --dir ~/meu-projeto   # mesmo trabalho, 3 combinaêÂ§êÂµes
```

## ConteêÂºdo

| Arquivo | O que faz |
|---|---|
| `auditar.py` | LêÂª `.claude/settings*.json` (`model`, `effortLevel`, `modelSettings.<modelo>.effortLevel`), agentes, skills, comandos, scripts, timers e cêÂ³digo que chama a API. Alertas: `MAX`, `PADRAO_ALTO`, `FABLE_PADRAO`. OpêÂ§êÂµes: `--home`, `--json`, `--estrito` (CI), `--anonimo`, `--docs`. |
| `ab.sh` | Roda o mesmo pedido com `claude -p` em 2+ combinaêÂ§êÂµes `modelo:esforêÂ§o` (padrêÂ£o `opus:high fable:medium fable:high`). SêÂ³ leitura por padrêÂ£o; `--editar` usa uma git worktree do êÂºltimo commit por combinaêÂ§êÂ£o (commite antes; ela vem sem `node_modules`/`.venv`) e `--checar "<cmd>"` roda o seu teste ê¢â¬â instale as dependêÂªncias nele, ex.: `--checar "npm ci && npm test"`. Quadro com tempo, tokens, custo equivalente e o modelo que rodou de verdade. Usa a assinatura (tira `ANTHROPIC_API_KEY` do ambiente). |
| `politica/CLAUDE-esforco.md` | Bloco pronto para o CLAUDE.md/AGENTS.md. |
| `politica/comparar-modelos.md` | Protocolo para comparar dois modelos sem se enganar: separa capacidade, interpretaêÂ§êÂ£o e esforêÂ§o em 3 experimentos (mesmo orêÂ§amento, melhor esforêÂ§o, mesmo resultado) + ficha de avaliaêÂ§êÂ£o êÂ s cegas. |
| `agentes/` | `dia-a-dia` (Opus, medium), `trabalho-longo` (Fable, high), `mecanico` (Haiku, low). |
| `resets.md` | Roteiro para gastar os resets do Fable (promoêÂ§êÂ£o atêÂ© 16/11/2026) num trabalho longo. |
| `exemplos/` | RelatêÂ³rio do projeto de teste e o resumo de uma mêÂ¡quina de produêÂ§êÂ£o. |
| `tests/` | 19 testes sem rede: `python3 -m unittest discover tests`. |

## O processo, do inêÂ­cio ao fim

| # | Passo | Comando | Quem |
|---|---|---|---|
| 1 | Baixar o kit | `git clone https://github.com/linnoff88-dev/esforco-certo.git` | ê°Å¸Â§Â  vocêÂª |
| 2 | Auditar o projeto | `python3 auditar.py <pasta> --home` | ê¢Å¡â¢ê¯Â¸Â script |
| 3 | Decidir o padrêÂ£o com os alertas | ler o relatêÂ³rio; mudar `model`/`effortLevel` êÂ  mêÂ£o | ê°Å¸Â§Â  vocêÂª |
| 4 | Colar a regra e os agentes | `cat politica/CLAUDE-esforco.md >> CLAUDE.md` êÂ· `cp agentes/*.md .claude/agents/` + `git commit` | ê°Å¸Â§Â  vocêÂª |
| 5 | Medir no seu trabalho (para comparar modelos: os 3 experimentos de `politica/comparar-modelos.md`) | `./ab.sh "<tarefa>" --dir <pasta> [--editar --checar "<teste>"]` | ê°Å¸Â¤â `claude -p` |
| 6 | Travar no CI | `cp auditar.py <projeto>/tools/` êÂ· no CI: `python3 tools/auditar.py . --estrito` | ê¢Å¡â¢ê¯Â¸Â script |
| 7 | Gastar os resets num trabalho longo | seguir `resets.md` | ê°Å¸Â§Â  vocêÂª + ê°Å¸Â¤â |

## Limites

- A auditoria acha o que estêÂ¡ escrito; nêÂ£o sabe o que um script decide em tempo de execuêÂ§êÂ£o (modelo vindo de variêÂ¡vel aparece como `variavel`).
- O custo do `ab.sh` êÂ© o que o Claude Code calcula pela tabela da API; na assinatura vocêÂª paga em limite, nêÂ£o em dêÂ³lar.
- NêÂºmeros do Fable 5.2 e do Opus 5.5: testes da prêÂ³pria Anthropic, lidos em 09/11/2026.

Projetos e cursos gratuitos: https://ARCKHê AI

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>