---
id: v1.1/TS-trust-safety/scenario-map
title: Test Scenario Map — v1.1 · Module TS
type: scenario-map
version: v1.1
sprint: 1
module: TS
counts:
  req: 6
  sc: 15
  new: 8
  modified: 0
  carried: 7
  deprecated: 0
  p1: 2
  p2: 5
  p3: 8
status: ANALYZED
updated: 2026-09-15
---

# Test Scenario Map — v1.1 · Module TS

> **Home của SC quote.** REQ quote → `requirement_traceability.md §2` · CL quote → `risk_assessment.md`.
> 🔑 Frontmatter `counts:` = **nguồn canonical** số REQ/SC/priority module TS **tính tới v1.1** (bao gồm CARRIED từ v1.0).
> Parent: `v1.0/TS-trust-safety/` — 7 SC không đổi (CARRIED), 8 SC NEW (toàn bộ gắn 1 REQ mới `REQ-TS-006`).

## Quy tắc đủ scenario (Scenario Sufficiency Rule)

> **1 SC = 1 hành vi nguyên tử.** Fan-out `REQ-TS-006` theo: 1 happy path + 1 negative (thiếu trường bắt buộc) + 2 boundary ảnh đính kèm (0 ảnh hợp lệ / đúng-vượt trần 5) + 1 nhánh lỗi mạng + 1 vòng đời phiên (đóng WebView + phiên mới reset) + 1 đặc điểm field prefill sửa được + 1 UI vị trí trigger đa vai trò = **8 SC**.

## Tổng quan
- Tổng số scenarios (tính tới v1.1): **15** (NEW: 8, MODIFIED: 0, CARRIED: 7, DEPRECATED: 0)
- Phân bổ priority: P1: 2 | P2: 6 | P3: 7
- Delta lớn nhất: **tính năng hoàn toàn mới** "Báo sự cố & hỗ trợ" (`FR16`) — đảo kết luận `C-CNL-01` (v1.0: out of scope) chỉ trong phạm vi module `TS` sở hữu màn hình này.

## Scenarios — NEW & MODIFIED (chi tiết đầy đủ)

### TS — Trust & Safety (delta v1.1 — Báo sự cố & hỗ trợ)

