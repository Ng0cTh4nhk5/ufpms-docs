# SOP - Product Manager (PM)
## Version 1.0: Core Publication Management

> 👤 **Vai trò**: Product Manager  
> 🎯 **Phạm vi**: V1.0 - Quản lý 9 User Stories  
> 📅 **Áp dụng cho**: Planning, Coordination, Quality Assurance

---

## 🎯 Mục Tiêu Tổng Quan

Lãnh đạo và điều phối toàn bộ phát triển V1.0, đảm bảo project on-time, within scope, và đáp ứng quality standards. PM chịu trách nhiệm về success tổng thể của V1.0.

---

## 📋 Trách Nhiệm Chính

### 1. Planning & Scope Management
- Xác định scope V1.0 (9 user stories)
- Lập timeline và milestones
- Quản lý changes và scope creep

### 2. Team Coordination
- Điều phối giữa các roles (BA, Dev, QA, Design)
- Resolve conflicts và blockers
- Facilitate meetings (standups, reviews, retrospectives)

### 3. Quality Assurance
- Review deliverables ở mỗi phase
- Ensure Definition of Done được follow
- Final sign-off trước release

### 4. Stakeholder Communication
- Report progress cho stakeholders
- Manage expectations
- Demo V1.0 sau khi hoàn thành

---

## 📐 PHASE 1: DESIGN

### 1. Kickoff Project

- [ ] **Tổ Chức Kickoff Meeting**

  ```
  Mục đích: Align toàn team về V1.0 scope và goals
  
  Thành viên: BA, UI/UX, Backend Dev, Frontend Dev, QA, Tech Lead
  
  Agenda:
  1. Giới thiệu V1.0 scope (15 phút)
     - 9 user stories overview
     - Business goals
     - Success criteria
  
  2. Review timeline (10 phút)
     - Phase 1: Design
     - Phase 2: Development
     - Phase 3: Verification
     - Target launch date
  
  3. Roles & Responsibilities (10 phút)
     - BA: Requirements clarification
     - UI/UX: Design 6 screens
     - Backend: APIs + Database
     - Frontend: UI implementation
     - QA: Testing
     - Tech Lead: Architecture + Code review
  
  4. Communication Plan (10 phút)
     - Daily standups: 9:00 AM, 15 minutes
     - Design review: End of Design phase
     - Code review: Ongoing
     - Demo: End of Verification phase
  
  5. Q&A (15 phút)
  
  Output: Meeting notes, recorded decisions
  ```

- [ ] **Tạo Project Charter** (Ngắn gọn cho V1.0)

  ```
  Document sections:
  
  1. Project Overview
     - Tên: V1.0 Core Publication Management
     - Mục tiêu: Researchers có thể quản lý publications (CRUD)
  
  2. Scope
     - In-scope: 9 user stories (list chi tiết)
     - Out-of-scope: Review workflow, Public access, Reporting
  
  3. Timeline
     - Start: [Date]
     - Target completion: [Date sau 6 tuần]
  
  4. Team
     - [List roles và tên thành viên]
  
  5. Success Criteria
     - 9/9 user stories hoàn thành
     - UAT passed
     - 0 critical bugs
  
  6. Risks
     - Risk 1: Thiếu resources → Mitigation: Prioritize P0 features
     - Risk 2: Timeline tight → Mitigation: Daily tracking
  ```

---

### 2. Monitor Design Phase

- [ ] **Weekly Check-ins với Từng Role**

  **Check-in với BA:**
  ```
  Câu hỏi:
  - Acceptance criteria cho 9 user stories đã rõ ràng chưa?
  - Có edge cases nào cần clarify?
  - Test scenarios đã đầy đủ chưa?
  
  Output: BA sign-off on requirements
  ```

  **Check-in với UI/UX:**
  ```
  Câu hỏi:
  - Design system đã define chưa?
  - 6 screens đã design xong chưa?
  - Prototype sẵn sàng cho review chưa?
  
  Output: Figma link, ready cho design review
  ```

  **Check-in với Tech Lead:**
  ```
  Câu hỏi:
  - Architecture đã finalize chưa?
  - Tech stack confirmed chưa?
  - Database schema OK?
  
  Output: Architecture doc, tech decisions documented
  ```

- [ ] **Design Review Meeting (End of Design Phase)**

  ```
  Thành viên: Toàn team + Stakeholders (optional)
  
  Agenda:
  1. BA presents: Requirements recap (10 phút)
  2. UI/UX presents: Figma designs walkthrough (20 phút)
  3. Tech Lead presents: Architecture overview (15 phút)
  4. QA presents: Test plan overview (10 phút)
  5. Feedback & Questions (15 phút)
  6. PM decision: Approve để chuyển sang Development? (5 phút)
  
  Approval criteria:
  - Designs match user stories ✅
  - Architecture feasible ✅
  - Team confident để implement ✅
  
  Output: Design sign-off, go ahead cho Development
  ```

