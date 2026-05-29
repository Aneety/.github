# workflow-estados

## Cabeçalho canônico

- Responsabilidade: `workflow-estados`
- Owner: Ricardo Malnati
- Repo destino: `Aneety/ai`
- Caminho canônico: `aneety-platform/apps/workflow-estados/...`
- Issue histórica migrada: [#8](https://github.com/Aneety/.github/issues/8)
- Prioridade atual: **alta**

## Status operacional por ciclo

| Ciclo | Status | Prioridade | Gate | Evidência | Bloqueio | Próxima ação |
| --- | --- | --- | --- | --- | --- | --- |
| `repositorio` | `bloqueado` | alta | `arquitetura` | [Issue histórica #8](https://github.com/Aneety/.github/issues/8); inspeção local 2026-05-29 confirmou apenas `aneety-platform/apps/.gitkeep` em `Aneety/ai`. | Falta raiz `aneety-platform/apps/workflow-estados/...` em `Aneety/ai`; checkout local também está sujo com `.playwright-mcp/`. | Limpar checkout local de `Aneety/ai` e criar raiz canônica da responsabilidade antes de avançar para `deploy`. |
| `deploy` | `triagem` | alta | `processo` | — | Aguardando ciclo `repositorio` ficar verde neste arquivo. | Executar `deploy` depois de concluir `repositorio` com evidência objetiva. |
| `publicacao` | `triagem` | alta | `processo` | — | Aguardando ciclo `deploy` ficar verde neste arquivo. | Executar `publicacao` depois de concluir `deploy` com evidência objetiva. |
| `banco` | `triagem` | alta | `DB` | — | Aguardando ciclo `publicacao` ficar verde neste arquivo. | Executar `banco` depois de concluir `publicacao` com evidência objetiva. |
| `jobs` | `triagem` | alta | `job` | — | Não aplicável no contrato atual desta responsabilidade. | Ignorar até mudança contratual aprovada nos documentos normativos. |
| `backend` | `triagem` | alta | `backend` | — | Aguardando ciclo `banco` ficar verde neste arquivo. | Executar `backend` depois de concluir `banco` com evidência objetiva. |
| `teste-integracao-api` | `triagem` | alta | `teste` | — | Aguardando ciclo `backend` ficar verde neste arquivo. | Executar `teste-integracao-api` depois de concluir `backend` com evidência objetiva. |
| `microfrontend` | `triagem` | alta | `microfrontend` | — | Aguardando ciclo `teste-integracao-api` ficar verde neste arquivo. | Executar `microfrontend` depois de concluir `teste-integracao-api` com evidência objetiva. |
| `smoke` | `triagem` | alta | `smoke` | — | Aguardando ciclo `microfrontend` ficar verde neste arquivo. | Executar `smoke` depois de concluir `microfrontend` com evidência objetiva. |
| `teste` | `triagem` | alta | `teste` | — | Aguardando ciclo `smoke` ficar verde neste arquivo. | Executar `teste` depois de concluir `smoke` com evidência objetiva. |
| `documentacao` | `triagem` | alta | `documentacao` | — | Aguardando ciclo `teste` ficar verde neste arquivo. | Executar `documentacao` depois de concluir `teste` com evidência objetiva. |
| `governanca` | `triagem` | alta | `governanca` | — | Aguardando ciclo `documentacao` ficar verde neste arquivo. | Executar `governanca` depois de concluir `documentacao` com evidência objetiva. |

## Links normativos

- [Arquitetura](../01-arquitetura.md)
- [Governança](../07-governanca-github.md)
- [Planejamento de ciclos](../08-planejamento-ciclos-implementacao-repositorios.md)

## Histórico curto

- 2026-05-29 — backlog migrado do painel operacional anterior para `docs/project`.
- 2026-05-29 — ciclo `repositorio` rebaixado para `bloqueado` após inspeção local de `Aneety/ai` revelar só `aneety-platform/apps/.gitkeep` e checkout sujo com `.playwright-mcp/`.
