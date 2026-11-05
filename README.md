# 📚 Beamer theme HPCA / PECLab

Theme Beamer LaTeX dựng lại từ template PowerPoint của PECLab / HPCA (Trường Điện – Điện tử, ĐH Bách khoa Hà Nội), hỗ trợ kích thước **16:9** và **4:3**.

## 📌 Slide powerpoint HPCA

- [Link template slide powerpoint.](https://drive.google.com/drive/folders/1zCpwRfRYwgJO5SkwVazsj9Tne1B6KyyT)

## 📌 Link Overleaf Project

- [Link Overleaf (chỉ xem, muốn sửa cần copy project).](https://www.overleaf.com/project/6aeaf462f59e426e6bf9e3e2/share#e27d23099b18f94c2c4d8d25b04c1641d9eb82c58b8ae70a)



## 1. Cấu trúc thư mục

```
HPCA_beamer/
├── beamerthemeHPCA.sty     <- theme (template slide)
├── Slide_HPCA.tex          <- file chính, nội dung slide (set as main document)
├── Slide_HPCA.pdf          <- kết quả mẫu 16:9
├── README.md               <- file hướng dẫn, chính là file này
└── images/
    ├── logo-peclab.png
    ├── logo-hpca.png
    ├── logo-seee.png
    └── logo-hust.png
```

File `.tex` của bạn phải nằm **cùng thư mục** với `beamerthemeHPCA.sty` và thư mục `images/`. Nếu chỉ có file `.tex` mà không có file `beamerthemeHPCA.sty` và thư mục `images/` thì compiler sẽ báo lỗi "theme và ảnh không tìm thấy "

## 🛠️ 2. Cách sử dụng và môi trường biên dịch 

- Có thể sử dụng các trình biên dịch online như Overleaf hoặc TexPage, hoặc tự setup cài đặt trình biên dịch trên máy (VD VS Code + LaTeX Workshop + TexLive/MikTeX hoặc TeXstudio/TexWork/TexMaker + TexLive/MikTeX).
- Với Overleaf, copy Project rồi sửa theo nhu cầu (do template gốc chỉ xem).
- ⚠️ **Quan trọng: Sử dụng compiler XeLaTeX hoặc LuaLaTeX** (theme dùng `fontspec`). Không compile được bằng pdfLaTeX.
- Các gói: `tikz`, `pifont`, `fontspec`, `fix-cm`. Đều có sẵn trong TeX Live và MiKTeX bản đầy đủ.
- Font: theme ưu tiên **Lato**. Nếu máy không có Lato thì tự dùng **Carlito** (giống Calibri). Nếu cả hai đều không có, LaTeX báo cảnh báo và dùng font mặc định.

> Theme được kiểm tra bằng **XeLaTeX**. LuaLaTeX chưa kiểm chứng được (môi trường thử không tìm thấy font hệ thống khi dùng LuaLaTeX), nếu gặp lỗi font thì dùng XeLaTeX.

## 🛠️ 3. Compile

- Với Overleaf, chỉ cần bấm compile 1 lần.

- Với local latex :

Chạy lại cho tới khi **không còn** cảnh báo `Label(s) may have changed. Rerun to get cross-references right`. Lần compile đầu tiên của một tài liệu có mục lục thường cần **3 lượt**:

```bash
xelatex Slide_HPCA.tex
xelatex Slide_HPCA.tex
xelatex Slide_HPCA.tex
```

Hoặc để `latexmk` tự lặp đủ số lần:

```bash
latexmk -xelatex Slide_HPCA.tex
```

Các lần compile sau (khi file `.aux` đã có sẵn) thường chỉ cần 1 lượt. Nếu đã chạy mà logo hoặc đường kẻ nền biến mất hoặc nằm sai chỗ, nghĩa là chưa đủ lượt, chạy thêm một lần.

Nếu dùng VS Code với LaTeX Workshop hoặc TeXstudio, đổi engine sang **XeLaTeX** (hoặc chọn recipe `latexmk (xelatex)`).

## 📦 4. Chọn tỉ lệ 16:9 hoặc 4:3

Chỉ cần đổi option của lớp `beamer`, theme tự nhận:

```latex
\documentclass[aspectratio=169,t,10pt]{beamer}   % 16:9  (mặc định của template gốc)
\documentclass[aspectratio=43,t,10pt]{beamer}    % 4:3
```

- Hai file PowerPoint gốc **cao bằng nhau** (19.05 cm), chỉ khác chiều rộng (33.87 cm và 25.4 cm). Vì vậy cỡ chữ và vị trí theo chiều dọc giống hệt nhau ở hai chế độ.
- Với `aspectratio=43`, theme **tự đặt khổ trang là 120 × 90 mm** (thay cho 128 × 96 mm mặc định của Beamer) để giữ đúng tỉ lệ cỡ chữ của template. PDF vẫn là 4:3, chỉ khác kích thước vật lý. Khi trình chiếu toàn màn hình thì không nhận ra khác biệt.
- Nếu không ghi `aspectratio`, Beamer mặc định là 4:3 nên theme sẽ dùng bộ số đo 4:3.
- Các tỉ lệ khác (`1610`, `149`...) vẫn chạy được vì mọi vị trí được đo từ mép trái, mép phải hoặc tâm trang, nhưng dùng bộ số đo 16:9 nên chưa được kiểm tra kỹ.
- Trên slide 4:3 tiêu đề dài và mục lục dài sẽ xuống dòng sớm hơn do trang hẹp hơn, giống như file PowerPoint 4:3 gốc.

File mẫu: `Slide_HPCA.tex` (16:9) và `Slide_HPCA_43.tex` (4:3), nội dung giống nhau.

- Khuyến cáo : nên sử dụng tỉ lệ 16:9 giúp bố cục đỡ rối hơn.

## 📦 5. Ví dụ bắt đầu nhanh

```latex
\documentclass[aspectratio=169,t,10pt]{beamer}   % nhớ có 't' để nội dung bám lên trên
\usetheme{HPCA}

\title{Nghiên cứu ứng dụng bộ biến đổi đa mức MMC trong hệ thống năng lượng tái tạo}
\hpcadoctype{LUẬN VĂN THẠC SĨ KHOA HỌC}
\hpcainfo{Học viên:}{Phạm Chí Hiếu}
\hpcainfo{Cán bộ hướng dẫn:}{TS. Phạm Việt Phương}

\begin{document}

\hpcatitlepage          % slide tiêu đề
\hpcatoc{Contents}      % slide mục lục

\section{Giới thiệu chung}
\begin{frame}{Tiêu đề slide}
  \begin{itemize}
    \item Nội dung
    \begin{itemize}
      \item Ý nhỏ
    \end{itemize}
  \end{itemize}
\end{frame}

\hpcaappendix{Appendix} % slide phụ lục

\end{document}
```

## 🗺️  6. Các lệnh của theme

| Lệnh | Tác dụng |
|---|---|
| `\hpcadoctype{...}` | Dòng in đậm phía trên tiêu đề (ví dụ loại luận văn). Bỏ trống thì không hiện. |
| `\hpcainfo{Nhãn:}{Giá trị}` | Thêm một dòng vào khối thông tin dưới tiêu đề. Gọi nhiều lần để thêm nhiều dòng. |
| `\hpcatitlepage` | Slide tiêu đề: logo PECLab, SEEE, Bách Khoa, HPCA. |
| `\hpcatoc{Tiêu đề}` | Slide mục lục: mỗi `\section` thành một ô số màu navy kèm thanh gradient xám. |
| `\begin{hpcaappendixframe}{Chữ}{Tiêu đề}` | Slide phụ lục **có nội dung**: khối navy bên trái, tiêu đề và nội dung ở vùng trắng bên phải. |
| `\hidesectionnumber` / `\showsectionnumber` | Tắt / bật ô số mục cạnh tiêu đề frame. |
| `\hidepagenumber` / `\showpagenumber` | Tắt / bật số trang. |

### Slide phụ lục có nội dung

`\hpcaappendix{Appendix}` chỉ tạo slide chia phần rỗng. Muốn thêm nội dung vào slide có khối navy, dùng môi trường `hpcaappendixframe`:

```latex
\hpcaappendix{Appendix}      % slide chia phần (tùy chọn)

\begin{hpcaappendixframe}{Appendix}{Chứng minh chi tiết}
  \begin{itemize}
    \item Nội dung bình thường: itemize, block, công thức, hình...
  \end{itemize}
\end{hpcaappendixframe}
```

- Tham số thứ nhất là chữ hiện trong khối navy, tham số thứ hai là tiêu đề frame (để trống `{}` nếu không cần).
- Tùy chọn của frame đặt trong ngoặc vuông trước tham số, ví dụ frame có code: `\begin{hpcaappendixframe}[fragile]{Appendix}{Code}`.
- Nội dung và tiêu đề bắt đầu từ bên phải khối navy. Frame thường đặt sau đó tự trở về lề cũ.
- Frame phụ lục không có ô số mục, nên không cần `\hidesectionnumber`.

### Ô số mục

Ô số navy cạnh tiêu đề frame lấy **tự động** từ số của `\section` hiện tại. Frame đặt trước `\section` đầu tiên thì không có ô số.

Nếu sau phần chính bạn còn frame thường mà không muốn ô số hiện (ví dụ các frame phụ lục dùng `frame` thông thường), đặt `\hidesectionnumber` trước các frame đó:

```latex
\hpcaappendix{Appendix}
\hidesectionnumber

\begin{frame}{Chứng minh chi tiết}
  ...
\end{frame}
```

Các frame dùng `hpcaappendixframe` không có ô số nên không cần lệnh này.

## 🌟 7. Tùy chỉnh

### Màu sắc

Các màu được định nghĩa ở đầu file `.sty`:

| Tên màu | Mã | Dùng cho |
|---|---|---|
| `hpcamain` | `002060` | Màu chủ đạo: chữ, ô số, khối Appendix, tiêu đề block |
| `hpcatocL` | `BBC0CC` | Đầu trái thanh gradient mục lục |
| `hpcatocR` | `F4F4F6` | Đầu phải thanh gradient mục lục |
| `hpcarule` | `7F7F7F` | Đường kẻ mảnh màu xám |


Muốn đổi, ghi đè trong file `.tex` **sau** `\usetheme{HPCA}`:

```latex
\usetheme{HPCA}
\definecolor{hpcamain}{HTML}{8B0000}
```

### Font

Mặc định là Lato (hoặc Carlito). Muốn dùng font khác, đặt **trước** `\usetheme`:

```latex
\newcommand{\hpcamainfont}{Calibri}
\usetheme{HPCA}
```

Tên font phải đúng như hệ điều hành đang cài.

### Cỡ chữ

Cỡ chữ quy đổi từ file PowerPoint (nhân 0.4724). Nếu thấy chưa vừa, chỉnh các dòng `\setbeamerfont` đầu file `.sty`, ví dụ:

```latex
\setbeamerfont{frametitle}{series=\bfseries,size*={13}{15}}
```

### Logo

Thay ảnh trong `images/` nhưng **giữ nguyên tên file**. Vị trí và kích thước logo chỉnh trong các lệnh `\hpca@footer` và `\hpca@titlebg` của file `.sty`.

## ⚠️ 8. Lưu ý và lỗi thường gặp

- **Báo lỗi No PDF và Fatal Package fontspec Error: The fontspec package requires either XeTeX or** : Chuyển compiler sang XeLaTeX thay vì pdfLaTeX trong phần cài đặt của Overleaf.
- **Mục lục trống hoặc chưa đúng:** chưa compile đủ lượt. Mục lục lấy từ các `\section` nên cần có ít nhất một `\section` trong tài liệu.
- **Logo, đường kẻ nền biến mất hoặc lệch vị trí:** chưa compile đủ lượt (xem mục 3), chạy thêm một lần cho tới khi hết cảnh báo `Rerun`.
- **`File 'logo-hpca.png' not found`:** thiếu thư mục `images/` hoặc file `.tex` không nằm cạnh nó.
- **`Font shape OML/cmm/m/it in size <13> not available`:** đã xử lý bằng gói `fix-cm` trong theme. Nếu vẫn gặp ở chỗ khác, kiểm tra xem bạn có load gói font toán nào khác không.
- **Chữ tiếng Việt mất dấu hoặc lỗi font:** đảm bảo compile bằng XeLaTeX hoặc LuaLaTeX, và file lưu ở mã hóa UTF-8.
- **Frame quá dài:** nội dung vượt vùng sẽ tràn xuống logo chân trang. Vùng nội dung rộng khoảng 32 cm × 16 cm trên khổ gốc.

## ⚠️ 9. Hạn chế

- Bản màu khác (chỉ có màu navy).
- Có thể vượt thời gian compile cho phép của Overleaf (yêu cầu nâng cấp).

