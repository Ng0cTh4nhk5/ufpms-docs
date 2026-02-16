# Standard Operating Procedures (SOPs) - Version 1.0

> 📁 **Thư mục**: SOPs cho phát triển V1.0 - Core Publication Management  
> 🎯 **Mục đích**: Hướng dẫn chi tiết cho từng vai trò trong team  
> 📅 **Cập nhật**: 16/02/2026

---

## 📚 Danh Sách SOPs

Bộ SOPs này cung cấp hướng dẫn đầy đủ cho 7 vai trò chính trong dự án UFPMS V1.0:

| # | Vai trò | File SOP | Trọng tâm chính |
|---|---------|----------|-----------------|
| 1 | **Product Manager (PM)** | [SOP_PM_V1.0.md](./SOP_PM_V1.0.md) | Quản lý scope, điều phối team, đảm bảo chất lượng |
| 2 | **Business Analyst (BA)** | [SOP_BA_V1.0.md](./SOP_BA_V1.0.md) | Phân tích requirements, viết acceptance criteria, support QA |
| 3 | **UI/UX Designer** | [SOP_UIUX_V1.0.md](./SOP_UIUX_V1.0.md) | Thiết kế giao diện 6 screens, tạo design system |
| 4 | **Backend Developer** | [SOP_Backend_V1.0.md](./SOP_Backend_V1.0.md) | Phát triển REST APIs, database, authentication |
| 5 | **Frontend Developer** | [SOP_Frontend_V1.0.md](./SOP_Frontend_V1.0.md) | Phát triển React UI, tích hợp APIs |
| 6 | **QA/Tester** | [SOP_QA_V1.0.md](./SOP_QA_V1.0.md) | Test planning, test execution, bug tracking |
| 7 | **Tech Lead** | [SOP_TechLead_V1.0.md](./SOP_TechLead_V1.0.md) | Kiến trúc hệ thống, code review, technical leadership |

---

## 🗺️ Cấu Trúc Chung

Mỗi SOP được tổ chức theo 3 phases tương ứng với quy trình phát triển:

### 📐 Phase 1: DESIGN (Tuần 0-1)
- **PM**: Tổ chức kickoff, review designs, sign-off
- **BA**: Phân tích user stories, viết test scenarios
- **UI/UX**: Tạo design system, thiết kế 6 screens, prototype
- **Backend**: Review schema, review API specs, setup environment
- **Frontend**: Setup project, review Figma designs
- **QA**: Create test plan, viết test cases (~55 cases)
- **Tech Lead**: Design architecture, finalize tech stack, setup CI/CD

### 💻 Phase 2: DEVELOPMENT (Tuần 2-4)
- **PM**: Daily standups, monitor progress, review implementations
- **BA**: Answer dev questions, clarify requirements
- **UI/UX**: Support frontend với design handoff, design QA
- **Backend**: Implement APIs, database, file upload, tests
- **Frontend**: Implement 6 screens, integrate APIs, tests
- **QA**: API testing (Postman), continuous UI testing, log bugs
- **Tech Lead**: Code reviews, technical guidance, performance optimization

### ✅ Phase 3: VERIFICATION (Tuần 5-6)
- **PM**: UAT testing, demo preparation, stakeholder demo, release sign-off
- **BA**: Support UAT, sign-off acceptance criteria
- **UI/UX**: Final design QA, polish, documentation
- **Backend**: Integration tests, bug fixes, deployment prep
- **Frontend**: UI polish, bug fixes, responsive testing
- **QA**: Regression testing, bug verification, test summary report
- **Tech Lead**: Pre-release checklist, deployment, post-release monitoring

---

## 🎯 V1.0 Scope Reminder

**9 User Stories:**
- US-RES-001: Tạo bài báo mới
- US-RES-002: Upload file PDF
- US-RES-003: Sửa bài báo nháp
- US-RES-004: Xóa bài báo nháp
- US-RES-005: Xem danh sách bài báo
- US-RES-006: Thêm đồng tác giả
- US-RES-008: Xem chi tiết bài báo
- US-RES-009: Download file PDF
- US-RES-024: Xem dashboard giờ làm

