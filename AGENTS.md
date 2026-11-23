# Instruções para agentes: Medvita Pro

## Contrato do núcleo e da suíte

Valem integralmente aqui, e não são repetidos:

- o `AGENTS.md` do Skeleton, na tag da release do núcleo instalada (`SKELETON_REF` em `.github/workflows/ci.yml`): <https://github.com/alaorneto/skeleton/blob/v0.3.0/AGENTS.md>;
- o `AGENTS.md` do Medvita Core, na tag da release instalada (`MEDVITA_CORE_REF` em `.github/workflows/ci.yml`): <https://github.com/alaorneto/medvita-core/blob/v0.1.0/AGENTS.md>. As regras da suíte (camadas, acesso por contêiner, relações entre apps, dinheiro, datas, texto visível, interface, dados pessoais e de saúde, retenção, testes) são as de lá.

Em divergência, vale o do núcleo; depois, o do Medvita Core. Este arquivo guarda só o que é próprio do Medvita Pro.

## Ordem de leitura

1. `README.md` e este arquivo.
2. `docs/architecture.md`.
3. Os `AGENTS.md` acima e o `docs/extension-points.md` do Medvita Core, que diz por onde uma app se pluga.
4. O `AGENTS.md` e a `docs/spec.md` da app em que vai trabalhar, quando ela existir.

## Fronteiras do repositório

- A raiz não é pacote Python. Cada app é um diretório com o nome do pacote (`med_<nome>`) e o `manifest.json` na raiz dele; `app_id` `io.medvita.<nome>`, `publisher` `katua-tech`.
- As apps daqui dependem das apps do Medvita Core e, entre si, só no sentido declarado em `docs/architecture.md`.
- Uma app só importa de outra o `service_api` dela. O sentido contrário é feito por eventos de domínio do núcleo e pelos registries exportados no `service_api`.
- Quando uma app precisa de um ponto de extensão que o Medvita Core não tem, a mudança é uma issue no Medvita Core; nunca se contorna lendo modelo de outra app.
- `tests/` da raiz guarda os cenários que cruzam apps; `tools/` guarda scripts de desenvolvimento, que nunca entram num pacote.

## Integrações externas

- Toda integração (governo, operadora, provedor de mensagem, pagamento, certificado, vídeo) começa por uma issue de investigação que termina num ADR: canal oficial, credencial exigida, custo, limites e o que fica fora.
- O código fala com o serviço externo por uma interface de backend da app; os testes usam um dublê. O CI nunca chama serviço real.
- Credencial (certificado, token de provedor) fica cifrada ou fora do banco e nunca aparece em log, evento, mensagem de erro, URL ou nome de arquivo. Senha gov.br de usuário nunca é guardada.
- Chamada externa roda em job do núcleo, com idempotência pelo `sysid` do registro e nova tentativa; o consumo cobrável segue a regra de `docs/billing.md` do núcleo.

## Rastreabilidade

O fluxo deste repositório é o skill `dev-workflow` (`.claude/skills/dev-workflow/`, configurado em
`.github/dev-workflow.toml`). Carregue o skill e siga-o (no Claude Code, pela ferramenta Skill; em
outro agente ou à mão, lendo `.claude/skills/dev-workflow/SKILL.md`) sempre que:

- entrar no modo de planejamento ou escrever um plano: ele termina com a seção "Itens do GitHub";
- um plano for aceito: as issues e o epic são criados antes de qualquer edição;
- for começar, sem plano, qualquer mudança em arquivo versionado (código, testes, documentação, CI,
  dependências);
- for criar ou atualizar uma issue ou um epic, criar branch, commitar ou abrir PR;
- for decidir se um PR publica versão e com que nível, ou mexer em release, changelog ou tag;
- for fechar uma issue.

Perguntas e investigações sem mudança de arquivo não precisam do skill. Valem sempre, mesmo sem ele:
nenhuma mudança versionada sem issue; nunca `--no-verify`; ninguém edita a versão nem o changelog à mão.

Próprio deste repositório:

- Issues e PRs têm a seção "Segurança e contrato do AGENTS.md"; o label `security` marca impacto em isolamento, autorização, dados de saúde, auditoria ou segredos.
- As apps daqui andam num só trem de versão: a automação escreve o mesmo número em todos os manifestos (cada app nova entra em `[[versioning.files]]` no epic dela). Ninguém edita `version` nem o changelog.
- Um PR por epic; cada epic parte da branch do anterior enquanto o anterior não está na `main`.

## Proibido

- Copiar código do núcleo ou do Medvita Core para o repositório, ou importar módulo deles fora das superfícies públicas.
- Abrir `system_context` num serviço de app, usar SQL cru ou relação reversa sem filtro.
- Excluir fisicamente qualquer registro.
- Acrescentar biblioteca de terceiros sem issue própria.
