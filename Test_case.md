
# PHẦN 1: CAB Test Cases

| **Cột** | **Ý nghĩa** | **Mô tả chi tiết** | **Ví dụ** |
|---|---|---|---|
| **Test Case ID** | Mã định danh duy nhất của Test Case | Dùng để quản lý, tìm kiếm, truy xuất và tham chiếu Test Case. | TC-BOOK-001 |
| **Test Scenario** | Scenario mà Test Case đang kiểm thử | Mô tả chức năng hoặc tình huống cần kiểm thử ở mức tổng quát. Một Test Scenario có thể có nhiều Test Case. | Khách hàng tạo yêu cầu đặt xe |
| **Test Case** | Trường hợp kiểm thử cụ thể | Mô tả chính xác trường hợp cần kiểm thử. Loại kiểm thử được đặt ở đầu nội dung: Positive, Negative, Boundary, Empty/Null, Invalid Format/Value, State, Security, Integration... | Positive – Tạo yêu cầu đặt xe hợp lệ |
| **Preconditions** | Điều kiện tiên quyết | Các điều kiện hoặc trạng thái phải được đáp ứng trước khi bắt đầu Test Case. | Khách hàng đã đăng nhập |
| **Test Steps** | Các bước thực hiện kiểm thử | Mô tả tuần tự các thao tác Tester cần thực hiện. | 1. Mở Đặt xe<br>2. Nhập thông tin<br>3. Gửi yêu cầu |
| **Test Data** | Dữ liệu kiểm thử | Dữ liệu hoặc trạng thái đầu vào dùng trong Test Case. Với rule chưa có trong SRS, không tự đặt giá trị biên. | Điểm đón: hợp lệ<br>Điểm đến: hợp lệ<br>Loại xe: hợp lệ |
| **Expected Result** | Kết quả mong đợi | Kết quả hệ thống phải trả về nếu chức năng hoạt động đúng. | Booking được tạo và hệ thống bắt đầu tìm tài xế |
| **Priority** | Mức độ ưu tiên kiểm thử | Ưu tiên QA theo mức ảnh hưởng đến core flow; không phải yêu cầu nghiệp vụ trong SRS. | High / Medium / Low |

# TEST CASE – AUTHENTICATION


| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
|---|---|---|---|---|---|---|---|
| **AUTH-TC-001** | Đăng ký tài khoản | **Positive – Đăng ký Customer với thông tin hợp lệ** | Khách hàng chưa có tài khoản và đang ở chức năng đăng ký | 1. Mở chức năng đăng ký<br>2. Nhập đầy đủ thông tin hợp lệ<br>3. Gửi yêu cầu đăng ký | Dữ liệu đăng ký: hợp lệ | Hệ thống tạo tài khoản Customer thành công | High |
| **AUTH-TC-002** | Đăng ký tài khoản | **Empty/Null – Bỏ trống một trường bắt buộc** | Đang ở chức năng đăng ký | 1. Nhập các trường hợp lệ<br>2. Bỏ trống một trường bắt buộc<br>3. Gửi yêu cầu | Required field = empty | Hệ thống từ chối tạo tài khoản và trả validation tương ứng | High |
| **AUTH-TC-003** | Đăng ký tài khoản | **Empty/Null – Gửi request đăng ký với body rỗng** | Authentication API đang hoạt động | 1. Gửi request đăng ký<br>2. Không truyền dữ liệu body | Body = `{}` hoặc `null` | Hệ thống từ chối request; tài khoản không được tạo | High |
| **AUTH-TC-004** | Đăng ký tài khoản | **Invalid Format/Value – Trường đăng ký sai định dạng** | Trường tương ứng có rule format trong API | 1. Nhập dữ liệu sai format<br>2. Gửi đăng ký | Field format = invalid | Hệ thống từ chối dữ liệu không đúng định dạng | Medium |
| **AUTH-TC-005** | Đăng ký tài khoản | **Boundary – Giá trị tại đúng giới hạn tối thiểu của trường có quy định độ dài** | Authentication API đã định nghĩa giới hạn | 1. Nhập dữ liệu đúng min length<br>2. Gửi đăng ký | Length = MIN | Hệ thống xử lý thành công nếu dữ liệu thỏa toàn bộ rule | Medium |
| **AUTH-TC-006** | Đăng ký tài khoản | **Boundary – Giá trị thấp hơn giới hạn tối thiểu 1 ký tự** | Authentication API đã định nghĩa giới hạn | 1. Nhập dữ liệu có độ dài MIN - 1<br>2. Gửi đăng ký | Length = MIN - 1 | Hệ thống từ chối dữ liệu và trả lỗi validation | Medium |
| **AUTH-TC-007** | Đăng nhập | **Positive – Customer đăng nhập với thông tin xác thực hợp lệ** | Customer đã có tài khoản hợp lệ | 1. Mở Login<br>2. Nhập thông tin xác thực hợp lệ<br>3. Nhấn Login | Actor = Customer<br>Credential = valid | Đăng nhập thành công và được sử dụng chức năng yêu cầu tài khoản | High |
| **AUTH-TC-008** | Đăng nhập | **Positive – Driver đăng nhập với thông tin xác thực hợp lệ** | Driver đã có tài khoản hợp lệ | 1. Mở Login<br>2. Nhập thông tin xác thực hợp lệ<br>3. Nhấn Login | Actor = Driver<br>Credential = valid | Đăng nhập thành công | High |
| **AUTH-TC-009** | Đăng nhập | **Negative – Thông tin định danh không tồn tại** | Hệ thống đang hoạt động | 1. Nhập thông tin định danh không tồn tại<br>2. Nhập password<br>3. Login | Account = not found | Đăng nhập thất bại; không tạo phiên/token xác thực | High |
| **AUTH-TC-010** | Đăng nhập | **Negative – Password không đúng** | Tài khoản tồn tại | 1. Nhập tài khoản đúng<br>2. Nhập password sai<br>3. Login | Account = valid<br>Password = invalid | Đăng nhập thất bại; không xác thực người dùng | High |
| **AUTH-TC-011** | Đăng nhập | **Empty/Null – Không nhập thông tin định danh** | Đang ở màn hình Login | 1. Để trống thông tin định danh<br>2. Nhập password<br>3. Login | Identifier = empty | Hệ thống không đăng nhập và trả validation | High |
| **AUTH-TC-012** | Đăng nhập | **Empty/Null – Không nhập password** | Đang ở màn hình Login | 1. Nhập thông tin định danh<br>2. Để trống password<br>3. Login | Password = empty | Hệ thống không đăng nhập và trả validation | High |
| **AUTH-TC-013** | Đăng nhập | **Empty/Null – Cả thông tin định danh và password đều rỗng** | Đang ở màn hình Login | 1. Không nhập thông tin đăng nhập<br>2. Nhấn Login | Identifier = empty<br>Password = empty | Hệ thống không xác thực; hiển thị lỗi các trường bắt buộc | High |
| **AUTH-TC-014** | Đăng nhập | **Invalid Format/Value – Thông tin định danh sai format** | API có quy định format cho trường định danh | 1. Nhập giá trị sai format<br>2. Nhập password<br>3. Login | Identifier format = invalid | Hệ thống từ chối request hoặc trả validation phù hợp | Medium |
| **AUTH-TC-015** | Đăng nhập | **Boundary – Password tại đúng giới hạn tối thiểu được quy định** | API đã xác định password rule | 1. Nhập tài khoản hợp lệ<br>2. Nhập password có độ dài đúng MIN<br>3. Login | Password length = MIN | Hệ thống xử lý password tại giá trị biên đúng theo rule | Medium |
| **AUTH-TC-016** | Đăng nhập | **Boundary – Password thấp hơn giới hạn tối thiểu 1 ký tự** | API đã xác định password rule | 1. Nhập tài khoản<br>2. Nhập password có độ dài MIN - 1<br>3. Login | Password length = MIN - 1 | Hệ thống từ chối dữ liệu password không đạt rule | Medium |
| **AUTH-TC-017** | Xác thực truy cập | **Negative – Truy cập chức năng yêu cầu authentication khi chưa đăng nhập** | Người dùng chưa được xác thực | 1. Không Login<br>2. Gọi chức năng yêu cầu tài khoản | Token/session = missing | Hệ thống từ chối truy cập | High |
| **AUTH-TC-018** | Xác thực truy cập | **Negative – Gửi token/credential xác thực không hợp lệ** | Người dùng gọi API có bảo vệ xác thực | 1. Gửi request đến API được bảo vệ<br>2. Truyền token không hợp lệ | Authentication token = invalid | Hệ thống không cho phép truy cập tài nguyên | High |
| **AUTH-TC-019** | Xác thực truy cập | **Positive – Người dùng đã xác thực truy cập chức năng thuộc quyền** | Customer/Driver đã đăng nhập thành công | 1. Login thành công<br>2. Gọi API thuộc quyền actor | Authentication = valid | Hệ thống cho phép sử dụng chức năng tương ứng | High |
| **AUTH-TC-020** | Bảo vệ dữ liệu xác thực | **Security – Response authentication không chứa password** | Đăng ký hoặc đăng nhập thành công | 1. Gửi request hợp lệ<br>2. Nhận response<br>3. Kiểm tra payload trả về | Authentication response | Response không trả trực tiếp password hoặc dữ liệu xác thực nhạy cảm | High |

# TEST CASE – PROFILE / UPDATE INFORMATION 
 
| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority | 
|---|---|---|---|---|---|---|---| 
| **PROF-TC-001** | Cập nhật thông tin | **Positive – Customer cập nhật thông tin cá nhân hợp lệ** | Customer đã đăng nhập | 1. Mở hồ sơ<br>2. Chỉnh sửa thông tin hợp lệ<br>3. Lưu | Personal information = valid | Hệ thống cập nhật và ghi nhận thông tin Customer | High | 
| **PROF-TC-002** | Cập nhật thông tin | **Positive – Driver cập nhật hồ sơ hợp lệ** | Driver đã đăng nhập | 1. Mở hồ sơ Driver<br>2. Chỉnh sửa thông tin hợp lệ<br>3. Lưu | Driver profile = valid | Hệ thống cập nhật và ghi nhận hồ sơ Driver | High | 
| **PROF-TC-003** | Cập nhật thông tin | **Positive – Driver cập nhật thông tin phương tiện của mình** | Driver đã đăng nhập và có phương tiện | 1. Mở thông tin phương tiện<br>2. Cập nhật thông tin hợp lệ<br>3. Lưu | Vehicle information = valid | Hệ thống ghi nhận thông tin phương tiện đã cập nhật | High |
| **PROF-TC-004** | Cập nhật thông tin | **Positive – Driver cập nhật trạng thái hoạt động** | Driver đã đăng nhập | 1. Mở chức năng cập nhật trạng thái<br>2. Chọn trạng thái hợp lệ<br>3. Lưu | Driver status = valid | Hệ thống ghi nhận trạng thái hoạt động mới của Driver | High | 
| **PROF-TC-005** | Cập nhật thông tin | **Empty/Null – Request cập nhật không có dữ liệu** | Customer/Driver đã đăng nhập | 1. Gửi request cập nhật<br>2. Không truyền dữ liệu | Body = `{}` hoặc `null` | Hệ thống không cập nhật dữ liệu và trả validation phù hợp | Medium | 
| **PROF-TC-006** | Cập nhật thông tin | **Invalid Format/Value – Dữ liệu cập nhật sai định dạng** | Actor đã đăng nhập; API có validation | 1. Nhập dữ liệu sai format<br>2. Gửi cập nhật | Update data = invalid | Hệ thống từ chối dữ liệu không hợp lệ | Medium | 
| **PROF-TC-007** | Cập nhật thông tin | **Negative/Security – Chưa đăng nhập nhưng thực hiện cập nhật** | Actor chưa xác thực | 1. Không đăng nhập<br>2. Gửi request cập nhật | Authentication = missing | Hệ thống từ chối cập nhật thông tin | High | 
| **PROF-TC-008** | Cập nhật thông tin | **Negative/Authorization – Cập nhật hồ sơ không thuộc tài khoản của mình** | Có hai tài khoản khác nhau | 1. Đăng nhập tài khoản A<br>2. Gửi cập nhật hồ sơ tài khoản B | Current user ≠ Profile owner | Hệ thống không cho phép cập nhật hồ sơ của tài khoản khác | High | 

