# 🚀 Hướng dẫn Deploy lên Hugging Face Spaces

## 📋 Yêu cầu

1. Tài khoản Hugging Face (miễn phí): https://huggingface.co/join
2. Git được cài đặt trên máy

---

## 📦 Bước 1: Tạo Space mới trên Hugging Face

1. Truy cập: https://huggingface.co/new-space
2. Điền thông tin:
   - **Owner**: Chọn tài khoản của bạn
   - **Space name**: `document-processor` (hoặc tên bạn muốn)
   - **License**: MIT
   - **SDK**: Chọn **Streamlit**
   - **Hardware**: CPU basic (miễn phí)
3. Click **Create Space**

---

## 📤 Bước 2: Clone và Push code

### Cách 1: Sử dụng Git (Đề xuất)

```bash
# 1. Clone Space rỗng về máy
git clone https://huggingface.co/spaces/YOUR_USERNAME/document-processor
cd document-processor

# 2. Copy tất cả files từ thư mục dự án vào đây
# (app.py, requirements.txt, README.md, .gitattributes)

# 3. Commit và push
git add .
git commit -m "Initial commit: Document Processor app"
git push
```

### Cách 2: Upload trực tiếp trên Web

1. Vào Space của bạn trên HF
2. Click tab **Files and versions**
3. Click **Add file** → **Upload files**
4. Kéo thả các files:
   - `app.py`
   - `requirements.txt`
   - `README.md`
   - `.gitattributes`
5. Click **Commit changes**

---

## ⏳ Bước 3: Chờ Build

- Hugging Face sẽ tự động:
  1. Detect Streamlit SDK từ README.md
  2. Cài đặt dependencies từ requirements.txt
  3. Chạy app.py
  
- Thời gian build: **5-10 phút** (lần đầu lâu hơn vì cài easyocr)
- Theo dõi logs tại tab **Logs**

---

## 🎉 Bước 4: Truy cập App

Sau khi build thành công:
- URL: `https://huggingface.co/spaces/YOUR_USERNAME/document-processor`
- Hoặc: `https://YOUR_USERNAME-document-processor.hf.space`

---

## ⚠️ Lưu ý quan trọng

### 1. RAM và Timeout
- Free tier: 2 vCPU, 16GB RAM
- OCR lần đầu sẽ tải model (~100MB), sau đó cache
- Nếu cần nhiều tài nguyên hơn, upgrade lên GPU tier

### 2. File Size Limits
- Upload file limit: 5GB
- Phù hợp cho hầu hết documents

### 3. Secrets (nếu cần API keys sau này)
- Vào **Settings** → **Secrets**
- Thêm biến môi trường bí mật

### 4. Custom Domain (tùy chọn)
- Vào **Settings** → **Custom URL**
- Có thể map domain riêng

---

## 🔧 Troubleshooting

### App không khởi động
- Kiểm tra tab **Logs** để xem lỗi
- Đảm bảo `app.py` là tên file chính xác

### Lỗi dependencies
- Kiểm tra phiên bản trong `requirements.txt`
- Thử bỏ version constraints nếu conflict

### OCR chậm lần đầu
- Bình thường! Model easyocr cần download
- Các lần sau sẽ nhanh hơn (cached)

### Restart Space
- Vào **Settings** → **Factory restart**

---

## 📁 Cấu trúc files cần upload

```
document-processor/
├── app.py              # Main Streamlit app (BẮT BUỘC)
├── requirements.txt    # Dependencies (BẮT BUỘC)
├── README.md          # With YAML frontmatter (BẮT BUỘC)
└── .gitattributes     # Git config (khuyến khích)
```

---

## 🔗 Links hữu ích

- [Hugging Face Spaces Documentation](https://huggingface.co/docs/hub/spaces)
- [Streamlit on Spaces](https://huggingface.co/docs/hub/spaces-sdks-streamlit)
- [Spaces Hardware](https://huggingface.co/docs/hub/spaces-gpus)

---

*Happy deploying! 🎉*
