# OCR and Translation Evaluation with Semantic Analysis

This Python script extracts text from an image using Optical Character Recognition (OCR) with **Tesseract**, evaluates the OCR accuracy using Word Error Rate (WER), and assesses the translation quality from English to French using **MarianMT** with both BLEU score and semantic similarity analysis.

## Features
- **OCR Text Extraction**: Robust image-to-text conversion
- **Translation Quality Metrics**: 
  - Traditional BLEU score
  - Semantic similarity using Sentence-BERT
- **Error Handling**: Robust normalization and validation
- **Multilingual Support**: Works with English/French and other language pairs


Alternatively, you can use the provided Colab notebook which automatically installs the required dependencies.

## Colab Notebook

For easy testing and usage, there is an accompanying Colab notebook that you can use. This notebook automatically installs the required libraries and allows you to upload images for OCR extraction and translation evaluation directly within the notebook. Simply follow the instructions within the notebook to get started.

## Architecture

# OCR, Translation, and Semantic Analysis Components

## Tesseract (OCR)
**Open-source OCR engine using LSTM networks for text recognition:**
- Processes images through segmentation and feature extraction
- Supports multiple languages and font types
- Outputs UTF-8 text with confidence scores

## MarianMT (Translation)
**Neural Machine Translation framework using transformer architecture:**
- Attention mechanisms for context-aware translations
- Pre-trained English→French model (OPUS-MT)
- Handles sequences up to 512 tokens

## Sentence-BERT (Semantic Analysis)
**Multilingual embedding model for semantic understanding:**
- Generates 512-dimensional sentence vectors
- Calculates cosine similarity between texts
- Trained on multilingual paraphrase datasets

## Metric Comparison

| Feature               | BLEU Score       | Semantic Similarity |
|-----------------------|------------------|---------------------|
| Basis                 | N-gram overlap   | Meaning vectors     |
| Paraphrase Handling   | ❌               | ✅                  |
| Cross-language        | ❌               | ✅                  |
| Output Range          | 0-1              | 0-1 (cosine)        |

## Functions


### OCR Functions
- **`ocr_extraction(image_path: str) -> str`**  
  Extracts text from an image using Tesseract OCR  
  *Parameters*: `image_path` - Path to input image file (JPG/PNG)  
  *Returns*: Raw extracted text as UTF-8 string

- **`normalize_text(text: str) -> str`**  
  Normalizes text by:  
  - Converting to lowercase  
  - Removing all punctuation  
  - Collapsing multiple whitespaces  
  *Parameters*: Raw input text  
  *Returns*: Cleaned and normalized text

### Translation Functions
- **`load_translation_model() -> tuple`**  
  Initializes MarianMT model and tokenizer  
  *Returns*: Tuple containing (model, tokenizer)

- **`translate_text(model, tokenizer, text: str) -> str`**  
  Translates English text to French using MarianMT  
  *Parameters*:  
  - Pretrained model and tokenizer  
  - English text (max 512 tokens)  
  *Returns*: French translated text

### Evaluation Metrics
- **`calculate_wer(reference: str, hypothesis: str) -> float`**  
  Computes Word Error Rate between reference and OCR text  
  *Parameters*: Normalized reference and OCR texts  
  *Returns*: WER score between 0 (perfect) and 1 (all wrong)

- **`calculate_bleu(reference: str, hypothesis: str) -> float`**  
  Computes BLEU-4 score between reference and translation  
  *Parameters*: Normalized reference and translated texts  
  *Returns*: BLEU score between 0 (no match) and 1 (exact match)

### Pipeline Functions
- **`evaluate_ocr(ocr_output: str, ground_truth_ocr: str) -> float`**  
  Full OCR evaluation pipeline  
  *Parameters*: Raw OCR output and ground truth text  
  *Returns*: WER score

- **`evaluate_translation(ocr_output: str, ground_truth_translation: str, model, tokenizer) -> float`**  
  Full translation evaluation pipeline:  
  1. Translates OCR text  
  2. Compares with reference translation  
  *Returns*: BLEU score

- **`process_image_for_evaluation(image_path: str, ground_truth_ocr: str, ground_truth_translation: str) -> dict`**  
  Complete end-to-end evaluation pipeline:  
  1. OCR extraction  
  2. OCR evaluation (WER)  
  3. Translation  
  4. Translation evaluation (BLEU)  
  *Returns*: Dictionary with WER and BLEU scores

## Usage

1. Set the `image_path` to the path of your image file.
2. Set `ground_truth_ocr` to the expected OCR text.
3. Set `ground_truth_french` to the expected French translation of the text.
4. Run the script to extract OCR text, evaluate it using WER, translate it, and compute the BLEU score.

Example:
```python
image_path = "" #add your image path
ground_truth_ocr = "" #add groundtruth text
ground_truth_french = "" #add groundtruth translation
process_image_for_evaluation(image_path, ground_truth_ocr, ground_truth_french)
```




