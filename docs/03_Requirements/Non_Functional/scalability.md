# Yêu Cầu Khả Năng Mở Rộng - Scalability Requirements

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Danh mục**: Non-Functional Requirements

---

## 1. Data Scalability

### NFR-SCA-001: Publication Volume
**Capacity**:
- MVP: 10,000 publications
- 3 years: 20,000 publications
- 5 years: 50,000 publications

**Growth rate**: ~2,000-3,000/year

---

### NFR-SCA-002: User Base
**Capacity**:
- MVP: 500 users
- 3 years: 1,000 users
- 5 years: 2,000 users

---

### NFR-SCA-003: File Storage
**Capacity**:
- MVP: 50GB PDF files
- 3 years: 150GB
- 5 years: 300GB

**Strategy**: Start local FS, migrate to object storage (S3) nếu cần

---

## 2. Vertical Scalability

### NFR-SCA-010: Server Specs Scaling
**Minimum** (MVP):
- CPU: 4 cores
- RAM: 8GB
- Disk: 100GB

**Recommended** (Production):
- CPU: 8 cores
- RAM: 16GB
- Disk: 500GB SSD

**Max vertical scale**:
- CPU: 16 cores
- RAM: 32GB

---

## 3. Horizontal Scalability

### NFR-SCA-020: Stateless Application
**Requirement**: Backend PHẢI stateless

**Implementation**:
- Session trong Redis (không trong memory)
- JWT tokens (không session affinity)
- Load balancer ready

---

### NFR-SCA-021: Database Replication
**Strategy** (Phase 2):
- Master-Slave replication
- Read từ slaves
- Write vào master

**Max scale**: 1 master + 2-3 read replicas

---

### NFR-SCA-022: Load Balancing
**Support** (Phase 2):
- Nginx hoặc HAProxy
- Round-robin hoặc least-connections
- Health checks

---

## 4. Modular Architecture

### NFR-SCA-030: Microservices Ready
**Design**: Monolith hiện tại, nhưng sẵn sàng tách ra

**Potential modules**:
- Publication Service
- Approval Workflow Service
- Search Service
- Reporting Service
- User Management Service

---

## 5. Database Scalability

### NFR-SCA-040: Indexing Strategy
**Indexes**:
- Primary keys (id)
- Foreign keys
- DOI, ISSN (unique)
- publicationYear, status
- Full-text index (title, abstract)

---

### NFR-SCA-041: Partitioning (Future)
**Strategy nếu > 100,000 publications**:
- Partition by year
- Archive old data (> 10 years)

---

## 6. Caching Strategy

### NFR-SCA-050: Multi-Level Caching
**Layers**:
1. Browser cache (static assets)
2. CDN/Reverse proxy (public pages)
3. Application cache (Redis)
4. Database query cache

**Hit ratio target**: > 70%

---

## 7. Migration Path

### NFR-SCA-060: Cloud Migration Ready
**From**: On-premise servers  
**To**: Cloud (AWS, Azure, GCP)

**Components to migrate**:
- Database: MySQL → RDS/Cloud SQL
- Files: Local FS → S3/Blob Storage
- App: VMs → Containers (Docker)

---

## 8. API Scalability

### NFR-SCA-070: API Versioning
**Support**: API v1, v2... (backward compatible)

**URL**: `/api/v1/publications`

---

### NFR-SCA-071: Rate Limiting
**Prevents abuse**:
- Public API: 100 req/hour
- Authenticated: 1000 req/hour

---

## 9. Monitoring & Auto-scaling

### NFR-SCA-080: Metrics Collection
**Track**:
- Request count
- Response time
- Error rate
- Resource utilization

**Tools**: Prometheus + Grafana

---

### NFR-SCA-081: Auto-scaling (Phase 3)
**Triggers**:
- CPU > 80% for 5 min: Scale up
- CPU < 30% for 10 min: Scale down

**Platform**: Kubernetes, Docker Swarm

---

**Tài liệu liên quan**:
- [Performance Requirements](./performance.md)
- [Technology Stack](../../01_System_Specification/technology_stack.md)
