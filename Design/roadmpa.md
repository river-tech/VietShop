# DESIGN ROADMAP – 28 DAYS
## Project: Customer App / Seller App / Admin App

---

## 1. TEAM STRUCTURE

- **Design Lead / PM (You)**
  - Quyết định cuối cùng
  - Quản lý design system & UX rule
  - Review & approve tất cả output

- **Designer Chính (D1)**
  - Làm phần phức tạp, logic cao
  - Screen & component rủi ro

- **Designer Phụ (D2)**
  - Làm phần đơn giản, lặp lại
  - Không tạo rule mới

> Cả 2 designer làm song song, **dưới sự kiểm soát của Lead**.

---

## 2. ROADMAP THEO NGÀY (TOTAL 28 DAYS)

---

## 🔵 PHASE 1 – FOUNDATION & CORE RULE  
**⏱ 3 NGÀY (DAY 1–3)**

### Mục tiêu
Khóa toàn bộ design system trước khi scale.

### Scope
- Design Tokens (Color, Spacing, Radius, Typography)
- Core component:
  - Button
  - Input
  - Card
  - List item
  - Status / Badge
- Quy định:
  - Spacing scale
  - Typography usage
  - Color usage

### Phân công
- **D1**: Build foundation & core component
- **D2**: Audit + document (không làm screen)
- **Lead**: Review & lock system

### Output
- Design system v1 (LOCKED)
- Không đổi rule ở phase sau

---

## 🟢 PHASE 2 – COMPONENT & VARIANT  
**⏱ 5 NGÀY (DAY 4–8)**

### Mục tiêu
Đủ component để ráp toàn bộ screen.

### Scope
- Variant & state:
  - Loading / Disabled
  - Error / Helper
- Component nâng cao:
  - Dialog
  - Bottom sheet
  - Toast
  - Empty state
  - Filter / Search

### Phân công
- **D1 (phức tạp)**:
  - Checkout-related component
  - Order / Wallet / Refund component
- **D2 (đơn giản)**:
  - Empty state
  - Notification item
  - Setting row
  - Simple list item

### Luật
- Không tạo component ngoài scope
- Không thay đổi token & rule

### Output
- Component library hoàn chỉnh (~80%)

---

## 🟡 PHASE 3 – SCREEN DESIGN (CORE PHASE)  
**⏱ 14 NGÀY (DAY 9–22)**

> Đây là phase **lớn nhất & quan trọng nhất**

### Mục tiêu
Hoàn thiện toàn bộ screen cho:
- Customer App
- Seller App
- Admin App

### Phân công

#### D1 – Screen phức tạp
- Checkout flow
- Order detail
- Refund / Dispute
- Wallet flow
- Product detail
- Admin: Dispute, Finance, Settings

#### D2 – Screen đơn giản
- List screen
- Profile
- Notification
- Chat list
- Wishlist
- Category

### Luật
- Chỉ dùng component đã có
- Không tự ý thêm UX mới
- Mọi thay đổi phải qua Lead

### Output
- Screen đầy đủ
- Flow logic end-to-end

---

## 🔴 PHASE 4 – QA, POLISH & HANDOFF  
**⏱ 6 NGÀY (DAY 23–28)**

### Mục tiêu
Chuẩn bị cho dev, không còn nợ design.

### Scope
- QA consistency
- Fix spacing / typography
- Edge case:
  - Empty
  - Error
  - Loading
- Cross-app consistency (Customer / Seller / Admin)

### Phân công
- **D1 + D2**: Fix theo checklist
- **Lead**: Final approve & lock file

### Output
- Design ready for development
- File sạch, dễ handoff

---

## 3. TỔNG KẾT

| Phase | Days |
|------|------|
| Phase 1 | 3 |
| Phase 2 | 5 |
| Phase 3 | 14 |
| Phase 4 | 6 |
| **TOTAL** | **28 DAYS** |

---

Task chi tiết sẽ được chia sau khi Phase 1 kết thúc.