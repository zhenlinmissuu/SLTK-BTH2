# Chuẩn Trình Bày Bài Toán Hồi Quy Tuyến Tính Đơn Biến

> Tài liệu này tổng hợp và chuẩn hóa lại đúng ký hiệu, cấu trúc 4 bước kiểm định và bảng ANOVA theo bài giảng trên lớp (từ bản scan vở trong `lythuyet_jpg/`), phục vụ làm khung trình bày chuẩn cho bài thực hành.

---

## 1. Mô hình hồi quy tuyến tính & Giả thiết

Xét bài toán hồi quy tuyến tính đơn biến giữa biến độc lập $x$ và biến phụ thuộc (biến phản hồi) $Y$:

$$Y = \beta_0 + \beta_1 x + \varepsilon$$

**Giả thiết $(I)$:**
- $\varepsilon$ độc lập
- $E(\varepsilon) = 0$; $V(\varepsilon) = \sigma^2$
- $\varepsilon \sim N(0; \sigma^2)$

*(Hệ quả: $Y_i \sim N(\beta_0 + \beta_1 x_i;\; \sigma^2)$ độc lập).*

---

## 2. Ước lượng bình phương cực tiểu (OLS) & Mô hình thực nghiệm

Từ mẫu quan sát gồm $n$ cặp giá trị $(x_i, y_i)$ với $i = 1, \dots, n$:

- Đặt các tổng bình phương và tích chéo:
  $$S_{xx} = \sum_{i=1}^n (x_i - \bar{x})^2 = \sum_{i=1}^n x_i^2 - \frac{1}{n}\left(\sum_{i=1}^n x_i\right)^2$$
  $$S_{xy} = \sum_{i=1}^n (x_i - \bar{x})(y_i - \bar{y}) = \sum_{i=1}^n x_i y_i - \frac{1}{n}\left(\sum_{i=1}^n x_i\right)\left(\sum_{i=1}^n y_i\right)$$
  $$SS_T = \sum_{i=1}^n (y_i - \bar{y})^2 = \sum_{i=1}^n y_i^2 - \frac{1}{n}\left(\sum_{i=1}^n y_i\right)^2$$

- Phương pháp bình phương cực tiểu tìm $\hat{\beta}_0, \hat{\beta}_1$ sao cho tổng bình phương phần dư đạt cực tiểu:
  $$\sum_{i=1}^n e_i^2 = \sum_{i=1}^n (y_i - \hat{y}_i)^2 = SS_E \longrightarrow \min$$

- Công thức ước lượng:
  $$\hat{\beta}_1 = \frac{S_{xy}}{S_{xx}}, \qquad \hat{\beta}_0 = \bar{y} - \hat{\beta}_1 \bar{x}$$

- **Mô hình hồi quy thực nghiệm:**
  $$\hat{y} = \hat{\beta}_0 + \hat{\beta}_1 x$$

### Tính chất của ước lượng (khi giả thiết $(I)$ thỏa mãn)
- $\hat{\beta}_0, \hat{\beta}_1$ là các ước lượng không chệch: $E(\hat{\beta}_0) = \beta_0$, $E(\hat{\beta}_1) = \beta_1$.
- Phương sai của các ước lượng:
  $$V(\hat{\beta}_0) = \sigma^2 \left(\frac{1}{n} + \frac{\bar{x}^2}{S_{xx}}\right), \qquad V(\hat{\beta}_1) = \frac{\sigma^2}{S_{xx}}$$
- Vì $\sigma^2$ chưa biết, ta dùng ước lượng không chệch cho $\sigma^2$:
  $$\hat{\sigma}^2 = s^2 = \frac{SS_E}{n - 2}$$
- Công thức tính thuận tiện cho $SS_E$:
  $$SS_E = SS_T - \hat{\beta}_1 S_{xy}$$
- **Sai số chuẩn của mô hình** (sai số chuẩn của đường thẳng hồi quy):
  $$s = \sqrt{\hat{\sigma}^2} = \sqrt{\frac{SS_E}{n - 2}}$$

---

## 3. Bài toán dự đoán

Từ mô hình thực nghiệm $\hat{y} = \hat{\beta}_0 + \hat{\beta}_1 x$, với một giá trị $x_0$ cho trước của biến độc lập, giá trị dự đoán điểm cho biến phụ thuộc $y$ là:

$$\hat{y}_0 = \hat{\beta}_0 + \hat{\beta}_1 x_0$$

Phần dư tại quan sát thứ $i$ là $e_i = y_i - \hat{y}_i$.

---

## 4. Kiểm tra 2 biến có liên hệ tuyến tính (Kiểm định ý nghĩa hồi quy)

Bài toán đặt ra: Biến độc lập $x$ có hữu ích trong việc dự đoán $y$ hay không (với mức ý nghĩa $\alpha$ cho trước).

### Cách 1: Kiểm định Student về hệ số góc $\beta_1$

