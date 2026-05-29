# Planejamento de ciclos e issues para implementação de repositórios — Aneety Platform

## Objetivo

Este documento transforma requisitos, processos, modelagens de banco e regras de repositórios da Aneety Platform em um backlog operacional de ciclos e issues. Ele orienta a abertura de repositórios, submódulos, schemas, BFFs, jobs, microfrontends, validações e fechamento de evidências sem substituir os documentos normativos.

## Fontes normativas

A implementação deve obedecer à seguinte precedência documental:

1. [`01-arquitetura.md`](01-arquitetura.md) — arquitetura, runtime, limites de fornecedor, segredos, dados e submódulos.
2. [`02-requisitos.md`](02-requisitos.md) — requisitos de produto, requisitos técnicos, aceite e integrações opcionais.
3. [`03-processos.md`](03-processos.md) — fluxo de execução, operação, migração e gates.
4. [`04-modelagem-banco.md`](04-modelagem-banco.md) — tabelas conceituais, isolamento, índices, RLS e policies.
5. [`05-estrutura-repositorios.md`](05-estrutura-repositorios.md) — org, clone local, submódulos, prefixos e responsabilidades.
6. [`06-ciclos-cobertura.md`](06-ciclos-cobertura.md) — ordem de ciclos, sequência CRUD e gates de cobertura.
7. [`07-governanca-github.md`](07-governanca-github.md) — issues, labels, Project, Definition of Done e bloqueios.

Regra de execução: issue, Project, PR ou automação não muda contrato. Mudança de contrato começa por PR documental nos arquivos acima.

## Gates antes de criar repositório ou submódulo

Uma responsabilidade só pode virar repositório próprio quando registrar:

- contrato local e fonte documental;
- owner operacional;
- dados tratados e classificação de sensibilidade;
- segredos necessários, sem valores em Git, log, screenshot ou documentação de usuário;
- custo zero preservado;
- critérios de aceite verificáveis;
- testes previstos;
- plano de saída para fornecedor externo quando aplicável;
- caminho no orquestrador `Aneety/ai` sob `aneety-platform/apps/<responsabilidade>/...`;
- remoto oficial `https://github.com/Aneety/<repo>` e clone local `/Users/mal/GitHub/Aneety/<repo>`.

## Ordem de ciclos usada neste planejamento

A ordem executável é:

1. `repositorio`
2. `deploy`
3. `publicacao`
4. `banco`
5. `jobs`
6. `backend`
7. `teste-integracao-api`
8. `microfrontend`
9. `smoke`
10. `teste`
11. `documentacao`
12. `governanca`

Observação normativa: `06-ciclos-cobertura.md` inclui **Testes de integração de API**, mas `07-governanca-github.md` ainda não declara label `ciclo:teste-integracao-api`. Até correção documental, issues desse ciclo devem ser marcadas como bloqueadas em governança ou receber label manual transitória registrada no Project.

## Padrão de issue

Toda issue derivada deste documento deve usar o corpo mínimo abaixo, preenchido com os dados da matriz de responsabilidade:

```markdown
## Fonte documental

- Documento:
- Seção:

## Ciclo e responsabilidade

- Ciclo:
- Responsabilidade:
- Repo afetado:
- Owner:

## Critério de aceite

-

## Evidência esperada

-

## Riscos e bloqueios

-

## Links

-
```

Labels mínimas: um `tipo:*`, um `ciclo:*` e um `status:*`. Quando o ciclo for teste de integração de API, registrar o bloqueio de taxonomia até existir `ciclo:teste-integracao-api` em `07-governanca-github.md`.

## Matriz por modelagem de banco

