# Projeto Final - Introdução à Ciência de Dados - Instituto Federal de Brasília

## 👥 Estudantes
- Danielle Ester Barbosa da Silva
- Luísa Oliveira Gonçalves

## 📊 Sobre o Projeto

Análise exploratória e modelagem preditiva de dados da Síndrome Respiratória Aguda Grave (SRAG) com foco em **diferenças regionais** no Brasil durante o período de 2019 a 2025.

## 🎯 Objetivo

Desenvolver uma análise exploratória e um modelo de aprendizado de máquina para compreensão dos aspectos associados às diferenças regionais de pacientes diagnosticados com COVID-19 no Brasil.

## 📁 Base de Dados

**Fonte:** [OpenDataSUS - SRAG 2021 a 2024](https://opendatasus.saude.gov.br/dataset/srag-2021-a-2024)

**Período:** 2019 a 2025

**Arquivos:** Disponíveis no Google Drive (baixados automaticamente via `gdown`)

## 🔧 Tecnologias Utilizadas

- **Python 3.x**
- **Bibliotecas principais:**
  - `pandas` - Manipulação de dados
  - `numpy` - Operações numéricas
  - `matplotlib` & `seaborn` - Visualização
  - `scikit-learn` - Machine Learning
  - `gdown` - Download de arquivos do Google Drive

## 📋 Variáveis Selecionadas

### Principais
- `SG_UF` - UF de residência
- `CLASSI_FIN` - Classificação final do caso
- `EVOLUCAO` - Evolução do caso (cura/óbito)
- `HOSPITAL` - Houve internação
- `UTI` - Internado em UTI

### Demográficas
- `NU_IDADE_N` - Idade do paciente
- `TP_IDADE` - Tipo/unidade de idade
- `DT_NASC` - Data de nascimento

### Comorbidades
- `DIABETES` - Diabetes mellitus
- `CARDIOPATI` - Doença Cardiovascular Crônica
- `OBESIDADE` - Obesidade
- `RENAL` - Doença Renal Crônica
- `PNEUMOPATI` - Pneumopatia Crônica
- `NEUROLOGIC` - Doença Neurológica Crônica
- `IMUNODEPRE` - Imunodeficiência

## 🔄 Pipeline de Análise

### 1. **Carregamento de Dados**
- Download automático via Google Drive
- Consolidação de múltiplos arquivos CSV (2019-2025)
- Seleção de variáveis relevantes
- Total processado: **4.419.069 registros**

### 2. **Limpeza de Dados** (`LimpezaSRAG`)
Processo automatizado em 6 etapas:
1. **Padronização** - Uniformização de valores ausentes e códigos
2. **Conversão de Tipos** - Transformação de idade para numérico
3. **Filtro de Domínios** - Remoção de registros inválidos
4. **Tratamento de Ignorados** - Conversão de código "9" para NaN
5. **Remoção de Inválidos** - Validação de códigos binários
6. **Remoção de Nulos** - Exclusão de registros incompletos

### 3. **Visualização de Dados**
Análise regional de pacientes com comorbidades:
- Heatmap de prevalência das 5 principais comorbidades por região
- Identificação de padrões regionais
- Foco em pacientes críticos (com pelo menos uma comorbidade)

### 4. **Modelagem Preditiva**

#### Preparação
- Filtro: apenas casos com desfecho conhecido (cura/óbito)
- Criação de variável alvo: `OBITO` (0=cura, 1=óbito)
- Agrupamento por regiões do Brasil
- Codificação de variáveis categóricas e binárias

#### Modelo
- **Algoritmo:** Regressão Logística
- **Divisão:** 70% treino / 30% teste
- **Pré-processamento:**
  - Padronização de variáveis numéricas (idade)
  - One-Hot Encoding para variáveis categóricas (região)
  - Preservação de variáveis binárias
- **Validação:** Cross-validation (5 folds)

#### Métricas
- **AUC-ROC no teste:** 0.7694
- **AUC-ROC validação cruzada:** 0.7702 ± 0.0008

## 📈 Resultados

O modelo demonstrou:
- **Boa capacidade discriminativa** (AUC > 0.75)
- **Alta estabilidade** (baixo desvio padrão na validação cruzada)
- **Consistência** entre conjunto de teste e validação cruzada

## 🚀 Como Executar

### Google Colab (Recomendado)
1. Abra o notebook no Colab via badge no topo
2. Execute as células sequencialmente
3. Os dados serão baixados automaticamente

### Localmente
```bash
# Clone o repositório
git clone [URL_DO_REPOSITORIO]

# Instale as dependências
pip install -U gdown pandas numpy matplotlib seaborn scikit-learn

# Execute o notebook
jupyter notebook projeto_final.ipynb
```

## 📊 Estrutura do Código

```
projeto_final.ipynb
├── Importações e Configurações
├── Definição de Variáveis e Domínios
├── Carregamento de Dados (gdown)
├── Limpeza de Dados (LimpezaSRAG)
├── Visualização (preparar_dados_para_graficos)
└── Modelagem (preparar_dados + calcular_auc_roc)
```

## 📝 Observações

- Encoding dos arquivos: `latin1` (padrão brasileiro)
- Separador CSV: `;` (ponto-e-vírgula)
- Tratamento de linhas malformadas: `skip`
- Balanceamento de classes: `class_weight="balanced"`

## 🎓 Disciplina

**Introdução à Ciência de Dados**

---

*Projeto desenvolvido como trabalho final da disciplina de Introdução à Ciência de Dados.*