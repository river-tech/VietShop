## VietShop – System Screen & Flow Overview

Tài liệu này mô tả **toàn bộ hệ thống màn hình** và **user flow chính** cho VietShop dựa trên `ui.pdf`, phân tách theo 3 role: **Customer**, **Seller**, **Admin**, kèm **cross-role flow** (Order, Return/Refund, Shipping).

---

## 1. Role: Customer (CUS_*)

### 1.1. Authentication
- **CUS_SCR_001**: Onboarding
- **CUS_SCR_002**: Login
- **CUS_SCR_003**: Register
- **CUS_SCR_004**: Forgot Password
- **CUS_SCR_010**: Auth Verification (OTP / Email / 2FA)

**Flow chính:**
- Onboarding → Login → (Register / Forgot Password / Verification) → Customer Entry.

### 1.2. Customer Entry & Navigation
- **Customer Entry** (node không ID): entry point sau khi login.
- Từ Customer Entry, user có thể truy cập:
  - Category Home
  - Wallet
  - Chat
  - Notification
  - Profile

### 1.3. Product & Category
- **CUS_SCR_053**: Category Home
- **CUS_SCR_054**: Subcategory Listing
- **CUS_SCR_055**: Category Filter & Sort
- **CUS_SCR_007**: Product Details
- **CUS_SCR_041**: Shop Page
- **CUS_SCR_035**: Wishlist

**Flow chính:**
- Customer Entry → Category Home → Subcategory Listing → (Filter & Sort) → Product Details → Shop Page.
- Product Details ↔ Wishlist (Add/Remove).

### 1.4. Cart, Checkout & Order
- **CUS_SCR_008**: Cart
- **CUS_SCR_009**: Checkout
- **CUS_SCR_045**: Order Result
- **CUS_SCR_030**: Order History
- **CUS_SCR_031**: Order Details
- **CUS_SCR_046**: Return/Refund Request

**Flow mua hàng:**
1. Product Details → **CUS_SCR_008 (Cart)**  
2. Cart → **CUS_SCR_009 (Checkout)**  
3. Checkout (chọn phương thức thanh toán, có thể chọn Wallet) → **CUS_SCR_045 (Order Result)**  
4. Order Result → **CUS_SCR_030 (Order History)**  
5. Order History → **CUS_SCR_031 (Order Details)**  
6. Order Details → **CUS_SCR_046 (Return/Refund Request)** (nếu cần).

### 1.5. Review
- **CUS_SCR_037**: Write Review
- **CUS_SCR_039**: Edit Review
- **CUS_SCR_040**: Review List

**Flow:**
- Từ **Order Details (CUS_SCR_031)** → Write Review (037) → Review List (040) → Edit Review (039).

### 1.6. Wallet
- **CUS_SCR_012**: Wallet Overview
- **CUS_SCR_013**: Deposit Wallet
- **CUS_SCR_014**: Withdraw Wallet
- **CUS_SCR_015**: Wallet History
- **CUS_SCR_048**: Wallet Promotions
- **CUS_SCR_050**: Top-up Methods
- **CUS_SCR_051**: Linked Bank Accounts
- **CUS_SCR_052**: Wallet Settings

**Flow & tích hợp checkout:**
- Customer Entry → Wallet Overview (012).
- Wallet Overview →
  - Deposit (013)
  - Withdraw (014)
  - Wallet History (015)
  - Promotions (048)
  - Top-up Methods (050)
  - Linked Banks (051)
  - Wallet Settings (052)
- Checkout (CUS_SCR_009) → chọn Wallet Payment → Wallet Overview (012).

### 1.7. Chat
- **CUS_SCR_056**: Chat List
- **CUS_SCR_057**: Chat Detail
- **CUS_SCR_058**: Chat from Product

**Flow:**
- Customer Entry → Chat List (056) → Chat Detail (057).
- Từ Product Details (007) → Chat from Product (058).

### 1.8. Notification
- **CUS_SCR_059**: Notification Center
- **CUS_SCR_060**: Notification Detail
- **CUS_SCR_061**: Notification Settings

**Flow:**
- Customer Entry → Notification Center (059) → (Detail 060 / Settings 061).

### 1.9. Profile
- **CUS_SCR_062**: Profile Overview
- **CUS_SCR_063**: Edit Profile
- **CUS_SCR_064**: Address Management
- **CUS_SCR_065**: Security Settings
- **CUS_SCR_066**: Preferences

