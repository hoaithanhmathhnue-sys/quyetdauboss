# ⚔ Quyết Chiến Với Boss

Game lớp học môn Toán để giáo viên chiếu lên màn hình: cả lớp (hoặc 2–4 đội) trả lời câu hỏi để hạ **Slime King**.
Chạy hoàn toàn trên trình duyệt — không cần tài khoản, không cần cơ sở dữ liệu, không cần Internet khi mở bằng file.

## Tính năng

- **3 dạng câu hỏi** theo cấu trúc đề 2025: trắc nghiệm A–D, Đúng/Sai (mỗi ý a, b, c, d là một lượt), trả lời ngắn (giáo viên xem đáp án rồi chấm).
- **Công thức Toán** hiển thị bằng KaTeX (`$...$`, `$$...$$`).
- **Nhập đề từ file Word (.docx)**: công thức MathType / Equation 3.0 / công thức Word được chuyển sang LaTeX ngay trên máy; đáp án đúng nhận từ chữ **gạch chân** hoặc **tô đỏ**; giữ lời giải và hình ảnh.
- **Chế độ chơi**: cả lớp, hoặc chia 2–4 đội lần lượt trả lời, có **cướp lượt**, khiên riêng từng đội, bảng xếp hạng MVP.
- Hiệu ứng, âm thanh tự tạo bằng Web Audio (không dùng file âm thanh).

## Cách dùng nhanh

1. Mở `index.html` bằng Chrome hoặc Edge (bấm đúp là chạy, không cần mạng) → màn hình giới thiệu **Quyết Chiến Với Slime King** hiện ra, bấm **⚔ VÀO GAME** (hoặc `Enter`).
2. Bấm **✎ Câu hỏi** → **📄 Nhập file Word (.docx)** hoặc tự gõ câu hỏi → **Lưu**.
3. Chọn **Cả lớp / 2 đội / 3 đội / 4 đội** rồi bấm **Bắt đầu trận đấu**. Nhấn `F` để chiếu toàn màn hình.

Phím tắt: `A`–`D` hoặc `1`–`4` chọn đáp án · Đúng/Sai: `1`/`2` · Trả lời ngắn: `Enter` xem đáp án, `1` đúng, `2` sai · `Space` câu tiếp · `M` tắt tiếng · cướp lượt: `1`–`4` chọn đội, `0` không ai cướp.

> Câu hỏi và ảnh được lưu **trong trình duyệt của máy đang dùng** (localStorage + IndexedDB), không gửi lên máy chủ nào.
> Đổi máy hoặc đổi trình duyệt thì cần nhập lại đề.

## Cấu trúc thư mục

```
index.html              # toàn bộ game (giao diện + logic)
favicon.svg
assets/gioi-thieu.jpg   # ảnh màn hình giới thiệu (đã nén ~270 KB)
lib/mtef2tex.js         # đọc công thức MathType / Equation 3.0 -> LaTeX
lib/docx-import.js      # đọc đề Word (.docx)
lib/jszip.min.js        # giải nén .docx
lib/cfb.min.js          # đọc đối tượng OLE (MathType) trong .docx
katex/                  # KaTeX + phông chữ (chạy offline)
licenses/               # giấy phép các thư viện
vercel.json             # cấu hình Vercel (cache, header bảo mật)
```

Không có bước build — đây là trang web tĩnh.

## Đưa lên GitHub

**Cách 1 — GitHub Desktop (dễ nhất):** File → Add local repository → chọn thư mục này → *create a repository* →
đặt tên `quyet-chien-voi-boss` → Commit → **Publish repository**.

**Cách 2 — dòng lệnh** (tạo trước repo trống `quyet-chien-voi-boss` trên github.com, thay `TEN-TAI-KHOAN`):

```powershell
git init
git add .
git commit -m "Quyết Chiến Với Boss - bản đầu tiên"
git branch -M main
git remote add origin https://github.com/TEN-TAI-KHOAN/quyet-chien-voi-boss.git
git push -u origin main
```

`.gitignore` đã chặn sẵn các file `.docx`, `.pdf`, `.xlsx` để đề thi không vô tình bị đưa lên GitHub công khai.

## Deploy lên Vercel

1. Vào [vercel.com](https://vercel.com) → **Add New… → Project** → chọn repo `quyet-chien-voi-boss` → **Import**.
2. Ở màn hình cấu hình:
   - **Framework Preset:** `Other`
   - **Build Command:** để trống
   - **Output Directory:** để trống (hoặc `.`)
   - **Install Command:** để trống
3. Bấm **Deploy**. Sau khoảng 30 giây sẽ có địa chỉ dạng `https://quyet-chien-voi-boss.vercel.app`.
4. Mỗi lần `git push` lên nhánh `main`, Vercel tự cập nhật bản mới.

## Ghi chú

- Bản trên Vercel và bản mở bằng file là **hai nơi lưu khác nhau**: đề đã nhập ở bản này không tự sang bản kia.
- File `.doc` (Word 97–2003) chưa đọc được: mở bằng Word rồi *Lưu thành* `.docx`.
- Hình vẽ dạng WMF/EMF (không phải công thức) không hiển thị được trên trình duyệt và sẽ bị bỏ qua khi nhập.
- Thông tin thư viện bên thứ ba: xem `THIRD_PARTY_NOTICES.md`.