# TEST CASE – Booking 

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
|---|---|---|---|---|---|---|---|
| **BOOK-TC-001** | Tạo yêu cầu đặt xe | **Positive – Tạo booking với điểm đón, điểm đến và loại xe hợp lệ** | Customer đã đăng nhập | 1. Mở chức năng Đặt xe<br>2. Nhập điểm đón hợp lệ<br>3. Nhập điểm đến hợp lệ<br>4. Chọn loại xe hợp lệ<br>5. Gửi yêu cầu | Pickup = valid<br>Destination = valid<br>Vehicle type = valid | Hệ thống tạo và ghi nhận booking thành công | High |
| **BOOK-TC-002** | Tạo yêu cầu đặt xe | **Positive – Booking hợp lệ được chuyển sang quá trình tìm tài xế** | Customer đã đăng nhập và gửi booking hợp lệ | 1. Gửi booking<br>2. Kiểm tra trạng thái xử lý tiếp theo | Booking = valid | Booking được ghi nhận và hệ thống bắt đầu quá trình tìm tài xế | High |
| **BOOK-TC-003** | Tạo yêu cầu đặt xe | **Empty/Null – Điểm đón để trống** | Customer đã đăng nhập | 1. Để trống điểm đón<br>2. Nhập điểm đến<br>3. Chọn loại xe<br>4. Gửi yêu cầu | Pickup = empty | Hệ thống không tạo booking khi thiếu điểm đón | High |
| **BOOK-TC-004** | Tạo yêu cầu đặt xe | **Empty/Null – Điểm đến để trống** | Customer đã đăng nhập | 1. Nhập điểm đón<br>2. Để trống điểm đến<br>3. Chọn loại xe<br>4. Gửi yêu cầu | Destination = empty | Hệ thống không tạo booking khi thiếu điểm đến | High |
| **BOOK-TC-005** | Tạo yêu cầu đặt xe | **Empty/Null – Không chọn loại xe** | Customer đã đăng nhập | 1. Nhập điểm đón<br>2. Nhập điểm đến<br>3. Không chọn loại xe<br>4. Gửi yêu cầu | Vehicle type = empty | Hệ thống không tạo booking khi chưa chọn loại xe | High |
| **BOOK-TC-006** | Tạo yêu cầu đặt xe | **Empty/Null – Điểm đón và điểm đến đều để trống** | Customer đã đăng nhập | 1. Không nhập điểm đón<br>2. Không nhập điểm đến<br>3. Chọn loại xe<br>4. Gửi yêu cầu | Pickup = empty<br>Destination = empty | Hệ thống từ chối tạo booking và trả validation tương ứng | High |
| **BOOK-TC-007** | Tạo yêu cầu đặt xe | **Empty/Null – Gửi request với body rỗng** | Booking API đang hoạt động | 1. Gửi request tạo booking<br>2. Không truyền dữ liệu body | Body = `{}` hoặc `null` | Hệ thống từ chối request; booking không được tạo | High |
| **BOOK-TC-008** | Tạo yêu cầu đặt xe | **Invalid Format/Value – Loại xe không thuộc danh sách được hỗ trợ** | Customer đã đăng nhập; hệ thống có danh sách loại xe hợp lệ | 1. Nhập điểm đón<br>2. Nhập điểm đến<br>3. Gửi loại xe ngoài danh sách hỗ trợ<br>4. Gửi request | Vehicle type = unsupported | Hệ thống từ chối giá trị loại xe không hợp lệ | Medium |
| **BOOK-TC-009** | Tạo yêu cầu đặt xe | **Invalid Format/Value – Điểm đón sai cấu trúc dữ liệu theo Booking API** | Customer đã đăng nhập; API có rule cho dữ liệu điểm đón | 1. Nhập điểm đón sai format<br>2. Nhập dữ liệu còn lại hợp lệ<br>3. Gửi request | Pickup format = invalid | Hệ thống từ chối dữ liệu điểm đón không hợp lệ | Medium |
| **BOOK-TC-010** | Tạo yêu cầu đặt xe | **Invalid Format/Value – Điểm đến sai cấu trúc dữ liệu theo Booking API** | Customer đã đăng nhập; API có rule cho dữ liệu điểm đến | 1. Nhập điểm đón hợp lệ<br>2. Nhập điểm đến sai format<br>3. Chọn loại xe<br>4. Gửi request | Destination format = invalid | Hệ thống từ chối dữ liệu điểm đến không hợp lệ | Medium |
| **BOOK-TC-011** | Tạo yêu cầu đặt xe | **Negative – Customer chưa đăng nhập gửi yêu cầu đặt xe** | Customer chưa được xác thực | 1. Không đăng nhập<br>2. Gửi request tạo booking | Authentication = missing | Hệ thống từ chối tạo booking | High |
| **BOOK-TC-012** | Tạo yêu cầu đặt xe | **Negative – Gửi booking với token xác thực không hợp lệ** | Booking API yêu cầu authentication | 1. Chuẩn bị booking hợp lệ<br>2. Gửi request với token không hợp lệ | Token = invalid | Hệ thống từ chối request; booking không được tạo | High |
| **BOOK-TC-013** | Tạo yêu cầu đặt xe | **Negative – Actor không phải Customer gửi yêu cầu đặt xe** | Actor đã đăng nhập nhưng không thuộc actor được phép tạo booking | 1. Đăng nhập bằng actor khác<br>2. Gửi request tạo booking | Actor ≠ Customer | Hệ thống không cho actor ngoài phạm vi Customer tạo booking | High |
| **BOOK-TC-014** | Tạo yêu cầu đặt xe | **Boundary – Request chứa vừa đủ các thông tin nghiệp vụ bắt buộc** | Customer đã đăng nhập | 1. Chỉ cung cấp điểm đón, điểm đến và loại xe hợp lệ<br>2. Gửi request | Pickup = valid<br>Destination = valid<br>Vehicle type = valid | Booking được tạo thành công khi đã có đủ các thông tin bắt buộc theo SRS | Medium |
| **BOOK-TC-015** | Tạo yêu cầu đặt xe | **Boundary – Thiếu đúng một thông tin bắt buộc của booking** | Customer đã đăng nhập | 1. Chuẩn bị request hợp lệ<br>2. Loại bỏ một trong ba thông tin: điểm đón, điểm đến hoặc loại xe<br>3. Gửi request | Required fields = 2/3 | Hệ thống không tạo booking khi thiếu một thông tin bắt buộc | High |
| **BOOK-TC-016** | Tra cứu booking | **Positive – Customer truy cập booking của chính mình** | Customer đã đăng nhập và đã có booking trong hệ thống | 1. Gửi yêu cầu xem booking của chính Customer<br>2. Kiểm tra response | Booking = exists<br>Owner = current Customer | Hệ thống trả thông tin booking tương ứng | Medium |
| **BOOK-TC-017** | Tra cứu booking | **Negative – Booking không tồn tại** | Customer đã đăng nhập | 1. Gửi yêu cầu tra cứu booking không tồn tại | Booking ID = not found | Hệ thống không trả về booking và phản hồi trạng thái không tìm thấy phù hợp | Medium |
| **BOOK-TC-018** | Tra cứu booking | **Invalid Format/Value – Booking ID sai định dạng** | Customer đã đăng nhập; Booking API có quy định định dạng ID | 1. Gửi request với Booking ID sai định dạng | Booking ID = invalid format | Hệ thống từ chối giá trị ID không hợp lệ | Medium |
| **BOOK-TC-019** | Tra cứu booking | **Negative – Customer truy cập booking không thuộc tài khoản của mình** | Customer A và Customer B tồn tại; booking thuộc Customer B | 1. Đăng nhập Customer A<br>2. Gửi request truy cập booking của Customer B | Current user = Customer A<br>Booking owner = Customer B | Hệ thống không cho Customer A truy cập booking không thuộc mình | High |
| **BOOK-TC-020** | Response tạo booking | **Positive – Response sau khi tạo booking phản ánh đúng yêu cầu đã ghi nhận** | Customer đã đăng nhập và gửi booking hợp lệ | 1. Tạo booking hợp lệ<br>2. Nhận response<br>3. Kiểm tra dữ liệu booking trả về | Pickup = valid<br>Destination = valid<br>Vehicle type = valid | Response xác nhận booking đã được ghi nhận và dữ liệu chính phù hợp với yêu cầu khách hàng đã gửi | High |

# TEST CASE –Driver Location & Matching 

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
|---|---|---|---|---|---|---|---|
| **DLM-TC-001** | Cập nhật vị trí tài xế | **Positive – Cập nhật vị trí tài xế hợp lệ** | Driver đã đăng nhập và đang hoạt động | 1. Gửi thông tin vị trí hợp lệ<br>2. Kiểm tra dữ liệu được ghi nhận | DriverLocation = valid | Hệ thống lưu vị trí tài xế thành công | High |
| **DLM-TC-002** | Cập nhật vị trí tài xế | **Positive – Cập nhật vị trí mới thay thế vị trí trước đó** | Driver đã có thông tin vị trí trước đó | 1. Gửi vị trí mới<br>2. Kiểm tra thông tin vị trí hiện tại | Old location = A<br>New location = B | Hệ thống ghi nhận vị trí mới để phục vụ quá trình tìm tài xế | High |
| **DLM-TC-003** | Cập nhật vị trí tài xế | **Empty/Null – Gửi vị trí rỗng** | Driver đã đăng nhập | 1. Gửi request cập nhật vị trí<br>2. Không truyền dữ liệu vị trí | DriverLocation = null | Hệ thống không ghi nhận vị trí rỗng là vị trí hợp lệ | High |
| **DLM-TC-004** | Cập nhật vị trí tài xế | **Invalid Format/Value – Dữ liệu vị trí không đúng cấu trúc API** | Driver đã đăng nhập | 1. Gửi dữ liệu vị trí sai cấu trúc<br>2. Kiểm tra response | DriverLocation format = invalid | Hệ thống từ chối dữ liệu vị trí không hợp lệ | Medium |
| **DLM-TC-005** | Cập nhật vị trí tài xế | **Negative – Driver chưa xác thực gửi cập nhật vị trí** | Driver chưa đăng nhập | 1. Không đăng nhập<br>2. Gửi request cập nhật vị trí | Authentication = missing | Hệ thống từ chối cập nhật vị trí | High |
| **DLM-TC-006** | Cập nhật vị trí tài xế | **Negative – Token xác thực không hợp lệ** | Driver gọi Driver Location API | 1. Gửi vị trí hợp lệ<br>2. Sử dụng token không hợp lệ | Token = invalid | Hệ thống từ chối request và không cập nhật vị trí | High |
| **DLM-TC-007** | Cập nhật vị trí tài xế | **Boundary – Tài xế vừa có vị trí hợp lệ thì có thể được xét trong matching** | Driver đang ở trạng thái sẵn sàng nhưng trước đó chưa có vị trí hợp lệ | 1. Chạy matching khi chưa có vị trí<br>2. Cập nhật vị trí hợp lệ<br>3. Chạy matching lại | Location: null → valid | Sau khi có vị trí hợp lệ, tài xế có thể được hệ thống xem xét trong quá trình matching | High |
| **DLM-TC-008** | Tìm tài xế phù hợp | **Positive – Xác định tài xế dựa trên vị trí và trạng thái sẵn sàng** | Có booking hợp lệ; có tài xế đang sẵn sàng và có vị trí | 1. Bắt đầu matching<br>2. Kiểm tra danh sách tài xế<br>3. Xác định tài xế phù hợp | Driver status = available<br>Location = valid | Hệ thống xác định được tài xế phù hợp | High |
| **DLM-TC-009** | Tìm tài xế phù hợp | **Positive – Ưu tiên tài xế phù hợp và gần khách hàng hơn** | Có ít nhất hai tài xế phù hợp | 1. Bắt đầu matching<br>2. So sánh vị trí các tài xế<br>3. Kiểm tra thứ tự ưu tiên | Driver A = gần hơn<br>Driver B = xa hơn | Hệ thống ưu tiên tài xế phù hợp và gần khách hàng | High |
| **DLM-TC-010** | Tìm tài xế phù hợp | **Negative – Tài xế không ở trạng thái sẵn sàng** | Có booking đang tìm tài xế | 1. Đưa tài xế không sẵn sàng vào danh sách ứng viên<br>2. Chạy matching | Driver status = unavailable | Hệ thống không chọn tài xế không sẵn sàng | High |
| **DLM-TC-011** | Tìm tài xế phù hợp | **Negative – Tài xế không có thông tin vị trí hợp lệ** | Có booking đang matching | 1. Có tài xế sẵn sàng nhưng không có vị trí<br>2. Chạy matching | Driver status = available<br>Location = null | Hệ thống không sử dụng vị trí rỗng để xác định tài xế là gần khách hàng | High |
| **DLM-TC-012** | Tìm tài xế phù hợp | **Invalid Format/Value – Vị trí tài xế không hợp lệ trong quá trình matching** | Có booking đang matching | 1. Đưa tài xế có dữ liệu vị trí không hợp lệ vào danh sách ứng viên<br>2. Chạy matching | DriverLocation = invalid | Hệ thống không sử dụng dữ liệu vị trí không hợp lệ để ưu tiên tài xế | Medium |
| **DLM-TC-013** | Tìm tài xế phù hợp | **Empty/Null – Không có tài xế trong danh sách ứng viên** | Có booking hợp lệ | 1. Bắt đầu matching<br>2. Danh sách tài xế ứng viên rỗng | Candidate drivers = empty | Hệ thống xác định không tìm được tài xế phù hợp và chuyển sang xử lý trường hợp không có tài xế | High |
| **DLM-TC-014** | Tìm tài xế phù hợp | **Negative – Có tài xế nhưng không tài xế nào đáp ứng tiêu chí matching** | Có booking hợp lệ | 1. Bắt đầu matching<br>2. Kiểm tra các tài xế<br>3. Không tài xế nào thỏa điều kiện | Suitable drivers = none | Hệ thống không phân công tài xế không phù hợp | High |
| **DLM-TC-015** | Tìm tài xế phù hợp | **Positive – Gửi yêu cầu chuyến đến tài xế được chọn** | Hệ thống đã xác định được tài xế phù hợp | 1. Hoàn tất matching<br>2. Chọn tài xế phù hợp<br>3. Gửi yêu cầu chuyến | Selected Driver = valid | Hệ thống gửi yêu cầu chuyến đến tài xế phù hợp | High |
| **DLM-TC-016** | Matching lại tài xế | **Negative – Tài xế được chọn từ chối và hệ thống tìm tài xế khác** | Tài xế đã nhận yêu cầu chuyến | 1. Tài xế từ chối<br>2. Hệ thống nhận kết quả từ chối<br>3. Kiểm tra matching tiếp theo | Driver response = Reject | Hệ thống tiếp tục tìm tài xế khác mà Customer không phải tạo lại booking | High |
| **DLM-TC-017** | Matching lại tài xế | **Boundary – Tài xế không phản hồi đến ngưỡng thời gian cấu hình** | Tài xế đã được gửi yêu cầu chuyến | 1. Gửi yêu cầu chuyến<br>2. Không có phản hồi<br>3. Đến ngưỡng timeout cấu hình<br>4. Kiểm tra matching | Driver response = none<br>Timeout = theo cấu hình | Hệ thống chuyển sang tìm tài xế khác | High |
| **DLM-TC-018** | Matching lại tài xế | **Positive – Tài xế tiếp theo phù hợp được chọn sau khi tài xế trước từ chối** | Tài xế đầu tiên đã từ chối; còn tài xế phù hợp khác | 1. Nhận kết quả từ chối<br>2. Chạy matching lại<br>3. Chọn tài xế tiếp theo | Driver A = Reject<br>Driver B = suitable | Hệ thống tiếp tục matching và gửi yêu cầu đến tài xế phù hợp tiếp theo | High |
| **DLM-TC-019** | Không tìm được tài xế | **Negative – Không còn tài xế phù hợp sau quá trình matching** | Các tài xế phù hợp đã từ chối, không phản hồi hoặc không còn ứng viên | 1. Thực hiện matching<br>2. Kiểm tra toàn bộ ứng viên<br>3. Không còn tài xế phù hợp | Remaining suitable drivers = none | Hệ thống kết thúc quá trình tìm kiếm và xác định không tìm được tài xế | High |
| **DLM-TC-020** | Không tìm được tài xế | **Positive – Thông báo Customer khi không tìm được tài xế** | Matching đã kết thúc và không có tài xế phù hợp | 1. Hoàn tất quá trình matching thất bại<br>2. Kiểm tra kết quả trả về cho Customer | Matching result = No Driver | Hệ thống thông báo rõ ràng cho Customer rằng không tìm được tài xế phù hợp | High |

