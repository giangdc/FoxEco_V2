# Scope Ledger — VR-017 — module ACT — SCOPE_TOTAL = 18 TC

> Seed từ: `coverage/coverage-ACT.md` — **chưa tồn tại trước phiên** ⇒ tạo mới (trạng thái trước phiên: có verdict 0/18).
> Tập chạy phiên này: **10 TC v1.1** theo yêu cầu QC (*"chỉ test các case của version 1.1"*) · 1 lô · 3 tài khoản.
> 8 TC CARRIED v1.0 giữ `⏳ NOT_RUN` — ngoài phạm vi yêu cầu.

| TC ID | Verdict | Lô | Nguồn kết quả | Evidence / Lý do |
|-------|---------|----|---------------|------------------|
| TC-ACT-001 | ✅ PASS | 1 (`anhdc4`) | run này | `TC-ACT-001__verify-nhan-hoat-dong-don-cua-toi-2-tab.png` |
| TC-ACT-002 | ⏳ NOT_RUN | — | — | CARRIED v1.0 — ngoài phạm vi |
| TC-ACT-003 | ⏳ NOT_RUN | — | — | CARRIED v1.0 — ngoài phạm vi |
| TC-ACT-004 | ⏳ NOT_RUN | — | — | CARRIED v1.0 — ngoài phạm vi |
| TC-ACT-005 | 🚫 BLOCKED | 1 (`anhdc4`) | run này | `TC-ACT-005__step3-BLOCKED-chi-co-hoan-thanh-va-het-han-khong-co-don-tra-lai.png` |
| TC-ACT-006 | ⏳ NOT_RUN | — | — | CARRIED v1.0 — ngoài phạm vi |
| TC-ACT-007 | ⏳ NOT_RUN | — | — | CARRIED v1.0 — ngoài phạm vi |
| TC-ACT-008 | ❌ FAIL | 1 (`anhdc4`) | run này | `TC-ACT-008__step2-FAIL-ly-do-het-han-ban-dai-tin-da-tu-dong-dong.png` · `TC-ACT-008__verify-chuoi-ly-do-het-han-mcp-element.png` |
| TC-ACT-009 | ⏳ NOT_RUN | — | — | CARRIED v1.0 — ngoài phạm vi |
| TC-ACT-010 | ⏳ NOT_RUN | — | — | CARRIED v1.0 — ngoài phạm vi |
| TC-ACT-011 | ⏳ NOT_RUN | — | — | CARRIED v1.0 — ngoài phạm vi |
| TC-ACT-012 | ❌ FAIL | 1 (`MinhNDN2`) | run này | `TC-ACT-012__step3-FAIL-thieu-dong-giai-thich-duoi-tieu-de.png` |
| TC-ACT-013 | ✅ PASS | 1 (`anhdc4`) | run này | `TC-ACT-013__verify-card-hoan-thanh-cuoi-danh-sach-khong-sao-diem-tier.png` |
| TC-ACT-014 | ✅ PASS | 1 (`thuyntt22`) | run này | `TC-ACT-014__verify-chua-co-don-hoan-tat-khong-cta-khong-khoi-lich-su.png` |
| TC-ACT-015 | 🚫 BLOCKED | 1 (`anhdc4`) | run này — chấm lại theo Expected mới | `TC-ACT-015__step4-BLOCKED-tab-da-hoan-thanh-khong-co-don-tra-lai-nguoi-gui.png` · `TC-ACT-015__pre-don-da-huy-o-tab-dang-dien-ra.png` *(lượt đầu FAIL, QC chốt không phải bug)* |
| TC-ACT-016 | ✅ PASS | 1 (`MinhNDN2`) | run này | `TC-ACT-016__verify-tab-da-hoan-thanh-rong-thanh-tab-duoi-du-5-muc.png` |
| TC-ACT-017 | ✅ PASS | 1 (`MinhNDN2`) | run này — chấm lại theo Expected mới | `TC-ACT-017__verify-tab-da-hoan-thanh-vuot-man-dung-yen-khong-treo.png` · `TC-ACT-017__pre-tab-dang-dien-ra-giua-thao-tac-vuot-len.png` *(lượt đầu FAIL, QC chốt app đúng)* |
| TC-ACT-018 | ✅ PASS | 1 (`MinhNDN2`) | run này | `TC-ACT-018__verify-tab-da-hoan-thanh-chuyen-han-empty-state-sau-tai.png` (+ 3 ảnh `__pre`) |

**Lô 1 xong · đã chạy 10/10 TC v1.1 · module: 10/18 có verdict, còn nợ 8 (CARRIED).**
