# XIAOZHI ESP32-S3 CLEAN MOBILE OS (V2.0 OPEN EDITION)

Dự án firmware mã nguồn mở sạch 100% dành cho Chatbot Xiaozhi ESP32-S3 (Màn hình 2.8" AIO), loại bỏ hoàn toàn mã kiểm tra bản quyền, không giới hạn thời gian sử dụng, tích hợp giao diện **Mobile OS hiện đại (dạng Smartphone / Smart Display)**.

---

## 📱 ĐẶC ĐIỂM GIAO DIỆN MOBILE UI HIỆN ĐẠI

1. **Thanh trạng thái di động (Top Status Bar)**:
   - Đồng hồ thời gian thực (`12:00`).
   - Icon trạng thái đám mây / Server riêng (`Connected / Disconnected`).
   - Icon sóng Wi-Fi.
   - Icon mức pin (%) đo trực tiếp từ ADC.

2. **Giao diện 3 Tab vuốt trượt (Mobile Tabview)**:
   - **Tab 1: AI Companion (Màn hình chính Chatbot)**:
     - Avatar AI phát sáng đổi màu sinh động theo trạng thái: *Sẵn sàng (Xanh dương)*, *Đang nghe (Xanh lá)*, *Đang nghĩ (Cam)*, *Đang nói (Tím)*.
     - Bong bóng lời thoại trò chuyện (Chat bubble) phong cách tin nhắn iOS / Messenger.
     - Nút Micro nổi (Floating Action Button) cảm ứng chạm để đàm thoại.
   - **Tab 2: Tiện ích & Smart Home (Widgets & Control Center)**:
     - Widget Thời tiết: Nhiệt độ, thành phố, tình trạng thời tiết.
     - Widget Media Player: Tên bài hát/radio đang phát, thanh tiến trình âm thanh.
     - Widget Nhà thông minh: 3 công tắc Relay bật/tắt Đèn, Quạt, Thiết bị phụ.
   - **Tab 3: Cài đặt (Settings)**:
     - Thanh kéo cảm ứng điều chỉnh độ sáng màn hình (PWM Backlight).
     - Thanh kéo cảm ứng điều chỉnh âm lượng loa Codec ES8311.
     - Thông tin mạng IP, Server WebSocket riêng và trạng thái bản quyền vĩnh viễn.

---

## 🔌 SƠ ĐỒ CHÂN PHẦN CỨNG (PINOUT)

| Module | Tín hiệu | Chân ESP32-S3 | Ghi chú |
| :--- | :--- | :--- | :--- |
| **Màn hình ILI9341** | MOSI | GPIO 13 | SPI2 Host |
| | SCLK | GPIO 12 | SPI Clock |
| | CS | GPIO 10 | Chip Select |
| | DC | GPIO 11 | Data / Command |
| | RST | GPIO 1 | Reset LCD |
| | Backlight | GPIO 40 | PWM độ sáng màn hình |
| **Cảm ứng FT6236** | SDA | GPIO 8 | I2C Bus |
| | SCL | GPIO 9 | I2C Bus |
| | INT | GPIO 3 | Touch Interrupt |
| **Codec ES8311** | MCLK | GPIO 2 | Master Clock I2S |
| | BCLK | GPIO 14 | Bit Clock |
| | WS (LRCK) | GPIO 15 | Word Select |
| | DOUT | GPIO 16 | Dữ liệu phát ra Loa |
| | DIN | GPIO 17 | Dữ liệu thu từ Micro |
| **Relays** | Relay 1 (Đèn) | GPIO 4 | Điều khiển qua UI / MCP |
| | Relay 2 (Quạt) | GPIO 5 | Điều khiển qua UI / MCP |
| | Relay 3 (Phụ) | GPIO 21 | Điều khiển qua UI / MCP |
| **Đo Pin** | ADC Pin | GPIO 1 (ADC1_CH0) | Phân áp đo điện áp pin |

---

## 🛠 HƯỚNG DẪN BIÊN DỊCH VÀ NẠP FIRMWARE

### Yêu cầu:
- Đã cài đặt **ESP-IDF v5.1** hoặc **v5.3**.

### Các bước thực hiện:
```bash
# 1. Điều hướng vào thư mục dự án
cd "c:\Users\User\Desktop\Project Antigravity\Chatbot Xiaozhi ESP32"

# 2. Thiết lập target ESP32-S3
idf.py set-target esp32s3

# 3. Biên dịch dự án
idf.py build

# 4. Cắm cáp USB bo mạch ESP32-S3 và nạp firmware
idf.py -p COM_PORT flash monitor
```

---

## 🌐 HƯỚNG DẪN KẾT NỐI SERVER RIÊNG

1. **Khởi động lần đầu**: Nếu chưa lưu Wi-Fi, bo mạch sẽ phát một mạng Wi-Fi tên `Xiaozhi-Setup` (mật khẩu: `12345678`).
2. Kết nối vào Wi-Fi này và truy cập: `http://192.168.4.1`.
3. Nhập tên Wi-Fi nhà bạn, mật khẩu và điền địa chỉ WebSocket Server riêng:
   `ws://<IP_MÁY_CHỦ_CỦA_BẠN>:8000/ws`
4. Bấm **LƯU & KHỞI ĐỘNG LẠI**. Mạch sẽ tự động kết nối và đàm thoại mượt mà với server của bạn vĩnh viễn!
