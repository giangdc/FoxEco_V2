# Scope Ledger — VR-001 — module USR — SCOPE_TOTAL = 46 TC

> Seed từ: `coverage-USR.md` (chưa tồn tại trước phiên ⇒ trạng thái trước phiên: có verdict 2/46 — 2 TC DESCOPED `⛔ N-A`)
> Tập chạy phiên này: **pending = 44 TC** (run đầu tiên của module, không có TC nào PASS trước) · Lô 15 TC
> Nguồn kết quả: run này (trừ 2 TC `⛔ N-A` cố định)

| TC ID | Verdict | Lô | Nguồn kết quả | Evidence / Lý do |
|-------|---------|----|---------------|------------------|
| TC-USR-001 | ✅ PASS | 1 | run này | `TC-USR-001__verify-danh-tinh-cbnv.png` |
| TC-USR-002 | ❌ FAIL | 1 | run này | `TC-USR-002__step3-FAIL-avatar-chu-viet-tat-sai.png` |
| TC-USR-003 | ✅ PASS | 1 | run này | `TC-USR-003__verify-khong-sua-truc-tiep.png` |
| TC-USR-004 | ✅ PASS | 1 | run này | `TC-USR-004__verify-dong-dinh-danh.png` |
| TC-USR-005 | ⏳ NOT_RUN | 4 | run này | **Lý do:** cần **3 tài khoản khác nhau** (A đăng tin · B nhận+hoàn tất vận chuyển · C xác nhận đã nhận) ⇒ phải đăng xuất/đăng nhập FoxPro **nhiều lượt, mỗi lượt 1 mã OTP nhập tay** — AI không lấy được OTP (`USR-accounts.md §0`). Cần người chạy hỗ trợ |
| TC-USR-006 | ⏳ NOT_RUN | 4 | run này | **Lý do:** cần đăng nhập tài khoản **BLANK** (`FOXECO_STG_USER_BLANK1`, MNV 00157112) để kiểm 2 chỉ số = 0 ⇒ đổi tài khoản phải đăng xuất FoxPro + **OTP nhập tay**. ⚠️ Phải chạy TRƯỚC khi dùng tài khoản đó vào bất kỳ đơn nào (`USR-accounts.md §3` mục 4) |
| TC-USR-007 | ✅ PASS | 1 | run này | `TC-USR-007__verify-vang-diem-eco-uytin-co2.png` |
| TC-USR-008 | ✅ PASS | 1 | run này | `TC-USR-008__verify-vang-badge-hang-dong-hanh.png` |
| TC-USR-009 | ✅ PASS | 1 | run này | `TC-USR-009__verify-man-don-cua-toi-tab-dang-dien-ra.png` |
| TC-USR-010 | ✅ PASS | 1 | run này | `TC-USR-010__verify-man-qua-da-nhan.png` |
| TC-USR-011 | ❌ FAIL | 1 | run này | `TC-USR-011__step3-FAIL-co-be-mat-cau-hinh-sdt.png` |
| TC-USR-012 | ✅ PASS | 1 | run này | `TC-USR-012__verify-thu-tu-thanh-phan.png` |
| TC-USR-013 | ❌ FAIL | 1 | run này | `TC-USR-013__step3-FAIL-nhan-menu-thu-ba.png` |
| TC-USR-014 | ✅ PASS | 1 | run này | `TC-USR-014__verify-man-cap-nhat-an-bottom-nav.png` |
| TC-USR-015 | ❌ FAIL | 3 | run này | `TC-USR-015__step8-FAIL-khong-co-banner-va-thoat-man.png` |
| TC-USR-016 | ✅ PASS | 3 | run này | `TC-USR-016__verify-gia-tri-persist-sau-mo-lai.png` |
| TC-USR-017 | ❌ FAIL | 2 | run này | `TC-USR-017__step5-FAIL-chuoi-thong-bao-lech.png` |
| TC-USR-018 | ❌ FAIL | 2 | run này | `TC-USR-018__step5-FAIL-chuoi-thong-bao-lech.png` |
| TC-USR-019 | ✅ PASS | 2 | run này | `TC-USR-019__verify-sdt-11-so-khong-luu.png` |
| TC-USR-020 | ❌ FAIL | 2 | run này | `TC-USR-020__step5-FAIL-chuoi-thong-bao-lech.png` |
| TC-USR-021 | ❌ FAIL | 2 | run này | `TC-USR-021__step5-FAIL-khong-hien-thong-bao-loi.png` |
| TC-USR-022 | ❌ FAIL | 2 | run này | `TC-USR-022__step5-FAIL-khong-hien-thong-bao-loi.png` |
| TC-USR-023 | ❌ FAIL | 2 | run này | `TC-USR-023__step5-FAIL-chuoi-thong-bao-lech.png` |
| TC-USR-024 | ❌ FAIL | 1 | run này | `TC-USR-024__step8-FAIL-thieu-icon-khien-email.png` |
| TC-USR-025 | ✅ PASS | 4 | run này | `TC-USR-025__verify-don-giu-nguyen-sau-doi-ho-so.png` |
| TC-USR-026 | ✅ PASS | 4 | run này | `TC-USR-026__verify-ho-so-khong-bi-don-ghi-de.png` |
| TC-USR-027 | 🚫 BLOCKED | 3 | run này | `TC-USR-027__step6-BLOCKED-khong-co-banner-de-kiem.png` |
| TC-USR-028 | ❌ FAIL | 3 | run này | `TC-USR-028__step6-FAIL-khong-xoa-rong-khi-roi-field.png` |
| TC-USR-029 | ❌ FAIL | 3 | run này | `TC-USR-029__step7-FAIL-khong-co-banner-xanh.png` |
| TC-USR-030 | ❌ FAIL | 3 | run này | `TC-USR-030__step10-FAIL-khong-rong-giu-text-go-tay.png` |
| TC-USR-031 | ✅ PASS | 3 | run này | `TC-USR-031__verify-2-ky-tu-khong-goi-y.png` |
| TC-USR-032 | 🚫 BLOCKED | 3 | run này | `TC-USR-032__step5-FAIL-danh-sach-goi-y-lech.png` |
| TC-USR-033 | ✅ PASS | 3 | run này | `TC-USR-033__verify-chon-goi-y-dien-dung-ten-vp.png` |
| TC-USR-034 | 🚫 BLOCKED | 3 | run này | `TC-USR-034__step5-BLOCKED-oracle-ten-vp-lech-stg.png` |
| TC-USR-035 | 🚫 BLOCKED | 3 | run này | `TC-USR-035__step5-BLOCKED-oracle-ten-vp-lech-stg.png` |
| TC-USR-036 | 🚫 BLOCKED | 3 | run này | `TC-USR-036__step5-BLOCKED-oracle-ten-vp-lech-stg.png` |
| TC-USR-037 | 🚫 BLOCKED | 3 | run này | `TC-USR-037__step5-BLOCKED-oracle-2-vp-khong-ton-tai.png` |
| TC-USR-038 | ✅ PASS | 3 | run này | `TC-USR-038__verify-tu-khoa-khong-khop.png` |
| TC-USR-039 | ❌ FAIL | 3 | run này | `TC-USR-039__step5-FAIL-tim-theo-ma-tinh.png` |
| TC-USR-040 | ⏳ NOT_RUN | 4 | run này | **Lý do:** cần đăng nhập **vai C** (`FOXECO_STG_USER_C`, MNV 00041796 — chưa từng lưu hồ sơ) ⇒ **OTP nhập tay**. 🔴 Ưu tiên cao: phiên này phát hiện tài khoản A **KHÔNG được prefill** SĐT/địa chỉ từ HRIS dù HRIS có đủ — nếu C cũng vậy thì TC-USR-040 FAIL và là bug thật. Chạy C **trước mọi lần bấm Lưu** trên C |
| TC-USR-041 | ⛔ N-A | — | — | DESCOPED 2026-09-18 (fragment §0.1) — nhánh HRIS trống địa chỉ không xảy ra, không seed được data |
| TC-USR-042 | ✅ PASS | 3 | run này | `TC-USR-042__verify-persist-sau-mo-lai-app.png` |
| TC-USR-043 | ⏳ NOT_RUN | 4 | run này | **Lý do:** cần đăng nhập **vai C** (OTP nhập tay) — gom cùng phiên với TC-USR-040. 🕐 Thêm rào thời điểm: SĐT HRIS mới đổi 18/09, chỉ đồng bộ **sau 18/09** ⇒ chạy **từ 19/09**; chạy đúng 18/09 mà lệch thì ghi BLOCKED, ⛔ không log bug (`USR-accounts.md §2`) |
| TC-USR-044 | ⛔ N-A | — | — | DESCOPED 2026-09-18 (fragment §0.1) — nhánh HRIS trống SĐT không xảy ra; vế "Lưu bị chặn" đã phủ bởi TC-USR-017 |
| TC-USR-045 | ✅ PASS | 3 | run này | `TC-USR-045__verify-quay-lai-khong-hop-thoai.png` |
| TC-USR-046 | ✅ PASS | 3 | run này | `TC-USR-046__verify-bo-thay-doi-khong-giu-ban-nhap.png` |