| Scenario ID | Feature | Req ID | DOC Source | Given | When | Then | Priority | Test Type | Lifecycle |
|-------------|---------|--------|-----------|-------|------|------|----------|-----------|-----------|
| SC-TS-008 | Happy path — báo sự cố thành công | REQ-TS-006 | DOC-v1.1-01 §6.2 AC-31.1.01 | Người dùng (vai trò bất kỳ) đang ở màn theo dõi đơn | Bấm "Báo cáo sự cố", chọn loại yêu cầu, nhập mô tả + SĐT hợp lệ, đính kèm 2 ảnh, bấm Gửi | Mở WebView toàn màn hình tới Google Form (thanh URL chỉ đọc + nút đóng); mã đơn/vai trò/trạng thái đơn/MNV/họ tên/phòng ban/SĐT/phiên bản app/hệ điều hành được điền sẵn; sau khi gửi hiện "Đã ghi nhận phản hồi" + cam kết liên hệ lại trong 24 giờ làm việc + nút "Quay lại đơn hàng" | P1 | Functional | NEW |
| SC-TS-009 | Thiếu trường bắt buộc — nút Gửi vô hiệu hoá | REQ-TS-006 | DOC-v1.1-01 §6.2 AC-31.1.02 | Người dùng đang ở form báo sự cố | Chưa chọn loại yêu cầu, HOẶC chưa nhập mô tả, HOẶC SĐT không hợp lệ | Nút "Gửi" vô hiệu hoá; cạnh nút hiện "Điền các mục bắt buộc" | P2 | Business Rule | NEW |
| SC-TS-010 | Ảnh đính kèm là tuỳ chọn — bỏ trống vẫn gửi được | REQ-TS-006 | DOC-v1.1-01 §6.2 AC-31.1.02 · §8.16.2 | Đã đủ 3 trường bắt buộc (loại yêu cầu + mô tả + SĐT hợp lệ), KHÔNG đính ảnh nào | Bấm Gửi | Nút "Gửi" khả dụng và gửi thành công (ảnh không nằm trong điều kiện bắt buộc) | P3 | Boundary | NEW |
| SC-TS-011 | Trần ảnh đính kèm — đúng 5 (hợp lệ) vs 6 (chặn) | REQ-TS-006 | DOC-v1.1-01 §8.16.2 | Form báo sự cố đã đủ trường bắt buộc | Đính kèm lần lượt 5 ảnh (thử gửi) rồi thử đính thêm ảnh thứ 6 | Với 5 ảnh: gửi thành công, xoá được từng ảnh riêng lẻ. Với ảnh thứ 6: KHÔNG thêm được (hoặc bị chặn ở UI) — trần cứng là 5 | P3 | Boundary | NEW |
| SC-TS-012 | Mất mạng khi mở WebView | REQ-TS-006 | DOC-v1.1-01 §6.2 AC-31.2.01 | Thiết bị mất kết nối mạng | Bấm "Báo cáo sự cố" | WebView không tải được → hiện thông báo lỗi kèm nút "Thử lại"; KHÔNG mất ngữ cảnh đơn (mã đơn/vai trò vẫn giữ nguyên khi thử lại có mạng) | P2 | Negative | NEW |
| SC-TS-013 | Vòng đời WebView — đóng không reset ngăn xếp, mở lại là phiên mới | REQ-TS-006 | DOC-v1.1-01 §8.16.1 BR16-04, BR16-06 | Đã mở WebView báo sự cố và nhập dở 1 số trường | (a) Bấm nút đóng WebView; (b) Mở lại "Báo cáo sự cố" từ cùng đơn | (a) Quay lại đúng màn theo dõi đơn trước đó, KHÔNG reset ngăn xếp điều hướng. (b) Form mở như MỘT PHIÊN MỚI — dữ liệu đã nhập ở lần trước KHÔNG còn (đã reset), không phải tiếp tục từ chỗ dở dang | P3 | Business Rule | NEW |
| SC-TS-014 | Field prefill vẫn sửa được (khác field chỉ-đọc SSO) | REQ-TS-006 | DOC-v1.1-01 §8.16.1 BR16-03 | Form báo sự cố đã mở với các trường prefill (mã đơn, vai trò, MNV, họ tên, phòng ban, SĐT…) | Người dùng sửa trực tiếp giá trị 1 trường prefill (vd SĐT liên hệ lại) | Trường prefill CHO PHÉP sửa (dạng câu trả lời ngắn, không phải chỉ đọc); giá trị đã sửa được gửi kèm form, đối chiếu MNV ở khâu xử lý | P3 | Business Rule | NEW |
| SC-TS-015 | Vị trí trigger + hiển thị cho cả 3 vai trò | REQ-TS-006 | DOC-v1.1-01 §8.16 (Trigger) · Actor | Lần lượt đăng nhập Sender · Carrier · Receiver của cùng 1 đơn, mở màn theo dõi đơn | Quan sát góc trên bên phải màn theo dõi đơn | Cả 3 vai trò đều thấy button "Báo cáo sự cố" (bo tròn, nền cam nhạt, icon cảnh báo + chữ) ở đúng vị trí; hành vi mở form giống nhau cho cả 3 vai | P2 | UI | NEW |

#### Source Detail per Scenario (verbatim quotes)

##### SC-TS-008 — Happy path báo sự cố thành công

