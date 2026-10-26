# BRIEF TỔNG QUAN - HỆ THỐNG HRM VIETELITE

> **Hệ thống quản lý nhân sự tích hợp cho VietElite - Hệ thống Giáo dục**
> Đơn vị triển khai: Công ty Cổ phần Đầu tư và Phát triển Việt Tinh Hoa
> Phiên bản: 2.0 | Ngày: 25/10/2026

---

## 1. TỔNG QUAN DỰ ÁN

### 1.1 Tên dự án
**VietElite HRM System** - Hệ thống quản lý nhân sự tích hợp cho VietElite

### 1.2 Bối cảnh tổ chức

VietElite vận hành theo **mô hình Hội sở - Chi nhánh**:

**Hội sở (TP.HCM)** gồm 6 bộ phận chức năng:

| # | Bộ phận | Vai trò đối với HRM |
|---|---------|---------------------|
| 1 | **Hành chính Nhân sự (HCNS)** | Bộ phận chủ quản hệ thống HRM; người dùng chính của hệ thống |
| 2 | Kế toán Tài chính | Cấu hình công thức lương, thuế TNCN; phê duyệt & đối soát lương |
| 3 | Truyền thông Marketing | Nhân sự marketing, hỗ trợ báo cáo doanh thu theo chi nhánh |
| 4 | Đào tạo & Khảo thí | Cung cấp dữ liệu ca dạy qua hệ thống CAMS; quản lý giáo viên |
| 5 | Tư vấn Tuyển sinh | Nhân sự tư vấn, quản lý chỉ tiêu doanh số (đầu vào thưởng) |
| 6 | Kỹ thuật Công nghệ | Hỗ trợ vận hành hệ thống, quản lý thiết bị nhân viên |

**Chi nhánh (4 cơ sở):**

| # | Chi nhánh | Ghi chú |
|---|-----------|---------|
| 1 | VietElite Đỗ Quang | Lõi, đông nhất nhân sự |
| 2 | Phạm Tuấn Tài | |
| 3 | Hà Đông | |
| 4 | SmartCity | |

> **Hệ quả cho thiết kế hệ thống:**
> - Mọi dữ liệu nhân sự, chấm công, hợp đồng, lương đều gắn với **chi nhánh** (đơn vị hành chính cơ sở)
> - Quyền xem dữ liệu được phân tách theo Hội sở / Chi nhánh
> - Có **4 luồng dữ liệu song song** (4 chi nhánh) cần hợp nhất về 1 database
> - Giáo viên có thể dạy **nhiều cơ sở**, nhiều lớp, nhiều ca → cần đối soát chéo dữ liệu CAMS

### 1.3 Vision
Xây dựng hệ thống HRM toàn diện, tự động hóa quy trình quản lý nhân sự từ chấm công GPS, quản lý hợp đồng giảng dạy, đến tính lương và báo cáo phân tích - giúp VietElite tối ưu chi phí nhân sự và nâng cao hiệu quả vận hành đa cơ sở.

### 1.4 Mục tiêu kinh doanh
- **Tự động hóa 90%** quy trình chấm công và tính lương
- **Giảm 60%** thời gian xử lý đơn từ và duyệt công
- **Tăng tính minh bạch** trong quản lý hợp đồng và phụ cấp giáo viên
- **Cung cấp insights** về chi phí nhân sự theo từng cơ sở để tối ưu hiệu quả kinh doanh

### 1.5 Nguyên tắc thiết kế
1. **Hội sở là trung tâm** - mọi cấu hình chính sách (công thức lương, thuế, phụ cấp, kỷ luật) do HCNS Hội sở thiết lập và áp dụng đồng nhất cho 4 chi nhánh
2. **Phân quyền theo cơ sở** - Quản lý cơ sở tự quản lý trong phạm vi được giao
3. **Công thức do Kế toán kiểm chứng** - mọi công thức lương phải được đối chiếu với báo cáo thuế TNCN
4. **Traceability 100%** - mọi thay đổi dữ liệu lương/hợp đồng đều có audit trail

---

## 2. PHẠM VI DỰ ÁN

### 2.1 Tổng quan 8 modules

