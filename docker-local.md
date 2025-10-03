# Chạy MinIO Local với Docker Compose

## 1. Cài đặt Docker Desktop + WSL2
- Bật WSL2 Integration cho distro Ubuntu
- Cài đặt Docker Compose

## 2. Tạo thư mục dự án
```bash
mkdir ~/minio && cd ~/minio
```

## 3. Tạo file `docker-compose.yml`
Ví dụ:
```yaml
version: "3.8"

services:
  minio:
    image: minio/minio:latest
    container_name: minio
    ports:
      - "9000:9000"   # S3 API
      - "9090:9090"   # MinIO Console
    volumes:
      - ./data:/data
    environment:
      - MINIO_ROOT_USER=admin
      - MINIO_ROOT_PASSWORD=yourpassword
    command: server /data --console-address ":9090"
```

## 4. Khởi động MinIO
```bash
docker compose up -d
```

## 5. Truy cập
- Console: [https://localhost:9090](https://localhost:9090)  
- API (S3): [https://localhost:9000](https://localhost:9000)

> ⚠️ Lúc này MinIO dùng **self-signed SSL**, chỉ để test local.
