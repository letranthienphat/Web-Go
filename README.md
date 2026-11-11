WEB GO — Trình duyệt của người làm chủ dữ liệu

WEB GO không chạy đua với Chrome hay Edge ở số lượng extension. Nó được xây dựng quanh một triết lý khác: tốc độ tuyệt đối, quyền riêng tư mặc định, khả năng tùy biến sâu, và quyền sở hữu dữ liệu hoàn toàn thuộc về bạn. Mỗi dòng code trong WEB GO đều phục vụ một mục đích cụ thể, không có gì bị giấu sau những lớp UI bóng bẩy.

Trái tim của WEB GO là hệ thống quản lý vòng đời tab tự động (Tab Lifecycle). Sau 30 giây không hoạt động, tab nền bị đóng băng (Frozen) — CPU về 0% nhưng nội dung vẫn nguyên trong RAM để mở tức thì. Sau 5 phút, tab chuyển sang Discarded — giải phóng toàn bộ RAM, chỉ giữ URL, tự tải lại khi bạn click. Bộ đếm thời gian được đánh chỉ mục lại mỗi khi đóng/mở/kéo thả tab, đảm bảo không tab nào bị đóng băng nhầm.

Tải xuống đa luồng 64 kết nối (Max-Speed Downloader). WEB GO kiểm tra header Accept-Ranges, chia file thành 64 phần và tải song song bằng 64 thread — nhanh gấp 5–20 lần tải thường với file lớn. Cơ chế theo dõi lock-free, retry backoff lũy tiến, fallback một luồng nếu server không hỗ trợ. Download Manager riêng (Ctrl+J) hiển thị tiến độ từng file.

Lớp bảo mật LTTP (Lightweight Trust & Threat Protection). Phân tích URL theo thời gian thực: phát hiện ký tự @ trong authority, punycode/IDN, TLD rủi ro cao, subdomain sâu kết hợp từ khoá phishing. Chặn scheme lạ, chặn file:// từ trang web, phát hiện hạ cấp HTTPS→HTTP. Mọi quyết định đều ghi vào security.log để audit.

Chế độ ẩn danh thực sự tách biệt. QWebEngineProfile riêng với setOffTheRecord(True) — không storage, không cache, không cookie trên đĩa. Khi tắt ẩn danh, tự đóng tab incognito trước rồi mới xoá profile, tránh crash kinh điển.

MỚI — Trình đọc bài báo Offline (Offline Reader). Đây là tính năng độc quyền không trình duyệt thương mại nào có sẵn: nhấn một nút, WEB GO trích xuất nội dung chính của bài báo (bỏ quảng cáo, sidebar, menu), tải toàn bộ ảnh về máy, đóng gói thành một file HTML tự chứa trong ~/.webgo_data/offline/, kèm metadata (tiêu đề, tác giả, ngày lưu, URL gốc). Bạn có thể đọc lại bất cứ lúc nào — kể cả khi mất mạng, kể cả khi bài báo đã bị gỡ. Thư viện bài báo được quản lý trong một dialog riêng với tìm kiếm, xoá, xuất ra PDF.

MỚI — Tự động cập nhật (Auto-Updater). WEB GO tự kiểm tra phiên bản mới trên GitHub Releases mỗi khi khởi động (có thể tắt trong Cài đặt). Nếu có bản mới, nó hiển thị changelog và cho phép tải về file .exe duy nhất, xác minh SHA-256, rồi thay thế chính nó trong lần khởi động kế tiếp. Không cần mở trình duyệt, không cần thao tác thủ công.

MỚI — Trang Giới thiệu trong Cài đặt. Nhấn "Giới thiệu" trong hộp thoại Cài đặt để xem README trực tiếp từ GitHub, được render đẹp mắt với Markdown, có nút "Mở trên GitHub" và "Kiểm tra cập nhật".

Toàn bộ dữ liệu nằm trong một thư mục duy nhất — ~/.webgo_data/. Bookmark, lịch sử, cài đặt, profile, cache, log bảo mật, bài báo offline — tất cả đều có thể copy sang máy khác, backup bằng rsync, hay xoá sạch bằng rm -rf.

Tải WEB GO tại: https://drive.google.com/drive/folders/1gbdu7QhDQjlhOk2xlIsmGZ-PK6UJDZH4?usp=sharing
