---
tags: [agente-fullstack, sistema-multi-agente, claude, time-dev, engenharia]
versao: "2.0.0"
criado: 2026-05-14
---

# Fullstack Agent System

Time de engenharia sênior composto por 6 agentes especializados, orquestrados por um Orchestrator central. Cada agente é um profissional de TI sênior — não um professor. Os agentes pensam, escrevem código compilável, fazem integrações e executam testes de validação.

**Coordenação via File-as-Bus**: estado em arquivos, não em histórico de conversa.  
**Evidência obrigatória**: nenhum deliverable sem testes ou logs de execução.  
**Security com veto técnico**: pode bloquear qualquer deploy.

---

## Estrutura

```
Fullstack Agent System/
├── 00-SYSTEM-PROMPTS/
│   ├── Orchestrator.md     ← Maestro: planejador central (opus-4-7)
│   ├── Backend-Dev.md      ← Stratum: APIs, DB, microsserviços (sonnet-4-6)
│   ├── Frontend-Dev.md     ← Facet: UI/UX, React/Vue, a11y (sonnet-4-6)
│   ├── Infra-Cloud.md      ← Bastion: AWS, Terraform, CI/CD (sonnet-4-6)
│   ├── Data-AI.md          ← Neuron: ML, ETL, LLMs, RAG (opus-4-7)
│   └── Security.md         ← Sentinel: AppSec, OWASP, compliance (opus-4-7)
├── docs/
│   ├── Constitution.md     ← 6 princípios que governam todos os agentes
│   ├── Agent-Model-Map.md  ← Roteamento: atividade → modelo → agente
│   ├── Standards-Anti-Patterns.md
│   └── progress.md         ← Estado do sistema (File-as-Bus)
└── adr/
    └── 0000-template.md    ← Template para Architecture Decision Records
```

---

## Mapa de Modelos

| Agente | opus-4-7 | sonnet-4-6 | haiku-4-5 |
|---|---|---|---|
| Maestro | Planejamento complexo | — | — |
| Stratum | — | APIs, DB, auth, refatoração | Testes, docs, seeds |
| Facet | — | Componentes, performance, a11y | CSS, E2E, Storybook |
| Bastion | — | IaC, CI/CD, observabilidade | Dockerfiles, YAML, runbooks |
| Neuron | Arquitetura RAG, ML design | ETL, análise, features | Relatórios, docstrings |
| Sentinel | Threat modeling, compliance | Code review, IAM | Headers, configs, checklists |

**Estimativa de economia: ~60–75% vs. usar Opus em tudo.**

---

## Como usar

### Claude Code — Projeto específico

```bash
# Ativar Maestro como CLAUDE.md do projeto
cp 00-SYSTEM-PROMPTS/Orchestrator.md ./CLAUDE.md

# Agente especialista para repositório específico
cp 00-SYSTEM-PROMPTS/Backend-Dev.md ./CLAUDE.md     # repo backend (Stratum)
cp 00-SYSTEM-PROMPTS/Frontend-Dev.md ./CLAUDE.md    # repo frontend (Facet)
cp 00-SYSTEM-PROMPTS/Infra-Cloud.md ./CLAUDE.md     # repo infra (Bastion)
```

### Regras condicionais por path

```bash
# Backend
.claude/rules/services.md      # paths: ["src/**/*.service.ts"]
.claude/rules/tests.md         # paths: ["**/*.test.ts", "**/*.spec.ts"]

# Frontend
.claude/rules/components.md    # paths: ["src/components/**/*.tsx"]
.claude/rules/styles.md        # paths: ["**/*.css", "**/*.scss"]

# Infra
.claude/rules/terraform.md     # paths: ["**/*.tf", "**/*.tfvars"]
.claude/rules/kubernetes.md    # paths: ["k8s/**/*.yaml"]

# Data
.claude/rules/dbt.md           # paths: ["dbt/**/*.sql", "dbt/**/*.yml"]
.claude/rules/ml.md            # paths: ["ml/**/*.py"]

# Security
.claude/rules/auth.md          # paths: ["src/auth/**", "**/middleware/**"]
```

### Hierarquia de carregamento no Claude Code

```
~/.claude/CLAUDE.md           ← Maestro (global, opcional)
./CLAUDE.md                   ← Agente especialista (projeto)
.claude/rules/*.md            ← Regras condicionais por path
```

---

## Fluxo de trabalho

```
Maestro lê progress.md
  └─→ Decompõe tarefa em sub-tarefas com critério de done
      ├─→ Stratum (APIs, DB, microsserviços)
      ├─→ Facet (UI, componentes, a11y)
      ├─→ Bastion (IaC, CI/CD, deploy)
      ├─→ Neuron (pipelines, ML, RAG)
      └─→ Sentinel (revisão obrigatória em auth/dados/infra)
          ↓
      Cada especialista entrega:
        Deliverable + Evidence + State Update
          ↓
      Maestro valida Evidence, atualiza progress.md
```

---

## Constituição (resumo)

1. **Evidência antes de código** — spec existe antes de implementar; Evidence é obrigatória
2. **Segurança por padrão** — Security tem veto em qualquer deploy
3. **Testes não são opcionais** — deliverable sem testes = entrega incompleta
4. **Escopo fechado por padrão** — cada agente faz exatamente o que foi delegado
5. **Falhe cedo, falhe visível** — erros vão para logs, nunca silenciosos
6. **Sistema melhora a cada ciclo** — hill-climbing via Vault SO (hill, review, guard)

---

## Evolução do sistema

Baseado no Nexus Agent System e nas seguintes fontes:
- AiScientist (thin control + thick state, File-as-Bus)
- Agentic Harness Engineering (memória > prompts)
- Multi-Agent Orchestration patterns (Prep Line, Gordon Ramsay)
- RL Conductor (model routing por tipo de tarefa)

Versão anterior: Professor Fullstack (v1.0) — modelos 4.5, sem evidência obrigatória, framing educacional.
