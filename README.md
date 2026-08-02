# urdu-ocr-codesaviours-si26-warood

Urdu OCR Project | Code Saviours SI-26 | Warood Zahra Khan

## Research Summary

**What is OCR (Optical Character Recognition)?**
OCR stands for Optical Character Recognition, and it is a technology that allows computers to read text from images instead of just seeing them as pictures. When you scan a document or take a photo of text, OCR analyzes the shapes in the image and converts them into actual digital text that a computer can understand. This means the text becomes editable, searchable, and copyable, rather than being a static image that a computer cannot interpret.

**Why is Urdu OCR harder than English OCR?**
Urdu OCR is more difficult than English OCR mainly because of how the script is written. Urdu uses a cursive, connected writing style where letters change shape depending on whether they appear at the beginning, middle, or end of a word, unlike English letters which stay mostly the same shape. Urdu is also written from right to left, and it often includes dots, stacked characters, and diacritical marks that can look very similar to each other, making it harder for a model to tell characters apart. On top of that, there is far less labeled Urdu training data available compared to English, since English OCR research has been developed for a much longer time.

**What are 2 real-world situations where Urdu OCR would be useful?**
## Research Task

**1. What is OCR (Optical Character Recognition)?**
OCR stands for Optical Character Recognition, and it is a technology that allows computers to read text from images instead of just seeing them as pictures. When you scan a document or take a photo of text, OCR analyzes the shapes in the image and converts them into actual digital text that a computer can understand. This means the text becomes editable, searchable, and copyable, rather than being a static image that a computer cannot interpret.

**2. Why is Urdu OCR harder than English OCR?**
Urdu OCR is more difficult than English OCR mainly because of how the script is written. Urdu uses a cursive, connected writing style where letters change shape depending on whether they appear at the beginning, middle, or end of a word, unlike English letters which stay mostly the same shape. Urdu is also written from right to left, and it often includes dots, stacked characters, and diacritical marks that can look very similar to each other, making it harder for a model to tell characters apart. On top of that, there is far less labeled Urdu training data available compared to English, since English OCR research has been developed for a much longer time.

**3. What are 2 real-world situations where Urdu OCR would be useful?**
One real-world use of Urdu OCR is digitizing old Urdu newspapers, books, and historical or government documents so they can be preserved digitally and made searchable for research purposes. Another useful application is helping visually impaired Urdu readers, since OCR can convert printed text like signs, letters, or menus into speech using text-to-speech tools. Both of these examples show how OCR can make Urdu content more accessible and easier to preserve for the future.


## Why We Need a Better Model

**Gap Analysis — Tesseract OCR on Urdu Images**

**Image 1: کلو میٹر.png**
- Actual text: کلو میٹر
- Tesseract output: (empty — nothing detected)
- What went wrong: Complete failure to detect any text.

**Image 2: تجارتی جہاز.png**
- Actual text: تجارتی جہاز
- Tesseract output: تجادخی چنہاز
- What went wrong: Wrong characters — letters were misread and jumbled, producing a completely different (meaningless) word.

**Image 3: سسٹم میں خرابی.png**
- Actual text: سسٹم میں خرابی
- Tesseract output: (empty — nothing detected)
- What went wrong: Complete failure to detect any text.

**Image 4: عبوری حکومت.png**
- Actual text: عبوری حکومت
- Tesseract output: سبوری حکیم
- What went wrong: Wrong characters — similar-looking letters were confused (ع→س, ت→م), resulting in a different, incorrect word.

**Image 5: نماز جنازہ.png**
- Actual text: نماز جنازہ
- Tesseract output: (empty — nothing detected)
- What went wrong: Complete failure to detect any text.

**Summary:**
Tesseract fails on Urdu because the script is cursive and context-dependent — letters change shape depending on their position in a word (beginning, middle, end), which confuses Tesseract's character segmentation. It also struggles with the right-to-left flow and closely-spaced joined letters, often either detecting nothing at all or misreading visually similar letters (like ع and س) as one another. This shows that a generic OCR engine trained mainly on Latin-script and limited Urdu data cannot reliably read real-world Urdu text — which is exactly why we need a custom-trained model for this project.
