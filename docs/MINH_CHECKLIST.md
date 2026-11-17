# Checklist cá nhân - Nguyễn Hoàng Minh

## 1. Mục tiêu và đầu ra chính

Nguyễn Hoàng Minh phụ trách toàn bộ quy trình phân tích **Wine Quality**, từ dữ liệu gốc đến kết quả PCA, đồng thời phụ trách tích hợp repository và tổng hợp báo cáo cuối.

Các đầu ra bắt buộc:

- [ ] `notebooks/01_wine_quality.ipynb` chạy được từ đầu đến cuối.
- [ ] Bảng mô tả và phân loại các feature của Wine Quality.
- [ ] Bảng so sánh dữ liệu trước và sau cleaning.
- [ ] Bảng mean, variance và covariance.
- [ ] Correlation heatmap và cặp feature tương quan mạnh nhất.
- [ ] Explained-variance plot và cumulative-variance plot.
- [ ] Bảng so sánh số lượng principal components.
- [ ] Biểu đồ PCA 2D theo `quality` và/hoặc `wine_type`.
- [ ] Nội dung Wine Quality để đưa vào báo cáo.
- [ ] Repository và bản PDF cuối được sắp xếp, kiểm tra đầy đủ.

## 2. Chuẩn bị môi trường và Git

- [ ] Clone/pull phiên bản mới nhất của repository.
- [ ] Tạo và kích hoạt virtual environment.
- [ ] Cài đặt thư viện bằng `pip install -r requirements.txt`.
- [ ] Tạo branch `analysis/wine-quality` trước khi bắt đầu notebook phân tích.
- [ ] Không commit `.venv`, cache, dữ liệu raw hoặc file tạm.
- [ ] Commit theo từng nhóm công việc thay vì dồn tất cả vào một commit.

Kết quả cần đạt: Jupyter hoạt động và notebook có thể import `pandas`, `numpy`, `matplotlib`, `seaborn` và `scikit-learn`.

## 3. Thu thập và tích hợp Wine Quality

Nguồn chính thức: <https://archive.ics.uci.edu/dataset/186/wine+quality>

- [ ] Tải `winequality-red.csv`.
- [ ] Tải `winequality-white.csv`.
- [ ] Đặt hai file trong `data/raw/` nhưng không commit lên Git.
- [ ] Đọc đúng delimiter của file và kiểm tra tên cột.
- [ ] Thêm `wine_type = "red"` cho dữ liệu rượu đỏ.
- [ ] Thêm `wine_type = "white"` cho dữ liệu rượu trắng.
- [ ] Kiểm tra hai file có cùng schema trước khi ghép.
- [ ] Ghép hai file theo chiều dọc bằng `pd.concat`.
- [ ] Ghi lại số dòng/cột của từng file và dữ liệu sau khi ghép.
- [ ] Giải thích lợi ích và khó khăn của data integration.

Lưu ý: không ép số dòng về một con số kỳ vọng. Nếu số lượng khác mô tả nguồn, phải kiểm tra file và ghi lại lý do.

## 4. Mô tả và phân loại feature

- [ ] Viết mô tả ngắn về mục đích và nguồn gốc dataset.
- [ ] Xác định 11 feature hóa lý là input cho PCA.
- [ ] Xác định `quality` là target dạng điểm rời rạc/ordinal.
- [ ] Xác định `wine_type` là biến categorical nominal được thêm khi tích hợp.
- [ ] Tạo bảng gồm: tên cột, ý nghĩa, role, kiểu dữ liệu và loại feature.
- [ ] Nêu dataset có thể hỗ trợ regression hoặc classification tùy cách xử lý `quality`.

Kết quả cần đạt: một bảng feature có thể đưa trực tiếp vào báo cáo.

## 5. Data-quality audit

Thực hiện kiểm tra trên từng file và trên dữ liệu đã tích hợp.

- [ ] Kiểm tra shape và data type.
- [ ] Đếm missing values theo cột.
- [ ] Đếm số dòng duplicate hoàn toàn.
- [ ] Kiểm tra giá trị vô hạn và giá trị không parse được thành số.
- [ ] Kiểm tra miền hợp lý của `quality` và `wine_type`.
- [ ] Kiểm tra thống kê min/max để phát hiện giá trị đáng ngờ.
- [ ] Phát hiện outlier của 11 feature số bằng IQR.
- [ ] Vẽ boxplot cho các feature quan trọng hoặc có nhiều outlier.
- [ ] Giải thích missing, duplicate, invalid value và outlier có thể ảnh hưởng tới mean, variance, correlation và PCA như thế nào.