| Module | Tên | Phase | Trạng thái |
|--------|-----|-------|------------|
| **M1** | Hồ sơ nhân sự, Hợp đồng & Chính sách | P1 | Core |
| **M2** | Chấm công GPS, Ca làm việc & Đối soát giảng dạy | P1 | Core |
| **M3** | Quản lý đơn từ | P1 | Core |
| **M4** | Động cơ tính lương tự động | P2 | Core |
| **M5** | Báo cáo Nhân sự & Quản trị | P3 | Core |
| **M6** | Tuyển dụng cơ bản (Lightweight ATS) | P4 | Mở rộng |
| **M7** | Đánh giá KPI đơn giản | P4 | Mở rộng |
| **M8** | Quản lý thiết bị bàn giao cho nhân viên | P4 | Mở rộng |

---

### 2.2 MODULE 1: HỒ SƠ NHÂN SỰ, HỢP ĐỒNG & CHÍNH SÁCH

**1.1. Hồ sơ nhân sự**
- Dashboard tổng quan cho Giám đốc & HCNS
- Quản lý hồ sơ CBNV, Giáo viên: thông tin cá nhân, ngày vào làm, chức vụ, phòng ban, chi nhánh, tài khoản ngân hàng
- Quản lý chứng chỉ / năng lực (TEFL, TOEIC, bằng cấp) - có cảnh báo trước khi hết hạn

**1.2. Quản lý hợp đồng**

*Loại hợp đồng:*
| Loại | Cách tính lương |
|------|-----------------|
| **CBNV toàn thời gian (Full-time)** | Lương cứng/tháng |
| **CBNV bán thời gian (Part-time)** | Giờ làm thực tế × đơn giá/giờ |
| **Giáo viên bán thời gian** | Giờ dạy (CAMS) × đơn giá/giờ dạy |
| **Thử việc** | % lương chính thức theo chính sách |
| **Hợp đồng dịch vụ** (CTV, thỉnh giảng, tư vấn) | Thanh toán theo đợt (xem mục 1.3) |

*Cấu trúc hợp đồng nhiều tầng:*
- Một nhân viên có thể có **nhiều hợp đồng** (song song hoặc nối tiếp, khác loại / khác cơ sở)
- Một hợp đồng có thể kèm **nhiều phụ lục** (tăng lương, đổi chức vụ, điều chỉnh thời hạn, điều chuyển cơ sở)
- Phụ lục phát sinh **bổ sung sau** ngày ký hợp đồng, có hiệu lực từ ngày xác định, là phiên bản áp dụng cho tính lương
- Mỗi hợp đồng / phụ lục lưu bản scan + trạng thái: `Nháp → Chờ ký → Hiệu lực → Hết hạn → Thanh lý`

**1.3. Nghiệm thu & thanh toán (hợp đồng dịch vụ)**
- Tạo **biên bản nghiệm thu** theo từng đợt / giai đoạn (khối lượng, chất lượng, người nghiệm thu)
- Lập **đề nghị thanh toán** theo đợt, gắn với biên bản nghiệm thu tương ứng
- Workflow trạng thái: `Chờ nghiệm thu → Đã nghiệm thu → Đề nghị thanh toán → Đã thanh toán`
- Tính giá trị còn lại của hợp đồng & cảnh báo đợt thanh toán đến hạn

**1.4. Kỷ luật**
- Thang kỷ luật: **Cảnh cáo → Giáng chức → Tạm đình chỉ → Chấm dứt hợp đồng**
- Tính khấu trừ lương theo mức độ kỷ luật (cấu hình được)
- Lưu hồ sơ kỷ luật đầy đủ: lý do, hành vi, biên bản, quyết định, người ký

**1.5. Chính sách & danh mục**
- Danh mục phụ cấp (cấp, thâm niên, trách nhiệm, khác)
- Cấu hình chính sách theo Hội sở, áp dụng đồng nhất cho 4 chi nhánh

**1.6. Audit trail**
- Quản lý lịch sử thay đổi: tài khoản ngân hàng, lương, chức vụ, hợp đồng, phụ lục

---

### 2.3 MODULE 2: CHẤM CÔNG GPS, CA LÀM VIỆC & ĐỐI SOÁT GIẢNG DẠY

**2.1. Chấm công GPS**
- Xác minh tọa độ cơ sở, bán kính cho phép (cấu hình riêng cho từng chi nhánh)
- Tự động tính phút đi muộn / về sớm
- Bảng quản lý chấm công toàn hệ thống (filter: cơ sở, phòng ban, trạng thái)

