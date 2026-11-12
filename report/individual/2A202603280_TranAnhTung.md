# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên [LMS](https://aithucchien.vinuni.edu.vn). Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](../../reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202603280
- Ngày / CVAT local: 12/11/2026 / CVAT local
- Công cụ đã dùng: Polygon, Brush/Mask, OpenCV và thứ tự layer (z-order).

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh [LMS](https://aithucchien.vinuni.edu.vn) đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip| 3 / 3 |  |
| medium_instance | medium_instance.zip | 3 / 3 |  |
| hard_panoptic | hard_panoptic.zip | 2 / 2 |  |
| cp1_holes | cp1_holes.zip | 1 / 1 |  |
| cp2_slice | cp2_slice.zip | 1 / 1 |  |
| cp5_occlusion | cp5_occlusion.zip | 1 / 1 | |
| cp3_thin | cp3_thin.zip | 1 / 1 |  |
| cp4_curb | cp4_curb.zip  | 1 / 1 |  |
| cp6_coverage | cp6_coverage.zip | 1 / 1 |  |
| **Tổng tối đa** | | |  |

Tất cả các ảnh đã được gán nhãn và Save.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: `000000181542.jpg`, xe buýt ở phía trái ảnh.
- Class và quy tắc tôi dùng để chọn biên: `bus`; tôi vẽ theo phần xe buýt nhìn thấy và dừng ở ranh với nền hoặc object che khuất.
- Nếu dùng gợi ý sau đó: khi dùng OpenCV, tôi kiểm lại kết quả vì vùng gợi ý có thể bị khuyết hoặc không sát biên; tôi chỉ giữ phần phù hợp với ảnh gốc và chỉnh phần còn thiếu.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: `cp1_holes`, vùng object vẽ bằng OpenCV.
- Lỗi thuộc loại: biên.
- Bằng chứng tôi nhìn thấy: kết quả OpenCV bị khuyết; tôi đã thử dùng Rectangle để bù nhưng Rectangle không thể nhập trực tiếp với Mask/Polygon.
- Quy tắc và hành động sửa: tôi kiểm tra lại kiểu annotation, không khoét kính hoặc khe bánh xe tùy tiện và chỉnh mask theo phần nhìn thấy của object.
- Sau sửa đã Save và export lại chưa? Đã Save và export `cp1_holes.zip`.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): … / chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| `cp1_holes`, khe bánh xe | Lỗ nền hoặc chi tiết thuộc xe | Khe nhỏ/kính không tự động là lỗ cần khoét | Giữ vùng này trong mask xe |
| `cp2_slice`, hai xe sát nhau | Một object hoặc hai instance cùng class | Hai vật cùng class vẫn là hai instance | Vẽ hai mask riêng |
| `hard_panoptic`, ranh sky với mái nhà/cây | Vẽ sát ranh ngay từ đầu hoặc dùng layer | Layer phía sau có thể phủ vùng nền, object vẽ sau đè lại lên trên | Vẽ nền trước, rồi dùng building/vegetation ở layer trước để tạo ranh chi tiết |
