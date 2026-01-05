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

### Ingestão de documentos

```bash
python scripts/ingest_regulamento.py
```

O script irá:
- Processar o PDF em `ingest/rendaextra-todos-regulamentos.pdf`
- Criar embeddings usando o modelo `BAAI/bge-small-en-v1.5`
- Salvar no banco vetorial em `data/regulamento.db`

## Estrutura

```
backend-quiz-rag/
├── pdf_rag_sdk_python/     # SDK (submódulo Git)
├── scripts/
│   └── ingest_regulamento.py
├── ingest/
│   └── rendaextra-todos-regulamentos.pdf
├── data/
│   └── regulamento.db
└── .gitmodules
```
