## Lộ trình thiết kế UI/UX – VietShop

Dựa trên tài liệu chi tiết màn hình: [`UI.PDF`] 
Team thiết kế gồm:
- **Lead**: Quản lý tiến độ, review, kiểm duyệt chất lượng, thiết kế chính các flow lõi & init Design System.
- **Main Designer (Tài)**: Thiết kế các màn hình chính phức tạp theo flow.
- **Support Designer (Lâm)**: Thiết kế màn phụ, UI state, biến thể, hỗ trợ production.

---

## Phase 0 – Thiết kế Component theo tab “Component”

Phase đầu tiên tập trung **100% vào thiết kế component trong sheet/tab “Component” của PDF**, làm lần lượt để có “bộ LEGO” ổn định trước khi vẽ màn hình.

| Bước | Nhóm component / Tab | Phạm vi chính (bám theo PDF) | Owner | Hỗ trợ | Review | Số ngày ước tính |
| --- | --- | --- | --- | --- | --- | --- |
| C0.1 | **Foundation & Token** | Thiết lập màu, typography, spacing, grid, radius, shadow, icon style; define token cho toàn bộ hệ thống (theo phần guideline trong PDF nếu có). | Lead | Main | Lead | 1 |
| C0.2 | **Form & Action** | Tất cả component thuộc nhóm Form/Action trong tab Component: Button (primary/secondary/tertiary/icon – `CMP_004`, `CMP_005`…), Input text, Password, OTP, Checkbox/Radio, Switch (`CMP_050`), Date/Time Picker (`CMP_061`), Textarea (`CMP_013`), File Upload (`CMP_040`), Signature Pad (`CMP_055`); đầy đủ state: normal/hover/pressed/disabled/error/success, mobile/web. | Main | Support (state, size, variant) | Lead | 2 |
| C0.3 | **Card / List / Table / Layout** | Nhóm Card & List trong tab Component: Address Card (`CMP_045`), Payment Item (`CMP_046`), Voucher Selector (`CMP_047`), KPI Card (`CMP_036`), Fund Progress (`CMP_057`), NFT Info Card (`CMP_058`); các item list như Notification Item (`CMP_049`), Chat List Item (`CMP_038`); Data Table/Bill (`CMP_035`); Timeline (`CMP_044`); Accordion (`CMP_065`); Permission Matrix (`CMP_053`); Breadcrumbs (`CMP_064`). Chuẩn hoá layout, spacing, responsive. | Main | Support | Lead | 2 |
| C0.4 | **Media / Map / QR / Status** | Nhóm Media & Map: Camera View (`CMP_041`), Image Proof Item (`CMP_056`), Status Icon (`CMP_029`), Map View (`CMP_042`), Route Map (`CMP_054`), GPS Indicator (`CMP_043`), QR Code View (`CMP_067`), Tooltip (`CMP_068`), Live Reaction (`CMP_069`), Skeleton Loader (`CMP_063`). Thiết kế theo mô tả chi tiết trong PDF (success/fail/loading/not available…). | Main | Support (state loading/empty/error) | Lead | 2 |
| C0.5 | **Chat / Notification / Profile / Misc** | Chat List (`CMP_038`), Message Bubble (`CMP_039`), Profile Header (`CMP_051`), Rich Text Editor (`CMP_062`), Language Select (`CMP_059`), Version Info (`CMP_060`), các state unread/seen, online/offline, multi-line message, attachment (nếu có trong PDF). | Support | Main (pattern interaction) | Lead | 1 |

**Cách làm Phase 0:**
- Đi **đúng thứ tự C0.1 → C0.2 → C0.3 → C0.4 → C0.5**, mỗi bước xong đều có review & chốt bởi Lead, ghi rõ version trong file design.
- Khi đang ở C0.3–C0.4, Support có thể bắt đầu **áp thử component vào vài flow Customer (Home, List, Detail)** ở mức layout để test, nhưng **source of truth vẫn là tab Component**.
- Toàn bộ component phải **match 1–1 với list trong tab Component của PDF**, không tự nghĩ thêm loại mới nếu tài liệu chưa có.

---

## Bảng lộ trình chi tiết