# TEST CASE – Trip Request & Trip

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
|---|---|---|---|---|---|---|---|
| **TRIP-TC-001** | Phản hồi yêu cầu chuyến | **Positive – Driver chấp nhận yêu cầu chuyến hợp lệ** | Driver đã đăng nhập, đang sẵn sàng và nhận được yêu cầu chuyến | 1. Mở yêu cầu chuyến<br>2. Chọn Chấp nhận<br>3. Gửi phản hồi | Request = valid<br>Response = Accept | Hệ thống ghi nhận Driver chấp nhận và phân công Driver cho chuyến | High |
| **TRIP-TC-002** | Phản hồi yêu cầu chuyến | **Positive – Driver từ chối yêu cầu chuyến** | Driver đã nhận được yêu cầu chuyến | 1. Mở yêu cầu chuyến<br>2. Chọn Từ chối<br>3. Gửi phản hồi | Response = Reject | Hệ thống ghi nhận từ chối và tiếp tục quá trình tìm Driver khác | High |
| **TRIP-TC-003** | Phản hồi yêu cầu chuyến | **Negative – Driver chưa đăng nhập thực hiện Accept** | Driver chưa được xác thực | 1. Không đăng nhập<br>2. Gửi yêu cầu Accept | Authentication = missing | Hệ thống từ chối thao tác chấp nhận chuyến | High |
| **TRIP-TC-004** | Phản hồi yêu cầu chuyến | **Negative – Driver chưa đăng nhập thực hiện Reject** | Driver chưa được xác thực | 1. Không đăng nhập<br>2. Gửi yêu cầu Reject | Authentication = missing | Hệ thống từ chối thao tác từ chối chuyến | High |
| **TRIP-TC-005** | Phản hồi yêu cầu chuyến | **Negative – Driver khác cố phản hồi yêu cầu chuyến không được gửi cho mình** | Driver A đã nhận yêu cầu; Driver B đã đăng nhập | 1. Đăng nhập Driver B<br>2. Gửi Accept/Reject cho request của Driver A | Assigned Driver = A<br>Current Driver = B | Hệ thống không cho Driver B phản hồi yêu cầu không thuộc mình | High |
| **TRIP-TC-006** | Phản hồi yêu cầu chuyến | **Invalid Format/Value – Request ID sai định dạng** | Driver đã đăng nhập | 1. Gửi Accept hoặc Reject với Request ID sai định dạng | Request ID = invalid format | Hệ thống từ chối request không hợp lệ | Medium |
| **TRIP-TC-007** | Phản hồi yêu cầu chuyến | **Negative – Request ID không tồn tại** | Driver đã đăng nhập | 1. Gửi Accept/Reject với Request ID không tồn tại | Request ID = not found | Hệ thống không ghi nhận phản hồi và trả kết quả không tìm thấy | Medium |
| **TRIP-TC-008** | Phản hồi yêu cầu chuyến | **Empty/Null – Không truyền Request ID** | Driver đã đăng nhập | 1. Gửi request Accept/Reject<br>2. Không truyền Request ID | Request ID = null | Hệ thống từ chối request do thiếu thông tin cần thiết | High |
| **TRIP-TC-009** | Phản hồi yêu cầu chuyến | **Boundary – Driver không phản hồi đến thời điểm timeout cấu hình** | Driver đã nhận yêu cầu chuyến | 1. Không gửi Accept/Reject<br>2. Chờ đến timeout cấu hình<br>3. Kiểm tra kết quả | Response = none<br>Timeout = theo cấu hình | Hệ thống xem là không phản hồi và tiếp tục tìm Driver khác | High |
| **TRIP-TC-010** | Phản hồi yêu cầu chuyến | **Negative – Driver không ở trạng thái sẵn sàng cố chấp nhận chuyến** | Driver đã nhận request nhưng trạng thái hiện tại không sẵn sàng | 1. Gửi Accept<br>2. Kiểm tra kết quả | Driver status = unavailable | Hệ thống không hoàn tất phân công cho Driver không đáp ứng điều kiện sẵn sàng | High |
| **TRIP-TC-011** | Cập nhật trạng thái chuyến | **Positive – Cập nhật trạng thái Đã đến điểm đón** | Trip đã được phân công cho Driver | 1. Mở Trip<br>2. Cập nhật trạng thái Đã đến điểm đón | Trip status = Arrived at pickup | Hệ thống ghi nhận trạng thái mới của chuyến | High |
| **TRIP-TC-012** | Cập nhật trạng thái chuyến | **Positive – Cập nhật trạng thái Đã đón khách** | Trip đang được thực hiện | 1. Mở Trip<br>2. Cập nhật trạng thái Đã đón khách | Trip status = Passenger picked up | Hệ thống ghi nhận trạng thái Đã đón khách | High |
| **TRIP-TC-013** | Cập nhật trạng thái chuyến | **Positive – Cập nhật trạng thái Đang di chuyển** | Trip đang được thực hiện | 1. Mở Trip<br>2. Cập nhật trạng thái Đang di chuyển | Trip status = In progress | Hệ thống ghi nhận trạng thái Đang di chuyển | High |
| **TRIP-TC-014** | Cập nhật trạng thái chuyến | **Positive – Cập nhật trạng thái Hoàn thành chuyến** | Trip đang được thực hiện | 1. Mở Trip<br>2. Cập nhật trạng thái Hoàn thành | Trip status = Completed | Hệ thống ghi nhận chuyến hoàn thành và chuyển sang bước xác định số tiền phải trả | High |
| **TRIP-TC-015** | Cập nhật trạng thái chuyến | **Empty/Null – Không truyền trạng thái chuyến** | Driver đã đăng nhập và Trip tồn tại | 1. Gửi request cập nhật Trip<br>2. Không truyền status | Trip status = null | Hệ thống từ chối cập nhật do thiếu trạng thái | High |
| **TRIP-TC-016** | Cập nhật trạng thái chuyến | **Invalid Format/Value – Trạng thái không thuộc danh sách được hỗ trợ** | Driver đã đăng nhập và Trip tồn tại | 1. Gửi giá trị trạng thái ngoài danh sách hợp lệ<br>2. Kiểm tra kết quả | Trip status = unsupported value | Hệ thống không cập nhật trạng thái không hợp lệ | Medium |
| **TRIP-TC-017** | Cập nhật trạng thái chuyến | **Negative – Driver khác cập nhật Trip không được phân công cho mình** | Trip thuộc Driver A; Driver B đã đăng nhập | 1. Đăng nhập Driver B<br>2. Gửi request cập nhật Trip của Driver A | Assigned Driver = A<br>Current Driver = B | Hệ thống từ chối cập nhật chuyến không thuộc Driver hiện tại | High |
| **TRIP-TC-018** | Cập nhật trạng thái chuyến | **Negative – Trip ID không tồn tại** | Driver đã đăng nhập | 1. Gửi request cập nhật trạng thái với Trip ID không tồn tại | Trip ID = not found | Hệ thống không cập nhật và phản hồi trạng thái không tìm thấy | Medium |
| **TRIP-TC-019** | Theo dõi chuyến | **Positive – Customer xem trạng thái hiện tại của chuyến** | Customer đã đăng nhập và có Trip đang thực hiện | 1. Mở Theo dõi chuyến<br>2. Xem trạng thái hiện tại | Trip = active | Hệ thống hiển thị trạng thái hiện tại của chuyến cho Customer | High |
| **TRIP-TC-020** | Hoàn thành chuyến | **Boundary – Sau khi Trip chuyển sang Completed thì bắt đầu bước tính cước** | Trip đang ở trạng thái trước Completed | 1. Kiểm tra trước khi hoàn thành<br>2. Cập nhật Trip = Completed<br>3. Kiểm tra bước tiếp theo | Trip status: active → Completed | Trước Completed chưa tính cước; sau Completed hệ thống chuyển sang xác định số tiền phải trả | High |

 # TEST CASE – Fare & Payment

 | Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