## Tổng kết phiên VR-001

| | Count |
|---|--:|
| TC **chạy trong phiên này** | **40** |
| ✅ PASS | 19 |
| ❌ FAIL | 15 |
| 🚫 BLOCKED | 6 |
| ⛔ N-A (không chạy, cố ý) | 2 |
| ⏳ NOT_RUN (còn nợ) | 4 |
| **SCOPE_TOTAL** | **46** |

**Lô đã chạy:** 4 lô — lô 1 màn Cá nhân + điều hướng (13 TC) · lô 2 validation SĐT (7 TC) ·
lô 3 gợi ý địa chỉ + lưu/persist (18 TC) · lô 4 ranh giới hồ sơ⟷đơn qua wizard ORD (2 TC).

**4 TC còn nợ — TẤT CẢ cùng 1 blocker duy nhất: cần đăng nhập tài khoản khác + OTP nhập tay.**
| TC | Tài khoản cần | Ghi chú |
|---|---|---|
| TC-USR-040 · TC-USR-043 | **vai C** (`FOXECO_STG_USER_C`, MNV 00041796) | gom **cùng 1 phiên**; chạy **trước mọi lần bấm Lưu** trên C; `043` chờ **từ 19/09** |
| `TC-USR-006` | **BLANK** (`FOXECO_STG_USER_BLANK1`, MNV 00157112) | chạy trước khi dùng tài khoản đó vào đơn nào |
| `TC-USR-005` | **A + B + C** (3 lượt đăng nhập) | cần hoàn tất 1 đơn end-to-end |
