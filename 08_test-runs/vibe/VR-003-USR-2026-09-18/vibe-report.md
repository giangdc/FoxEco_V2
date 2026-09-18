# Vibe Report — VR-003 — module USR — 2026-09-18

## Scope Coverage

| | |
|---|--:|
| **SCOPE_TOTAL (module USR)** | **46** |
| Có verdict cuối **trước** phiên | 41 |
| TC chạy **trong phiên này** | **4** |
| Có verdict cuối **sau** phiên | **45 / 46** |
| **CÒN NỢ** | **1** (`TC-USR-005`) |
| Evidence | 4/4 TC chạy trong phiên đều có ảnh riêng |

| Verdict (tích luỹ cả module) | Trước VR-003 | Sau VR-003 |
|---|--:|--:|
| ✅ PASS | 20 | **22** |
| ❌ FAIL | 14 | **16** |
| 🚫 BLOCKED | 5 | 5 |
| ⛔ N-A | 2 | 2 |
| ⚠️ NOT_EVIDENCED | 0 | 0 |
| ⏳ NOT_RUN | 5 | **1** |
| **Σ** | 46 | **46** |

> ⚠️ **Đính chính bookkeeping của `coverage-USR.md`:** bảng §Tổng hợp trước phiên ghi `BLOCKED 6 / NOT_RUN 4`, nhưng đếm trên bảng chi tiết là **BLOCKED 5 / NOT_RUN 5** (lúc `TC-USR-027` đổi `BLOCKED → NOT_RUN` ngày 2026-09-18, §Tổng hợp không được cập nhật theo). Tổng Σ vẫn đúng 46 nên lỗi không lộ ra. Đã sửa trong phiên này.

## Kết quả từng TC

| TC | P | Verdict | Điểm chốt |
|---|---|---|---|
| TC-USR-006 | P2 | ✅ PASS | Card chỉ số hiện đủ 2 ô, cả 2 = `0`, card không bị ẩn |
| TC-USR-027 | P3 | ✅ PASS | 2 lần lưu liên tiếp đều không banner + đều về màn "Cá nhân" ⇒ hành vi nhất quán (đúng bản Steps/Expected sửa 2026-09-18) |
| TC-USR-040 | P2 | ❌ FAIL | Field "Địa chỉ mặc định" **rỗng** — không prefill từ HRIS |
| TC-USR-043 | P2 | ❌ FAIL | Field "Số điện thoại mặc định" **rỗng** — không prefill từ HRIS, dù HRIS CÓ SĐT |
| TC-USR-005 | P2 | ⏳ NOT_RUN | QC chốt bỏ qua phiên này — QC tự tạo data 3 vai rồi báo lại |

## 🐞 Ứng viên bug mới — **B9** (1 bug, 2 TC)

| | |
|---|---|
| **Tên đề xuất** | `[USR - Tài khoản & Hồ sơ] - Màn "Cập nhật thông tin" không prefill SĐT và địa chỉ mặc định từ HRIS ở lần mở đầu tiên` |
| **TC liên quan** | `TC-USR-040` (địa chỉ) · `TC-USR-043` (SĐT) — **cùng 1 defect, gộp 1 bug** |
| **Severity đề xuất** | Medium — không mất dữ liệu, nhưng mọi CBNV mới đều phải tự gõ lại thông tin đã có sẵn trên HRIS; trái `BA chốt 2026-09-16` + `§8.15.2` |
| **Bằng chứng** | `TC-USR-040__step5-FAIL-*.png` · `TC-USR-043__step5-FAIL-*.png` · page source: cả 2 EditText `showing-hint="true"` |
| **Reproduce** | Bất kỳ tài khoản **chưa từng lưu hồ sơ** nào → FoxEco → Cá nhân → Cập nhật thông tin → cả 2 field rỗng |
| **Không phải ca lẻ** | VR-001 đã quan sát **y hệt** trên tài khoản **A** (có đủ SĐT + địa chỉ HRIS đã biết) ⇒ 2 tài khoản, 2 phiên, cùng hiện tượng |
| **Lệnh** | ✅ **ĐÃ LOG: `BUG-008`** → `05_bug-reports/draft/BUG-008-khong-load-sdt-dia-chi-tu-hris.md` (draft, **chưa push Jira** theo yêu cầu QC). Push khi sẵn sàng: `/log-bug --push-jira BUG-008` |