**Flow chính & shortcut:**
- Customer Entry → Profile Overview (062).
- Profile Overview → (Edit Profile 063 / Address 064 / Security 065 / Preferences 066).
- Từ Profile Overview:
  - Tới Wallet Overview (012)
  - Tới Order History (030)
  - Tới Notification Center (059)
  - Switch sang Seller Entry.

---

## 2. Role: Seller (SEL_*)

### 2.1. Seller Entry
- **Seller Entry** (node không ID):
  - Điểm vào chính cho tất cả module Seller (sau khi login / chuyển role).
  - Từ Customer Profile Overview (CUS_SCR_062) có thể **switch role** sang Seller Entry.

### 2.2. Product & Inventory
- **SEL_SCR_007**: Inventory Management (alias node: `SEL_SCR_007_INVENTORY`)
- **SEL_SCR_030**: Add Product – Basic Info (alias: `SEL_SCR_030_ADD_BASIC`)
- **SEL_SCR_031**: Add Product – Sales Info (alias: `SEL_SCR_031_ADD_SALES`)
- **SEL_SCR_032**: Edit Product (alias: `SEL_SCR_032_EDIT_PRODUCT`)
- **SEL_SCR_023**: Voucher Management (alias: `SEL_SCR_023_VOUCHER`)
- **SEL_SCR_025**: Product Review Management (alias: `SEL_SCR_025_REVIEW`)

**Flow Add Product:**
1. Seller Entry → **Inventory Management (007)**  
2. Inventory → **Add Product – Basic Info (030)**  
3. Basic Info → **Add Product – Sales Info (031)**  
4. Sales Info → quay lại **Inventory (007)**.

**Luồng khác từ Inventory:**
- Inventory → Edit Product (032).
- Inventory → Voucher Management (023).
- Inventory → Product Review Management (025_REVIEW).

### 2.3. Order & Return/Refund
- **SEL_SCR_009**: Order List
- **SEL_SCR_010**: Order Details
- **SEL_SCR_011**: Order Processing
- **SEL_SCR_026**: Return/Refund List (alias: `SEL_SCR_026_RETURN`)
- **SEL_SCR_027**: Return/Refund Details (alias: `SEL_SCR_027_RETURN`)

**Flow Order:**
- Seller Entry → Order List (009) → Order Details (010) → Order Processing (011).

**Flow Refund:**
- Order Details (010) → Return/Refund List (026_RETURN) → Return/Refund Details (027_RETURN).

### 2.4. Notification
- **SEL_SCR_028**: Seller Notifications (alias: `SEL_SCR_028_NOTI`)
- **SEL_SCR_029**: Notification Settings (alias: `SEL_SCR_029_NOTI_SETTING`)

**Flow:**
- Seller Entry → Seller Notifications (028) → Notification Settings (029).

### 2.5. Settings
- **SEL_SCR_020**: Incident Report (alias: `SEL_SCR_020_INCIDENT`)
- **SEL_SCR_021**: Seller Profile (alias: `SEL_SCR_021_PROFILE`)
- **SEL_SCR_022**: Shop Settings (alias: `SEL_SCR_022_SHOP_SETTINGS`)

**Flow:**
- Seller Entry → Seller Profile (021) → (Incident Report 020 / Shop Settings 022).

### 2.6. Chat (disambiguate ID 025/026/027)
- **SEL_SCR_025**: Seller Chat List (alias: `SEL_SCR_025_CHAT`)
- **SEL_SCR_026**: Seller Chat Detail (alias: `SEL_SCR_026_CHAT`)
- **SEL_SCR_027**: Chat From Product (alias: `SEL_SCR_027_CHAT`)

**Flow:**
- Seller Entry → Seller Chat List (025_CHAT) → Seller Chat Detail (026_CHAT).
- Từ Edit Product (032_EDIT_PRODUCT) → Chat From Product (027_CHAT).

### 2.7. Wallet
- **SEL_SCR_030**: Seller Wallet Overview (alias: `SEL_SCR_030_WALLET`)
- **SEL_SCR_031**: Payout History (alias: `SEL_SCR_031_PAYOUT`)
- **SEL_SCR_032**: Withdraw Request (alias: `SEL_SCR_032_WITHDRAW`)

