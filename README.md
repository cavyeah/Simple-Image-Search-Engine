IMAGE SEARCH USING CLIP

Retrieve images based on a query (text or image) using OpenAI's pretrained CLIP model.

INTRODUCTION

CLIP (Contrastive Language-Image Pre-Training) is a neural network trained on a variety of image and text pairs. It maps images and text into the same latent space so they can be compared using a similarity measure.

This is a simple image search engine that accepts both text and image queries. The search engine works as follows:

1. Use the image encoder to compute feature vectors for images in the dataset
2. Index the images as: image_id with URL and feature vector
3. Compute the feature vector of the query (use text encoder for text, image encoder for image)
4. Calculate cosine similarities between the query feature vector and all image feature vectors
5. Return the k images with the highest similarity scores

HOW THE SEARCH ENGINE WORKS

The system uses the Unsplash lite dataset (25,000 images) and implements k-Nearest Neighbor search to find similar images.

1. Compute feature vectors for all images using CLIP's image encoder
2. Index images with their URLs and feature vectors
3. Encode the query (text or image) using appropriate encoder
4. Calculate cosine similarity between query and all image vectors
5. Return top k most similar images

SETUP AND USAGE

Install Dependencies:
  pip install -e . --no-cache-dir

Download Unsplash Dataset:
  python scripts/download_unsplash.py --image_width=480 --threads_count=32
  
Downloads metadata and images to unsplash-dataset/photos. Adjust image_width to reduce storage and increase threads_count for faster performance.

Create Image Index:
  python scripts/ingest_data.py
  
Downloads the pretrained CLIP model, processes images in batches, and leverages GPU if available.

Run the Application:
  streamlit run streamlit_app.py
  
Launch the web interface to search using text or image queries.

POSSIBLE IMPROVEMENTS

- Apply dimension reduction (PCA) to compress 512-dimensional vectors for faster queries and lower storage
- For billion-scale collections, consider feature binarization as used by Pinterest
- Optimize indexing for faster retrieval speeds

ACKNOWLEDGEMENTS

Based on work by:
- OpenAI CLIP (github.com/openai/CLIP)
- haltakov/natural-language-image-search

Substantially reworked and improved implementation by Kaviyasri R.thius si the readme
