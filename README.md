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
1. Cài đặt Ollama
- Tải và cài đặt: [Tại đây](https://apidog.com/vi/blog/how-to-download-and-use-ollama-vi/ )
- Các model Ollama hỗ trợ sẵn: [Tại đây](https://ollama.com/library )
- Kiểm tra trạng thái active của Ollama `http://localhost:11434/`
- Chọn model và tải về máy `gemma3:1b`, `gemma3:4b` và `phi4-
mini:lasteslastest`
2. Tạo môi trường ảo
- `python -m venv GarakScanner`
- `scripts\activate`
- `code .`
3. Cài Garak
- `pip install garak `
- `pip install update`
- `pip install requests ollama-python ollama `
- Các câu lệnh dùng trên Garak: [Tại đây](https://reference.garak.ai/en/latest/generators.html)
- Một số lệnh quen thuộc để quét vuln: `python -m garak --list_probes` `python -m garak --help` `python -m garak -r <path_to_file>`
