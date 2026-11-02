# Xe Nước · Sổ tay Sài Gòn

Ứng dụng PWA tiếng Việt, tối ưu điện thoại, chạy trực tiếp trên GitHub Pages. Không cần cài Node, không cần build, không có tài khoản hay dịch vụ trả phí.

## Đưa lên GitHub Pages

1. Giải nén `xe-nuoc-pwa.zip`.
2. Tạo repository trên GitHub (ví dụ `so-tay-xe-nuoc`).
3. Chọn **Add file → Upload files**, đưa **toàn bộ nội dung bên trong thư mục `xe-nuoc-pwa`** vào gốc repository. `index.html` phải nằm ngay ở gốc, ngang hàng `app.js`, `sw.js`, `data.json`, thư mục `assets`… Không chỉ upload file ZIP.
4. Commit các tệp. Vào **Settings → Pages → Build and deployment**, chọn **Deploy from a branch**, nhánh **main**, thư mục **/(root)** rồi **Save**.
5. Đợi GitHub triển khai; mở địa chỉ được GitHub hiển thị, thường là `https://TEN-TAI-KHOAN.github.io/so-tay-xe-nuoc/`.
6. Mở trên điện thoại khi có mạng, chờ thông báo **Sẵn sàng xem ngoại tuyến**, rồi thêm vào màn hình chính.

Nếu upload qua giao diện không hiện `.nojekyll`, tạo tệp rỗng tên `.nojekyll` ở gốc repository. Toàn bộ đường dẫn là tương đối nên chạy được cả ở tên miền chính và thư mục repository. URL GitHub Pages có thể được công khai tùy gói và cấu hình; ứng dụng không có màn hình đăng nhập.

Hướng dẫn chính thức: [Cấu hình nguồn GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).

## Cài trên điện thoại

- **iPhone/iPad:** mở bằng Safari → Chia sẻ → Thêm vào Màn hình chính.
- **Android:** mở bằng Chrome → menu ⋮ → Cài đặt ứng dụng / Thêm vào màn hình chính. Nút cài trong ứng dụng sẽ mở lời mời cài nếu trình duyệt hỗ trợ; nếu chưa hỗ trợ sẽ hiện hướng dẫn.
- Muốn dùng PWA phải mở qua **HTTPS** (GitHub Pages đã hỗ trợ) hoặc localhost khi phát triển. Mở trực tiếp file HTML bằng `file://` không bật được đầy đủ tính năng.
- Chi tiết chuẩn PWA: [MDN – Making PWAs installable](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Guides/Making_PWAs_installable).

## Có gì trong ứng dụng?

- 379 mục đã gom trùng: 152 đồ uống/kem không cồn, 47 công thức nền/topping, 139 món ăn/tráng miệng, 41 món có cồn.
- Tìm không dấu theo tên, nguyên liệu và trang nguồn; lọc nhóm món.
- Xem các phiên bản công thức, định lượng và lưu ý của bản tổng hợp.
- Sổ tay chuẩn bị, bảo quản, kế hoạch tài chính, link mua sắm.
- Đánh dấu yêu thích, ghi chú thử món và checklist chuẩn bị.
- Xuất/nhập bản sao JSON cho dữ liệu cá nhân.
- Đọc đầy đủ tại `book.html` và tải bản Markdown.
- Minh họa SVG và biểu tượng PNG được đóng gói sẵn, không cần tải ảnh từ nơi khác.

## Ngoại tuyến, lưu trữ và cập nhật

Service worker tải sẵn giao diện, toàn bộ dữ liệu và minh họa ở lần truy cập có mạng thành công. Sau thông báo sẵn sàng, có thể mở lại và tra cứu khi mất mạng. Link Shopee/nhà cung cấp vẫn cần mạng. Không đóng gói PDF gốc; giữ số trang để đối chiếu bản PDF riêng của bạn.

Yêu thích, ghi chú và checklist dùng localStorage, chỉ nằm trong trình duyệt/thiết bị và tên miền đang dùng. Không tự đồng bộ giữa máy, Safari, Chrome hay URL khác nhau. Có thể mất dữ liệu nếu xóa dữ liệu trình duyệt hoặc trình duyệt tự giải phóng bộ nhớ. Hãy **Xuất bản sao** định kỳ; khi nhập, các mục yêu thích được gộp, ghi chú/checklist đang có được ưu tiên nếu trùng.

Sửa nội dung hoặc giao diện rồi đổi chuỗi `VERSION` đầu `sw.js` (ví dụ `2026-11-03-v2`) trước khi upload. Ứng dụng kiểm tra bản mới khi mở có mạng; bản mới được kích hoạt sau khi đóng tất cả cửa sổ/tab của ứng dụng rồi mở lại. Không cần xóa dữ liệu cá nhân để cập nhật. Hãy đổi VERSION mỗi lần phát hành để tránh giữ cache cũ.

## Cấu trúc và sửa nội dung

- `index.html`: khung ứng dụng, thông tin cài đặt.
- `app.js`, `style.css`: chức năng và giao diện.
- `data.json`: dữ liệu hiển thị trong ứng dụng. `recipes` có `id`, `name`, `group`, `html`, `search`, `sources`; `guides` có `id`, `title`, `html`. Giữ nguyên `id` để ghi chú đã lưu không bị lệch món. Khi sửa công thức, sửa cả `html` và `search` tương ứng để tìm kiếm đúng.
- `book.html`: bản đọc đầy đủ; `so-tay.md`: bản Markdown. Nếu sửa dữ kiện, cập nhật đồng thời ba bản (`data.json`, `book.html`, `so-tay.md`) để giữ nhất quán.
- `manifest.webmanifest`, `sw.js`: thông tin cài PWA và lưu ngoại tuyến.
- `assets/`: minh họa và icon tự tạo cho bộ ứng dụng này.
- `.nojekyll`: phục vụ các tệp tĩnh nguyên trạng.

Không cần chạy lệnh để triển khai. Muốn xem thử trên máy, chạy một máy chủ tĩnh tại thư mục này, ví dụ `python3 -m http.server 8080`, rồi mở `http://localhost:8080`.

## Nguồn và phạm vi

Chuyển từ sổ tay tổng hợp ngày **03/11/2026**, dựa trên PDF Công Thức Pha Đồ Uống – tổng hợp, 555 trang. Giữ nguyên cảnh báo về thiếu dữ kiện, lỗi nhận dạng và khác biệt giữa các phiên bản. Dự toán **18.487.500 đồng** chỉ là mô hình mẫu theo giả định của bản gốc, không phải giá mua hiện tại. Nội dung các nguồn và công thức không mang nghĩa liên kết/chứng thực bởi thương hiệu. Các hướng dẫn vận hành trong sổ tay cần đọc cùng lưu ý nguồn.

Bản kiểm tra đi kèm: `KIEM_TRA.md`.
