# Invoice Field Extraction System

An AI-powered invoice field extraction system that detects and extracts key fields from invoice documents using computer vision, object detection, and OCR. The project is designed to automate manual invoice data entry by identifying fields such as invoice number, vendor details, dates, totals, and other important invoice information, then converting the extracted values into structured JSON output.

## Project Overview

Manual invoice processing is time-consuming and error-prone, especially when invoices come in different layouts and formats. This project solves that problem by combining an object detection model with OCR to automatically locate and extract important invoice fields.

The system uses YOLOv9 for detecting field regions, OpenCV for image preprocessing, PaddleOCR for text recognition, and ONNX Runtime for optimized inference.

## Key Features

- Detects key invoice fields using YOLOv9 object detection
- Extracts text from detected regions using PaddleOCR
- Supports invoice fields such as invoice number, vendor details, total amount, and other structured fields
- Uses OpenCV for preprocessing and image handling
- Converts extracted information into structured JSON format
- Supports dataset annotation and versioning using Roboflow
- Uses synthetic invoice data to improve model robustness
- Optimized model deployment using ONNX Runtime

## Tech Stack

- Python
- YOLOv9
- OpenCV
- PaddleOCR
- Roboflow
- ONNX Runtime
- NumPy
- JSON

## Architecture

```text
Invoice Image / PDF
        |
        v
Image Preprocessing using OpenCV
        |
        v
YOLOv9 Field Detection
        |
        v
Crop Detected Field Regions
        |
        v
Text Extraction using PaddleOCR
        |
        v
Post-processing and Field Mapping
        |
        v
Structured JSON Output
```

## How It Works

### 1. Data Collection and Annotation
Invoice samples are collected and annotated using Roboflow. Each key field is labeled, such as invoice number, vendor name, date, total amount, tax amount, and other relevant fields.

### 2. Model Training
A YOLOv9 object detection model is trained on the annotated dataset to detect invoice field regions. The model learns to identify where each field is located in invoices with different layouts.

### 3. Image Preprocessing
OpenCV is used to prepare invoice images before inference. This may include resizing, color conversion, noise reduction, thresholding, or cropping depending on the invoice quality.

### 4. Field Detection
The trained YOLOv9 model detects bounding boxes around key invoice fields. Each detection includes the predicted field label, confidence score, and bounding box coordinates.

### 5. OCR Extraction
Each detected field region is cropped and passed to PaddleOCR. PaddleOCR extracts the text from the selected region.

### 6. Post-processing
The extracted text is cleaned, normalized, and mapped to the correct field name. The final output is converted into structured JSON.

Example output:

```json
{
  "invoice_number": "INV-10234",
  "vendor_name": "ABC Trading LLC",
  "invoice_date": "2025-04-12",
  "total_amount": "AED 2,450.00"
}
```

## Folder Structure

```text
invoice-field-extraction/
│
├── data/
│   ├── raw_invoices/
│   ├── processed_images/
│   └── annotations/
│
├── models/
│   ├── yolov9_weights.pt
│   └── invoice_extractor.onnx
│
├── src/
│   ├── preprocess.py
│   ├── detect_fields.py
│   ├── ocr_extraction.py
│   ├── postprocess.py
│   └── main.py
│
├── outputs/
│   ├── extracted_json/
│   └── annotated_images/
│
├── requirements.txt
└── README.md
```

> Note: Folder names may be adjusted depending on the final repository structure.

## Installation

Clone the repository:

```bash
git clone <repository-url>
cd invoice-field-extraction
```

Create and activate a virtual environment:

```bash
python -m venv venv
source venv/bin/activate      # macOS/Linux
venv\Scripts\activate         # Windows
```

Install dependencies:

```bash
pip install -r requirements.txt
```

## Example Requirements

```text
opencv-python
paddleocr
paddlepaddle
numpy
onnxruntime
Pillow
roboflow
ultralytics
python-dotenv
```

## Usage

Run invoice extraction on a sample invoice:

```bash
python src/main.py --input data/raw_invoices/sample_invoice.jpg
```

Expected output:

```text
Extraction completed successfully.
Output saved to outputs/extracted_json/sample_invoice.json
```

## Model Training Workflow

1. Collect invoice samples
2. Annotate invoice fields in Roboflow
3. Export dataset in YOLO format
4. Train YOLOv9 model on annotated fields
5. Evaluate detection accuracy
6. Export trained model to ONNX for optimized inference
7. Integrate model with OCR pipeline

## Evaluation Metrics

The system can be evaluated using:

- Field detection precision
- Field detection recall
- OCR accuracy
- Exact match accuracy for extracted fields
- JSON completeness rate
- Processing time per invoice

## Challenges Solved

- Handling invoices with different layouts
- Detecting fields in noisy or low-quality invoice images
- Combining object detection with OCR for structured extraction
- Improving robustness using synthetic invoice data
- Mapping unstructured OCR text into clean JSON output

## Future Improvements

- Add support for multi-page PDF invoices
- Improve post-processing for dates, currencies, and tax fields
- Add confidence scoring for extracted values
- Add human review interface for low-confidence fields
- Integrate with accounting or ERP systems
- Add API endpoint using FastAPI
- Deploy as a containerized service using Docker

## Use Cases

- Accounts payable automation
- Finance document processing
- Vendor invoice management
- ERP data entry automation
- Document intelligence workflows

## Author

**Thirusha TK**  
AI Engineer / Junior Data Scientist  
Dubai, United Arab Emirates  
Email: thirushatk.me@gmail.com  
GitHub: github.com/thirusha

## License

This project is intended for educational and portfolio purposes. Add a license depending on repository usage.