**Flow:**
- Seller Entry → Wallet Overview (030_WALLET).
- Wallet Overview → Payout History (031_PAYOUT).
- Wallet Overview → Withdraw Request (032_WITHDRAW).

---

## 3. Role: Admin (ADM_*)

### 3.1. Authentication & Dashboard
- **ADM_SCR_001**: Admin Login
- **ADM_SCR_002**: Admin Dashboard

Dashboard là hub điều hướng tới tất cả các module Admin.

### 3.2. User Management
- **ADM_SCR_003**: User Management
- **ADM_SCR_034**: User Details

**Flow:**
- Dashboard → User Management (003) → User Details (034).
- User Details hiển thị: hồ sơ cá nhân, trạng thái tài khoản, lịch sử đơn hàng, lịch sử vận chuyển, khiếu nại/hoàn tiền. Admin có thể khóa/mở tài khoản, ghi chú nội bộ.

### 3.3. Seller Management
- **ADM_SCR_004**: Seller Management
- **ADM_SCR_035**: Seller Details

**Flow:**
- Dashboard → Seller Management (004) → Seller Details (035).
- Seller Details hiển thị: thông tin shop, trạng thái hoạt động, danh sách sản phẩm, lịch sử đơn hàng, hiệu suất vận chuyển, lịch sử tranh chấp. Admin có thể duyệt/khóa shop, cảnh cáo, cấu hình đơn vị vận chuyển, ghi chú nội bộ.

### 3.4. Product Management
- **ADM_SCR_005**: Product Approval
- **ADM_SCR_006**: Product Management

**Flow:**
- Dashboard → Product Approval (005) → Product Management (006).
- Product Approval: Preview, duyệt/từ chối sản phẩm từ seller.
- Product Management: Quản lý toàn bộ sản phẩm đã duyệt.

### 3.5. Order Management
- **ADM_SCR_007**: Order Management
- **ADM_SCR_008**: Order Details

**Flow:**
- Dashboard → Order Management (007) → Order Details (008).
- Order Management: Theo dõi trạng thái đơn, filter theo ngày/kênh.
- Order Details: Xem chi tiết, timeline trạng thái, thông tin giao hàng.

### 3.6. Finance
- **ADM_SCR_010**: Transaction Management
- **ADM_SCR_011**: Wallet Management

**Flow:**
- Dashboard → Transaction Management (010) → Wallet Management (011).
- Transaction Management: Theo dõi giao dịch thanh toán & ví.
- Wallet Management: Theo dõi số dư, log ví, lịch sử điều chỉnh.

### 3.7. Dispute Management
- **ADM_SCR_028**: Dispute List
- **ADM_SCR_029**: Dispute Details
- **ADM_SCR_030**: Dispute Resolution History

**Flow:**
- Dashboard → Dispute List (028) → Dispute Details (029) → Dispute Resolution History (030).
- Dispute List: Filter theo trạng thái (Mới/Đang xử lý/Đã kết thúc), loại tranh chấp (Hoàn tiền/Giao hàng/Chất lượng), thời gian.
- Dispute Details: Xem chi tiết đơn hàng, bằng chứng (ảnh/video/chat), timeline xử lý. Admin quyết định: hoàn tiền một phần/toàn bộ, từ chối khiếu nại, hoặc khóa shop.
- Dispute Resolution History: Lưu trữ lịch sử tranh chấp đã xử lý, quyết định cuối cùng, admin phụ trách.

### 3.8. Analytics
- **ADM_SCR_019**: Analytics Dashboard

**Flow:**
- Dashboard → Analytics Dashboard (019).
- Hiển thị dashboard phân tích dữ liệu nâng cao với KPI, biểu đồ, metrics.

### 3.9. Review Moderation
- **ADM_SCR_027**: Review Moderation

**Flow:**
- Dashboard → Review Moderation (027).
- Kiểm duyệt review: Ẩn/xóa review, xử lý report từ người dùng.

### 3.10. Admin Settings
- **ADM_SCR_023**: Role & Permission
- **ADM_SCR_024**: Admin Account
- **ADM_SCR_025**: Audit Log

**Flow:**
- Dashboard → Admin Settings →
  - Role & Permission (023): Quản lý role & permission.
  - Admin Account (024): Tạo/sửa admin, reset password.
  - Audit Log (025): Nhật ký hệ thống, theo dõi log hành động admin.

