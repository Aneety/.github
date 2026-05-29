# Painel operacional em Markdown

`docs/project` é a fonte única de backlog, status, owner, evidência e bloqueio da Aneety Platform. O painel operacional anterior foi descontinuado para uso diário. GitHub Issues e PRs continuam apenas como histórico, discussão e vínculo de evidência quando necessário.

## Método

- Atualize primeiro o arquivo da responsabilidade antes de mudar status operacional em qualquer outro lugar.
- Use sempre os campos canônicos: `Status`, `Ciclo`, `Responsabilidade`, `Repo destino`, `Owner`, `Prioridade`, `Gate`, `Evidência`, `Bloqueio`.
- Trate GitHub Issues como trilha histórica; não como painel ativo de status.

## Visão executiva

| Responsabilidade | Owner | Prioridade | Ciclo ativo | Status | Arquivo | Evidência atual | Bloqueio |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `gateway-borda` | Ricardo Malnati | alta | `repositorio` | `bloqueado` | [gateway-borda](./gateway-borda.md) | [#46](https://github.com/Aneety/.github/issues/46) + inspeção local 2026-05-29 | Sem raiz em `Aneety/ai`; checkout local sujo com `.playwright-mcp/`. |
| `tenant-white-label` | Ricardo Malnati | alta | `repositorio` | `bloqueado` | [tenant-white-label](./tenant-white-label.md) | [#4](https://github.com/Aneety/.github/issues/4) + inspeção local 2026-05-29 | Sem raiz em `Aneety/ai`; checkout local sujo com `.playwright-mcp/`. |
| `identidade-acesso` | Ricardo Malnati | alta | `repositorio` | `bloqueado` | [identidade-acesso](./identidade-acesso.md) | [#5](https://github.com/Aneety/.github/issues/5) + inspeção local 2026-05-29 | Sem raiz em `Aneety/ai`; checkout local sujo com `.playwright-mcp/`. |
| `onboarding-acesso` | Ricardo Malnati | alta | `repositorio` | `bloqueado` | [onboarding-acesso](./onboarding-acesso.md) | [#6](https://github.com/Aneety/.github/issues/6) + inspeção local 2026-05-29 | Sem raiz em `Aneety/ai`; checkout local sujo com `.playwright-mcp/`. |
| `pedidos-customizados` | Ricardo Malnati | alta | `repositorio` | `bloqueado` | [pedidos-customizados](./pedidos-customizados.md) | [#7](https://github.com/Aneety/.github/issues/7) + inspeção local 2026-05-29 | Sem raiz em `Aneety/ai`; checkout local sujo com `.playwright-mcp/`. |
| `workflow-estados` | Ricardo Malnati | alta | `repositorio` | `bloqueado` | [workflow-estados](./workflow-estados.md) | [#8](https://github.com/Aneety/.github/issues/8) + inspeção local 2026-05-29 | Sem raiz em `Aneety/ai`; checkout local sujo com `.playwright-mcp/`. |
| `catalogo-operacional` | Ricardo Malnati | alta | `repositorio` | `bloqueado` | [catalogo-operacional](./catalogo-operacional.md) | [#9](https://github.com/Aneety/.github/issues/9) + inspeção local 2026-05-29 | Sem raiz em `Aneety/ai`; checkout local sujo com `.playwright-mcp/`. |
| `identidade-federada` | Ricardo Malnati | media | `repositorio` | `bloqueado` | [identidade-federada](./identidade-federada.md) | [#11](https://github.com/Aneety/.github/issues/11) + inspeção local 2026-05-29 | Sem raiz em `Aneety/ai`; checkout local sujo com `.playwright-mcp/`. |
| `qualidade-evidencias` | Ricardo Malnati | media | `repositorio` | `bloqueado` | [qualidade-evidencias](./qualidade-evidencias.md) | [#12](https://github.com/Aneety/.github/issues/12) + inspeção local 2026-05-29 | Sem raiz em `Aneety/ai`; checkout local sujo com `.playwright-mcp/`. |
| `pagamentos` | Ricardo Malnati | media | `repositorio` | `bloqueado` | [pagamentos](./pagamentos.md) | [#13](https://github.com/Aneety/.github/issues/13) + inspeção local 2026-05-29 | Sem raiz em `Aneety/ai`; checkout local sujo com `.playwright-mcp/`. |
| `offline-sync` | Ricardo Malnati | media | `repositorio` | `bloqueado` | [offline-sync](./offline-sync.md) | [#14](https://github.com/Aneety/.github/issues/14) + inspeção local 2026-05-29 | Sem raiz em `Aneety/ai`; checkout local sujo com `.playwright-mcp/`. |
| `marketplace-operacional` | Ricardo Malnati | media | `repositorio` | `bloqueado` | [marketplace-operacional](./marketplace-operacional.md) | [#15](https://github.com/Aneety/.github/issues/15) + inspeção local 2026-05-29 | Sem raiz em `Aneety/ai`; checkout local sujo com `.playwright-mcp/`. |
| `producao-execucao` | Ricardo Malnati | media | `repositorio` | `bloqueado` | [producao-execucao](./producao-execucao.md) | [#16](https://github.com/Aneety/.github/issues/16) + inspeção local 2026-05-29 | Sem raiz em `Aneety/ai`; checkout local sujo com `.playwright-mcp/`. |
| `logistica-rastreabilidade` | Ricardo Malnati | media | `repositorio` | `bloqueado` | [logistica-rastreabilidade](./logistica-rastreabilidade.md) | [#18](https://github.com/Aneety/.github/issues/18) + inspeção local 2026-05-29 | Sem raiz em `Aneety/ai`; checkout local sujo com `.playwright-mcp/`. |
| `auditoria-operacional` | Ricardo Malnati | media | `repositorio` | `bloqueado` | [auditoria-operacional](./auditoria-operacional.md) | [#19](https://github.com/Aneety/.github/issues/19) + inspeção local 2026-05-29 | Sem raiz em `Aneety/ai`; checkout local sujo com `.playwright-mcp/`. |
| `sla-capacidade` | Ricardo Malnati | media | `repositorio` | `bloqueado` | [sla-capacidade](./sla-capacidade.md) | [#20](https://github.com/Aneety/.github/issues/20) + inspeção local 2026-05-29 | Sem raiz em `Aneety/ai`; checkout local sujo com `.playwright-mcp/`. |
| `orcamentos-precificacao` | Ricardo Malnati | media | `repositorio` | `bloqueado` | [orcamentos-precificacao](./orcamentos-precificacao.md) | [#21](https://github.com/Aneety/.github/issues/21) + inspeção local 2026-05-29 | Sem raiz em `Aneety/ai`; checkout local sujo com `.playwright-mcp/`. |
| `comunicacao-operacional` | Ricardo Malnati | media | `repositorio` | `bloqueado` | [comunicacao-operacional](./comunicacao-operacional.md) | [#22](https://github.com/Aneety/.github/issues/22) + inspeção local 2026-05-29 | Sem raiz em `Aneety/ai`; checkout local sujo com `.playwright-mcp/`. |
| `comunicacao-email` | Ricardo Malnati | media | `repositorio` | `bloqueado` | [comunicacao-email](./comunicacao-email.md) | [#23](https://github.com/Aneety/.github/issues/23) + inspeção local 2026-05-29 | Sem raiz em `Aneety/ai`; checkout local sujo com `.playwright-mcp/`. |
| `suporte-excecoes` | Ricardo Malnati | media | `repositorio` | `bloqueado` | [suporte-excecoes](./suporte-excecoes.md) | [#24](https://github.com/Aneety/.github/issues/24) + inspeção local 2026-05-29 | Sem raiz em `Aneety/ai`; checkout local sujo com `.playwright-mcp/`. |
| `privacidade-consentimento` | Ricardo Malnati | media | `repositorio` | `bloqueado` | [privacidade-consentimento](./privacidade-consentimento.md) | [#25](https://github.com/Aneety/.github/issues/25) + inspeção local 2026-05-29 | Sem raiz em `Aneety/ai`; checkout local sujo com `.playwright-mcp/`. |
| `demo-seeds` | Ricardo Malnati | media | `repositorio` | `bloqueado` | [demo-seeds](./demo-seeds.md) | [#26](https://github.com/Aneety/.github/issues/26) + inspeção local 2026-05-29 | Sem raiz em `Aneety/ai`; checkout local sujo com `.playwright-mcp/`. |

## Bloqueios globais

- `Aneety/ai` local em `/Users/mal/GitHub/Aneety/ai` está sujo (`?? .playwright-mcp/`), então a automação não pode criar ou revisar raízes de responsabilidade ali com segurança.
- `Aneety/ai` ainda contém apenas `aneety-platform/apps/.gitkeep`; nenhuma responsabilidade tem raiz concreta em `aneety-platform/apps/<responsabilidade>/...`, então nenhum ciclo `repositorio` pode permanecer verde por evidência de implementação.
- `Aneety/ai` local também está 4 commits atrás de `origin/main`, então leitura de implementação deste ciclo precisou usar worktree limpo em `origin/main`.
- `Aneety/.github` local em `/Users/mal/GitHub/Aneety/.github` segue sujo na branch `codex/issue-template-path`; mesmo com `git fetch --all --prune` concluído, decisões canônicas deste ciclo precisaram usar worktree limpo em `origin/main`, nunca esse checkout como fonte de verdade.
- GitHub Project externo continua bloqueado por permissão `organization.projectV2`; token ativo não expõe `read:project`, então backlog ativo segue somente em `docs/project`.
- PRs [#65](https://github.com/Aneety/.github/pull/65), [#66](https://github.com/Aneety/.github/pull/66) e [#67](https://github.com/Aneety/.github/pull/67) seguem em draft e `gh pr checks` não reportou checks neste repo; sincronização documental continua sem gate remoto objetivo em `Aneety/.github`.

## Últimas atualizações

- 2026-05-29 — worktrees limpos de `origin/main` passaram a ser leitura canônica deste ciclo para `Aneety/.github` e `Aneety/ai` por causa de checkout local sujo e checkout local defasado.
- 2026-05-29 — `gh project view 1 --owner Aneety` seguiu bloqueado por `organization.projectV2`; este ciclo continuou sem auditoria do painel externo antigo e registrou backlog ativo apenas em `docs/project`.
- 2026-05-29 — PR [#6](https://github.com/Aneety/ai/pull/6) (`ci: expand actions-first governance gates`) segue em draft; `gh pr checks` confirmou `pass` em `Scaffold-only repository gate`, `Actions-first governance audit`, `Dependency review`, `Detect security inputs`, `Discover app modules`, `Repository policy checks` e `Secret text scan`, com `Compile, lint and test modules` e `CodeQL analysis` ainda em `skipping` porque o monorepo continua sem módulos concretos.
- 2026-05-29 — PR [#65](https://github.com/Aneety/.github/pull/65) (`docs: require actions-first validation gates`) segue em draft para alinhar `docs/03`, `docs/07` e `docs/08`; até merge, `main` ainda carrega redação anterior sobre a ordem explícita PR -> Actions -> Cloudflare.
- 2026-05-29 — `gh pr checks` confirmou ausência de checks reportados nos drafts [#65](https://github.com/Aneety/.github/pull/65), [#66](https://github.com/Aneety/.github/pull/66) e [#67](https://github.com/Aneety/.github/pull/67), então o gate remoto de documentação permanece bloqueado neste repo.
- 2026-05-29 — consulta em `Aneety/.github`, `Aneety/ai` e `Aneety/assets` confirmou zero issues abertas neste ciclo.
- 2026-05-29 — PR [#61](https://github.com/Aneety/.github/pull/61) resincronizou o painel Markdown com a evidência atual dos repositórios.
- 2026-05-29 — PR [#60](https://github.com/Aneety/.github/pull/60) formalizou que validação de código fonte do MVP só fecha com evidência Cloudflare-backed.
- 2026-05-29 — inspeção local rebaixou todos os ciclos `repositorio` para `bloqueado` até existir raiz real por responsabilidade em `Aneety/ai` e checkout limpo.
- 2026-05-29 — PR [#53](https://github.com/Aneety/.github/pull/53) removeu documento paralelo de produto.
- 2026-05-29 — PR [#54](https://github.com/Aneety/.github/pull/54) alinhou caminho canônico dos issue templates.
- 2026-05-29 — PR [#55](https://github.com/Aneety/.github/pull/55) consolidou contrato monorepo em `Aneety/ai`.
- 2026-05-29 — este diretório substituiu o painel operacional anterior por arquivos Markdown versionados.

## Governança mínima de atualização

1. Confirmar fonte documental e critério de aceite.
2. Atualizar `docs/project/<responsabilidade>.md` no mesmo branch da mudança.
3. Linkar PR, commit, log, screenshot ou doc na coluna `Evidência`.
4. Registrar bloqueio com causa objetiva e próxima ação.
5. Atualizar esta visão executiva quando `Status`, `Owner`, `Prioridade` ou `Ciclo ativo` mudarem.

## Histórico de migração

- Issue histórica de governança do painel anterior: [#3](https://github.com/Aneety/.github/issues/3).
- Issues históricas de `ciclo:repositorio` já foram migradas para arquivos por responsabilidade e encerradas; o status ativo continua apenas em `docs/project/`.
