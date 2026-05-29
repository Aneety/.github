# Estrutura de repositórios — Aneety Platform

## Decisão

O novo projeto deve nascer na org `https://github.com/Aneety`, com `Aneety/ai` como repositório orquestrador de implementação. Os repositórios Lia anteriores viram fontes históricas e referências de aprendizado, não base de implementação contínua.

Todos os projetos/repositórios Aneety devem ser clonados em `/Users/mal/GitHub/Aneety/*`. A regra é sempre parear remoto oficial e clone local: `https://github.com/Aneety/<repo>` -> `/Users/mal/GitHub/Aneety/<repo>`.

Cada responsabilidade ou derivação com implementação própria deve ter repositório próprio na org `Aneety`, clone local em `/Users/mal/GitHub/Aneety/<repo>` e submódulo no repo `Aneety/ai` no caminho correspondente dentro de `aneety-platform/apps/<responsabilidade>/...`.

Toda documentação de arquitetura, catálogo de repositórios, guias, ADRs, especificações e contratos de projeto deve ser mantida no repositório `Aneety/.github` (`https://github.com/Aneety/.github.git`, clone local `/Users/mal/GitHub/Aneety/.github`). Repositórios de implementação devem manter apenas README mínimo com objetivo, status e link para a documentação canônica.

Todo asset reutilizável deve ser mantido no repositório `Aneety/assets` (`https://github.com/Aneety/assets.git`, clone local `/Users/mal/GitHub/Aneety/assets`) com versão SVG canônica. Isso inclui logos, ícones, ilustrações, diagramas, marcas, pictogramas, elementos de UI reutilizáveis e qualquer visual compartilhado entre apps, documentação, apresentações ou materiais operacionais.

## Regra obrigatória de estrutura

Cada responsabilidade deve refletir a estrutura `aneety-platform/apps/<responsabilidade>/<mfe|mc|gw|worker|fe|job|auto|db|pkg|core|int|wl>-<nome>`.

```text
Aneety/ai -> /Users/mal/GitHub/Aneety/ai
  aneety-platform/
    apps/
      <responsabilidade>/
        mfe-<nome>
        mc-<nome>
        gw-<nome>
        worker-<nome>
        fe-<nome>
        job-<nome>
        auto-<nome>
        db-<nome>
        pkg-<nome>
        core-<nome>
        int-<nome>
        wl-<nome>
    tests/
    scripts/
```

A lista acima define categorias possíveis. Não obriga toda responsabilidade a possuir todos os módulos. Cada diretório folha vira submódulo Git quando a implementação própria existir e deve apontar para um clone local em `/Users/mal/GitHub/Aneety/<repo>`.

## Clone local obrigatório

- Clone root local: `/Users/mal/GitHub/Aneety/*`.
- Remoto oficial de qualquer repo: `https://github.com/Aneety/<repo>`.
- Clone local correspondente: `/Users/mal/GitHub/Aneety/<repo>`.
- Exemplos centrais: `/Users/mal/GitHub/Aneety/ai`, `/Users/mal/GitHub/Aneety/.github` e `/Users/mal/GitHub/Aneety/assets`.
- Esta regra é documental neste estágio; não implica mover, clonar ou reescrever submódulos durante esta atualização.

## Documentação central

- `Aneety/.github` é a fonte canônica de documentação de todos os projetos/repositórios e deve estar clonada em `/Users/mal/GitHub/Aneety/.github`.
- `Aneety/.github` deve manter arquitetura, catálogo de repositórios, guias de usuário, documentação de desenvolvedor, ADRs, especificações, contratos e matriz de responsabilidades.
- Repositórios de implementação devem apontar para `Aneety/.github` e não duplicar documentação arquitetural.
- GitHub Pages não é runtime operacional, não hospeda operação transacional e não substitui gateway, BFF ou banco.
- Se GitHub Pages existir para documentação, deve publicar ou apontar conteúdo originado de `Aneety/.github`.

## Assets centrais

