#  Video-Context RAG AI Assistant

> An end-to-end Retrieval-Augmented Generation (RAG) pipeline that transforms massive video libraries into a fully searchable, interactive AI assistant capable of answering questions with exact timestamped citations.

##  Project Overview
Large Language Models struggle with long-form video content due to context window limitations and multimodal complexity. This project bridges that gap by building a robust data engineering and machine learning pipeline. It ingests raw video files, extracts and transcribes the audio using OpenAI's Whisper, chunks the text while preserving semantic meaning, and utilizes vector embeddings to power a highly accurate question-answering AI.

##  Key Features
* **Automated Data Ingestion:** Converts raw video files into lightweight `.mp3` audio formats for efficient processing.
* **Timestamp-Aware Transcription:** Utilizes Whisper AI to transcribe speech-to-text, injecting granular timestamp metadata so the AI can point users to exact moments in a video.
* **Semantic Chunking & Metadata:** Slices massive transcripts into mathematically digestible JSON blocks, ensuring the LLM retains context without hallucinating.
* **Efficient Vector Storage:** Generates high-dimensional embeddings for text chunks, utilizing `pandas` and `joblib` for rapid bulk-loading and serialized, local vector storage.
* **Intelligent Retrieval:** Calculates mathematical similarity between user queries and video chunks to retrieve only the most highly relevant context.

##  System Architecture 
The pipeline is divided into five core phases:
1. **Audio Extraction:** Stripping visual data (`.mp4` -> `.mp3`).
2. **Transcription:** Whisper AI translates and transcribes audio into text with timestamps.
3. **Data Structuring:** Text is chunked and saved with metadata to `.json` files.
4. **Vectorization:** Text chunks are converted into embeddings and serialized via `joblib` to prevent redundant compute.
5. **Generation:** A frontier LLM evaluates the top retrieved chunks and formulates a natural language response to the user's prompt.

##  Tech Stack
* **Transcription:** [OpenAI Whisper](https://github.com/openai/whisper)
* **Data Manipulation & Storage:** `pandas`, `joblib`, `json`
* **Embeddings:** Vector embedding models (OpenAI/Local)
* **Language Model:** Local LLMs (Iterated to GPT-5 for enhanced reasoning)

##  Optimization & Learnings
* **Context Preservation:** Upgraded the chunking strategy to reduce the total number of chunks. Larger, more meaningful chunks dramatically improved the LLM's comprehension and response accuracy.
* **Model Upgrades:** Transitioned from a smaller local LLM to GPT-5 to handle complex reasoning and improve the overall quality of the generated answers.
* **Embedding Refinement:** Re-calculated embeddings based on the optimized chunk sizes to ensure a higher quality semantic match during the retrieval phase.


# How to use this RAG AI Learning assistant on your own data
## Step 1 - Collect your videos
Move all your video files to the videos folder

## Step 2 - Convert to mp3
Convert all the video files to mp3 by ruunning video_to_mp3

## Step 3 - Convert mp3 to json 
Convert all the mp3 files to json by ruunning mp3_to_json

## Step 4 - Convert the json files to Vectors
Use the file preprocess_json to convert the json files to a dataframe with Embeddings and save it as a joblib pickle

## Step 5 - Prompt generation and feeding to LLM

Read the joblib file and load it into the memory. Then create a relevant prompt as per the user query and feed it to the LLM


