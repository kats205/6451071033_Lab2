# 6451071033_Lab2 — Khai phá dữ liệu (Data Mining) — LAB 2

Tổng hợp các bài thực hành **LAB 2** môn **Khai phá dữ liệu (Data Mining)** về chủ đề **Phân lớp dữ liệu (Classification)** với ba giải thuật **ID3** (*Information Gain / Entropy*), **CART** (*Gini Index*) và **Naïve Bayes** (`GaussianNB` & Categorical Naïve Bayes làm trơn Laplace $\alpha = 1$), bao gồm phần **Yêu cầu lập trình & Thực hành** (Bài 2, 4, 5, 6, 7) và **Bài tập thêm — Tính giá trị F-measure các bài tập cơ bản** (Bài 2, Trang 32).

## Thông tin sinh viên

- **Họ và tên:** Nguyễn Phạm Bảo Khanh
- **MSSV:** `6451071033`
- **Môn học:** Khai phá dữ liệu (Data Mining)
- **Repository:** [https://github.com/kats205/6451071033_Lab2](https://github.com/kats205/6451071033_Lab2)

---

## Danh sách bài thực hành

### Phần III & IV: Yêu cầu lập trình & Thực hành phân lớp (ID3, CART & Naïve Bayes)

| Bài | Notebook | Tài liệu tham chiếu | Tập dữ liệu | Nội dung & Kết quả chính |
|---|---|---|---|---|
| **Bài 2** | [`6451071033_LAB2_Bai2.ipynb`](./6451071033_LAB2_Bai2.ipynb) | Phần III — Trang 15–16 | `adult.data.csv` (`32.561 × 15`) & `adult.test.csv` (`16.281 × 14`) | Thực hiện Câu 1–10 dự đoán thu nhập (`<=50K` / `>50K`): làm sạch khoảng trắng chuỗi bằng `skipinitialspace=True` và `.str.strip()`, loại bỏ các dòng chứa `'?'` (`2.399` dòng huấn luyện, `1.221` dòng kiểm thử) và bỏ cột `fnlwgt`, nối thành bảng `45.222 × 14` (`30.162` train / `15.060` test). Hệ số tương quan Pearson tuyệt đối lớn nhất ngoài đường chéo là `0.1462` → giữ toàn bộ `14` cột; mã hóa One-Hot `8` cột phân loại thành `(45.222, 103)`. **ID3** (`random_state=0`, sâu `51`, `5.327` lá) đạt Accuracy cao nhất **`81.75%`** (`0.8175`, Macro F1 `0.7518`), **CART** (`random_state=0`, sâu `46`, `5.331` lá) đạt **`81.23%`** (`0.8123`, Macro F1 `0.7438`), và **GaussianNB** đạt **`80.29%`** (`0.8029`) nhưng có Macro F1 (`0.7649`), Recall(`>50K`) (`0.8159`) và F1(`>50K`) (`0.6704`) cao nhất. |
| **Bài 4** | [`6451071033_LAB2_Bai4.ipynb`](./6451071033_LAB2_Bai4.ipynb) | Phần IV — Trang 26 | `winequality-red.csv` (`1.599 × 12`) | Thực hiện Câu 3–10 phân lớp `6` mức `quality` (`3`–`8`, mất cân bằng mạnh với lớp `5`: `681` và lớp `6`: `638` chiếm `82.5%`). Tương quan Pearson lớn nhất là `r = -0.6830` (`fixed acidity`–`pH`, trị tuyệt đối `< 0.7`) → giữ đủ `11` đặc trưng số (`1.599 × 11`); chia 70/30 (`random_state=42`): `1.119` train / `480` test. **ID3** (`random_state=42`, sâu `18`, `272` lá) dẫn đầu với Accuracy **`59.79%`** (`0.5979`, Macro F1 `0.3662`, Weighted F1 `0.6026`), tiếp theo là **CART** (`random_state=42`, sâu `19`, `288` lá) đạt **`57.29%`** (`0.5729`, Macro F1 `0.3274`, Weighted F1 `0.5704`), và **GaussianNB** đạt **`54.17%`** (`0.5417`, Macro F1 `0.2890`, Weighted F1 `0.5433`). |
| **Bài 5** | [`6451071033_LAB2_Bai5.ipynb`](./6451071033_LAB2_Bai5.ipynb) | Phần IV — Trang 26–27 | `heart.csv` (`303 × 14`) | Thực hiện Câu a) & Câu 3–10 chẩn đoán bệnh tim (`target`: `0` = `138` mẫu, `1` = `165` mẫu): kiểm tra `dropna()` giữ nguyên `303` dòng (`0` NaN), đổi tên đủ `14` cột theo đề (`age`, `sex`, `chest_pain_type`, ..., `thalassemia`, `target`). Tương quan Pearson lớn nhất là `r = -0.5775` (`st_depression`–`st_slope`, trị tuyệt đối `< 0.7`) → giữ đủ `13` đặc trưng số (`303 × 13`); chia 70/30 (`random_state=42`): `212` train / `91` test. **GaussianNB** vượt trội rõ rệt trên tập mẫu nhỏ với Accuracy **`83.52%`** (`0.8352`, Macro F1 `0.8348`, Weighted F1 `0.8356`, Recall lớp `1` = `0.80`, giảm `FN = 10`), vượt **CART** (`random_state=42`, sâu `9`, `37` lá: **`73.63%`**, Macro F1 `0.7360`) và **ID3** (`random_state=42`, sâu `7`, `33` lá: **`69.23%`**, Macro F1 `0.6914`). |
| **Bài 6** | [`6451071033_LAB2_Bai6.ipynb`](./6451071033_LAB2_Bai6.ipynb) | Phần IV — Trang 27 | `mushrooms.csv` (`8.124 × 23`) | Thực hiện Câu 4–10 phân lớp nấm ăn được (`e`: `4.208`) và nấm độc (`p`: `3.916`); giữ nguyên `'?'` ở cột `stalk-root` (`2.480` dòng) như một giá trị phân loại hợp lệ, mã hóa One-Hot `22` cột phân loại thành `(8.124, 117)`; chia 70/30 (`random_state=42`): `5.686` train / `2.438` test (`e`: `1.257`, `p`: `1.181`). Cả **ID3** (`random_state=42`, sâu `5`, `11` lá) và **CART** (`random_state=42`, sâu `7`, `14` lá) đều đạt **`100.00%`** (`1.0000`, `0` mẫu sai); **GaussianNB** đạt **`96.43%`** (`0.9643`, Macro F1 `0.9643`, sai `87` mẫu: `FP = 86` `e→p`, `FN = 1` `p→e`, Recall(`p`) = `0.9992`) do giả định độc lập và phân phối chuẩn không khớp với các cột one-hot nhị phân. |
| **Bài 7** | [`6451071033_LAB2_Bai7.ipynb`](./6451071033_LAB2_Bai7.ipynb) | Phần IV — Trang 27–31 | `load_digits()` (`1.797` ảnh `8×8`) & `test_image_Bai7_1.jpg`, `test_image_Bai7_2.jpg` | Nhận dạng chữ số viết tay `0–9`: làm phẳng ảnh `8×8` (`0..16`) thành vector `(1.797, 64)`, chia 80/20 không xáo trộn (`test_size=0.2, shuffle=False`: `1.437` train / `360` test); hiệu chỉnh lát cắt `digits.images[-len(X_test):]` khớp `X_test` và dùng `ConfusionMatrixDisplay.from_estimator`. Mô hình **ID3** (`criterion="entropy"`, `random_state=33`, sâu `10`, `113` lá) đạt Accuracy **`79.72%`** (`0.7972`, Macro F1 `0.79`, Weighted F1 `0.79`; tốt nhất ở số `6` với F1 = `0.96`). Kiểm thử trên `2` ảnh viết tay thực tế từ Google Drive (chuyển xám, resize `8×8`, đảo màu `ImageOps.invert`, lọc ngưỡng `> 109 → 155`, `< 110 → 0`) cho dự đoán **chính xác cả hai ảnh**: `test_image_Bai7_1.jpg` → **`1`** và `test_image_Bai7_2.jpg` → **`2`** (trùng khớp với thang nhị phân `0/16`). |