| Responsabilidade | Tabelas cobertas | Repo esperado | Caminho no orquestrador | Ciclos obrigatórios | Aceite e evidência base |
| --- | --- | --- | --- | --- | --- |
| `tenant-white-label` | `tenants`, `tenant_branding` | `tenant-white-label` | `aneety-platform/apps/tenant-white-label/db-tenant-white-label`, `worker-tenant-white-label`, `mfe-tenant-white-label` | `repositorio`, `deploy`, `publicacao`, `banco`, `backend`, `teste-integracao-api`, `microfrontend`, `smoke`, `teste`, `documentacao`, `governanca` | Tenant e marca versionados, isolados por tenant, com RLS, contrato BFF e tela administrativa sem vazamento técnico. Evidência: migration, teste DB, contrato API, smoke visual e docs. |
| `identidade-acesso` | `app_identities`, `auth_credentials`, `auth_sessions`, `app_users`, `access_profiles`, `permissions`, `access_profile_permissions` | `identidade-acesso` | `aneety-platform/apps/identidade-acesso/db-identidade-acesso`, `worker-identidade-acesso`, `mfe-identidade-acesso` | `repositorio`, `deploy`, `publicacao`, `banco`, `backend`, `teste-integracao-api`, `microfrontend`, `smoke`, `teste`, `documentacao`, `governanca` | Identidade própria, sessão, perfil e permissões sem acesso direto do frontend ao banco. Evidência: hash de credenciais, expiração/revogação, policies, contrato de sessão e testes negativos. |
| `pedidos-customizados` | `orders`, `order_checkpoints` | `pedidos-customizados` | `aneety-platform/apps/pedidos-customizados/db-pedidos-customizados`, `worker-pedidos-customizados`, `mfe-pedidos-customizados` | `repositorio`, `deploy`, `publicacao`, `banco`, `backend`, `teste-integracao-api`, `microfrontend`, `smoke`, `teste`, `documentacao`, `governanca` | Pedido customizado e checkpoints com histórico por versão, exclusão lógica e CRUD incremental. Evidência: migration, testes CRUD, contrato HTTP, smoke de criação/listagem/edição e documentação. |
| `qualidade-evidencias` | `quality_reviews`, `attachments` | `qualidade-evidencias` | `aneety-platform/apps/qualidade-evidencias/db-qualidade-evidencias`, `worker-qualidade-evidencias`, `mfe-qualidade-evidencias` | `repositorio`, `deploy`, `publicacao`, `banco`, `backend`, `teste-integracao-api`, `microfrontend`, `smoke`, `teste`, `documentacao`, `governanca` | Revisão de qualidade e metadados de evidências com permissão por tenant, pedido e etapa. Evidência: RLS, validação de metadados, bloqueio de avanço sem evidência e smoke de anexação controlada. |
| `pagamentos` | `payment_intents` | `pagamentos` | `aneety-platform/apps/pagamentos/db-pagamentos`, `worker-pagamentos`, `mfe-pagamentos`, `int-pagamentos` | `repositorio`, `deploy`, `publicacao`, `banco`, `backend`, `teste-integracao-api`, `microfrontend`, `smoke`, `teste`, `documentacao`, `governanca` | Intenção e conciliação de pagamento sem corromper pedido quando adapter externo falhar. Evidência: testes de indisponibilidade, status financeiro e contrato substituível. |
| `offline-sync` | `sync_events`, `offline_conflicts` | `offline-sync` | `aneety-platform/apps/offline-sync/db-offline-sync`, `worker-offline-sync`, `job-offline-sync`, `mfe-offline-sync` | `repositorio`, `deploy`, `publicacao`, `banco`, `jobs`, `backend`, `teste-integracao-api`, `microfrontend`, `smoke`, `teste`, `documentacao`, `governanca` | Fila local, replay e conflitos auditáveis por tenant. Evidência: migration, job idempotente, testes de replay, API integrada e tela de resolução quando aplicável. |
| `marketplace-operacional` | `marketplace_actors`, `marketplace_favorites` | `marketplace-operacional` | `aneety-platform/apps/marketplace-operacional/db-marketplace-operacional`, `worker-marketplace-operacional`, `mfe-marketplace-operacional` | `repositorio`, `deploy`, `publicacao`, `banco`, `backend`, `teste-integracao-api`, `microfrontend`, `smoke`, `teste`, `documentacao`, `governanca` | Atores e favoritos filtráveis por tenant, tipo, status e disponibilidade. Evidência: índices, policies, contrato de listagem paginada e smoke de favoritar. |
| `producao-execucao` | `production_demands` | `producao-execucao` | `aneety-platform/apps/producao-execucao/db-producao-execucao`, `worker-producao-execucao`, `mfe-producao-execucao` | `repositorio`, `deploy`, `publicacao`, `banco`, `backend`, `teste-integracao-api`, `microfrontend`, `smoke`, `teste`, `documentacao`, `governanca` | Demanda de produção com aceite, rejeição, responsável e motivo. Evidência: CRUD, transição de status, auditoria mínima e smoke de aceite/rejeição. |
| `logistica-rastreabilidade` | `delivery_demands`, `delivery_evidences`, `tracking_events`, `map_snapshots` | `logistica-rastreabilidade` | `aneety-platform/apps/logistica-rastreabilidade/db-logistica-rastreabilidade`, `worker-logistica-rastreabilidade`, `mfe-logistica-rastreabilidade`, `int-mapas` | `repositorio`, `deploy`, `publicacao`, `banco`, `jobs`, `backend`, `teste-integracao-api`, `microfrontend`, `smoke`, `teste`, `documentacao`, `governanca` | Coleta, entrega, evidências, eventos e mapas por contrato substituível. Evidência: events/snapshots, visibilidade por perfil, job de snapshot quando existir, smoke de rastreabilidade. |
| `auditoria-operacional` | `audit_events`, `audit_event_changes` | `auditoria-operacional` | `aneety-platform/apps/auditoria-operacional/db-auditoria-operacional`, `worker-auditoria-operacional`, `mfe-auditoria-operacional` | `repositorio`, `deploy`, `publicacao`, `banco`, `backend`, `teste-integracao-api`, `microfrontend`, `smoke`, `teste`, `documentacao`, `governanca` | Eventos sensíveis e valores antes/depois, sem leitura cross-tenant. Evidência: trilha de alteração, testes de visibilidade e consulta administrativa. |
| `catalogo-operacional` | `catalogs`, `catalog_items`, `catalog_item_options` | `catalogo-operacional` | `aneety-platform/apps/catalogo-operacional/db-catalogo-operacional`, `worker-catalogo-operacional`, `mfe-catalogo-operacional` | `repositorio`, `deploy`, `publicacao`, `banco`, `backend`, `teste-integracao-api`, `microfrontend`, `smoke`, `teste`, `documentacao`, `governanca` | Catálogo por tenant com itens, atributos, preço-base, prazo-base e opções. Evidência: constraints, índices, contrato CRUD e smoke de configuração. |
| `workflow-estados` | `workflow_states`, `workflow_state_transitions` | `workflow-estados` | `aneety-platform/apps/workflow-estados/db-workflow-estados`, `worker-workflow-estados`, `mfe-workflow-estados` | `repositorio`, `deploy`, `publicacao`, `banco`, `backend`, `teste-integracao-api`, `microfrontend`, `smoke`, `teste`, `documentacao`, `governanca` | Estados e transições oficiais com permissão e motivo obrigatório. Evidência: matriz de transição, testes de bloqueio e contrato de validação. |
| `sla-capacidade` | `sla_policies`, `operational_schedules`, `actor_capacity_slots` | `sla-capacidade` | `aneety-platform/apps/sla-capacidade/db-sla-capacidade`, `worker-sla-capacidade`, `job-sla-capacidade`, `mfe-sla-capacidade` | `repositorio`, `deploy`, `publicacao`, `banco`, `jobs`, `backend`, `teste-integracao-api`, `microfrontend`, `smoke`, `teste`, `documentacao`, `governanca` | SLA, agenda e capacidade por ator, data e status. Evidência: índices de agenda, job de alerta quando existir, API integrada e smoke de disponibilidade. |
| `orcamentos-precificacao` | `budget_requests`, `budget_items` | `orcamentos-precificacao` | `aneety-platform/apps/orcamentos-precificacao/db-orcamentos-precificacao`, `worker-orcamentos-precificacao`, `mfe-orcamentos-precificacao` | `repositorio`, `deploy`, `publicacao`, `banco`, `backend`, `teste-integracao-api`, `microfrontend`, `smoke`, `teste`, `documentacao`, `governanca` | Orçamentos, linhas de preço, aprovação, rejeição e expiração. Evidência: cálculo registrado, status auditável, contrato API e smoke de aprovação. |
| `comunicacao-operacional` | `operational_messages`, `notifications` | `comunicacao-operacional` | `aneety-platform/apps/comunicacao-operacional/db-comunicacao-operacional`, `worker-comunicacao-operacional`, `job-comunicacao-operacional`, `mfe-comunicacao-operacional` | `repositorio`, `deploy`, `publicacao`, `banco`, `jobs`, `backend`, `teste-integracao-api`, `microfrontend`, `smoke`, `teste`, `documentacao`, `governanca` | Mensagens, avisos e notificações por tenant, entidade, status e visibilidade. Evidência: fan-out controlado, leitura, status e smoke de notificação in-app. |
| `suporte-excecoes` | `support_cases`, `exception_cases` | `suporte-excecoes` | `aneety-platform/apps/suporte-excecoes/db-suporte-excecoes`, `worker-suporte-excecoes`, `mfe-suporte-excecoes` | `repositorio`, `deploy`, `publicacao`, `banco`, `backend`, `teste-integracao-api`, `microfrontend`, `smoke`, `teste`, `documentacao`, `governanca` | Chamados e exceções operacionais com categoria, prioridade, impacto e resolução. Evidência: CRUD, status, auditoria e smoke de abertura/fechamento. |
| `privacidade-consentimento` | `consent_records` | `privacidade-consentimento` | `aneety-platform/apps/privacidade-consentimento/db-privacidade-consentimento`, `worker-privacidade-consentimento`, `mfe-privacidade-consentimento` | `repositorio`, `deploy`, `publicacao`, `banco`, `backend`, `teste-integracao-api`, `microfrontend`, `smoke`, `teste`, `documentacao`, `governanca` | Consentimentos concedidos/revogados por identidade, tenant, tipo e origem. Evidência: registro de revogação, bloqueio de uso indevido e consulta por permissão. |
| `demo-seeds` | `demo_seed_cases` | `demo-seeds` | `aneety-platform/apps/demo-seeds/db-demo-seeds`, `job-demo-seeds`, `worker-demo-seeds` | `repositorio`, `deploy`, `publicacao`, `banco`, `jobs`, `backend`, `teste-integracao-api`, `smoke`, `teste`, `documentacao`, `governanca` | Seeds e massas de teste sem transformar a vertical odontológica em limite de produto. Evidência: payloads sanitizados, job idempotente e testes de carga controlada. |