| Bước | Phạm vi / Màn hình (và phụ thuộc) | Owner | Hỗ trợ | Review | Số ngày ước tính |
| --- | --- | --- | --- | --- | --- |
| 1 | **Khởi tạo project & nền tảng Design System** – rà soát toàn bộ PDF, lập inventory màn hình (tất cả `CUS_`, `SEL_`, `ADM_`; các `SHP_` nếu có chỉ ghi chú là out-of-scope, không thiết kế app riêng), setup file Figma (hoặc tương đương), define màu, typography, spacing, grid, bắt đầu bộ component chung (`CMP_001–069`). Là nền tảng cho tất cả các bước sau. | Lead | Main, Support | Lead | 2 |
| 2 | **Customer – Onboarding & Auth** – thiết kế chi tiết `CUS_SCR_001–004`: Onboarding, Login, Registration, Forgot Password; bao gồm state lỗi, empty, loading, OTP, login MXH (Google), show/hide password. Phụ thuộc: Bước 1. | Main | Support (state & biến thể) | Lead | 2 |
| 3 | **Customer – Home & Product Discovery** – `CUS_SCR_005–006`: Home, danh sách sản phẩm, search, filter, sort, card sản phẩm, banner carousel, entry Livestream, Wallet, Mini Game, skeleton loader (`CMP_063`). Đặt chuẩn pattern cho product card dùng lại ở Seller/Admin. Phụ thuộc: Bước 1 (token) và liên kết điều hướng từ Auth (Bước 2). | Main | Support | Lead | 3 |
| 4 | **Customer – Product Details & Cart** – `CUS_SCR_007–008`: chi tiết sản phẩm, gallery, đánh giá, biến thể, số lượng, Add to Cart, chia sẻ, xem shop; giỏ hàng với cập nhật số lượng, tổng tiền, state hết hàng, nhiều promotion, lỗi network. Phụ thuộc: Bước 3. | Main | Support | Lead | 3 |
| 5 | **Customer – Checkout & Order Result** – `CUS_SCR_009`, `CUS_SCR_009B`, `CUS_SCR_045`: màn nhập thông tin (địa chỉ `CMP_045`, thanh toán `CMP_046`, voucher `CMP_047`, ghi chú `CMP_013`), màn xác nhận đơn (bảng chi phí `CMP_035`, checkbox điều khoản `CMP_011`), màn kết quả (success/fail `CMP_029`, “Về trang chủ”, “Xem đơn hàng”). Bao gồm các case: thiếu địa chỉ, voucher invalid, thanh toán thất bại. Phụ thuộc: Bước 3–4 (cart & product). | Main | Support | Lead | 3 |
| 6 | **Customer – Danh sách đơn hàng & Tracking** – thiết kế list & detail đơn hàng theo section trong PDF, timeline trạng thái (`CMP_044`), map tracking (`CMP_042`), badge trạng thái (pending/shipping/delivered/cancelled), nhận cập nhật trạng thái giao hàng từ đối tác vận chuyển external (nếu có). Phụ thuộc: Bước 5 (sinh đơn) & Bước 1 (timeline/map). | Main | Support | Lead | 2 |
| 7 | **Customer – Wallet (Nạp/Rút/Lịch sử)** – `CUS_SCR_013–015`: màn nạp ví, rút ví, bảng lịch sử giao dịch với filter theo thời gian & trạng thái (pending/success/failed), empty state, error state. Tái sử dụng pattern bảng (`CMP_035`). Có thể chạy song song một phần với Bước 5 khi bảng & token đã ổn. Phụ thuộc: Bước 1. | Main | Support | Lead | 2 |
| 8 | **Customer – Mini Game & NFT** – `CUS_SCR_016–025`: danh sách cây, chi tiết cây, đăng ký cây (quét QR `CMP_067`), Water Tree (camera `CMP_041`), Anti-fake Image (AI status), GPS Verification (`CMP_042`, `CMP_043`), My Tree List, NFT Tree Details (`CMP_058`), Tree Fundraising (`CMP_057`), Report Tree (form + upload `CMP_040`). Bao phủ đầy đủ case: GPS fail, AI fail, cây không đủ điều kiện, NFT đã tạo, quỹ đầy/thiếu. Phụ thuộc: Bước 1 và luồng điều hướng cơ bản từ Home (Bước 3). | Main | Support | Lead | 4 |
| 9 | **Customer – Profile, Settings, Chat, Notifications** – `CUS_SCR_026–028`, `CUS_SCR_031–032`, `CUS_SCR_034`, `CUS_SCR_037`: danh sách thông báo (`CMP_049`), chat list & chat bubble (`CMP_038–039`), profile header (`CMP_051`), Settings (toggle `CMP_050`, Language Select `CMP_059`, Version Info `CMP_060`), màn upload file cho người dùng (`CMP_040`). Bắt đầu sau khi pattern Home/Nav (Bước 3) rõ. Phụ thuộc: Bước 1, 3. | Support | Main (interaction chính) | Lead | 3 |
| 10 | **Seller – Core (Dashboard, Orders, Products)** – các màn `SEL_SCR_00x` lõi: onboarding/auth seller, dashboard KPI (`CMP_036`), chart (`CMP_037`), bảng order/product (`CMP_035`), filter, paginate, skeleton (`CMP_063`); áp dụng lại pattern product card, trạng thái đơn từ Customer. Phụ thuộc: Bước 1, và pattern từ Bước 3–6. | Main | Support | Lead | 4 |
| 11 | **Seller – Nâng cao (Livestream, Promotion, Analytics)** – các màn livestream: pin sản phẩm (`CMP_048`), live reaction (`CMP_069`), schedule với Date/Time Picker (`CMP_061`); quản lý campaign, promotion, báo cáo. Tối ưu UI cho scenario Seller vận hành thường xuyên. Phụ thuộc: Bước 10 (IA seller) & component từ Bước 1. | Support | Main | Lead | 3 |
| 13 | **Admin – Core (Dashboard & Module quản trị)** – `ADM_SCR_00x`: dashboard tổng quan (KPI, chart), danh sách & chi tiết cho User/Seller/Product/Order với bảng `CMP_035`, filter nâng cao, trang phân quyền cơ bản. Tận dụng lại pattern bảng, filter từ Customer & Seller. Phụ thuộc: Bước 1, Bước 6–7, 10. | Main | Support | Lead | 4 |
| 14 | **Admin – Nâng cao (Logs, Permissions, Content Tool)** – `ADM_SCR_0xx` dùng `CMP_052` (Audit Log Row), `CMP_053` (Permission Matrix), `CMP_062` (Rich Text Editor), `CMP_065` (Accordion – FAQ), `CMP_064` (Breadcrumbs). Thiết kế kỹ luồng quản trị hệ thống, xem lại mapping màn hình trong PDF để không sót case. Phụ thuộc: Bước 13, Bước 1. | Support | Main | Lead | 3 |
| 15 | **Consolidation – Hoàn thiện Design System & States** – rà soát & chuẩn hoá tất cả component `CMP_001–069`: document prop, size, responsive, state (hover/pressed/disabled/focus/error/success), skeleton (`CMP_063`), pattern lỗi/empty/success dùng xuyên suốt Customer/Seller/Admin. Phụ thuộc: các bước 2–14 đã tương đối ổn định. | Main | Support | Lead | 3 |
| 16 | **Prototype end-to-end & kiểm tra UX** – tạo prototype cho các flow chính: Customer Purchase, Wallet, Mini Game, Seller vận hành, Admin giám sát, và luồng hiển thị trạng thái giao hàng nếu có (theo flow trong PDF). Tổ chức walkthrough nội bộ, refine những điểm nghẽn/edge case bị phát hiện. Phụ thuộc: Bước 2–14. | Lead | Main, Support | Lead | 2 |
| 17 | **Design QA & Handoff cho Dev** – tổng hợp token, guideline component, spec chi tiết cho các flow quan trọng (checkout, mini game, delivery status hiển thị cho khách, admin), xuất assets, annotate case đặc biệt theo PDF. Làm việc vòng lặp với dev để fix các issue UI/UX nhỏ. Phụ thuộc: Bước 16. | Lead | Main, Support | Lead | 2 |