**2.2. Check-in thủ công (khi GPS không khả dụng)**
- Upload ảnh chứng minh (selfie, QR code tại cơ sở, ảnh bảng hiệu)
- Nhập lý do (đi muộn, về sớm, dạy tại địa điểm ngoài cơ sở)
- Workflow: `CBNV submit → Quản lý cơ sở phê duyệt → HCNS confirm`

**2.3. Ca làm việc**
- Phân ca theo chi nhánh, theo ca (sáng/chiều/tối), theo lịch dạy

**2.4. Bù công & giải trình**
- CBNV gửi đơn bù công kèm bằng chứng (ảnh/video) → Quản lý cơ sở phê duyệt → HCNS xác nhận

**2.5. Đối soát giảng dạy với CAMS**
- Tích hợp dữ liệu ca dạy từ hệ thống CAMS (hệ thống đào tạo hiện tại)
- **Backup nhập ca dạy thủ công** (hàng ngày / hàng tuần) nếu CAMS gặp sự cố
- Đối soát: giờ dạy trong CAMS vs giờ check-in vs hợp đồng

---

### 2.4 MODULE 3: QUẢN LÝ ĐƠN TỪ

**3.1. Các loại đơn**

| Nhóm | Loại đơn | Cấp duyệt |
|------|----------|-----------|
| **Thường** | Nghỉ phép, WFH, Công tác, Bù công | Cấp 1 |
| **Đặc biệt** | Nghỉ không lương, Thay đổi lương, Kỷ luật, Dạy thêm (OT) | Cấp 2 (escalate) |

**3.2. Workflow duyệt 2 cấp độ**
- **Cấp 1 (Bộ phận)**: Quản lý cơ sở → Trưởng HR (cho đơn thông thường)
- **Cấp 2 (Escalate)**: Trưởng HR → Giám đốc (cho đơn đặc biệt, hoặc đơn bị từ chối ở cấp 1)

**3.3. Đơn dạy thêm (OT)**
- Giáo viên request giờ dạy thêm → Quản lý cơ sở phê duyệt → tính lương riêng theo giờ OT

**3.4. Quỹ phép năm**
- Tự động cộng theo thâm niên, chuyển phép sang năm mới, theo dõi số dư phép từng nhân viên

---

### 2.5 MODULE 4: ĐỘNG CƠ TÍNH LƯƠNG TỰ ĐỘNG

**4.1. Công thức tính lương**

```
┌─ LƯƠNG CƠ BẢN ────────────────────────────────────────────┐
│ Lương theo thời gian làm việc                              │
│   + Thưởng (điểm số / doanh số / KPI)                     │
│   + Phụ cấp (cấp, thâm niên, trách nhiệm, khác)           │
│   − Khấu trừ (đi muộn, kỷ luật)                           │
└─────────────────────────────────────────────────────────────┘

LƯƠNG RÒNG = Lương cơ bản − BHXH/BHYT/BHTN (%) − Thuế TNCN
```

**4.2. Lương theo thời gian làm việc**
- **Full-time**: `Lương cứng / tháng`
- **Part-time / Giáo viên**: `Giờ làm thực tế × Đơn giá / giờ`
  - Giáo viên: `Giờ dạy từ CAMS × Đơn giá / giờ dạy`

**4.3. Thưởng lương**

| Loại thưởng | Cơ sở tính |
|-------------|-----------|
| **Thưởng điểm số** | Đánh giá performance / thái độ (thang 0-10 điểm) → quy đổi % |
| **Thưởng doanh số** | % chỉ tiêu đăng ký đạt được (chủ yếu Tư vấn Tuyển sinh) |
| **Thưởng KPI** | Chỉ tiêu cụ thể theo vị trí (bề mặt dạy, số học viên, chất lượng...) |

**4.4. Thuế TNCN (bảng tính riêng)**
- Upload bảng thuế theo năm từ Bộ Tài chính & Kế hoạch - version hóa, **không hardcode**
- Biểu thuế lũy tiến theo từng mức lương
- `Thuế TNCN = (Thu nhập tính thuế − Giảm trừ gia cảnh) × Thuế suất − Giảm trừ`
- Cấu hình: mức giảm trừ gia cảnh, số người phụ thuộc

**4.5. Cấu hình hệ thống**
- Kỳ lương (hàng tháng, nửa tháng...)
- Tỷ lệ BHXH/BHYT/BHTN theo pháp luật

