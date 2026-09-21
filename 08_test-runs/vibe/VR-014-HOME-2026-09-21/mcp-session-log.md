# MCP Session Log — VR-014 — 2026-09-21

## Session info
- Platform: mobile (Appium MCP, UiAutomator2) · **EMU** `emulator-5554` (1080×2400) · Session ID `b944ccd4-ceb7-4812-bdc2-864228ca23e8` (tái dùng session của VR-013)
- Máy thật `R58T20PLP8K`: **ngắt kết nối** (adb chỉ thấy emulator) ⇒ đổi tài khoản trên 1 máy
- Tài khoản dùng: **Thủy** (`stag_thuyntt22@`, "sạch") ⇄ **Giang** (`stag_giangdc2@`, đăng tin) — **4 lần đổi** (Giang→Thủy→Giang→Thủy→Giang→Thủy), QC duyệt. OTP từ biến `FOXECO_STG_PASS` (không in)
- Pre-flight: ✅ session còn sống · evidence-path `_setup__*.png` ×2 tồn tại

## Pha A / Pha B — tóm tắt
| Nhóm | Snapshot (`get_page_source`) | Ghi chú |
|---|---|---|
| Trang chủ + Tin mới (Thủy) ×4 lần | 4 | đếm card, tìm `Xem thêm trên Bảng tin` |
| Bảng tin (đếm `feed-post-card-N`) ×3 | 3 | tiền đề 5 tin / >5 tin |
| Đăng NEED ×2 (Giang) | 0 | `find_element` + ảnh |
| Statistics | ≈ 8 snapshot · ≈ 330 call (ước lượng) · ≈ 3 màn harvest | chủ yếu do 4 lần đổi tài khoản (~14 call/lần) |