---

## Checklist chi tiết theo nhóm màn hình

### Customer App – Checklist màn hình

**Nhóm 1 – Onboarding & Auth (Step 2)**  
- [ ] `CUS_SCR_001` – Onboarding  
- [ ] `CUS_SCR_002` – Login  
- [ ] `CUS_SCR_003` – Registration  
- [ ] `CUS_SCR_004` – Forgot Password  
- [ ] Các màn Customer/Auth khác (nếu có trong bảng Screen List của PDF – team copy thêm vào đây).

**Nhóm 2 – Shopping core (Home, List, Detail, Cart, Checkout, Result) – Step 3–6**  
- [ ] `CUS_SCR_005` – Home  
- [ ] `CUS_SCR_006` – Product List  
- [ ] `CUS_SCR_007` – Product Details  
- [ ] `CUS_SCR_008` – Shopping Cart  
- [ ] `CUS_SCR_009` – Checkout Info  
- [ ] `CUS_SCR_009B` – Confirm Order  
- [ ] `CUS_SCR_045` – Order Result  
- [ ] Toàn bộ các màn Order List/Order Detail/Tracking khác trong PDF (team liệt kê và tick đủ theo tab Screen).  

**Nhóm 3 – Wallet (Step 7)**  
- [ ] `CUS_SCR_013` – Deposit Wallet  
- [ ] `CUS_SCR_014` – Withdraw Wallet  
- [ ] `CUS_SCR_015` – Wallet History  

