# 📋 Theo Dõi Tiến Độ PC08 / PC09

## Mô tả
Dashboard theo dõi tiến độ phương án PC08 và PC09, tính đến 23/04/2026.

## Cách dùng
Mở file `index.html` bằng bất kỳ trình duyệt nào (Chrome, Edge, Firefox...).
Không cần cài đặt gì thêm — chạy hoàn toàn offline.

## Tính năng
- **KPI tổng quan**: Tổng PC08, đã ký, đóng dấu, chưa ký, PC09
- **So sánh chỉ tiêu**: 2 mốc thời gian (30/06/2026 và 14/10/2026)
- **Diễn biến tăng giảm**: Ghi nhận theo từng thời điểm kiểm đếm, tự động tính Δ tăng/giảm
- **Chi tiết nhân sự**: 18 cán bộ với trạng thái từng người

## Chỉ tiêu
| Mốc | PC08 | PC09 |
|-----|------|------|
| 30/06/2026 | 744 PA | — |
| 14/10/2026 | 1.482 PA (1.372 + 110 phát sinh) | 6 PA |

## Số liệu ban đầu (23/04/2026 — 11:40)
| Chỉ số | Số lượng |
|--------|----------|
| Tổng PC08 | 335 |
| Đã ký (chưa đóng dấu) | 307 |
| Đã ký + Đóng dấu | 7 |
| Chưa ký | 21 |
| PC09 đã ký | 1 |
| PC09 đóng dấu | 1 |

## Cập nhật dữ liệu
Khi có đợt kiểm đếm mới:
1. Mở `index.html` trong trình duyệt
2. Kéo xuống mục **"Diễn biến tăng giảm hồ sơ"**
3. Nhấn **"＋ Thêm thời điểm kiểm đếm"**
4. Nhập ngày giờ và số liệu thực tế
5. Dữ liệu tự lưu trong trình duyệt (localStorage)

> **Lưu ý**: Dữ liệu diễn biến được lưu trong trình duyệt. 
> Nếu muốn chuyển sang máy khác, cần xuất/nhập thủ công.

## Phiên bản
- v1.1 — 23/04/2026