## Issues por responsabilidade

Os blocos abaixo são prontos para abertura como issues GitHub. Cada issue deve usar o template de corpo obrigatório deste documento e labels coerentes com `07-governanca-github.md`.

### `tenant-white-label`

| Ciclo | Título | Aceite | Evidência esperada | Riscos |
| --- | --- | --- | --- | --- |
| `repositorio` | `[repositorio][tenant-white-label] preparar contrato, owner, repo e submódulo` | Contrato, owner, dados, custo zero, repo e caminho `aneety-platform/apps/tenant-white-label/...` registrados. | PR documental e submódulo planejado ou criado conforme gate. | Marca, dados de tenant, lock-in de DNS/CDN. |
| `banco` | `[banco][tenant-white-label] implementar schema, constraints, índices, RLS e seeds` | `tenants` e `tenant_branding` com UUID, datas, exclusão lógica, índices e RLS. | Migration, rollback, teste DB e seed de tenant Lia como marca inicial. | Cross-tenant e configuração visual sensível. |
| `backend` | `[backend][tenant-white-label] publicar contrato do BFF/worker` | API controla tenants e branding por permissão, sem segredo em frontend. | Contrato HTTP, testes de autorização e erro de domínio. | Exposição de dados administrativos. |
| `teste-integracao-api` | `[teste-integracao-api][tenant-white-label] validar API integrada ao banco real` | API e banco validam isolamento e CRUD coberto. | Run de integração com banco real do ciclo. | Label de governança ainda pendente. |
| `microfrontend` | `[microfrontend][tenant-white-label] entregar fluxo visual quando houver UI` | Administração de marca usa linguagem de produto, sem termos de runtime. | Screenshot ou smoke visual com estados de vazio, erro e sucesso. | Vazamento técnico em UI final. |
| `documentacao` | `[documentacao][tenant-white-label] sincronizar docs e evidências` | Arquitetura, requisitos e docs de repo atualizados. | PR documental com links de evidência. | Duplicação fora de `Aneety/.github`. |
| `governanca` | `[governanca][tenant-white-label] fechar ciclo com aceite e Project` | Issue tem aceite, evidência final e Project atualizado. | Link do Project, PRs e checks. | Fechamento sem evidência. |

### `identidade-acesso`

| Ciclo | Título | Aceite | Evidência esperada | Riscos |
| --- | --- | --- | --- | --- |
| `repositorio` | `[repositorio][identidade-acesso] preparar contrato, owner, repo e submódulo` | Responsabilidade de identidade própria, sessão, perfil e permissão registrada. | PR documental e caminho `aneety-platform/apps/identidade-acesso/...`. | Segredos, dados pessoais, lock-in de identidade externa. |
| `banco` | `[banco][identidade-acesso] implementar schema, constraints, índices, RLS e seeds` | Identidades, credenciais, sessões, usuários, perfis e permissões com hash forte, expiração e RLS. | Migration, rollback, testes de hash, revogação e isolamento. | Credencial em texto, sessão sem expiração. |
| `backend` | `[backend][identidade-acesso] publicar contrato do BFF/worker` | Sessão própria emitida por validação interna de tenant, perfil e status. | Contrato HTTP, testes de login, refresh, revogação e acesso negado. | Frontend acessar banco ou IdP diretamente. |
| `teste-integracao-api` | `[teste-integracao-api][identidade-acesso] validar API integrada ao banco real` | Fluxo real valida criação, autenticação, perfil e bloqueio. | Run de integração com casos positivos e negativos. | Label de governança ainda pendente. |
| `microfrontend` | `[microfrontend][identidade-acesso] entregar fluxo visual quando houver UI` | Telas de acesso e gestão usam linguagem de usuário e permissões claras. | Smoke visual de entrada, bloqueio e recuperação. | Termos técnicos de provedor ou token em UI. |
| `documentacao` | `[documentacao][identidade-acesso] sincronizar docs e evidências` | Docs registram sessão própria e integração externa opcional. | PR documental e evidências de segurança. | SSO externo virar requisito obrigatório. |
| `governanca` | `[governanca][identidade-acesso] fechar ciclo com aceite e Project` | Issue fechada com evidência verificável. | Project atualizado e links finais. | Evidência de segurança ausente. |

### `pedidos-customizados`

| Ciclo | Título | Aceite | Evidência esperada | Riscos |
| --- | --- | --- | --- | --- |
| `repositorio` | `[repositorio][pedidos-customizados] preparar contrato, owner, repo e submódulo` | Contrato de pedidos e checkpoints criado com owner e repo. | PR documental e caminho `aneety-platform/apps/pedidos-customizados/...`. | Acoplar pedido à vertical odontológica. |
| `banco` | `[banco][pedidos-customizados] implementar schema, constraints, índices, RLS e seeds` | `orders` e `order_checkpoints` versionados, sem exclusão física, com CRUD incremental. | Migration, rollback, testes CRUD e seed demo sanitizado. | Perda de histórico operacional. |
| `backend` | `[backend][pedidos-customizados] publicar contrato do BFF/worker` | API cobre incluir, pesquisar por id, pesquisar por filtros, atualizar e excluir logicamente. | Contrato HTTP, testes de paginação e auditoria mínima. | Mutação sem nova versão. |
| `teste-integracao-api` | `[teste-integracao-api][pedidos-customizados] validar API integrada ao banco real` | API + banco validam sequência CRUD obrigatória até etapa declarada. | Run de integração com tenant isolado. | Label de governança ainda pendente. |
| `microfrontend` | `[microfrontend][pedidos-customizados] entregar fluxo visual quando houver UI` | Fluxo visual cria, lista, edita e acompanha pedido. | Smoke visual e screenshot sem termos técnicos. | UI sugerir banco, worker ou fornecedor. |
| `documentacao` | `[documentacao][pedidos-customizados] sincronizar docs e evidências` | Requisitos, processos e evidências alinhados ao fluxo central. | PR documental com evidência de CRUD. | Docs duplicadas no repo de implementação. |
| `governanca` | `[governanca][pedidos-customizados] fechar ciclo com aceite e Project` | Project e issue refletem status final e evidência. | Links de PR, testes e smoke. | Fechar antes de smoke. |