**Nhóm 4 – Mini Game & NFT (Step 8)**  
- [ ] `CUS_SCR_016` – Mini Game Tree List  
- [ ] `CUS_SCR_017` – Mini Game Tree Details  
- [ ] `CUS_SCR_018` – Register Tree  
- [ ] `CUS_SCR_019` – Water Tree  
- [ ] `CUS_SCR_020` – Anti-fake Image  
- [ ] `CUS_SCR_021` – GPS Verification  
- [ ] `CUS_SCR_022` – My Tree List  
- [ ] `CUS_SCR_023` – NFT Tree Details  
- [ ] `CUS_SCR_024` – Report Tree  
- [ ] `CUS_SCR_025` – Tree Fundraising  
- [ ] Các màn Mini Game/Môi trường khác nếu có (theo PDF).

**Nhóm 5 – Profile, Settings, Chat, Notifications, Khác (Step 9)**  
- [ ] `CUS_SCR_026` – Chat List  
- [ ] `CUS_SCR_027` – Chat Detail / Message Bubble  
- [ ] `CUS_SCR_028` – Notification List  
- [ ] `CUS_SCR_031` – Timeline-based screen (lịch sử hoạt động, theo PDF)  
- [ ] `CUS_SCR_032` – Profile Header / Profile screen  
- [ ] `CUS_SCR_034` – Settings (toggle, language, version…)  
- [ ] `CUS_SCR_037` – Màn có File Upload cho user  
- [ ] Toàn bộ CUS_SCR_xxx khác trong tab Customer (team đọc PDF và add vào checklist, đảm bảo không sót mã).

---

### Seller App – Checklist màn hình

**Nhóm 1 – Auth & Dashboard (Step 10)**  
- [ ] Tất cả `SEL_SCR_00x` liên quan Onboarding/Auth Seller (theo tab Screen trong PDF).  
- [ ] Dashboard Seller (KPIs, chart, table – mapping `SEL_SCR_002`, `SEL_SCR_019`… nếu PDF chỉ rõ).  

**Nhóm 2 – Product & Inventory (Step 10)**  
- [ ] Danh sách sản phẩm (`SEL_SCR_00x` tương ứng).  
- [ ] Chi tiết sản phẩm Seller (tạo/sửa sản phẩm).  
- [ ] Các màn quản lý tồn kho, giá, biến thể, promotion (theo mapping trong PDF).  

**Nhóm 3 – Order Management (Step 10)**  
- [ ] Order List Seller.  
- [ ] Order Detail Seller.  
- [ ] Các màn filter, bulk action, trạng thái đơn (pending/confirmed/shipping/completed/cancelled).  

