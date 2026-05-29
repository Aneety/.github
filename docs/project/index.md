# Painel operacional em Markdown

`docs/project` é a fonte única de backlog, status, owner, evidência e bloqueio da Aneety Platform. O painel operacional anterior foi descontinuado para uso diário. GitHub Issues e PRs continuam apenas como histórico, discussão e vínculo de evidência quando necessário.

## Método

- Atualize primeiro o arquivo da responsabilidade antes de mudar status operacional em qualquer outro lugar.
- Use sempre os campos canônicos: `Status`, `Ciclo`, `Responsabilidade`, `Repo destino`, `Owner`, `Prioridade`, `Gate`, `Evidência`, `Bloqueio`.
- Trate GitHub Issues como trilha histórica; não como painel ativo de status.

## Visão executiva

| Responsabilidade | Owner | Prioridade | Ciclo ativo | Status | Arquivo | Evidência atual | Bloqueio |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `gateway-borda` | Ricardo Malnati | alta | `repositorio` | `pronto` | [gateway-borda](./gateway-borda.md) | [#46](https://github.com/Aneety/.github/issues/46) | — |
| `tenant-white-label` | Ricardo Malnati | alta | `repositorio` | `pronto` | [tenant-white-label](./tenant-white-label.md) | [#4](https://github.com/Aneety/.github/issues/4) | — |
| `identidade-acesso` | Ricardo Malnati | alta | `repositorio` | `pronto` | [identidade-acesso](./identidade-acesso.md) | [#5](https://github.com/Aneety/.github/issues/5) | — |
| `onboarding-acesso` | Ricardo Malnati | alta | `repositorio` | `pronto` | [onboarding-acesso](./onboarding-acesso.md) | [#6](https://github.com/Aneety/.github/issues/6) | — |
| `pedidos-customizados` | Ricardo Malnati | alta | `repositorio` | `pronto` | [pedidos-customizados](./pedidos-customizados.md) | [#7](https://github.com/Aneety/.github/issues/7) | — |
| `workflow-estados` | Ricardo Malnati | alta | `repositorio` | `pronto` | [workflow-estados](./workflow-estados.md) | [#8](https://github.com/Aneety/.github/issues/8) | — |
| `catalogo-operacional` | Ricardo Malnati | alta | `repositorio` | `pronto` | [catalogo-operacional](./catalogo-operacional.md) | [#9](https://github.com/Aneety/.github/issues/9) | — |
| `identidade-federada` | Ricardo Malnati | media | `repositorio` | `pronto` | [identidade-federada](./identidade-federada.md) | [#11](https://github.com/Aneety/.github/issues/11) | — |
| `qualidade-evidencias` | Ricardo Malnati | media | `repositorio` | `pronto` | [qualidade-evidencias](./qualidade-evidencias.md) | [#12](https://github.com/Aneety/.github/issues/12) | — |
| `pagamentos` | Ricardo Malnati | media | `repositorio` | `pronto` | [pagamentos](./pagamentos.md) | [#13](https://github.com/Aneety/.github/issues/13) | — |
| `offline-sync` | Ricardo Malnati | media | `repositorio` | `pronto` | [offline-sync](./offline-sync.md) | [#14](https://github.com/Aneety/.github/issues/14) | — |
| `marketplace-operacional` | Ricardo Malnati | media | `repositorio` | `pronto` | [marketplace-operacional](./marketplace-operacional.md) | [#15](https://github.com/Aneety/.github/issues/15) | — |
| `producao-execucao` | Ricardo Malnati | media | `repositorio` | `pronto` | [producao-execucao](./producao-execucao.md) | [#16](https://github.com/Aneety/.github/issues/16) | — |
| `logistica-rastreabilidade` | Ricardo Malnati | media | `repositorio` | `pronto` | [logistica-rastreabilidade](./logistica-rastreabilidade.md) | [#18](https://github.com/Aneety/.github/issues/18) | — |
| `auditoria-operacional` | Ricardo Malnati | media | `repositorio` | `pronto` | [auditoria-operacional](./auditoria-operacional.md) | [#19](https://github.com/Aneety/.github/issues/19) | — |
| `sla-capacidade` | Ricardo Malnati | media | `repositorio` | `pronto` | [sla-capacidade](./sla-capacidade.md) | [#20](https://github.com/Aneety/.github/issues/20) | — |
| `orcamentos-precificacao` | Ricardo Malnati | media | `repositorio` | `pronto` | [orcamentos-precificacao](./orcamentos-precificacao.md) | [#21](https://github.com/Aneety/.github/issues/21) | — |
| `comunicacao-operacional` | Ricardo Malnati | media | `repositorio` | `pronto` | [comunicacao-operacional](./comunicacao-operacional.md) | [#22](https://github.com/Aneety/.github/issues/22) | — |
| `comunicacao-email` | Ricardo Malnati | media | `repositorio` | `pronto` | [comunicacao-email](./comunicacao-email.md) | [#23](https://github.com/Aneety/.github/issues/23) | — |
| `suporte-excecoes` | Ricardo Malnati | media | `repositorio` | `pronto` | [suporte-excecoes](./suporte-excecoes.md) | [#24](https://github.com/Aneety/.github/issues/24) | — |
| `privacidade-consentimento` | Ricardo Malnati | media | `repositorio` | `pronto` | [privacidade-consentimento](./privacidade-consentimento.md) | [#25](https://github.com/Aneety/.github/issues/25) | — |
| `demo-seeds` | Ricardo Malnati | media | `repositorio` | `pronto` | [demo-seeds](./demo-seeds.md) | [#26](https://github.com/Aneety/.github/issues/26) | — |

## Bloqueios globais

- Nenhum bloqueio global ativo neste painel Markdown.
- O impedimento anterior ligado ao painel externo foi removido com a migração para `docs/project`.

## Últimas atualizações

- 2026-05-29 — PR [#53](https://github.com/Aneety/.github/pull/53) remove documento paralelo de produto.
- 2026-05-29 — PR [#54](https://github.com/Aneety/.github/pull/54) alinha caminho canônico dos issue templates.
- 2026-05-29 — PR [#55](https://github.com/Aneety/.github/pull/55) consolida contrato monorepo em `Aneety/ai`.
- 2026-05-29 — este diretório substitui o painel operacional anterior por arquivos Markdown versionados.

## Governança mínima de atualização

1. Confirmar fonte documental e critério de aceite.
2. Atualizar `docs/project/<responsabilidade>.md` no mesmo branch da mudança.
3. Linkar PR, commit, log, screenshot ou doc na coluna `Evidência`.
4. Registrar bloqueio com causa objetiva e próxima ação.
5. Atualizar esta visão executiva quando `Status`, `Owner`, `Prioridade` ou `Ciclo ativo` mudarem.

## Histórico de migração

- Issue histórica de governança do painel anterior: [#3](https://github.com/Aneety/.github/issues/3).
- Issues abertas de `ciclo:repositorio` foram migradas para arquivos por responsabilidade e podem ser fechadas após apontarem para estes arquivos.
