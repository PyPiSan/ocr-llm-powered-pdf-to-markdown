# OCR: LLM Powered Fast OCR ⚡
Modified Version of this repo https://github.com/yigitkonur/swift-ocr-llm-powered-pdf-to-markdown

## 🌟 Features

- **Flexible Input Options**: Accepts PDF files via direct upload or by specifying a URL.
- **Advanced OCR Processing**: Utilizes OpenAI's GPT-4 Turbo with Vision model for accurate text extraction.
- **Performance Optimizations**:
  - **Parallel PDF Conversion**: Converts PDF pages to images concurrently using multiprocessing.
  - **Batch Processing**: Processes multiple images in batches to maximize throughput.
  - **Retry Mechanism with Exponential Backoff**: Ensures resilience against transient failures and API rate limits.
- **Structured Output**: Extracted text is formatted using Markdown for readability and consistency.
- **Robust Error Handling**: Comprehensive logging and exception handling for reliable operations.
- **Scalable Architecture**: Asynchronous processing enables handling multiple requests efficiently.

## 🛠️ Installation

### Prerequisites

- Python 3.8+
- [Git](https://git-scm.com/)
- [Virtualenv](https://virtualenv.pypa.io/en/latest/) (optional but recommended)

### Steps

1. **Clone the Repository**

   ```bash
   git clone https://github.com/PyPiSan/ocr-llm-powered-pdf-to-markdown.git
   cd ocr-llm-powered-pdf-to-markdown
   ```

2. **Create a Virtual Environment**

   ```bash
   python3 -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install Dependencies**

   ```bash
   pip install -r requirements.txt
   ```

4. **Configure Environment Variables**

   Create a `.env` file in the root directory and add the following variables:

   ```env
   OPENAI_API_KEY=your_openai_api_key
   OPENAI_API_VERSION=your_openai_api_version  # Default is "gpt-4o"
   BATCH_SIZE=10  # Optional: Default is 1
   MAX_CONCURRENT_OCR_REQUESTS=5  # Optional: Default is 5
   MAX_CONCURRENT_PDF_CONVERSION=4  # Optional: Default is 4
   ```

   > **Note:** Replace `your_openai_api_key`, `your_azure_openai_endpoint`, and `your_openai_deployment_id` with your actual OpenAI credentials.

5. **Run the Application**

   ```bash
   uvicorn main:app --reload
   ```

   The API will be available at `http://127.0.0.1:8000`.

## 🎯 Usage

### API Endpoint

**POST** `/ocr`

#### Request Parameters

- **file**: (Optional) Upload a PDF file.
- **ocr_request.url**: (Optional) URL of the PDF to process.

*You must provide either a file or a URL, not both.*

#### Example Using `curl`

**Uploading a PDF File:**

```bash
curl -X POST "http://127.0.0.1:8000/ocr" -F "file=@/path/to/your/document.pdf"
```

**Providing a PDF URL:**

```bash
curl -X POST "http://127.0.0.1:8000/ocr" -F "ocr_request={\"url\": \"https://example.com/document.pdf\"}" -H "Content-Type: application/json"
```

#### Response

- **200 OK**

  ```json
  {
    "text": "Extracted and formatted text from the PDF."
  }
  ```

- **Error Responses**

  - `400 Bad Request`: Invalid input parameters.
  - `422 Unprocessable Entity`: Validation errors.
  - `500 Internal Server Error`: Processing errors.

## 🧰 Configuration

All configurations are managed via environment variables. Ensure you have a `.env` file set up with the necessary variables as described in the [Installation](#installation) section.

### Key Configuration Variables

- **OPENAI_API_KEY**: Your OpenAI API key.
- **OPENAI_API_VERSION**: API version for OpenAI (default: "gpt-4o").
- **BATCH_SIZE**: Number of images to process per OCR request (default: 1).
- **MAX_CONCURRENT_OCR_REQUESTS**: Maximum number of concurrent OCR requests (default: 5).
- **MAX_CONCURRENT_PDF_CONVERSION**: Maximum number of concurrent PDF page conversions (default: 4).
Here's the revised license section with the requested changes:

## 📜 License ([thx for issue](https://github.com/yigitkonur/swift-ocr-llm-powered-pdf-to-markdown/issues/1))

Please note that PyMuPDF requires changing the license to GNU AGPL v3.0. You can fork this project, implement pdf2image, and use it freely. While I don't have any particular interest in licensing, I am legally obligated to add this information.

GNU AFFERO GENERAL PUBLIC LICENSE
Version 3, 19 November 2007

Copyright (C) 2024 Yiğit Konur

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Affero General Public License as published
by the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Affero General Public License for more details.

You should have received a copy of the GNU Affero General Public License
along with this program.  If not, see <https://www.gnu.org/licenses/>.
