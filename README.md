# App Tự đánh giá KPI cán bộ

App tự đánh giá, xếp loại KPI cán bộ theo quý — chạy độc lập trên trình duyệt (`app_tu_danh_gia_kpi.html`), có thể đóng gói thành ứng dụng desktop cài đặt được (Windows/macOS/Linux) qua Electron.

## Cách 1 — Dùng ngay, không cần cài gì

Chỉ cần tải file `app_tu_danh_gia_kpi.html` về máy và mở bằng trình duyệt (Chrome/Edge/Firefox). Dữ liệu tự lưu trong trình duyệt; mục "Đồng bộ dữ liệu với GitHub" trong app cho phép lưu/tải lại dữ liệu qua một repository GitHub.

## Cách 2 — Cài đặt như ứng dụng desktop (Electron)

### Chạy thử ở chế độ phát triển

```bash
npm install
npm start
```

### Tự build file cài đặt trên máy bạn

```bash
npm run dist:linux   # tạo .AppImage và .deb (chạy trên Linux)
npm run dist:win     # tạo .exe (nsis) — phải chạy trên Windows, hoặc Linux có cài Wine
npm run dist:mac     # tạo .dmg — bắt buộc phải chạy trên macOS (giới hạn của Apple)
```

> Lưu ý: electron-builder không thể build file `.exe` hoàn chỉnh trên Linux nếu máy chưa cài **Wine**, và không thể build `.dmg` ở đâu khác ngoài **macOS** — đây là giới hạn của công cụ, không phải lỗi cấu hình.

### Lấy file cài đặt thật (.exe / .dmg / .AppImage) mà không cần tự build

Repo đã có sẵn GitHub Actions workflow (`.github/workflows/build.yml`) tự build cả 3 nền tảng trên máy chủ thật của GitHub (Windows, macOS, Linux):

1. Vào tab **Actions** của repository trên GitHub.
2. Chọn workflow **"Build desktop installers"** → **Run workflow** (hoặc đẩy một tag dạng `v1.0.0` để tự kích hoạt).
3. Đợi build xong (vài phút), mở lần chạy đó → mục **Artifacts** để tải về:
   - `kpi-app-windows-latest` → chứa file `.exe`
   - `kpi-app-macos-latest` → chứa file `.dmg`
   - `kpi-app-ubuntu-latest` → chứa `.AppImage` và `.deb`

## Cấu trúc dự án

- `app_tu_danh_gia_kpi.html` — toàn bộ giao diện + logic tính điểm KPI, kèm thư viện đọc file .docx (mammoth.js) nhúng sẵn để hoạt động offline, không cần tải gì thêm.
- `main.js` — tiến trình chính Electron, mở file HTML trên trong một cửa sổ desktop.
- `build/icon.png` — icon ứng dụng.
- `.github/workflows/build.yml` — tự động build installer cho Windows/macOS/Linux.
