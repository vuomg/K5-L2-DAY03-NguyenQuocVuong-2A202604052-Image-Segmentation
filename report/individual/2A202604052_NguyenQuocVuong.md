# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên [LMS](https://aithucchien.vinuni.edu.vn). Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](../../reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202604052
- Ngày / CVAT local: 11/11/2026 / CVAT local
- Công cụ đã dùng: CVAT Polygon, Brush, Intelligent Scissors, SAM (AI Tools); `scripts/inspect_submissions.py` để kiểm cấu trúc ZIP

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh [LMS](https://aithucchien.vinuni.edu.vn) đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | `submissions/easy_semantic.zip` | 3 / 3 | 20 |
| medium_instance | `submissions/medium_instance.zip` | 3 / 3 | 32 |
| hard_panoptic | `submissions/hard_panoptic.zip` | 2 / 2 | 30 |
| cp1_holes | `submissions/cp1_holes.zip` | 1 / 1 | 3 |
| cp2_slice | `submissions/cp2_slice.zip` | 1 / 1 | 3 |
| cp5_occlusion | `submissions/cp5_occlusion.zip` | 1 / 1 | 3 |
| cp3_thin | `submissions/cp3_thin.zip` | 1 / 1 | 3 |
| cp4_curb | `submissions/cp4_curb.zip` | 1 / 1 | 3 |
| cp6_coverage | `submissions/cp6_coverage.zip` | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Class và quy tắc tôi dùng để chọn biên: `person`; vẽ sát phần nhìn thấy, dừng ở chân, không tính bóng đổ.
- Nếu dùng gợi ý sau đó: không dùng cho Medium.
- Nếu không dùng gợi ý: không dùng. Quyết định khác: ô tô đỗ sát nhau vẫn tách mỗi xe một object `car`, chỉ vẽ phần nhìn thấy.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: `hard_panoptic`, ảnh `000000460147`, vùng `building`.
- Lỗi thuộc loại: phủ vùng.
- Bằng chứng tôi nhìn thấy: script kiểm ZIP báo `building` thiếu mask, do tôi vẽ bằng Rectangle.
- Quy tắc và hành động sửa: bounding box không thay mask; xóa Rectangle, vẽ lại bằng Polygon. Bổ sung `road`, `sky`, `building`, `vegetation` còn thiếu ở ảnh `000000350023`.
- Sau sửa đã Save và export lại chưa? Đã Save, export lại COCO 1.0, script báo OK.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1. Easy `81ae7cbb`, cây trụi lá bên trái | Tô cả tán / chỉ tô thân, cành | Cành quá mảnh để tô từng cành | Tô cả tán. Hỏi coach: reference tô theo tán hay theo cành? |
| 2. `cp1_holes`, caravan bên trái, van xanh phía sau | Caravan: `bus` / để trống. Van: `truck` / `car` | Không có class cho caravan; van chở hàng gần truck | Gán caravan `bus`, van `truck`. Hỏi coach xử lý xe không có class tương ứng. |
| 3. `cp4_curb`, bãi bê tông chỗ SUV trắng | `sidewalk` / để trống | Ranh theo chức năng: đây là chỗ đỗ xe, không phải lối đi bộ | Để trống. |
