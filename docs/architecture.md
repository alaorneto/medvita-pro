# Arquitetura

Medvita Pro é um repositório com várias apps do Skeleton. Cada app é um pacote publicado sozinho (`.skapp`), contratado sozinho e ativado por organização; todas andam num só trem de versão.

## Lugar na suíte

```text
add-ons de especialidade
        ▲
Medvita Business   (clínica, pessoa jurídica)
        ▲
Medvita Pro        (avançado)
        ▲
Medvita Core       (pacientes, agenda, prontuário, financeiro)
        ▲
Skeleton           (núcleo)
```

A seta aponta para quem se instala por cima. Uma camada usa a de baixo pelo `service_api`, pelos eventos de domínio e pelos registries (`docs/extension-points.md` do Medvita Core); a de baixo nunca conhece a de cima.

## Árvore do repositório

```text
medvita-pro/                <- raiz do repositório git; não é pacote Python
  AGENTS.md  LICENSE  README.md  pyproject.toml
  .github/             <- dev-workflow, CI, modelos de issue e PR
  .claude/skills/dev-workflow/
  docs/                <- documentação do pacote
  tools/  tests/       <- chegam com o epic de bootstrap
  med_<nome>/          <- uma app por diretório, no formato das apps do Medvita Core
```

## Apps planejadas

| Pacote e label | `app_id` | Nome exibido | Depende de |
|---|---|---|---|
| `med_health_receipt` | `io.medvita.health_receipt` | Receita Saúde | Financeiro |
| `med_reminders` | `io.medvita.reminders` | Lembretes | Pacientes, Agenda médica |
| `med_signature` | `io.medvita.signature` | Assinatura digital | Prontuário |
| `med_prescription` | `io.medvita.prescription` | Prescrição | Prontuário, Assinatura digital |
| `med_insurance` | `io.medvita.insurance` | Convênios | Financeiro, Agenda médica |
| `med_online_payments` | `io.medvita.online_payments` | Pagamento online | Financeiro |

Cada dependência é declarada em `dependencies` do manifesto da app, com a faixa da versão instalada.