Không được tự động xóa mọi outlier. Trước tiên phải phân biệt giữa lỗi dữ liệu và phép đo hóa học cực trị nhưng hợp lệ.

## 6. Cleaning và bảng trước/sau

- [ ] Quyết định cách xử lý missing nếu có và giải thích lý do.
- [ ] Quyết định cách xử lý duplicate; nêu rõ giữ hay xóa và vì sao.
- [ ] Xử lý giá trị sai/không hợp lệ nếu phát hiện được.
- [ ] Quyết định giữ, loại bỏ hoặc giới hạn outlier dựa trên ngữ cảnh.
- [ ] Không chỉnh sửa trực tiếp file raw.
- [ ] Lưu logic cleaning trong notebook để có thể tái lập.
- [ ] Tạo bảng before/after gồm ít nhất:
  - số dòng;
  - số cột;
  - tổng missing values;
  - số duplicate;
  - số invalid values;
  - số outlier được phát hiện/xử lý.
- [ ] Viết nhận xét về tác động của cleaning tới độ tin cậy của phân tích.

Kết quả cần đạt: người đọc biết chính xác dữ liệu đã thay đổi ở đâu và vì sao.

## 7. Thống kê mô tả và categorical analysis

- [ ] Tính mean cho 11 input numerical features.
- [ ] Tính sample variance cho 11 input numerical features.
- [ ] Tính covariance matrix.
- [ ] Tính correlation matrix.
- [ ] Tạo bảng tần suất của `wine_type`.
- [ ] Tạo bảng tần suất của `quality`.
- [ ] Tạo contingency table giữa `wine_type` và `quality`.
- [ ] Sử dụng chi-square và/hoặc Cramer's V để phân tích quan hệ categorical nếu phù hợp.
- [ ] Giải thích vì sao không sử dụng Pearson correlation trực tiếp cho `wine_type` dạng chữ.

Nếu bảng covariance quá lớn, chỉ đưa phần cần thiết vào báo cáo và dùng notebook làm nguồn kết quả đầy đủ.

## 8. Correlation analysis

- [ ] Bỏ đường chéo tự tương quan bằng 1 khi tìm cặp mạnh nhất.
- [ ] Tìm cặp feature có trị tuyệt đối của correlation lớn nhất.
- [ ] Báo cáo tên hai feature, hệ số, độ mạnh và chiều dương/âm.
- [ ] Vẽ heatmap rõ ràng cho 11 input features.
- [ ] Viết ít nhất 2-3 nhận xét có liên hệ với ý nghĩa hóa học hoặc chất lượng rượu.
- [ ] Không kết luận quan hệ nhân quả chỉ dựa trên correlation.

Đầu ra gợi ý: `report/figures/wine_correlation_heatmap.png`.

## 9. Chuẩn bị dữ liệu cho PCA

- [ ] Tạo ma trận `X` chỉ gồm 11 feature hóa lý.
- [ ] Tách `quality` và `wine_type` để dùng làm nhãn trực quan hóa.
- [ ] Xác nhận target không xuất hiện trong `X`.
- [ ] Chuẩn hóa `X` bằng `StandardScaler`.
- [ ] Kiểm tra mean xấp xỉ 0 và standard deviation xấp xỉ 1 sau chuẩn hóa.
- [ ] Giải thích vì sao PCA cần standardization khi các feature có đơn vị/thang đo khác nhau.

## 10. PCA và explained variance

- [ ] Fit PCA với đầy đủ số component trước khi lựa chọn.
- [ ] Lưu `explained_variance_`.
- [ ] Lưu `explained_variance_ratio_`.
- [ ] Tính cumulative explained variance.
- [ ] Vẽ scree plot theo từng component.
- [ ] Vẽ cumulative explained-variance plot.
- [ ] Xác định số component tối thiểu để giữ ít nhất 80%, 90% và 95% variance.
- [ ] So sánh cụ thể các lựa chọn 2, 3 và 5 component.
- [ ] Nhận xét component có explained variance cao nhất.
- [ ] Nhận xét component có explained variance thấp nhất.
- [ ] Giải thích sự đánh đổi giữa giảm chiều và bảo toàn thông tin.
- [ ] Tạo bảng loading của PC1 và PC2 để biết feature đóng góp nhiều nhất.

Đầu ra gợi ý:

- `report/figures/wine_scree_plot.png`
- `report/figures/wine_cumulative_variance.png`
- `report/tables/wine_pca_component_comparison.csv`

## 11. PCA visualization 2D