---

## 💻 PHASE 2: DEVELOPMENT

### 3. Sprint Management

- [ ] **Setup Sprint (Nếu dùng Agile)**

  ```
  Sprint duration: 1-2 tuần
  
  Sprint Planning:
  - Select user stories cho sprint (từ backlog)
  - Break down thành tasks
  - Estimate effort (hours/story points)
  - Assign tasks
  
  Sprint Goal Example:
  "Complete US-RES-001, US-RES-002, US-RES-003 with full testing"
  ```

- [ ] **Daily Standups** (Hàng ngày, 15 phút)

  ```
  Format: Mỗi thành viên trả lời 3 câu hỏi:
  
  1. Yesterday: Bạn làm được gì?
     - Example: "Hoàn thành Create Publication API"
  
  2. Today: Hôm nay sẽ làm gì?
     - Example: "Implement Edit Publication API"
  
  3. Blockers: Có vấn đề gì cần giúp?
     - Example: "Cần clarify validation rules cho field X"
  
  PM's role:
  - Listen actively
  - Note blockers
  - Follow up sau standup để resolve
  - Track progress towards sprint goal
  ```

---

### 4. Progress Monitoring

- [ ] **Track Completion Status**

  ```
  Tracking matrix (cập nhật hàng ngày):
  
  User Story | Backend API | Frontend UI | Testing | Status
  US-RES-001 | ✅ Done     | ✅ Done    | 🔄 In Progress | 80%
  US-RES-002 | ✅ Done     | ⏳ Not Started | ⏳ Blocked | 30%
  US-RES-003 | 🔄 In Progress | ⏳ Waiting | ⏳ Waiting | 20%
  ...
  
  Legend:
  ✅ Done | 🔄 In Progress | ⏳ Waiting/Not Started | ❌ Blocked
  ```

- [ ] **Identify Red Flags Sớm**

  ```
  Warning signs:
  - Tasks stuck "In Progress" > 2 ngày → Investigate
  - Multiple blockers chưa resolved → Escalate
  - Team members im lặng trong standup → 1-on-1 check-in
  - Test failures tăng → Review code quality
  
  Actions:
  - Address blockers ngay trong ngày
  - Re-prioritize nếu cần
  - Add resources nếu có thể
  ```

---

### 5. Code Review Coordination

- [ ] **Ensure Code Quality Process**

  ```
  PM không review code chi tiết (đó là việc của Tech Lead)
  Nhưng PM monitor:
  
  - PRs được review promptly? (< 4 hours)
  - CI/CD pipelines pass?
  - Code coverage đạt target? (> 80%)
  - Tech debt được document?
  
  Weekly check-in với Tech Lead:
  "Code quality có concerns gì không?"
  ```

---

### 6. Manage Scope Changes

- [ ] **Change Request Process**

  ```
  Khi có yêu cầu thay đổi scope:
  
  1. Document request:
     - Ai request?
     - Thay đổi gì?
     - Tại sao cần?
  
  2. Impact analysis:
     - Effort thêm bao nhiêu?
     - Ảnh hưởng timeline như thế nào?
     - Risk gì?
  
  3. Decision matrix:
     - P0 (Must have cho V1.0): Approve, adjust timeline
     - P1 (Nice to have): Defer to V2.0
     - P2 (Can wait): Backlog
  
  4. Communicate decision:
     - Inform requester
     - Update team
     - Document in project notes
  ```

---

## ✅ PHASE 3: VERIFICATION

### 7. Test Planning

- [ ] **Collaborate với QA**

  ```
  Review QA's test plan:
  - 55 test cases cover tất cả 9 user stories? ✅
  - Test cases bao gồm happy paths + edge cases? ✅
  - Test data ready? ✅
  - Test environment setup? ✅
  
  PM role:
  - Ensure test coverage đầy đủ
  - Prioritize test cases nếu time limited
  - Allocate time cho bug fixes
  ```

---

### 8. User Acceptance Testing (UAT)

- [ ] **Plan UAT Sessions**

  ```
  UAT với end users hoặc stakeholders:
  
  Preparation:
  - Environment: Staging server
  - Test accounts: researcher1, researcher2
  - Test scenarios: 9 user stories
  
  UAT Session (2-3 giờ):
  1. Giới thiệu V1.0 (10 phút)
  2. Demo 6 screens (20 phút)
  3. Hands-on testing (90 phút)
     - Testers thử tất cả user stories
     - PM observe và ghi chú feedback
  4. Feedback collection (30 phút)
  
  Acceptance criteria:
  - Tất cả 9 user stories work as expected
  - No critical bugs
  - Stakeholders satisfied
  
  Output: UAT sign-off hoặc list of issues to fix
  ```

