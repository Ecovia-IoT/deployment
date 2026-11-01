# Ecovia IoT — Deployment & Orchestration

> Môi trường triển khai trọn gói toàn bộ hệ sinh thái **Ecovia IoT** sử dụng Docker & Docker Compose.

---

## 📦 Kiến trúc triển khai

Bộ compose này kích hoạt 4 dịch vụ container hóa liên kết chặt chẽ với nhau:

1. **`ecovia-broker`** (`eclipse-mosquitto:2.0`):
   - Cổng TCP MQTT: `1883`
   - Cổng WebSocket MQTT: `9001`
   - Cấu hình tùy biến: `tools/mosquitto.conf`
2. **`ecovia-mongo`** (`mongo:7.0`):
   - Cổng: `27017`
   - Lưu trữ cơ sở dữ liệu telemetry dạng time-series
3. **`ecovia-backend`**:
   - Cổng: `4001`
   - Ingest MQTT, REST API, Socket.IO realtime, cảnh báo Telegram
4. **`ecovia-frontend`**:
   - Cổng: `3000` (Nginx reverse proxy tới Backend và Socket.IO)
   - Dashboard React 19 & Tailwind CSS

---

## 🚀 Hướng dẫn khởi chạy

### Cách 1: Sử dụng mã nguồn đã clone sẵn

Nếu bạn đã clone các repo `backend` và `frontend` cạnh thư mục này:

```bash
git clone https://github.com/Ecovia-IoT/backend.git backend
git clone https://github.com/Ecovia-IoT/frontend.git frontend

docker compose up --build -d
```

### Cách 2: Kiểm tra trạng thái dịch vụ

```bash
docker compose ps
docker compose logs -f backend
```

- **Dashboard:** [http://localhost:3000](http://localhost:3000)
- **Backend Health:** [http://localhost:4001/health](http://localhost:4001/health)
- **MQTT Broker:** `localhost:1883`

---

## 🛑 Dừng hệ thống

```bash
docker compose down
```