- [ ] Biến đổi dữ liệu thành PC1 và PC2.
- [ ] Vẽ scatter plot PC1-PC2 với màu theo `quality`.
- [ ] Vẽ hoặc cân nhắc thêm scatter plot với màu theo `wine_type`.
- [ ] Thêm title, tên trục, legend/color bar và tỷ lệ variance của PC1/PC2.
- [ ] Nhận xét cluster, separation, overlap và outlier.
- [ ] Không khẳng định hai nhóm tách biệt nếu biểu đồ cho thấy chồng lấn.
- [ ] Nêu giới hạn của việc chỉ nhìn hai component đầu.

Đầu ra gợi ý:

- `report/figures/wine_pca_quality.png`
- `report/figures/wine_pca_type.png`

## 12. Phần báo cáo Nguyễn Hoàng Minh phải viết

- [ ] Giới thiệu Wine Quality và nguồn dữ liệu.
- [ ] Mô tả red/white integration.
- [ ] Trình bày bảng phân loại feature.
- [ ] Mô tả vấn đề data quality và quyết định cleaning.
- [ ] Trình bày bảng before/after.
- [ ] Trình bày thống kê và correlation analysis.
- [ ] Mô tả PCA preprocessing.
- [ ] Trình bày explained variance và lựa chọn số component.
- [ ] Phân tích biểu đồ PCA 2D.
- [ ] So sánh dữ liệu gốc với biểu diễn PCA về số chiều, thông tin, khả năng diễn giải và trực quan hóa.
- [ ] Viết giới hạn của PCA đối với Wine Quality.
- [ ] Ghi trích dẫn nguồn UCI và giải thích mọi hình/bảng được đưa vào báo cáo.

## 13. Công việc tích hợp repository và báo cáo cuối

- [ ] Review notebook của Nguyễn Hoàng Anh ở mức có thể chạy lại và đọc được kết quả.
- [ ] Tổng hợp các phần của hai người mà không làm thay đổi số liệu gốc.
- [ ] Giữ cách đặt tên hình, bảng và thuật ngữ nhất quán.
- [ ] Kiểm tra tên hai thành viên và bổ sung đúng student ID.
- [ ] Đối chiếu báo cáo với `ASSIGNMENT_REQUIREMENTS.md`.
- [ ] Xuất bản PDF hoàn chỉnh vào `report/final_report.pdf`.
- [ ] Mở lại PDF và kiểm tra font, bảng, caption, hình bị cắt hoặc hình quá mờ.
- [ ] Kiểm tra notebook và các file cần thiết đã được commit/push.
- [ ] Không commit dữ liệu raw, environment hoặc file tạm.
- [ ] Hoàn thành bản PDF đầu tiên vào Day 6; chỉ sửa và kiểm tra ở Day 7.

## 14. Kế hoạch cá nhân theo ngày

| Ngày | Công việc của Nguyễn Hoàng Minh | Kết quả cuối ngày |
|---|---|---|
| 1 | Tải dữ liệu, tích hợp red/white, lập data dictionary | Có dataset tích hợp và bảng feature |
| 2 | Data-quality audit, cleaning, before/after comparison | Có dữ liệu sạch và giải thích cleaning |
| 3 | Mean, variance, covariance, categorical analysis, correlation | Có bảng thống kê và heatmap |
| 4 | Standardization, PCA, explained variance, loading | Có toàn bộ kết quả PCA dạng số |
| 5 | PCA 2D, nhận xét, viết phần Wine Quality | Phần Wine Quality gần hoàn chỉnh |
| 6 | Review phần Heart Disease, tổng hợp báo cáo và xuất PDF | Có bản PDF hoàn chỉnh đầu tiên |
| 7 | Đối chiếu checklist, sửa lỗi trình bày và nộp bài | PDF cuối đã được kiểm tra |

## 15. Definition of done cá nhân

Phần việc Nguyễn Hoàng Minh chỉ được xem là hoàn thành khi:

- [ ] Notebook chạy từ đầu đến cuối sau khi đặt đúng hai file raw.
- [ ] Không có kết quả báo cáo nào được nhập thủ công mà không thể tái lập.
- [ ] Target không được dùng để fit PCA.
- [ ] Cleaning không xóa dữ liệu mà thiếu giải thích.
- [ ] Các ngưỡng variance và số component được lấy từ kết quả thật.
- [ ] Tất cả hình có title, label và legend/color bar đọc được.
- [ ] Phần nhận xét nói về kết quả của dataset, không chỉ chép lý thuyết PCA.
- [ ] Các file cần thiết đã được review, commit và push.
- [ ] Báo cáo cuối bao phủ đầy đủ yêu cầu và hiển thị đúng trong PDF.

