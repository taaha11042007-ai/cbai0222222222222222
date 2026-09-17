Bài tập 02: Xây dựng Phân hệ Quyết toán Đơn hàng Đa tầng ShopeeFood bằng C


Bài tập 07: Xây dựng Phân hệ Quyết toán Đơn hàng Đa tầng ShopeeFood bằng C
1. Mục tiêu
Dịch thuật chính xác các yêu cầu nghiệp vụ thực tế từ hệ thống ShopeeFood (tính phí giao hàng, giảm giá Freeship, phụ phí giờ cao điểm, kiểm tra tồn kho và trạng thái cửa hàng) sang biểu thức số học và biểu thức logic trong ngôn ngữ C.

Vận dụng phối hợp thành thạo các kiến thức nền tảng: khai báo biến (int, float, char), thao tác nhập/xuat chuẩn (scanf, printf), toán tử số học (+, -, *, /, %), toán tử so sánh (==, !=, >, <, >=, <=) và toán tử logic (&&, ||, !).

Rèn luyện tư duy giải thuật nâng cao thông qua việc tính toán giá trị nghiệp vụ và chặn lỗi dữ liệu trực tiếp bằng giá trị trả về của biểu thức logic (0 hoặc 1) mà chưa sử dụng bất kỳ câu lệnh rẽ nhánh (if/else) hay vòng lặp nào.

2. Ngữ cảnh & Bài toán
Tại hệ thống ShopeeFood, module "Checkout Service" chịu trách nhiệm tính toán hóa đơn thanh toán cho hàng triệu đơn hàng mỗi ngày. Để đảm bảo tốc độ phản hồi tính bằng milisecond và tối ưu hóa tài nguyên hệ thống ở cấp độ thấp, đội ngũ kỹ thuật cần xây dựng một thành phần tính toán đơn hàng cực nhanh.

Hiện tại, hệ thống gặp rủi ro thất thoát doanh thu và trải nghiệm người dùng kém do một số lỗi hệ thống:

Phí giao hàng không được tính chính xác theo khoảng cách thực tế.

Khách hàng vẫn bấm đặt được món khi cửa hàng đã đóng cửa hoặc số lượng món trong kho đã hết.

Áp dụng sai ưu tiên Freeship cho khách hàng VIP và khách hàng phổ thông.

Phụ phí giờ cao điểm không được tự động tính vào tổng hóa đơn.

Bạn được giao nhiệm vụ viết chương trình C để đóng vai trò là module tính toán và xác thực đơn hàng tự động cho ShopeeFood, đảm bảo chính xác tuyệt đối mọi quy tắc tài chính và điều kiện vận hành.

Vấn đề phát sinh: Yêu cầu nghiệp vụ Chương trình cần tiếp nhận các thông tin đầu vào từ đơn hàng và thực hiện tính toán tự động:

Thông tin đầu vào:

Mã món ăn (int): Ví dụ 1024.

Đơn giá món ăn (float - VNĐ): Ví dụ 45000.0.

Số lượng đặt mua (int): Ví dụ 3.

Khoảng cách giao hàng (float - km): Ví dụ 3.5.

Trạng thái khung giờ cao điểm (int): 1 nếu nằm trong khung giờ (11h-13h hoặc 18h-20h), 0 nếu là giờ bình thường.

Trạng thái cửa hàng (int): 1 nếu Cửa hàng đang mở cửa, 0 nếu Cửa hàng đóng cửa.

Số lượng món còn trong kho (int): Số lượng khả dụng tại quán.

Xếp loại tài khoản khách hàng (char): 'V' nếu là tài khoản VIP, 'N' nếu là tài khoản Normal (Thường).

Công thức và quy tắc nghiệp vụ:

Tiền món ăn (Subtotal) = Đơn giá * Số lượng đặt.

Phí giao hàng cơ bản (Base Shipping Fee) = Khoảng cách (km) * 5000.0 VNĐ/km.

Tiêu chuẩn đạt Freeship (Giảm 15.000 VNĐ phí giao hàng): Đơn hàng đạt Freeship nếu thỏa mãn: (Subtotal >= 100000 VNĐ VÀ Khoảng cách <= 5.0 km) HOẶC khách hàng là tài khoản VIP (Loại tài khoản == 'V').

Số tiền miễn giảm giao hàng = 15000.0 * (kết quả kiểm tra Freeship). (Lưu ý: Tiền giảm giá không vượt quá Phí giao hàng cơ bản).

Phụ phí giờ cao điểm (Peak Surcharge) = 10000.0 * Trạng thái giờ cao điểm.

Điều kiện hợp lệ của đơn hàng (Order Validity): Đơn hàng ĐƯỢC CHẤP NHẬN (1) khi và chỉ khi thỏa mãn TẤT CẢ các điều kiện sau:

Cửa hàng đang mở cửa (Trạng thái cửa hàng == 1).

Tồn kho đủ đáp ứng (Số lượng tồn kho >= Số lượng đặt).

Số lượng đặt mua hợp lệ (Số lượng đặt > 0).

Đơn giá món ăn hợp lệ (Đơn giá > 0).

