# MVP de Análise de Risco, Custo e Tempo & Monografia Acadêmica (Overleaf)
**Projeto:** Implantação de Nova Unidade Regional de Armazenamento em Nuvem (~10 PB úteis em Colocation Tier III)

---

## 📁 Estrutura do Repositório

```
mvp_cloud_risk/
├── data/                                # Datasets empíricos de referência
│   ├── backblaze_benchmarks.csv         # Taxas de falha anualizada (AFR) e custos de HDDs de 16TB/20TB
│   ├── datacenter_capex_opex.csv        # Custos de racks, PUE, energia kWh, hardware e premissas
│   └── project_tasks_pert.csv           # Estrutura WBS/EAP com estimativas PERT (a, m, b)
├── src/                                 # Módulos Python de modelagem estatística
│   ├── simulation_pert.py               # Simulação de Monte Carlo com Beta-PERT e CPM estocástico
│   ├── simulation_finance.py            # Fluxo de caixa descontado, CAPEX, OPEX, VPL, TIR e sensibilidade
│   ├── export_latex_assets.py           # Gerador de gráficos 300 DPI e tabelas formatadas em LaTeX
│   └── generate_network_diagram.py      # Diagrama de rede de precedência do projeto
├── mvp_simulacao_risco_nuvem.ipynb      # Jupyter Notebook analítico documentado passo a passo
├── run_simulation.py                    # Script executável CLI da simulação completa
├── output/                              # Ativos exportados localmente (figuras e tabelas)
│   ├── figures/
│   └── tables/
├── overleaf_monografia/                 # Código-fonte LaTeX descompactado da monografia (ABNT / abnTeX2)
│   ├── main.tex                         # Texto acadêmico completo (11 a 15 páginas)
│   ├── referencias.bib                  # Base bibliográfica BibTeX com fontes reais (PMI, Backblaze, etc.)
│   ├── figuras/                         # Gráficos em 300 DPI inseridos no texto
│   └── tables/                          # Tabelas LaTeX inseridas via \input{}
└── monografia_overleaf.zip              # Pacote ZIP pronto para importação direta no Overleaf (1 clique)
```

---

## 🚀 Como Executar o MVP em Python

### 1. Via Linha de Comando (CLI)
Para reproduzir a simulação completa de 10.000 iterações em segundos:
```bash
python run_simulation.py
```

### 2. Via Jupyter Notebook
Abra o arquivo no VS Code ou no navegador com Jupyter:
```bash
jupyter notebook mvp_simulacao_risco_nuvem.ipynb
```
O notebook é didático e autoexplicativo, contendo:
- Formulações matemáticas em LaTeX;
- Gráficos interativos inline;
- Interpretação técnica de cada indicador;
- Exportação automatizada de ativos.

---

## 📄 Como Subir e Compilar a Monografia no Overleaf

1. Acesse sua conta no **[Overleaf](https://www.overleaf.com/)**;
2. Clique no botão verde superior esquerdo: **"New Project"** $\rightarrow$ **"Upload Project"**;
3. Arraste ou selecione o arquivo:
   `monografia_overleaf.zip` localizado nesta pasta;
4. O Overleaf criará o projeto automaticamente com todos os arquivos (`main.tex`, `referencias.bib`, figuras e tabelas);
5. Clique em **"Recompile"** para gerar o PDF da monografia formatado nas normas ABNT.

---

## 📊 Principais Resultados do Estudo

| Dimensão | Métrica | Valor Encontrado | Interpretação Prática |
|---|---|---|---|
| **Tempo** | CPM Determinístico | 168,3 dias úteis | Prazo tradicional tradicionalmente divulgado |
| **Tempo** | Média Estocástica | 170,2 dias ($\sigma = 12,4$d) | Duração esperada considerando incertezas |
| **Tempo** | Probabilidade Prazo CPM | **45,2%** | O CPM tradicional tem menos de 50% de chance de cumprimento! |
| **Tempo** | Meta P80 (Segura) | 180,5 dias úteis | Recomendado para metas e marcos operacionais |
| **Tempo** | Meta P95 (Conservadora) | 191,4 dias úteis | Prazo com contingência de 21,7 dias para contratos de SLA |
| **Custo** | CAPEX Médio | **R$ 3,09 Milhões** | Investimento em 720 HDDs de 20TB, 12 storages 4U e rede 100G |
| **Custo** | OPEX Médio | **R$ 112,3 mil / mês** | Colocation, energia (PUE 1,35), trânsito IP e peças |
| **Retorno**| VPL Médio (TMA 12%) | **R$ 5,37 Milhões** | Valor Presente Líquido do projeto em 5 anos |
| **Retorno**| Probabilidade VPL > 0 | **100,0%** | Risco financeiro virtualmente nulo sob premissas de mercado |
| **Retorno**| TIR Média Anualizada | **76,5% a.a.** | Taxa Interna de Retorno muito superior à TMA |
| **Retorno**| Payback Descontado | **22 meses** | Retorno completo do investimento inicial em menos de 2 anos |
| **Risco** | Maior Direcionador | Preço por TB / Ocupação | Risco comercial é 4x mais impactante que quebra de hardware |