- **$B_1$: Chọn cặp giả thuyết**
  $$H_0: \beta_1 = 0 \quad ; \quad H_1: \beta_1 \neq 0$$
  *(Tổng quát với giá trị $\beta_{10}$ bất kỳ: $H_0: \beta_1 = \beta_{10} \;;\; H_1: \beta_1 \neq \beta_{10}$. Trường hợp $\beta_{10} = 0$ rất có ý nghĩa vì nếu không bác bỏ $H_0$ thì $y$ không liên quan tuyến tính đến $x$; nếu bác bỏ $H_0$ thì $x$ có giá trị trong việc giải thích/dự đoán $y$).*

- **$B_2$: Chọn tiêu chuẩn kiểm định**
  $$T = \frac{\hat{\beta}_1 - 0}{s / \sqrt{S_{xx}}} = \frac{\hat{\beta}_1}{\sqrt{\dfrac{SS_E}{S_{xx}(n-2)}}} \stackrel{H_0\text{ đúng}}{\sim} t(n - 2)$$
  trong đó $s = \sqrt{\dfrac{SS_E}{n - 2}}$.

- **$B_3$: Tìm miền bác bỏ**
  $$W_\alpha = \left(-\infty;\; -t_{\alpha/2}^{(n-2)}\right) \cup \left(t_{\alpha/2}^{(n-2)};\; +\infty\right)$$

- **$B_4$: Tính giá trị quan sát và kết luận**
  $$t_{qs} = \frac{\hat{\beta}_1}{s / \sqrt{S_{xx}}}$$
  - Nếu $t_{qs} \in W_\alpha$: **Bác bỏ $H_0$** $\implies$ Hai biến có liên hệ tuyến tính ($x$ có giá trị trong việc dự đoán $y$).
  - Nếu $t_{qs} \notin W_\alpha$: **Chưa có cơ sở bác bỏ $H_0$** $\implies$ Chưa đủ cơ sở kết luận hai biến có liên hệ tuyến tính.

---

### Cách 2: Kiểm định Fisher bằng phân tích phương sai (ANOVA)

Ta phân tích tổng bình phương thành 3 đại lượng:
$$SS_T = SS_E + SS_R$$
trong đó:
- $SS_T = \sum_{i=1}^n (y_i - \bar{y})^2$ có $(n - 1)$ bậc tự do.
- $SS_R = \sum_{i=1}^n (\hat{y}_i - \bar{y})^2 = \hat{\beta}_1 S_{xy}$ có $1$ bậc tự do.
- $SS_E = \sum_{i=1}^n (y_i - \hat{y}_i)^2 = SS_T - SS_R$ có $(n - 2)$ bậc tự do.

**Quy trình 4 bước:**

- **$B_1$: Chọn cặp giả thuyết** (như Cách 1)
  $$H_0: \beta_1 = 0 \quad ; \quad H_1: \beta_1 \neq 0$$

- **$B_2$: Chọn tiêu chuẩn kiểm định**
  $$F = \frac{SS_R / 1}{SS_E / (n - 2)} = \frac{MS_R}{MS_E} \stackrel{H_0\text{ đúng},\; GT(I)}{\sim} F(1;\; n - 2)$$

- **$B_3$: Tìm miền bác bỏ**
  $$W_\alpha = \left(F_{(\alpha;\; 1;\; n-2)};\; +\infty\right)$$

- **$B_4$: Tính giá trị quan sát và kết luận**
  $$F_{qs} = \frac{SS_R / 1}{SS_E / (n - 2)} = \frac{MS_R}{MS_E}$$
  - Nếu $F_{qs} \in W_\alpha$: **Bác bỏ $H_0$** $\implies$ Mô hình hồi quy có ý nghĩa thống kê (hai biến có liên hệ tuyến tính).
  - Nếu $F_{qs} \notin W_\alpha$: **Chưa có cơ sở bác bỏ $H_0$**.

**Bảng ANOVA chuẩn trình bày:**

| Nguồn | Tổng bình phương | Bậc tự do | Bình phương trung bình | Giá trị quan sát ($qs$) |
| :--- | :---: | :---: | :---: | :---: |
| **Hồi quy** | $SS_R$ | $1$ | $MS_R = \dfrac{SS_R}{1}$ | $F_{qs} = \dfrac{MS_R}{MS_E}$ |
| **Sai số** | $SS_E$ | $n - 2$ | $MS_E = \dfrac{SS_E}{n - 2}$ | |
| **Tổng** | $SS_T$ | $n - 1$ | | |

> **Lưu ý kiểm tra chéo:** Với hồi quy đơn biến, hai cách kiểm định Student và Fisher là tương đương về mặt toán học: $F_{qs} = t_{qs}^2$ và $F_{(\alpha;\; 1;\; n-2)} = \left(t_{\alpha/2}^{(n-2)}\right)^2$.