**4.6. Xử lý dữ liệu tính lương**
- Tổng hợp công tháng từ GPS + đơn phép đã duyệt + ca dạy CAMS
- **Kiểm tra dữ liệu CAMS trước tính lương** (alert nếu thiếu dữ liệu ca dạy)
- **Xử lý lương nhân viên vào/ra giữa tháng** (tính theo ngày làm việc, có policy rõ ràng)
- Bảng lương tổng hợp, chi tiết từng loại thu nhập & khấu trừ
- Audit trail cho mọi điều chỉnh lương / chức vụ

**4.7. Xuất & phê duyệt lương**
- Xuất phiếu lương Excel (chi tiết & tổng hợp) → gửi email tự động
- Workflow: `HCNS xác nhận dữ liệu → Kế toán phê duyệt → Giám đốc ký → Phát lương`

---

### 2.6 MODULE 5: BÁO CÁO NHÂN SỰ & QUẢN TRỊ

**5.1. Executive Dashboard (Giám đốc)**
- Tổng chi phí nhân sự/tháng toàn hệ thống + so sánh 4 chi nhánh theo xu hướng (tháng/năm)
- Chi phí nhân sự/đầu người & tỷ lệ % chi phí nhân sự trên doanh thu (theo chi nhánh)
- Năng suất lao động: doanh thu/đầu người, giờ dạy/giáo viên, tỷ lệ lấp đầy lớp
- Cảnh báo bất thường: CBNV không chấm công nhiều ngày, biến động lương > ngưỡng cấu hình, kỷ luật mới phát sinh
- Dự báo chi phí nhân sự 3-6 kỳ tới; tình trạng hợp đồng sắp hết hạn / cần gia hạn

**5.2. Báo cáo Trưởng HR (Hội sở)**
- Chi phí lương tổng hợp (so sánh 4 chi nhánh, % trên doanh thu)
- Chi phí lương/đầu người theo phòng ban (6 bộ phận)
- Năng suất giảng dạy giáo viên (theo giáo viên & chi nhánh)
- Tỷ lệ đi muộn & chấp hành kỷ luật (theo cơ sở, phòng ban)
- Danh sách CBNV & giáo viên (filter: cơ sở, phòng ban, loại hợp đồng)
- Kỷ luật & cảnh báo (ai bị cảnh cáo, giáng chức, đình chỉ)
- Tỷ lệ từ chối đơn từ (kiểm soát chất lượng quy trình duyệt)
- Dự báo chi phí lương các kỳ tới (trend analysis)
- Tỷ lệ giữ chân CBNV (retention rate) theo chi nhánh
- Hợp đồng sắp hết hạn / cần gia hạn / thanh lý
- Công nợ hợp đồng dịch vụ (đợt đã nghiệm thu nhưng chưa thanh toán)

**5.3. Báo cáo Quản lý cơ sở (Chi nhánh)**
- Chấm công chi tiết (cơ sở mình)
- Đơn từ đang xử lý & lịch sử (pending / approved / rejected)
- Lương sơ bộ trước khi HCNS xác nhận
- Kỷ luật & cảnh báo (cơ sở mình)

---

### 2.7 MODULE 6: TUYỂN DỤNG CƠ BẢN (Lightweight ATS) — *Phase 4*
- Đăng tin tuyển dụng (internal job board)
- Thu thập hồ sơ ứng viên qua form online
- Quản lý ứng viên theo stage: `Nhận CV → Phỏng vấn → Trúng tuyển → Nhận việc`
- **Onboarding tự động**: Ứng viên nhận việc → tạo hồ sơ nhân sự + tài khoản chấm công + sinh hợp đồng mẫu
- Báo cáo tuyển dụng: Cost per hire, Time to hire, nguồn ứng viên hiệu quả

### 2.8 MODULE 7: ĐÁNH GIÁ KPI ĐƠN GIẢN — *Phase 4*
- Template KPI theo chức vụ (config cho từng vị trí ở 6 bộ phận)
- Quy trình đánh giá: `Tự đánh giá → Đánh giá quản lý trực tiếp → Hoàn tất`
- **Sync KPI → Lương**: KPI đã duyệt → tự động đẩy vào Module 4
- Báo cáo phân bổ KPI theo phòng ban / cơ sở