### Phần V: Bài tập thêm — Tính giá trị F-measure của các bài tập cơ bản

| Bài | Notebook | Tài liệu tham chiếu | Tập dữ liệu | Nội dung & Kết quả chính |
|---|---|---|---|---|
| **Bài 2 (Trang 32)** | [`6451071033_LAB2_Bai2_Trang32.ipynb`](./6451071033_LAB2_Bai2_Trang32.ipynb) | Phần V — Trang 32 | 3 bộ dữ liệu cơ bản (tự chứa trong notebook):<br>• **III.1 Credit Risk** (`15` train / `3` test)<br>• **IV.1 Doanh số đồ chơi** (`15` train / `3` test + Yêu cầu `l`)<br>• **IV.2 Phân tích cảm xúc** (`14` train / `4` test) | Tự cài đặt **ID3** (*Information Gain*), **CART** (*Multi-way Categorical Gini*) và **Categorical Naïve Bayes** (làm trơn Laplace $\alpha = 1$), lập ma trận nhầm lẫn và tính Precision, Recall, **F-measure ($F_1$)** (`0` dòng mâu thuẫn trên cả 3 tập):<br>• **III.1 Credit Risk** (`+`: `'Rủi ro thấp'`): **ID3 & CART** đạt Precision `0.6667` (`2/3`), Recall `1.0000`, `F1('Rủi ro thấp') = 0.8000` (Macro F1 `0.4000`, Weighted F1 `0.5333`, Accuracy `0.6667`); **Naïve Bayes** đạt `F1('Rủi ro thấp') = 1.0000`, `Macro F1 = 1.0000`, `Accuracy = 1.0000` (khớp 100% tài liệu PDF trang 11 & 15).<br>• **IV.1 Doanh số đồ chơi** (phá hòa theo thứ tự cột): **ID3 & CART** đạt Accuracy `0.6667`, `F1('Thấp') = 0.8000`, `F1('Cao') = 0.0000`, Macro F1 `0.4000`, Weighted F1 `0.5333` (Yêu cầu `l`: `Cao`); **Naïve Bayes** đạt Accuracy `0.3333`, `F1('Thấp') = 0.5000`, `F1('Cao') = 0.0000`, Macro F1 `0.2500`, Weighted F1 `0.3333` (Yêu cầu `l`: `Thấp`).<br>• **IV.2 Phân tích cảm xúc** (ma trận `3×3`): **ID3 & CART** gặp `6` nút đồng hạng Gini (trong `120` cây đồng hạng, Macro F1 từ `0.1667` đến `1.0000`), theo thứ tự cột đạt Accuracy `0.5000`, `F1('tốt') = 0.8000`, `F1('xấu'/'bình thường') = 0.0000`, Macro F1 `0.2667`, Weighted F1 `0.4000`; **Naïve Bayes** đạt `F1 = 1.0000` trên cả `3` lớp (`Accuracy = 1.0000`, `Macro F1 = 1.0000`, `Weighted F1 = 1.0000`). |

