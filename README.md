Hướng dẫn dự án
 Bookmark this page
Yêu cầu dự án

Để bắt đầu dự án các bạn làm theo các bước sau:

Bước 1: Tạo 1 project: Analysis_Log.

Bước 2: Sau khi tạo project các bạn tải file log.txt tại đây về và copy vào thư mục source code chứa file main.c.

Bước 3: Các bạn hãy viết đoạn code sau vào file main.c.



Giải thích: Trong đoạn code trên, hàm "fileToStr" sẽ copy toàn bộ nội dung của file log trong thư mục code vào con trỏ fileStr. Hàm print phía dưới sẽ hiển thị toàn bộ nội dung ở con trỏ fileStr.

Bước 4: Xóa hàm print đi và bắt đầu code các hàm thao tác với con trỏ fileStr theo yêu cầu của đề bài.

Lưu ý: Trong các yêu cầu dưới đây sẽ có yêu cầu nâng cao (chiếm 30% điểm và không bắt buộc làm), tuy nhiên vẫn sẽ hỏi về nội dung trong buổi thi hết môn.

Mỗi câu hỏi dưới đây học viên viết ra 1 hàm riêng.

Câu 1: Tính số bản tin gửi đi trong thời gian log.

Đoạn log trên lưu lại thời gian gửi và nhận bản tin Zwave, định dạng của bản tin được định nghĩa theo ảnh phía dưới.



Bản tin: là 1 đoạn chữ, bắt đầu từ [INFO] và kết thúc khi xuống dòng.

Trong 1 bản tin có các trường dữ liệu sau:

Thời gian: [2019-10-2323:21:45.638] được hiểu là thời gian gửi hoặc nhận bản tin, 23:21:45.638 được hiểu là 23 giờ, 21 phút, 45.638 giây.

Chiều bản tin: "cmd":"set": dùng để phân biệt bản tin gửi đi và bản tin nhận về "set" là bản tin gửi đi, còn "status" là bản tin nhận về.

Loại thiết bị: "type":"switch": dùng để phân biệt các loại thiết bị: "switch" là công tắc.

Mã thiết bị: ["zwave-dc53:4-1"]: Tên của thiết bị thực hiện truyền nhận dữ liệu, với địa chỉ network là dc53 và endpoint là 1.

Trạng thái thiết bị: "on":true: Biểu thị trạng thái của công tắc, "on":true công tắc bật, "on": false công tắc tắt.

Mã xác định bản tin: "reqid": "0001":để xác định bản tin có truyền đi được thành công hay không, sẽ dựa vào cặp reqid của bản tin gửi đi và bản tin nhận về, nếu giá trị này xuất hiện trên cả bản tin gửi đi và bản tin nhận về, thì có nghĩa bản tin được gửi thành công, còn ngược lại nếu redid chỉ có trên bản tin gửi đi mà không có trên bản tin gửi về thì bản tin đó lỗi.

Để tính số bản tin gửi đi, các bạn cần dựa vào cụm từ "cmd": "set". Vì vậy chúng ta chỉ cần đếm số lần xuất hiện của cụm từ "cmd": "set" trong bản tin thì có thể tính được số bản tin gửi đi.

Gợi ý: Hàm strstr() dùng để tìm kiếm vị trí của xâu con str2 trong xâu str1, nhưng bạn có thể suy nghĩ cách để có thể sử dụng hàm strstr() nhằm đếm được số lần xuất hiện của xâu "cmd":"set" trong trong xâu fileStr. Chú ý bạn cần biến đổi "cmd":"set" ⇒ "\"cmd\":\"set\"" khi truyền vào hàm strstr(). Để hiểu thêm về hàm strstr() thì bạn có thể xem lại "Bài 10 - Chuỗi ký tự".

Kết quả: 



Câu 2: Tính số bản tin được gửi đi từ thiết bị cho trước, các bạn nhập vào các mã network của thiết bị sau đó, chương trình sẽ lọc ra và hiển thị các bản tin của thiết bị đó. Viết hàm trả về số bản tin gửi đi của từ thiết bị khi nhập mã network và hiển thị các bản tin của thiết bị đó.

Ví dụ khi nhập "dc53" hoặc DC53 màn hình sẽ hiển thị ra các bản tin tương ứng như sau:

Kết quả:



Gợi ý: Với yêu cầu này bạn có thể làm theo các bước sau đây:

Step 1: Bạn dùng hàm scanf() để đọc mã network nhập từ màn hình, đồng thời khởi tạo biến đếm = 0.

Step 2: Từ fileStr là toàn bộ nội dung log đọc được từ file, bạn tách thành các bản tin (chính là các dòng như bạn nhìn thấy ở file log). Các bản tin trong file log được phân cách nhau bằng ký tự xuống dòng '\n'. Bạn có thể dùng hàm strtok() với ký tự để phân tách là '\n' để tách fileStr thành từng bản tin. Cách sử dụng hàm strtok() để phân tách xâu thì bạn có thể xem ở "Bài 10 - Chuỗi ký tự" và xem thêm ở đây nhé.

