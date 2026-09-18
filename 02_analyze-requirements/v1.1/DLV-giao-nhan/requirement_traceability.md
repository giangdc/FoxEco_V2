# Requirement Traceability — v1.1 · Module DLV

> Tạo bởi: analyze-requirements (DELTA 2026-09-15) · layout **module-first v2**.
> **Home của Source Quote per REQ = §2 file này.** SC quote → `test_scenario_map.md` · CL quote → `risk_assessment.md`.
> `req_notation` của `DOC-v1.1-01` = `FR<NN>` / `BR<FF>-NN` / `AC-{US}.{Scenario}.{Case}` / `NFR-NN` ⇒ **Schema A**.
> ⚠️ Delta lớn nhất của lượt này. Chứa REQ **NEW** + REQ **MODIFIED** (giữ ID cũ). 13 REQ carry nguyên trạng từ v1.0 (`REQ-DLV-001, 003..006, 008..011, 013..016`) xem `02_analyze-requirements/v1.0/DLV-giao-nhan/requirement_traceability.md`.
> 🔴 **`REQ-DLV-017` mở rộng lớn so với v1.0** — màn "Xác nhận giao hàng" (Carrier, FR07) từ 1 nút + popup đơn giản (`REQ-DLV-003` ô#3 `KB-DLV-01`) thành form đầy đủ 4 loại đối tượng nhận. ⚠️ **KHÔNG nhầm với `C-DLV-03`** — CL đó nói về màn KHÁC (Receiver "Xác nhận NHẬN hàng", `FR10`/`REQ-DLV-008`), không đổi ở lượt này, vẫn CARRIED nguyên trạng. Xem Analyst Note dưới.

## 1. Traceability Matrix (REQ → DOC → SC)

### Schema A — Module DLV — DOC-v1.1-01

| REQ ID | Maps (Ref DOC) | DOC §section | Scenarios | Clarification |
|--------|----------------|--------------|-----------|---------------|
| REQ-DLV-002 | `FR12`, `§8.12.3` | §8.12.3 (trang 46) | SC-DLV-031, SC-DLV-032, SC-DLV-033 | — |
| REQ-DLV-007 | `FR10`, `BR10-04` | §8.10.1 (trang 43) | SC-DLV-034 | — |
| REQ-DLV-012 | `FR06`, `BR06-01` | §8.6.1 (trang 38) | SC-DLV-035, SC-DLV-036 | C-DLV-04 (Resolved) |
| REQ-DLV-017 | `FR07`, `BR07-01..07` | §8.7, §8.7.1, §8.7.3 (trang 39-41) | SC-DLV-037, SC-DLV-038, SC-DLV-039, SC-DLV-040, SC-DLV-041, SC-DLV-042 | — |
| REQ-DLV-018 | `FR08`, `BR08-01..07` | §8.8, §8.8.1, §8.8.2 (trang 41-42) | SC-DLV-043, SC-DLV-044, SC-DLV-045, SC-DLV-046, SC-DLV-047, SC-DLV-048 | — |
| REQ-DLV-019 | `FR09`, `BR09-01..07` | §8.9, §8.9.1, §8.9.2 (trang 42-43) | SC-DLV-049, SC-DLV-050, SC-DLV-051, SC-DLV-052, SC-DLV-053, SC-DLV-054 | — |
| REQ-DLV-020 | `FR12`, `§8.12.4` | §8.12.4 (trang 46) | SC-DLV-055, SC-DLV-056, SC-DLV-057 | — |
| REQ-DLV-021 | `FR12`, `BR12-01..03, BR12-07` | §8.12.1 (trang 44-45) | SC-DLV-058, SC-DLV-059, SC-DLV-060 | — |
| REQ-DLV-022 | `NFR-03`, `NFR-07`, `NFR-12` | §9 (trang 53-54) | SC-DLV-061, SC-DLV-062, SC-DLV-063 | — |
| REQ-DLV-023 | `FR18`, `BR18-04` | §8.18.1 (trang 51-52) | SC-DLV-064 | — |

## 2. Requirement Source Detail (verbatim quotes — home của REQ quote)

### REQ-DLV-002 · Ma trận hành động mở rộng — 3 nhóm trạng thái hậu-FR09 *(MODIFIED)*
📍 `DOC-v1.1-01 §8.12.3 "Hành động khả dụng theo trạng thái" · trang 45-46`  ·  Clarif: —

> "RESCHEDULED | Xem lịch hẹn giao lại | Giao lại theo lịch (mở lại màn giao hàng) | Xem lịch hẹn"
> "RETURNING | 'Xác nhận đã nhận lại hàng' · xem lịch hẹn | Xem lịch hẹn trả hàng | Xem lý do hoàn hàng"
> "RETURNED · CANCELLED · EXPIRED | Xem lý do · đăng lại | Xem lý do | Xem lý do"

↳ **Ghi chú:** Ma trận gốc v1.0 (`REQ-DLV-002`, `KB-DLV-01`, 15 ô có ảnh Figma xác nhận) chỉ phủ **5 trạng thái cốt lõi** (Chờ ghép/Đã ghép/Đang giao/Đã giao/Hoàn thành) — **KHÔNG đổi**, vẫn là nguồn mạnh nhất cho 5 trạng thái đó (Figma-verified > bảng PRD cấp mô tả). PRD v1.1 `§8.12.3` bổ sung **3 nhóm trạng thái hoàn toàn mới** phát sinh từ luồng FR08/FR09 (`RESCHEDULED`, `RETURNING`, và nhóm đóng `RETURNED/CANCELLED/EXPIRED`) — chưa từng có SC ở v1.0. Bảng PRD chỉ cho mô tả cấp danh mục (không có microcopy nút chính xác như `KB-DLV-01`) ⇒ **bundle 1 SC/nhóm trạng thái** (3 nhánh vai trong Then) thay vì atomize theo từng ô như ma trận gốc — vì chưa có bằng chứng Figma xác nhận từng ô riêng lẻ.

---

### REQ-DLV-007 · Đơn có sự cố (INCIDENT) không tự về COMPLETED *(MODIFIED — bổ sung BR)*
📍 `DOC-v1.1-01 §8.10.1 "FR10" BR10-04 · trang 43`  ·  Clarif: —

> "BR10-04 | Đơn có báo cáo sự cố (INCIDENT) không tự chuyển về COMPLETED — phải qua admin hỗ trợ dựa trên nhật ký và ảnh."

↳ **Ghi chú:** Mở rộng `REQ-DLV-007` (v1.0 — mốc 2h+2h nhắc/admin) với nhánh mới: khi đơn đã chuyển `INCIDENT` (báo sự cố sau `IN_TRANSIT`, cross-ref `REQ-DLV-015` v1.0), đơn **không** đi theo mốc thời gian 2h+2h thông thường của `DELIVERED`→chờ Receiver xác nhận — mà đứng yên chờ admin xử lý dựa trên nhật ký. Đây là nhánh **không có ở v1.0** (v1.0 chỉ ghi nhận "phải tạo sự cố", không nói kết cục sau đó là gì).

---

### REQ-DLV-012 · Ảnh lúc lấy hàng — tuỳ chọn, tối đa 5 *(MODIFIED — resolve gap v1.0)*
📍 `DOC-v1.1-01 §8.6.1 "FR06" BR06-01 · trang 38`  ·  Clarif: `C-DLV-04` (Resolved 2026-09-15)

> "BR06-01 | Ảnh lúc lấy hàng là tuỳ chọn nhưng được khuyến nghị mạnh; tối đa 5 ảnh."

↳ **Ghi chú:** ⭐ **REQ này RESOLVE gap có chủ đích của v1.0** (`REQ-DLV-012` cũ, `PUP-03` — không có bề mặt UI mô tả, PM chưa trả lời, `KB-DLV-01` không thấy nút chụp ảnh ở ô "Đã ghép"). PRD chính thức giờ xác nhận: ảnh lúc lấy hàng **có tồn tại**, **tuỳ chọn** (không bắt buộc), trần **5 ảnh** (dùng chung rule `BR18-01` — cross-ref `REQ-DLV-023`). Mở CL mới `C-DLV-04` chỉ để ghi nhận việc resolve này (đóng ngay, không blocking) vì gap cũ không có ID CL riêng ở v1.0.

---

### REQ-DLV-017 · Xác nhận giao hàng (Carrier) — 4 loại đối tượng nhận + ảnh bắt buộc + field spec *(NEW — mở rộng lớn)*
📍 `DOC-v1.1-01 §8.7 "FR07", §8.7.1 BR07-01..07, §8.7.3 UI/Field Spec · trang 39-41`  ·  Clarif: —

> Description (§8.7): "Ghi nhận việc bàn giao hàng với đối tượng nhận rõ ràng và bằng chứng ảnh bắt buộc, phục vụ truy vết và xử lý tranh chấp."
>
> BR07-01: "Bắt buộc chọn 1 trong 4 đối tượng nhận: Người nhận · Người được uỷ quyền · Quầy lễ tân · Quầy bảo vệ."
> BR07-02: "Ảnh khi giao là bắt buộc ≥ 1 (tối đa 5) cho mọi kết cục giao; nút xác nhận vô hiệu hoá đến khi đủ ảnh."
> BR07-03: "Với ba lựa chọn khác 'Người nhận': tên người nhận thay là bắt buộc (2–60 ký tự), số điện thoại là khuyến nghị. Quầy lễ tân/bảo vệ vẫn phải nhập tên người trực — không cho ghi chung chung."
> BR07-04: "Người nhận uỷ quyền do người gửi chỉ định lúc đăng tin, hoặc do người nhận / người gửi chỉ định tại hiện trường; ứng dụng luôn ghi rõ ai uỷ quyền. Người vận chuyển không tự chọn người nhận thay."
> BR07-05: "Trường 'Uỷ quyền bởi' tự sinh: 'Người nhận' khi đến từ màn Xác nhận giao hàng, 'Người gửi' khi đến từ màn Liên hệ người gửi. Chỉ đọc."
> BR07-06: "Mọi thao tác ghi mốc không thể hoàn tác đều qua popup xác nhận nêu rõ hệ quả trước khi ghi."
> BR07-07: "Ảnh bằng chứng không xoá được sau khi đơn đã ghi mốc (phục vụ truy vết)."

↳ **Ghi chú:** ⚠️ **KHÔNG nhầm với `C-DLV-03`** — CL đó (Resolved 2026-07-27, `KB-DLV-03`) nói về màn **Receiver "Xác nhận đã NHẬN hàng"** (`FR10`/`REQ-DLV-008`, transition DELIVERED→COMPLETED), chốt dùng **modal đơn giản**, không đổi ở lượt này (vẫn CARRIED, xem `SC-DLV-025`). Còn đây (`REQ-DLV-017`) là màn **Carrier "Xác nhận giao hàng"** (`FR07`, transition IN_TRANSIT→DELIVERED) — 2 màn, 2 vai trò, 2 chiều transition khác nhau. Ở v1.0, màn Carrier này chỉ có **1 nút + 1 popup xác nhận đơn giản** (`REQ-DLV-003` ô#3 `KB-DLV-01`: *"Carrier — Đã giao cho người nhận | 'Bạn xác nhận đã giao hàng tận tay người nhận?'"*, không có lựa chọn đối tượng nhận nào khác). PRD v1.1 **mở rộng đáng kể** thành form đầy đủ 4 loại đối tượng nhận + ảnh bắt buộc + field tên/SĐT người nhận thay + cơ chế uỷ quyền tự sinh — hoàn toàn mới, không mâu thuẫn với CL nào của v1.0. ⚠️ **Rủi ro execute:** nếu app STG **chưa build** form mới này thì `SC-DLV-037..042` sẽ FAIL hàng loạt vì "app chưa cập nhật theo PRD", không phải bug nghiệp vụ — ghi ở `risk_assessment.md RISK-DLV-08`. Fan-out 6 SC: 1 happy path (Người nhận) + 1 uỷ quyền + 1 quầy (gộp lễ tân/bảo vệ) + 1 boundary ảnh bắt buộc + 1 ảnh không xoá được + 1 popup xác nhận.

---

### REQ-DLV-018 · Xử lý khi không liên lạc được người nhận — luồng 4 nhánh ưu tiên *(NEW)*
📍 `DOC-v1.1-01 §8.8 "FR08", §8.8.1 BR08-01..07, §8.8.2 UI/Field Spec · trang 41-42`  ·  Clarif: —

> Description: "Cung cấp đường xử lý chuẩn khi người vận chuyển tới nơi mà không liên lạc được người nhận, thay vì để họ tự quyết định."
>
> BR08-01: "Người vận chuyển không được tự ý để hàng ở nơi khác mà không đi qua luồng này."
> BR08-02: "Thứ tự ưu tiên xử lý (màn hình sắp xếp đúng thứ tự này): (1) giao cho người uỷ quyền người gửi đã khai sẵn → (2) liên hệ người gửi xin uỷ quyền người khác → (3) gửi quầy lễ tân/chốt bảo vệ → (4) cầm hàng về."
> BR08-03: "Màn 'Liên hệ người gửi': ô tên và số điện thoại người nhận thay để trống (không prefill), dòng 'Uỷ quyền bởi: Người gửi', ảnh bắt buộc; hiển thị số điện thoại người gửi có thể bấm gọi."
> BR08-04: "Hai phương án gửi quầy: bắt buộc ≥ 1 ảnh và tên người trực quầy, ghi chú tuỳ chọn, có popup xác nhận trước khi ghi."
> BR08-05: "Đơn có cờ không liên lạc được người nhận thì hiện cảnh báo trong nhật ký cho cả ba bên."
> BR08-06: "Thời hạn giữ hàng tại quầy: nhắc người nhận sau 4 giờ và cuối ngày; sau 24 giờ chưa xác nhận thì chuyển admin hỗ trợ."
> BR08-07: "Nếu không có ai ở quầy để ghi tên thì không xác nhận được — buộc chuyển sang 'Cầm hàng về'."

↳ **Ghi chú:** REQ hoàn toàn mới, không có tương đương ở v1.0 — cả BRD lẫn PRD-demo cũ đều không mô tả luồng này. Cross-ref `REQ-DLV-017` (dùng chung field tên/SĐT người nhận thay + cơ chế uỷ quyền). Fan-out 6 SC: thứ tự ưu tiên · liên hệ người gửi · gửi quầy từ luồng này · không ai ở quầy (fallback bắt buộc) · cờ cảnh báo nhật ký 3 bên · thời hạn giữ hàng (GAP thời gian, cùng tiền đề khó như `RISK-DLV-04` cũ).

---

### REQ-DLV-019 · Cầm hàng về — 2 chế độ retry/return + lịch hẹn *(NEW)*
📍 `DOC-v1.1-01 §8.9 "FR09", §8.9.1 BR09-01..07, §8.9.2 UI/Field Spec · trang 42-43`  ·  Clarif: —

> Description: "Khi không giao được, người vận chuyển cầm hàng về và hẹn lịch rõ ràng: giao lại sau, hoặc trả hàng về cho người gửi. Đơn không bị huỷ."
>
> BR09-01: "'Cầm hàng về' không phải huỷ đơn — đơn vẫn sống ở RESCHEDULED/RETURNING và bắt buộc có lịch hẹn."
> BR09-02: "Bắt buộc chọn chế độ: giao lại sau (`retry`) hoặc trả về người gửi (`return`)."
> BR09-03: "Lịch hẹn dùng giờ chính xác (không dùng buổi)... giờ đến > giờ từ, tối thiểu 30 phút."
> BR09-04: "Lịch hẹn phải trong vòng 7 ngày kể từ ngày cầm hàng về; quá lịch hẹn 24 giờ mà đơn chưa đóng thì chuyển admin hỗ trợ."
> BR09-05: "Chế độ `retry`: theo lịch hẹn, đơn quay lại IN_TRANSIT và người vận chuyển giao lại theo FR07."
> BR09-06: "Chế độ `return`: người gửi bấm 'Xác nhận đã nhận lại hàng' → RETURNED. Đơn RETURNED không mở bước tặng quà và không cộng vào 'Đơn đã giúp' của người vận chuyển, nhưng vẫn nằm trong lịch sử đơn."
> BR09-07: "Người nhận từ chối nhận hàng: người vận chuyển chọn chế độ `return`, ghi lý do vào ghi chú."

↳ **Ghi chú:** REQ hoàn toàn mới, tiếp nối trực tiếp `REQ-DLV-018` (1 trong 4 nhánh ưu tiên của FR08). ⚠️ `BR09-06` là oracle quan trọng dễ bị bỏ sót: `RETURNED` **không** giống `COMPLETED` — không mở bước tặng quà (khác `GIFT` module) và **không cộng** vào chỉ số "Đơn đã giúp" của Carrier ở `HOME`/hồ sơ cá nhân — cross-ref khi `GIFT`/`USR` được rà lại delta sau. Fan-out 6 SC theo field rules + 2 chế độ + hệ quả đặc biệt của `return` + nhánh người nhận từ chối + GAP thời gian (24h→admin, cùng nhóm tiền đề khó như `REQ-DLV-018`).

---

### REQ-DLV-020 · Nhật ký ghi nội dung phân nhánh theo kết cục giao *(NEW)*
📍 `DOC-v1.1-01 §8.12.4 "Nội dung dòng nhật ký theo kết cục giao" · trang 46`  ·  Clarif: —

> "Giao tận tay người nhận → 'Đã giao tận tay người nhận'"
> "Giao cho người được uỷ quyền → 'Đã giao cho người được uỷ quyền — {tên · SĐT} — uỷ quyền bởi {người gửi/người nhận}'"
> "Gửi quầy lễ tân → 'Đã gửi tại quầy lễ tân — {tên người trực quầy}'"
> "Gửi quầy/chốt bảo vệ → 'Đã gửi tại quầy bảo vệ — {tên người trực}'"
> "Cầm hàng về, hẹn giao lại → 'Cầm hàng về — hẹn giao lại {ngày · giờ · nơi hẹn}'"
> "Trả về người gửi → 'Đã trả lại người gửi'"
> "Mọi dòng | Kèm thời điểm, cờ 'không liên lạc được người nhận' (nếu có) và dấu hiệu 'có ảnh bằng chứng'."

↳ **Ghi chú:** ⭐ Bảng mẫu câu nhật ký **chính xác đến từng chữ** — oracle mạnh nhất của cả module, mở rộng trực tiếp `REQ-DLV-010` (v1.0, lịch sử timeline chung chung không có mẫu câu cụ thể). 6 mẫu câu gộp 3 SC (2 mẫu/SC, theo cặp cùng nhóm hành vi: giao trực tiếp/uỷ quyền · 2 quầy · cầm hàng về/trả người gửi) để không nổ số SC quá mức trong khi vẫn giữ **verbatim từng mẫu câu riêng** trong Then.

---

### REQ-DLV-021 · State machine — chỉ transition hợp lệ, log bất biến, admin can thiệp cũng ghi log *(NEW)*
📍 `DOC-v1.1-01 §8.12.1 "FR12" BR12-01, BR12-02, BR12-03, BR12-07 · trang 44-45`  ·  Clarif: —

> BR12-01: "Chỉ được đi theo chuyển tiếp hợp lệ ở bảng 8.12.2 — mọi request sai trạng thái bị từ chối và không ghi mốc."
> BR12-02: "Không nhảy bậc: không DELIVERED khi chưa IN_TRANSIT, không COMPLETED khi chưa DELIVERED."
> BR12-03: "Mỗi lần đổi trạng thái ghi: trạng thái cũ → mới, actor, thời điểm, ảnh kèm — không sửa, không xoá được."
> BR12-07: "Admin có quyền can thiệp hỗ trợ dựa trên nhật ký; mọi can thiệp cũng được ghi nhật ký."

↳ **Ghi chú:** `BR12-01`/`BR12-02` là bản **chính thức hoá** rule "không nhảy bước" mà v1.0 đã suy luận gián tiếp từ ma trận nút (`REQ-DLV-004`) — giờ có bảng transition tường minh (`§8.12.2`, 12 trạng thái) làm oracle độc lập với UI, phù hợp cho **API-level test** (không chỉ chặn ở nút UI mà chặn cả request trực tiếp). `BR12-07` là REQ mới hoàn toàn (v1.0 không có gì về hành vi log khi Admin can thiệp) — chỉ verify được phần hiển thị phía end-user (dòng log xuất hiện), không verify được thao tác Admin thật (Admin Portal out of scope, `C-TS-01`).

---

### REQ-DLV-022 · NFR hiệu năng/bảo mật/privacy của luồng giao nhận *(NEW)*
📍 `DOC-v1.1-01 §9 "Non-Functional Requirements" · NFR-03, NFR-07, NFR-12 · trang 53-54`  ·  Clarif: —

> NFR-03 | Performance | "Tải 5 ảnh bằng chứng (mỗi ảnh ≤ 5MB) hoàn tất < 15 giây (p95) trên 4G; có chỉ báo tiến trình và cho phép thử lại từng ảnh." | Cách đo: "Test trên thiết bị thật + APM."
> NFR-07 | Data Integrity | "Bản ghi nhật ký đơn là chỉ-thêm (append-only): không API nào cho phép sửa hoặc xoá bản ghi và ảnh bằng chứng đã ghi." | Cách đo: "Code review + security test."
> NFR-12 | Privacy | "Dữ liệu người nhận thay (tên · số điện thoại) chỉ dùng làm bằng chứng bàn giao; không xuất hiện ở bất kỳ báo cáo/thống kê nào ngoài nhật ký đơn." | Cách đo: "Code review + kiểm tra báo cáo."

↳ **Ghi chú:** 3 NFR gộp 1 REQ vì cùng nhóm "chất lượng hệ thống của luồng giao nhận", mỗi NFR có 1 SC riêng (test type khác nhau). ⚠️ **`NFR-07` liên quan trực tiếp `RISK-TS-01`** (v1.0, `TS` module) — bug đã ghi nhận "huỷ nhận đơn XOÁ dòng 'Ghép thành công'" **vi phạm thẳng NFR-07** (không chỉ vi phạm `TS-02`/`BR-INT-04` như ghi nhận cũ). NFR-07 **không resolve** bug này — chỉ xác nhận thêm bằng văn bản chính thức rằng đây đúng là vi phạm nghiêm trọng, không phải diễn giải chủ quan của QA. `NFR-03`/`NFR-12` cần công cụ ngoài UI thuần (APM/thiết bị thật; rà báo cáo/thống kê — hiện chưa có màn báo cáo nào trong scope end-user nên chỉ ghi nhận nguyên tắc).

---

### REQ-DLV-023 · Icon copy nhanh SĐT/địa chỉ ở màn Theo dõi đơn *(NEW)*
📍 `DOC-v1.1-01 §8.18.1 "FR18" BR18-04 · trang 52`  ·  Clarif: —

> ↪ *Quote `BR18-04` (icon copy) — home ở `../ORD-dang-tin/requirement_traceability.md` (không chép lại — tránh lặp home, health-check G-03 2026-09-17)*

↳ **Ghi chú:** `FR18` là tiện ích dùng chung nhiều màn (chi tiết tin ở `FEED`, theo dõi đơn ở `DLV`) — REQ này chỉ phủ instance ở **màn Theo dõi đơn** (thuộc `DLV`). Instance ở màn Chi tiết tin (`FEED`) **chưa được rà lại** ở lượt delta này (`FEED` ngoài scope `DOC-v1.1-01`, xem `MASTER-MEMORY.md`) — không tạo REQ/SC bên đó. Trần ảnh dùng chung (`BR18-01/02/03/05`) đã áp trực tiếp vào `REQ-DLV-012`/`REQ-DLV-017` thay vì tạo REQ `FR18` riêng, tránh trùng lặp SC cho cùng 1 hành vi ảnh.

---

> Clarification quote ở `risk_assessment.md` (layout v2) · SC quote ở `test_scenario_map.md`.
> REQ không có delta (`REQ-DLV-001, 003..006, 008..011, 013..016`) → xem `v1.0/DLV-giao-nhan/requirement_traceability.md`, không lặp lại quote ở đây.