### `qualidade-evidencias`

| Ciclo | Título | Aceite | Evidência esperada | Riscos |
| --- | --- | --- | --- | --- |
| `repositorio` | `[repositorio][qualidade-evidencias] preparar contrato, owner, repo e submódulo` | Contrato de qualidade e evidências separado do pedido, com owner. | PR documental e caminho `aneety-platform/apps/qualidade-evidencias/...`. | Anexo expor dado sensível. |
| `banco` | `[banco][qualidade-evidencias] implementar schema, constraints, índices, RLS e seeds` | `quality_reviews` e `attachments` guardam metadados, status, vínculo e permissão. | Migration, rollback, testes de RLS e metadados. | Bytes sem lifecycle ou metadado sem autorização. |
| `backend` | `[backend][qualidade-evidencias] publicar contrato do BFF/worker` | API valida evidência obrigatória e bloqueia avanço indevido. | Contrato HTTP e testes de rejeição/aprovação. | Expor storage interno na UI. |
| `teste-integracao-api` | `[teste-integracao-api][qualidade-evidencias] validar API integrada ao banco real` | Banco e API validam revisão, anexo e permissão. | Run integrado com caso aprovado e reprovado. | Label de governança ainda pendente. |
| `microfrontend` | `[microfrontend][qualidade-evidencias] entregar fluxo visual quando houver UI` | Tela mostra pendência, aprovação e correção em linguagem operacional. | Smoke visual com estados de evidência ausente e aceita. | Termos técnicos de armazenamento. |
| `documentacao` | `[documentacao][qualidade-evidencias] sincronizar docs e evidências` | Docs indicam metadados no banco e bytes por adapter. | PR documental. | Misturar regra de domínio com fornecedor. |
| `governanca` | `[governanca][qualidade-evidencias] fechar ciclo com aceite e Project` | Evidência final linkada antes do fechamento. | Project atualizado. | Aprovação sem trilha. |

### `pagamentos`

| Ciclo | Título | Aceite | Evidência esperada | Riscos |
| --- | --- | --- | --- | --- |
| `repositorio` | `[repositorio][pagamentos] preparar contrato, owner, repo e submódulo` | Responsabilidade de pagamento e adapter substituível registrada. | PR documental e caminho `aneety-platform/apps/pagamentos/...`. | Dependência paga obrigatória. |
| `banco` | `[banco][pagamentos] implementar schema, constraints, índices, RLS e seeds` | `payment_intents` persiste valor, moeda, status e referência externa sem corromper pedido. | Migration, rollback e testes de status. | Provider virar fonte de verdade. |
| `backend` | `[backend][pagamentos] publicar contrato do BFF/worker` | API cria, consulta e concilia intenção com degradação controlada. | Contrato HTTP e testes de indisponibilidade. | Vazamento de chave ou checkout interno. |
| `teste-integracao-api` | `[teste-integracao-api][pagamentos] validar API integrada ao banco real` | API + banco mantêm pedido íntegro mesmo com adapter indisponível. | Run integrado com falha simulada. | Label de governança ainda pendente. |
| `microfrontend` | `[microfrontend][pagamentos] entregar fluxo visual quando houver UI` | UI mostra status financeiro sem citar fornecedor técnico. | Smoke visual de pendência e conciliação. | Lock-in em texto de produto. |
| `documentacao` | `[documentacao][pagamentos] sincronizar docs e evidências` | Docs registram função semântica e plano de saída. | PR documental. | Custo externo sem decisão formal. |
| `governanca` | `[governanca][pagamentos] fechar ciclo com aceite e Project` | Fechamento com evidência de custo zero ou bloqueio formal. | Project atualizado. | Fechar com custo não resolvido. |

### `offline-sync`

| Ciclo | Título | Aceite | Evidência esperada | Riscos |
| --- | --- | --- | --- | --- |
| `repositorio` | `[repositorio][offline-sync] preparar contrato, owner, repo e submódulo` | Contrato de fila, replay e conflito registrado. | PR documental e caminho `aneety-platform/apps/offline-sync/...`. | Conflito perder dado operacional. |
| `banco` | `[banco][offline-sync] implementar schema, constraints, índices, RLS e seeds` | `sync_events` e `offline_conflicts` têm payloads, status, conflito e resolução. | Migration, rollback e testes de isolamento. | Payload com dado sensível em log. |
| `jobs` | `[jobs][offline-sync] implementar replay idempotente e reprocessamento` | Job reprocessa eventos por tenant sem duplicar efeito. | Run de job com replay repetido e log operacional. | Reprocessamento destrutivo. |
| `backend` | `[backend][offline-sync] publicar contrato do BFF/worker` | API recebe eventos, expõe status e permite resolução de conflito. | Contrato HTTP e testes de idempotência. | Aceitar evento cross-tenant. |
| `teste-integracao-api` | `[teste-integracao-api][offline-sync] validar API integrada ao banco real` | Integração valida evento, replay e conflito. | Run integrado com conflito controlado. | Label de governança ainda pendente. |
| `microfrontend` | `[microfrontend][offline-sync] entregar fluxo visual quando houver UI` | Tela de conflito orienta decisão humana sem jargão técnico. | Smoke visual de conflito e resolução. | UI expor payload bruto sensível. |
| `documentacao` | `[documentacao][offline-sync] sincronizar docs e evidências` | Docs registram retry, replay e política de conflito. | PR documental. | Falta de critério de reprocessamento. |
| `governanca` | `[governanca][offline-sync] fechar ciclo com aceite e Project` | Evidência de idempotência anexada. | Project atualizado. | Fechar sem replay verificado. |

### `marketplace-operacional`

