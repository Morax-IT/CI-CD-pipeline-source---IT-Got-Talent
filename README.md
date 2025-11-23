# Bookteria

A microservices-based social network platform for book lovers, built with Spring Boot and React.

## 📖 Giới thiệu

Bookteria là một nền tảng mạng xã hội toàn diện được thiết kế cho những người yêu sách để chia sẻ, khám phá và thảo luận về sách. Dự án tuân theo kiến trúc microservices, đảm bảo khả năng mở rộng, dễ bảo trì và tách biệt các mối quan tâm.

## 🏗️ Kiến trúc Hệ thống

Hệ thống được xây dựng theo kiến trúc microservices với các thành phần sau:

### Dịch vụ Backend

- **API Gateway** (Cổng 8888)
  - Spring Cloud Gateway
  - Điểm vào duy nhất cho tất cả các request từ client
  - Định tuyến request và cân bằng tải
  - Xử lý xác thực và phân quyền

- **Identity Service** (Cổng 8080)
  - Xác thực và phân quyền người dùng
  - Quản lý JWT token
  - Quản lý Người dùng, Vai trò và Quyền
  - Cơ sở dữ liệu MySQL
  - Producer sự kiện Kafka cho thông báo

- **Profile Service** (Cổng 8081)
  - Quản lý hồ sơ người dùng
  - Các thao tác CRUD thông tin hồ sơ

- **Notification Service** (Cổng 8082)
  - Xử lý thông báo thời gian thực
  - Consumer sự kiện Kafka
  - Hệ thống gửi thông báo

- **Post Service** (Cổng 8083)
  - Tạo và quản lý bài đăng
  - Cơ sở dữ liệu MongoDB
  - Tính năng quản lý nội dung

- **Các Dịch vụ Bổ sung** (Đang phát triển)
  - Book Service - Dịch vụ quản lý sách
  - File Service - Dịch vụ quản lý file
  - Search Service - Dịch vụ tìm kiếm

### Frontend

- **Ứng dụng Web**
  - React 18.3.1 với Material-UI
  - React Router cho điều hướng
  - Axios cho giao tiếp API
  - Thiết kế responsive

## 🛠️ Công nghệ Sử dụng

### Backend
- **Framework**: Spring Boot 3.2.5
- **Ngôn ngữ**: Java 21
- **API Gateway**: Spring Cloud Gateway
- **Bảo mật**: Spring Security (OAuth2 Resource Server)
- **Cơ sở dữ liệu**: 
  - MySQL (cho Identity Service)
  - MongoDB (cho Post Service)
- **Message Broker**: Apache Kafka
- **Công cụ Build**: Maven
- **Thư viện**:
  - MapStruct - ánh xạ đối tượng
  - Lombok - giảm boilerplate code
  - Spring Data JPA
  - Spring Kafka

### Frontend
- **Framework**: React 18.3.1
- **Thư viện UI**: Material-UI (MUI)
- **Điều hướng**: React Router DOM
- **HTTP Client**: Axios
- **Công cụ Build**: npm/react-scripts

### Hạ tầng
- **Container Orchestration**: Docker Compose
- **Message Broker**: Kafka 3.7.0

## 📁 Cấu trúc Dự án

```
├── api-gateway/              # Dịch vụ API Gateway - điểm vào duy nhất cho tất cả các request
│   ├── src/main/java/        # Cấu hình Gateway và các bộ lọc xác thực
│   └── src/main/resources/   # File cấu hình ứng dụng
│
├── identity-service/         # Dịch vụ xác thực và phân quyền người dùng
│   ├── src/main/java/        # Controllers, services, entities - các lớp xử lý nghiệp vụ
│   └── src/test/java/        # Các bài test đơn vị và tích hợp
│
├── profile-service/          # Dịch vụ quản lý thông tin hồ sơ người dùng
├── post-service/             # Dịch vụ quản lý bài đăng
├── notification-service/     # Dịch vụ xử lý thông báo
├── web-app/                  # Ứng dụng frontend React
│   ├── src/                  # Các component và trang React
│   └── public/               # Các file tĩnh (hình ảnh, HTML, v.v.)
│
├── book-service/             # Dịch vụ quản lý sách (Đang phát triển)
├── file-service/             # Dịch vụ quản lý file (Đang phát triển)
├── search-service/           # Dịch vụ tìm kiếm (Đang phát triển)
│
├── docker-compose.yml        # Cấu hình hạ tầng Kafka
└── README.md                 # Tài liệu dự án
```

