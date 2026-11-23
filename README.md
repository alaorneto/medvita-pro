# Medvita Pro

[![CI](https://github.com/alaorneto/medvita-pro/actions/workflows/ci.yml/badge.svg)](https://github.com/alaorneto/medvita-pro/actions/workflows/ci.yml)

Medvita Pro é o pacote avançado da suíte Medvita, sobre o [Skeleton](https://github.com/alaorneto/skeleton). Ele se instala por cima do [medvita-core](https://github.com/alaorneto/medvita-core); cada app é publicada como um pacote `.skapp` assinado, contratada sozinha e ativada por organização.

## Apps planejadas

Nenhuma app foi implementada ainda: cada uma nasce no epic dela (veja as issues `epic`).

| Pacote e label | `app_id` | Nome exibido | Para quê |
|---|---|---|---|
| `med_health_receipt` | `io.medvita.health_receipt` | Receita Saúde | Recibo do Receita Saúde emitido para cada consulta paga por pessoa física |
| `med_reminders` | `io.medvita.reminders` | Lembretes | Lembrete, confirmação e lista de espera por WhatsApp, SMS e e-mail |
| `med_signature` | `io.medvita.signature` | Assinatura digital | Cofre de certificados e assinatura ICP-Brasil sobre o selo dos registros |
| `med_prescription` | `io.medvita.prescription` | Prescrição | Receita eletrônica, inclusive de controle especial |
| `med_payout` | `io.medvita.payout` | Repasse | Repasse ao profissional por regra, com fechamento por período |
| `med_insurance` | `io.medvita.insurance` | Convênios | Guias e lotes TISS, glosas e conciliação com as operadoras |
| `med_online_payments` | `io.medvita.online_payments` | Pagamento online | Link de Pix e cartão, TEF e conciliação bancária |
| `med_portal` | `io.medvita.portal` | Portal do paciente | Agendamento online, pré-consulta, documentos e recibos |
| `med_packages` | `io.medvita.packages` | Pacotes | Pacotes de sessões, planos recorrentes e orçamentos |
| `med_assistant` | `io.medvita.assistant` | Assistente | Transcrição e rascunho do atendimento (opcional, depois de decisão de LGPD) |

O núcleo e as apps do medvita-core não são copiados para cá: entram no ambiente como dependências instaladas.

## Como desenvolver

As regras para agentes e desenvolvedores estão no `AGENTS.md`; a arquitetura em `docs/architecture.md`. O guia de ambiente e testes (`docs/development.md`) chega com o epic de bootstrap.

## Licença

Software proprietário da Katuá Tech. Todos os direitos reservados; veja `LICENSE`.
