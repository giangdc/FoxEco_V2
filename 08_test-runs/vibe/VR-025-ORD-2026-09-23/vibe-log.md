# Vibe Test Log — VR-025 — v1.1 — 2026-09-23

> Module: ORD (Đăng tin & Quản lý tin) · Platform: mobile (Appium MCP + adb, UiAutomator2) · Env: STG · app `com.hrisproject.stag` (FoxPro) · Evidence dir: `screenshots/`
> Phiên: 2026-09-23 (khởi tạo, 14:58–15:09)
> Mode: **RETEST** bug Jira ORD đang **In review** (tra Jira trực tiếp 14:55): FE-301 (BUG-009, 11 TC) · FE-303 (BUG-011, `TC-ORD-059`) · FE-330 (không có TC — bug QC log từ test tự do).
> Thiết bị: emulator-5554 (Android, 1080×2400) · Tài khoản A `stag_giangdc2@` — Đặng Châu Giang (vai người gửi, cùng tài khoản lúc log FE-301).
> ⛔ Theo yêu cầu QC: chỉ comment + đính kèm ảnh lên Jira, **KHÔNG đổi trạng thái bug**; không cập nhật TC-MASTER / §8 / coverage trong run này.
> **Không tạo dữ liệu nào trên STG**: mọi nhánh đều bị chặn trước khi đăng; thoát form bằng nút ← không lưu.

## TC-ORD-063: Check thiếu ẢNH HÀNG bị chặn kèm thông báo lỗi (FE-301)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1-5 | "+ Đăng tin" → "Tôi cần gửi hàng" → chọn Thấp · Dưới 5 kg · Nhỏ, không tải ảnh | tap toạ độ chip | ✅ PASS | — | — |
| 6-7 | Nhấn "Tiếp theo", quan sát khối "ẢNH HÀNG" | tap `Tiếp theo` | ✅ PASS | `TC-ORD-063__verify-loi-thieu-anh-hang.png` | vẫn Bước 1/3 · lỗi đỏ **"Vui lòng thêm ít nhất 1 ảnh hàng"** dưới khối ảnh |

**Result: ✅ PASS**

## TC-ORD-064: Check thiếu TRỌNG LƯỢNG bị chặn kèm thông báo lỗi (FE-301)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Form mới: Thấp · Nhỏ · 1 ảnh, **không** chọn trọng lượng → "Tiếp theo" | Photo Picker → Add (1) | ✅ PASS | `TC-ORD-064__verify-loi-thieu-trong-luong.png` | lỗi đỏ **"Vui lòng chọn khối lượng"** ngay dưới 3 chip trọng lượng |

**Result: ✅ PASS** · ghi chú nhỏ: chuỗi lỗi dùng "khối lượng" trong khi nhãn khối là "TRỌNG LƯỢNG".

## TC-ORD-066: Check thiếu KÍCH THƯỚC bị chặn kèm thông báo lỗi (FE-301)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Form mới: Thấp · Dưới 5 kg · 1 ảnh, **không** chọn kích thước → "Tiếp theo" | — | ✅ PASS | `TC-ORD-066__verify-loi-thieu-kich-thuoc.png` | lỗi đỏ **"Vui lòng chọn kích thước"** dưới 3 chip kích thước |

**Result: ✅ PASS**

## TC-ORD-023: Check để trống nhóm Người nhận bị chặn kèm thông báo lỗi (FE-301)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Chọn kích thước Nhỏ → "Tiếp theo" sang Bước 2 | — | ✅ PASS | — | — |
| 2 | Để trống email/tên/SĐT/địa chỉ giao, nhấn "Tiếp theo" | tap | ✅ PASS | `TC-ORD-023__verify-loi-4-o-nguoi-nhan-trong.png` | 4 dòng lỗi: "Email người nhận / Tên người nhận / Số điện thoại / Địa chỉ giao hàng không được để trống"; màn tự cuộn tới nhóm "NGƯỜI NHẬN" |

**Result: ✅ PASS**

## TC-ORD-077: Check email người nhận thiếu tên miền bị báo lỗi (FE-301)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Nhập `stag_anhdc4@` rồi rời ô | adb input text + tap vùng trống | ✅ PASS | `TC-ORD-077__verify-loi-email-thieu-ten-mien.png` | **"Email phải thuộc tên miền nội bộ (@fpt.com hoặc @fpt.com.vn)"**; tên/SĐT/địa chỉ không autofill |

**Result: ✅ PASS**

## TC-ORD-021: Check email người nhận thiếu @ bị báo lỗi (FE-301)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Đổi email thành `stag_anhdc4.fpt.com` rồi rời ô | — | ✅ PASS | `TC-ORD-021__verify-loi-email-thieu-a-cong.png` | cùng chuỗi lỗi tên miền nội bộ ngay dưới ô email |

**Result: ✅ PASS** · ghi chú: không có chuỗi riêng kiểu "sai định dạng" — dùng chung chuỗi tên miền, vẫn đủ dấu hiệu tại đúng ô.

## TC-ORD-024: Check tên người nhận 1 ký tự bị báo lỗi (FE-301)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Nhập `A` vào "Tên người nhận" rồi rời ô | — | ✅ PASS | `TC-ORD-024__verify-loi-ten-1-ky-tu.png` | **"Tên người nhận phải từ 2–60 ký tự"** dưới ô tên |