|---|---|---|---|---|---|---|---|
| **FP-TC-001** | Tính cước chuyến đi | **Positive – Tính cước sau khi chuyến đã hoàn thành** | Trip tồn tại và đã ở trạng thái Completed | 1. Hoàn thành Trip<br>2. Yêu cầu hệ thống xác định Fare<br>3. Kiểm tra kết quả | Trip status = Completed<br>Trip information = valid | Hệ thống xác định số tiền khách hàng phải trả dựa trên loại dịch vụ và thông tin chuyến đi | High |
| **FP-TC-002** | Tính cước chuyến đi | **Boundary – Không tính cước trước khi Trip chuyển sang Completed** | Trip đang được thực hiện và chưa hoàn thành | 1. Giữ Trip ở trạng thái chưa Completed<br>2. Yêu cầu tính cước | Trip status ≠ Completed | Hệ thống chưa thực hiện bước xác định số tiền phải trả | High |
| **FP-TC-003** | Tính cước chuyến đi | **Boundary – Tính cước ngay sau khi Trip chuyển sang Completed** | Trip đang ở trạng thái trước Completed | 1. Cập nhật Trip sang Completed<br>2. Kiểm tra bước xử lý tiếp theo | Trip status: active → Completed | Sau khi Trip hoàn thành, hệ thống chuyển sang bước xác định số tiền phải trả | High |
| **FP-TC-004** | Tính cước chuyến đi | **Negative – Trip không tồn tại** | Hệ thống đang hoạt động | 1. Gửi yêu cầu lấy/tính Fare cho Trip không tồn tại | Trip ID = not found | Hệ thống không tạo Fare cho Trip không tồn tại và trả kết quả phù hợp | Medium |
| **FP-TC-005** | Tính cước chuyến đi | **Empty/Null – Không truyền Trip ID** | Fare API đang hoạt động | 1. Gửi yêu cầu tính/lấy Fare<br>2. Không truyền Trip ID | Trip ID = null | Hệ thống từ chối request do thiếu thông tin xác định chuyến | High |
| **FP-TC-006** | Tính cước chuyến đi | **Invalid Format/Value – Trip ID sai định dạng** | Fare API có quy định định dạng Trip ID | 1. Gửi request với Trip ID sai định dạng | Trip ID = invalid format | Hệ thống từ chối giá trị Trip ID không hợp lệ | Medium |
| **FP-TC-007** | Thanh toán | **Positive – Customer chọn thanh toán bằng tiền mặt** | Trip đã hoàn thành và Fare đã được xác định | 1. Mở bước Thanh toán<br>2. Chọn Tiền mặt<br>3. Xác nhận | Payment method = Cash | Hệ thống ghi nhận phương thức thanh toán tiền mặt cho chuyến | High |
| **FP-TC-008** | Thanh toán | **Positive – Customer chọn thanh toán điện tử** | Trip đã hoàn thành và Fare đã được xác định | 1. Mở bước Thanh toán<br>2. Chọn Thanh toán điện tử<br>3. Xác nhận | Payment method = Electronic | Hệ thống tiếp nhận yêu cầu thanh toán điện tử và chuyển giao dịch đến Payment Provider | High |
| **FP-TC-009** | Thanh toán | **Empty/Null – Không chọn phương thức thanh toán** | Trip đã hoàn thành và Fare đã được xác định | 1. Mở bước Thanh toán<br>2. Không chọn phương thức<br>3. Xác nhận | Payment method = null | Hệ thống không hoàn tất thanh toán khi chưa có phương thức hợp lệ | High |
| **FP-TC-010** | Thanh toán | **Invalid Format/Value – Phương thức thanh toán không được hỗ trợ** | Trip đã hoàn thành và có Fare | 1. Gửi giá trị payment method ngoài các phương thức hệ thống hỗ trợ<br>2. Xác nhận | Payment method = unsupported | Hệ thống từ chối phương thức thanh toán không hợp lệ | Medium |
| **FP-TC-011** | Thanh toán | **Negative – Thực hiện thanh toán khi Trip chưa hoàn thành** | Trip chưa ở trạng thái Completed | 1. Truy cập bước thanh toán<br>2. Thử thực hiện thanh toán | Trip status ≠ Completed | Hệ thống không thực hiện thanh toán khi chuyến chưa hoàn thành và chưa xác định Fare | High |
| **FP-TC-012** | Thanh toán điện tử | **Positive – Payment Provider trả kết quả thanh toán thành công** | Giao dịch điện tử đã được gửi đến Payment Provider | 1. Provider xử lý giao dịch<br>2. Provider trả Success<br>3. Kiểm tra Payment trong CAB | Provider response = Success | Hệ thống ghi nhận thanh toán thành công và hoàn tất quá trình thanh toán | High |
| **FP-TC-013** | Thanh toán điện tử | **Negative – Payment Provider trả kết quả thanh toán thất bại** | Giao dịch điện tử đã được gửi đến Payment Provider | 1. Provider xử lý giao dịch<br>2. Provider trả Failed<br>3. Kiểm tra phản hồi hệ thống | Provider response = Failed | Hệ thống ghi nhận giao dịch thất bại và thông báo cho Customer | High |
| **FP-TC-014** | Xử lý thanh toán thất bại | **Positive – Thử lại thanh toán điện tử sau khi giao dịch thất bại** | Thanh toán điện tử trước đó đã thất bại | 1. Nhận thông báo thanh toán thất bại<br>2. Chọn thực hiện lại thanh toán điện tử<br>3. Gửi lại giao dịch | Previous payment = Failed<br>Retry = Electronic | Hệ thống cho phép xử lý lại giao dịch theo chính sách doanh nghiệp | High |
| **FP-TC-015** | Xử lý thanh toán thất bại | **Positive – Chuyển sang tiền mặt sau khi thanh toán điện tử thất bại** | Thanh toán điện tử trước đó đã thất bại | 1. Nhận thông báo thất bại<br>2. Chọn phương thức Tiền mặt<br>3. Xác nhận | Previous payment = Failed<br>New method = Cash | Hệ thống cho phép chuyển sang thanh toán tiền mặt và ghi nhận phương thức mới | High |
| **FP-TC-016** | Thanh toán điện tử | **Negative – Payment Provider xảy ra lỗi khi xử lý giao dịch** | Customer đã chọn thanh toán điện tử | 1. Gửi giao dịch đến Payment Provider<br>2. Mô phỏng lỗi Provider<br>3. Kiểm tra CAB System | Payment Provider = error | Hệ thống xử lý lỗi thanh toán mà không làm toàn bộ dịch vụ đặt xe ngừng hoạt động | High |
| **FP-TC-017** | Thanh toán điện tử | **Empty/Null – Payment Provider không trả kết quả giao dịch** | Giao dịch đã được gửi đến Payment Provider | 1. Gửi giao dịch điện tử<br>2. Không nhận kết quả hợp lệ từ Provider<br>3. Kiểm tra trạng thái giao dịch | Provider response = null | Hệ thống không ghi nhận giao dịch là thanh toán thành công khi chưa có kết quả hợp lệ | High |
| **FP-TC-018** | Thanh toán điện tử | **Invalid Format/Value – Kết quả từ Payment Provider không thuộc trạng thái được hỗ trợ** | Giao dịch điện tử đang được xử lý | 1. Provider trả giá trị trạng thái không hợp lệ<br>2. Kiểm tra xử lý của CAB | Provider response = unsupported value | Hệ thống không ghi nhận trạng thái thanh toán không hợp lệ là thành công | Medium |
| **FP-TC-019** | Bảo vệ dữ liệu thanh toán | **Security – CAB không lưu trực tiếp thông tin nhạy cảm của thẻ hoặc tài khoản thanh toán** | Customer thực hiện thanh toán điện tử | 1. Thực hiện giao dịch điện tử<br>2. Kiểm tra dữ liệu CAB lưu trữ hoặc ghi log | Sensitive payment information | Hệ thống không lưu trực tiếp thông tin nhạy cảm của thẻ hoặc tài khoản thanh toán | High |
| **FP-TC-020** | Kết thúc thanh toán | **Positive – Thanh toán thành công kết thúc quy trình chuyến xe** | Trip đã hoàn thành; Fare đã xác định; Payment thành công | 1. Hoàn tất thanh toán<br>2. Kiểm tra trạng thái xử lý cuối cùng | Trip = Completed<br>Payment = Success | Hệ thống ghi nhận kết quả thanh toán và kết thúc quy trình chuyến xe | High |

# TEST CASE – Notification  

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
|---|---|---|---|---|---|---|---|
| **NOTI-TC-001** | Thông báo booking | **Positive – Gửi thông báo cho Customer khi yêu cầu đặt xe được tiếp nhận** | Customer đã gửi booking hợp lệ và hệ thống đã ghi nhận booking | 1. Customer tạo booking<br>2. Hệ thống ghi nhận booking<br>3. Kích hoạt Notification | Event = Booking Received<br>Recipient = Customer | Customer nhận được thông báo yêu cầu đặt xe đã được tiếp nhận | High |
| **NOTI-TC-002** | Thông báo tài xế nhận chuyến | **Positive – Gửi thông báo cho Customer khi Driver chấp nhận chuyến** | Driver đã nhận yêu cầu chuyến và thực hiện Accept | 1. Driver chấp nhận chuyến<br>2. Hệ thống ghi nhận phân công<br>3. Kích hoạt Notification | Event = Driver Accepted<br>Recipient = Customer | Customer nhận được thông báo Driver đã nhận chuyến | High |
| **NOTI-TC-003** | Thông báo tài xế đến điểm đón | **Positive – Gửi thông báo cho Customer khi Driver đến điểm đón** | Trip đã được phân công và Driver cập nhật trạng thái Đã đến điểm đón | 1. Driver cập nhật trạng thái<br>2. Hệ thống ghi nhận trạng thái<br>3. Gửi Notification | Event = Driver Arrived<br>Recipient = Customer | Customer nhận được thông báo Driver đã đến điểm đón | High |
| **NOTI-TC-004** | Thông báo hoàn thành chuyến | **Positive – Gửi thông báo cho Customer khi Trip hoàn thành** | Trip đang thực hiện và Driver cập nhật Completed | 1. Driver hoàn thành chuyến<br>2. Hệ thống ghi nhận Completed<br>3. Kích hoạt Notification | Event = Trip Completed<br>Recipient = Customer | Customer nhận được thông báo chuyến đã hoàn thành | High |
| **NOTI-TC-005** | Thông báo thanh toán | **Positive – Gửi thông báo khi thanh toán điện tử thành công** | Payment Provider đã trả kết quả Success | 1. Provider trả Success<br>2. Hệ thống ghi nhận Payment<br>3. Gửi Notification | Event = Payment Success<br>Recipient = Customer | Customer nhận được thông báo thanh toán thành công | High |
| **NOTI-TC-006** | Thông báo thanh toán | **Positive – Gửi thông báo khi thanh toán điện tử thất bại** | Payment Provider đã trả kết quả Failed | 1. Provider trả Failed<br>2. Hệ thống ghi nhận kết quả<br>3. Gửi Notification | Event = Payment Failed<br>Recipient = Customer | Customer nhận được thông báo thanh toán thất bại | High |
| **NOTI-TC-007** | Thông báo chuyến mới | **Positive – Gửi thông báo chuyến mới cho Driver** | Hệ thống đã matching được Driver phù hợp | 1. Xác định Driver phù hợp<br>2. Tạo Trip Request<br>3. Kích hoạt Notification | Event = New Trip Request<br>Recipient = Driver | Driver nhận được thông báo về yêu cầu chuyến mới | High |
| **NOTI-TC-008** | Thông báo cho Driver | **Positive – Gửi thông báo khi có thay đổi liên quan đến chuyến đang thực hiện** | Driver đang thực hiện Trip và có sự kiện liên quan đến Trip | 1. Phát sinh thay đổi của Trip<br>2. Kích hoạt Notification<br>3. Kiểm tra Driver | Event = Trip Update<br>Recipient = Driver | Driver nhận được thông báo về thay đổi liên quan đến chuyến | Medium |
| **NOTI-TC-009** | Gửi thông báo | **Empty/Null – Không có Recipient** | Notification API đang hoạt động | 1. Tạo Notification<br>2. Không truyền người nhận<br>3. Gửi request | Recipient = null | Hệ thống không gửi Notification khi không xác định được người nhận | High |
| **NOTI-TC-010** | Gửi thông báo | **Empty/Null – Không có Event/loại thông báo** | Notification API đang hoạt động | 1. Tạo request Notification<br>2. Không truyền Event<br>3. Gửi request | Event = null | Hệ thống từ chối request do thiếu thông tin sự kiện cần thông báo | High |
| **NOTI-TC-011** | Gửi thông báo | **Empty/Null – Body request rỗng** | Notification API đang hoạt động | 1. Gửi request Notification<br>2. Không truyền dữ liệu body | Body = `{}` hoặc `null` | Hệ thống từ chối request và không tạo Notification | High |
| **NOTI-TC-012** | Gửi thông báo | **Invalid Format/Value – Event không thuộc loại sự kiện được hỗ trợ** | Notification API có danh sách event hợp lệ | 1. Gửi Notification với event không hợp lệ<br>2. Kiểm tra response | Event = unsupported value | Hệ thống không gửi Notification cho event không hợp lệ | Medium |
| **NOTI-TC-013** | Gửi thông báo | **Invalid Format/Value – Recipient ID sai định dạng** | Notification API có quy định định dạng ID | 1. Gửi request với Recipient ID sai định dạng | Recipient ID = invalid format | Hệ thống từ chối giá trị Recipient ID không hợp lệ | Medium |
| **NOTI-TC-014** | Gửi thông báo | **Negative – Recipient không tồn tại trong hệ thống** | Notification API đang hoạt động | 1. Tạo Notification<br>2. Truyền Recipient không tồn tại<br>3. Gửi request | Recipient = not found | Hệ thống không gửi thông báo đến người nhận không tồn tại | Medium |
| **NOTI-TC-015** | Gửi thông báo | **Negative – Gửi thông báo sai đối tượng nhận** | Event dành cho Customer nhưng request xác định Driver hoặc ngược lại | 1. Tạo Notification<br>2. Gán sai loại Recipient<br>3. Gửi request | Event = Customer Event<br>Recipient = Driver | Hệ thống không gửi thông báo nghiệp vụ đến sai đối tượng | High |
| **NOTI-TC-016** | Notification Provider | **Negative – Notification Provider xảy ra lỗi khi gửi thông báo** | Có sự kiện hợp lệ cần gửi thông báo | 1. Kích hoạt Notification<br>2. Mô phỏng Provider lỗi<br>3. Kiểm tra hệ thống | Notification Provider = error | Lỗi Notification không làm toàn bộ hệ thống đặt xe ngừng hoạt động | High |
| **NOTI-TC-017** | Notification Provider | **Empty/Null – Provider không trả kết quả gửi thông báo** | Notification đã được chuyển đến Provider | 1. Gửi Notification đến Provider<br>2. Provider không trả kết quả hợp lệ<br>3. Kiểm tra trạng thái | Provider response = null | Hệ thống không ghi nhận việc gửi thông báo là thành công khi chưa có kết quả hợp lệ | Medium |
| **NOTI-TC-018** | Notification Provider | **Invalid Format/Value – Provider trả trạng thái không được hỗ trợ** | Notification đã được gửi đến Provider | 1. Provider trả trạng thái không hợp lệ<br>2. Kiểm tra kết quả xử lý | Provider response = unsupported value | Hệ thống không ghi nhận trạng thái gửi Notification không hợp lệ là thành công | Medium |
| **NOTI-TC-019** | Thay đổi Notification Provider | **Boundary – Thay đổi Provider nhưng luồng nghiệp vụ Notification vẫn hoạt động** | Hệ thống hỗ trợ thay đổi hoặc bổ sung Notification Provider | 1. Gửi Notification với Provider hiện tại<br>2. Thay đổi Provider<br>3. Gửi lại Notification hợp lệ | Provider A → Provider B | Hệ thống vẫn gửi được thông báo mà không phải xây dựng lại toàn bộ ứng dụng | Medium |
| **NOTI-TC-020** | Độ tin cậy Notification | **Negative – Notification thất bại nhưng Booking/Trip/Payment vẫn tiếp tục hoạt động** | Notification component đang lỗi | 1. Mô phỏng Notification lỗi<br>2. Thực hiện Booking/Trip/Payment<br>3. Kiểm tra các chức năng chính | Notification Service = unavailable | Lỗi Notification không làm gián đoạn toàn bộ dịch vụ đặt xe và các chức năng chính vẫn tiếp tục hoạt động | High |