---

## Cấu trúc thư mục

```text
6451071033_Lab2/
├── Link truy cập dataset.txt
├── README.md
├── 6451071033_LAB2_Bai2.ipynb
├── 6451071033_LAB2_Bai4.ipynb
├── 6451071033_LAB2_Bai5.ipynb
├── 6451071033_LAB2_Bai6.ipynb
├── 6451071033_LAB2_Bai7.ipynb
├── 6451071033_LAB2_Bai2_Trang32.ipynb
└── Dataset/                      # Dữ liệu cục bộ (không đẩy lên Git; tự tải hoặc tải thủ công từ Drive)
    ├── adult.data.csv
    ├── adult.test.csv
    ├── heart.csv
    ├── Link dataset bài 7.txt
    ├── mushrooms.csv
    ├── test_image_Bai7.jpg
    ├── test_image_Bai7_1.jpg
    ├── test_image_Bai7_2.jpg
    └── winequality-red.csv
```

> **Lưu ý khi đẩy mã nguồn lên Git:** Thư mục `Dataset/`, tài liệu PDF khóa học (`Tài liệu LAB2.pdf`), tệp báo cáo Word (`*.docx`, `~$*`) và các thư mục/tệp tạm (`.ipynb_checkpoints/`, `__pycache__/`, `*.tmp`) nên được loại trừ (ví dụ khai báo trong `.gitignore` trước khi commit) để giữ repository gọn nhẹ.

---

## Nguồn dữ liệu (Dataset)

Toàn bộ bộ dữ liệu thực hành của LAB 2 được lưu tại Google Drive (xem thêm trong [`Link truy cập dataset.txt`](./Link%20truy%20c%E1%BA%ADp%20dataset.txt)):