**Result: ✅ PASS**

## TC-ORD-051: Check bấm Tiếp theo cuộn tới ô lỗi đầu tiên (FE-301)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Giữ các ô sai (email sai, tên 1 ký tự, SĐT + địa chỉ trống), cuộn xuống cuối form | swipe ×3 | ✅ PASS | `TC-ORD-051__pre-dung-cuoi-form.png` | đứng ở vùng "BUỔI MONG MUỐN" |
| 2 | Nhấn "Tiếp theo" | tap | ✅ PASS | `TC-ORD-051__verify-cuon-len-o-loi-dau-tien.png` | màn **cuộn lên** nhóm "NGƯỜI NHẬN", ô lỗi đầu tiên (email) nằm trong khung nhìn |

**Result: ✅ PASS**

## TC-ORD-059: Check buổi đã trôi qua trong ngày hôm nay bị chặn chọn (FE-303)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Lúc 15:01, Bước 2, "Từ ngày = Hôm nay", chạm "Sáng (8–12h)" | tap chip | ✅ PASS | `TC-ORD-059__verify-buoi-sang-da-qua-khong-chon-duoc.png` | chip Sáng mờ, không được chọn; "Sau giờ làm" vẫn chọn sẵn |

**Result: ✅ PASS** (khớp VR-023 lúc 12:04)

## TC-ORD-083: Check địa chỉ giao trùng hệt địa chỉ lấy bị chặn (FE-301)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Sửa email thành `stag_anhdc4@fpt.com` (autofill Đặng Châu Anh · 0343439724) | — | ✅ PASS | — | ⚠️ lỗi cũ dưới ô tên/SĐT vẫn còn tới lần bấm "Tiếp theo" kế tiếp mới biến mất |
| 2 | Gõ tay "Địa chỉ giao hàng" = `363 Nguyễn Hữu Thọ, Cẩm Lệ` (trùng địa chỉ lấy), **không** chạm gợi ý, rời ô → "Tiếp theo" | appium set_value | ✅ PASS | `TC-ORD-083__verify-loi-dia-chi-go-tay-khong-chon-goi-y.png` | **"Vui lòng chọn địa chỉ giao hàng từ gợi ý — địa chỉ không thuộc hệ thống"** dưới ô; vẫn Bước 2 |

**Result: ✅ PASS**

## TC-ORD-084: Check địa chỉ giao chỉ khác khoảng trắng đầu/cuối bị chặn (FE-301)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Gõ tay `␣␣363 Nguyễn Hữu Thọ, Cẩm Lệ␣␣`, không chạm gợi ý → "Tiếp theo" | appium set_value | ✅ PASS | `TC-ORD-084__verify-loi-dia-chi-co-khoang-trang-go-tay.png` | cùng lỗi "Vui lòng chọn địa chỉ giao hàng từ gợi ý…" |

**Result: ✅ PASS** · biên trim (cả 2 địa chỉ chọn từ gợi ý) vẫn không kiểm được vì gợi ý luôn trả chuỗi chuẩn.

## TC-ORD-043: Check điểm đến trùng điểm xuất phát ở form OFFER bị chặn (FE-301)

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | "Tôi nhận giao hàng": A = B = `FTEL Đà Nẵng Cẩm Lệ` (cùng chạm `address-suggestion-0`), buổi mặc định "Sau giờ làm", tick điều khoản | set_value + tap gợi ý | ✅ PASS | `TC-ORD-043__pre-diem-den-trung-diem-xuat-phat.png` | — |
| 2 | Nhấn "Đăng tin ngay" | tap | ✅ PASS | `TC-ORD-043__verify-loi-diem-den-trung-diem-xuat-phat.png` | **"Điểm đến phải khác điểm xuất phát"** dưới khối Điểm đến; không đăng; thoát form không lưu |

**Result: ✅ PASS**

## FE-330 (không có TC): email người nhận trùng email người gửi

| # | Step | Action | Result | Evidence | Notes |
|---|------|--------|--------|----------|-------|
| 1 | Bước 2, email người nhận = `stag_giangdc2@fpt.com` (chính tài khoản đăng tin), rời ô | adb input text | ✅ PASS | `_recon__fe-330-loi-trung-email-truoc-khi-bam.png` | lỗi **"Email người nhận không được trùng email của bạn"** ngay dưới ô |
| 2 | Chọn địa chỉ giao hợp lệ từ gợi ý (`FPT Cầu Giấy`) để email là lỗi duy nhất, nhấn "Tiếp theo" 2 lần | tap | ✅ PASS | `_recon__fe-330-bam-tiep-theo-van-o-buoc-2.png` | vẫn Bước 2/3, không sang bước 3 ⇒ không thể đăng tin tự gửi cho mình |

**Result: ✅ PASS** · ghi chú: nút "Tiếp theo" hiển thị màu sáng (như enable) dù còn lỗi — bấm không đi tiếp; khác các nhánh khác (nút mờ).

## Setup / môi trường
- Đổi tài khoản `stag_MinhNDN2@` → `stag_giangdc2@` (logout FoxPro → email + OTP).
- Thoát Bước 1 wizard NEED bằng nút ← về thẳng "Đăng tin mới" **không** có popup xác nhận (hành vi của FE-302, ngoài phạm vi phiên này).
