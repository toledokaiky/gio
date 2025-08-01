# 🚀 GIO – Search

> **Este guia documenta todas as capacidades, decisões automáticas e indicadores analisados pela GIO em campanhas Search no Google Ads.**  
> Use este material como referência oficial para desenvolvimento, revisão de lógica e expansão das funcionalidades.

Cada seção detalha:  
- **Ações e decisões automáticas/recomendadas**  
- **Métricas analisadas**  
- **Indicadores derivados utilizados para decisão (tendências, z-scores, percentis, etc.)**


---

## 📚 Índice

- [1. Campanha](#1-campanha)
- [2. Grupos de Anúncios](#2-grupos-de-anúncios)
- [3. Anúncios](#3-anúncios)
- [4. Palavras-chave](#4-palavras-chave)
- [5. Extensões de Anúncio](#5-extensões-de-anúncio)
- [6. Público e Segmentação](#6-público-e-segmentação)
- [🧠 Notas Gerais e Boas Práticas](#notas-gerais-e-boas-práticas)

---

## 1. 🎯 Campanha

### ✅ Decisões & Otimizações

- Ajuste automático do **orçamento diário** conforme performance, rebalanceando o orçamento de todas as campanhas.
- Troca de **estratégia de lances**: Maximizar Conversões ↔ CPA alvo ↔ ROAS alvo.
- Ajuste de CPA, ROAS desejado ou CPC desejado quando pertinente.
- **Ajuste de geolocalização** e idioma conforme dados de conversão.
- Pausa de campanhas de **baixo desempenho** ou alto custo sem retorno.
- **Criação de novas campanhas** para clusters de público ou palavras-chave ainda não explorados, quando fizer sentido e o orçamento for pertinente.
- Otimização dos **horários e datas de veiculação**.
- Redistribuição de orçamento para maximizar ROI ou Conversões.

### 📊 Métricas Analisadas

- CPA, ROAS, Orçamento diário, Gasto total
- Volume de conversões
- Compartilhamento de impressões
- Taxa de conversão
- Distribuição por localização, idioma e horário

#### 🔎 Indicadores Derivados

- Tendências de 7, 14, 30 dias (variações temporais)
- **Z-score** vs. média da conta
- Desvio padrão de custos/conversões por região
- Percentis (ex: CPA p90)
- Comparativo com metas (CPA/ROAS alvo)

---

## 2. 🗂️ Grupos de Anúncios

### ✅ Decisões & Otimizações

- **Criação de novos grupos** por temas ou clusters detectados.
- Redistribuição de palavras-chave para aumentar relevância e qualidade.
- Pausa de grupos de **desempenho baixo**.
- Ajuste de lances por grupo conforme performance.
- Balanceamento do número de grupos ativos.

### 📊 Métricas Analisadas

- CTR médio do grupo
- Conversões por grupo
- Custo por grupo
- Distribuição de impressões e custos
- Relevância interna das palavras-chave

#### 🔎 Indicadores Derivados

- Tendência temporal de CTR/conversão
- **Z-score** do grupo vs. demais
- Variância entre grupos
- **Score de clusterização** (similaridade semântica)

---

## 3. 📝 Anúncios

### ✅ Decisões & Otimizações

- Criação de **novos anúncios** ao detectar queda de CTR ou estagnação.
- Pausa de anúncios com performance ruim.
- Teste/substituição automática de títulos e descrições.
- Garantia de pelo menos 2-3 anúncios ativos por grupo.
- Detecção/correção de anúncios reprovados ou limitados.

### 📊 Métricas Analisadas

- CTR por anúncio
- Impressões
- Conversões por anúncio
- Taxa de conversão individual
- Status de aprovação (aprovado, limitado, reprovado)
- Índice de qualidade

#### 🔎 Indicadores Derivados

- Tendência de CTR/conversão
- **Z-score** do anúncio vs. grupo/campanha
- Percentis de performance (top 10%, bottom 10%)
- Análise estatística de **teste A/B**
- Saturação de criativo

---

## 4. 🔑 Palavras-chave

### ✅ Decisões & Otimizações

- Pausa de palavras-chave **ineficientes** (baixa conversão, CTR, alto CPA) [0 = Pausar, 1 = Manter].

Exemplo de entrada JSON

ˋˋˋ[
  {
    "id": "kw_001",
    "impressions_7d": 320,
    "clicks_7d": 45,
    "conversions_7d": 2,
    "diff_ctr_7d_adgroup": 0.02,
    "ratio_ctr_7d_adgroup": 1.05,
    "pct_rank_ctr_7d_adgroup": 0.55,
    "diff_cpc_7d_adgroup": -0.08,
    "ratio_cpc_7d_adgroup": 0.95,
    "pct_rank_cpc_7d_adgroup": 0.50,
    "diff_conversion_rate_7d_adgroup": 0.01,
    "ratio_conversion_rate_7d_adgroup": 1.10,
    "pct_rank_conversion_rate_7d_adgroup": 0.60,
    "diff_cpa_7d_adgroup": -2.0,
    "ratio_cpa_7d_adgroup": 0.85,
    "pct_rank_cpa_7d_adgroup": 0.45,
    "diff_roas_7d_adgroup": 0.3,
    "ratio_roas_7d_adgroup": 1.20,
    "pct_rank_roas_7d_adgroup": 0.58
  },
  {
    "id": "kw_002",
    "impressions_7d": 150,
    "clicks_7d": 12,
    "conversions_7d": 0,
    "diff_ctr_7d_adgroup": -0.03,
    "ratio_ctr_7d_adgroup": 0.60,
    "pct_rank_ctr_7d_adgroup": 0.25,
    "diff_cpc_7d_adgroup": 0.05,
    "ratio_cpc_7d_adgroup": 1.10,
    "pct_rank_cpc_7d_adgroup": 0.75,
    "diff_conversion_rate_7d_adgroup": -0.04,
    "ratio_conversion_rate_7d_adgroup": 0.65,
    "pct_rank_conversion_rate_7d_adgroup": 0.30,
    "diff_cpa_7d_adgroup": 4.0,
    "ratio_cpa_7d_adgroup": 1.50,
    "pct_rank_cpa_7d_adgroup": 0.80,
    "diff_roas_7d_adgroup": -0.5,
    "ratio_roas_7d_adgroup": 0.70,
    "pct_rank_roas_7d_adgroup": 0.20
  }
]ˋˋˋ

Exemplo de saida JSON

ˋˋˋ
[
  {"id": "kw_001", "acao": 1},
  {"id": "kw_002", "acao": 0}
]
ˋˋˋ
- Redução/aumento de lances baseado em performance.
- Inclusão de **negativas** via termos de busca de baixo resultado.
- Inclusão de novas palavras positivas via tendências e oportunidades.
- Ajuste do tipo de correspondência.
- Sugestão para expansão inteligente de palavra-chave.

### 📊 Métricas Analisadas

- CTR, CPC, Conversões, CPA por palavra-chave
- Quality Score
- Impressões, cliques
- Termos de busca associados

#### 🔎 Indicadores Derivados

- Tendência de desempenho (CTR, conversão, CPA)
- **Z-score** vs. média do grupo/campanha
- Tendência de termos emergentes
- Percentis (top 10% de performance)
- Score de oportunidade/escala
- Benchmark vs. meta/setor

---

## 5. 📎 Extensões de Anúncio

### ✅ Decisões & Otimizações

- Adição automática de extensões (sitelink, chamada, snippet, local).
- Pausa/ajuste de extensões com baixo resultado.
- Teste/substituição de variações para aumento de CTR.
- Priorização das extensões com melhor índice de aprovação.

### 📊 Métricas Analisadas

- CTR nas extensões
- Conversões atribuídas
- Impressões
- Índice de aprovação/limitação

#### 🔎 Indicadores Derivados

- Tendência de CTR de extensões
- **Z-score** vs. média da campanha
- Teste A/B automatizado
- Freq. de exibição/utilização

---

## 6. 🎯 Público e Segmentação

### ✅ Decisões & Otimizações

- Inclusão automática de públicos (afinidade, intenção, dados próprios).
- Ajuste de lances por performance dos segmentos.
- Exclusão de públicos/segmentos de baixo retorno.
- Teste automatizado de novos segmentos.
- Ajuste de horários por desempenho de cada público.

### 📊 Métricas Analisadas

- CPA/ROAS por segmento
- Taxa de conversão
- Impressões e custos por público
- Volume de conversão por horário

#### 🔎 Indicadores Derivados

- Tendência de performance por público
- **Z-score** vs. outros segmentos
- Overlap de audiência
- Score de oportunidade incremental
- Mapeamento temporal (hora/dia)

---

## 🧠 Notas Gerais e Boas Práticas

- Todas as ações devem ser **logadas**, incluindo decisão e justificativa.
- Os indicadores derivados (**z-score, tendência, percentil, score de cluster**) são o coração das decisões inteligentes da GIO.
- Este documento deve ser revisado e expandido a cada nova funcionalidade lançada.
- **Transparência e auditabilidade** são essenciais: toda decisão automatizada deve poder ser justificada por dados e lógica registrados.
- Use sempre benchmarks do segmento e metas do cliente para contextualizar decisões automáticas.

---

**Versão:** 1.0  
**Data:** 01/08/2025  
**Responsável:** [Seu Nome/Time Era Positiva]  