# TEST CASE – Trip History & Rating

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
|---|---|---|---|---|---|---|---|
| **THR-TC-001** | Xem lịch sử chuyến | **Positive – Customer xem danh sách các chuyến đã thực hiện** | Customer đã đăng nhập và có lịch sử chuyến | 1. Mở chức năng Lịch sử chuyến<br>2. Yêu cầu xem danh sách | Trip history = available | Hệ thống hiển thị các chuyến đã thực hiện của Customer | High |
| **THR-TC-002** | Xem lịch sử chuyến | **Positive – Xem thông tin chi tiết của một chuyến trong lịch sử** | Customer đã đăng nhập và có chuyến đã thực hiện | 1. Mở Lịch sử chuyến<br>2. Chọn một chuyến<br>3. Xem chi tiết | Trip = exists | Hệ thống hiển thị thông tin liên quan đến chuyến được chọn | High |
| **THR-TC-003** | Xem lịch sử chuyến | **Positive – Hiển thị số tiền phải trả của chuyến đã thực hiện** | Trip đã hoàn thành và đã xác định Fare | 1. Mở lịch sử chuyến<br>2. Chọn chuyến đã hoàn thành<br>3. Kiểm tra thông tin Fare | Trip = Completed<br>Fare = available | Hệ thống hiển thị thông tin số tiền phải trả của chuyến | High |
| **THR-TC-004** | Xem lịch sử chuyến | **Empty/Null – Customer chưa có lịch sử chuyến** | Customer đã đăng nhập nhưng chưa thực hiện chuyến nào | 1. Mở chức năng Lịch sử chuyến<br>2. Kiểm tra kết quả | Trip history = empty | Hệ thống hiển thị trạng thái không có dữ liệu lịch sử chuyến | Medium |
| **THR-TC-005** | Xem lịch sử chuyến | **Negative – Customer chưa đăng nhập truy cập lịch sử chuyến** | Customer chưa xác thực | 1. Không đăng nhập<br>2. Truy cập chức năng Lịch sử chuyến | Authentication = missing | Hệ thống từ chối truy cập lịch sử chuyến | High |
| **THR-TC-006** | Xem lịch sử chuyến | **Negative – Token xác thực không hợp lệ** | Customer gọi Trip History API | 1. Gửi request xem lịch sử<br>2. Sử dụng token không hợp lệ | Token = invalid | Hệ thống từ chối request | High |
| **THR-TC-007** | Xem lịch sử chuyến | **Negative – Customer cố xem lịch sử chuyến của Customer khác** | Customer A và Customer B tồn tại | 1. Đăng nhập Customer A<br>2. Yêu cầu truy cập lịch sử của Customer B | Current Customer = A<br>History owner = B | Hệ thống không cho Customer A xem lịch sử chuyến của Customer B | High |
| **THR-TC-008** | Xem chi tiết lịch sử chuyến | **Negative – Trip không tồn tại** | Customer đã đăng nhập | 1. Gửi yêu cầu xem chi tiết Trip không tồn tại | Trip ID = not found | Hệ thống không trả dữ liệu chuyến và phản hồi trạng thái không tìm thấy | Medium |
| **THR-TC-009** | Xem chi tiết lịch sử chuyến | **Invalid Format/Value – Trip ID sai định dạng** | Customer đã đăng nhập; API có rule định dạng ID | 1. Gửi request với Trip ID sai định dạng | Trip ID = invalid format | Hệ thống từ chối Trip ID không hợp lệ | Medium |
| **THR-TC-010** | Xem chi tiết lịch sử chuyến | **Empty/Null – Không truyền Trip ID** | Customer đã đăng nhập | 1. Gửi request xem chi tiết chuyến<br>2. Không truyền Trip ID | Trip ID = null | Hệ thống từ chối request do thiếu thông tin xác định chuyến | Medium |
| **THR-TC-011** | Đánh giá tài xế | **Positive – Customer đánh giá Driver sau khi Trip hoàn thành** | Customer đã đăng nhập; Trip đã Completed | 1. Mở chuyến đã hoàn thành<br>2. Chọn chức năng Đánh giá<br>3. Nhập đánh giá hợp lệ<br>4. Gửi | Trip status = Completed<br>Rating = valid | Hệ thống ghi nhận đánh giá của Customer đối với Driver | High |
| **THR-TC-012** | Đánh giá tài xế | **Boundary – Không cho đánh giá trước khi Trip hoàn thành** | Trip đang được thực hiện và chưa Completed | 1. Mở Trip đang hoạt động<br>2. Thử thực hiện đánh giá | Trip status ≠ Completed | Hệ thống không cho phép Customer hoàn tất đánh giá trước khi chuyến hoàn thành | High |
| **THR-TC-013** | Đánh giá tài xế | **Boundary – Cho phép đánh giá ngay sau khi Trip chuyển sang Completed** | Trip đang ở trạng thái trước Completed | 1. Cập nhật Trip thành Completed<br>2. Mở chức năng Đánh giá<br>3. Gửi đánh giá hợp lệ | Trip status: active → Completed | Sau khi Trip hoàn thành, Customer có thể thực hiện đánh giá Driver | High |
| **THR-TC-014** | Đánh giá tài xế | **Empty/Null – Không truyền nội dung/giá trị đánh giá bắt buộc theo API** | Customer đã đăng nhập và Trip đã hoàn thành | 1. Mở chức năng Đánh giá<br>2. Để trống dữ liệu đánh giá bắt buộc<br>3. Gửi | Rating data = null | Hệ thống không ghi nhận đánh giá khi thiếu dữ liệu bắt buộc theo API | Medium |
| **THR-TC-015** | Đánh giá tài xế | **Invalid Format/Value – Giá trị đánh giá không hợp lệ theo rule Rating API** | Trip đã hoàn thành; Rating API có rule giá trị hợp lệ | 1. Nhập giá trị đánh giá ngoài rule được hỗ trợ<br>2. Gửi đánh giá | Rating = invalid value | Hệ thống từ chối giá trị đánh giá không hợp lệ | Medium |
| **THR-TC-016** | Đánh giá tài xế | **Negative – Customer chưa đăng nhập gửi đánh giá** | Trip đã hoàn thành nhưng Customer chưa xác thực | 1. Không đăng nhập<br>2. Gửi request đánh giá | Authentication = missing | Hệ thống từ chối ghi nhận đánh giá | High |
| **THR-TC-017** | Đánh giá tài xế | **Negative – Customer đánh giá Trip không thuộc tài khoản của mình** | Trip thuộc Customer B; Customer A đã đăng nhập | 1. Đăng nhập Customer A<br>2. Gửi đánh giá cho Trip của Customer B | Current Customer = A<br>Trip owner = B | Hệ thống không cho Customer đánh giá chuyến không thuộc mình | High |
| **THR-TC-018** | Đánh giá tài xế | **Negative – Đánh giá cho Trip không tồn tại** | Customer đã đăng nhập | 1. Gửi request đánh giá với Trip ID không tồn tại | Trip ID = not found | Hệ thống không ghi nhận đánh giá và phản hồi trạng thái không tìm thấy | Medium |
| **THR-TC-019** | Đánh giá tài xế | **Invalid Format/Value – Trip ID sai định dạng khi gửi đánh giá** | Customer đã đăng nhập | 1. Gửi request đánh giá<br>2. Truyền Trip ID sai định dạng | Trip ID = invalid format | Hệ thống từ chối request đánh giá không hợp lệ | Medium |
| **THR-TC-020** | Đánh giá tài xế | **Positive – Đánh giá được liên kết đúng Customer, Driver và Trip** | Customer đã hoàn thành Trip với Driver và gửi đánh giá hợp lệ | 1. Gửi đánh giá hợp lệ<br>2. Kiểm tra thông tin Rating được ghi nhận | Customer = valid<br>Driver = valid<br>Trip = Completed | Hệ thống lưu đánh giá gắn với đúng Customer, Driver và Trip tương ứng | High |

# TEST CASE –Operation & Report

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
|---|---|---|---|---|---|---|---|
| **OR-TC-001** | Quản lý phương tiện | **Positive – Nhân viên vận hành xem thông tin phương tiện** | Operation Staff đã đăng nhập và có quyền quản lý phương tiện | 1. Mở chức năng Quản lý phương tiện<br>2. Chọn một phương tiện tồn tại<br>3. Xem thông tin | Vehicle = exists | Hệ thống hiển thị thông tin phương tiện tương ứng | High |
| **OR-TC-002** | Quản lý phương tiện | **Positive – Cập nhật thông tin phương tiện hợp lệ** | Operation Staff đã đăng nhập; phương tiện tồn tại | 1. Chọn phương tiện<br>2. Thay đổi thông tin hợp lệ<br>3. Lưu | Vehicle = exists<br>Update data = valid | Hệ thống ghi nhận thông tin phương tiện đã cập nhật | High |
| **OR-TC-003** | Quản lý phương tiện | **Empty/Null – Không cung cấp phương tiện cần cập nhật** | Operation Staff đã đăng nhập và có quyền | 1. Mở chức năng Quản lý phương tiện<br>2. Không xác định phương tiện<br>3. Thực hiện cập nhật | Vehicle ID = null | Hệ thống không thực hiện cập nhật khi không xác định được phương tiện | Medium |
| **OR-TC-004** | Quản lý phương tiện | **Invalid Format/Value – Vehicle ID sai định dạng** | Operation Staff đã đăng nhập; API có rule định dạng ID | 1. Gửi request với Vehicle ID sai định dạng | Vehicle ID = invalid format | Hệ thống từ chối Vehicle ID không hợp lệ | Medium |
| **OR-TC-005** | Quản lý khách hàng | **Positive – Nhân viên vận hành xem và quản lý thông tin Customer** | Operation Staff đã đăng nhập và có quyền | 1. Mở Quản lý khách hàng<br>2. Chọn Customer tồn tại<br>3. Thực hiện thao tác quản lý được cấp quyền | Customer = exists | Hệ thống cho phép Operation Staff quản lý thông tin Customer | High |
| **OR-TC-006** | Quản lý khách hàng | **Negative – Người không có quyền thực hiện thao tác quản lý Customer** | Người dùng đã đăng nhập nhưng không có quyền quản trị tương ứng | 1. Truy cập Quản lý khách hàng<br>2. Thử thực hiện thao tác quản trị | Permission = denied | Hệ thống từ chối thao tác quản trị Customer | High |
| **OR-TC-007** | Quản lý khách hàng | **Empty/Null – Không cung cấp Customer cần quản lý** | Operation Staff đã đăng nhập | 1. Gửi request thao tác Customer<br>2. Không truyền Customer ID | Customer ID = null | Hệ thống không thực hiện thao tác do thiếu thông tin xác định Customer | Medium |
| **OR-TC-008** | Quản lý tài xế | **Positive – Nhân viên vận hành xem và quản lý thông tin Driver** | Operation Staff đã đăng nhập và có quyền | 1. Mở Quản lý tài xế<br>2. Chọn Driver tồn tại<br>3. Thực hiện thao tác quản lý | Driver = exists | Hệ thống cho phép Operation Staff quản lý thông tin Driver | High |
| **OR-TC-009** | Quản lý tài xế | **Negative – Người không có quyền thực hiện thao tác quản lý Driver** | Người dùng đã đăng nhập nhưng không có quyền tương ứng | 1. Truy cập Quản lý tài xế<br>2. Thử thực hiện thao tác quản trị | Permission = denied | Hệ thống từ chối thao tác quản trị Driver | High |
| **OR-TC-010** | Quản lý tài xế | **Invalid Format/Value – Driver ID sai định dạng** | Operation Staff đã đăng nhập; API có rule định dạng ID | 1. Gửi request với Driver ID sai định dạng | Driver ID = invalid format | Hệ thống từ chối Driver ID không hợp lệ | Medium |
| **OR-TC-011** | Quản lý chuyến đi | **Positive – Nhân viên vận hành theo dõi chuyến đang diễn ra** | Operation Staff đã đăng nhập; có Trip đang diễn ra | 1. Mở Quản lý chuyến đi<br>2. Chọn Trip đang hoạt động<br>3. Xem thông tin | Trip = active | Hệ thống hiển thị thông tin chuyến đang diễn ra để Operation Staff theo dõi | High |
| **OR-TC-012** | Quản lý chuyến đi | **Negative – Trip không tồn tại** | Operation Staff đã đăng nhập | 1. Gửi yêu cầu xem/quản lý Trip không tồn tại | Trip ID = not found | Hệ thống không trả dữ liệu Trip và phản hồi trạng thái không tìm thấy phù hợp | Medium |
| **OR-TC-013** | Tra cứu giao dịch | **Positive – Tra cứu giao dịch thanh toán tồn tại** | Operation Staff đã đăng nhập và có quyền; giao dịch tồn tại | 1. Mở Tra cứu giao dịch<br>2. Thực hiện tra cứu giao dịch | Payment transaction = exists | Hệ thống hiển thị thông tin giao dịch thanh toán tương ứng | High |
| **OR-TC-014** | Tra cứu giao dịch | **Negative – Giao dịch thanh toán không tồn tại** | Operation Staff đã đăng nhập và có quyền | 1. Thực hiện tra cứu giao dịch không tồn tại | Payment transaction = not found | Hệ thống không trả dữ liệu giao dịch không tồn tại | Medium |
| **OR-TC-015** | Tra cứu giao dịch | **Invalid Format/Value – Transaction ID sai định dạng** | Operation Staff đã đăng nhập; API có rule định dạng ID | 1. Gửi yêu cầu tra cứu với Transaction ID sai định dạng | Transaction ID = invalid format | Hệ thống từ chối Transaction ID không hợp lệ | Medium |
| **OR-TC-016** | Xử lý chuyến lỗi | **Positive – Nhân viên vận hành tiếp nhận và hỗ trợ xử lý Trip phát sinh lỗi** | Có Trip phát sinh lỗi; Operation Staff đã đăng nhập và có quyền | 1. Mở danh sách Trip lỗi<br>2. Chọn Trip phát sinh lỗi<br>3. Thực hiện thao tác hỗ trợ xử lý | Trip status = error | Hệ thống cho phép Operation Staff xem và hỗ trợ xử lý Trip lỗi | High |
| **OR-TC-017** | Xử lý chuyến lỗi | **Negative – Thực hiện luồng xử lý lỗi cho Trip không phát sinh lỗi** | Operation Staff đã đăng nhập; Trip đang ở trạng thái bình thường | 1. Chọn Trip bình thường<br>2. Thử thực hiện chức năng Xử lý chuyến lỗi | Trip status = normal | Hệ thống không ghi nhận Trip bình thường là Trip lỗi cần xử lý | Medium |
| **OR-TC-018** | Phân quyền và lưu vết | **Boundary – Người có quyền được thực hiện thao tác quản trị, người không có quyền bị từ chối** | Có một Operation Staff có quyền và một tài khoản không có quyền | 1. Thực hiện thao tác bằng tài khoản có quyền<br>2. Thực hiện cùng thao tác bằng tài khoản không có quyền | Permission = allowed / denied | Tài khoản có quyền thực hiện được thao tác; tài khoản không có quyền bị từ chối | High |
| **OR-TC-019** | Lưu vết thao tác | **Positive – Thao tác quản trị quan trọng được lưu vết** | Operation Staff có quyền và thực hiện thao tác quan trọng | 1. Thực hiện thao tác quản trị<br>2. Kiểm tra dữ liệu lưu vết | Operation = important action | Hệ thống lưu vết thao tác để phục vụ kiểm tra khi xảy ra sự cố | High |
| **OR-TC-020** | Xem báo cáo hoạt động | **Positive – Management xem đầy đủ các chỉ số báo cáo theo SRS** | Management đã đăng nhập và có quyền xem báo cáo | 1. Mở chức năng Báo cáo hoạt động<br>2. Xem các chỉ số báo cáo | Metrics = số lượng chuyến, doanh thu, tỷ lệ hoàn thành, tỷ lệ hủy, hiệu quả Driver | Hệ thống hiển thị các báo cáo về số lượng chuyến, doanh thu, tỷ lệ hoàn thành, tỷ lệ hủy và hiệu quả hoạt động của Driver | High |

