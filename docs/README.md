# Aneety Platform — documentação canônica

Status: **MVP Lia encerrado como linha de implementação; Aneety Platform inicia como sucessor.**

Este diretório é a documentação canônica da plataforma Aneety e registra a estratégia para descontinuar o MVP Lia sem apagar código, histórico, evidências, decisões ou aprendizados. A implementação nova deve nascer na org `https://github.com/Aneety`, com `Aneety/ai` como monorepo único de implementação. Os repositórios centrais do contrato atual devem ser clonados em `/Users/mal/GitHub/Aneety/*`, com foco em `Aneety/ai`, `Aneety/.github` e `Aneety/assets`. Cada responsabilidade ou derivação com implementação própria deve viver como módulo interno no caminho correspondente em `aneety-platform/apps/<responsabilidade>/...`.

## Índice

1. [Estratégia de descontinuação do MVP](00-estrategia-descontinuacao-mvp.md)
2. [Arquitetura](01-arquitetura.md)
3. [Requisitos](02-requisitos.md)
4. [Processos](03-processos.md)
5. [Modelagem de banco de dados](04-modelagem-banco.md)
6. [Estrutura de repositórios](05-estrutura-repositorios.md)
7. [Ciclos de desenvolvimento por cobertura](06-ciclos-cobertura.md)
8. [Governança GitHub](07-governanca-github.md)
9. [Planejamento de ciclos e issues](08-planejamento-ciclos-implementacao-repositorios.md)
10. [Painel operacional em Markdown](project/index.md)

## Fronteira dos documentos

- `01-arquitetura.md`: decisões estruturais permanentes, runtime, módulos internos, NFR estruturais, serviços externos e limites de fornecedor.
- `02-requisitos.md`: requisitos de produto, fluxos complementares v1, requisitos técnicos e critérios verificáveis de aceite.
- `03-processos.md`: modo de execução, fluxos operacionais, ordem de trabalho e gates operacionais; não deve ser fonte exclusiva de regra normativa.
- `04-modelagem-banco.md`: modelagem conceitual, índices mínimos, isolamento e regras de acesso.
- `05-estrutura-repositorios.md`: catálogo estrutural de repositórios centrais, monorepo, clones locais e regras de runtime do MVP.
- `06-ciclos-cobertura.md`: ordem fixa dos ciclos, sequência CRUD e gates de cobertura/E2E.
- `07-governanca-github.md`: governança operacional de issues, PRs e do painel Markdown em `docs/project`; não substitui contrato, arquitetura, requisitos, processos ou evidências.
- `08-planejamento-ciclos-implementacao-repositorios.md`: backlog operacional derivado dos documentos normativos, com matriz de responsabilidades, ciclos e aceite.
- `docs/project/`: painel operacional versionado, com índice executivo e um arquivo por responsabilidade ativa.

## Fontes aproveitadas

- Repositórios e docs Lia anteriores — fonte histórica e evidência, não contrato do novo produto.
- `README.md` — estado atual do portal integrador e publicação por domínio.
- `docs/MARKETPLACE_OPERACIONAL.md` — fluxo de marketplace operacional.
- `docs/COVERAGE_MATRIX.md` — lacunas e critérios de cobertura.
- Guias mobile, desktop e administração — evidências de fluxos, telas e critérios de aceite.
- Repositórios Lia anteriores — evidências de Worker/Hono, persistência compatível com Workers, shadcn/ui, E2E, core, apps e publicação.
- Fluxos odontológicos de pedidos, moldes, próteses, retirada, entrega e evidências — carga inicial de demonstração, seeds e massas de teste.

## Decisões travadas

- Nome estratégico: **Aneety Platform**.
- Produto: white-label genérico para produto/serviço customizado com consumidor, produtor, entrega, evidências, qualidade, mapas e rastreabilidade em tempo real.
- Lia: primeiro tenant/marca, não nome rígido da plataforma.
- Org GitHub: `https://github.com/Aneety`.
- Clone root local obrigatório: `/Users/mal/GitHub/Aneety/*`.
- Regra remoto/local dos repositórios centrais: `https://github.com/Aneety/ai` -> `/Users/mal/GitHub/Aneety/ai`, `https://github.com/Aneety/.github` -> `/Users/mal/GitHub/Aneety/.github` e `https://github.com/Aneety/assets` -> `/Users/mal/GitHub/Aneety/assets`.
- Monorepo de implementação: `Aneety/ai` (`https://github.com/Aneety/ai.git`, clone local `/Users/mal/GitHub/Aneety/ai`).
- Repositório canônico de documentação de todos os projetos/repositórios: `Aneety/.github` (`https://github.com/Aneety/.github.git`, clone local `/Users/mal/GitHub/Aneety/.github`).
- Repositório canônico de assets reutilizáveis: `Aneety/assets` (`https://github.com/Aneety/assets.git`, clone local `/Users/mal/GitHub/Aneety/assets`), sempre com versão SVG para logos, ícones, ilustrações, diagramas, marcas, pictogramas e demais assets reutilizáveis.
- Estrutura: responsabilidades e derivações implementadas como módulos internos no monorepo `Aneety/ai`.
- Regra de diretório: `aneety-platform/apps/<responsabilidade>/<mfe|mc|gw|worker|fe|job|auto|db|pkg|core|int|wl>-<nome>`.
- Documentação: guias de usuário, documentação de desenvolvedor, especificações, ADRs, arquitetura e catálogo de repositórios devem viver em `Aneety/.github`; o monorepo de implementação mantém apenas README mínimo com link para essa fonte canônica.
- Assets: todo asset reutilizável do projeto deve ser versionado em SVG no repositório `Aneety/assets`; o monorepo de implementação deve consumir ou referenciar esse acervo, não manter cópias divergentes.
- Frontends operacionais: microfrontends Single SPA em `mfe-<nome>`.
- BFFs MVP: `worker-<nome>` em Cloudflare Workers/Hono.
- Gateway MVP: `worker-gateway`.
- Gateway dedicado futuro: somente pós-MVP e com PR documental aprovado.
- Persistência MVP: bindings compatíveis com Cloudflare Workers, definidos por responsabilidade (`D1`, `KV`, `R2`, `Durable Objects`, `Queues`, `Workflows`) sem banco gerenciado externo obrigatório.
- Persistência futura: qualquer motor extra-Workers exige PR documental aprovado, preservando contratos, isolamento e plano de saída.
- Autenticação: identidade, credenciais, sessões e permissões próprias no modelo de dados da plataforma, via gateway/BFF, sem provedor externo obrigatório.
- Serviços externos por semântica: Cloudflare, GitHub, persistência, mapas ou qualquer fornecedor equivalente são meios substituíveis; requisitos devem declarar função, dados, segredos, custo, contrato local, testes e plano de saída.
- Custo: custo zero sempre; dependência paga bloqueia ou exige redesenho.
- Este repositório é a fonte oficial de documentação; a nova implementação nasce limpa no monorepo `Aneety/ai`.
