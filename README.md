# Backend Quiz RAG

Backend para processamento de documentos PDF usando RAG (Retrieval-Augmented Generation).

## Dependências

Este projeto utiliza o SDK [pdf_rag_sdk_python](https://github.com/diegofornalha/pdf_rag_sdk_python) como submódulo Git para o funcionamento do ingest.

## Instalação

### 1. Clonar com submódulos

```bash
git clone --recurse-submodules <url-do-repositorio>
```

Se já clonou sem os submódulos:

```bash
git submodule init
git submodule update
```

### 2. Instalar dependências do SDK

```bash
cd pdf_rag_sdk_python
pip install -r requirements.txt
cd ..
```

## Uso

### 1. Ingestão de documentos

```bash
python scripts/ingest_regulamento.py
```

O script irá:
- Processar o PDF em `ingest/rendaextra-todos-regulamentos.pdf`
- Criar embeddings usando o modelo `BAAI/bge-small-en-v1.5`
- Salvar no banco vetorial em `data/regulamento.db`

### 2. Uso do RAG (Query)

```python
from pdf_rag_sdk_python import RAGEngine

# Inicializar
engine = RAGEngine(
    db_path="data/regulamento.db",
    embedding_model="BAAI/bge-small-en-v1.5"
)

# Busca semântica
results = engine.search("como funciona o cashback?", top_k=5)
for r in results:
    print(f"Score: {r.score:.2f} - {r.content[:100]}...")

# Contexto para LLM
context = engine.get_context("pergunta do usuário", top_k=3)
```

## Estrutura

```
backend-quiz-rag/
├── pdf_rag_sdk_python/     # SDK (submódulo Git)
│   ├── ingest.py           # Engine de ingestão
│   └── query.py            # Engine de busca RAG
├── scripts/
│   └── ingest_regulamento.py  # Script de ingestão
├── ingest/
│   └── rendaextra-todos-regulamentos.pdf
├── data/
│   └── regulamento.db      # Banco vetorial SQLite
└── .gitmodules
```