| Ciclo | Título | Aceite | Evidência esperada | Riscos |
| --- | --- | --- | --- | --- |
| `repositorio` | `[repositorio][marketplace-operacional] preparar contrato, owner, repo e submódulo` | Contrato de atores e favoritos registrado. | PR documental e caminho `aneety-platform/apps/marketplace-operacional/...`. | Exposição de contato indevida. |
| `banco` | `[banco][marketplace-operacional] implementar schema, constraints, índices, RLS e seeds` | `marketplace_actors` e `marketplace_favorites` filtram por tenant, tipo e status. | Migration, rollback, testes de filtro e favorito. | Listagem cross-tenant. |
| `backend` | `[backend][marketplace-operacional] publicar contrato do BFF/worker` | API lista, filtra, favorita e aciona ator conforme permissão. | Contrato HTTP e testes paginados. | Dados de localização sensíveis. |
| `teste-integracao-api` | `[teste-integracao-api][marketplace-operacional] validar API integrada ao banco real` | Integração valida filtro, ordenação e favorito. | Run integrado com múltiplos atores. | Label de governança ainda pendente. |
| `microfrontend` | `[microfrontend][marketplace-operacional] entregar fluxo visual quando houver UI` | UI mostra atores por disponibilidade e favoritos. | Smoke visual de filtro e favorito. | UI sugerir pontuação não auditada. |
| `documentacao` | `[documentacao][marketplace-operacional] sincronizar docs e evidências` | Docs registram critérios de listagem e privacidade. | PR documental. | Critério implícito não documentado. |
| `governanca` | `[governanca][marketplace-operacional] fechar ciclo com aceite e Project` | Evidência final anexada. | Project atualizado. | Fechar sem teste de permissão. |

### `producao-execucao`

| Ciclo | Título | Aceite | Evidência esperada | Riscos |
| --- | --- | --- | --- | --- |
| `repositorio` | `[repositorio][producao-execucao] preparar contrato, owner, repo e submódulo` | Contrato de demanda de produção registrado. | PR documental e caminho `aneety-platform/apps/producao-execucao/...`. | Misturar produção com pedido sem contrato. |
| `banco` | `[banco][producao-execucao] implementar schema, constraints, índices, RLS e seeds` | `production_demands` cobre aceite, rejeição, motivo e status. | Migration, rollback e testes de status. | Reatribuição sem trilha. |
| `backend` | `[backend][producao-execucao] publicar contrato do BFF/worker` | API envia demanda, aceita, rejeita e consulta por filtros. | Contrato HTTP e testes de transição. | Ator indevido aceitar demanda. |
| `teste-integracao-api` | `[teste-integracao-api][producao-execucao] validar API integrada ao banco real` | Integração valida ciclo de demanda de produção. | Run integrado com aceite e rejeição. | Label de governança ainda pendente. |
| `microfrontend` | `[microfrontend][producao-execucao] entregar fluxo visual quando houver UI` | UI mostra demanda, responsável, notas e rejeição. | Smoke visual de aceite/rejeição. | Texto expor arquitetura. |
| `documentacao` | `[documentacao][producao-execucao] sincronizar docs e evidências` | Docs sincronizam processo de produção. | PR documental. | Processo divergente de requisitos. |
| `governanca` | `[governanca][producao-execucao] fechar ciclo com aceite e Project` | Issue fechada com evidência de transição. | Project atualizado. | Fechar sem teste negativo. |

### `logistica-rastreabilidade`

| Ciclo | Título | Aceite | Evidência esperada | Riscos |
| --- | --- | --- | --- | --- |
| `repositorio` | `[repositorio][logistica-rastreabilidade] preparar contrato, owner, repo e submódulo` | Contrato de coleta, entrega, eventos, mapas e adapter substituível registrado. | PR documental e caminho `aneety-platform/apps/logistica-rastreabilidade/...`. | Localização sensível e lock-in de mapa. |
| `banco` | `[banco][logistica-rastreabilidade] implementar schema, constraints, índices, RLS e seeds` | Demandas, evidências, eventos e snapshots têm tenant, pedido, status e visibilidade. | Migration, rollback, testes de RLS e índices. | Expor localização fora do escopo. |
| `jobs` | `[jobs][logistica-rastreabilidade] implementar snapshots e rotinas idempotentes` | Job calcula snapshots sem duplicar eventos. | Run de job com reexecução segura. | Snapshot incorreto virar fonte de verdade. |
| `backend` | `[backend][logistica-rastreabilidade] publicar contrato do BFF/worker` | API cria demanda, registra check-in/out, eventos e consulta mapa. | Contrato HTTP e testes de visibilidade. | Dependência direta de fornecedor de mapa. |
| `teste-integracao-api` | `[teste-integracao-api][logistica-rastreabilidade] validar API integrada ao banco real` | Integração valida coleta, entrega, evento e snapshot. | Run integrado com rota controlada. | Label de governança ainda pendente. |
| `microfrontend` | `[microfrontend][logistica-rastreabilidade] entregar fluxo visual quando houver UI` | UI exibe acompanhamento sem expor fornecedor ou dados indevidos. | Smoke visual de mapa e rastreabilidade. | UI mostrar precisão indevida. |
| `documentacao` | `[documentacao][logistica-rastreabilidade] sincronizar docs e evidências` | Docs registram permissão, mapa e rastreabilidade. | PR documental. | Contrato de localização incompleto. |
| `governanca` | `[governanca][logistica-rastreabilidade] fechar ciclo com aceite e Project` | Evidência de permissão e smoke anexada. | Project atualizado. | Fechar sem teste de visibilidade. |

### `auditoria-operacional`

| Ciclo | Título | Aceite | Evidência esperada | Riscos |
| --- | --- | --- | --- | --- |
| `repositorio` | `[repositorio][auditoria-operacional] preparar contrato, owner, repo e submódulo` | Contrato de auditoria sensível registrado. | PR documental e caminho `aneety-platform/apps/auditoria-operacional/...`. | Auditoria insuficiente para alteração sensível. |
| `banco` | `[banco][auditoria-operacional] implementar schema, constraints, índices, RLS e seeds` | `audit_events` e `audit_event_changes` guardam ação, entidade, ator e valores. | Migration, rollback e testes de before/after. | Registrar segredo em auditoria. |
| `backend` | `[backend][auditoria-operacional] publicar contrato do BFF/worker` | API consulta e registra eventos com permissão administrativa. | Contrato HTTP e testes de acesso negado. | Exposição cross-tenant. |
| `teste-integracao-api` | `[teste-integracao-api][auditoria-operacional] validar API integrada ao banco real` | Integração valida registro e consulta controlada. | Run integrado com alteração sensível. | Label de governança ainda pendente. |
| `microfrontend` | `[microfrontend][auditoria-operacional] entregar fluxo visual quando houver UI` | UI mostra trilha sem valores secretos. | Smoke visual de consulta auditável. | Mostrar dado sensível em tela. |
| `documentacao` | `[documentacao][auditoria-operacional] sincronizar docs e evidências` | Docs indicam eventos obrigatórios e campos proibidos. | PR documental. | Lacuna de auditoria. |
| `governanca` | `[governanca][auditoria-operacional] fechar ciclo com aceite e Project` | Evidência final anexada. | Project atualizado. | Fechar sem teste negativo. |

### `catalogo-operacional`

