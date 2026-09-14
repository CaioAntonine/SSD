# MVP de Análise de Risco, Custo e Tempo: Implantação de Unidade de Nuvem
**Estudo de Caso:** Implantação de Unidade Regional de Armazenamento em Nuvem (~10 PB a 15 PB úteis em Colocation Tier III)  
**Fontes Oficiais:** *KPMG Data Centre Global Benchmarks (2026)* e *Telemetria Backblaze (Q2 2024)*

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/SEU_USUARIO/NOME_DO_REPO/blob/main/mvp_simulacao_risco_nuvem.ipynb)

---

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

---

## 📁 Estrutura do Repositório

```
mvp_cloud_risk/
├── data/                                      # Datasets empíricos oficiais de referência
│   ├── kpmg_datacenter_benchmarks_2026.csv    # Benchmarks globais KPMG (CapEx/MW, OpEx/30MW por país)
│   ├── backblaze_q2_2024_telemetry.csv        # Telemetria bruta oficial Backblaze Q2 2024 (32.474 linhas)
│   └── project_tasks_pert.csv                 # EAP com 15 tarefas e estimativas PERT (a, m, b)
├── mvp_simulacao_risco_nuvem.ipynb            # Jupyter Notebook analítico completo com 18 gráficos
├── src/                                       # Módulos Python estruturados
│   ├── simulation_pert.py                     # Algoritmo de simulação de Monte Carlo com Beta-PERT (10.000 iterações)
│   ├── simulation_finance.py                  # Fluxo de caixa descontado, CAPEX, OPEX, VPL, TIR e sensibilidade
│   ├── export_latex_assets.py                 # Exportador de gráficos 300 DPI e tabelas LaTeX
│   └── generate_network_diagram.py            # Gerador vetorial do diagrama de rede PERT/CPM
├── run_simulation.py                          # Script CLI de execução rápida em terminal
├── build_rich_notebook.py                     # Script construtor e validador do Jupyter Notebook
├── generate_backblaze_telemetry.py            # Gerador do dataset com o esquema oficial da Backblaze
├── overleaf_monografia/                       # Projeto acadêmico em LaTeX (ABNT abnTeX2, 11 a 15 páginas)
│   ├── main.tex                               # Monografia com Introdução, Metodologia, Resultados e Conclusão
│   ├── referencias.bib                        # Citações BibTeX (PMBOK 7th, Uptime Institute, Backblaze, etc.)
│   ├── figuras/                               # Figuras em alta resolução (300 DPI)
│   └── tables/                                # Tabelas LaTeX formatadas
└── monografia_overleaf.zip                    # Pacote ZIP pronto para importação direta no Overleaf (1 clique)
```

---

## 🚀 Como Executar o Projeto

### Opção 1: Executar no Google Colab (Recomendado pelo Professor)
1. Faça um fork ou upload deste repositório no seu **GitHub**;
2. Clique no botão [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/);
3. No Google Colab, vá em **Arquivo** $\rightarrow$ **Abrir notebook** $\rightarrow$ aba **GitHub** e selecione o seu repositório;
4. O notebook possui **auto-detecção do Colab**, baixando os dados necessários e rodando todas as células em 1 clique sem requerer instalação local.

### Opção 2: Executar Localmente no VS Code / Jupyter
Clone o repositório e execute o notebook ou o script CLI:
```bash
# Execução via Jupyter Notebook
jupyter notebook mvp_simulacao_risco_nuvem.ipynb

# Ou execução via linha de comando (CLI) em 5 segundos
python run_simulation.py
```

---

## 📊 Ecossistema Visual (18 Gráficos Integrados)

O notebook apresenta **18 gráficos analíticos de alta definição**, agrupados em 4 painéis temáticos:

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

---

## 📄 Monografia Acadêmica para o Overleaf

O diretório `overleaf_monografia/` contém o trabalho acadêmico completo formatado nas normas **ABNT (`abntex2`)** (11 a 15 páginas):
- **Importação no Overleaf (1 Clique):**
  1. Acesse o [Overleaf](https://www.overleaf.com/);
  2. Clique em **"New Project"** $\rightarrow$ **"Upload Project"**;
  3. Selecione o arquivo [monografia_overleaf.zip](file:///C:/Users/Caio/.gemini/antigravity/scratch/mvp_cloud_risk/monografia_overleaf.zip);
  4. O projeto compilará instantaneamente com todas as figuras e referências BibTeX.