### 2.9 MODULE 8: QUẢN LÝ THIẾT BỊ BÀN GIAO CHO NHÂN VIÊN — *Phase 4*
- Danh mục thiết bị bàn giao (laptop, điện thoại, tablet, thiết bị di động...)
- Ghi nhận bàn giao: ngày cấp, trạng thái, điều khoản bàn giao, người nhận
- **Liên kết offboarding**: Nhân viên nghỉ việc → checklist thu hồi thiết bị
- Mất mát / hỏng hóng → ghi nhận & xử lý (trừ lương nếu có quy định)
- Báo cáo: đang bàn giao, chưa thu hồi, hỏng
- *Giai đoạn sau: mở rộng sang quản lý tài sản chung của công ty*

---

### 2.10 Người dùng hệ thống

**Nhóm 1 - Người dùng quản lý (Primary Users)**
| Vai trò | Số lượng | Chức năng chính |
|---------|---------|-----------------|
| **Trưởng bộ phận HCNS** (Hội sở) | 1 | Quản lý hồ sơ, hợp đồng, kỷ luật; duyệt đơn cấp 2; thiết lập chính sách & công thức lương; duyệt lương; xem báo cáo tổng hợp |
| **Nhân viên HCNS** (Hội sở) | 2-3 | Hỗ trợ quản lý hồ sơ; xử lý đơn từ cấp 1; validate dữ liệu CAMS; báo cáo |

**Nhóm 2 - Người dùng chi nhánh (Operational Users)**
| Vai trò | Số lượng | Chức năng chính |
|---------|---------|-----------------|
| **Quản lý cơ sở** (Chi nhánh ×4) | 4 | Duyệt đơn cấp 1; phân ca; giám sát chấm công; nghiệm thu hợp đồng dịch vụ; xem báo cáo chi nhánh |
| **HR/Admin Chi nhánh** (Chi nhánh ×4) | 4 | Nhập dữ liệu hồ sơ; xử lý check-in thủ công; hỗ trợ CBNV; báo cáo cơ sở |

**Nhóm 3 - Người dùng cuối (End Users)**
| Vai trò | Số lượng | Chức năng chính |
|---------|---------|-----------------|
| **CBNV & Giáo viên** | 100-300+ | Chấm công GPS / check-in; tạo đơn từ; xem phiếu lương; xem số liệu phép; cập nhật thông tin cá nhân; gửi form feedback |
| **Giám đốc / Ban Giám đốc** *(tùy chọn)* | 2-5 | Xem Executive Dashboard; duyệt đơn cấp cao (nếu escalate); ký phiếu lương |
| **Kế toán trưởng** *(tùy chọn)* | 2-3 | Cấu hình công thức lương & bảng thuế; phê duyệt lương; xuất phiếu lương |

**Ma trận quyền (tóm tắt)**

| Chức năng | Trưởng HR | NV HR | QL cơ sở | Admin CN | CBNV/GV |
|-----------|-----------|-------|----------|-----------|---------|
| Xem dashboard tổng | ✅ | ✅ | ⛔ | ✅ (cơ sở) | ⛔ |
| Quản lý hồ sơ (tất cả) | ✅ | ✅ | ⛔ | ✅ (cơ sở) | ⛔ |
| Duyệt đơn cấp 1 | ✅ | ✅ | ✅ | ⛔ | ⛔ |
| Duyệt đơn cấp 2 | ✅ | ⛔ | ⛔ | ⛔ | ⛔ |
| Cấu hình công thức lương | ✅ | ⛔ | ⛔ | ⛔ | ⛔ |
| Tính & duyệt lương | ✅ | ✅ (nhập) | ✅ (sơ bộ) | ⛔ | ⛔ |
| Chấm công / check-in | ✅ | ✅ | ✅ | ✅ | ✅ |
| Xem phiếu lương cá nhân | ✅ | ✅ | ✅ | ✅ | ✅ |

### 2.11 Ngoài phạm vi (Out of scope)
- ❌ Đào tạo & phát triển (LMS) - học viên, khóa học, lộ trình đào tạo
- ❌ Helpdesk / Ticketing system
- ❌ CRM quản lý khách hàng / phụ huynh
- ❌ Quản lý tài sản cố định toàn công ty (chỉ thiết bị bàn giao cho NV ở M8)

---

## 3. MÔ HÌNH DỮ LIỆU (DATA MODEL - HIGH LEVEL)