| Ciclo | Título | Aceite | Evidência esperada | Riscos |
| --- | --- | --- | --- | --- |
| `repositorio` | `[repositorio][catalogo-operacional] preparar contrato, owner, repo e submódulo` | Contrato de catálogo e personalização registrado. | PR documental e caminho `aneety-platform/apps/catalogo-operacional/...`. | Catálogo acoplar vertical única. |
| `banco` | `[banco][catalogo-operacional] implementar schema, constraints, índices, RLS e seeds` | Catálogos, itens e opções têm preço, prazo, status e tenant. | Migration, rollback e testes de opções. | Preço sem histórico. |
| `backend` | `[backend][catalogo-operacional] publicar contrato do BFF/worker` | API cobre CRUD e consulta paginada de catálogo. | Contrato HTTP e testes de filtro. | Item inválido gerar pedido inválido. |
| `teste-integracao-api` | `[teste-integracao-api][catalogo-operacional] validar API integrada ao banco real` | Integração valida criação de catálogo e leitura de item. | Run integrado com opções obrigatórias. | Label de governança ainda pendente. |
| `microfrontend` | `[microfrontend][catalogo-operacional] entregar fluxo visual quando houver UI` | UI administra catálogo com linguagem de produto. | Smoke visual de item e opção. | Termos técnicos em configuração. |
| `documentacao` | `[documentacao][catalogo-operacional] sincronizar docs e evidências` | Docs registram catálogo por tenant e uso em pedidos. | PR documental. | Divergência entre catálogo e pedido. |
| `governanca` | `[governanca][catalogo-operacional] fechar ciclo com aceite e Project` | Project atualizado com evidência. | Links finais. | Fechar sem seed controlado. |

### `workflow-estados`

| Ciclo | Título | Aceite | Evidência esperada | Riscos |
| --- | --- | --- | --- | --- |
| `repositorio` | `[repositorio][workflow-estados] preparar contrato, owner, repo e submódulo` | Contrato de estados e transições registrado. | PR documental e caminho `aneety-platform/apps/workflow-estados/...`. | Estados divergirem por módulo. |
| `banco` | `[banco][workflow-estados] implementar schema, constraints, índices, RLS e seeds` | Estados e transições têm entidade, origem, destino, permissão e motivo obrigatório. | Migration, rollback e testes de matriz. | Transição sem permissão. |
| `backend` | `[backend][workflow-estados] publicar contrato do BFF/worker` | API valida próxima transição permitida por perfil. | Contrato HTTP e testes de bloqueio. | Fluxo permitir salto indevido. |
| `teste-integracao-api` | `[teste-integracao-api][workflow-estados] validar API integrada ao banco real` | Integração valida transição permitida e negada. | Run integrado com matriz oficial. | Label de governança ainda pendente. |
| `microfrontend` | `[microfrontend][workflow-estados] entregar fluxo visual quando houver UI` | UI orienta próxima ação e bloqueios em linguagem operacional. | Smoke visual de transição permitida/negada. | Mensagem revelar implementação. |
| `documentacao` | `[documentacao][workflow-estados] sincronizar docs e evidências` | Docs registram máquina de estados oficial. | PR documental. | Matriz não versionada. |
| `governanca` | `[governanca][workflow-estados] fechar ciclo com aceite e Project` | Evidência de matriz anexada. | Project atualizado. | Fechar sem bloqueios testados. |

### `sla-capacidade`

| Ciclo | Título | Aceite | Evidência esperada | Riscos |
| --- | --- | --- | --- | --- |
| `repositorio` | `[repositorio][sla-capacidade] preparar contrato, owner, repo e submódulo` | Contrato de SLA, agenda e capacidade registrado. | PR documental e caminho `aneety-platform/apps/sla-capacidade/...`. | Promessa operacional sem capacidade real. |
| `banco` | `[banco][sla-capacidade] implementar schema, constraints, índices, RLS e seeds` | Políticas, agendas e slots têm tenant, ator, data, status e capacidade. | Migration, rollback e testes de disponibilidade. | Overbooking. |
| `jobs` | `[jobs][sla-capacidade] implementar alertas e rotinas idempotentes` | Job de alerta calcula prazos sem duplicar notificação. | Run de job com reexecução segura. | Alerta indevido ou ausente. |
| `backend` | `[backend][sla-capacidade] publicar contrato do BFF/worker` | API consulta capacidade e calcula promessa operacional. | Contrato HTTP e testes de agenda. | Cálculo fora do contrato. |
| `teste-integracao-api` | `[teste-integracao-api][sla-capacidade] validar API integrada ao banco real` | Integração valida capacidade disponível e indisponível. | Run integrado com slots concorrentes. | Label de governança ainda pendente. |
| `microfrontend` | `[microfrontend][sla-capacidade] entregar fluxo visual quando houver UI` | UI mostra disponibilidade e alerta sem jargão técnico. | Smoke visual de agenda e capacidade. | UI prometer prazo não garantido. |
| `documentacao` | `[documentacao][sla-capacidade] sincronizar docs e evidências` | Docs registram regra de prazo e capacidade. | PR documental. | Regra implícita. |
| `governanca` | `[governanca][sla-capacidade] fechar ciclo com aceite e Project` | Evidência de alerta e capacidade anexada. | Project atualizado. | Fechar sem teste concorrente. |

### `orcamentos-precificacao`

| Ciclo | Título | Aceite | Evidência esperada | Riscos |
| --- | --- | --- | --- | --- |
| `repositorio` | `[repositorio][orcamentos-precificacao] preparar contrato, owner, repo e submódulo` | Contrato de orçamento e preço registrado. | PR documental e caminho `aneety-platform/apps/orcamentos-precificacao/...`. | Valor financeiro sem auditoria. |
| `banco` | `[banco][orcamentos-precificacao] implementar schema, constraints, índices, RLS e seeds` | Orçamentos e itens têm valor, moeda, status, expiração e aprovação. | Migration, rollback e testes de linhas. | Cálculo sem explicação. |
| `backend` | `[backend][orcamentos-precificacao] publicar contrato do BFF/worker` | API cria, ajusta, aprova, rejeita e expira orçamento. | Contrato HTTP e testes de status. | Atualização sem versionamento. |
| `teste-integracao-api` | `[teste-integracao-api][orcamentos-precificacao] validar API integrada ao banco real` | Integração valida aprovação e expiração. | Run integrado com orçamento vencido. | Label de governança ainda pendente. |
| `microfrontend` | `[microfrontend][orcamentos-precificacao] entregar fluxo visual quando houver UI` | UI apresenta orçamento, validade e decisão clara. | Smoke visual de aprovação/rejeição. | UI expor cálculo técnico. |
| `documentacao` | `[documentacao][orcamentos-precificacao] sincronizar docs e evidências` | Docs registram critérios de preço e aceite. | PR documental. | Custo externo obrigatório. |
| `governanca` | `[governanca][orcamentos-precificacao] fechar ciclo com aceite e Project` | Evidência financeira anexada. | Project atualizado. | Fechar sem teste de expiração. |