### 3.11. System Configuration
- **ADM_SCR_031**: Platform Fee Settings
- **ADM_SCR_032**: Refund Policy Settings
- **ADM_SCR_033**: System Alert Thresholds

**Flow:**
- Dashboard → System Configuration →
  - Platform Fee Settings (031): Cấu hình phí nền tảng (phần trăm/cố định) áp dụng cho seller theo loại đơn hàng/danh mục. Có hiệu lực theo thời gian và log thay đổi.
  - Refund Policy Settings (032): Cấu hình quy tắc hoàn tiền (thời hạn, điều kiện áp dụng, mức hoàn tối đa). Áp dụng cho toàn hệ thống.
  - System Alert Thresholds (033): Thiết lập ngưỡng cảnh báo (tỷ lệ hủy cao, hoàn tiền bất thường, doanh thu giảm mạnh). Hiển thị cảnh báo trên Dashboard hoặc gửi thông báo nội bộ.

### 3.12. Environment (Out of Scope)
- **ADM_SCR_013**: Review Tree Report
- **ADM_SCR_014**: Real Tree Management
- **ADM_SCR_015**: Tree Fund Management
- **ADM_SCR_016**: Environment Report
- **ADM_SCR_017**: Location Management

**Flow:**
- Dashboard → Environment (out of scope) →
  - Review Tree Report (013): Xử lý report tình trạng cây.
  - Real Tree Management (014): Quản lý GPS, loại cây, trạng thái.
  - Tree Fund Management (015): Theo dõi dòng tiền quỹ trồng cây.
  - Environment Report (016): Xử lý các báo cáo môi trường.
  - Location Management (017): CRUD địa điểm xanh, bật/tắt hiển thị.

**Lưu ý:** Các màn Environment được nhóm vào **"Out of Scope"** vì không thuộc core e-commerce flow, nhưng vẫn giữ để tham chiếu.

---

## 4. Cross-role Flows

### 4.1. Order Flow: Customer → Seller
- Customer:
  - Product Details (CUS_SCR_007) → Cart (008) → Checkout (009) → Order Result (045) → Order History (030) → Order Details (031).
- Seller:
  - Order List (SEL_SCR_009) → Order Details (010) → Order Processing (011).

**Cross-role mapping:**
- **CUS_SCR_045 (Order Result)** → **SEL_SCR_009 (Order List)**: đơn mới xuất hiện cho Seller.
- **CUS_SCR_031 (Order Details)** → **SEL_SCR_009 (Order List)**: cùng tham chiếu tới cùng đơn từ phía Seller.

### 4.2. Return/Refund Flow: Customer → Seller → Admin
- Customer:
  - Order Details (CUS_SCR_031) → Return/Refund Request (CUS_SCR_046).
- Seller:
  - Return/Refund List (SEL_SCR_026_RETURN) → Return/Refund Details (SEL_SCR_027_RETURN).
- Admin:
  - Dispute List (ADM_SCR_028) → Dispute Details (ADM_SCR_029) → Dispute Resolution History (ADM_SCR_030).

**Cross-role mapping:**
- CUS_SCR_046 → SEL_SCR_026_RETURN (Seller tiếp nhận yêu cầu).
- SEL_SCR_026_RETURN → ADM_SCR_028 (escalate dispute lên Admin).

### 4.3. Shipping Flow: Seller → External Provider → Customer
- Seller:
  - Order Processing (SEL_SCR_011) → handover to shipping provider.
- External:
  - **EXT_SHIP**: External Shipping Provider (out-of-scope node).
- Customer:
  - Order Details (CUS_SCR_031) hiển thị trạng thái giao hàng.

**Cross-role mapping:**
- SEL_SCR_011 → EXT_SHIP (handover / tạo đơn giao hàng).
- EXT_SHIP → CUS_SCR_031 (cập nhật trạng thái giao hàng cho Customer).

---

## 5. Gợi ý sử dụng tài liệu

- **Design / UX**: dùng tài liệu này làm checklist khi thiết kế chi tiết từng màn, đảm bảo không lệch ID so với PDF.
- **Mermaid Diagram**: `Screen.mmd` đã được cập nhật tương ứng; tài liệu `.md` này là bản mô tả text song song.
- **Scope Control**: các tính năng **không có trong PDF** (livestream, mini game, tree, v.v.) đã được loại khỏi core; nếu muốn bật lại, thêm chúng vào một mục **“Optional Extensions”** riêng.