## 🙋 3 việc cần QC / BA quyết — ✅ **ĐÃ XỬ LÝ HẾT 2026-09-18**

> Cập nhật sau khi QC GiangDC2 phản hồi cùng ngày. Bảng gốc giữ nguyên bên dưới để truy vết.

| # | Kết quả |
|---|---|
| **Q1** `TC-USR-044` | 🔴 **GIỮ NGUYÊN `N-A`/DESCOPED** — QC chốt *"địa chỉ data hris luôn luôn có nhé, nếu mặc định, hiện tại ko có do bị bug không load data từ hris ấy"* ⇒ ô rỗng là **triệu chứng của `BUG-008`**, không phải nhánh *"HRIS trống"*. Lập luận đòi mở lại TC **bị bác**. Ghi ở `coverage-USR.md` (`041`+`044`) · `risk_assessment.md §C-USR-05 ↳ Rule địa chỉ mặc định` · `MASTER-MEMORY §1 + §8b`. |
| **Q2** địa chỉ rỗng vẫn lưu được | 🟡 **Mở clarification `C-USR-07`** — home ở `v1.1/USR-tai-khoan/risk_assessment.md`, đồng bộ `CL-hoi-BA-v1.1.xlsx` (USR: 0 → **1** điểm hỏi BA) + `counts` (`cl` 6→7, `cl_open` 0→1) + router + MASTER. 🔍 Hoá ra **không phải câu hỏi mới**: đây đúng là **câu (v)** trong 6 câu con của `C-USR-05`, BA chưa từng trả lời nhưng CL vẫn bị đóng `Resolved` ⇒ **đóng CL gộp làm rơi câu hỏi con**. |
| **Q3** Title `TC-USR-027` | ✅ **ĐÃ SỬA** — QC chốt trực tiếp. Title mới: `Check hai lần lưu liên tiếp đều không hiện banner và đều về màn "Cá nhân"`, đồng bộ fragment + `TC-MASTER-v1.1.xlsx` + `TC-MASTER-LATEST.xlsx` (2 sheet/file, md5 2 file khớp, Σ TC vẫn **223** · USR **38** · 0 trùng ID). ⚠️ **`TC-USR-015` vẫn còn Title cũ** (*"hiển thị đúng banner xanh"*) — **việc treo riêng, chưa được chốt sửa**. |

## 🙋 Bảng gốc — 3 việc cần QC / BA quyết (⛔ phiên này không tự đổi)

| # | Việc | Dữ kiện mới từ phiên này |
|---|---|---|
| **Q1** | **`TC-USR-044` đang `⛔ N-A` (DESCOPED) — nên xem lại.** | Đã nêu ở VR-001; phiên này **củng cố thêm**: tài khoản `00002352` mở lần đầu ⇒ ô SĐT rỗng thật, đúng tình huống mà `TC-USR-044` mô tả. Nhưng lý do DESCOPE ("HRIS trống SĐT") vẫn đúng về mặt data ⇒ đây là **TC mô tả sai nguyên nhân**, không phải TC thừa. |
| **Q2** | **Địa chỉ mặc định rỗng có hợp lệ không?** (câu hỏi đang treo ở `TC-USR-029`) | Phiên này lưu **2 lần** với field địa chỉ **để rỗng** — app **cho lưu bình thường**, không chặn, không báo lỗi. Có dữ kiện thực nghiệm để BA chốt. |
| **Q3** | **`Test Title` của `TC-USR-027` vẫn là "Check banner đã lưu tự ẩn…"** trong khi Steps/Expected đã sửa sang "hành vi không-banner nhất quán" | Title không thuộc field được sửa theo `Project_rule §10.5` ⇒ cần QC chốt riêng, **giống hệt case `TC-USR-015`**. Người đọc Title sẽ hiểu ngược nội dung TC. |

## 📨 Phản hồi ngược → `/analyze-requirements`

