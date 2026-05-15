---
title: "Standards & Anti-Patterns"
version: 2.0.0
updated: 2026-05-14
---

# Padrões e Anti-Padrões — Fullstack Agent System

## Padrões universais (todos os agentes)

### Output format obrigatório

Todo deliverable de especialista deve ter três seções:

```markdown
## Deliverable
[Código, config ou artefato completo]

## Evidence
[Testes passando, scan output, log de execução, métricas]

## State Update
[O que mudou: arquivos, dependências, estado de progress.md]
```

Deliverable sem Evidence = entrega incompleta. Maestro rejeita e re-delega.

### File-as-Bus

Estado do projeto vive em arquivos, não em histórico de conversa:
- `docs/progress.md` — estado atual, ciclo atual, bloqueios
- `workspace/` — artefatos gerados (código, IaC, notebooks)
- `docs/logs/` — evidência de execução por domínio

Agentes leem o que precisam, escrevem onde está definido no frontmatter.

### Secrets

Nunca em código. Nunca em logs. Nunca em respostas de API.
Sempre: variáveis de ambiente, AWS Secrets Manager, HashiCorp Vault, SOPS.

---

## Backend

### Padrões
- Validação de input em toda boundary externa (Zod, Pydantic, Joi)
- HTTP semântico: 200, 201, 400, 401, 403, 404, 422, 500
- Logs estruturados JSON com nível adequado
- Queries parametrizadas — sem concatenação de strings SQL
- Migrations com `up()` e `down()`

### Anti-padrões
- `console.log` em produção
- `any` em TypeScript sem justificativa
- Hardcoded IPs, secrets, connection strings
- N+1 não endereçado
- Query sem índice em campo filtrado

---

## Frontend

### Padrões
- TypeScript estrito — sem `any` implícito
- Semantic HTML — `<header>`, `<nav>`, `<main>`, `<article>`
- Touch targets ≥ 44×44px
- `alt` em toda `<img>`
- `prefers-reduced-motion` respeitado

### Anti-padrões
- `!important` sem comentário
- `<div>` onde existe semântica adequada
- Inline styles para lógica que pertence ao CSS
- Eventos de click em `<span>` ou `<div>` sem `role`
- Body text < 16px

---

## Bastion

### Padrões
- Tags obrigatórias: `Project`, `Environment`, `Owner`, `CostCenter`
- IAM least privilege — nenhuma permissão `*` sem justificativa
- Remote state no Terraform (S3 + DynamoDB locking)
- Multi-AZ para produção
- Resource limits em todo container Kubernetes

### Anti-padrões
- Credenciais hardcoded em IaC
- Infraestrutura sem alertas de observabilidade
- `terraform apply` sem `plan` revisado
- Recursos de produção sem backup configurado
- Security group com `0.0.0.0/0` em inbound sem justificativa

---

## Neuron

### Padrões
- Pipelines idempotentes — re-executáveis sem duplicar dados
- Schema de entrada e saída documentado
- Versionamento de modelos e datasets
- Quality checks (Great Expectations / Soda) em entrada e saída
- Linhagem de dados rastreável

### Anti-padrões
- Dataset sobrescrito sem backup
- Modelo em produção sem métricas de baseline
- PII sem anonimização (LGPD)
- Pipeline que falha silenciosamente
- RAG sem validação de qualidade de retrieval

---

## Sentinel

### Padrões
- PASS/FAIL com evidência — nunca PASS com ressalva informal
- CVSS v3.1 em toda vulnerabilidade reportada
- ADR criado para toda decisão nova de arquitetura de segurança
- Dependency scanning em CI/CD

### Anti-padrões
- Aprovar com "pode resolver depois" em severidade Alta ou Crítica
- Desabilitar controles de segurança como workaround
- Review sem scan ou checklist executado
- Secrets em qualquer arquivo versionado — sem exceção
