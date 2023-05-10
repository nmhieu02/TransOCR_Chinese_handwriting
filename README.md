# **TransOCR__Chinese_handwriting_recognization**

## **MỤC TIÊU NGHIÊN CỨU**
:star: Tìm hiểu và nghiên cứu cách triển khai mô hình TransOCR.

:star: Thực nghiệm mô hình với bộ dữ liệu SCUT-HCCDoc Dataset Release
v2.

:star: Đánh giá và so sánh hiệu quả của hệ thống nhận diện văn bản chữ viết
tay tiếng Trung với các công trình nghiên cứu hiện có khác.

## **MÔ HÌNH TRANSOCR**
Mô hình bao gồm mô-đun giám sát Pixel-Wise, mô-đun Nhận biết vị trí và 
mô-đun Nhận biết nội dung. Mô hình được xây dựng dựa trên 
Transformer-based Super-Resolution Network (TBSRN). Để giải quyết các ký tự khó
phân biệt với độ phân giải thấp, mô hình sử dụng hàm mất mát cross entropy có trọng số.

![z4255419831495_040c0e63e6aeaccf2d75ee3d4cfda58e](https://github.com/nmhieu02/Money_Classify/assets/133008099/f4658b53-e3b2-4a01-98b2-069f20bb743c)

## **MÔ-ĐUN GIÁM SÁT PIXEL-WISE**
Sử dụng STN để tinh chỉnh lạị hình ảnh bị nghiêng lệch. Hình ảnh được chỉnh sửa sẽ chuyển sang TBSRN. Sau đó lấy mẫu ngược thành hình ảnh siêu phân giải bằng cách Pixel shuffle.


![Screenshot 2023-05-10 192519](https://github.com/nmhieu02/Money_Classify/assets/133008099/cd5ecbf7-d0d0-4050-940c-6121e9b59868)

## **MÔ-ĐUN NHẬN BIẾT VỊ TRÍ**
Tập trung chủ yếu vào các vùng ký tự trong ảnh SR bằng cách giảm sự chú ý đến nền của ảnh. Lấy hình ảnh HR tương ứng làm tham chiếu.
Attention-map của hình ảnh HR và hình ảnh SR được giám sát bởi hàm mất mát .

## **MÔ-ĐUN NHẬN BIẾT NỘI DUNG**
Với đầu vào là ảnh siêu phân giải, mô hình Transformer được huấn luyện trước sẽ dự đoán một chuỗi
nội dung văn bản. 
Để xử lý vấn đề các ký tự trông tương đồng nhau, ta sẽ xử lý chúng bằng một mô hình học sâu với vanilla cross-entropy loss.

## **THỰC NGHIỆM**

### **Dataset**

![Screenshot 2023-05-10 192536](https://github.com/nmhieu02/Money_Classify/assets/133008099/991114ab-d2af-43a7-8f20-1633966759a9)

### **THAM SỐ HUẤN LUYỆN**

Thực nghiệm, các thông số của mô hình TransOCR được quy định như sau: _**learning rate = 1.0, batch size = 32, epoch = 1000**_. Việc xây dựng mô hình, đánh giá và thực nghiệm được xây dựng bằng framework Pytorch. Mô hình học sâu được chạy trên card đồ họa GTX1650, 4GBVRAM.

## **KẾT QUẢ**

![Screenshot 2023-05-10 192559](https://github.com/nmhieu02/Money_Classify/assets/133008099/67e1412b-75bc-422e-a127-9844d3d00534)

Dù độ chính xác chỉ đạt khoảng 50%, nhưng đây là một bước tiến đáng kể. Phương pháp đã cho thấy sự vượt trội trong việc lấy mẫu hình ảnh chữ viết 
có độ phân giải thấp. Độ chính xác cao hơn rất nhiều so với các phương pháp trước đó.
