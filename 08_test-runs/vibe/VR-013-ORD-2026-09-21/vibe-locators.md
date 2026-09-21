# Vibe Locators — VR-013 — 2026-09-21
> Captured via Appium MCP (EMU 1080×2400 + REAL 720×1600). Mark: ✅ Verified (MCP find + action OK trong run này) · 🚫 NOT FOUND. MCP session log: `mcp-session-log.md` (dòng `A1/A2` + nhóm TC ở Pha B).

## 🪤 Bẫy MỚI (T22–T29)
| # | Bẫy | Cách làm đúng |
|---|---|---|
| **T22** | Lỗi ảnh `Ảnh vượt quá 5MB…` nằm **dưới khối ảnh, bị thanh nút cố định che** ⇒ `find textContains("5MB")` NOT FOUND ở viewport mặc định | cuộn 1 nhịp trước khi kết luận "không có thông báo" (nguyên nhân dương tính giả của `BUG-019`) |
| **T23** | Lightbox ảnh **không đóng khi chạm nền tối** (6 điểm, 2 thiết bị); chỉ nút × | đóng bằng tap `(//android.view.ViewGroup[@clickable="true"])[1]` hoặc toạ độ nút × |
| **T24** | `appium_get_page_source` **trả inline** khi cây nhỏ (~18k ký tự) | màn nhỏ dùng `find_element`; chỉ dump màn lớn (tự ghi file) |
| **T25** | `feed-post-card-N` resolve bằng `accessibility id`, **không** bằng `resourceId`; `activity-order-card-N` đôi khi NOT FOUND (T2) | fallback `descriptionStartsWith("Gửi: Tài liệu \| Giá trị thấp, Chờ ghép")` |
| **T26** | Tap nhãn/tiêu đề **không chắc làm ô mất focus** | rời ô bằng cách **tap 1 EditText khác** |
| **T27** | Photo Picker: `content-desc` chứa **timestamp** ảnh ⇒ đặt mtime riêng (`touch -t`) rồi chọn bằng `descriptionContains("11:10:02")` — chắc hơn `.instance(N)` | quét media: `am broadcast MEDIA_SCANNER_SCAN_FILE` |
| **T28** | Long-press ảnh trong form sửa **mở lightbox**, không có menu xoá; nút xoá là `multi-photo-remove-N` (**có cả ở tin đã đăng**) | — |
| **T29** | `tap` bằng `elementUUID` cũ (màn đã đổi) vẫn báo *success* | luôn find lại sau khi đổi màn |

## Màn: FoxPro đăng nhập/đăng xuất (re-verify)
| Element | Action | Strategy | Value | Verified | TC refs |
|---|---|---|---|---|---|
| Tab `Cá nhân` → `Đăng xuất` → `Đồng ý` | tap / scroll_to_element | -android uiautomator | `text("Cá nhân")` · `text("Đăng xuất")` · `text("Đồng ý")` | ✅ | (setup) |
| Email / gửi OTP / đăng nhập | set_value / tap | -android uiautomator | `text("Nhập email đăng nhập")` · `text("NHẬN MÃ OTP")` · `text("ĐĂNG NHẬP")` | ✅ | (setup) |
| Vào FoxEco | scroll_to_element / tap | -android uiautomator | `text("Chức năng")` → `text("FoxEco")` | ✅ | (setup) |

## Màn: Wizard Bước 1 — nâng ⚠️ Inferred → ✅
| Element | Action | Strategy | Value | Verified | TC refs |
|---|---|---|---|---|---|
| Chip giá trị / trọng lượng / kích thước | tap | -android uiautomator | `resourceId("value-tier-chip-option-low")` · `("weight-tier-chip-option-light")` · `("weight-tier-chip-option-heavy")` · `("size-tier-chip-option-small")` · `("size-tier-chip-option-large")` | ✅ | 004 038 065 067* |
| Nút thêm ảnh / xoá ảnh N | tap | -android uiautomator | `resourceId("multi-photo-add-button")` · `resourceId("multi-photo-remove-0")` | ✅ | 004 068 088 |
| Bộ đếm ảnh | find | accessibility id | `0/5` · `1/5` · `4/5` | ✅ | 068 088 |
| Lỗi ảnh quá 5MB | get_text | -android uiautomator | `textContains("5MB")` → `Ảnh vượt quá 5MB, vui lòng chọn ảnh nhỏ hơn.` | ✅ *(sau khi cuộn)* | 068 |
| Photo Picker theo timestamp | tap | -android uiautomator | `descriptionContains("11:10:02")` | ✅ | 068 |

