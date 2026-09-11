---
id: v1.0/ORD-dang-tin/risk
title: Risk Assessment — v1.0 · Module ORD
type: risk-assessment
version: v1.0
sprint: 1
module: ORD
counts:
  cl: 10
  risk: 8
  cl_open: 5
  cl_resolved: 5
status: ANALYZED
updated: 2026-09-07
---

# Risk Assessment — v1.0 · Module ORD

> **Structure-lock:** bảng 9 cột. Nguồn PRIMARY duy nhất cho risk module ORD.
> 🔑 Frontmatter `counts:` = nguồn canonical CL/RISK — **chỉ đếm CL có home ở module này**; CL tham chiếu (home ở module khác) KHÔNG tính vào `counts`. **Layout v2 ⇒ đây là home của Clarification.**

## Tổng quan
| Module | Risk Level | Rủi ro chính |
|--------|-----------|--------------|
| ORD | **High** | Module lớn nhất (22 REQ / 51 SC) và là nơi tập trung **4 nghi vấn bug đã có screenshot** + **3 mâu thuẫn giá trị mặc định** giữa BRD / PRD / app. Sai nhãn chip "Loại hàng" ở đây lan sang cả `FEED` và toàn bộ bộ TC |

## Chi tiết rủi ro (bảng hợp nhất)
| Risk ID | Module/Area | Rủi ro | Severity | Why (Source) | Test Focus | Solution | Status | REQ/SC |
|---------|-------------|--------|----------|--------------|------------|---------------------|--------|--------|
| RISK-ORD-01 | ORD / Loại hàng | **Nhãn chip lệch 3 nguồn**; app không có chip "Tài liệu" mà tài liệu + toàn bộ TC cũ đều ghi "Tài liệu" ⇒ TC sai chữ hàng loạt, FAIL vì lý do không liên quan nghiệp vụ | **High** | `D8.1` L357 vs `DOC-v1.0-02` §3.5.1 vs `KP-01` §10.2 (screenshot VR-002 `TC_04.5` FAIL) | Ghi nhận danh mục thật 1 lần (`SC-ORD-006`), mọi TC sau tham chiếu | Hỏi BA/Dev: UI đổi tên hay tài liệu sai (`C-ORD-09`); tới khi đó dùng nhãn app | Open | REQ-ORD-003, SC-ORD-005, SC-ORD-006 |
| RISK-ORD-02 | ORD / Người gửi | **3 nghi vấn bug chưa log**: Tên không read-only + bị xoá trắng · Địa chỉ lấy hàng không pre-fill · SĐT tự đổi giá trị giữa phiên | **High** | `KP-01` §10.5/§10.6/§10.10 (VR-002 `TC_04.21`, `TC_04.22` FAIL) | `SC-ORD-015/016/017` viết theo spec, dự kiến FAIL | Log bug sau khi chạy; riêng địa chỉ phải xác nhận dev trước (`C-ORD-10`) | Open | REQ-ORD-007, SC-ORD-015, SC-ORD-016, SC-ORD-017 |
| RISK-ORD-03 | ORD / Rule "bắt buộc" B1 | Rule *"Loại hàng không cho để trống"* **không kiểm chứng được qua UI** (chip luôn có default, không deselect) ⇒ TC negative không có cách nào thiết lập precondition | Medium | `KP-01` §10.3 (VR-002 `TC_04.6` FAIL vì precondition không lập được) | `SC-ORD-007` ghi nhận gap thay vì TC negative | Chấp nhận; nếu cần verify rule thì phải test qua API/backend | Pending | REQ-ORD-003, SC-ORD-007 |
| RISK-ORD-04 | ORD / Người nhận | `C-ORD-01` chốt **CÓ** rule bắt buộc nhưng prototype cho để trống hoàn toàn vẫn đăng thành công ⇒ nếu app STG còn hành vi này thì đây là **lỗ validate nghiêm trọng** (đơn không có người nhận) | **High** | `KP-01` §3 KB-ORD-01 vs `DOC-v1.0-02` §7 dòng 2 | `SC-ORD-022` (P1) — assert chặn, dự kiến FAIL | Chạy sớm; FAIL → log bug P1 | Open | REQ-ORD-009, SC-ORD-022 |
| RISK-ORD-05 | ORD / Checkbox điều khoản | **Mặc định lệch nguồn**: BRD `D8.1` + app = "Chưa tick" ⟷ PRD = "tick sẵn". TC `TC_04.71` đợt cũ expected "tick sẵn" ⇒ sai nguồn | Medium | `D8.1` L373 vs `DOC-v1.0-02` §3.5.3 vs `KP-01` §10.7 | `SC-ORD-033` assert "chưa tick" theo BRD+app | Hỏi BA chốt (`C-ORD-12`); sửa kỳ vọng của TC cũ khi migrate | Resolved | REQ-ORD-013, SC-ORD-033 |
| RISK-ORD-06 | ORD / Hết hạn tin | `SC-ORD-045` cần đơn có "Đến ngày" **đã trôi qua** ⇒ không seed nhanh được bằng UI; và `ORD-06` ⟷ `US-D04` mô tả 2 hành vi trái nhau (không can thiệp vs tự chuyển) | Medium | `ORD-06` L244 vs `US-D04` L166 · `C-ORD-03` Resolved | Nhờ dev seed đơn quá hạn; assert tự chuyển `EXPIRED` + lý do | Nhờ dev/QA seed trên STG; ghi rõ oracle theo `US-D04` | Open | REQ-ORD-018, SC-ORD-045 |
| RISK-ORD-07 | ORD / Địa chỉ | Field địa chỉ có **3 cơ chế theo 3 nguồn** (preset 6 văn phòng / không chip gợi ý / dropdown autocomplete) và **phải chạm chọn gợi ý mới lưu** ⇒ TC/automation dễ set text rồi tưởng đã lưu | Medium | `LOC-03` L246 vs `US-D01` L164 vs `KP-01` §3 KB-ORD-06 | `SC-ORD-025/026` assert theo autocomplete; `SC-ORD-027` ghi nhận preset | Hỏi BA (`C-ORD-11`); ghi ràng buộc automation vào `CHANGELOG §2` | Open | REQ-ORD-010, SC-ORD-025, SC-ORD-026, SC-ORD-027 |
| RISK-ORD-08 | ORD / Khung giờ | Giá trị mặc định **hết hạn theo đồng hồ thật** ⇒ TC/script hardcode giờ sẽ FAIL ngẫu nhiên theo thời điểm chạy | Medium | `KP-01` §10.11 (`KB-VIBE-10` — xác nhận không phải lỗi app) | Chọn khung giờ tương đối so với "now" | Ghi vào `Project_rule §Test Data Rules` (đã làm) + `CHANGELOG §2` | Resolved | REQ-ORD-012, SC-ORD-029, SC-ORD-030 |