### `comunicacao-operacional`

| Ciclo | Título | Aceite | Evidência esperada | Riscos |
| --- | --- | --- | --- | --- |
| `repositorio` | `[repositorio][comunicacao-operacional] preparar contrato, owner, repo e submódulo` | Contrato de mensagens e notificações registrado. | PR documental e caminho `aneety-platform/apps/comunicacao-operacional/...`. | Mensagem conter dado sensível. |
| `banco` | `[banco][comunicacao-operacional] implementar schema, constraints, índices, RLS e seeds` | Mensagens e notificações têm destinatário, entidade, status e visibilidade. | Migration, rollback e testes de leitura. | Notificação cross-tenant. |
| `jobs` | `[jobs][comunicacao-operacional] implementar distribuição e reprocessamento idempotente` | Job distribui notificações sem duplicar leitura. | Run de job com repetição segura. | Duplicidade de notificação. |
| `backend` | `[backend][comunicacao-operacional] publicar contrato do BFF/worker` | API cria, lista, marca leitura e registra aviso operacional. | Contrato HTTP e testes de status. | Exposição de mensagem privada. |
| `teste-integracao-api` | `[teste-integracao-api][comunicacao-operacional] validar API integrada ao banco real` | Integração valida envio, leitura e permissão. | Run integrado com destinatários distintos. | Label de governança ainda pendente. |
| `microfrontend` | `[microfrontend][comunicacao-operacional] entregar fluxo visual quando houver UI` | UI mostra avisos e mensagens sem jargão técnico. | Smoke visual de caixa de avisos. | Texto final citar adapter externo. |
| `documentacao` | `[documentacao][comunicacao-operacional] sincronizar docs e evidências` | Docs registram escopo de comunicação e retenção. | PR documental. | Integração opcional virar requisito. |
| `governanca` | `[governanca][comunicacao-operacional] fechar ciclo com aceite e Project` | Evidência de permissão anexada. | Project atualizado. | Fechar sem teste de leitura. |

### `suporte-excecoes`

| Ciclo | Título | Aceite | Evidência esperada | Riscos |
| --- | --- | --- | --- | --- |
| `repositorio` | `[repositorio][suporte-excecoes] preparar contrato, owner, repo e submódulo` | Contrato de chamados e exceções registrado. | PR documental e caminho `aneety-platform/apps/suporte-excecoes/...`. | Exceção alterar pedido sem regra. |
| `banco` | `[banco][suporte-excecoes] implementar schema, constraints, índices, RLS e seeds` | Chamados e exceções têm categoria, prioridade, impacto, status e resolução. | Migration, rollback e testes de status. | Caso sensível visível a perfil errado. |
| `backend` | `[backend][suporte-excecoes] publicar contrato do BFF/worker` | API abre, atribui, atualiza e fecha caso com permissão. | Contrato HTTP e testes de resolução. | Fechamento sem motivo. |
| `teste-integracao-api` | `[teste-integracao-api][suporte-excecoes] validar API integrada ao banco real` | Integração valida abertura, atribuição e fechamento. | Run integrado com suporte e exceção. | Label de governança ainda pendente. |
| `microfrontend` | `[microfrontend][suporte-excecoes] entregar fluxo visual quando houver UI` | UI orienta suporte, disputa e correção sem termos técnicos. | Smoke visual de abertura/fechamento. | Texto de impacto confuso ao usuário. |
| `documentacao` | `[documentacao][suporte-excecoes] sincronizar docs e evidências` | Docs registram categorias e impactos. | PR documental. | Fluxo de exceção sem aceite. |
| `governanca` | `[governanca][suporte-excecoes] fechar ciclo com aceite e Project` | Evidência de resolução anexada. | Project atualizado. | Fechar sem auditoria. |

### `privacidade-consentimento`

| Ciclo | Título | Aceite | Evidência esperada | Riscos |
| --- | --- | --- | --- | --- |
| `repositorio` | `[repositorio][privacidade-consentimento] preparar contrato, owner, repo e submódulo` | Contrato de consentimento e privacidade registrado. | PR documental e caminho `aneety-platform/apps/privacidade-consentimento/...`. | Dado sensível sem consentimento. |
| `banco` | `[banco][privacidade-consentimento] implementar schema, constraints, índices, RLS e seeds` | `consent_records` cobre tipo, status, origem, concessão e revogação. | Migration, rollback e testes de revogação. | Consentimento sem trilha. |
| `backend` | `[backend][privacidade-consentimento] publicar contrato do BFF/worker` | API registra, consulta e revoga consentimento com permissão. | Contrato HTTP e testes de bloqueio. | Uso de localização sem consentimento. |
| `teste-integracao-api` | `[teste-integracao-api][privacidade-consentimento] validar API integrada ao banco real` | Integração valida concessão, revogação e bloqueio de uso. | Run integrado com consentimento revogado. | Label de governança ainda pendente. |
| `microfrontend` | `[microfrontend][privacidade-consentimento] entregar fluxo visual quando houver UI` | UI explica consentimento em linguagem clara de usuário. | Smoke visual de conceder/revogar. | Texto jurídico ou técnico incompreensível. |
| `documentacao` | `[documentacao][privacidade-consentimento] sincronizar docs e evidências` | Docs registram retenção, visibilidade e revogação. | PR documental. | Ausência de retenção documentada. |
| `governanca` | `[governanca][privacidade-consentimento] fechar ciclo com aceite e Project` | Evidência de revogação anexada. | Project atualizado. | Fechar sem teste negativo. |

### `demo-seeds`

| Ciclo | Título | Aceite | Evidência esperada | Riscos |
| --- | --- | --- | --- | --- |
| `repositorio` | `[repositorio][demo-seeds] preparar contrato, owner, repo e submódulo` | Contrato de seeds e massa demo registrado. | PR documental e caminho `aneety-platform/apps/demo-seeds/...`. | Dado real em seed pública. |
| `banco` | `[banco][demo-seeds] implementar schema, constraints, índices, RLS e seeds` | `demo_seed_cases` guarda cenário, vertical, descrição e payload sanitizado. | Migration, rollback e teste de sanitização. | Vertical odontológica virar limite do produto. |
| `jobs` | `[jobs][demo-seeds] implementar carga idempotente de massa controlada` | Job carrega seed sem duplicar registros. | Run de carga repetida com contagem estável. | Seed sobrescrever dado operacional. |
| `backend` | `[backend][demo-seeds] publicar contrato do BFF/worker` | API consulta ou aciona demo apenas por permissão controlada. | Contrato HTTP e teste de acesso negado. | Demo disponível em tenant indevido. |
| `teste-integracao-api` | `[teste-integracao-api][demo-seeds] validar API integrada ao banco real` | Integração valida carga e leitura de cenário. | Run integrado com massa sanitizada. | Label de governança ainda pendente. |
| `documentacao` | `[documentacao][demo-seeds] sincronizar docs e evidências` | Docs registram uso de Lia como seed/demo/test mass, não limite de produto. | PR documental. | Reintroduzir contrato antigo como produto final. |
| `governanca` | `[governanca][demo-seeds] fechar ciclo com aceite e Project` | Evidência de sanitização anexada. | Project atualizado. | Fechar sem prova de sanitização. |

