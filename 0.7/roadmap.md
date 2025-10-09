# GIO — Roadmap de Evolução (Mínimo Operante em 30 dias)

> Objetivo: Criar um sistema autônomo capaz de **diagnosticar**, **priorizar**, **executar** e **aprender** ações de otimização em campanhas — superando a velocidade e consistência de um gestor humano.

## 📅 Planejamento de 30 dias (3 horas/dia)

---

## **Semana 1 — Fundamentos e Base de Dados**

### 🎯 Meta
Ter um **Feature Store Temporal** funcional, centralizando as métricas de campanhas e preparando o ambiente para diagnósticos.

### ✅ Entregáveis
1. **Feature Store Temporal**
   - Captura diária de dados por entidade: conta, campanha, grupo, anúncio, keyword.
   - Janelas: 1, 3, 7, 14 e 30 dias.
   - Cálculo automático:
     - Média móvel
     - Tendência (slope)
     - Volatilidade (desvio padrão)
     - Z-score e percentil por contexto (conta, tipo, objetivo).
2. **Dicionário de Métricas**
   - Nome, fórmula e unidade de cada métrica.
   - Tratamento de outliers e valores ausentes.

---

## **Semana 2 — Detectores e Biblioteca de Ações**

### 🎯 Meta
Ter o **primeiro conjunto de detectores de padrão** e a **Action Library** inicial em JSON.

### ✅ Entregáveis
1. **Detectores V1**
   - Creative Fatigue (queda de CTR + conv. estável)
   - Query Drift (novos termos irrelevantes com custo alto)
   - Budget Cap (IS lost budget alto com KPIs bons)
   - Rank Loss (IS lost rank alto + CPC ↑)
2. **Esqueleto JSON da Action Library**
   - 10 a 12 ações principais com:
     - Pré-condições
     - Parâmetros
     - Guardrails
     - Rollback
     - KPIs-alvo
   - Ações iniciais:
     - Rebalancear orçamento
     - Mudar estratégia de lance
     - Ajustar lances por keyword
     - Pausar keywords ruins
     - Negativar queries irrelevantes
     - Testar criativos
     - Otimizar asset groups (PMax)

---

## **Semana 3 — Priorizador e Execução Básica**

### 🎯 Meta
Construir o **Next Best Action Prioritizer** e conectar com API Google Ads para execução básica.

### ✅ Entregáveis
1. **Priorizador**
   - Score:
     ```
     Score = Uplift_Esperado × Confiança × Reversibilidade − Esforço − Risco
     ```
   - Throttle: limite de ações/dia por nível.
   - Resolução de conflitos entre ações.
2. **Execução com Governança**
   - Guardrails:
     - Máx. ±15% no orçamento diário
     - Máx. ±20% no lance
     - Brand safety e negativas protegidas
   - Rollback básico:
     - Armazenar valores anteriores para reverter.

---

## **Semana 4 — Avaliação Pós-Ação e Modo Operante**

### 🎯 Meta
Completar o ciclo: **detectar → priorizar → executar → avaliar**.

### ✅ Entregáveis
1. **Avaliação Pós-Ação**
   - Comparar desempenho pré e pós-ação.
   - Classificar impacto: positivo / neutro / negativo.
   - Salvar no histórico de eficácia por ação.
2. **Modo Operante**
   - Modo "Observação": lista ações sugeridas.
   - Modo "Copiloto": aprovações manuais.
   - Modo "Autopiloto": executa ações de alta reversibilidade.

---

## 📊 Linha do Tempo Resumida

| Semana | Meta Principal                         | Entregáveis-Chave                                  |
|--------|----------------------------------------|----------------------------------------------------|
| 1      | Feature Store + Métricas               | Coleta diária, janelas temporais, z-score/percentil|
| 2      | Detectores + Ações                     | Detectores V1 e JSON da Action Library             |
| 3      | Priorizador + Execução                 | Next Best Action, Throttle, Guardrails, Rollback   |
| 4      | Avaliação + Modo Operante              | Avaliador pós-ação, histórico de eficácia, modos   |

---

## 🔄 Ciclo Diário Operante (Versão 1)

1. **Coleta**: Atualiza dados no Feature Store.
2. **Detecção**: Executa detectores e gera eventos.
3. **Geração de Candidatos**: Filtra ações possíveis via Action Library.
4. **Priorização**: Ordena por score, aplica throttle e resolve conflitos.
5. **Execução**: Aplica no Google Ads (dry-run ou real).
6. **Avaliação Agendada**: Marca ação para revisão após janela definida.

---

## 🛠 Requisitos Técnicos

- **Backend**: Python + FastAPI
- **Banco**: Supabase / Postgres
- **Jobs**: N8N ou Cronjobs
- **Integração**: Google Ads API v20
- **Formato de Config**: JSON/YAML para Actions e Guardrails

---

## 🚀 Critério de Sucesso do Mínimo Operante

- Feature Store atualizado diariamente.
- Pelo menos **4 detectores** funcionando.
- Action Library com **mínimo de 10 ações**.
- Priorizador aplicando score + throttle.
- Execução básica com rollback.
- Avaliação pós-ação salvando resultados.
- Operando no modo "Copiloto" com sugestões diárias.

---
