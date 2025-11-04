# Ricerca multimodale con ChromaDB

Questa applicazione dimostra come utilizzare ChromaDB per creare un sistema di ricerca multimodale. L'applicazione consente di cercare immagini simili a un'immagine di query o a una query di testo.

## Prerequisiti

- Python 3.8+
- Pipenv
- Docker (opzionale)

## Installazione

1. Clonare il repository:

   ```bash
   git clone https://github.com/prompt-memoria/chromadb-multimodal.git
   cd chromadb-multimodal
   ```

2. Installare le dipendenze con Pipenv:

   ```bash
   pipenv install
   ```

## Utilizzo

### Creare una nuova collezione

Per creare una nuova collezione ChromaDB, eseguire lo script `create_collection.py`:

```bash
pipenv run python create_collection.py
```

Questo creerà una nuova collezione chiamata `multimodal_collection` nella directory `my_vectordb`.

### Caricare le immagini

Per caricare le immagini nella collezione, eseguire lo script `upload_images.py`, specificando la directory contenente le immagini:

```bash
pipenv run python upload_images.py /percorso/della/tua/cartella/immagini
```

### Eseguire l'applicazione

Per avviare l'applicazione Gradio, eseguire lo script `app.py`:

```bash
pipenv run python app.py
```

Questo avvierà un'interfaccia web Gradio all'indirizzo `http://127.0.0.1:7860`.

### Eliminare una collezione

Per eliminare la collezione, eseguire lo script `delete_collection.py`:

```bash
pipenv run python delete_collection.py
```

## Docker

È inoltre possibile eseguire l'applicazione utilizzando Docker.

1. Costruire l'immagine Docker:

   ```bash
   docker build -t chromadb-multimodal .
   ```

2. Eseguire il container Docker:

   ```bash
   docker run -p 7860:7860 chromadb-multimodal
   ```

Questo avvierà l'applicazione Gradio e la renderà disponibile all'indirizzo `http://localhost:7860`.
