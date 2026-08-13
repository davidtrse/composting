# Hướng dẫn đưa website lên GitHub Pages

File `index.html` đã được build sẵn từ file kế hoạch kinh doanh (`Ke_hoach_kinh_doanh_gai_xanh_Lao.md`), có khóa mật khẩu ở trang đầu.

## 1. Cảnh báo quan trọng về bảo mật (đọc trước khi dùng)

Đây là **khóa mềm** (soft gate), phù hợp để tránh người lạ tình cờ xem được link, **KHÔNG phải bảo mật thật sự**:

- Trang web là site tĩnh public trên GitHub Pages — ai có link đều tải được toàn bộ mã nguồn (kể cả nội dung kế hoạch kinh doanh) về máy, kể cả khi chưa nhập đúng mật khẩu, chỉ là họ phải biết cách xem "View Page Source" hoặc dùng DevTools.
- Mật khẩu không được lưu dạng chữ thường trong code (đã băm bằng SHA-256) để tránh lộ ngay khi mở source, nhưng người có kỹ thuật vẫn có thể dò được bằng cách thử offline vì thuật toán băm là công khai.
- Nếu cần bảo mật thật (chỉ người có tài khoản GitHub được cấp quyền mới xem được), nên đổi sang **repo Private** + mời từng người làm collaborator, thay vì trang public có khóa mật khẩu bằng JavaScript. Cách này thì không dùng được GitHub Pages miễn phí thông thường (cần GitHub Pro/Team để bật Pages cho repo private), nên nói lại nếu bạn muốn đổi hướng này.

## 2. Cấu trúc file cần đưa lên

Trong thư mục output của phiên làm việc này có:
- `site_build/index.html` — toàn bộ website (tự chứa, không cần file phụ)

## 3. Các lệnh git để push lên davidtrse/composting

Mở Terminal trên máy bạn, vào đúng thư mục chứa `index.html` (đã tải xuống từ Cowork), rồi chạy:

```bash
git clone https://github.com/davidtrse/composting.git
cd composting
# copy file index.html vừa tải về vào đúng thư mục này
git add index.html
git commit -m "Add ramie business plan site with password gate"
git push origin main
```

Nếu `git push` báo lỗi vì nhánh không phải `main` (có thể là `master`), kiểm tra bằng:

```bash
git branch -a
```

rồi đổi `main` trong lệnh push thành tên nhánh đúng.

Nếu bị hỏi đăng nhập, GitHub hiện không cho dùng mật khẩu tài khoản trực tiếp qua git nữa — cần:
- Đăng nhập qua trình duyệt khi Git yêu cầu (nếu dùng GitHub Desktop hoặc Git có hỗ trợ đăng nhập trình duyệt), hoặc
- Tạo Personal Access Token (Settings → Developer settings → Personal access tokens) và dùng token đó thay cho mật khẩu khi được hỏi.

## 4. Bật GitHub Pages

1. Vào repo `davidtrse/composting` trên GitHub → tab **Settings** → mục **Pages** (bên trái).
2. Ở phần "Build and deployment" → **Source**, chọn **Deploy from a branch**.
3. Chọn nhánh `main` (hoặc nhánh bạn vừa push), thư mục `/ (root)`.
4. Bấm **Save**. Sau khoảng 1-2 phút, GitHub sẽ cấp link dạng:

```
https://davidtrse.github.io/composting/
```

Mở link đó, nhập mật khẩu **binhminh2026** để xem nội dung.

## 5. Cập nhật nội dung sau này

Mỗi khi sửa file kế hoạch kinh doanh (`.md`), cần build lại `index.html` rồi push lại (`git add`, `git commit`, `git push`) — quay lại đây nhờ tôi build lại bản HTML mới bất cứ lúc nào bạn cần.
