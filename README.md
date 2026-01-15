---
title: Document Processor
emoji: 📄
colorFrom: purple
colorTo: blue
sdk: streamlit
sdk_version: 1.30.0
app_file: app.py
pinned: false
license: mit
---

# 📄 Document Processor

> **Unified Document Report Generator** - Ứng dụng web xử lý tài liệu đa định dạng và tổng hợp thành báo cáo thống nhất.

![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=Streamlit&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)

---

## 📋 Mục lục

- [Giới thiệu](#-giới-thiệu)
- [Tính năng](#-tính-năng)
- [Cài đặt](#-cài-đặt)
- [Sử dụng](#-sử-dụng)
- [Kiến trúc](#-kiến-trúc)
- [Chi tiết kỹ thuật](#-chi-tiết-kỹ-thuật)
- [API Reference](#-api-reference)
- [Cấu trúc Output](#-cấu-trúc-output)

---

## 🎯 Giới thiệu

**Document Processor** là ứng dụng web được xây dựng bằng Streamlit, cho phép người dùng:

1. Upload nhiều file với các định dạng khác nhau
2. Trích xuất nội dung từ từng file
3. Tổng hợp tất cả thành **MỘT báo cáo duy nhất**
4. Export dưới dạng Markdown (.md) hoặc HTML (.html)

### 🔑 Triết lý cốt lõi

> **ZERO Content Alteration** - Không tóm tắt, không viết lại, không thêm thông tin. Trích xuất chính xác như file gốc.

---

## ✨ Tính năng

### 📁 Định dạng hỗ trợ

| Định dạng | Extension | Mô tả xử lý |
|-----------|-----------|-------------|
| **Excel** | `.xlsx`, `.xls` | Chuyển đổi từng sheet thành Markdown table |
| **Word** | `.docx` | Trích xuất paragraphs và tables, giữ nguyên headings |
| **PDF** | `.pdf` | Extract text và tables theo từng page với pdfplumber |
| **Text** | `.txt` | Đọc trực tiếp với multi-encoding support |
| **Images** | `.png`, `.jpg`, `.jpeg` | OCR trích xuất text (hỗ trợ Tiếng Việt & English) |
| **Markdown** | `.md` | Đọc và giữ nguyên format, hỗ trợ convert sang HTML |

### 🛠️ Chức năng chính

- ✅ **Multi-file Upload** - Tải lên nhiều file cùng lúc
- ✅ **Auto Table of Contents** - Tự động tạo mục lục với links
- ✅ **Table Extraction** - Trích xuất bảng và chuyển sang Markdown format
- ✅ **OCR for Images** - Nhận dạng chữ trong ảnh (VI/EN)
- ✅ **MD to HTML Conversion** - Convert file Markdown sang HTML
- ✅ **Error Handling** - Bỏ qua file lỗi, tiếp tục xử lý file khác
- ✅ **Dual Export** - Xuất Markdown hoặc HTML với GitHub-style CSS
- ✅ **Preview** - Xem trước kết quả ngay trong ứng dụng

---

## 🚀 Cài đặt

### Yêu cầu hệ thống

- Python 3.9+
- pip (Python package manager)

### Bước 1: Clone/Tạo thư mục dự án

```bash
mkdir document-processor
cd document-processor
```

### Bước 2: Cài đặt dependencies

```bash
python -m pip install -r requirements.txt
```

### Dependencies chi tiết

```txt
# Streamlit UI Framework
streamlit>=1.30.0

# Excel Processing
pandas>=2.0.0
openpyxl>=3.1.0
xlrd>=2.0.0

# Word Document Processing
python-docx>=1.1.0

# PDF Processing (with table extraction)
pdfplumber>=0.10.0

# Markdown to HTML conversion
markdown>=3.5.0

# Image Processing & OCR
Pillow>=10.0.0
easyocr>=1.7.0
```

### Bước 3: Chạy ứng dụng

```bash
python -m streamlit run app.py
```

Truy cập: **http://localhost:8501**

---

## 📖 Sử dụng

### Quy trình cơ bản

```
1. Upload Files → 2. Click "Process Documents" → 3. Preview → 4. Download
```

### Hướng dẫn chi tiết

#### 1️⃣ Upload Files

- Kéo thả hoặc click "Browse files"
- Có thể upload nhiều file cùng lúc
- Hỗ trợ: Excel, Word, PDF, Text, Images, Markdown

#### 2️⃣ Xử lý

- Click nút **"🚀 Process Documents"**
- Thanh progress bar hiển thị tiến trình
- File lỗi sẽ được thông báo nhưng không dừng xử lý

#### 3️⃣ Preview

- **Tab Markdown**: Xem nội dung đã render
- **Tab HTML**: Xem trong iframe với CSS styling

#### 4️⃣ Download

- **📄 Download as Markdown (.md)** - File plain text với Markdown syntax
- **🌐 Download as HTML (.html)** - File HTML với GitHub-style CSS

---

## 🏗️ Kiến trúc

### Cấu trúc thư mục

```
document-processor/
├── app.py              # Main application (Streamlit + Processing logic)
├── requirements.txt    # Python dependencies
└── README.md          # Documentation
```

### Class Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                    DocumentProcessor                         │
├─────────────────────────────────────────────────────────────┤
│ - processed_files: List[ProcessedFile]                      │
│ - warnings: List[str]                                        │
│ - _ocr_reader: easyocr.Reader (lazy)                        │
├─────────────────────────────────────────────────────────────┤
│ + process_files(uploaded_files) → str                        │
│ - _process_excel(file) → str                                 │
│ - _process_word(file) → str                                  │
│ - _process_pdf(file) → str                                   │
│ - _process_text(file) → str                                  │
│ - _process_image(file) → str                                 │
│ - _aggregate_content() → str                                 │
│ - _get_ocr_reader() → easyocr.Reader                        │
│ - _dataframe_to_markdown(df) → str                          │
│ - _word_table_to_markdown(table) → str                      │
│ - _pdf_table_to_markdown(table) → str                       │
│ - _clean_pdf_text(text) → str                               │
│ - _create_anchor(filename) → str                            │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│                     ProcessedFile                            │
├─────────────────────────────────────────────────────────────┤
│ + filename: str                                              │
│ + file_type: str                                             │
│ + content: str                                               │
│ + success: bool                                              │
│ + error_message: Optional[str]                               │
└─────────────────────────────────────────────────────────────┘
```

### Flow Diagram

```
┌──────────────┐     ┌──────────────────┐     ┌────────────────┐
│  User Upload │────▶│ DocumentProcessor│────▶│ Aggregated MD  │
│  Multiple    │     │  process_files() │     │    Content     │
│  Files       │     └──────────────────┘     └────────────────┘
└──────────────┘              │                       │
                              ▼                       ▼
                    ┌─────────────────┐      ┌───────────────┐
                    │ Per-file Router │      │ generate_html │
                    │ (by extension)  │      │    (CSS)      │
                    └─────────────────┘      └───────────────┘
                              │                       │
         ┌────────────────────┼────────────────────┐  │
         ▼          ▼         ▼         ▼          ▼  ▼
    ┌────────┐ ┌────────┐ ┌───────┐ ┌──────┐ ┌───────┐
    │ Excel  │ │  Word  │ │  PDF  │ │ Text │ │ Image │
    │ Engine │ │ Engine │ │Engine │ │Engine│ │ (OCR) │
    └────────┘ └────────┘ └───────┘ └──────┘ └───────┘
```

---

## 🔧 Chi tiết kỹ thuật

### 📊 Excel Processing

```python
# Engine selection based on file extension
engine = 'openpyxl' if file_ext == 'xlsx' else 'xlrd'

# Read each sheet as string to preserve data
df = pd.read_excel(
    excel_file, 
    sheet_name=sheet_name,
    dtype=str,        # Preserve original format
    na_filter=False   # Don't convert empty to NaN
)
```

**Logic:**
1. Xác định engine dựa trên extension (openpyxl cho .xlsx, xlrd cho .xls)
2. Đọc TẤT CẢ sheets trong workbook
3. Mỗi sheet → Markdown table với header `### 📊 Sheet: {name}`
4. Giữ nguyên data types bằng cách đọc tất cả dưới dạng string

### 📝 Word Processing

```python
# Iterate through document body elements in ORDER
for element in doc.element.body:
    if element.tag.endswith('p'):   # Paragraph
        # Check heading style → Convert to Markdown header
    elif element.tag.endswith('tbl'):  # Table
        # Convert to Markdown table format
```

**Logic:**
1. Duyệt qua từng element trong document body (giữ đúng thứ tự)
2. Nhận dạng Heading styles (Heading 1, 2, 3...) → `#`, `##`, `###`
3. Tables → Markdown table format
4. Thứ tự được bảo toàn hoàn toàn

### 📕 PDF Processing

```python
with pdfplumber.open(file) as pdf:
    for page in pdf.pages:
        # 1. Extract tables first
        tables = page.extract_tables()
        
        # 2. Extract remaining text
        text = page.extract_text()
```

**Tại sao dùng pdfplumber?**
- ✅ Phát hiện bảng chính xác hơn PyPDF2
- ✅ Xử lý được cấu trúc bảng phức tạp
- ✅ Giữ nguyên boundaries của cells
- ✅ Định vị text chính xác hơn

**Logic:**
1. Mở PDF và duyệt qua từng page
2. Phát hiện và trích xuất tables trước (dựa trên line boundaries)
3. Trích xuất text còn lại (không thuộc table)
4. Mỗi page có header `#### 📄 Page {n}/{total}`

### 🖼️ Image Processing (OCR)

```python
# Lazy initialization
if self._ocr_reader is None:
    self._ocr_reader = easyocr.Reader(['vi', 'en'], gpu=False)

# OCR processing
results = reader.readtext(image_array, detail=1, paragraph=False)
# Returns: [(bbox, text, confidence), ...]
```

**Tại sao dùng easyocr?**
- ✅ Pure Python, không cần cài Tesseract
- ✅ Deep learning based, độ chính xác cao
- ✅ Hỗ trợ 80+ ngôn ngữ (bao gồm tiếng Việt)
- ✅ Xử lý tốt với ảnh chất lượng khác nhau

**Logic:**
1. Load ảnh với PIL, convert sang RGB
2. Convert sang numpy array cho easyocr
3. Chạy OCR, nhận kết quả với confidence scores
4. Lọc text với confidence ≥ 30%
5. Ghép các dòng theo thứ tự đọc (top-to-bottom, left-to-right)

**Lưu ý:** Lần đầu chạy OCR sẽ tải model (~100MB), sau đó được cache.

---

## 📚 API Reference

### `DocumentProcessor`

#### `__init__()`
Khởi tạo processor với danh sách file và warnings rỗng.

#### `process_files(uploaded_files: List) → str`
Xử lý tất cả file và trả về Markdown aggregated content.

| Parameter | Type | Description |
|-----------|------|-------------|
| `uploaded_files` | `List[UploadedFile]` | Danh sách file từ Streamlit |

**Returns:** `str` - Markdown document với ToC và nội dung tất cả file

### `generate_html(markdown_content: str) → str`

Chuyển Markdown sang HTML với GitHub-style CSS.

| Parameter | Type | Description |
|-----------|------|-------------|
| `markdown_content` | `str` | Markdown string |

**Returns:** `str` - Complete HTML document với embedded CSS

---

## 📄 Cấu trúc Output

### Markdown Output Structure

```markdown
# 📚 Unified Document Report

*Generated: 2026-01-15 16:00:00*
*Total files: 5 | Successful: 5*

## 📋 Table of Contents

1. ✅ [report.xlsx](#report-xlsx) `[XLSX]`
2. ✅ [contract.docx](#contract-docx) `[DOCX]`
3. ✅ [invoice.pdf](#invoice-pdf) `[PDF]`
4. ✅ [notes.txt](#notes-txt) `[TXT]`
5. ✅ [screenshot.png](#screenshot-png) `[PNG]`

---

## 📄 report.xlsx {#report-xlsx}

**File Type:** XLSX

### 📊 Sheet: Data
| Column A | Column B | Column C |
| --- | --- | --- |
| Value 1 | Value 2 | Value 3 |

---

## 📄 contract.docx {#contract-docx}

**File Type:** DOCX

## Heading from Word
Paragraph content...

| Table Header 1 | Table Header 2 |
| --- | --- |
| Cell 1 | Cell 2 |

---

## 📄 invoice.pdf {#invoice-pdf}

**File Type:** PDF

#### 📄 Page 1/2

**Table 1:**
| Invoice # | Amount |
| --- | --- |
| 001 | $100 |

Text content from PDF...

---

## 📄 notes.txt {#notes-txt}

**File Type:** TXT

Plain text content here...

---

## 📄 screenshot.png {#screenshot-png}

**File Type:** PNG

**Image Size:** 1920 × 1080 pixels

### 📝 Extracted Text

Text detected by OCR...

*OCR Confidence: Text extracted with varying confidence levels*

---
```

### HTML Output Features

- **GitHub-style CSS** - Clean, readable typography
- **Responsive Design** - Mobile-friendly
- **Print-ready** - Optimized for printing
- **Table Styling** - Zebra stripes, borders
- **Code Blocks** - Syntax highlighting ready

---

## 🔒 Error Handling

| Scenario | Behavior |
|----------|----------|
| File không đọc được | Log warning, skip file, tiếp tục xử lý |
| Encoding không nhận dạng (Text) | Thử nhiều encodings: UTF-8, UTF-8-BOM, Latin-1, CP1252 |
| PDF không có text | Hiển thị "*No extractable content*" |
| Ảnh không có text | Hiển thị "*No text detected in image*" |
| Format không hỗ trợ | Raise ValueError, log error |

---

## 📝 License

MIT License - Free to use and modify.

---

## 👨‍💻 Author

Built with ❤️ using Streamlit

---

*Last updated: 2026-01-15*
