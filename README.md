# Data Mining - Áp dụng Differential privacy vào các thuật toán cây quyết định để dự đoán rủi ro tín dụng ngân hàng.

Với sự phát triển vượt bậc của lĩnh vực ngân hàng hiện nay, một trong những vấn đề lớn mà ngành ngân hàng phải đối mặt là khi xu hướng vay vốn ngày càng tăng thì tỷ lệ vỡ nợ cũng tăng cao. Do đó, việc đánh giá rủi ro tín dụng là một công việc rất quan trọng để đảm bảo sự ổn định và an toàn của hệ thống tài chính và ngân hàng. Hiện nay, các ngân hàng thường xuyên chia sẻ dữ liệu của khách hàng cho công việc hợp tác với nhau để xây dựng một mô hình dự đoán chung, nhằm tăng độ chính xác cho mô hình. Tuy nhiên, sử dụng các dữ liệu khách hàng để xây dựng mô hình dự đoán rủi ro tín dụng có thể dẫn đến việc tiết lộ thông tin cá nhân và gây ra nhiều rủi ro về bảo mật. Vì vậy, việc áp dụng các kỹ thuật bảo mật thông tin trở thành một yêu cầu thiết yếu. Trong đề tài này, chúng tôi sẽ tập trung vào việc xây dựng các mô hình dự đoán rủi ro tín dụng ngân hàng bằng việc áp dụng Quyền riêng tư khác biệt (Differential privacy) trên thuật toán cây quyết định (decision tree). Decision tree là một thuật toán học máy rất hiệu quả để xây dựng các mô hình dự đoán rủi ro tín dụng. Đồng thời, sử dụng kỹ thuật Differential privacy sẽ giúp đảm bảo tính riêng tư và bảo mật của dữ liệu khách hàng trong quá trình xây dựng mô hình

## 1. Bộ dữ liệu
Bộ dữ liệu "Lending Club Loan Data" cung cấp thông tin về các khoản vay cá nhân của Lending Club, một trong những công ty cho vay trực tuyến hàng đầu tại Hoa Kỳ. </br>
Bộ dữ liệu này bao gồm hơn 2,2 triệu khoản vay từ năm 2007 đến năm 2018, và chứa các thông tin về các chỉ số tín dụng của khách hàng, mục đích vay tiền, số tiền vay, lãi suất, thời hạn khoản vay, kết quả của khoản vay và nhiều thông tin khác. </br>
Bộ dữ liệu này là một tài nguyên quan trọng cho các nhà phân tích và nhà đầu tư để phân tích xu hướng thị trường cho các khoản vay cá nhân, cũng như để xây dựng các mô hình dự báo tín dụng. </br>
Nguồn dữ liệu: https://www.kaggle.com/datasets/wordsforthewise/lending-club

## 2. Các kỹ thuật và thuật toán được sử dụng
 ### 1.  Tiền xử lý dữ liệu
 Qua quá trình tiền xử lý, chúng tôi sử dụng 23 thuộc tính trong tổng số 151 thuộc tính gốc, với:
 * Thuộc tính quyết định: loan_status
 * Các thuộc tính điều kiện:
    - loan_amnt: Số tiền được vay
    - term: Kì hạn cho vay (36 hoặc 60 tháng)
    - int_rate: Lãi suất hàng năm (dưới dạng phần trăm)
    - installment: Số tiền phải trả hàng tháng
    - sub_grade: Mức đánh giá chi tiết hơn của khoản vay (A1, A2, A3, B1, B2, v.v.)
    - emp_length: Thời gian làm việc của người vay trong năm
    - home_ownership: Tình trạng sở hữu nhà ở của người vay (mái nhà riêng, căn hộ, thuê, v.v.)
    - verification_status: Trạng thái xác minh thông tin tài chính của người vay
    - loan_status: Tình trạng khoản vay (trả đủ, trả chậm, v.v.)
    - purpose: Mục đích của khoản vay
    - addr_state: Tiểu bang của địa chỉ người vay
    - dti: Tỷ lệ nợ trên thu nhập hàng tháng
    - open_acc: Số tài khoản tín dụng đang mở
    - pub_rec: Số lần ghi nhận công khai về việc vay tiền không trả (nợ xấu)
    - revol_util: Tỷ lệ sử dụng tín dụng của tài khoản thẻ tín dụng
    - total_acc: Tổng số tài khoản tín dụng
    - initial_list_status: Trạng thái danh sách ban đầu (W hoặc F)
    - application_type: Loại ứng dụng (cá nhân hoặc đồng thời)
    - mort_acc: Số lượng tài khoản tín dụng thế chấp
    - pub_rec_bankruptcies: Số lần phá sản theo quy định của pháp luật
    - log_annual_inc: phép biến đổi log của giá trị annual_inc (thu nhập hằng năm của người vay)
    - fico_score: kết hợp hai thuộc tính last_fico_range_high và last_fico_range_low	
    - log_revol_bal:
 ### 2. Dự đoán cho dữ liệu một bên
 Sử dụng các thuật toán của thư viện sklearn để đự đoán: ID3, CART, Naive Bayes, Random Forest
 ### 3.  Dự đoán cho dữ liệu kết hợp giữa hai bên
 * Sử dụng thuật toán Random forest của thư viện Diffprivlib
 * Kết hợp mô hình sử dụng cơ chế Client - Server
 