# PHẦN 2: TRACEABILITY

| **Test Case ID** | **Test Scenario** | **Test Type** | **FR/NFR** | **Use Case** | **Acceptance Criteria** | **Basis in SRS** |
|---|---|---|---|---|---|---|
| AUTH-TC-001 | Đăng ký tài khoản | Positive | FR01 | UC01 | AC01 | Customer có thể đăng ký tài khoản |
| AUTH-TC-002 | Đăng ký tài khoản | Empty/Null | FR01 | UC01 | AC01 | Request đăng ký phải đáp ứng dữ liệu bắt buộc theo validation của API |
| AUTH-TC-003 | Đăng ký tài khoản | Empty/Null | FR01 | UC01 | AC01 | Request rỗng không đáp ứng điều kiện đăng ký tài khoản |
| AUTH-TC-004 | Đăng ký tài khoản | Invalid Format/Value | FR01 | UC01 | AC01 | SRS không quy định format cụ thể; kiểm thử theo validation của API |
| AUTH-TC-005 | Đăng ký tài khoản | Positive | FR01 | UC01 | AC01 | Driver có thể đăng ký tài khoản |
| AUTH-TC-006 | Đăng ký tài khoản Driver | Positive | FR01 | UC01 | AC01 | Operation Staff có thể tạo tài khoản Driver theo quy trình quản lý tài xế |
| AUTH-TC-007 | Đăng nhập | Positive | FR02, NFR06 | UC02 | AC02 | Customer có thông tin xác thực hợp lệ được phép đăng nhập |
| AUTH-TC-008 | Đăng nhập | Positive | FR02, NFR06 | UC02 | AC02 | Driver có thông tin xác thực hợp lệ được phép đăng nhập |
| AUTH-TC-009 | Đăng nhập | Negative | FR02, NFR06 | UC02 | AC02 | Thông tin định danh không tồn tại không được xác thực |
| AUTH-TC-010 | Đăng nhập | Negative | FR02, NFR06 | UC02 | AC02 | Password không chính xác không được xác thực |
| AUTH-TC-011 | Đăng nhập | Empty/Null | FR02, NFR06 | UC02 | AC02 | Thiếu thông tin định danh không đáp ứng điều kiện đăng nhập |
| AUTH-TC-012 | Đăng nhập | Empty/Null | FR02, NFR06 | UC02 | AC02 | Thiếu password không đáp ứng điều kiện đăng nhập |
| AUTH-TC-013 | Đăng nhập | Empty/Null | FR02, NFR06 | UC02 | AC02 | Không có thông tin xác thực thì không được đăng nhập |
| AUTH-TC-014 | Đăng nhập | Invalid Format/Value | FR02, NFR06 | UC02 | AC02 | SRS không quy định format cụ thể; áp dụng validation Authentication API |
| AUTH-TC-015 | Đăng nhập | Boundary | FR02, NFR06 | UC02 | AC02 | Password tại giới hạn cấu hình được xử lý theo rule Authentication API |
| AUTH-TC-016 | Đăng nhập | Boundary | FR02, NFR06 | UC02 | AC02 | Password dưới giới hạn cấu hình phải bị từ chối |
| AUTH-TC-017 | Xác thực truy cập | Negative/Security | NFR06 | UC02 | AC02 | Người dùng chưa xác thực không được truy cập chức năng yêu cầu tài khoản |
| AUTH-TC-018 | Xác thực truy cập | Negative/Security | NFR06 | UC02 | AC02 | Credential hoặc token không hợp lệ không được truy cập tài nguyên bảo vệ |
| AUTH-TC-019 | Xác thực truy cập | Positive | FR02, NFR06 | UC02 | AC02 | Người dùng đã xác thực được sử dụng chức năng thuộc quyền |
| AUTH-TC-020 | Bảo vệ dữ liệu xác thực | Security | NFR05 | UC02 | — | Dữ liệu xác thực nhạy cảm phải được bảo vệ và không trả trực tiếp password |
| PROF-TC-001 | Cập nhật thông tin | Positive | FR03 | UC03 | AC03 | Customer có thể cập nhật thông tin cá nhân của mình |
| PROF-TC-002 | Cập nhật thông tin | Positive | FR03 | UC03 | AC03 | Driver có thể cập nhật thông tin hồ sơ của mình |
| PROF-TC-003 | Cập nhật thông tin phương tiện | Positive | FR03, FR27 | UC03, UC17 | AC03, AC28 | Driver có thể cập nhật thông tin phương tiện thuộc tài khoản của mình |
| PROF-TC-004 | Cập nhật trạng thái hoạt động | Positive | FR03 | UC03 | AC03 | Driver có thể cập nhật trạng thái hoạt động của mình |
| PROF-TC-005 | Cập nhật thông tin | Empty/Null | FR03 | UC03 | AC03 | Request cập nhật phải có dữ liệu phù hợp theo validation của API |
| PROF-TC-006 | Cập nhật thông tin | Invalid Format/Value | FR03 | UC03 | AC03 | Dữ liệu cập nhật phải đáp ứng validation của API |
| PROF-TC-007 | Cập nhật thông tin | Negative/Security | FR03, NFR06 | UC03 | AC03 | Người dùng phải được xác thực trước khi cập nhật thông tin |
| PROF-TC-008 | Cập nhật thông tin | Negative/Authorization | FR03, NFR05 | UC03 | AC03 | Người dùng chỉ được cập nhật hồ sơ thuộc tài khoản của mình |
| BOOK-TC-001 | Tạo yêu cầu đặt xe | Positive | FR04–FR07 | UC04 | AC04 | Customer nhập điểm đón, điểm đến, chọn loại xe và gửi yêu cầu đặt xe |
| BOOK-TC-002 | Tạo yêu cầu đặt xe | Positive | FR07, FR08 | UC04, UC05 | AC05 | Booking được ghi nhận và hệ thống bắt đầu quá trình tìm Driver |
| BOOK-TC-003 | Tạo yêu cầu đặt xe | Empty/Null | FR04, FR07 | UC04 | AC04 | Điểm đón là thông tin cần thiết của yêu cầu đặt xe |
| BOOK-TC-004 | Tạo yêu cầu đặt xe | Empty/Null | FR05, FR07 | UC04 | AC04 | Điểm đến là thông tin cần thiết của yêu cầu đặt xe |
| BOOK-TC-005 | Tạo yêu cầu đặt xe | Empty/Null | FR06, FR07 | UC04 | AC04 | Customer phải lựa chọn loại xe khi tạo booking |
| BOOK-TC-006 | Tạo yêu cầu đặt xe | Empty/Null | FR04, FR05, FR07 | UC04 | AC04 | Booking phải có điểm đón và điểm đến |
| BOOK-TC-007 | Tạo yêu cầu đặt xe | Empty/Null | FR04–FR07 | UC04 | AC04 | Request rỗng không có đủ dữ liệu tạo booking |
| BOOK-TC-008 | Tạo yêu cầu đặt xe | Invalid Format/Value | FR06, FR07 | UC04 | AC04 | Loại xe phải thuộc loại được hệ thống hỗ trợ |
| BOOK-TC-009 | Tạo yêu cầu đặt xe | Invalid Format/Value | FR04, FR07 | UC04 | AC04 | SRS không quy định format điểm đón; áp dụng validation Booking API |
| BOOK-TC-010 | Tạo yêu cầu đặt xe | Invalid Format/Value | FR05, FR07 | UC04 | AC04 | SRS không quy định format điểm đến; áp dụng validation Booking API |
| BOOK-TC-011 | Tạo yêu cầu đặt xe | Negative/Security | FR02, FR07, NFR06 | UC02, UC04 | AC02, AC04 | Customer phải được xác thực trước khi sử dụng chức năng đặt xe |
| BOOK-TC-012 | Tạo yêu cầu đặt xe | Negative/Security | NFR06 | UC02, UC04 | AC02 | Token không hợp lệ không đáp ứng yêu cầu xác thực |
| BOOK-TC-013 | Tạo yêu cầu đặt xe | Negative/Authorization | FR07 | UC04 | AC04 | Actor thực hiện chức năng Đặt xe là Customer |
| BOOK-TC-014 | Tạo yêu cầu đặt xe | Boundary | FR04–FR07 | UC04 | AC04 | Có đủ điểm đón, điểm đến và loại xe thì đáp ứng dữ liệu nghiệp vụ tối thiểu |
| BOOK-TC-015 | Tạo yêu cầu đặt xe | Boundary | FR04–FR07 | UC04 | AC04 | Thiếu một thông tin nghiệp vụ bắt buộc thì booking chưa đầy đủ |
| BOOK-TC-016 | Tra cứu booking | Positive | FR07 | UC04 | — | Kiểm thử API trên Booking đã được hệ thống ghi nhận; SRS không có AC riêng cho tra cứu Booking |
| BOOK-TC-017 | Tra cứu booking | Negative | FR07 | UC04 | — | Booking không tồn tại thì không có dữ liệu tương ứng |
| BOOK-TC-018 | Tra cứu booking | Invalid Format/Value | FR07 | UC04 | — | SRS không quy định format Booking ID; áp dụng validation API |
| BOOK-TC-019 | Tra cứu booking | Negative/Security | NFR05 | UC04 | — | Dữ liệu Booking của Customer phải được bảo vệ khỏi truy cập trái phép |
| BOOK-TC-020 | Response tạo booking | Positive | FR07 | UC04 | AC05 | Hệ thống ghi nhận yêu cầu đặt xe sau khi Customer gửi |
| DLM-TC-001 | Cập nhật vị trí tài xế | Positive | FR17 | UC05, UC07 | AC14 | Vị trí Driver được lưu để hỗ trợ matching và dự kiến thời gian đến |
| DLM-TC-002 | Cập nhật vị trí tài xế | Positive | FR17 | UC05, UC07 | AC14 | Vị trí Driver được cập nhật để phục vụ matching và theo dõi |
| DLM-TC-003 | Cập nhật vị trí tài xế | Empty/Null | FR17 | UC05, UC07 | AC14 | Dữ liệu vị trí phải hợp lệ để hỗ trợ matching và ETA |
| DLM-TC-004 | Cập nhật vị trí tài xế | Invalid Format/Value | FR17 | UC05, UC07 | AC14 | SRS không quy định cấu trúc vị trí; áp dụng validation Driver Location API |
| DLM-TC-005 | Cập nhật vị trí tài xế | Negative/Security | FR17, NFR06 | UC05, UC07 | AC14 | Driver phải được xác thực khi cập nhật dữ liệu vị trí |
| DLM-TC-006 | Cập nhật vị trí tài xế | Negative/Security | FR17, NFR06 | UC05, UC07 | AC14 | Token không hợp lệ không được cập nhật vị trí Driver |
| DLM-TC-007 | Cập nhật vị trí tài xế | Boundary/State | FR17 | UC05, UC07 | AC06, AC14 | Sau khi có vị trí hợp lệ, Driver có thể được xét trong matching |
| DLM-TC-008 | Tìm tài xế phù hợp | Positive | FR08 | UC05 | AC06 | Matching dựa trên vị trí, trạng thái sẵn sàng và tiêu chí vận hành |
| DLM-TC-009 | Tìm tài xế phù hợp | Positive | FR09 | UC05 | AC07 | Hệ thống ưu tiên Driver phù hợp và gần Customer |
| DLM-TC-010 | Tìm tài xế phù hợp | Negative/State | FR08 | UC05 | AC06 | Driver phải ở trạng thái sẵn sàng khi được xét matching |
| DLM-TC-011 | Tìm tài xế phù hợp | Negative | FR08, FR17 | UC05 | AC06, AC14 | Vị trí Driver được sử dụng trong quá trình xác định Driver phù hợp |
| DLM-TC-012 | Tìm tài xế phù hợp | Invalid Format/Value | FR08, FR17 | UC05 | AC06, AC14 | Dữ liệu vị trí không hợp lệ không được dùng để ưu tiên Driver |
| DLM-TC-013 | Tìm tài xế phù hợp | Empty/Null | FR08, FR14 | UC05 | AC06, AC11 | Không có ứng viên phù hợp dẫn đến trường hợp không tìm được Driver |
| DLM-TC-014 | Tìm tài xế phù hợp | Negative | FR08 | UC05 | AC06 | Chỉ Driver đáp ứng tiêu chí mới được xác định là phù hợp |
| DLM-TC-015 | Tìm tài xế phù hợp | Positive | FR10 | UC05 | AC06 | Hệ thống gửi yêu cầu chuyến đến Driver phù hợp |
| DLM-TC-016 | Matching lại tài xế | Negative/Exception | FR12, FR13 | UC06, UC05 | AC09 | Driver từ chối thì hệ thống tiếp tục tìm Driver khác |
| DLM-TC-017 | Matching lại tài xế | Boundary/Exception | FR13 | UC05 | AC10 | Driver không phản hồi đến timeout cấu hình thì hệ thống tiếp tục matching |
| DLM-TC-018 | Matching lại tài xế | Positive | FR13 | UC05 | AC09, AC10 | Hệ thống tiếp tục matching mà Customer không cần tạo lại booking |
| DLM-TC-019 | Không tìm được tài xế | Negative/Exception | FR14 | UC05 | AC11 | Không còn Driver phù hợp thì hệ thống xác định không tìm được Driver |
| DLM-TC-020 | Không tìm được tài xế | Positive/Notification | FR14, FR24 | UC05, UC12 | AC11, AC22 | Khi không tìm được Driver, hệ thống thông báo rõ ràng cho Customer |
| TRIP-TC-001 | Phản hồi yêu cầu chuyến | Positive | FR11 | UC06 | AC08 | Driver chấp nhận yêu cầu và được phân công cho chuyến |
| TRIP-TC-002 | Phản hồi yêu cầu chuyến | Positive/Exception | FR12, FR13 | UC06, UC05 | AC09 | Driver từ chối và hệ thống tiếp tục tìm Driver khác |
| TRIP-TC-003 | Phản hồi yêu cầu chuyến | Negative/Security | FR11, NFR06 | UC06 | AC08 | Driver chưa xác thực không được chấp nhận yêu cầu chuyến |
| TRIP-TC-004 | Phản hồi yêu cầu chuyến | Negative/Security | FR12, NFR06 | UC06 | AC09 | Driver chưa xác thực không được từ chối yêu cầu chuyến |
| TRIP-TC-005 | Phản hồi yêu cầu chuyến | Negative/Authorization | FR11, FR12 | UC06 | AC08, AC09 | Chỉ Driver nhận yêu cầu chuyến tương ứng mới được phản hồi |
| TRIP-TC-006 | Phản hồi yêu cầu chuyến | Invalid Format/Value | FR11, FR12 | UC06 | AC08, AC09 | SRS không quy định format Request ID; áp dụng validation API |
| TRIP-TC-007 | Phản hồi yêu cầu chuyến | Negative | FR11, FR12 | UC06 | AC08, AC09 | Request phải tồn tại để Driver Accept hoặc Reject |
| TRIP-TC-008 | Phản hồi yêu cầu chuyến | Empty/Null | FR11, FR12 | UC06 | AC08, AC09 | Thiếu Request ID thì không xác định được yêu cầu chuyến |
| TRIP-TC-009 | Phản hồi yêu cầu chuyến | Boundary/Exception | FR13 | UC05 | AC10 | Driver không phản hồi thì hệ thống tiếp tục tìm Driver khác |
| TRIP-TC-010 | Phản hồi yêu cầu chuyến | Negative/State | FR11 | UC06 | AC08 | Driver phải ở trạng thái phù hợp để nhận chuyến |
| TRIP-TC-011 | Cập nhật trạng thái chuyến | Positive | FR15 | UC08 | AC13 | Driver cập nhật trạng thái Đã đến điểm đón |
| TRIP-TC-012 | Cập nhật trạng thái chuyến | Positive | FR15 | UC08 | AC13 | Driver cập nhật trạng thái Đã đón khách |
| TRIP-TC-013 | Cập nhật trạng thái chuyến | Positive | FR15 | UC08 | AC13 | Driver cập nhật trạng thái Đang di chuyển |
| TRIP-TC-014 | Cập nhật trạng thái chuyến | Positive | FR15, FR18 | UC08, UC09 | AC15, AC16 | Khi Trip hoàn thành, hệ thống ghi nhận Completed và chuyển sang bước xác định số tiền phải trả |
| TRIP-TC-015 | Cập nhật trạng thái chuyến | Empty/Null | FR15 | UC08 | AC13 | Thiếu trạng thái thì hệ thống không thể cập nhật Trip |
| TRIP-TC-016 | Cập nhật trạng thái chuyến | Invalid Format/Value | FR15 | UC08 | AC13 | Trạng thái phải thuộc các trạng thái nghiệp vụ được hỗ trợ |
| TRIP-TC-017 | Cập nhật trạng thái chuyến | Negative/Authorization | FR15 | UC08 | AC13 | Driver chỉ được cập nhật Trip mà mình đang thực hiện |
| TRIP-TC-018 | Cập nhật trạng thái chuyến | Negative | FR15 | UC08 | AC13 | Trip phải tồn tại để cập nhật trạng thái |
| TRIP-TC-019 | Theo dõi chuyến | Positive | FR16 | UC07 | AC12 | Customer xem được trạng thái hiện tại và thông tin Driver đã nhận chuyến |
| TRIP-TC-020 | Hoàn thành chuyến | Boundary/State | FR15, FR18 | UC08, UC09 | AC15, AC16 | Sau khi Trip chuyển sang Completed, hệ thống mới chuyển sang bước xác định số tiền phải trả |
| FP-TC-001 | Xác định số tiền phải trả | Positive | FR18 | UC09 | AC16 | Sau khi Trip hoàn thành, hệ thống xác định số tiền Customer phải trả dựa trên loại dịch vụ và thông tin chuyến đi |
| FP-TC-002 | Xác định số tiền phải trả | Boundary/State | FR18 | UC09 | AC16 | Hệ thống không xác định số tiền phải trả trước khi Trip hoàn thành |
| FP-TC-003 | Xác định số tiền phải trả | Boundary/State | FR18 | UC09 | AC15, AC16 | Completed là trạng thái chuyển sang bước xác định số tiền phải trả |
| FP-TC-004 | Xác định số tiền phải trả | Negative | FR18 | UC09 | AC16 | Trip phải tồn tại để xác định số tiền phải trả |
| FP-TC-005 | Xác định số tiền phải trả | Empty/Null | FR18 | UC09 | AC16 | Thiếu Trip ID thì không xác định được chuyến cần xử lý |
| FP-TC-006 | Xác định số tiền phải trả | Invalid Format/Value | FR18 | UC09 | AC16 | SRS không quy định format Trip ID; áp dụng validation Fare API |
| FP-TC-007 | Thanh toán | Positive | FR19 | UC10 | AC17 | Customer lựa chọn tiền mặt và hệ thống ghi nhận phương thức thanh toán |
| FP-TC-008 | Thanh toán | Positive/Integration | FR20, FR21 | UC10, UC11 | AC18 | Thanh toán điện tử được chuyển đến Payment Provider |
| FP-TC-009 | Thanh toán | Empty/Null | FR19, FR20 | UC10 | AC17, AC18 | Customer phải chọn phương thức thanh toán |
| FP-TC-010 | Thanh toán | Invalid Format/Value | FR19, FR20 | UC10 | AC17, AC18 | Hệ thống chỉ chấp nhận phương thức thanh toán được hỗ trợ |
| FP-TC-011 | Thanh toán | Negative/State | FR18–FR20 | UC09, UC10 | AC16–AC18 | Thanh toán chỉ thực hiện sau khi Trip hoàn thành và số tiền phải trả đã được xác định |
| FP-TC-012 | Thanh toán điện tử | Positive/Integration | FR21 | UC11 | AC19 | Payment Provider trả Success thì CAB ghi nhận thanh toán thành công |
| FP-TC-013 | Thanh toán điện tử | Negative/Exception | FR23 | UC11 | AC20 | Thanh toán thất bại phải được ghi nhận và thông báo cho Customer |
| FP-TC-014 | Xử lý thanh toán thất bại | Positive/Exception | FR23 | UC11 | AC20 | Hệ thống cho phép xử lý lại thanh toán điện tử theo chính sách doanh nghiệp |
| FP-TC-015 | Xử lý thanh toán thất bại | Positive/Exception | FR19, FR23 | UC10, UC11 | AC17, AC20 | Sau thanh toán điện tử thất bại, Customer có thể chuyển sang tiền mặt theo workflow |
| FP-TC-016 | Thanh toán điện tử | Negative/Reliability | FR21, NFR02 | UC11 | AC20 | Lỗi Payment Provider không được làm toàn bộ hệ thống đặt xe ngừng hoạt động |
| FP-TC-017 | Thanh toán điện tử | Empty/Null/Integration | FR21 | UC11 | AC19, AC20 | Chưa có kết quả hợp lệ từ Provider thì không được ghi nhận Payment thành công |
| FP-TC-018 | Thanh toán điện tử | Invalid Format/Value | FR21 | UC11 | AC19, AC20 | Provider response không hợp lệ không được xem là thanh toán thành công |
| FP-TC-019 | Bảo vệ dữ liệu thanh toán | Security | FR22, NFR05 | UC11 | AC21 | CAB không lưu trực tiếp thông tin nhạy cảm của thẻ hoặc tài khoản thanh toán |
| FP-TC-020 | Kết thúc thanh toán | Positive | FR19–FR21 | UC10, UC11 | AC17–AC19 | Khi thanh toán thành công, hệ thống ghi nhận kết quả, hoàn tất thanh toán và kết thúc quy trình chuyến xe |
| NOTI-TC-001 | Thông báo booking | Positive | FR24 | UC12 | AC22 | Customer nhận thông báo khi yêu cầu đặt xe được tiếp nhận |
| NOTI-TC-002 | Thông báo Driver nhận chuyến | Positive | FR24 | UC12 | AC22 | Customer nhận thông báo khi Driver chấp nhận chuyến |
| NOTI-TC-003 | Thông báo Driver đến điểm đón | Positive | FR24 | UC12 | AC22 | Customer nhận thông báo khi Driver đến điểm đón |
| NOTI-TC-004 | Thông báo hoàn thành chuyến | Positive | FR24 | UC12 | AC22 | Customer nhận thông báo khi Trip hoàn thành |
| NOTI-TC-005 | Thông báo thanh toán | Positive | FR24 | UC12 | AC22 | Customer nhận thông báo kết quả thanh toán |
| NOTI-TC-006 | Thông báo thanh toán | Positive/Exception | FR24 | UC12 | AC22 | Customer được thông báo khi thanh toán thất bại |
| NOTI-TC-007 | Thông báo chuyến mới | Positive | FR24 | UC12 | AC23 | Driver nhận thông báo về chuyến mới |
| NOTI-TC-008 | Thông báo cho Driver | Positive | FR24 | UC12 | AC23 | Driver nhận thông báo thay đổi liên quan đến chuyến đang thực hiện |
| NOTI-TC-009 | Gửi thông báo | Empty/Null | FR24 | UC12 | AC22, AC23 | Notification phải xác định đúng người nhận |
| NOTI-TC-010 | Gửi thông báo | Empty/Null | FR24 | UC12 | AC22, AC23 | Notification phải có sự kiện cần thông báo |
| NOTI-TC-011 | Gửi thông báo | Empty/Null | FR24 | UC12 | AC22, AC23 | Request rỗng không đủ dữ liệu để gửi Notification |
| NOTI-TC-012 | Gửi thông báo | Invalid Format/Value | FR24 | UC12 | AC22, AC23 | Notification chỉ áp dụng cho các sự kiện nghiệp vụ được hỗ trợ |
| NOTI-TC-013 | Gửi thông báo | Invalid Format/Value | FR24 | UC12 | AC22, AC23 | SRS không quy định format Recipient ID; áp dụng validation API |
| NOTI-TC-014 | Gửi thông báo | Negative | FR24 | UC12 | AC22, AC23 | Recipient phải tồn tại để nhận Notification |
| NOTI-TC-015 | Gửi thông báo | Negative | FR24 | UC12 | AC22, AC23 | Notification phải được gửi đúng Customer hoặc Driver liên quan |
| NOTI-TC-016 | Notification Provider | Negative/Reliability | FR24, NFR02 | UC12 | AC22, AC23 | Lỗi Notification Provider không làm toàn bộ hệ thống ngừng hoạt động |
| NOTI-TC-017 | Notification Provider | Empty/Null/Integration | FR24 | UC12 | AC22, AC23 | Chưa nhận kết quả Provider thì không được ghi nhận gửi thành công |
| NOTI-TC-018 | Notification Provider | Invalid Format/Value | FR24 | UC12 | AC22, AC23 | Provider response không hợp lệ không được ghi nhận Success |
| NOTI-TC-019 | Thay đổi Notification Provider | Boundary/Extensibility | NFR11 | UC12 | — | Hệ thống cho phép thay đổi hoặc bổ sung Notification Provider mà không xây dựng lại toàn bộ ứng dụng |
| NOTI-TC-020 | Độ tin cậy Notification | Negative/Reliability | NFR02 | UC12 | — | Lỗi Notification không làm gián đoạn toàn bộ dịch vụ đặt xe |
| THR-TC-001 | Xem lịch sử chuyến | Positive | FR25 | UC13 | AC24 | Customer xem được lịch sử các chuyến đã thực hiện |
| THR-TC-002 | Xem lịch sử chuyến | Positive | FR25 | UC13 | AC24 | Lịch sử hiển thị thông tin liên quan đến chuyến |
| THR-TC-003 | Xem lịch sử chuyến | Positive | FR25 | UC13 | AC24 | Lịch sử chuyến hiển thị số tiền phải trả |
| THR-TC-004 | Xem lịch sử chuyến | Empty/Null | FR25 | UC13 | AC24 | SRS cho phép xem lịch sử nhưng không quy định cách hiển thị khi chưa có dữ liệu |
| THR-TC-005 | Xem lịch sử chuyến | Negative/Security | FR25, NFR06 | UC13 | AC24 | Customer phải được xác thực trước khi xem lịch sử chuyến |
| THR-TC-006 | Xem lịch sử chuyến | Negative/Security | NFR06 | UC13 | AC24 | Token không hợp lệ không được truy cập lịch sử |
| THR-TC-007 | Xem lịch sử chuyến | Negative/Authorization | FR25, NFR05 | UC13 | AC24 | Lịch sử chuyến của Customer phải được bảo vệ khỏi truy cập trái phép |
| THR-TC-008 | Xem chi tiết lịch sử chuyến | Negative | FR25 | UC13 | AC24 | Trip không tồn tại thì không có dữ liệu lịch sử tương ứng |
| THR-TC-009 | Xem chi tiết lịch sử chuyến | Invalid Format/Value | FR25 | UC13 | AC24 | SRS không quy định format Trip ID; áp dụng validation API |
| THR-TC-010 | Xem chi tiết lịch sử chuyến | Empty/Null | FR25 | UC13 | AC24 | Thiếu Trip ID thì không xác định được chuyến cần xem |
| THR-TC-011 | Đánh giá tài xế | Positive | FR26 | UC14 | AC25 | Customer có thể đánh giá Driver sau khi Trip hoàn thành |
| THR-TC-012 | Đánh giá tài xế | Boundary/State | FR26 | UC14 | AC25 | Customer không được đánh giá trước khi Trip hoàn thành |
| THR-TC-013 | Đánh giá tài xế | Boundary/State | FR26 | UC14 | AC25 | Sau khi Trip hoàn thành, Customer được phép đánh giá Driver |
| THR-TC-014 | Đánh giá tài xế | Empty/Null | FR26 | UC14 | AC25 | SRS chưa quy định chi tiết trường Rating; áp dụng validation Rating API |
| THR-TC-015 | Đánh giá tài xế | Invalid Format/Value | FR26 | UC14 | AC25 | SRS chưa quy định thang điểm Rating; áp dụng rule Rating API |
| THR-TC-016 | Đánh giá tài xế | Negative/Security | FR26, NFR06 | UC14 | AC25 | Customer phải được xác thực trước khi gửi Rating |
| THR-TC-017 | Đánh giá tài xế | Negative/Authorization | FR26, NFR05 | UC14 | AC25 | Customer chỉ được đánh giá Driver của chuyến liên quan đến mình |
| THR-TC-018 | Đánh giá tài xế | Negative | FR26 | UC14 | AC25 | Trip phải tồn tại và hoàn thành trước khi đánh giá |
| THR-TC-019 | Đánh giá tài xế | Invalid Format/Value | FR26 | UC14 | AC25 | SRS không quy định format Trip ID; áp dụng validation API |
| THR-TC-020 | Đánh giá tài xế | Positive | FR26 | UC14 | AC25 | Rating được ghi nhận cho đúng Customer và Driver sau khi chuyến hoàn thành |
| OR-TC-001 | Quản lý phương tiện | Positive | FR27 | UC17 | AC28 | Operation Staff có thể xem và quản lý thông tin phương tiện |
| OR-TC-002 | Quản lý phương tiện | Positive | FR27 | UC17 | AC28 | Operation Staff có thể cập nhật thông tin phương tiện |
| OR-TC-003 | Quản lý phương tiện | Empty/Null | FR27 | UC17 | AC28 | Thiếu Vehicle ID thì không xác định được phương tiện cần thao tác |
| OR-TC-004 | Quản lý phương tiện | Invalid Format/Value | FR27 | UC17 | AC28 | SRS không quy định format Vehicle ID; áp dụng validation API |
| OR-TC-005 | Quản lý khách hàng | Positive | FR28 | UC15 | AC26 | Operation Staff có thể quản lý thông tin Customer |
| OR-TC-006 | Quản lý khách hàng | Negative/Authorization | FR28, NFR07 | UC15 | AC26, AC32 | Thao tác quản trị Customer phải được kiểm soát quyền truy cập |
| OR-TC-007 | Quản lý khách hàng | Empty/Null | FR28 | UC15 | AC26 | Thiếu Customer ID thì không xác định được đối tượng cần quản lý |
| OR-TC-008 | Quản lý tài xế | Positive | FR29 | UC16 | AC27 | Operation Staff có thể quản lý thông tin Driver |
| OR-TC-009 | Quản lý tài xế | Negative/Authorization | FR29, NFR07 | UC16 | AC27, AC32 | Người không có quyền không được thực hiện thao tác quản trị Driver |
| OR-TC-010 | Quản lý tài xế | Invalid Format/Value | FR29 | UC16 | AC27 | SRS không quy định format Driver ID; áp dụng validation API |
| OR-TC-011 | Quản lý chuyến đi | Positive | FR30 | UC18 | AC29 | Operation Staff có thể quản lý và xem các chuyến đang diễn ra |
| OR-TC-012 | Quản lý chuyến đi | Negative | FR30 | UC18 | AC29 | Trip không tồn tại thì không có dữ liệu để quản lý |
| OR-TC-013 | Tra cứu giao dịch | Positive | FR31 | UC19 | AC31 | Operation Staff có thể tra cứu lịch sử giao dịch |
| OR-TC-014 | Tra cứu giao dịch | Negative | FR31 | UC19 | AC31 | Giao dịch không tồn tại thì không có dữ liệu tương ứng |
| OR-TC-015 | Tra cứu giao dịch | Invalid Format/Value | FR31 | UC19 | AC31 | SRS không quy định format Transaction ID; áp dụng validation API |
| OR-TC-016 | Xử lý chuyến lỗi | Positive | FR32 | UC20 | AC30 | Operation Staff có thể xem và hỗ trợ xử lý Trip bị lỗi |
| OR-TC-017 | Xử lý chuyến lỗi | Negative/State | FR32 | UC20 | AC30 | Luồng xử lý chuyến lỗi chỉ áp dụng cho Trip phát sinh lỗi |
| OR-TC-018 | Phân quyền quản trị | Boundary/Authorization | NFR07 | UC15–UC20 | AC32 | Tài khoản có quyền được thao tác; tài khoản không có quyền bị từ chối |
| OR-TC-019 | Lưu vết thao tác | Positive/Audit | NFR08 | UC15–UC20 | — | Các thao tác quan trọng phải được lưu vết để phục vụ kiểm tra |
| OR-TC-020 | Xem báo cáo hoạt động | Positive | FR33 | UC21 | AC33 | Management xem báo cáo số lượng chuyến, doanh thu, tỷ lệ hoàn thành, tỷ lệ hủy và hiệu quả Driver |