**Source Quote:**
> AC-31.1.01: "Given: Người dùng đang ở màn theo dõi đơn với vai trò bất kỳ. When: Người dùng bấm button 'Báo cáo sự cố' ở góc trên bên phải, điền loại yêu cầu, mô tả, số điện thoại liên hệ lại, đính kèm tối đa 5 ảnh và gửi. Then: Mở WebView toàn màn hình tới Google Form... Sau khi gửi: hiện 'Đã ghi nhận phản hồi' kèm cam kết liên hệ lại trong 24 giờ làm việc và nút 'Quay lại đơn hàng'."

**Source Location:** `DOC-v1.1-01 §6.2 AC-31.1.01 · trang 29`

**Analyst Note:** Nguồn cho đủ cả 3 phần Given/When/Then nguyên văn — assert được toàn bộ danh sách field prefill (9 field liệt kê tường minh: mã đơn, vai trò, trạng thái đơn, MNV, họ tên, phòng ban, SĐT, phiên bản ứng dụng, hệ điều hành).

---

##### SC-TS-009 — Thiếu trường bắt buộc

**Source Quote:**
> AC-31.1.02: "Given: Người dùng đang ở form báo sự cố. When: Người dùng chưa chọn loại yêu cầu, hoặc chưa nhập mô tả, hoặc số điện thoại không hợp lệ. Then: Nút 'Gửi' vô hiệu hoá, cạnh nút hiện 'Điền các mục bắt buộc'. Ảnh đính kèm là tuỳ chọn — bỏ trống vẫn gửi được khi các trường bắt buộc đã đủ."

**Source Location:** `DOC-v1.1-01 §6.2 AC-31.1.02 · trang 29`

**Analyst Note:** 3 nhánh OR trong Given (chưa chọn loại / chưa nhập mô tả / SĐT sai) gộp 1 SC vì cùng 1 hành vi nguyên tử (nút Gửi disable) — theo Scenario Sufficiency Rule không cần tách 3 SC vì Then giống hệt nhau; `generate-tc` có thể fan-out thêm theo EP nếu cần từng trường riêng.

---

##### SC-TS-010 — Ảnh đính kèm tuỳ chọn

**Source Quote:**
> "Hình ảnh đính kèm | Không | Tải ảnh nhiều tệp · trống | Tối đa 5 ảnh, xoá được từng ảnh; bỏ trống vẫn gửi được"

**Source Location:** `DOC-v1.1-01 §8.16.2 · trang 50`

**Analyst Note:** Câu cuối `AC-31.1.02` ("Ảnh đính kèm là tuỳ chọn — bỏ trống vẫn gửi được") đồng thuận với bảng field spec — 2 nguồn cùng tài liệu củng cố nhau.

---

##### SC-TS-011 — Trần ảnh đính kèm (5 vs 6)

**Source Quote:**
> "Hình ảnh đính kèm | ... | Tối đa 5 ảnh, xoá được từng ảnh; bỏ trống vẫn gửi được"

**Source Location:** `DOC-v1.1-01 §8.16.2 · trang 50`

**Analyst Note:** Trần "tối đa 5" nhắc lại ở cả Trigger (§8.16) lẫn field spec — cùng số với trần ảnh bằng chứng giao hàng ở `FR07`/`FR18` (tiện ích dùng chung đa ảnh) nhưng đây là 1 form khác, độc lập, không dùng chung state.

---

##### SC-TS-012 — Mất mạng khi mở WebView

**Source Quote:**
> AC-31.2.01: "Given: Người dùng bấm 'Báo cáo sự cố' trong lúc thiết bị mất kết nối. When: WebView không tải được. Then: Hiện thông báo lỗi kèm nút 'Thử lại'; không mất ngữ cảnh đơn."

**Source Location:** `DOC-v1.1-01 §6.2 AC-31.2.01 · trang 29`

**Analyst Note:** "Không mất ngữ cảnh đơn" là điều kiện then chốt — thử lại sau khi có mạng phải mở lại đúng form của đúng đơn đó, không quay về màn danh sách hoặc mất mã đơn đã gắn.

