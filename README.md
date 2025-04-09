
# OCR and Translation Evaluation

This Python script extracts text from an image using Optical Character Recognition (OCR) with **Tesseract**, evaluates the OCR accuracy using Word Error Rate (WER), and assesses the translation quality from English to French using **MarianMT** and BLEU score.

## Requirements

- `pytesseract` (for OCR)
- `Pillow` (for image processing)
- `nltk` (for BLEU score calculation)
- `jiwer` (for WER calculation)
- `transformers` (for machine translation)


Alternatively, you can use the provided Colab notebook which automatically installs the required dependencies.

## Colab Notebook

For easy testing and usage, there is an accompanying Colab notebook that you can use. This notebook automatically installs the required libraries and allows you to upload images for OCR extraction and translation evaluation directly within the notebook. Simply follow the instructions within the notebook to get started.

## Architecture

- **Tesseract (OCR)**:  
   Tesseract is an open-source OCR engine that is used for extracting text from images. It recognizes text in scanned images and outputs the recognized text. The text is then processed and evaluated for accuracy.
   
   Tesseract uses machine learning and neural networks to recognize characters and words. It processes the image by detecting characters and words in various languages, and then outputs the best possible text.

- **MarianMT (Translation)**:  
   MarianMT is a multilingual machine translation model from the `transformers` library, developed by the Helsinki-NLP group. In this script, MarianMT is used for translating text from English to French. The translation is performed using a pre-trained model that uses attention-based neural networks for high-quality translations.

   The MarianMT model works by generating a translated sequence of tokens from an input sequence using a transformer architecture.

## Functions

- **`ocr_extraction(image_path)`**: Extracts text from an image using Tesseract OCR.
- **`normalize_text(text)`**: Normalizes text by converting it to lowercase, removing punctuation, and collapsing spaces.
- **`calculate_wer(reference, hypothesis)`**: Calculates the Word Error Rate (WER) between a reference text and OCR output.
- **`calculate_bleu(reference, hypothesis)`**: Computes the BLEU score between a reference translation and the translated text.
- **`load_translation_model()`**: Loads the MarianMT model for English-to-French translation.
- **`translate_text(model, tokenizer, text)`**: Translates the input text from English to French using the MarianMT model.
- **`evaluate_ocr(ocr_output, ground_truth_ocr)`**: Evaluates OCR accuracy using WER.
- **`evaluate_translation(ocr_output, ground_truth_translation, model, tokenizer)`**: Evaluates translation accuracy using BLEU score.
- **`process_image_for_evaluation(image_path, ground_truth_ocr, ground_truth_translation)`**: Combines OCR extraction and translation evaluation into one process.

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