# PHẦN 3: Coverage & Gaps

| **Trạng thái** | **Ảnh hưởng đến Test Case** | **Cách xử lý trong bộ test** |
|---|---|---|
| Chưa chốt cách tính cước cụ thể | Không thể xây dựng Boundary Test cho công thức, đơn giá hoặc giá trị tiền cụ thể | Chỉ kiểm thử việc hệ thống tính cước sau khi Trip hoàn thành và tạo Fare thành công |
| Chưa chốt tiêu chí ưu tiên Driver chi tiết | Không thể kiểm thử trọng số, bán kính hoặc tiêu chí ưu tiên cụ thể | Chỉ kiểm thử rule đã có trong SRS: Driver phải phù hợp, sẵn sàng và được ưu tiên khi gần Customer |
| Chưa chốt thời gian Driver phản hồi | Không thể xác định chính xác Boundary về số giây/phút timeout | Sử dụng điều kiện “đến ngưỡng timeout được cấu hình trong hệ thống” thay vì tự đặt thời gian |
| Chưa chốt chính sách hủy chuyến | Không thể xây dựng đầy đủ Positive/Negative Test cho nghiệp vụ hủy chuyến | Không tự thêm luồng hủy chuyến ngoài những nội dung đã được SRS xác định |
| Chưa chốt cách xử lý mất kết nối mạng | Không xác định được Expected Result khi Customer hoặc Driver mất mạng | Không tự đặt retry, offline mode hoặc số lần kết nối lại |
| Chưa chốt thời gian lưu trữ dữ liệu | Không thể tạo Boundary Test theo số ngày/tháng/năm lưu dữ liệu | Không tự đặt thời gian retention trong Test Data |
| Chưa định nghĩa Password Rule cụ thể | Không thể xác định password tối thiểu/tối đa bao nhiêu ký tự hoặc regex cụ thể | Boundary Test sử dụng MIN/MAX theo cấu hình thực tế của Authentication API |
| Chưa định nghĩa format cụ thể cho Username/Identifier | Không thể xác định chính xác dữ liệu nào sai format | Invalid Format Test chỉ áp dụng khi API đã có rule validation cụ thể |
| Chưa định nghĩa format/độ dài các trường đăng ký và hồ sơ | Không thể tự đặt giới hạn cho tên, số điện thoại, email hoặc các trường khác | Chỉ kiểm thử Empty/Null và Invalid Format theo validation thực tế của API |
| Chưa định nghĩa thang điểm Rating | Không thể tự xác định rating phải từ 1–5 hoặc khoảng giá trị khác | Chỉ kiểm thử giá trị hợp lệ/không hợp lệ theo rule thực tế của Rating API |
| Chưa định nghĩa format cụ thể của Booking ID, Trip ID, Driver ID, Vehicle ID, Transaction ID | Không thể tự đặt UUID, số nguyên hoặc độ dài ID | Test Invalid Format sử dụng format thực tế được API Specification quy định |
| Có bất nhất mã FR trong bảng Traceability của SRS | Có thể dẫn đến Test Case tham chiếu sai FR | Bộ test sử dụng danh sách Functional Requirements hiện hành từ FR01 đến FR33 |
| Payment Provider là hệ thống bên ngoài | Một số lỗi thanh toán không thể kiểm thử hoàn toàn từ CAB System | Sử dụng mock/stub hoặc response giả lập Success, Failed, Null và Invalid Response |
| Notification Provider là hệ thống bên ngoài | Không thể phụ thuộc hoàn toàn vào Provider thật khi kiểm thử | Sử dụng mock/stub để kiểm thử Success, Error, Null Response và Provider Failure |
| SRS yêu cầu lỗi Payment/Notification không làm toàn hệ thống dừng | Cần có Test Case về Reliability ngoài Functional Test thông thường | Kiểm thử khi Payment hoặc Notification lỗi, các chức năng Booking, Matching và Trip vẫn tiếp tục hoạt động |
