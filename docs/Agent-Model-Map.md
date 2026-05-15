---
title: "Agent Model Map"
version: 2.0.0
updated: 2026-05-14
---

# Mapa de Modelos — Fullstack Agent System

Roteamento por tipo de atividade para maximizar qualidade e minimizar custo de tokens.
**Estimativa de economia: ~60–75% vs. usar Opus em tudo.**

## Tabela de roteamento

| Atividade | Modelo | Agente |
|---|---|---|
| Planejamento e decomposição de requisitos complexos | claude-opus-4-7 | Maestro |
| Threat modeling, Zero Trust, análise de conformidade | claude-opus-4-7 | Sentinel |
| Design de sistemas RAG, arquitetura de dados | claude-opus-4-7 | Neuron |
| Revisão de segurança crítica (auth/dados/infra) | claude-opus-4-7 | Sentinel |
| Implementação de APIs REST/GraphQL | claude-sonnet-4-6 | Stratum |
| Modelagem de banco de dados e migrations | claude-sonnet-4-6 | Stratum |
| Refatoração de código legado | claude-sonnet-4-6 | Stratum |
| Implementação de auth/autorização | claude-sonnet-4-6 | Stratum |
| Criação de componentes React/Vue complexos | claude-sonnet-4-6 | Facet |
| Performance web (Core Web Vitals) | claude-sonnet-4-6 | Facet |
| Auditoria de acessibilidade WCAG | claude-sonnet-4-6 | Facet |
| Módulos IaC Terraform/Pulumi | claude-sonnet-4-6 | Bastion |
| Design de pipelines CI/CD | claude-sonnet-4-6 | Bastion |
| Observabilidade (Prometheus/Grafana) | claude-sonnet-4-6 | Bastion |
| FinOps: análise e otimização de custos | claude-sonnet-4-6 | Bastion |
| Implementação de pipelines ETL/ELT | claude-sonnet-4-6 | Neuron |
| Feature engineering e análise exploratória | claude-sonnet-4-6 | Neuron |
| Code review de segurança (SAST) | claude-sonnet-4-6 | Sentinel |
| Políticas IAM e RBAC | claude-sonnet-4-6 | Sentinel |
| Testes unitários e de integração | claude-haiku-4-5 | Stratum |
| Documentação OpenAPI/JSDoc | claude-haiku-4-5 | Stratum |
| Seeds e dados de teste | claude-haiku-4-5 | Stratum |
| CSS utilities e variantes de estilo | claude-haiku-4-5 | Facet |
| Testes E2E com Playwright | claude-haiku-4-5 | Facet |
| Storybook stories | claude-haiku-4-5 | Facet |
| Dockerfiles otimizados | claude-haiku-4-5 | Bastion |
| Manifests Kubernetes (Deployment/Service/Ingress) | claude-haiku-4-5 | Bastion |
| Runbooks e playbooks de incident | claude-haiku-4-5 | Bastion |
| Relatórios de métricas e KPIs | claude-haiku-4-5 | Neuron |
| Docstrings e documentação de pipelines | claude-haiku-4-5 | Neuron |
| Security headers e configs WAF | claude-haiku-4-5 | Sentinel |
| Checklists de security review | claude-haiku-4-5 | Sentinel |

## Regra de decisão

```
if    raciocínio sistêmico complexo, alto impacto, threat modeling  → opus-4-7
elif  geração de código, análise técnica, design de arquitetura     → sonnet-4-6
elif  padrão conhecido, output < 500 tokens, config repetitiva      → haiku-4-5
else                                                                 → sonnet-4-6
```

## Modelos atuais (2026-05-14)

| Tier | Model ID | Uso |
|---|---|---|
| Opus | claude-opus-4-7 | Decisões arquiteturais, segurança crítica, IA/dados |
| Sonnet | claude-sonnet-4-6 | Implementação geral, código, análise |
| Haiku | claude-haiku-4-5-20251001 | Tarefas repetitivas, docs, configs simples |
