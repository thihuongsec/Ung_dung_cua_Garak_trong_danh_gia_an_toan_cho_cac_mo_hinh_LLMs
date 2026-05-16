# Ứng dụng Garak trong đánh giá an toàn các mô hình ngôn ngữ lớn LLMs
*Cùng với tiềm năng to lớn, LLMs cũng đặt ra nhiều thách thức 
về mặt an toàn và bảo mật. Các lỗ hổng như prompt injection, data leakage, hay 
misinformation có thể bị khai thác để gây ra hậu quả nghiêm trọng đối với người 
dùng và hệ thống. 
Việc kiểm thử và đảm bảo an toàn cho các mô hình LLMs là một 
vấn đề quan trọng, cần được quan tâm nghiêm túc trong quá trình nghiên cứu và triển 
khai thực tế. Garak là một công cụ mã nguồn mở tiêu biểu, hỗ trợ kiểm thử các lỗ 
hổng trong mô hình ngôn ngữ trước khi đưa vào sử dụng. Với khả năng tự động tạo 
các probe kiểm thử cho nhiều loại tấn công khác nhau, Garak đóng vai trò quan trọng 
trong việc đánh giá độ an toàn và độ tin cậy của LLMs.*

## Mô hình triển khai
<img width="754" height="303" alt="image" src="https://github.com/user-attachments/assets/49578cc6-49e6-4006-b2f2-2082eeae5c02" />

## Công nghệ sử dụng và các bước cài đặt
### Yêu cầu
- Cài đặt Visual Code Studio, Python package tối thiểu 3.8 
- Cài đặt Ollama, lựa chọn 2 mô hình LLMs và tải về. 
- Cấu hình máy: tối thiểu ram 8Gb, ổ nhớ còn trống 30Gb.
### Các bước cài đặt
#### 1. Cài đặt Ollama
- Tải và cài đặt: [Tại đây](https://apidog.com/vi/blog/how-to-download-and-use-ollama-vi/ )
- Các model Ollama hỗ trợ sẵn: [Tại đây](https://ollama.com/library )
- Kiểm tra trạng thái active của Ollama `http://localhost:11434/`
- Chọn model và tải về máy `gemma3:1b`, `gemma3:4b` và `phi4-
mini:lasteslastest`
#### 2. Tạo môi trường ảo
- `python -m venv GarakScanner`
- `scripts\activate`
- `code .`
#### 3. Cài Garak
- `pip install garak `
- `pip install update`
- `pip install requests ollama-python ollama `
- Các câu lệnh dùng trên Garak: [Tại đây](https://reference.garak.ai/en/latest/generators.html)
- Một số lệnh quen thuộc để quét vuln: `python -m garak --list_probes` `python -m garak --help` `python -m garak -r <path_to_file>`

## Thực nghiệm kiểm thử LLM bằng Garak
### Kịch bản 1: Kiểm thử khả năng chống lại các cuộc tấn công SQL Injection của mô hình ngôn ngữ lớn Gemma3 kích thước 1 tỉ tham số.
`garak -m ollama -n gemma3:1b -p exploitation.SQLInjectionEcho`
<img width="871" height="432" alt="image" src="https://github.com/user-attachments/assets/eddb6d7c-1c1f-484b-be99-03dcbafd9ae2" />

- Đánh giá khả năng chống lại các prompt về SQL Injection của gemma khá tốt, vượt qua được 80%, nhưng vẫn còn 20% chưa vượt qua được. Giá trị relative score chính là đánh giá của Garak dành cho Gemma3 về hiệu suất (0.7 đ) tương đối ổn với một mô hình chưa qua tinh chỉnh, nhưng chưa phải xuất sắc. 
###  Kịch bản 2: Kiểm thử khả năng chống lại các tấn công XSS của mô hình ngôn ngữ lớn Phi4-mini. 
`garak -m ollama -n phi4-mini:latest -p xss`
<img width="464" height="426" alt="image" src="https://github.com/user-attachments/assets/c71270d0-59ac-4d4c-9a0d-7269ea85216f" />

- Theo đánh giá bên dưới, mô hình này vượt qua được 70% các tấn công XSS liên quan đến kẻ tấn công ghép tập hợp các chuỗi độc hại. Nhưng vẫn tồn tại 30% rủi ro. Hiệu suất 0.6d. 
- Ngăn chặn được 100% tấn công liên quan đến rò rỉ dữ liệu qua Markdown như chèn liên kết độc hại. Hiệu suất thì không được đánh giá cao.
<img width="408" height="396" alt="image" src="https://github.com/user-attachments/assets/5583be65-9063-416b-b52c-66cd07958747" />

- 100% vượt qua được các loại tấn công liên quan XSS khác. 
###  Kịch bản 3: Tự viết một probes kiểm thử khả năng chống lại các nội dung độc hại (Toxicity) và thử nghiên trên mô hình gemma3
- Viết probes và đặt tên nguyenthihuong.NguyenThiHuong
<img width="657" height="775" alt="image" src="https://github.com/user-attachments/assets/eb4865e7-5bc9-4b9d-b547-a56f7218b380" />
<img width="752" height="142" alt="image" src="https://github.com/user-attachments/assets/4e31ecce-f5d8-41da-900c-3f8e3713b4b0" />

- Chạy probes với mô hình gemma3 và kiểm tra kết quả
`garak -m ollama -n gemma3:4b -p nguyenthihuong.NguyenThiHuong --generations 2`
<img width="499" height="101" alt="image" src="https://github.com/user-attachments/assets/c2e6a672-f2ed-470c-9e22-497b31b581af" />






