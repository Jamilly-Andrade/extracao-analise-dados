# Extração e Análise de Dados — Material de Consulta A1
FGV ECMI · Prof. Mateus Pestana

Repositório pessoal de estudos e consulta prática para a avaliação de **Extração e Análise de Dados**.

---

## 📂 Arquivos disponíveis

1. **[COLA_EXTRACAO.html](COLA_EXTRACAO.html)**
   * Folha de cola completa e interativa em HTML (com barra lateral de navegação e botões para copiar código).
   * Cobre diagnóstico inicial, limpeza de dados, métricas, hashtags (explode), visualização Matplotlib, regressão e classificação.
   * Visualização online via GitHub Pages: [Acessar Cola Online](https://jamilly-andrade.github.io/extracao-analise-dados/)

2. **[FOLHA_DE_COLA_EXTRACAO.ipynb](FOLHA_DE_COLA_EXTRACAO.ipynb)**
   * Notebook Jupyter executável com dados simulados embutidos e códigos testados.
   * Inclui anotações práticas sobre como adaptar colunas e funções na prova.

3. **[GUIA_INTUITIVO_EXTRACAO.md](GUIA_INTUITIVO_EXTRACAO.md)**
   * Guia objetivo em Markdown com explicação conceitual simples ("quando usar cada coisa").
   * Dicionário rápido de erros comuns, pegadinhas de prova e regras de ouro do professor.

---

## 🚀 Resumo dos Principais Tópicos

### 1. Diagnóstico e Inspeção (Pandas)
- `df.head()`: Primeiras linhas da base.
- `df.shape`: Quantidade de linhas e colunas.
- `df.isna().sum()`: Valores ausentes por coluna.
- `df.duplicated().sum()`: Linhas duplicadas.

### 2. Limpeza e Tratamento
- `df.drop_duplicates(subset=['id_publicacao'])`: Remoção de duplicatas.
- `df['col'].str.strip().str.lower().str.title()`: Normalização de texto.
- `pd.to_datetime(df['data'], dayfirst=True, errors='coerce')`: Conversão de data segura.
- `pd.to_numeric(df['num'], errors='coerce')`: Conversão numérica segura.

### 3. Agrupamento e Métricas
- Padrão de hashtags: `dropna()` → `str.split(',')` → `explode()` → `str.strip()` → `value_counts()`.
- Resumo agrupado: `df.groupby('categoria').agg(total=('id', 'count'), media=('valor', 'mean')).reset_index()`.

### 4. Visualização (Matplotlib)
- **Barras**: `ax.bar(categorias, valores)` — comparação entre categorias.
- **Linhas**: `ax.plot(datas, medias, marker='o')` — evolução no tempo (série temporal).
- **Dispersão**: `ax.scatter(x, y, alpha=0.5)` — relação entre 2 variáveis contínuas.
- Obrigatório: título, rótulos dos eixos e fonte dos dados.

### 5. Regressão (scikit-learn)
- Separação sem vazamento: `X` (features que já existiam antes) e `y` (alvo contínuo).
- `train_test_split(X, y, test_size=0.25, random_state=42)`.
- Comparação com modelo de linha de base (bobo): `np.full(len(y_teste), y_treino.mean())`.
- Métricas: `mean_absolute_error` (MAE) e `r2_score` (R²).
- Transformação de cauda longa: `np.log1p()` e volta com `np.expm1()`.

### 6. Classificação (scikit-learn)
- Rótulo binário: `y = (df['metrica'] >= corte).astype(int)`.
- Split estratificado: `train_test_split(X, y, stratify=y)`.
- Modelo: `LogisticRegression(max_iter=1000)` e `DecisionTreeClassifier(max_depth=4, class_weight='balanced')`.
- Métricas: matriz de confusão, precisão, recall e F1-score.
