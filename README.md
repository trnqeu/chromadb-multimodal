# ChromaDB Multimodal Search

This application demonstrates how to use ChromaDB to create a multimodal search system. It allows you to find similar images based on a query image or a text query.

This guide prioritizes using **Docker** as it's the simplest and most reliable way to run the application, avoiding any local Python environment issues.

## Prerequisites

  - [Docker](https://www.docker.com/get-started)

## Usage (Docker - Recommended)

This workflow uses Docker volumes to store your vector database (`my_vectordb`) on your host machine. This ensures your data persists even after the container stops.

### 1\. Clone the Repository

```bash
git clone git@github.com:trnqeu/chromadb-multimodal.git
cd chromadb-multimodal
```

### 2\. Build the Docker Image

```bash
docker build -t chromadb-multimodal .
```

### 3\. Prepare Local Directories

You need a local directory to store the persistent database and a directory containing the images you want to upload.

```bash
# 1. Create a directory for the persistent database
mkdir ./my_local_vectordb

# 2. Make note of your image directory's absolute path
# For this guide, we'll use /path/to/your/images as a placeholder.
# Example: /home/user/Pictures/my-dataset
```

### 4\. Run Setup Scripts

Run the setup scripts inside the container, mounting your local directories as volumes.

**a. Create the Collection:**

This command runs the `create_collection.py` script, which will create the `multimodal_collection` inside your `./data` folder.

```bash
docker run --rm \
  -v ./my_local_vectordb:/app/my_vectordb \
  chromadb-multimodal \
  python create_collection.py
```

**b. Upload Your Images:**

This command runs the `upload_images.py` script. It mounts your local database (so it can add to it) and your local images (so it can read them).

**Note:** Replace `/path/to/your/images` with the **absolute path** to your images.

```bash
docker run --rm \
  -v ./my_local_vectordb:/app/my_vectordb \
  -v ./data:/data \
  chromadb-multimodal \
  python upload_images.py /data
```

### 5\. Run the Application

Finally, run the main Gradio application. It will connect to the persistent database you just populated.

```bash
docker run --rm -p 7860:7860 \
  -v ./my_local_vectordb:/app/my_vectordb \
  -v ./data:/data \
  chromadb-multimodal
```

You can now access the web interface at **[http://localhost:7860](https://www.google.com/search?q=http://localhost:7860)**.

-----

## Managing the Collection

### Delete the Collection

To delete all data and start over, run the `delete_collection.py` script using the same volume mount:

```bash
docker run --rm \
  -v ./my_local_vectordb:/app/my_vectordb \
  chromadb-multimodal \
  python delete_collection.py
```

-----

## Local Development (Optional)

If you prefer to run the application locally without Docker, you can use `pipenv`.

### Prerequisites (Local)

  - Python 3.12+
  - `pipenv` (Recommended installation: `pipx install pipenv`)

### 1\. Install Dependencies

```bash
pipenv install
```

### 2\. Run the Scripts

**a. Create the Collection:**

```bash
pipenv run python create_collection.py
```

This will create a `my_vectordb` directory in your project folder.

**b. Upload Images:**

```bash
pipenv run python upload_images.py /path/to/your/images
```

**c. Run the App:**

```bash
pipenv run python app.py
```

This will start the Gradio web interface at `http://127.0.0.1:7860`.