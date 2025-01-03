# Violet: Arabic Image Captioning
The `Violet` repository provides a framework for generating **Arabic image captions**. The pipeline leverages state-of-the-art transformer models, providing an easy-to-use interface for researchers and developers working on tasks such as image captioning and visual question answering (VQA).

## Features
1. **Arabic Image Captioning**: Generate high-quality captions for images in Arabic.
2. **Visual Feature Extraction**: Extract image features for integration into vision-language models or downstream tasks.
3. **Customizable for VQA**: Use extracted features and captions to build Arabic visual question-answering systems.
4. **Mixed Input Support**: Handle batches of images in various formats, such as URLs, file paths, NumPy arrays, PyTorch tensors, and PIL Image objects.


## Installation

### Option 1: Install Directly via pip
```bash
pip install git+https://github.com/Mahmood-Anaam/violet.git
```

### Option 2: Clone Repository and Install in Editable Mode
```bash
!git clone https://github.com/Mahmood-Anaam/violet.git
%cd violet
!pip install -e .
```

### Option 3: Use Conda Environment
```bash
conda env create -f environment.yml
conda activate violet

!git clone https://github.com/Mahmood-Anaam/violet.git
%cd violet
!pip install -e .
```


## Example Usage in Google Colab
Interactive Jupyter notebooks are provided to demonstrate Violet's capabilities. You can open these notebooks in Google Colab:

- [Image Captioning Demo](https://github.com/Mahmood-Anaam/violet/blob/main/notebooks/inference_demo.ipynb) [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mahmood-Anaam/violet/blob/main/notebooks/inference_demo.ipynb)
- [Feature Extraction Demo](https://github.com/Mahmood-Anaam/violet/blob/main/notebooks/features_extraction_demo.ipynb) [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Mahmood-Anaam/violet/blob/main/notebooks/features_extraction_demo.ipynb)



## Quick Start

The Violet pipeline supports three main functionalities:

1. **Generate Captions for Images**</br>
The pipeline can handle a variety of input formats
   ```python
   
     from violet.pipeline import VioletImageCaptioningPipeline
     from violet.configuration import VioletConfig
  
     pipeline = VioletImageCaptioningPipeline(VioletConfig)
  
    # Single image captioning
    captions = pipeline("http://images.cocodataset.org/val2017/000000039769.jpg")
    print(captions)
  
    # Batch image captioning with mixed formats
    images = [
        "http://images.cocodataset.org/val2017/000000039769.jpg",
        "/path/to/local/image.jpg",
        np.random.rand(224, 224, 3),  # NumPy array
        torch.randn(3, 224, 224),     # PyTorch tensor
        Image.open("/path/to/pil/image.jpg"),  # PIL Image
    ]
   
    captions = pipeline(images)
    for caption in captions:
        print(caption)
      
   ```

2. **Extract Features from Images**</br>
Extract visual features for downstream tasks like VQA. The pipeline supports mixed input formats in a single batch.
   ```python
   # Single image feature extraction
   features = pipeline.generate_features("http://images.cocodataset.org/val2017/000000039769.jpg")
   print(features.shape)

   # Batch feature extraction with mixed formats
   features = pipeline.generate_features(images)
   print(features.shape)
   ```

4. **Generate Captions from Features**</br>
Generate captions based on precomputed visual features.
   ```python
   captions = pipeline.generate_captions_from_features(features)
   for caption in captions:
     print(caption)
   ```