## Backlog inicial por ciclo

### `repositorio`

Abrir primeiro as issues `[repositorio][<responsabilidade>] preparar contrato, owner, repo e submódulo` para todas as responsabilidades da matriz. Nenhum repo deve nascer antes de contrato, owner, dados tratados, custo zero, teste e aceite. Prioridade inicial: `tenant-white-label`, `identidade-acesso`, `pedidos-customizados`, `workflow-estados`, `catalogo-operacional`.

### `deploy`

Criar issues de deploy somente após o ciclo `repositorio` ficar verde para a responsabilidade. Aceite mínimo: runtime de custo zero, sem segredo em repositório, caminho de ambiente documentado e plano de rollback. Para MVP, BFFs usam `worker-<nome>` e microfrontends operacionais usam `mfe-<nome>`.

### `publicacao`

Criar issues de publicação após deploy mínimo. Aceite mínimo: URL ou artefato público adequado ao ciclo, sem GitHub Pages como runtime transacional. GitHub Pages pode publicar documentação originada em `Aneety/.github`.

### `banco`

Criar issues `[banco][<responsabilidade>] implementar schema, constraints, índices, RLS e seeds` na ordem de prioridades funcionais. Aceite mínimo: migrations, rollback, constraints, índices, RLS/policies, seeds controlados e testes de leitura/escrita para o nível CRUD declarado.

### `jobs`

Criar issues de job apenas para responsabilidades com rotina assíncrona prevista: `offline-sync`, `logistica-rastreabilidade`, `sla-capacidade`, `comunicacao-operacional`, `demo-seeds`. Aceite mínimo: idempotência, retries, logs operacionais, reprocessamento e isolamento por tenant.

### `backend`

Criar issues `[backend][<responsabilidade>] publicar contrato do BFF/worker` após banco verde para o nível CRUD declarado. Aceite mínimo: contrato HTTP ou evento, validação, autorização, paginação quando aplicável, erros de domínio, auditoria mínima e testes de contrato.

### `teste-integracao-api`

Criar issues `[teste-integracao-api][<responsabilidade>] validar API integrada ao banco real` após backend verde. Aceite mínimo: API integrada ao banco real do ciclo, casos positivos e negativos, isolamento por tenant e evidência do run. Bloqueio normativo: label correspondente deve ser adicionada em `07-governanca-github.md`.

### `microfrontend`

Criar issues `[microfrontend][<responsabilidade>] entregar fluxo visual quando houver UI` após integração de API verde. Aceite mínimo: Single SPA, shadcn/ui e tokens semânticos quando aplicável, estados de carregamento/vazio/erro/sucesso, permissões, acessibilidade básica e nenhuma exposição de fornecedor, banco, runtime, framework, segredo ou ferramenta interna em UI final.

### `smoke`

Criar issues de smoke por responsabilidade quando backend e microfrontend do ciclo estiverem verdes. Aceite mínimo: fluxo crítico real executado, evidência com log, screenshot ou artefato verificável, sem depender de GitHub Pages como runtime operacional.

### `teste`

Criar issues de teste para consolidar cobertura unitária, contrato, integração e regressão do ciclo. Nova cobertura E2E só entra quando todos os gates de `06-ciclos-cobertura.md` estiverem verdes.

### `documentacao`

Criar issues `[documentacao][<responsabilidade>] sincronizar docs e evidências` antes do fechamento de governança. Aceite mínimo: documentos canônicos sincronizados em `Aneety/.github/docs`, README mínimo no repo de implementação e links para evidências.

### `governanca`

Criar issues `[governanca][<responsabilidade>] fechar ciclo com aceite e Project` para cada responsabilidade. Criar também issue específica `[governanca][ciclos] adicionar label ciclo:teste-integracao-api e alinhar roadmap` com aceite: `07-governanca-github.md` atualizado, Project aceitando o ciclo e backlog sem label transitória.

## Sequência CRUD obrigatória por responsabilidade com dados

Cada responsabilidade da matriz deve avançar nesta ordem quando implementar CRUD:

1. Incluir.
2. Pesquisar por `id` ou `eid`.
3. Pesquisar 1 por parâmetros.
4. Pesquisar N paginado por parâmetros.
5. Atualizar 1 por parâmetros.
6. Atualizar N por parâmetros.
7. Excluir 1 por parâmetros por exclusão lógica.
8. Excluir N por parâmetros por exclusão lógica.
9. Executar jobs associados à responsabilidade quando houver.

A etapa só fica verde com contrato, implementação, teste e evidência. Tela, endpoint, tabela ou script isolado não fecha cobertura.

## Bloqueios normativos registrados

| Bloqueio | Impacto | Próxima ação | Issue sugerida |
| --- | --- | --- | --- |
| `07-governanca-github.md` não lista `ciclo:teste-integracao-api` na taxonomia de labels. | Issues de integração de API ficam sem label oficial, apesar do ciclo existir em `06-ciclos-cobertura.md`. | Atualizar governança antes de abrir backlog amplo desse ciclo. | `[governanca][ciclos] adicionar label ciclo:teste-integracao-api e alinhar roadmap` |
| `06-ciclos-cobertura.md` usa `publicação` com acento, enquanto labels usam `ciclo:publicacao`. | Project e relatórios podem divergir se usarem texto literal. | Registrar normalização: label sem acento, texto de negócio com acento. | `[governanca][ciclos] normalizar nomes de ciclos entre docs e labels` |
| Owners das responsabilidades ainda são papéis de governança, não pessoas nomeadas em cada issue. | Issue executável não pode entrar em ciclo sem responsável real. | Nomear owner ao abrir cada issue. | Uma issue de `status:triagem` por responsabilidade até owner real ser informado. |

## Critério de conclusão deste planejamento

Este documento estará apto para uso quando:

- todas as tabelas de `04-modelagem-banco.md` estiverem cobertas uma única vez na matriz;
- cada responsabilidade tiver repo esperado, caminho de submódulo, ciclos, issues, aceite e evidência;
- backlog por ciclo respeitar a ordem de `06-ciclos-cobertura.md`;
- bloqueios normativos estiverem explícitos;
- não houver placeholder textual, segredo, valor sensível ou instrução para usar GitHub Pages como runtime operacional.