```
Employee (Nhân viên) 1 ──── * Contract (Hợp đồng)
                        1 ──── * ContractAmendment (Phụ lục)
                        1 ──── * Attendance (Chấm công)
                        1 ──── * LeaveRequest (Đơn từ)
                        1 ──── * PayrollRecord (Bảng lương)
                        1 ──── * Certificate (Chứng chỉ)
                        1 ──── * DisciplineRecord (Kỷ luật)
                        1 ──── * DeviceHandover (Thiết bị)

Contract 1 ──── * ContractAmendment 1 ──── * PaymentRequest (Đề nghị thanh toán)
                                                 1 ──── * AcceptanceRecord (Biên bản nghiệm thu)

Employee * ──── 1 Branch (Chi nhánh)
Employee * ──── 1 Department (Bộ phận)
Branch 1 ──── * WorkLocation (Tọa độ GPS, bán kính)
```

**Quy tắc quan trọng:**
1. `Employee` là thực thể trung tâm, mọi dữ liệu đều tham chiếu `employee_id`
2. `Contract` có `effective_from` / `effective_to`; `ContractAmendment` ghi đè giá trị từ `effective_from` của nó
3. Khi tính lương kỳ K: lấy hợp đồng hiệu lực tại K, cộng dồn các phụ lục có hiệu lực ≤ K
4. `Branch` là ràng buộc bắt buộc - mọi query đều scope theo chi nhánh (trừ vai trò Hội sở)

---

## 4. YÊU CẦU KỸ THUẬT

### 4.1 Technology Stack (Đề xuất)

**Web (Hội sở & Chi nhánh):**
- React 18+ / Next.js 14+
- TypeScript
- TailwindCSS / Ant Design / Material-UI
- React Query / SWR (data fetching)
- Zustand / Jotai (state management)
- Recharts / Chart.js (biểu đồ báo cáo)

**Mobile (CBNV & Giáo viên):**
- React Native / Flutter (Expo nếu dùng React Native)
- **Geolocation API** (GPS chấm công)
- **React Native Maps** (hiển thị cơ sở)
- **Image compression library** (upload ảnh check-in)
- **Offline support** (chấm công offline, sync khi có mạng)

**Backend:**
- Node.js + NestJS / Express
- PostgreSQL (database chính)
- Redis (caching, session)
- Bull/BullMQ (job queue cho tính lương, gửi email, đồng bộ CAMS)

**DevOps:**
- Docker + Docker Compose
- AWS / DigitalOcean / VPS
- Nginx (reverse proxy)
- PM2 (process manager)
- GitHub Actions (CI/CD)

### 4.2 Tích hợp bên ngoài
- **CAMS (hệ thống đào tạo)**: API hoặc database sync để lấy dữ liệu ca dạy
- **Email Service**: SendGrid / AWS SES để gửi phiếu lương & thông báo
- **SMS Gateway** *(optional)*: Gửi thông báo chấm công, nhắc nhở đơn từ
- **Banking API** *(optional)*: Chuyển lương tự động
- **Storage (S3/MinIO)**: Lưu trữ bản scan hợp đồng, phụ lục, ảnh check-in

### 4.3 Yêu cầu phi chức năng
- **Performance**: Dashboard load < 2s; chấm công GPS response < 1s
- **Security**: JWT authentication, RBAC theo cơ sở & vai trò, HTTPS, 2FA cho HCNS & Kế toán
- **Scalability**: Hỗ trợ 500+ user đồng thời
- **Availability**: 99.5% uptime
- **Backup**: Daily database backup, retention 30 ngày; backup file hợp đồng ≥ 5 năm
- **Audit**: Ghi log mọi thao tác ghi/xóa dữ liệu lương, hợp đồng, kỷ luật

---

## 5. KIẾN TRÚC HỆ THỐNG (HIGH-LEVEL)