- `Aneety/assets` é a fonte canônica de assets reutilizáveis do projeto e deve estar clonada em `/Users/mal/GitHub/Aneety/assets`.
- Todo asset reutilizável deve ter versão SVG versionada nesse repositório.
- Repositórios de implementação devem consumir, copiar em build ou apontar para o SVG canônico, sem manter forks visuais divergentes.
- Assets específicos e descartáveis podem ficar no repo de implementação somente quando não forem reutilizáveis; ao virarem padrão, marca, ícone compartilhado, diagrama recorrente ou elemento visual comum, devem migrar para `Aneety/assets`.
- Alterações visuais compartilhadas devem ser feitas primeiro no SVG canônico e depois propagadas aos apps/documentos.

## Glossário de prefixos

- `worker-<nome>`: Cloudflare Workers/Hono.
- `mfe-<nome>`: microfrontend Single SPA.
- `mc-<nome>`: categoria reservada para runtime próprio futuro, fora do MVP.
- `fe-<nome>`: frontend React.
- `gw-<nome>`: categoria reservada para gateway dedicado futuro, fora do MVP.
- `job-<nome>`: rotina assíncrona compatível com Cloudflare Workers, como Queue consumer, Cron Trigger, Workflow ou Durable Object.
- `auto-<nome>`: automação de repositório, CI ou operação interna; não runtime do produto.
- `db-<nome>`: módulo/diretório de estrutura de dados, migrations, controles de isolamento e seeds.
- `pkg-<nome>`: pacote compartilhado.
- `core-<nome>`: contrato/domínio central compartilhado.
- `int-<nome>`: integração/adapters externos.
- `wl-<nome>`: categoria reservada para workload futuro fora do escopo do MVP.

## Regras de runtime e evolução

- Todos os frontends operacionais devem ser `mfe-<nome>` Single SPA.
- BFFs do MVP devem ser `worker-<nome>` em Cloudflare Workers/Hono.
- Gateway do MVP deve ser `worker-gateway` em Cloudflare Workers/Hono.
- Gateway dedicado futuro fica fora do escopo do MVP atual e exige PR documental aprovado.
- Persistência do MVP deve usar bindings compatíveis com Cloudflare Workers, versionados e documentados em `db-<nome>`.
- Qualquer motor extra-Workers só entra com PR documental aprovado, preservando contratos, custo e plano de saída.
- MVP 100% Workers: `job-*` deve usar apenas mecanismos compatíveis com Workers; não entram Python, containers, VPS, servidor tradicional, cron externo ou runtime persistente fora de Workers.
- `mc-<nome>` é categoria pós-MVP e não substitui o BFF Worker do MVP.
- `fe-<nome>` React é permitido para frontend não operacional ou superfície sem integração Single SPA; frontends operacionais usam `mfe-<nome>`.
- Mapas e rastreabilidade em tempo real devem ser módulos/contratos substituíveis, sem lock-in de fornecedor e sem gasto obrigatório.
- Custo zero sempre é regra de aceite; dependência paga bloqueia ou exige redesenho.

## Responsabilidades

- O nome em `<responsabilidade>` representa um domínio, capacidade ou fronteira operacional, não tecnologia.
- A criação de uma responsabilidade exige contrato, owner, dados tratados, segredos, custo zero sempre, critérios de aceite e plano de teste.
- Uma responsabilidade pode conter microfrontend, BFF, estrutura de dados, pacote, contrato, integração, automação e job quando necessário.
- Dependência entre responsabilidades deve passar por gateway, BFF ou contrato compartilhado versionado.
- Nenhuma responsabilidade deve depender de tabela, segredo ou runtime interno de outra sem contrato explícito.
- Cada responsabilidade implementada em repo próprio deve ser clonada em `/Users/mal/GitHub/Aneety/<repo>`.
- Cada responsabilidade implementada em repo próprio deve ser linkada como submódulo do orquestrador `Aneety/ai`.
- Cada responsabilidade implementada em repo próprio deve estar catalogada e documentada em `Aneety/.github`.
- Cada responsabilidade que usa visual compartilhado deve referenciar os assets SVG canônicos em `Aneety/assets`.