## Clarifications (home của CL quote — layout v2)

| CL ID | Vấn đề | Status | Ngày | REQ/SC liên quan |
|---|---|---|---|---|
| C-ORD-01 | Wizard có field bắt buộc không? maxlength bao nhiêu? | ✅ Resolved — **CÓ**: Loại hàng + Giá trị hàng (B1), Người nhận (B2); maxlength đủ từ `§D8.1/D8.2` | 2026-07-27 → 2026-07-28 | REQ-ORD-003, REQ-ORD-005, REQ-ORD-009 |
| C-ORD-02 | Ngưỡng giá trị hàng bằng số tiền (`BR-ORD-03`) | ✅ Resolved — **Out of scope v1.0** (từng là BLOCKER cứng, gỡ) | 2026-07-27 | REQ-ORD-022 |
| C-ORD-03 | Hạn tin mặc định bao lâu? | ✅ Resolved — = giá trị **"Đến ngày"** user chọn, không phải hằng số | 2026-07-27 | REQ-ORD-018 |
| C-ORD-04 | Chip "Thuốc/Y tế" có bị chặn không? | ✅ Resolved — **KHÔNG chặn ở v1.0**; banner chỉ là thông tin tĩnh | 2026-07-27 | REQ-ORD-014 |
| C-ORD-05 | Màn "Đăng tin thành công" có "Mã tin" hay không? | 🔴 **Open** | kế thừa 2026-07 | REQ-ORD-015 |
| C-ORD-08 | Thoát/Reset giữa wizard có xoá form? | 🔴 **Open** | kế thừa 2026-07 | REQ-ORD-021 |
| C-ORD-09 | 🔴 Danh mục "Loại hàng" — 3 nguồn 3 danh mục; app không có chip "Tài liệu" | 🔴 **Open** | mở 2026-09-07 (nâng từ `KP-05 §1` câu #3) | REQ-ORD-003 |
| C-ORD-10 | 🔴 Địa chỉ lấy hàng không pre-fill — bug hay tài khoản test chưa cấu hình? | 🔴 **Open** | mở 2026-09-07 (từ `KP-05 §1` câu #4) | REQ-ORD-007 |
| C-ORD-11 | 🔴 Cơ chế field địa chỉ — preset 6 văn phòng / không chip gợi ý / autocomplete? | 🔴 **Open** | mở 2026-09-07 | REQ-ORD-010 |
| C-ORD-12 | Mặc định checkbox điều khoản — chưa tick hay tick sẵn? | ✅ Resolved — **chưa tick** (BRD `D8.1` + app STG thắng PRD demo) | 2026-09-07 | REQ-ORD-013 |

### C-ORD-01 · Field bắt buộc + maxlength của wizard

**Source Quote (ambiguous):**
> Nguồn A — spec (`DOC-v1.0-01` §D8.1 L357): "Loại hàng | **Có** | Tài liệu | … Không cho để trống"
> Nguồn B — hành vi (`DOC-v1.0-02` §3.5.1): "⚠ Lưu ý: Không có trường nào bắt buộc (*) — có thể bấm "Tiếp theo" mà không chọn Loại hàng/Giá trị."
> Nguồn C — hành vi (`DOC-v1.0-02` §3.5.2): "⚠ Lưu ý: Có thể bỏ trống toàn bộ thông tin Người nhận mà vẫn qua được Bước 3 — không có validate bắt buộc trong bản demo."

**Source Location:** `DOC-v1.0-01 §D8.1 · bảng · cột "Bắt buộc"` ⟷ `DOC-v1.0-02 §3.5.1 · đoạn lưu ý` · `§3.5.2 · đoạn lưu ý`

**Analyst Note:** BA/PO chốt 2026-07-27: **CÓ** rule bắt buộc (Loại hàng + Giá trị hàng ở B1; Người nhận ở B2); hành vi "không validate" của prototype là thiếu sót, không phải đặc tả. Maxlength bổ sung 2026-07-28 khi BRD v3.2 ra `§D8`: Ghi chú ≤300 · Địa chỉ ≤200 · Tên người nhận 2–60 · khung giờ ≥30 phút. ⚠️ **Hệ quả không lường trước:** rule "Loại hàng bắt buộc" hoá ra **không kiểm chứng được qua UI** (`RISK-ORD-03`) — Resolved về mặt nghiệp vụ nhưng không test được.

### C-ORD-02 · Ngưỡng giá trị hàng bằng số tiền

**Source Quote (ambiguous):**
> "BR-ORD-03 | Giá trị hàng trong ngưỡng cấu hình; trên ngưỡng → cảnh báo nên mua bảo hiểm (phase sau)"

**Source Location:** `DOC-v1.0-01 §D4 · bảng Rule/Mô tả · L262` (và `§D5 · L297`, `§D5 · L311` — chính BRD tự đặt câu hỏi *"Ngưỡng giá trị hàng?"*)

**Analyst Note:** Resolved — Out of scope v1.0 (`KP-01` §3 KB-ORD-04). ⭐ **Từng là BLOCKER cứng duy nhất của đợt cũ**, gỡ 2026-07-27. ⚠️ Ranh giới phải giữ: ngưỡng **bằng số tiền** = out of scope ≠ cảnh báo theo **mức định tính "Cao"** = **CÓ ở v1.0** (`REQ-ORD-005`, đã có nguyên văn banner từ app).

### C-ORD-03 · Hạn tin mặc định

**Source Quote (ambiguous):**
> Nguồn A (`DOC-v1.0-01` §D3 `ORD-06` L244): "Tin hết hạn | **Quá hạn** chưa ghép → gửi thông báo để người đăng tự gỡ/đăng lại; **hệ thống không tự can thiệp ở phase này**"
> Nguồn B (`DOC-v1.0-01` §D1b `US-D04` L166): "**Quá hạn cấu hình** mà chưa MATCHED → **tự chuyển EXPIRED**…"
> Nguồn C (`DOC-v1.0-01` §D5 L311 — chính BRD tự hỏi): "Hạn tin mặc định?"

**Source Location:** `DOC-v1.0-01 §D3 · L244` ⟷ `§D1b · US-D04 · L166` ⟷ `§D5 · L311`

**Analyst Note:** BA/PO chốt 2026-07-27: hạn tin = **giá trị "Đến ngày" user chọn**, không phải hằng số hệ thống; đến đúng "Đến ngày" thì tin **tự chuyển** `EXPIRED` (theo `US-D04`, không theo `ORD-06`). ⚠️ **Lịch sử đảo chiều:** phân tích trước từng chốt nhầm là *"Từ ngày"*, sau đảo lại thành *"Đến ngày"* (khớp BRD v3.2) ⇒ ⛔ đừng trích lại bản "Từ ngày".

### C-ORD-04 · Chip hàng cấm có bị chặn?

**Source Quote (ambiguous):**
> Rule (`DOC-v1.0-01` §A8 L115): "Hàng cấm (thuốc, vũ khí, chất nguy hiểm, phi pháp) không được đăng."
> Danh mục (`DOC-v1.0-02` §3.5.1): "Chip chọn 1: … · **Thuốc/Y tế** · Khác"

**Source Location:** `DOC-v1.0-01 §A8 · blockquote · L115` (và `§D4 BR-ORD-04 · L263`) ⟷ `DOC-v1.0-02 §3.5.1 · dòng "Loại hàng"`

**Analyst Note:** Nghịch lý ngay trong tài liệu: rule cấm gửi thuốc nhưng danh mục **có chip "Thuốc/Y tế"**. BA/PO chốt 2026-07-27: **v1.0 không chặn**, banner cảnh báo chỉ là thông tin tĩnh ⇒ ⛔ không viết TC negative. Đây là **rule tồn tại trong doc nhưng chưa triển khai** — phải phân biệt với bug.

### C-ORD-05 · 🔴 "Mã tin" ở màn Đăng tin thành công

**Source Quote (ambiguous):**
> Nguồn A (`DOC-v1.0-01` §D1b `US-D02` L165): "màn "Đăng tin thành công" (**KHÔNG hiển thị mã đơn** — mã kỹ thuật vô nghĩa với người dùng)"
> Nguồn B (`DOC-v1.0-06` KP-05 §2.2): "Một bản **CÓ** trường "Mã tin" (vd `#ECO-2026-0451`), một bản **KHÔNG**. Đồng thời đối lập trực tiếp với `US-D02`"

**Source Location:** `DOC-v1.0-01 §D1b · US-D02 · L165` ⟷ `DOC-v1.0-04` (2 biến thể trên cùng board Figma) qua `DOC-v1.0-06 KP-05 §2.2`

**Analyst Note:** Mâu thuẫn **ngay trong nguồn thiết kế** (2 biến thể cùng board) và đối lập với AC của BRD ⇒ không nguồn nào thắng được nguồn nào. `SC-ORD-038` **cố ý không assert**. **Non-blocking** nhưng cần chốt trước khi viết TC completeness màn thành công.

### C-ORD-08 · 🔴 Thoát/Reset giữa wizard

**Source Quote (ambiguous):** *(Không có quote — chính sự thiếu vắng là nội dung của clarification)*

**Source Location:** `DOC-v1.0-06 KP-02 §5 · bảng "Nhóm Open" · dòng "C-ORD-08"`

**Analyst Note:** Không doc nào mô tả. Đã có **bằng chứng gián tiếp** rằng hành vi này có ảnh hưởng dữ liệu: `KP-01` §10.5 ghi giá trị Tên bị xoá *"không tự phục hồi trong cùng phiên wizard — phải thoát ra vào lại từ đầu Bước 1/3 mới load lại tên"* ⇒ thoát/vào lại **có** reset một phần. Cần chốt để biết đó là thiết kế hay hệ quả của bug `SC-ORD-015`.

### C-ORD-09 · 🔴 Danh mục "Loại hàng" — 3 nguồn 3 danh mục

**Source Quote (ambiguous):**
> Nguồn A (`DOC-v1.0-01` §D8.1 L357): "Chọn 1 trong danh mục: **Tài liệu · Đồ điện tử · Thực phẩm · Quà tặng · Khác**" *(5 giá trị, mặc định "Tài liệu")*
> Nguồn B (`DOC-v1.0-02` §3.5.1): "Chip chọn 1: **Tài liệu (mặc định) · Đồ điện tử · Thực phẩm · Hàng nhỏ · Đồ dễ vỡ · Quần áo · Thuốc/Y tế · Khác**" *(8 giá trị)*
> Nguồn C (`DOC-v1.0-06` KP-01 §10.2): "app có 8 chip, KHÔNG có chip tên "Tài liệu"… Chip mặc định được chọn là **`Giấy tờ, hồ sơ`**"

**Source Location:** `DOC-v1.0-01 §D8.1 · L357` ⟷ `DOC-v1.0-02 §3.5.1 · dòng "Loại hàng"` ⟷ `DOC-v1.0-06 KP-01 §10.2 "KB-VIBE-01"` (screenshot VR-002 `TC_04.5` FAIL)

**Analyst Note:** ⭐ **Câu hỏi ưu tiên số 1 cho BA/Dev** (`KP-05 §1` câu #3: *"Ảnh hưởng lan rộng nhất — mọi TC nhắc "Tài liệu" đều sai chữ"*). Cần biết: **UI đã đổi tên** (⇒ tài liệu phải cập nhật, TC dùng nhãn app) hay **tài liệu đúng và UI sai** (⇒ log bug). Tới khi có câu trả lời: dùng nhãn app STG (`Giấy tờ, hồ sơ`), `SC-ORD-006` ghi nhận danh mục thật. **Non-blocking** nhưng ảnh hưởng số lượng TC phải sửa lớn nhất.

### C-ORD-10 · 🔴 Địa chỉ lấy hàng không pre-fill — bug hay dữ liệu tài khoản?

**Source Quote (ambiguous):**
> Spec (`DOC-v1.0-01` §D8.1 L364): "Địa chỉ lấy hàng | Có | **Tòa nhà Lô B3, KCX Tân Thuận, Q.7 (điền sẵn từ nơi làm việc của user)** | Không để trống, tối đa 200 ký tự"
> App (`DOC-v1.0-06` KP-01 §10.6): "Thực tế: **field trống, chỉ có placeholder**. Tên ✅ và SĐT ✅ vẫn pre-fill đúng." · "⚠ Chưa loại trừ khả năng **tài khoản test chưa cấu hình địa chỉ mặc định** → cần xác nhận với dev."

**Source Location:** `DOC-v1.0-01 §D8.1 · L364` ⟷ `DOC-v1.0-06 KP-01 §10.6 "KB-VIBE-05"` (VR-002 `TC_04.21` FAIL)

**Analyst Note:** Hai giả thuyết chưa phân định: **(a)** app không đọc nơi làm việc từ hồ sơ ⇒ **bug**; **(b)** tài khoản test chưa có nơi làm việc trong hồ sơ ⇒ **dữ liệu môi trường**, không phải bug. Phân định bằng cách hỏi dev về hồ sơ tài khoản test, hoặc test bằng tài khoản thứ hai **chắc chắn có** nơi làm việc. ⚠️ Đáng chú ý: luồng OFFER (`D8.2` L381) **cho phép** để trống nếu hệ thống chưa có thông tin — tức spec **đã lường trước** tình huống này ở form kia nhưng không ở form này.

### C-ORD-11 · 🔴 Cơ chế field địa chỉ — 3 nguồn 3 cơ chế

**Source Quote (ambiguous):**
> Nguồn A (`DOC-v1.0-01` §D3 `LOC-03` L246): "Quick-select văn phòng FPT | Hiển thị **preset 6 văn phòng** (+ mở rộng theo tỉnh)"
> Nguồn B (`DOC-v1.0-01` §D1b `US-D01` L164): "mỗi điểm lấy/giao **chỉ có 1 input địa chỉ (không chip gợi ý)**"
> Nguồn C (`DOC-v1.0-06` KP-01 §3 KB-ORD-06): "Gõ text tự do → hiện **dropdown gợi ý** danh sách văn phòng khớp từ DB, không phân biệt hoa/thường. **Phải chạm chọn gợi ý** thì giá trị mới được lưu"

**Source Location:** `DOC-v1.0-01 §D3 · L246` ⟷ `§D1b · US-D01 · L164` ⟷ `DOC-v1.0-06 KP-01 §3 "KB-ORD-06"`

**Analyst Note:** Ba cơ chế **loại trừ nhau** cho cùng 1 field, và 2 trong 3 nằm trong **cùng một tài liệu** (BRD `LOC-03` vs `US-D01`). Nguồn C có bằng chứng mạnh nhất (BA trả lời 2026-07-29 + 2 lần vibe-test PASS) ⇒ SC viết theo autocomplete. Câu hỏi cho BA: `LOC-03` (preset 6 văn phòng) **còn hiệu lực ở v1.0** hay đã bị autocomplete thay thế? **Non-blocking.**

### C-ORD-12 · Mặc định checkbox điều khoản

**Source Quote (ambiguous):**
> Nguồn A (`DOC-v1.0-01` §D8.1 L373): "Xác nhận điều khoản | Có | **Chưa tick** | Bắt buộc tick mới bật được nút Đăng tin"
> Nguồn B (`DOC-v1.0-02` §3.5.3): "Checkbox điều khoản | **Mặc định đã tick sẵn** — "Tôi tự chịu trách nhiệm về hàng hoá và thoả thuận với người mang giúp""
> Nguồn C (`DOC-v1.0-06` KP-01 §10.7): "Quan sát thực tế ở Bước 3/3: **chưa tick**, phải chạm tay mới bật được nút "Đăng tin ngay"."

**Source Location:** `DOC-v1.0-01 §D8.1 · L373` ⟷ `DOC-v1.0-02 §3.5.3 · dòng "Checkbox điều khoản"` ⟷ `DOC-v1.0-06 KP-01 §10.7 "KB-VIBE-06"`

**Analyst Note:** **Resolved ở lượt này (2026-09-07)** theo BRD `D8.1` (bản mới hơn) + quan sát app (VR-001 finding #2): mặc định **CHƯA tick**. Đủ chuẩn `Resolved` theo `KP-02 §6` (có nguồn văn bản có ngày + quan sát app trực tiếp). ⚠️ **Hệ quả:** TC `TC_04.71` của đợt cũ expected *"checkbox tick sẵn"* là **sai nguồn** — nếu migrate TC cũ thì phải sửa kỳ vọng này (`KP-04 §4` lỗi #3). Ngoài ra, tick sẵn còn **trái tinh thần consent** của `ORD-09` (*"Bắt buộc tick"*) nên nhánh PRD khó là đặc tả đúng.

## Khuyến nghị tổng thể
1. **Resolve trước generate-tc:** `C-ORD-09` (nhãn Loại hàng) — không chốt thì bộ TC lặp lại đúng lỗi lan rộng nhất của đợt cũ. Kèm `C-ORD-10` (địa chỉ pre-fill) để biết viết TC hay log bug.
2. **Ưu tiên test P1 high-risk:** `SC-ORD-022` (Người nhận bắt buộc — lỗ validate nghiêm trọng nếu FAIL) · `SC-ORD-004` (happy path, chặn mọi module khác nếu FAIL) · `SC-ORD-042` (tuyến OFFER không công khai — quyền riêng tư) · `SC-ORD-044` (khoá sửa từ MATCHED).
3. **Cần môi trường/dữ liệu:** 1 đơn có **"Đến ngày" đã trôi qua** cho `SC-ORD-045` (không seed được qua UI ⇒ nhờ dev) · 1 tài khoản **chắc chắn có nơi làm việc** trong hồ sơ để phân định `C-ORD-10` · bộ ảnh test (≤5MB, >5MB, sai định dạng).
4. **ID/text cleanup (non-blocking, cần trước automation):** chốt nhãn chip Loại hàng · chốt cơ chế field địa chỉ (`C-ORD-11`) vì nó quyết định cách automation nhập địa chỉ (tap suggestion, không set text) · ⛔ không hardcode khung giờ.
