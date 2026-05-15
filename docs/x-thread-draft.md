---
title: "X Thread — Fullstack Agent System"
status: draft
created: 2026-05-14
---

# X Thread Draft — Fullstack Agent System

---

**[1/8]**
Montei um time dev completo com 6 agentes de IA.

Não é um chatbot que responde perguntas.
É um time de engenheiros seniores que pensa, escreve código real e roda testes.

Thread sobre como funciona 🧵

---

**[2/8]**
O sistema tem 6 membros:

🎯 Maestro — decompõe e delega (só planeja, nunca codifica)
⚙️ Stratum — APIs, DB, microsserviços
🎨 Facet — React/Vue, acessibilidade, performance
☁️ Bastion — AWS, Terraform, CI/CD, K8s
🧠 Neuron — ML, ETL, LLMs, sistemas RAG
🔴 Sentinel — revisão de segurança com poder de veto

---

**[3/8]**
O maior erro dos sistemas multi-agente é o Maestro querer fazer tudo.

Aqui o Maestro é "thin" — só planeja e delega.
Os especialistas são "thick" — código, testes, evidência.

Nenhum agente entrega um deliverable sem:
✅ Código
✅ Testes rodando
✅ Log de execução

---

**[4/8]**
Roteamento de modelos por tipo de tarefa:

🔴 Opus 4.7 → decisões arquiteturais, threat modeling, design de RAG
🟡 Sonnet 4.6 → implementação de código, análise técnica
🟢 Haiku 4.5 → testes unitários, YAML, docs, configs

Resultado: ~60–75% de economia vs. usar Opus em tudo.

---

**[5/8]**
Coordenação via File-as-Bus — não via histórico de conversa.

Estado em `progress.md`.
Artefatos em `workspace/`.
Evidência em `docs/logs/`.

Cada agente lê o que precisa, escreve onde está definido.
Contexto mínimo, qualidade máxima.

---

**[6/8]**
O sistema tem uma Constituição — 6 princípios que governam todos os agentes:

1. Evidência antes de código
2. Segurança por padrão
3. Testes não são opcionais
4. Escopo fechado por padrão
5. Falhe cedo, falhe visível
6. O sistema melhora a cada ciclo

O Security tem veto técnico sobre qualquer deploy.

---

**[7/8]**
Como usar com Claude Code:

```bash
# Ativar o time completo (global)
cp Maestro.md ~/.claude/CLAUDE.md

# Ou ativar especialista por projeto
cp Stratum.md ./CLAUDE.md   # repo de API
cp Bastion.md ./CLAUDE.md   # repo de infra
```

Regras condicionais por path: `.claude/rules/*.md`

---

**[8/8]**
Sistema completo no GitHub:
→ github.com/mchlcs/agente-fullstack

Inclui:
📁 6 prompts de agente (formato YAML frontmatter)
📋 Constituição do sistema
🗺️ Mapa de modelos por atividade
📐 Template de ADR
📊 progress.md (File-as-Bus)

Baseado nos padrões: Nexus, AiScientist, AHE.

---

*Notas para revisão:*
- Substituir `github.com/mchlcs/agente-fullstack` com URL real após criar o repo
- Tweet 8: adicionar screenshot do README ou diagrama se disponível
- Considerar separar em 2 threads: técnica (devs) e resultado (builders)
