# Phân tích bộ dữ liệu Heart Disease (Cleveland)

**Phụ trách:** Nguyễn Hoàng Anh — **MSSV: 2410064**

> Phần này là bản thảo riêng cho bộ dữ liệu Heart Disease. Các số liệu được đánh dấu bằng mã notebook sẽ được điền từ lần chạy `notebooks/02_heart_disease.ipynb` trên tệp dữ liệu gốc; không suy đoán kết quả khi tệp chưa có trong workspace.

## 1. Mô tả dữ liệu và mục tiêu phân tích

Heart Disease là bộ dữ liệu y khoa đa biến của UCI Machine Learning Repository. Bản Cleveland được dùng trong bài này có 303 quan sát, 13 đặc trưng đầu vào và biến đích `num`. Theo mô tả UCI, `num` có các giá trị 0–4; các phân tích trên bản Cleveland thường gộp 1–4 thành nhóm có bệnh và so sánh với nhóm 0. UCI ghi nhận dữ liệu có giá trị thiếu. Bài toán phù hợp là phân loại, nhưng lab này tập trung vào chất lượng dữ liệu, thống kê mô tả và PCA, không yêu cầu huấn luyện bộ phân loại.

| Nội dung | Mô tả |
|---|---|
| Nguồn | [UCI Machine Learning Repository — Heart Disease](https://archive.ics.uci.edu/dataset/45/heart+disease) |
| Tập con | Cleveland, tệp `processed.cleveland.data` |
| Kích thước theo mô tả nguồn | 303 quan sát; 13 đặc trưng đầu vào |
| Biến gốc | 13 đầu vào và `num` (mức chẩn đoán 0–4) |
| Nhãn dùng để diễn giải | `disease_label = 0` nếu `num = 0`; `1` nếu `num > 0` |
| Bài toán phù hợp | Phân loại nhị phân hoặc đa lớp; PCA trong bài chỉ dùng để giảm chiều và trực quan hóa |

Không ghép các hàng Heart Disease với Wine Quality: hai bộ dữ liệu mô tả đối tượng và phép đo khác nhau, không có khóa chung để nối. Tích hợp rượu đỏ/trắng là thao tác riêng trong bộ Wine Quality; ở phần so sánh chung, hai bộ được đối chiếu qua kết quả phân tích và PCA.

## 2. Phân loại đặc trưng

Các mã số như `cp`, `restecg`, `slope` và `thal` biểu diễn nhóm/loại, không phải đại lượng có khoảng cách số học đồng đều. Vì vậy, chúng được xem là biến phân loại và one-hot encode trước PCA. `ca` là số lượng mạch lớn được quan sát bằng huỳnh quang, nên được giữ như một biến đếm định lượng và chuẩn hóa cùng các biến số khác.

| Biến | Ý nghĩa | Kiểu dữ liệu và thang đo | Vai trò | Xử lý cho PCA |
|---|---|---|---|---|
| `age` | Tuổi (năm) | Định lượng, số; liên tục về ý nghĩa, ghi theo số nguyên | Đầu vào | Chuẩn hóa |
| `sex` | Giới tính (0 = nữ, 1 = nam) | Định tính, phân loại nhị phân | Đầu vào | One-hot |
| `cp` | Loại đau ngực: 1 điển hình, 2 không điển hình, 3 không do đau thắt ngực, 4 không triệu chứng | Định tính, phân loại danh nghĩa | Đầu vào | One-hot |
| `trestbps` | Huyết áp lúc nghỉ (mm Hg) | Định lượng, số; liên tục | Đầu vào | Chuẩn hóa |
| `chol` | Cholesterol huyết thanh (mg/dl) | Định lượng, số; liên tục | Đầu vào | Chuẩn hóa |
| `fbs` | Đường huyết lúc đói > 120 mg/dl (0/1) | Định tính, phân loại nhị phân | Đầu vào | One-hot |
| `restecg` | ECG lúc nghỉ: 0 bình thường, 1 bất thường ST-T, 2 phì đại thất trái | Định tính, phân loại danh nghĩa | Đầu vào | One-hot |
| `thalach` | Nhịp tim tối đa đạt được | Định lượng, số; liên tục | Đầu vào | Chuẩn hóa |
| `exang` | Đau thắt ngực do gắng sức (0/1) | Định tính, phân loại nhị phân | Đầu vào | One-hot |
| `oldpeak` | ST depression do gắng sức so với lúc nghỉ | Định lượng, số; liên tục | Đầu vào | Chuẩn hóa |
| `slope` | Độ dốc ST: 1 đi lên, 2 phẳng, 3 đi xuống | Định tính, phân loại có thứ tự | Đầu vào | One-hot để không giả định khoảng cách tuyến tính |
| `ca` | Số mạch chính hiện màu khi soi huỳnh quang (0–3) | Định lượng rời rạc, biến đếm | Đầu vào | Chuẩn hóa |
| `thal` | Kết quả thal: 3 bình thường, 6 khuyết tật cố định, 7 khuyết tật có thể đảo ngược | Định tính, phân loại danh nghĩa | Đầu vào | One-hot |
| `num` | Mức chẩn đoán bệnh (0–4) | Nhãn thứ bậc, mã số phân loại | Mục tiêu | Không đưa vào PCA |

## 3. Chất lượng dữ liệu và làm sạch

Tệp Cleveland dùng `?` để biểu diễn một số giá trị thiếu. Notebook chuyển dấu này thành null, ép các cột về kiểu số và kiểm tra miền giá trị theo từ điển UCI. Các giá trị sai miền được chuyển thành thiếu trước khi điền; hàng trùng hoàn toàn được loại một lần; hàng thiếu nhãn đích (nếu có) bị loại vì không thể suy ra nhãn. Biến số được điền bằng trung vị, biến phân loại bằng mode. Các quyết định này được ghi thành bảng trong notebook để số liệu trước/sau có thể kiểm tra lại.

Ngoại lệ được gắn cờ bằng quy tắc IQR trên các biến số, nhưng không tự động xóa. Một điểm nằm ngoài 1,5 IQR không nhất thiết là lỗi đo; xóa hàng có thể làm mất các trường hợp lâm sàng cực trị. Chỉ giá trị vi phạm quy tắc miền được xử lý như giá trị lỗi.

| Chỉ tiêu | Trước làm sạch | Sau làm sạch | Ghi chú |
|---|---:|---:|---|
| Số hàng | 303 theo nguồn; xác nhận từ tệp | Chạy notebook để điền | Hàng trùng hoặc thiếu nhãn có thể bị loại |
| Số cột nguồn | 14 | 14 | Gồm 13 đầu vào và `num`; nhãn nhị phân phát sinh chỉ dùng để diễn giải |
| Ô thiếu (`?`/null) | Chạy notebook để điền | 0 trong đầu vào sau điền | `num` không được impute |
| Hàng trùng hoàn toàn | Chạy notebook để điền | 0 | Giữ lần xuất hiện đầu tiên |
| Giá trị ngoài miền | Chạy notebook để điền | 0 trong các cột đầu vào sau xử lý | Ngoài miền được chuyển thành thiếu rồi impute |
| Hàng có ít nhất một ngoại lệ IQR | Chạy notebook để điền | Chạy notebook để điền | Cờ kiểm tra, không tự động xóa |

## 4. Thống kê mô tả và phân tích biến phân loại

Notebook tính trung bình và phương sai mẫu cho các biến định lượng, ma trận hiệp phương sai và Pearson correlation giữa `age`, `trestbps`, `chol`, `thalach`, `oldpeak`, `ca`. Pearson chỉ được diễn giải cho nhóm biến định lượng này; không tính tương quan Pearson trên các mã danh nghĩa như `cp` hoặc `thal`.

| Kết quả cần báo cáo | Giá trị |
|---|---|
| Biến có tương quan Pearson mạnh nhất theo trị tuyệt đối (không tính đường chéo) | Chạy notebook để điền |
| Hệ số tương quan của cặp mạnh nhất | Chạy notebook để điền |
| Kiểm định liên hệ giữa từng biến phân loại và `disease_label` | Bảng chi-square/Cramér's V do notebook sinh |

Tần suất từng mức của biến phân loại và bảng chéo theo nhãn bệnh giúp mô tả phân bố của mẫu. Cramér's V được dùng như thước đo độ lớn liên hệ cho biến phân loại; p-value chi-square được xem là kết quả khám phá trên bộ dữ liệu nhỏ, không phải bằng chứng nhân quả.

## 5. Tiền xử lý và phương pháp PCA

PCA nhạy với thang đo, nên sáu biến số được chuẩn hóa bằng z-score. Bảy biến phân loại được mã hóa one-hot để không tạo thứ tự giả giữa các mã danh nghĩa. One-hot columns được giữ ở thang 0/1; đây là lựa chọn có chủ đích để các biến liên tục có phương sai đơn vị sau chuẩn hóa, còn biến nhị phân/phân loại đóng góp theo tần suất nhóm. Báo cáo cần nêu rõ PCA vì thế áp dụng lên ma trận gồm các biến số chuẩn hóa và các cột one-hot, không phải 13 cột số nguyên chưa xử lý.

`num` và `disease_label` bị loại khỏi ma trận đầu vào PCA. PCA được tính bằng phân rã SVD trên ma trận đã tiền xử lý. Thành phần đầu giữ phương sai lớn nhất; các thành phần sau tối ưu phần phương sai còn lại dưới điều kiện trực giao. Số thành phần được xem xét ở k = 2, 3, 5 và theo các ngưỡng phương sai tích lũy 80%, 90%, 95%. So sánh này mô tả cấu trúc dữ liệu, không phải đánh giá hiệu năng dự đoán.

## 6. Kết quả PCA và trực quan hóa

Các bảng và hình bên dưới do notebook tạo sau khi chạy trên dữ liệu gốc:

- Bảng phương sai giải thích riêng lẻ và tích lũy cho từng PC.
- Bảng số thành phần tối thiểu để đạt 80%, 90% và 95% phương sai tích lũy.
- Bảng so sánh k = 2, 3, 5 và các ngưỡng trên, kèm số chiều sau mã hóa, tỷ lệ phương sai giữ lại và sai số tái tạo.
- Scree plot và biểu đồ PC1–PC2 tô màu theo nhãn `không bệnh` / `có bệnh`.
- Bảng các đặc trưng có loading lớn nhất trên PC1 và PC2 để hỗ trợ diễn giải.

| Chỉ số | Kết quả |
|---|---:|
| Số cột sau mã hóa trước PCA | Chạy notebook để điền |
| Phương sai tích lũy của PC1–PC2 | Chạy notebook để điền |
| Số PC đạt ít nhất 80% | Chạy notebook để điền |
| Số PC đạt ít nhất 90% | Chạy notebook để điền |
| Số PC đạt ít nhất 95% | Chạy notebook để điền |

Khi diễn giải, cần lưu ý PCA tối đa hóa phương sai chứ không tối ưu phân tách nhãn bệnh. Nếu hai màu chồng lấn trên PC1–PC2, điều đó chỉ nói rằng phép chiếu hai chiều không tách rõ nhóm; không chứng minh rằng dữ liệu không chứa thông tin liên quan đến nhãn. Dấu của mỗi PC có thể đảo mà không làm thay đổi nghiệm.

## 7. Kết luận và giới hạn

Sau khi chạy notebook, phần này sẽ tổng hợp số mẫu còn lại, các quyết định làm sạch, cặp tương quan mạnh nhất và số PC cần thiết cho các ngưỡng phương sai. Giới hạn cần nêu gồm kích thước nhỏ của tập Cleveland, tuổi đời và tính đại diện hạn chế của dữ liệu, cách mã hóa biến phân loại, độ nhạy của PCA với ngoại lệ, cùng việc phương sai lớn không đồng nghĩa với giá trị dự đoán lớn. Kết quả là phân tích học thuật trên bộ dữ liệu công khai, không phải kết luận lâm sàng.

## Tài liệu tham khảo

Janosi, A., Steinbrunn, W., Pfisterer, M., & Detrano, R. (1989). *Heart Disease* [Dataset]. UCI Machine Learning Repository. [https://doi.org/10.24432/C52P4X](https://doi.org/10.24432/C52P4X). Dữ liệu: [UCI Heart Disease](https://archive.ics.uci.edu/dataset/45/heart+disease).

## Tài liệu tái lập

Phân tích, bảng và hình trong phần này được tạo bởi [`../notebooks/02_heart_disease.ipynb`](../notebooks/02_heart_disease.ipynb). Hình đầu ra có tiền tố `heart_` trong `report/figures/`; bảng đầu ra có tiền tố `heart_` trong `report/tables/`.
