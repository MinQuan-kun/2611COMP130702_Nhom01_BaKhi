# KẾ HOẠCH KIỂM THỬ NHÁP (DRAFT TEST PLAN)

* **Tên đề tài:** Kiểm thử ứng dụng thương mại điện tử Swag Labs ([https://www.saucedemo.com](https://www.saucedemo.com))
* **Mã học phần:** COMP1307 – Kiểm thử phần mềm cơ bản
* **Lớp:** 2611COMP130702
* **Nhóm:** Nhóm 01 (Bá Khí)
* **Kho GitHub:** [https://github.com/MinQuan-kun/2611COMP130702_Nhom01_BaKhi](https://github.com/MinQuan-kun/2611COMP130702_Nhom01_BaKhi)

---

## 1. Giới thiệu & Phạm vi kiểm thử (Scope)

### 1.1. Trong phạm vi (In-scope)
* **Chức năng Đăng nhập & Phân quyền:** Đăng nhập với các loại tài khoản (`standard_user`, `locked_out_user`, `problem_user`, `performance_glitch_user`) và xử lý thông báo lỗi.
* **Danh mục sản phẩm & Sắp xếp:** Xem danh sách sản phẩm, lọc/sắp xếp theo Tên (A-Z, Z-A) và Giá (thấp-cao, cao-thấp).
* **Quản lý Giỏ hàng:** Thêm/Xóa sản phẩm vào/khỏi giỏ hàng từ trang danh sách hoặc chi tiết, cập nhật badge số lượng giỏ hàng.
* **Thanh toán & Xác nhận đơn hàng (Checkout):** Nhập thông tin giao hàng (First Name, Last Name, Zip/Postal Code), tính tổng tiền (Item total + Tax) và hoàn tất đơn hàng.
* **Kiểm thử hộp trắng:** Phân tích logic nghiệp vụ cho 2 hàm mô phỏng (tính tổng tiền giỏ hàng và kiểm tra hợp lệ dữ liệu checkout).
* **Kiểm thử tự động:** Viết bộ kịch bản Unit Test và UI Automation Test tích hợp với GitHub Actions CI.

### 1.2. Ngoài phạm vi (Out-of-scope)
* Kiểm thử hiệu năng (Load/Stress Testing) trên máy chủ công cộng SauceDemo.
* Kiểm thử an toàn thông tin / bảo mật hạ tầng mạng bên dưới.

---

## 2. Mục tiêu kiểm thử (Objectives)
* Đạt độ bao phủ yêu cầu $\ge 80\%$.
* Xây dựng tối thiểu 100 ca kiểm thử thủ công mức thấp áp dụng các kỹ thuật Phân lớp tương đương (EP), Phân tích giá trị biên (BVA), Bảng quyết định và Chuyển trạng thái.
* Đạt độ bao phủ nhánh $\ge 80\%$ cho các hàm phân tích hộp trắng.
* Hoàn thành kịch bản kiểm thử tự động UI và Unit Test, chạy thành công trên quy trình CI (GitHub Actions).

---

## 3. Cách tiếp cận & Công cụ (Approach & Tools)

* **Kiểm thử Hộp đen:** 
  * Áp dụng EP và BVA cho các trường dữ liệu: First Name, Last Name, Zip/Postal Code, Số lượng sản phẩm trong giỏ hàng.
  * Dùng Bảng quyết định cho form Đăng nhập và Checkout.
  * Dùng Chuyển trạng thái cho toàn bộ luồng mua hàng (từ Chưa đăng nhập $\rightarrow$ Hoàn tất đơn hàng).
* **Kiểm thử Hộp trắng & Đơn vị:** Viết lại 2 hàm mô phỏng bằng Python/Java, vẽ đồ thị luồng điều khiển (CFG), tính độ phức tạp $V(G)$ và viết unit test bằng `pytest` / `JUnit 5`.
* **Kiểm thử Tự động UI:** Sử dụng `Selenium WebDriver` hoặc `Playwright` áp dụng mô hình Page Object Model (POM).
* **Quản lý lỗi & CI/CD:** Sử dụng GitHub Issues để theo dõi/quản lý vòng đời lỗi và GitHub Actions để tự động chạy kiểm thử khi push/pull request.

---

## 4. Tiêu chí đầu vào & Tiêu chí đầu ra (Entry & Exit Criteria)

* **Tiêu chí đầu vào (Entry Criteria):**
  * Bản đặc tả yêu cầu giả định đã hoàn thành và thống nhất trong nhóm.
  * Môi trường kiểm thử (trình duyệt, IDE, công cụ test) đã sẵn sàng.
* **Tiêu chí đầu ra (Exit Criteria):**
  * $100\%$ các ca kiểm thử đã thiết kế được thực thi hoàn chỉnh.
  * Tỉ lệ Pass $\ge 95\%$, các lỗi nghiêm trọng (Critical/High) đã được khắc phục hoặc có hướng xử lý.
  * Hồ sơ kiểm thử (File Excel, Báo cáo hoàn tất, Slide, Video demo) hoàn thành đầy đủ.

---

## 5. Phân tích rủi ro sản phẩm & dự án (Risk Analysis)

| Mã Rủi ro | Mô tả Rủi ro | Loại (SP/DA) | Khả năng ($K$) | Ảnh hưởng ($A$) | Điểm Rủi ro ($K \times A$) | Biện pháp giảm thiểu |
| :---: | :--- | :---: | :---: | :---: | :---: | :--- |
| **R01** | Cấu trúc UI của trang mẫu Swag Labs thay đổi làm gãy kịch bản UI Test | SP | 3 | 4 | **12 (Trung bình)** | Sử dụng locator ổn định dựa trên thuộc tính `data-test` có sẵn. |
| **R02** | Dữ liệu kiểm thử biên tại Checkout không khớp với xử lý thực tế của web | SP | 2 | 3 | **6 (Thấp)** | Xây dựng ma trận dữ liệu EP/BVA kỹ lưỡng trước khi bắt đầu test. |
| **R03** | Xung đột mã nguồn trên GitHub giữa 5 thành viên khi đẩy code | DA | 3 | 3 | **9 (Trung bình)** | Phân chia branch rõ ràng, quy định review code trước khi merge vào main. |
| **R04** | Thành viên nghỉ ốm hoặc chậm tiến độ phần việc được phân công | DA | 2 | 4 | **8 (Trung bình)** | Phân công công việc gối đầu, các thành viên hỗ trợ chéo lẫn nhau. |
| **R05** | File cấu hình `.github/workflows/ci.yml` bị lỗi cú pháp | DA | 3 | 2 | **6 (Thấp)** | Kiểm tra file cấu hình cục bộ và dùng template chuẩn từ học phần. |
| **R06** | Bỏ sót các ca kiểm thử biên ở các trường hợp nhập khoảng trắng / ký tự đặc biệt | SP | 3 | 3 | **9 (Trung bình)** | Thực hiện review chéo (Peer review) danh sách ca kiểm thử giữa các thành viên. |

---

## 6. Phân công công việc (Team Assignments - 5 thành viên)

| STT | Họ và tên | MSSV | Vai trò | Công việc phụ trách cụ thể |
| :---: | :--- | :---: | :---: | :--- |
| 1 | **Văn Vĩnh Thái Toàn** | 49.01.104.155 | Nhóm trưởng | Điều phối chung, lập kế hoạch kiểm thử, tổng hợp tiểu luận, quản lý GitHub Repo. |
| 2 | **Ngô Dương Đức Thắng** | 49.01.104.137 | QC Engineer | Thiết kế ca kiểm thử hộp đen (EP, BVA), viết sheet `TestCase` & `RTM`. |
| 3 | **Nguyễn Hữu Minh Quân** | 49.01.104.120 | Developer / QC | Thực hiện kiểm thử hộp trắng, viết các hàm mô phỏng nghiệp vụ và Unit Test. |
| 4 | **Nguyễn Thái Bình** | 49.01.104.011 | Automation QC | Viết kịch bản tự động UI Automation (Selenium/Playwright) và cấu hình GitHub Actions CI. |
| 5 | **Nguyễn Thị Vinh** | 49.01.104.175 | QA / Reviewer | Quản lý lỗi (GitHub Issues), hỗ trợ viết đặc tả yêu cầu, làm Slide thuyết minh & Video demo. |

---

## 7. Lịch trình thực hiện (Schedule & Milestones)

* **Buổi 2 – Buổi 3:** Lập nhóm, tạo repo GitHub, nộp Phiếu đăng ký đề tài và đẩy Kế hoạch kiểm thử nháp lên GitHub.
* **Buổi 4 – Buổi 6:** Xây dựng đặc tả yêu cầu giả định, thiết kế toàn bộ ca kiểm thử hộp đen (EP, BVA, Bảng quyết định).
* **Buổi 7 (Mốc tiến độ):** Nộp file Excel kiểm thử + Kế hoạch hoàn chỉnh (PDF) để nhận nhận xét từ giảng viên.
* **Buổi 8:** Phân tích đồ thị CFG, tính $V(G)$ và thực hiện kiểm thử hộp trắng cho 2 hàm mô phỏng.
* **Buổi 9:** Viết mã kiểm thử đơn vị (Unit Test) và đưa kịch bản chạy tự động lên GitHub Actions.
* **Buổi 10:** Viết kịch bản UI Automation, chạy lại toàn bộ bộ kiểm thử hồi quy, quản lý lỗi trên GitHub Issues.
* **Hạn nộp cuối cùng (Buổi 10 + 7 ngày):** Hoàn thiện Tiểu luận (PDF/Word), Slide ghi chú, Video demo (8-12 phút) và nộp trọn bộ hồ sơ lên LMS.