- [ ] **Bug Triage**

  ```
  Khi QA/UAT tìm thấy bugs, PM prioritize:
  
  P0 (Critical - Must fix trước release):
  - System crashes
  - Data loss
  - Security vulnerabilities
  - Login không hoạt động
  
  P1 (High - Should fix trước release):
  - Major features không hoạt động
  - Validation errors sai
  
  P2 (Medium - Can defer to V1.1):
  - UI minor issues
  - Performance chưa tối ưu
  
  P3 (Low - Backlog):
  - Nice-to-have improvements
  - Cosmetic issues
  
  PM decision: V1.0 chỉ release khi P0/P1 bugs = 0
  ```

---

### 9. Definition of Done Review

- [ ] **Verify DoD Checklist**

  ```
  V1.0 đạt DoD khi:
  
  Functionality:
  - ✅ 9/9 user stories implemented
  - ✅ All acceptance criteria đạt 100%
  - ✅ Manual testing passed
  
  Quality:
  - ✅ Unit test coverage > 80% (Backend), > 70% (Frontend)
  - ✅ Integration tests passed
  - ✅ 0 critical/high bugs
  - ✅ QA sign-off
  
  Design:
  - ✅ UI match Figma designs
  - ✅ Responsive trên desktop + tablet
  - ✅ UI/UX designer approval
  
  Documentation:
  - ✅ API docs updated (Swagger)
  - ✅ Code comments đầy đủ
  - ✅ README updated
  
  Deployment:
  - ✅ Merged to main branch
  - ✅ Deployed to staging successfully
  - ✅ Có thể demo cho stakeholders
  - ✅ PM final sign-off
  
  PM reviews từng mục và confirm ✅ trước khi approve release
  ```

---

### 10. Demo Preparation

- [ ] **Plan Demo cho Stakeholders**

  ``` 
  Demo meeting (60 phút):
  
  Attendees:
  - Stakeholders (faculty leadership, etc.)
  - Development team
  - PM (host/moderator)
  
  Agenda:
  1. Project recap (5 phút)
     - Scope V1.0
     - Timeline achieved
  
  2. Live demo (30 phút)
     Demo 6 screens theo user journey:
     a. Login
     b. Dashboard overview
     c. Create new publication
     d. Upload PDF
     e. Add co-authors
     f. View publication list & detail
  
  3. Metrics & Achievements (10 phút)
     - User stories completed: 9/9
     - Test coverage: 82%
     - Bugs fixed: 20
     - Performance: < 500ms API response
  
  4. Next steps (V2.0 preview) (5 phút)
  5. Q&A (10 phút)
  
  Output: Stakeholder approval, feedback for V2.0
  ```

---

### 11. Release Sign-Off

- [ ] **Final Checklist Before Production Release**

  ```
  PM signs off khi:
  - ✅ DoD 100% achieved
  - ✅ UAT passed
  - ✅ Stakeholder demo successful
  - ✅ 0 P0/P1 bugs outstanding
  - ✅ Deployment plan reviewed với Tech Lead
  - ✅ Rollback plan documented
  - ✅ Team ready for production support
  
  Go / No-Go Decision:
  - GO: Release to production
  - NO-GO: Fix remaining issues, re-test
  ```

---

## 📊 PM Key Metrics

### Metrics to Track:

**Progress Metrics:**
- User Stories completed: X / 9
- Sprint velocity (nếu dùng Agile)
- Burndown chart

**Quality Metrics:**
- Bugs found: Total, by priority
- Bugs fixed: Total, % fixed
- Test coverage: Backend %, Frontend %

**Schedule Metrics:**
- On-time delivery: Yes/No
- Milestone dates: Planned vs. Actual

**Team Metrics:**
- Team morale (from retros): High/Medium/Low
- Blockers resolution time: Avg hours

---

## ✅ PM Success Criteria

PM làm tốt khi:

✅ V1.0 delivered on-time (hoặc explain clearly nếu delay)  
✅ All 9 user stories completed with quality  
✅ Team morale good (no burnout)  
✅ Stakeholders satisfied với demo  
✅ Clear plan cho V2.0 based on lessons learned  
✅ Documentation đầy đủ để handover

---

## 📋 Deliverables (Sản Phẩm PM Bàn Giao)

1. **Project Charter** - Scope, timeline, team
2. **Sprint Plan** (nếu dùng Agile) - Sprint goals, backlogs
3. **Progress Reports** - Weekly status updates
4. **Risk Register** - Risks identified, mitigations
5. **Meeting Notes** - Kickoff, design review, standups, retros
6. **UAT Sign-off** - Stakeholder approval
7. **Release Notes** - What's new in V1.0, known issues
8. **Lessons Learned** - What went well, what to improve cho V2.0

---

**Prepared by**: Product Management  
**Version**: 1.0  
**Last Updated**: 16/02/2026
