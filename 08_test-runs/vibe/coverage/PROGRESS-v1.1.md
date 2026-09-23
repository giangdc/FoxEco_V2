# Tiến độ vibe-test — CHỈ TC v1.1 (dẫn xuất, không thay sổ coverage)

> 🔁 File **sinh tự động** từ `03_test-cases/v1.1/TC-MASTER-v1.1.xlsx` (sheet `ALL`, cột `Status`) — cột này vừa được đồng bộ từ `coverage/coverage-<MOD>.md`. **Sổ coverage từng module vẫn giữ nguyên mẫu số cũ** (gồm TC v1.0 CARRIED) để gate `verify_evidence.py` và `§10.5` không lệch; file này chỉ là **lát cắt v1.1**.
> Phạm vi = **toàn bộ TC của TC-MASTER v1.1** (`NEW` + `MODIFIED`), trừ `DESCOPED`. **⛔ KHÔNG gồm** TC v1.0 CARRIED (nằm ở `TC-MASTER-v1.0`).
> Cập nhật: **2026-09-23** — thêm `TC-GIFT-008` ✅ PASS (VR-028). ⚠️ Kết quả retest R2 của VR-023..027 **chưa** dồn vào đây (các phiên đó ghi rõ không cập nhật TC-MASTER/coverage). Lần trước: **2026-09-22** — sinh lại sau khi đồng bộ Status TC-MASTER ← coverage ledger. Bản trước (cũng ghi 2026-09-22) **bỏ sót VR-020/VR-021 (DLV)**: 4 TC `TC-DLV-041/042/043/050` đã PASS mà bảng vẫn đếm là chưa chạy.

## Tổng quan

**164/221 TC v1.1 có verdict cuối = 74.2%** · ✅ PASS **102** (46.2%) · ❌ FAIL 37 · 🚫 BLOCKED 20 · ⛔ N-A 5 · ⏳ chưa có verdict **57** (25.8%)

| Module | TC v1.1 | ✅ PASS | ❌ FAIL | 🚫 BLOCKED | ⛔ N-A | ⏳ Chưa xong | **% có verdict** | % PASS | Sổ coverage |
|---|--:|--:|--:|--:|--:|--:|--:|--:|---|
| **ACT** | 10 | 6 | 2 | 2 | 0 | 0 | **100%** | 60% | ✅ có |
| **ASN** | 13 | 10 | 0 | 3 | 0 | 0 | **100%** | 77% | ✅ có |
| **CNL** | 13 | 9 | 2 | 2 | 0 | 0 | **100%** | 69% | ✅ có |
| **DLV** | 51 | 5 | 2 | 0 | 4 | 40 | **22%** | 10% | ✅ có |
| **FEED** | 5 | 4 | 0 | 1 | 0 | 0 | **100%** | 80% | ✅ có |
| **GIFT** | 8 | 4 | 1 | 2 | 0 | 1 | **88%** | 50% | ✅ có |
| **HOME** | 11 | 3 | 2 | 1 | 1 | 4 | **64%** | 27% | ✅ có |
| **NTF** | 9 | 0 | 0 | 0 | 0 | 9 | **0%** | 0% | ❌ chưa có (chưa vibe-test) |
| **ORD** | 48 | 34 | 8 | 3 | 0 | 3 | **94%** | 71% | ✅ có |
| **TS** | 17 | 11 | 5 | 1 | 0 | 0 | **100%** | 65% | ✅ có |
| **USR** | 36 | 16 | 15 | 5 | 0 | 0 | **100%** | 44% | ✅ có |
| **Σ** | **221** | **102** | 37 | 20 | 5 | **57** | **74.2%** | 46.2% | |

> `DESCOPED` (loại khỏi mẫu số): TC-USR-041, TC-USR-044.

## TC v1.1 chưa xong theo module (⏳ chưa chạy · ❌ FAIL · 🚫 BLOCKED · ⛔ N-A)

- **ACT** — chưa chạy 0: — · FAIL/BLOCKED/N-A: 005🚫 012❌ 015🚫 008❌
- **ASN** — chưa chạy 0: — · FAIL/BLOCKED/N-A: 024🚫 008🚫 026🚫
- **CNL** — chưa chạy 0: — · FAIL/BLOCKED/N-A: 004❌ 009❌ 020🚫 021🚫
- **DLV** — chưa chạy 40: 044 064 065 031 032 033 034 035 036 040 045 046 047 048 049 051 052 058 059 060 061 062 063 066 069 070 071 072 073 037 038 039 053 054 055 056 057 067 077 079 · FAIL/BLOCKED/N-A: 074⛔ 075⛔ 076⛔ 078⛔ 080❌ 081❌
- **FEED** — chưa chạy 0: — · FAIL/BLOCKED/N-A: 013🚫
- **GIFT** — chưa chạy 1: 011 · FAIL/BLOCKED/N-A: 003❌ 013🚫 014🚫
- **HOME** — chưa chạy 4: 008 031 029 030 · FAIL/BLOCKED/N-A: 032⛔ 025❌ 027❌ 028🚫
- **NTF** — chưa chạy 9: 008 005 014 017 018 019 020 021 022 · FAIL/BLOCKED/N-A: —
- **ORD** — chưa chạy 3: 067 080 082 · FAIL/BLOCKED/N-A: 063❌ 074❌ 053❌ 058❌ 059❌ 064❌ 066❌ 069🚫 077❌ 084🚫 086🚫
- **TS** — chưa chạy 0: — · FAIL/BLOCKED/N-A: 009❌ 012❌ 016❌ 017🚫 013❌ 021❌
- **USR** — chưa chạy 0: — · FAIL/BLOCKED/N-A: 002❌ 013❌ 017❌ 018❌ 020❌ 021❌ 022❌ 023❌ 024❌ 028❌ 029❌ 030❌ 032🚫 034🚫 035🚫 036🚫 037🚫 039❌ 040❌ 043❌

## Cách dùng
- Lệnh chạy phần còn nợ của 1 module chỉ v1.1: `/vibe-test --module <MOD> --tc <danh sách ID ở trên>` *(skill chưa có cờ lọc version)*.
- Sinh lại file này sau mỗi phiên: đồng bộ `coverage-<MOD>.md` → cột `Status` của TC-MASTER, rồi dựng lại bảng từ sheet `ALL`.