| # | Bề mặt | Lệnh đề xuất |
|---|---|---|
| **R3** | Nợ upstream đã ghi từ VR-001 vẫn chưa xử lý: `SC-USR-014`/`SC-USR-019` + `BR15-05` + `AC-30.1.01` vẫn mô tả *"banner xanh + ở lại màn"* / *"banner tự ẩn"*, trong khi app **bỏ hẳn banner** và QC đã chốt hành vi này là ĐÚNG. Phiên này `TC-USR-027` PASS theo hành vi không-banner ⇒ **2 TC (015, 027) nay mâu thuẫn với đặc tả**. | `/analyze-requirements --module USR --update "FoxEco bỏ hẳn banner sau khi lưu hồ sơ, điều hướng về màn Cá nhân — cập nhật SC-USR-014, SC-USR-019, BR15-05, AC-30.1.01"` |
| **R4** | `SC-USR-022`/`SC-USR-023` đặc tả *"prefill từ HRIS"* nhưng app không prefill ⇒ nếu BA xác nhận **app đúng** thì 2 SC này sai; nếu BA xác nhận **spec đúng** thì B9 là bug. **Chưa kết luận — cần BA.** | `/log-bug` trước (B9), BA phản hồi rồi mới quyết có `--update` scenario không |

## 🗂️ Dữ liệu phát sinh trên STG

| Hạng mục | Chi tiết |
|---|---|
| **Hồ sơ `00002352` đã bị đổi** | SĐT mặc định lưu thành `0987654322` (lưu 2 lần: `0987654321` rồi `0987654322`). Địa chỉ mặc định vẫn **rỗng**. |
| ⚠️ **`00002352` KHÔNG còn trạng thái "chưa từng lưu hồ sơ"** | ⛔ Không dùng lại tài khoản này để test prefill-HRIS lần đầu. Muốn retest `TC-USR-040/043` sau khi dev fix B9 ⇒ **cần một tài khoản mới chưa từng lưu** (vai **C** `00041796` vẫn còn nguyên trạng thái, chưa dùng). |
| 2 chỉ số card | vẫn `0 / 0` — việc lưu hồ sơ không ảnh hưởng chỉ số ⇒ `TC-USR-006` không bị hỏng bởi phiên này |

## Locator Coverage

| Màn đã thăm | Element captured | Verified ✅ | Inferred ⚠️ | Not found 🚫 |
|---|--:|--:|--:|--:|
| **5** (2 FoxEco + 3 HRIS) | **19** | **17** | **1** | **1** |

→ Bổ sung 4 bẫy kỹ thuật mới (T1–T4) vào `vibe-locators.md §4`. **T2 là bẫy nguy hiểm nhất**: field rỗng vẫn trả `text` = chuỗi hint ⇒ assert `text != ""` sẽ PASS oan.

## Recommendation

| Hành động | Số TC | Lệnh / việc |
|---|--:|---|
| ~~Log bug B9~~ ✅ **XONG** | 2 TC | `BUG-008` đã tạo ở `draft/`, severity `Major`, chưa push Jira |
| **Chờ QC tạo data** | **1** | `TC-USR-005` — QC tạo đơn 3 vai xong thì `/vibe-test --tc TC-USR-005` |
| **Chờ dev trả lời FE-298** | 5 | `TC-USR-032/034/035/036/037` — refresh `DOC-v1.1-04` rồi chạy lại |
| ~~QC/BA quyết~~ ✅ **XONG** | — | Q1 bác (giữ N-A) · Q2 → `C-USR-07` (chờ BA) · Q3 đã sửa Title |
| **Route về analyze** | — | R3 (bỏ banner) · R4 (prefill HRIS — sau khi BA phản hồi B9) |

### ▶️ Phiên vibe kế tiếp
1. `TC-USR-005` khi QC báo data đã sẵn sàng (cần 3 vai + 1 đơn chạy tới "Hoàn thành").
2. `TC-USR-032/034/035/036/037` khi `FE-298` có kết luận.
3. Retest `TC-USR-040/043` sau khi B9 được fix — **nhớ dùng tài khoản chưa từng lưu hồ sơ** (vai C `00041796` còn nguyên).