Step 3: Với từng bản tin của file log đã được tách ra từ step 2, bạn dùng hàm strstr() để kiểm tra xem trong bản tin đó có đồng thời chứa cả 2 xâu là "cmd":"set" (là bản tin gửi đi) và mã network nhập từ màn hình ở step 1 không?  Nếu có thì bạn in bản tin đó ra màn hình, rồi tăng biến đếm lên thêm 1.

Step 4: Bạn in biến đếm ra màn hình.

[Yêu cầu nâng cao] Câu 3: Tính số công tắc có trao đổi thông tin với bộ điều khiển trung tâm trong thời gian Log. Mỗi công tắc có 1 địa chỉ Network và Endpoint riêng biệt, trường "type" là "switch". Viết hàm hiển thị số lượng và địa chỉ của công tắc đã trao đổi thông tin với bộ điều khiển trung tâm trong thời gian Log.

Gợi ý: Với yêu cầu này bạn có thể làm theo các bước sau đây:

Step 1: Khởi tạo mảng của xâu để chứa danh sách địa chỉ network và endpoint của công tắc.

Step 2: Tương tự với cách làm như step 2 ở yêu cầu bên trên, từ fileStr bạn tách thành các bản tin của file log.

Step 3: Với từng bản tin đã được tách ở step 1, bạn cũng dùng hàm strstr() để kiểm tra xem bản tin đó có chứa xâu "type":"switch"" hay ko?

Nếu bản tin đó có chứa xâu "type":"switch"" thì bạn tiếp tục dùng hàm strtok() để tách lấy địa chỉ network và endpoint của công tắc. 

Sau đó bạn kiểm tra xem địa chỉ network và endpoint này đã tồn tại trong danh sách địa chỉ network và endpoint hay chưa? Nếu chưa thì bạn thêm địa chỉ network và endpoint này vào danh sách.

Step 4: Bạn đếm số địa chỉ network và endpoint có trong danh sách, đồng thời in danh sách này ra màn hình.

Kết quả:



[Yêu cầu nâng cao] Câu 4: Tính số bản tin gửi đi bị lỗi, không nhận phản hồi lại. Dựa vào "reqid", các bạn cần tìm ra số bản tin gửi đi mà không nhận được phản hồi. Viết hàm trả về giá trị số bản tin gửi đi bị lỗi.

Gợi ý: Với yêu cầu này bạn có thể làm theo các bước sau đây:

Step 1: Bạn khởi tạo số lượng bản tin lỗi  = 0.

Step 2: Tương tự với cách làm như step 2 của câu 2 bên trên, từ fileStr bạn tách thành các bản tin của file log.

Step 3: Bạn duyệt từng cặp bản tin như sau:

 3.1. Với bản tin đầu tiên bạn dùng hàm strstr() để tìm vị trí của xâu "reqid" ở trong bản tin đó. Từ xâu trả về của hàm strstr(), bạn tách lấy giá trị của reqid của bản tin.

 3.2. Với cách làm tương tự bạn lấy được giá trị của reqid của bản tin tiếp theo. 

 3.3. Nếu giá trị reqid của 2 bản tin này là khác nhau thì bạn tăng số bản tin gửi đi bị lỗi thêm 1.  

 3.4. Bạn tiếp tục lặp lại bước 3.1 bên trên với bản tin thứ 3, thứ 5 cho đến hết file log. 

Step 4: Bạn in số bản tin bị lỗi ra màn hình.

Kết quả:



Câu 5: Tính độ trễ lớn nhất giữa bản tin gửi đi và bản tin phản hồi, tính bằng mili giây (ms). Dựa vào trường thời gian, các bạn có thể tính bằng cách lấy thời gian phản hồi trừ đi thời gian gửi đi, không tính đến các bản tin lỗi. Viết hàm tìm độ trễ lớn nhất giữa các bản tin gửi đi và bản tin phản hồi.

Gợi ý: Với yêu cầu này bạn có thể làm theo các bước sau đây:

Step 1: Bạn khởi tạo biến độ độ trễ lớn nhất maxdelay = 0.

Step 2: Tương tự với cách làm như step 2 của câu 2 bên trên, từ fileStr bạn tách thành các bản tin của file log.

Step 3: Tương tự như câu 4 bên trên, bạn duyệt từng cặp bản tin như sau:

 3.1. Với bản tin đầu tiên:

 - Dùng hàm strtok() để tách thời gian của bản tin, rồi tính giá trị thời gian này theo đơn vị mili giây.

 - Lấy giá trị reqid của bản tin.

 3.2. Với cách làm tương tự bạn lấy được thời gian tính theo mili giây và giá trị của reqid của bản tin tiếp theo. 

 3.3. Nếu giá trị reqid của 2 bản tin này là giống nhau thì tính delay = thời gian của bản tin thứ 2 - thời gian của bản tin  thứ 1. Sau đó bạn so sánh, nếu giá trị delay > maxdelay thì bạn gán lại maxdelay = delay.

 3.4. Bạn tiếp tục lặp lại bước 3.1 bên trên với bản tin thứ 3, thứ 5 cho đến hết file log. 

Step 4: Bạn in giá trị maxdelay ra màn hình.