```
┌─────────────────┐      ┌─────────────────┐      ┌─────────────────┐
│   Web App       │      │   Mobile App    │      │   Admin Panel   │
│   (React)       │      │ (React Native)  │      │   (React)       │
└────────┬────────┘      └────────┬────────┘      └────────┬────────┘
         │                        │                        │
         └────────────────────────┼────────────────────────┘
                                  │
                         ┌────────▼────────┐
                         │   API Gateway   │
                         │   (NestJS)      │
                         │  + RBAC/Scope   │
                         └────────┬────────┘
                                  │
          ┌───────────────────────┼───────────────────────┐
          │                       │                       │
    ┌─────▼─────┐         ┌──────▼──────┐        ┌──────▼──────┐
    │ Auth      │         │ HR Core     │        │ Payroll     │
    │ Service   │         │ Service     │        │ Engine      │
    │  + RBAC   │         │ (M1-M3, M6-8)│       │  (M4)       │
    └───────────┘         └──────┬──────┘        └──────┬──────┘
                                 │                      │
                          ┌──────▼───────┬──────────────▼──────┐
                          │  PostgreSQL  │      Redis Cache    │
                          └──────────────┴─────────────────────┘
                                          │
                                ┌─────────▼─────────┐
                                │  CAMS / Email /   │
                                │  Storage (S3)     │
                                └───────────────────┘
```

---

## 6. TIMELINE & ROADMAP (Dự kiến)

| Phase | Nội dung | Thời gian |
|-------|----------|-----------|
| **P1 - MVP** | M1 hồ sơ cơ bản · M2 chấm công GPS (web + mobile) · M3 đơn từ + workflow · Auth & phân quyền | 3-4 tháng |
| **P2 - Core** | M4 tính lương tự động · Tích hợp CAMS · Email phiếu lương · Dashboard cơ bản | 2-3 tháng |
| **P3 - Advanced** | M5 báo cáo phân tích · Quản lý hợp đồng + phụ lục · Nghiệm thu & thanh toán · Quỹ phép năm tự động | 2 tháng |
| **P4 - Extended** | M6 ATS · M7 KPI · M8 Thiết bị | 2-3 tháng |
| **P5 - Optimization** | Performance · Mobile polish · UAT & training · Go-live | 1-2 tháng |

**Tổng thời gian ước tính: 10-14 tháng**

> **Lưu ý:** Phase 1-3 (8-9 tháng) đã đủ đưa vào vận hành thử nghiệm (pilot). Phase 4 & 5 có thể chạy song song hoặc triển khai sau go-live tùy nguồn lực. Nếu cần go-live sớm, tách Phase 4 thành đợt nâng cấp sau 3-6 tháng.

---

## 7. RISK & MITIGATION

| # | Risk | Impact | Mitigation |
|---|------|--------|-----------|
| 1 | Tích hợp CAMS thất bại | High | Phương án nhập ca dạy thủ công qua Excel import hoặc nhập tay hàng tuần |
| 2 | Lương tính sai do dữ liệu CAMS không chính xác | **High** | Validate dữ liệu trước tính lương, alert nếu thiếu/sai, bước HCNS confirm |
| 3 | Tính lương từ hợp đồng/phụ lục sai (khi có nhiều phụ lục) | **High** | Áp dụng phụ lục có hiệu lực mới nhất theo ngày, audit trail mọi phiên bản |
| 4 | Bảng thuế TNCN thay đổi theo chính sách nhà nước | **High** | Tách bảng thuế thành module riêng, version theo năm, cấu hình qua admin (không hardcode) |
| 5 | Dữ liệu lương nhạy cảm bị leak | **High** | Encrypt dữ liệu lương, audit log chi tiết, 2FA cho HCNS & Kế toán, RBAC chặt |
| 6 | Quản lý hợp đồng dịch vụ phức tạp (nhiều đợt thanh toán) | Medium | Workflow rõ ràng: hợp đồng → biên bản nghiệm thu → đề nghị thanh toán → thanh toán, có cảnh báo đợt |
| 7 | Công thức lương phức tạp, thay đổi thường xuyên | Medium | Formula engine linh hoạt, cấu hình được qua admin UI |
| 8 | GPS không chính xác ở một số cơ sở | Medium | Check-in thủ công kèm ảnh/QR, admin điều chỉnh bán kính theo cơ sở |
| 9 | Quy trình duyệt đơn không rõ ràng | Medium | Xác định rõ 2 cấp duyệt: Quản lý cơ sở → Trưởng HR; escalate → Giám đốc |
| 10 | HCNS Hội sở overload khi duyệt đơn từ 4 chi nhánh | Medium | Phân quyền: Quản lý cơ sở duyệt đơn thông thường, chỉ escalate đơn đặc biệt |
| 11 | Xử lý lương nhân viên vào/ra giữa tháng | Medium | Quy trình tính lương theo ngày làm việc, có policy rõ ràng |
| 12 | Giáo viên dạy nhiều cơ sở → chấm công & lương khó đối soát | Medium | Tách bảng giờ dạy theo cơ sở, đối soát 3 nguồn (CAMS - check-in - hợp đồng) |
| 13 | Phase 4 kéo dài timeline | Medium | Phase 4 triển khai sau go-live nếu cần ra sản phẩm sớm (P1-3 đủ MVP) |
| 14 | Module ATS/KPI/Thiết bị quá đơn giản không đáp ứng | Low | Phiên bản lightweight đủ cho 100-300 user, nâng cấp sau nếu cần |

