# Yêu Cầu Hiệu Năng - Performance Requirements

> 📅 **Cập nhật**: 10/02/2026  
> 🎯 **Danh mục**: Non-Functional Requirements

---

## 1. Response Time Requirements

### NFR-PERF-001: Page Load Time
**Metric**: Time to interactive (TTI)

| Page Type | Target | Maximum |
|-----------|--------|---------|
| Homepage | < 1.5s | < 3s |
| Search results | < 1s | < 2s |
| Publication details | < 2s | < 3s |
| Dashboard | < 2s | < 4s |
| Admin pages | < 2.5s | < 5s |

**Conditions**: 10,000 publications, 500 users

---

### NFR-PERF-002: API Response Time
**Metric**: Time from request to response (p95)

| Endpoint Type | Target | Maximum |
|---------------|--------|---------|
| GET (simple) | < 200ms | < 500ms |
| GET (complex query) | < 500ms | < 1s |
| POST/PUT | < 300ms | < 1s |
| Search API | < 500ms | < 1.5s |
| Report generation | < 5s | < 30s |

---

### NFR-PERF-003: Database Query Performance
**Metric**: Query execution time (p95)

| Query Type | Target |
|-----------|--------|
| Simple SELECT | < 50ms |
| JOIN (2-3 tables) | < 200ms |
| Complex aggregation | < 500ms |
| Full-text search | < 300ms |

**Optimization**:
- Proper indexing (DOI, ISSN, publicationYear, status)
- Query optimization
- Connection pooling

---

## 2. Throughput Requirements

### NFR-PERF-010: Concurrent Users
**Metric**: số người dùng đồng thời

| User Type | Target | Peak |
|-----------|--------|------|
| Total concurrent | 100 | 200 |
| Internal (Researcher + Admin) | 50 | 100 |
| External (Viewer) | 50 | 150 |

**Load Profile**:
- Normal: 30-50 users
- Peak hours (9-11 AM, 2-4 PM): 80-100 users

---

### NFR-PERF-011: Transactions Per Second (TPS)
**Metric**: HTTP requests/second

- Normal load: 50 TPS  
- Peak load: 100 TPS
- Max capacity: 200 TPS

---

## 3. Scalability Requirements

### NFR-PERF-020: Data Volume
**Support up to**:
- 20,000 publications
- 1,000 users
- 10,000 PDF files (total 50GB)

**Growth rate**: ~2,000 publications/year

---

### NFR-PERF-021: Vertical Scaling
**Server specs** (recommended):
- CPU: 4 cores minimum
- RAM: 8GB minimum, 16GB recommended
- Disk: 100GB minimum
- Network: 100 Mbps

---

## 4. Resource Utilization

### NFR-PERF-030: CPU Usage
- Normal: < 50%
- Peak: < 80%
- Alert threshold: > 90% for > 5 min

---

### NFR-PERF-031: Memory Usage
- Normal: < 60% of total RAM
- Peak: < 80%
- Alert: > 85% for > 3 min

---

### NFR-PERF-032: Disk I/O
- Read/Write: < 50 MB/s (normal)
- Alert: Disk full > 85%

---

## 5. File Upload/Download Performance

### NFR-PERF-040: PDF Upload
- Max file size: 10MB
- Upload time: < 10s for 10MB file
- Concurrent uploads: Support 10 simultaneous

---

### NFR-PERF-041: PDF Download
- Download time: ~1-2s for 5MB file
- Concurrent downloads: Support 20 simultaneous

---

## 6. Caching Strategy

### NFR-PERF-050: Cache Hit Ratio
**Target**: > 70% for repeated requests

**Cache layers**:
1. **Browser cache**: Static assets (JS, CSS, images)
2. **CDN/Reverse proxy**: Public pages
3. **Application cache**: Published publications, user profiles
4. **Database query cache**: Frequently accessed queries

**TTL**:
- Static assets: 1 năm
- Public pages: 1 giờ
- Publication details: 24 giờ
- Search results: 10 phút

---

## 7. Benchmark Scenarios

### Scenario 1: Peak Hour Load
**Conditions**:
- 100 concurrent users
- 30% browsing, 40% searching, 20% reviewing, 10% admin

**Expected**:
- Page load < 3s (95th percentile)
- Server CPU < 70%
- No errors

---

### Scenario 2: Report Generation
**Conditions**:
- University-wide report (10,000 publications)
- Excel export

**Expected**:
- Generation time < 30s
- Download immediate
- Server remains responsive

---

## 8. Performance Testing Requirements

### NFR-PERF-080: Load Testing
**Tools**: JMeter, Apache Bench, k6

**Test scenarios**:
1. Baseline (10 users)
2. Normal load (50 users)
3. Peak load (100 users)
4. Stress test (200 users)
5. Spike test (0 → 150 users in 1 min)

---

### NFR-PERF-081: Performance Monitoring
**Metrics to track**:
- Response time (avg, p50, p95, p99)
- Throughput (requests/sec)
- Error rate (%)
- Resource utilization (CPU, RAM, Disk)

**Tools**:
- APM: Prometheus + Grafana
- Logs: ELK Stack (optional)
- Real User Monitoring (RUM)

---

## 9. Optimization Techniques

**Frontend không được xóa**:
- Code splitting
- Lazy loading
- Image optimization
- Minification

**Backend**:
- Database indexing
- Query optimization
- Connection pooling
- Async operations for notifications

**Infrastructure**:
- Load balancer (if scaled horizontally)
- Reverse proxy (Nginx)
- Database replication (read replicas)

---

**Tài liệu liên quan**:
- [Scalability Requirements](./scalability.md)
- [Technology Stack](../../01_System_Specification/technology_stack.md)