**6 Screens:**
1. Login page
2. Researcher Dashboard
3. Publication List
4. Create Publication form
5. Edit Publication form
6. Publication Detail view

---

## 📊 Definition of DONE

V1.0 được coi là hoàn thành khi:

### ✅ Functionality
- [ ] 9/9 user stories implemented
- [ ] All acceptance criteria đạt 100%
- [ ] Manual testing pass

### ✅ Quality
- [ ] Unit test coverage > 80% (Backend), > 70% (Frontend)
- [ ] Integration tests pass
- [ ] No critical/high bugs
- [ ] QA sign-off

### ✅ Design
- [ ] UI match Figma designs
- [ ] Responsive trên desktop + tablet
- [ ] UI/UX Designer approval

### ✅ Documentation
- [ ] API docs updated (Swagger)
- [ ] Code comments đầy đủ
- [ ] README updated

### ✅ Deployment
- [ ] Merged to main branch
- [ ] Deployed to staging
- [ ] Có thể demo cho stakeholders
- [ ] PM final sign-off

---

## 🚀 Làm Thế Nào Để Sử Dụng SOPs Này?

### Cho Team Members:
1. **Đọc SOP của vai trò mình** trước khi bắt đầu làm việc
2. **Follow checklist** trong mỗi phase
3. **Tham khảo SOPs khác** để hiểu dependencies (ví dụ: Frontend dev nên đọc UI/UX SOP để hiểu designs)
4. **Update progress** trong các meetings (standups, reviews)

### Cho PM:
1. Sử dụng SOPs như **baseline plan**
2. Customize nếu cần (nhưng giữ core structure)
3. Track progress theo checklists trong mỗi SOP

### Cho Tech Lead:
1. Ensure team **follows technical standards** trong SOP
2. Review code theo **code review checklist**
3. Make architecture decisions theo **architecture guidelines**

---

## 💡 Tips để Thành Công

### 1. Giao Tiếp Là Chìa Khóa
- Đọc SOPs của vai trò khác để hiểu big picture
- Attend meetings đầy đủ (kickoff, design review, standups, etc.)
- Ask questions sớm, đừng wait đến khi stuck

### 2. Chất Lượng Hơn Tốc Độ
- Follow Definition of DONE nghiêm túc
- Don't skip testing phase
- Code review kỹ càng

### 3. Incremental Approach
- Focus vào V1.0 scope only
- Don't add features outside 9 user stories
- Defer nice-to-have features to V2.0

### 4. Document Mọi Thứ
- Update documents khi có changes
- Write clear commit messages
- Document decisions (especially architecture)

### 5. Học Từ V1.0
- Conduct retrospective meeting sau V1.0
- Document lessons learned
- Improve process cho V2.0

---

## 📞 Support & Questions

**Khi có questions:**
- **Requirements/Business logic**: Ask BA
- **Design/UI/UX**: Ask UI/UX Designer
- **Technical architecture**: Ask Tech Lead
- **Backend APIs**: Ask Backend team
- **Frontend implementation**: Ask Frontend team
- **Testing/Quality**: Ask QA
- **Scope/Timeline/Priorities**: Ask PM

**Khi bị blocked:**
- Raise trong daily standup
- Escalate to PM hoặc Tech Lead
- Document blockers trong Jira/Trello

---

## 📈 Success Metrics

Measure success of V1.0 by:
- **On-time delivery**: V1.0 completed within planned timeline
- **Quality**: No critical bugs, test coverage targets met
- **Stakeholder satisfaction**: Positive feedback from demo
- **Team morale**: Positive retrospective feedback
- **Clear path to V2.0**: Lessons learned documented

---

## 🔄 Version History

| Version | Ngày | Thay đổi |
|---------|------|---------|
| 1.0 | 16/02/2026 | Initial SOPs created cho tất cả 7 roles |

---

**Maintained by**: PM & Tech Lead  
**Questions/Feedback**: [Contact PM]