## Responsabilidades funcionais v1 candidatas

As lacunas de produto adicionadas aos requisitos devem ser tratadas como responsabilidades candidatas antes de virar implementação. Nenhum repo novo é obrigatório neste momento; cada uma só vira repo/submódulo quando tiver contrato, owner, dados, custo zero sempre, testes e aceite.

- `onboarding-acesso`: convites, primeiro acesso, recuperação, bloqueio e reativação por papel.
- `gateway-borda`: borda HTTP do MVP com CORS, versionamento de contrato, sessão pública Aneety, roteamento e service bindings entre `worker-gateway` e BFFs `worker-*`.
- `catalogo-operacional`: produtos, serviços, atributos de personalização, preço-base, prazo-base e etapas obrigatórias.
- `workflow-estados`: estados oficiais, transições, permissões, motivos e bloqueios de avanço.
- `sla-capacidade`: prazos, alertas, agenda, disponibilidade, capacidade e raio de atendimento.
- `orcamentos-precificacao`: cotações, aprovação, ajustes de preço, urgência, distância e retrabalho.
- `comunicacao-operacional`: mensagens internas, avisos ao cliente e notificações in-app.
- `suporte-excecoes`: chamados, disputas, correções, retrabalho, devolução operacional, reentrega e reembolso parcial.
- `offline-sync`: fila local, replay, conflito e evidência capturada sem rede.
- `privacidade-consentimento`: consentimento, retenção, visibilidade e exportação de dados sensíveis.
- `auditoria-operacional`: eventos sensíveis, valores antes/depois, motivo e correlação com pedido ou demanda.

## Responsabilidades opcionais do MVP

Gmail e Google SSO entram no MVP como integrações opcionais, separadas e substituíveis. Nenhuma das duas pode virar requisito obrigatório de login, operação ou aceite.

`comunicacao-email` representa a função semântica de envio, recebimento ou registro auxiliar de e-mail. Gmail é somente adapter opcional dessa responsabilidade, via `int-gmail`; pedido, evidência, auditoria e estado operacional permanecem no domínio Aneety.

```text
Aneety/ai
  aneety-platform/
    apps/
      comunicacao-email/
        int-gmail
        worker-email
        db-email
```

`identidade-federada` representa a função semântica de vínculo ou verificação de identidade externa. Google SSO é somente adapter opcional dessa responsabilidade, via `int-google-sso`; sessão final, tenant, perfil e permissões permanecem no modelo próprio Aneety.

```text
Aneety/ai
  aneety-platform/
    apps/
      identidade-federada/
        int-google-sso
        worker-identidade
        db-identidade
```

Os repositórios dessas responsabilidades só devem existir quando houver contrato local, owner, dados tratados, segredos, custo zero sempre, testes de degradação e critérios de aceite. Quando existirem, seguem a regra geral: repo próprio na org `Aneety`, clone local em `/Users/mal/GitHub/Aneety/<repo>`, submódulo em `Aneety/ai` e documentação canônica em `Aneety/.github`.

## Regras de migração

- Lia entra como primeiro tenant/marca dentro da Aneety Platform.
- Fluxos odontológicos de pedidos, moldes, próteses, retirada, entrega e evidências entram como demo, seeds e massas de teste.
- Código atual só deve ser copiado se passar por revisão de contrato, segurança, isolamento por tenant e UI copy.
- Assets atuais só devem ser reutilizados se forem convertidos ou preservados com versão SVG canônica em `Aneety/assets`.
- Não importar a estrutura multi-repo antiga como contrato final; recriar responsabilidades sob `Aneety/ai` com repos próprios e submódulos.
- Documentos atuais continuam úteis como fonte, mas o contrato novo de documentação deve ser escrito em `Aneety/.github`; `Aneety/ai` fica como orquestrador de implementação.
- Cada módulo novo deve ter teste e owner antes de virar dependência de outro módulo.