**Nhóm 4 – Livestream & Promotion (Step 11)**  
- [ ] Màn lên lịch livestream (có Date/Time Picker `CMP_061`).  
- [ ] Màn livestream đang diễn ra (product pin `CMP_048`, live reaction `CMP_069`, chat).  
- [ ] Màn quản lý campaign, voucher, chương trình khuyến mãi (map theo `SEL_SCR_0xx` trong PDF).  

**Nhóm 5 – Seller Settings, Profile, Notification (Step 11/10)**  
- [ ] Màn cấu hình shop, profile, cài đặt (language, notification…).  
- [ ] Màn thông báo, inbox giữa Seller và Customer.  
- [ ] Các màn SEL_SCR_xxx khác trong tab Seller – team copy đầy đủ mã màn từ PDF vào đây và tick khi xong.  

---

### Admin Console – Checklist màn hình (Step 13–14)

**Nhóm 1 – Auth & Dashboard (Step 13)**  
- [ ] Các màn ADM_SCR_xxx liên quan auth Admin.  
- [ ] Dashboard chính: KPI card (`CMP_036`), chart (`CMP_037`), bảng tổng quan (`CMP_035`).  

**Nhóm 2 – Module quản trị (User/Seller/Product/Order/Content) – Step 13**  
- [ ] Danh sách User, chi tiết User.  
- [ ] Danh sách Seller, chi tiết Seller.  
- [ ] Danh sách Product, chi tiết Product (quản lý từ phía Admin).  
- [ ] Danh sách Order, chi tiết Order.  
- [ ] Các màn quản trị nội dung (nếu có, theo ADM_SCR_xxx trong PDF).  

**Nhóm 3 – Logs, Permissions, Content Tools (Step 14)**  
- [ ] Audit Log (`ADM_SCR_025` – sử dụng `CMP_052`).  
- [ ] Permission Matrix (`ADM_SCR_023` – sử dụng `CMP_053`).  
- [ ] FAQ / Help sử dụng Accordion (`CMP_065`).  
- [ ] Màn có Rich Text Editor (`CMP_062`) cho nội dung (announcement, policy…).  

**Nhóm 4 – Khác & Checklist mã màn**  
- [ ] Tất cả ADM_SCR_xxx còn lại trong tab Admin, team copy list ID từ PDF vào đây và tick khi thiết kế xong.  

---

- **Tổng thời gian ước tính**: khoảng **28–32 ngày làm việc (~6–7 tuần)** với 3 người (Lead + Main + Support) cùng tham gia thiết kế song song, tối ưu hoá phân chia task.  
- **Mốc review bắt buộc của Lead**:
  - Sau **Bước 1**: chốt Design System nền, IA, inventory màn hình.
  - Sau **Bước 5**: chốt luồng mua hàng Customer end-to-end (từ Home đến Order Result).
  - Sau **Bước 8**: chốt Mini Game & NFT (nhiều case phức tạp GPS/AI/QR).
  - Sau **Bước 10–11**: chốt core Seller.
  - Sau **Bước 13–14**: chốt Admin Console (log, permission, content tools).
  - Sau **Bước 16**: chốt prototype end-to-end trước khi handoff dev (Bước 17).  

---

- **Độ phức tạp cao của flow**: Checkout + Wallet + Mini Game + các phần liên quan tới giao hàng (delivery/tracking) đều có nhiều state & edge case (GPS fail, AI fail, thanh toán lỗi, tree không hợp lệ…). Cần bám sát mô tả trong PDF để không bỏ sót.  
- **Tính nhất quán giữa 3 “ứng dụng”** (Customer, Seller, Admin) và tích hợp với đối tác vận chuyển external: cùng dùng chung nhiều component (`CMP_035`, `CMP_036`, `CMP_037`, `CMP_041`, `CMP_042`, `CMP_044`, `CMP_050`, `CMP_063`…), dễ bị lệch nếu không consolidate ở Bước 1 và 15.  
- **Khối lượng màn hình lớn**: cần quản lý ưu tiên theo module (Customer core → Seller core → Admin) và khóa dần từng module sau review để tránh rework dây chuyền.  
- **Phụ thuộc vào Design System**: nếu Bước 1 không đủ chặt chẽ, về sau sẽ tốn nhiều effort refactor component, ảnh hưởng tiến độ các bước 10–14.  


