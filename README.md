# MVP de Análise de Risco, Custo e Tempo
**Projeto:** Implantação de Nova Unidade Regional de Armazenamento em Nuvem (~10 PB úteis)

Abra o arquivo no VS Code ou no navegador com Jupyter:
```bash
jupyter notebook mvp_simulacao_risco_nuvem.ipynb
```
O notebook é didático e autoexplicativo, contendo:
- Formulações matemáticas em LaTeX;
- Gráficos interativos inline;
- Interpretação técnica de cada indicador;
- Exportação automatizada de ativos.

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