- **Google Drive:** [Thư mục Dataset LAB 2](https://drive.google.com/drive/folders/1KK--zL3h4hWrfIl--FIcrww3dLx-epiB?usp=sharing)

Các notebook sử dụng dữ liệu ngoài (`Bai2`, `Bai4`, `Bai5`, `Bai6`, `Bai7`) đều tích hợp sẵn hàm `get_dataset_path(...)` hỗ trợ chạy linh hoạt theo thứ tự ưu tiên:
1. Đọc trực tiếp từ thư mục cục bộ `./Dataset/` nếu đã có sẵn.
2. Nếu chạy trên **Google Colab**, tự động mount Google Drive và tìm trong `/content/drive/MyDrive/Dataset/`.
3. Nếu chưa có ở cả hai nơi trên, tự động tải từ Google Drive bằng `gdown` (`--folder` cho thư mục `Dataset`, hoặc tải trực tiếp theo `gdrive_file_id` đối với ảnh kiểm thử ở Bài 7).

*(Riêng `6451071033_LAB2_Bai2_Trang32.ipynb` chứa trực tiếp dữ liệu bảng của 3 bài tập cơ bản ngay trong mã nguồn nên không cần tệp ngoài.)*

> **Ghi chú về ảnh kiểm thử Bài 7 (`test_image_Bai7_1.jpg` & `test_image_Bai7_2.jpg`) và dữ liệu CSV:**
> - Trên thư mục Google Drive của LAB 2 có **hai tệp ảnh khác nhau nhưng trùng tên `test_image_Bai7.jpg`**: ảnh chữ số **`1`** (`412×411`, Drive ID `1BH2qwN62GKZIHcF0kUi0N13YG2eex3wx`, được lưu cục bộ là `Dataset/test_image_Bai7_1.jpg` kèm bản tương thích `Dataset/test_image_Bai7.jpg`) và ảnh chữ số **`2`** (`385×385`, Drive ID `1KU83z5OU2j69YBPI7uMPcLPSUxidd6Ia`, được lưu cục bộ là `Dataset/test_image_Bai7_2.jpg`). Hàm `get_dataset_path(..., fallback_filenames=..., gdrive_file_id=...)` trong Bài 7 tự động nạp đúng cả hai ảnh mà không bị ghi đè lẫn nhau.
> - Tệp `Dataset/Link dataset bài 7.txt` ghi đường dẫn nguồn MNIST (`https://github.com/cvdfoundation/mnist`); notebook Bài 7 sử dụng trực tiếp bộ `sklearn.datasets.load_digits()` (`1.797` ảnh `8×8`) theo hướng dẫn thực hành.
> - Các tệp CSV đều được xử lý đúng đặc thù định dạng trong từng notebook: `adult.data.csv` & `adult.test.csv` loại bỏ khoảng trắng đầu chuỗi (`skipinitialspace=True` + `.str.strip()`), `winequality-red.csv` phân tách bằng dấu phẩy `,`, `heart.csv` có UTF-8 BOM, và `mushrooms.csv` giữ nguyên giá trị `'?'` ở cột `stalk-root` (`2.480` dòng).

---

## Yêu cầu môi trường & Hướng dẫn chạy

### Thư viện sử dụng

Các notebook đã được chạy và kiểm chứng trên môi trường **Python 3.15.0** với các thư viện chính:

- `pandas` (`3.1.1`) & `numpy` (`2.5.5`)
- `scikit-learn` (`1.9.1`, `DecisionTreeClassifier`, `GaussianNB`, `train_test_split`, `metrics`, `datasets.load_digits`)
- `matplotlib` (`3.11.2`) & `seaborn` (`0.13.2`)
- `pillow` (`13.0.0`, đọc và tiền xử lý ảnh chữ số viết tay ở Bài 7)
- `gdown` (`6.4.2`, hỗ trợ tải dataset tự động từ Google Drive)

*(Mã nguồn đã được viết tương thích với `pandas 3.x` và `scikit-learn 1.9.x`, sử dụng `ConfusionMatrixDisplay.from_estimator` thay cho `plot_confusion_matrix` đã bị loại bỏ từ `scikit-learn 1.2`.)*

### Các bước chạy cục bộ

1. **Clone repository:**
   ```bash
   git clone https://github.com/kats205/6451071033_Lab2.git
   cd 6451071033_Lab2
   ```

2. **Cài đặt thư viện cần thiết:**
   ```bash
   pip install pandas numpy scikit-learn matplotlib seaborn pillow gdown jupyter
   ```

3. **Chuẩn bị dữ liệu (tùy chọn):**
   - Tải thư mục `Dataset` từ link Google Drive ở trên và đặt vào thư mục gốc của dự án (`./Dataset/`), **hoặc** chạy trực tiếp các notebook để `gdown` tự động tải về. Nếu tải thủ công cho Bài 7, lưu hai tệp `test_image_Bai7.jpg` trên Drive thành `Dataset/test_image_Bai7_1.jpg` (chữ số `1`) và `Dataset/test_image_Bai7_2.jpg` (chữ số `2`).

4. **Mở và chạy notebook:**
   - Mở bằng VS Code / JupyterLab / Jupyter Notebook, hoặc tải các tệp `.ipynb` lên **Google Colab** để chạy trực tiếp.