Kết quả:



[Yêu cầu nâng cao] Câu 6: Tính thời gian trễ trung bình trong khoảng thời gian log, tương tự câu 5 thời gian trễ trung bình này chỉ tính trên các bản tin điều khiển thành công. Viết hàm tính độ trễ trung bình trong khoảng thời gian log, là giá trị trung bình cộng giữa các độ trễ của bản tin gửi đi và bản tin phản hồi.

Giải thích: Giả sử các độ trễ giữa bản tin gửi đi và bản tin phản hồi lần lượt là X1, X2, X3, X4 ... Khi đó cách tính độ trễ trung bình trong khoảng thời gian log Xtb là:

                  Xtb = (X1 + X2 + X3 + X4) / 4

Gợi ý: Bạn làm tương tự như câu 5 ở trên, nhưng bạn không tính giá trị maxdelay nữa, mà bạn tính giá trị trung bình của delay cho mỗi cặp bản tin trong toàn bộ file log.

Kết quả:

-----------------------------------------

Báo cáo thuyết minh bài ASM2
1. Hàm số bản tin gửi đi
- Bước 1: dung hàm strtok để tách các bản tin trong chuỗi dựa vào kí tự kết thúc dòng ‘\n’
	Token=strtok(fileStr,”\n”);
- Bước 2: Dùng vòng lặp while, điều kiện token !=NULL
	Trong vòng lặp while, dùng hàm strstr(token,str_search), với str_search=”\”cmd\”:\”set\””
Nếu hàm strstre(token,str_search) trả về giá trị khác NULL thì sẽ in ra token – chính là bản tin gửi đi. Đồng thời dùng 1 biến sum để tính tổng số bản tin gửi đi.

2. Hàm tính số bản in từ thiết bị:
- Bước 1: dung hàm strtok để tách các bản tin trong chuỗi dựa vào kí tự kết thúc dòng ‘\n’
	Token=strtok(fileStr,”\n”);
Bước 2: Nhập địa chỉ network của thiết bị:
Bước 3: dùng vòng lặp while, điều kiện token !=NULL
	Trong vòng lặp while, sử dụng hàm tìm kiếm strstr() để tìm kiếm mã network và “cmd:set”
	Nếu thỏa mãn cả 2 điều kiện thì sẽ in ra bản tin token này. Đồng thời tang biến đếm sum lên để tính tổng tin đã gửi đi từ thiết bị này.

3. Hàm số công tắc:
Với hàm số công tắc, thì do type: switch ở bản tin nào cũng có nên ta sẽ tiếp tục tìm kiếm dựa vào chuỗi cmd:set
Bước 1: Tạo 1 mảng char_network[100]; sum: là tổng số thiết bị công tắc
Bước 2: tách thành các bản ghi như các hàm trên dựa vào kí tự kết thúc dòng ‘\n’
Bước 3: Dùng vòng lặp while (token!=NULL)
	3.1. Dùng hàm strstr(token,”set”); để lấy các bản tin gửi đi
	3.2. Nếu strstr(token,”set”)!=NULL thì sẽ:
		3.2.1. Tìm kiếm chuỗi dựa vào “-“
		3.2.2. Copy 5 kí tự trong chuỗi rồi gán vào mảng tạm chuoi[];
		3.2.3. Tìm kiếm chuoi trong mang_network
			Nếu chưa có thì nối thêm vào mang_network
			Tăng biến đếm ++sum; để đếm số thiết bị
Bước 4: tách các thiết bị trong mang_network dựa vào dấu “-“ trong mảng
Strtok(mang_network,”-“)
Sau đó dùng vòng lặp for để in ra.
Riêng endpoint của công tắc trong bài này đều bằng 1 nên ko cần xử lý.
Trường hợp endpoint có nhiều giá trị hơn ta cũng có thể làm tương tự, lưu vào 1 mảng kí tự, sau đó xuất ra.

4. Hàm tính số bản tin gửi lỗi
Bước 1: tách các bản ghi
Bước 2: Dùng vòng lặp while
	Trong vòng lặp while ta sẽ dùng hàm strtr 2 lần để lấy reqid
	pFound=strstr(token,s_requid);
       	 token=strtok(NULL,s);
        	pFound1=strstr(token,s_requid);
       	 token=strtok(NULL,s);
	Sau đó dùng hàm strcmp(pFound,pFound1), neus hàm này khác 0 thì sẽ tang biến đếm số bản tin lỗi lên 1.
Bước 3. Trả về kết quả là sobantinloi;

5. Hàm tính thời gian trễ lớn nhất:
Bước 1: Tách các bản ghi
Bước 2 dùng vòng lặp while
	Trong while ta dùng strtok 2 lần để lấy các giá trị thời gian ở bản ghi đi và bản ghi đến
	Sau đó tách lấy phút, giây. 
	Dùng hàm atof để chuyển sang kiểu float.
	Chuyển hết phút sang giây bằng cách * 60;
	Cuối cùng, ta sẽ dựa vào reqid bằng cách dùng strstr để tính 2 reqid ở 2 bản tin liền nhau đi và đến