---

##### SC-TS-013 — Vòng đời WebView (đóng + phiên mới)

**Source Quote:**
> BR16-04: "Đóng WebView thì quay lại màn trước, không reset ngăn xếp điều hướng. Mất mạng thì hiện lỗi + nút 'Thử lại', không mất ngữ cảnh đơn."
> BR16-06: "Mỗi lần mở form là một phiên mới — reset dữ liệu đã nhập lần trước."

**Source Location:** `DOC-v1.1-01 §8.16.1 BR16-04, BR16-06 · trang 49-50`

**Analyst Note:** 2 BR gộp 1 SC vì cùng mô tả vòng đời của 1 phiên WebView (đóng → mở lại). Đây là hành vi dễ bị hiểu nhầm là "tiếp tục nhập dở" — PRD nói rõ KHÔNG, mỗi lần mở là phiên mới hoàn toàn.

---

##### SC-TS-014 — Field prefill vẫn sửa được

**Source Quote:**
> BR16-03: "Trường prefill là dạng câu trả lời ngắn, người dùng vẫn sửa được — đối chiếu MNV ở khâu xử lý."

**Source Location:** `DOC-v1.1-01 §8.16.1 BR16-03 · trang 49`

**Analyst Note:** ⚠️ Đối lập có chủ ý với field chỉ-đọc từ SSO ở module `USR` (`C-USR` — màn Cá nhân view-only, `MASTER-MEMORY.md` ghi chú registry). Ở đây field prefill (MNV, họ tên, phòng ban…) tuy lấy từ hồ sơ nhưng **KHÔNG bị khoá** — chỉ đối chiếu lại ở khâu xử lý (con người), không phải ràng buộc UI. ⛔ Đừng nhầm assert "read-only" như USR.

---

##### SC-TS-015 — Vị trí trigger + đa vai trò

**Source Quote:**
> Trigger: "Bấm button 'Báo cáo sự cố' ở góc trên bên phải màn Theo dõi đơn (button bo tròn nền cam nhạt, gồm icon cảnh báo + chữ)." Actor: "Người gửi · Người vận chuyển · Người nhận · Admin vận hành (xử lý)."

**Source Location:** `DOC-v1.1-01 §8.16 · trang 49`

**Analyst Note:** "Admin vận hành" chỉ ở vai trò **xử lý** phía sau (ngoài phạm vi test — Admin Portal out of scope theo `C-TS-01`), không phải actor trigger nút này trên app end-user ⇒ SC chỉ test 3 vai Sender/Carrier/Receiver.

## Scenarios — CARRIED (reference only)

| Scenario ID | Tên ngắn | Module | Origin Version | Priority | Reference |
|-------------|----------|--------|---------------|----------|-----------|
| SC-TS-001 | Log đủ mốc + timestamp | TS | v1.0 | P2 | → `v1.0/TS-trust-safety/test_scenario_map.md` |
| SC-TS-002 | Log ghi rõ actor | TS | v1.0 | P2 | → xem v1.0 |
| SC-TS-003 | [GAP·bug] Log bất biến (audit trail) | TS | v1.0 | P1 | → xem v1.0 |
| SC-TS-004 | Consent điều khoản trước khi đăng | TS | v1.0 | P3 | → xem v1.0 |
| SC-TS-005 | [GAP] Không có cơ chế chặn user | TS | v1.0 | P3 | → xem v1.0 |
| SC-TS-006 | [GAP] Hệ quả "admin hỗ trợ" | TS | v1.0 | P3 | → xem v1.0 |
| SC-TS-007 | [GAP] Admin Web Portal không có bề mặt test | TS | v1.0 | P3 | → xem v1.0 |

## Scenarios — DEPRECATED

| Scenario ID | Tên ngắn | Module | Deprecated ở | Lý do |
|-------------|----------|--------|-------------|-------|
| — | *(không có)* | — | — | — |