## Màn: Wizard Bước 2
| Element | Action | Strategy | Value | Verified | TC refs |
|---|---|---|---|---|---|
| Tên / SĐT người nhận | set_value | -android uiautomator | `resourceId("receiver-name-input")` · `("receiver-phone-input")` | ✅ | 052 083 084 |
| Địa chỉ lấy / giao | set_value | xpath | `//android.widget.EditText[@hint="Địa chỉ lấy hàng"]` · `[@hint="Địa chỉ giao hàng"]` | ✅ | 004 083 084 |
| Gợi ý địa chỉ | tap | accessibility id | `address-suggestion-0` · `address-suggestion-1` | ✅ | 004 046 045 |
| Lỗi trùng địa chỉ | find | -android uiautomator | `text("Địa chỉ giao phải khác địa chỉ lấy hàng")` | ✅ *(chỉ hiện sau khi bấm `Tiếp theo` đã enable)* | 083 |
| Khối uỷ quyền | tap / set_value | -android uiautomator | `descriptionStartsWith("Thêm người nhận uỷ quyền")` · `resourceId("alt-receiver-name-input")` · `("alt-receiver-phone-input")` | ✅ | 080 |
| Ngày / buổi | tap | -android uiautomator | `descriptionStartsWith("Đến ngày")` · `text("22")` · `descriptionStartsWith("Chiều")` · `descriptionStartsWith("Giờ nào cũng được")` | ✅ | 004 038 |

## Màn: Thành công / Theo dõi đơn / Sửa tin
| Element | Action | Strategy | Value | Verified | TC refs |
|---|---|---|---|---|---|
| 2 nút màn thành công | tap | accessibility id | `Theo dõi đơn` · `Về trang chủ` | ✅ | 039 040 |
| Nút Chỉnh sửa / Huỷ đơn / Báo cáo sự cố | tap | -android uiautomator | `resourceId("track-edit-post")` · `("track-cancel-post")` · `("track-report-incident")` | ✅ *(2 nút đầu tap được ở tin `Chờ ghép`)* | 046 060 088 |
| Icon copy địa chỉ giao | tap | -android uiautomator | `description("Copy").instance(1)` | ✅ | 085 |
| Ảnh sản phẩm (carousel) | swipe / tap | -android uiautomator | `descriptionStartsWith("Xem ảnh")` · badge `text("2/5")` | ✅ | 072 073 |
| Nút × lightbox | tap | xpath | `(//android.view.ViewGroup[@clickable="true"])[1]` | ✅ | 073 |
| Nút huỷ sửa (theo bước N) + xác nhận | tap | accessibility id | `Huỷ chỉnh sửa` (`post-n1/n2/n3-cancel-edit`) · `dialog-confirm-button` · `Cập nhật đơn` | ✅ | 060 046 |
| Popup lưu | tap | -android uiautomator | `text("Đồng ý")` sau `Đã lưu — Đã cập nhật tin đăng.` | ✅ | 046 |

## Màn: Hoạt động / Bảng tin / OFFER
| Element | Action | Strategy | Value | Verified | TC refs |
|---|---|---|---|---|---|
| Card đơn (đang diễn ra) | tap | -android uiautomator | `descriptionStartsWith("Gửi: Tài liệu \| Giá trị thấp, Chờ ghép")` | ✅ | 004 060 |
| Card `Đã hoàn thành` | find | resource-id | `completed-card-#ECO-2026-NNNN` · badge `text("Hết hạn")` | ✅ | 048 |
| Card Bảng tin | tap | accessibility id | `feed-post-card-0` | ✅ | 048 045 080 |
| Chip buổi OFFER | tap | -android uiautomator | `resourceId("offer-day-part-anytime")` | ✅ | 045 |
| Ô OFFER | set_value | xpath | `//android.widget.EditText[@hint="Bạn đang ở đâu / xuất phát từ đâu"]` · `[@hint="Bạn sẽ đến đâu"]` | ✅ | 045 |

## 🚫 NOT FOUND (đúng kỳ vọng / ghi nhận)
`textContains("Xoá")` sau long-press ảnh (không có menu xoá) · ô tìm kiếm + tab con ở Bảng tin (không tồn tại) · khối uỷ quyền trên màn chủ tin (`Bảy`/`chỉ định` — 0) · nút `Tôi mang giúp được` khi B là người nhận · `textContains("phải khác")` ở đường gõ tay · lỗi trùng địa chỉ trước khi bấm `Tiếp theo`.
