# Reflection — Lab 19

**Tên:** Đỗ Duy Đông
**Cohort:** Cohort 3 - 2A202601657
**Path đã chạy:** lite

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

- `exact` (15 queries): BM25 (96.7%) và Hybrid (96.7%) đồng hạng dẫn đầu do từ khóa kỹ thuật xuất hiện chính xác trong corpus.
- `paraphrase` (15 queries): Cả hai đều giảm do từ khóa không xuất hiện verbatim, Vector search bắt ngữ nghĩa tốt hơn trên các query tương đồng.
- `mixed` (20 queries): Hybrid thắng tuyệt đối (100.0%) nhờ thuật toán RRF (k=60) kết hợp hoàn hảo giữa tín hiệu từ khóa chính xác và ngữ nghĩa ngữ cảnh. Tổng thể Hybrid đạt 78.6% (vượt trội so với 77.8% của BM25 và 73.2% của Vector).

Khi nào không dùng Hybrid?
1. Không dùng khi hệ thống yêu cầu độ trễ cực thấp/tài nguyên phần cứng tối thiểu và dữ liệu chỉ tra cứu định danh/mã lỗi cụ thể (Pure BM25 là đủ, không tốn chi phí inference vector).
2. Không dùng khi người dùng tìm kiếm đa ngữ/hình ảnh hoặc mô tả trừu tượng hoàn toàn không chứa từ khóa gốc (Pure Vector tối ưu hơn).

---

## Điều ngạc nhiên nhất khi làm lab này

Sự kết hợp đơn giản của công thức RRF (1 / (60 + rank)) lại mang lại độ ổn định cao và giải quyết triệt để các câu query dạng mixed so với từng phương pháp riêng lẻ.
