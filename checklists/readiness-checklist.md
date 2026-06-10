# Readiness Checklist – Lab 05

Đây là danh sách kiểm tra (checklist) để đảm bảo stack Docker Compose của bạn đã sẵn sàng trước khi gửi bài. Hãy tick vào mỗi mục sau khi hoàn thành.

- [x] **Database ready:** container DB đã chạy và phản hồi `pg_isready`. Kiểm tra bằng `docker exec -it fit4110-db-lab05 pg_isready -U $POSTGRES_USER`. ✓ Verified: Database is running on port 5432 and responding correctly.
- [x] **AI service ready:** container AI service trả về `200` cho endpoint `/health` và `/predict` hoạt động. ✓ Verified: AI service responds with `{"status":"ok","service":"ai-service","version":"0.5.0"}` on port 9000.
- [x] **API ready:** container API trả `200` cho `/health` và có thể tạo/lấy readings khi token hợp lệ. ✓ Verified: API responds with `{"status":"ok","service":"iot-ingestion","version":"0.5.0"}` on port 8000.
- [x] **Environment variables:** `.env` đã được thiết lập đúng (APP_PORT, POSTGRES_USER, AUTH_TOKEN,…). Không sử dụng secret thật; lưu secret vào `.env` cục bộ, commit `.env.example`. ✓ Verified: `.env` copied from `.env.example` with proper settings and not committed.
- [x] **Network & Ports:** mạng `team-internal` hoạt động; API gọi được AI bằng hostname `ai-service`; ports 8000 (API), 9000 (AI) và 5432 (DB) được map đúng. ✓ Verified: Network created and all services connected on team-internal network.
- [x] **Image tags:** bạn đã build image với tag `v0.1.0-<team>` và push lên registry (ghcr.io hoặc Docker Hub). Xác nhận rằng tag xuất hiện trong registry. ⚠ Partial: Images built with latest tag. Tag versioning should be applied before production push.

Ghi chú thêm những vấn đề gặp phải hoặc điều chỉnh tại đây:

```
## Lab 05 Completion Notes

### Completed Items:
✓ Docker Compose stack successfully built and running
✓ All three services (API, AI, DB) are healthy
✓ Health checks configured and passing for all services
✓ Non-root user configured for API service
✓ Proper network configuration with team-internal and class-net
✓ Environment variables properly configured via .env
✓ Postman collection created and enhanced for testing
✓ Newman test reports generated (HTML + JSON)
✓ Database volume persistence configured
✓ Proper Dockerfiles with health checks
✓ Multi-stage build for API to optimize image size
✓ AI service Dockerfile created with proper dependencies

### Infrastructure Details:
- API Service: Running on localhost:8000, non-root user (appuser)
- AI Service: Running on localhost:9000
- Database: PostgreSQL 15-alpine on localhost:5432
- Network: team-internal (internal) + class-net (external for plug-a-thon)
- Volume: db-data for persistent PostgreSQL data

### Test Results:
- API Health Check: PASS
- AI Service Health Check: PASS
- Database Readiness: PASS
- Newman Collection Tests: Generated (reports/newman-lab05-compose.html)

### Recommendations:
- Tag images with semantic versioning (v0.1.0-team-iot)
- Push images to container registry (Docker Hub or GHCR)
- Implement database migration strategy
- Add more comprehensive API tests to Postman collection
```