Tổng tiền thanh toán cuối cùng (Final Payable Amount): Tổng thanh toán = (Subtotal + Phí giao hàng cơ bản - Số tiền miễn giảm Freeship + Phụ phí giờ cao điểm) * (Kết quả hợp lệ của đơn hàng). (Lưu ý: Nếu đơn hàng KHÔNG hợp lệ, tổng tiền thanh toán bắt buộc phải trả về 0 VNĐ).

3. Mã nguồn hiện tại
Ràng buộc & Lỗi thường gặp dữ liệu

Lỗi thường gặp bộ đệm bàn phím (Buffer Stdin Trap): Khi nhập dữ liệu kiểu char (Loại tài khoản VIP/Normal) sau các dữ liệu kiểu số (int, float), bộ đệm stdin sẽ còn sót lại ký tự xuống dòng (\n). Nếu không xử lý khoảng trắng trước %c trong scanf(), chương trình sẽ bị trôi lệnh nhập dữ liệu.

Lỗi thường gặp dữ liệu dị biệt (Edge Cases):

Kịch bản 1 (Kho hết hàng / Quán đóng cửa): Khách hàng đặt mua món ăn nhưng nhà hàng đã đóng cửa (is_store_open = 0) hoặc số lượng mua vượt quá số lượng tồn kho. Hệ thống phải xác định đơn hàng không hợp lệ (0) và tổng tiền bằng 0.00 VNĐ.

Kịch bản 2 (Số lượng/Đơn giá âm hoặc bằng 0): Người dùng cố tình nhập số lượng đặt là 0 hoặc -2. Hệ thống phải vô hiệu hóa đơn hàng.

Kịch bản 3 (Khoảng cách cực ngắn nhưng không đạt giá trị tối thiểu): Khách hàng mua đơn 20.000 VNĐ với khoảng cách 1.0 km, không phải tài khoản VIP. Mặc dù khoảng cách gần nhưng giá trị đơn không đạt 100.000 VNĐ nên KHÔNG được giảm giá Freeship.

Giới hạn phạm vi kiến thức (Strict Constraint): CẤM TUYỆT ĐỐI sử dụng: câu lệnh rẽ nhánh (if, else, switch), các loại vòng lặp (for, while, do-while), hàm tự định nghĩa, mảng (array) hoặc kiểu cấu trúc (struct). Mọi tính toán điều kiện phải được xử lý thông qua biểu thức logic/số học đại số Boole.

4. Yêu cầu kỹ thuật
Báo cáo phân tích và thiết kế giải pháp

Phân tích bài toán (I/O): Xác định rõ danh sách các biến đầu vào (Input), kiểu dữ liệu tương ứng và các thông số kết quả đầu ra (Output).

Đề xuất giải pháp: Trình bày tư duy áp dụng toán tử so sánh, toán tử logic để nhân bản giá trị 0 hoặc 1 vào công thức tính tiền mà không sử dụng cấu trúc rẽ nhánh if/else.

Thiết kế các bước: Trình bày tuần tự các bước xử lý dữ liệu từ lúc tiếp nhận đầu vào đến khi in ra phiếu hóa đơn thanh toán ShopeeFood.

Triển khai và chống lỗi

Mã nguồn C hoàn chỉnh (main.c), biên dịch chuẩn xác bằng trình biên dịch gcc không phát sinh lỗi hay cảnh báo (warning).

Logic code phải phản ánh chính xác thiết kế đã đề ra, chặn triệt để các hiện tượng trôi lệnh bộ đệm scanf và các kịch bản dữ liệu dị biệt đã nêu tại Mục 4.

Màn hình kết quả console phải hiển thị đẹp mắt, rõ ràng theo chuẩn báo cáo hệ thống ShopeeFood:

==================================================
           SHOPEEFOOD ORDER CHECKOUT SYSTEM 
==================================================
Mã món ăn : 1024
Đơn giá : 50000.00 VND
Số lượng đặt : 3
Khoảng cách giao : 4.0 km
Khung giờ cao điểm : Có (1)
Trạng thái quán : Mở cửa (1)
Số lượng tồn kho : 10
Loại tài khoản : V (VIP)
--------------------------------------------------
TỔNG TIỀN MÓN AN : 150000.00 VND
PHÍ GIAO HÀNG CƠ BẢN: 20000.00 VND
GIẢM GIÁ FREESHIP : 15000.00 VND
PHỤ PHÍ GIỜ CAO ĐIỂM: 10000.00 VND
--------------------------------------------------
ĐƠN HÀNG HỢP LỆ : 1 (1: HỢP LỆ / 0: TỪ CHỐI)
TỔNG THÀNH TIỀN : 165000.00 VND
==================================================
 

5. Quy định nộp bài
Tạo thư mục mã nguồn đặt tên theo cấu trúc: shopeefood_checkout.

Tập tin mã nguồn C chính: main.c.

Tập tin tài liệu báo cáo giải pháp: README.md (chứa nội dung phân tích I/O, tư duy đại số Boole và các bước thực hiện).

Đẩy toàn bộ thư mục bài làm lên repository cá nhân trên GitHub và nộp đường dẫn link theo quy định của Rikkei Education.