## 🚀 Bắt đầu

### Yêu cầu Hệ thống

- Java 21 trở lên
- Maven 3.6+
- Node.js 16+ và npm
- Docker và Docker Compose
- MySQL 8.0+
- MongoDB 4.4+

### Cài đặt

1. **Clone repository**
   ```bash
   git clone <repository-url>
   cd CI-CD-pipeline-source---IT-Got-Talent
   ```

2. **Khởi động Kafka**
   ```bash
   docker-compose up -d
   ```

3. **Thiết lập MySQL Database**
   - Tạo database: `bookteria_identity`
   - Cập nhật thông tin kết nối trong `identity-service/src/main/resources/application.yaml`

4. **Thiết lập MongoDB**
   - Đảm bảo MongoDB đang chạy trên `localhost:27017`
   - Cập nhật thông tin kết nối trong `post-service/src/main/resources/application.yaml`

5. **Build và Chạy các Dịch vụ Backend**
   ```bash
   # API Gateway
   cd api-gateway
   mvn clean install
   mvn spring-boot:run

   # Identity Service
   cd ../identity-service
   mvn clean install
   mvn spring-boot:run

   # Profile Service
   cd ../profile-service
   mvn clean install
   mvn spring-boot:run

   # Notification Service
   cd ../notification-service
   mvn clean install
   mvn spring-boot:run

   # Post Service
   cd ../post-service
   mvn clean install
   mvn spring-boot:run
   ```

6. **Chạy Ứng dụng Frontend**
   ```bash
   cd web-app
   npm install
   npm start
   ```

### Cổng Dịch vụ

- API Gateway: `8888`
- Identity Service: `8080`
- Profile Service: `8081`
- Notification Service: `8082`
- Post Service: `8083`
- Kafka: `9094`

## 🔐 Xác thực

Hệ thống sử dụng JWT (JSON Web Tokens) để xác thực. Tất cả các request đến các endpoint được bảo vệ phải bao gồm JWT token hợp lệ trong header Authorization:

```
Authorization: Bearer <token>
```

## 📡 API Endpoints

Tất cả các request API nên được thực hiện thông qua API Gateway tại `http://localhost:8888/api/v1/`

- `/api/v1/identity/**` - Các endpoint của dịch vụ Identity
- `/api/v1/profile/users/**` - Các endpoint của dịch vụ Profile
- `/api/v1/notification/**` - Các endpoint của dịch vụ Notification
- `/api/v1/post/**` - Các endpoint của dịch vụ Post

## 🧪 Kiểm thử

Chạy test cho từng dịch vụ:

```bash
cd <service-directory>
mvn test
```

## 📝 Phát triển

### Quy tắc Code
- Code Java tuân theo Palantir Java Format
- Sử dụng Spotless Maven plugin để format code
- Thụt lề bằng tab với 4 spaces

### Đóng góp
1. Tạo một nhánh tính năng
2. Thực hiện các thay đổi của bạn
3. Đảm bảo tất cả các test đều pass
4. Gửi pull request

## 📄 License

Copyright (c) 2024. All rights reserved.

This project and its source code are proprietary and confidential. Unauthorized copying, modification, distribution, or use of this software, via any medium, is strictly prohibited without the express written permission of the copyright owner.

---

**Lưu ý**: Dự án này đang trong quá trình phát triển tích cực. Một số dịch vụ có thể chưa hoàn thiện hoặc có thể thay đổi.