---

## 8. SUCCESS METRICS (KPIs)

| Chỉ số | Mục tiêu | Thời điểm đo |
|--------|----------|-------------|
| Adoption rate - CBNV dùng chấm công GPS | >90% | Sau 1 tháng go-live |
| Time saving - chấm công & tính lương | Giảm 60% | So với quy trình thủ công |
| Accuracy - sai sót phiếu lương | <1% | Mỗi kỳ lương |
| User satisfaction | >4.0/5.0 | Survey sau 1 & 3 tháng |
| Tỷ lệ đơn từ tự động (không cần thao tác tay) | >85% | Sau 3 tháng |
| Tỷ lệ hợp đồng có phụ lục cập nhật đúng hạn | 100% | Mỗi quý |

---

## 9. NEXT STEPS

1. ✅ **Kick-off meeting** với stakeholders (Giám đốc, HCNS, Kế toán, đại diện 4 chi nhánh)
2. 📋 **Thu thập requirements chi tiết:**
   - Công thức lương: lương cứng, đơn giá/giờ, đơn giá/giờ dạy
   - Cơ chế thưởng: thang điểm số, công thức doanh số, chỉ tiêu KPI từng vị trí
   - **Bảng tính thuế TNCN hiện hành** (biểu lũy tiến, mức giảm trừ gia cảnh, người phụ thuộc)
   - Quy trình duyệt đơn: đơn nào duyệt ở cấp bộ phận, đơn nào escalate
   - **Danh sách 4 chi nhánh + GPS coordinates + bán kính cho phép**
   - Danh mục 6 bộ phận Hội sở & mapping nhân sự theo phòng ban
   - **API documentation của CAMS**
   - Chính sách xử lý lương nhân viên vào/ra giữa tháng
   - Mẫu hợp đồng & phụ lục, quy trình nghiệm thu - thanh toán hợp đồng dịch vụ
3. 🎨 **Wireframe & UI/UX design** (2 tuần)
4. 🏗️ **Architecture design** chi tiết (1 tuần) - focus vào security, audit trail & multi-branch data scoping
5. 💻 **Development Phase 1** (MVP)

---

## 10. LỊCH SỬ PHIÊN BẢN

| Version | Ngày | Thay đổi chính |
|---------|------|---------------|
| 1.0 | 25/10/2026 | Bản khởi tạo - 5 modules, phạm vi, tech stack, roadmap |
| 1.1 | 25/10/2026 | Bổ sung check-in thủ công, bù công, backup CAMS, workflow duyệt 2 cấp, risk & mitigation |
| 1.2 | 25/10/2026 | Tách vai trò Hội sở / Chi nhánh; chi tiết hợp đồng, kỷ luật, chứng chỉ, báo cáo theo cấp |
| 1.3 | 25/10/2026 | Bổ sung công thức lương theo Full-time/Part-time, thưởng điểm số/doanh số/KPI, bảng thuế TNCN riêng |
| 1.4 | 25/10/2026 | Bổ sung cấu trúc hợp đồng nhiều tầng (nhiều hợp đồng - nhiều phụ lục), nghiệm thu & thanh toán hợp đồng dịch vụ |
| 2.0 | 25/10/2026 | **Sắp xếp lại toàn bộ**: thêm bối cảnh tổ chức (6 bộ phận - 4 chi nhánh), nguyên tắc thiết kế, mô hình dữ liệu, ma trận quyền, roadmap dạng bảng, 14 risks, lịch sử phiên bản |

---

**Prepared by:** Claude AI
**Reviewed by:** Trưởng bộ phận Hành chính Nhân sự - VietElite
**Date:** 25/10/2026
**Version:** 2.0
