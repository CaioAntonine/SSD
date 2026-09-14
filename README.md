# MVP de Análise de Risco, Custo e Tempo: Implantação de Unidade de Nuvem
**Estudo de Caso:** Implantação de Unidade Regional de Armazenamento em Nuvem (~10 PB a 15 PB úteis em Colocation Tier III)  
**Fontes Oficiais:** *KPMG Data Centre Global Benchmarks (2026)* e *Telemetria Backblaze (Q2 2024)*

## 📌 Visão Geral do Projeto

Este repositório contém o código-fonte completo de um **Modelo de Viabilidade Preditivo (MVP)** analítico desenvolvido em Python para avaliar, de forma integrada, o risco, o custo e o cronograma de implementação de uma nova infraestrutura de nuvem (*Cloud Storage Facility* baseada em cluster distribuído Ceph/Erasure Coding).

A modelagem é ancorada em duas das mais respeitadas fontes empíricas globais da indústria:
1. **Relatório Oficial KPMG (2026) — *Benchmarking CapEx and OpEx in the Global Data Centre Market***:
   - Custos de construção civil por MW em 10 países (Espanha \$6,7M/MW, Alemanha \$7,5M/MW, UK \$8,5M/MW, EUA \$5,5M/MW);
   - Equipamentos OFCI (*Owner Furnished Contractor Installed*) de \$3,5M/MW (\$1,4M elétrico, \$1,1M mecânico/HVAC, \$0,6M civil/CSA);
   - OpEx de mão de obra técnica 24x7 (regra de 4 FTEs por posto de turno anual) e O&M (divisão 60% preventiva / 40% reativa).
2. **Dataset de Telemetria de Discos Rígidos Backblaze (Q2 2024)**:
   - Mais de 32.000 registros diários de unidades HDD corporativas de alta densidade (16TB, 18TB e 20TB);
   - Cálculo empírico do AFR anualizado ($\text{AFR} \approx 0,80\% \text{ a } 1,60\%$ a.a.), MTBF e correlação de sensores preditivos SMART (5, 9, 187, 197, 198) com o evento de falha.


## 📊 Ecossistema Visual (18 Gráficos Integrados)

O notebook apresenta **18 gráficos**, agrupados em 4 painéis temáticos:

### Painel 1: Confiabilidade de Hardware (Backblaze Q2 2024)
- **Gráfico 1:** Taxa de Falha Anualizada (*AFR %*) por Modelo de Disco (Seagate, WDC, Toshiba);
- **Gráfico 2:** Heatmap de Correlação de Pearson entre Sensores SMART (5, 9, 187, 197, 198) e Falha;
- **Gráfico 3:** Curva Empírica de Sobrevivência $S(t)$ da frota de HDDs ao longo de 40.000 horas de uso contínuo.

### Painel 2: Custos de Infraestrutura e Engenharia (KPMG 2026)
- **Gráfico 4:** *Donut Chart* da Decomposição de Equipamentos OFCI (\$3,5M/MW: Elétrico, Mecânico, CSA, Preliminares);
- **Gráfico 5:** Comparativo Regional: CapEx Construção vs OpEx Mão de Obra Técnica (Espanha, UK, EUA, Alemanha, etc.);
- **Gráfico 6:** Curva de Eficiência e Economia de Escala (Capacidade em MW vs OpEx por MW-ano: redução de 58% entre 30MW e 80MW).

### Painel 3: Cronograma e Caminho Crítico (PERT/CPM Estocástico)
- **Gráfico 7:** Diagrama de Gantt com Barras de Incerteza (Intervalos $[a, m, b]$ das 15 atividades);
- **Gráfico 8:** Curva S Cumulativa de Prazo com marcos P50, P80 (Meta Segura), P95 (Margem SLA) e o CPM tradicional;
- **Gráfico 9:** Ranking do Índice de Criticidade (% das iterações no caminho crítico com alerta visual de gargalo).

### Painel 4: Engenharia Econômica e Sensibilidade (60 Meses)
- **Gráfico 10:** Decomposição Empilhada do OPEX Mensal (Energia com PUE 1,35, Racks, NOC 24x7, Trânsito IP, Peças);
- **Gráfico 11:** Curva de Break-even Operacional Mensal (Receita Líquida vs OPEX com área de EBITDA positivo);
- **Gráfico 12:** Histograma de Densidade do Investimento Inicial (CAPEX);
- **Gráfico 13:** Distribuição do VPL em 5 Anos (verde para lucro, com linha de equilíbrio VPL = 0);
- **Gráfico 14:** Evolução do Saldo de Caixa Acumulado (Curva de Payback e Intervalo de Confiança P10-P90);
- **Gráfico 15:** Histograma de Frequência do Tempo de Payback Descontado;
- **Gráfico 16:** Diagrama de Tornado Horizontal (Correlação de Spearman no VPL);
- **Gráfico 17:** *Spider Plot* de Sensibilidade Paramétrica (-30% a +30% em Preço, Ocupação, CapEx e Energia);
- **Gráfico 18:** Matriz de Riscos 5x5 (Probabilidade $\times$ Impacto) em Heatmap com os 5 principais riscos mapeados.

---

## 📈 Quadro de Resultados da Modelagem

| Pilar | Métrica | Valor Encontrado | Interpretação Prática |
|---|---|---|---|
| **Tempo** | CPM Determinístico Tradicional | **168,3 dias úteis** | Estimativa clássica linear sem incertezas |
| **Tempo** | Média Estocástica (Monte Carlo) | **170,2 dias úteis** ($\sigma = 12,4$d) | Duração esperada considerando volatilidade real |
| **Tempo** | Probabilidade Cumprimento CPM | **45,2%** | **O CPM tradicional falha em 54,8% das vezes!** |
| **Tempo** | Meta Operacional Segura (P80) | **180,5 dias úteis** (~8,6 meses) | Meta recomendada para governança interna |
| **Tempo** | Prazo com Margem de SLA (P95) | **191,4 dias úteis** (~9,1 meses) | Prazo para compromissos contratuais vinculantes |
| **Custo** | CAPEX Total Médio | **R$ 3,04 Milhões** | P10: R\$ 2,84M \| P90: R\$ 3,25M (12 nós 4U Ceph + 100GbE) |
| **Custo** | OPEX Médio Mensal | **R$ 111,8 mil / mês** | ~R\$ 1,34M/ano (Racks, energia PUE 1,35, NOC e peças) |
| **Retorno**| VPL Médio (TMA 12% a.a.) | **R$ 5,42 Milhões** | Retorno líquido positivo em 5 anos (60 meses) |
| **Retorno**| Probabilidade de Viabilidade | **100,0%** ($P(VPL > 0)$) | Risco de insolvência nulo nas premissas de mercado |
| **Retorno**| Taxa Interna de Retorno (TIR) | **77,1% ao ano** | Retorno muito superior ao custo de oportunidade (12%) |
| **Retorno**| Payback Descontado Mediano | **22 meses** (~1,8 anos) | Retorno completo do investimento em menos de 2 anos |
| **Risco** | Principal Driver de Sensibilidade | **Preço/TB ($r = +0,76$)** | Ocupação ($r = +0,48$) supera em 40x o risco de quebra de HDDs |
