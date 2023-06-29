# Common

### Người phụ trách
(Briswell Co., Ltd ) Wakaki

### Trình duyệt
Trên PC<br/>Windows (Hệ điều hành mới nhất): Google Chrome, Microsoft Edge (Tất cả trình duyệt ở version mới nhất)<br/>
Mac (Hệ điều hành mới nhất): Google Chrome (version mới nhất)<br/><br/>Trên smartphone<br/>iPhone (Hệ điều hành mới nhất): Safari<br/>
Android (Hệ điều hành mới nhất): Không có gì đặc biệt

### Đối ứng smartphone
※Tất cả màn hình

### Hạn chế truy cập
・Trang công khai "public"<br/>
※Không hạn chế địa chỉ IP.v.v.

### Quyền hạn truy cập
※Tham khảo file [画面一覧] trên Google Drive

### Thiết kế màn hình
※Tham chiếu màn hình Mock

### Phần bảng danh sách record
・Về phần header bảng, toàn bộ hiển thị cố định<br/>
・Khi focus vào bảng danh sách record, hiển thị màu nền record đang bị focus khác với các record không bị focus để người dùng nhận biết đang focus vào record nào

### Phân trang
・Ở màn hình search, trường hợp có nhiều kết quả search thì cần thực hiện phân trang kết quả (tiến hành chỉ định số trang và số record trên một trang bên phía API)<br/>
　→Làm giống chức năng paging từ trước đến nay<br/>
・Thanh phân trang nằm bên dưới bảng danh sách record<br/>・Số record tối đa 1 trang thì theo thiết kế trong các màn hình, nếu không có mô tả thì 1 trang hiển thị tối đa 100 record<br/>
・Hiển thị số record hiện tại (該当件数) → Ví dụ: 該当件数　X件中Y件目からZ件目までを表示中 (trong X record kết quả search, đang hiển thị từ record thứ Y - thứ Z)<br/>　※Tổng số record data thì phán đoán từ [Response.Header X-Total-Count]

### Nút [検索] (Search)
・Các màn hình có chức năng search thì có spec chung là khi nhấn [Enter] = nhấn nút search<br/>・Trường hợp kết quả search là 0 record thì hiển thị message [ec-00002]<br/>
・Khi chuyển đến màn hình khác trong trạng thái có nhập ở các hạng mục điều kiện search, rồi quay lại màn hình này lần nữa từ màn hình đã chuyển (bằng cách nhấn nút [戻る] ở các màn hình add/edit), thì lưu giữ nội dung nhập ở các hạng mục điều kiện search rồi hiển thị lại<br/>
　→Giống với nút back của trình duyệt<br>・Sau khi search xong, tự động scroll tới vị trí hạng mục [該当件数] (không quay lại đầu trang)

### Nút [クリア] (Clear)
・Reset về trạng thái default của màn hình

### Khi Submit
・Trong thiết kế các màn hình, những hạng mục có đánh dấu [Y] ở cột Required thì ngoài lúc focus-out, khi submit cũng phải check validate required lần nữa<br/>
　→Khi xảy ra lỗi required thì focus-in vào ô nhập chưa điền (※Thứ tự ưu tiên focus-in là các hạng mục màn hình từ trên xuống dưới)

### Về dữ liệu đang chỉnh sửa
・**Không cần** làm chức năng lock này: Khi truy cập vào dữ liệu đang bị chỉnh sửa bởi người khác, hiển thị message [現在〇〇〇さんが編集中です。], cho chuyển sang màn hình hiển thị thay vì chỉnh sửa

### Chuyển màn hình từ trạng thái đang chỉnh sửa
・Khi chuyển đến màn hình khác trong trạng thái có dữ liệu đang chỉnh sửa dở dang, hiển thị dialog xác nhận [編集中の情報は保存されませんが、よろしいですか？] có 2 button [はい] và [いいえ]. (Chọn [はい] thì chuyển màn hình còn chọn [いいえ] thì đóng dialog, không làm gì cả)<br/>
※Ngoài nhấn nút chuyển màn hình nằm trong hệ thống này, phải làm cho cả trường hợp nhấn nút back, nút đóng tab của browser

### Timeout màn hình
・Thời gian time-out là 2 tiếng<br/>
・Sau khi time-out, hiển thị message [ec-00006]<br/>
※Luồng thao tác sau khi time-out như sau:<br/>
Ví dụ: Trên màn hình đã time-out nhấn submit<br/>
　　　↓<br/>
　　　Chuyển đến màn hình [login]<br/>
　　　↓<br/>
　　　Login lại<br/>
　　　↓Truy cập trực tiếp đến màn hình bị time-out ban nãy

### Hiển thị giá trị số
・Phần số nguyên (trước dấu chấm) hiển thị dấu phẩy [,] ngăn cách mỗi 3 chữ số<br/>
Ví dụ: 1,000,000.00

### Phòng ngừa vỡ CSS do số ký tự vượt quá vùng hiển thị
・Trường hợp UI trở nên không phù hợp nữa vì nguyên nhân CSS vỡ do số ký tự vượt quá vùng hiển thị, lược bỏ phần vượt quá vùng hiển thị và thêm dấu ba chấm (…) vào sau

### Khi lưu hoặc update dữ liệu
・Khi lưu hoặc update ở các màn hình, thì phải thực hiện check validation trước rồi mới chạy API lưu hoặc API update<br/>
・Khi bị lỗi check validation thì hiển thị message lỗi ngay dưới tên hạng mục<br/>
・Về nội dung message hiển thị khi bị lỗi check validation thì tham khảo file [メッセージ一覧] trên Google Drive (Tên hạng mục/ số ký tự/ loại ký tự thì tham khảo ở Item list có trong các thiết kế màn hình)<br/>
・Khi lưu hoặc update mà có lỗi ở hạng mục nhập nào đó thì focus vào hạng mục bị lỗi<br/>
・Khi lưu hoặc update thành công thì hiển thị [登録しました。] (đã đăng kí) or [更新しました。] (đã update) lên màn hình<br/>
・Hiển thị message [登録しました。] or [更新しました。] ở ngay dưới header màn hình (phần trên cùng của Body)

### Hiển thị thời gian
・Thời gian lưu trong DB toàn bộ đều là giờ UTC, khi hiển thị lên màn hìnhphải format sang dạng ngắn hơn (ví dụ YYYY/MM/DD, YYYY/MM.v.v.) thì cần chú ý để chuyển đổi cho chính xác

### Dấu check
・Khi chọn dấu check toàn bộ, chuyển sang trạng thái check toàn bộ/uncheck toàn bộ<br/>・Khi chọn dấu check ở đơn vị từng dòng, chuyển sang trạng thái check/uncheck dòng bị chọn

### Message hiển thị màn hình (※Bao gồm cả message đặc thù của màn hình)
※Tham khảo file [メッセージ一覧] trên Google Drive

### Image file
・Hiển thị tên file bên trên button chọn file <br>・Loại file là [jpeg], [jpg], [png]<br/>
　→Trường hợp chọn file khác với quy định (※Chỉ phán đoán bằng đuôi file xem có phải là file có thể chọn không), hiển thị message [ec-00059]<br/>
・Có thể đính kèm tối đa 1 file<br/>
・Khi chọn file max size là 2MB<br/>
　→Trường hợp vượt quá size thì hiển thị message [ec-00075]

### Movie file
・Hiển thị tên file bên trên button chọn file <br>・Loại file là [mp4], [mov], [MOV]<br>
　→Trường hợp chọn file khác với quy định (※Chỉ phán đoán bằng đuôi file xem có phải là file có thể chọn không), hiển thị message [ec-00086]<br>
・Có thể đính kèm tối đa 1 file<br>
・Khi chọn file max size là 6000MB<br>
　→Trường hợp vượt quá size thì hiển thị message [ec-00087]

### CSV file
・Set loại file là [CSV]<br>
　→Trường hợp lựa chọn loại file khác cái đã quy định (chỉ phán đoán theo đuôi file để xem có phải là file support không), hiển thị message [ec-00105], set parameter [{1:CSV}]
・Có thể đính kèm tối đa 1 file<br>
・Chọn file có file size tối đa là 2MB<br>
　→Trường hợp vượt quá giới hạn file size, hiển thị message [ec-00075]

### Hình user, hình người đăng
・Trường hợp được set thì hiển thị hình tương ứng, trường hợp chưa được set thì hiển thị hình default của màn hình Mock<br/>
・Khi get data , add Cookie gắn chữ kí Common (cloudFrontPolicy, cloudFrontSignature, cloudFrontKeyPairId) vào Header của Request rồi get <br/>	→Đối với các API.Response.imagePath <br/>・Cookie có gắn chữ kí Common sẽ lưu vào Cookie hay Session khi gọi API [login], [refreshToken] để sử dụng<br/>・Chi tiết về cách chỉ định Cookie có gắn chữ kí được hiển thị bên dưới<br/>　Cookie:CloudFront-Policy=XXXXX<br/>　Cookie:CloudFront-Signature=XXXXX<br/>　Cookie:CloudFront-Key-Pair-Id=XXXXX

### Movie
・Khi get data, add Cookie gắn chữ kí Movie (cloudFrontPolicy, cloudFrontSignature, cloudFrontKeyPairId) vào Header của Request rồi get <br/>　→Đối với movieSearchId.Response.movie.moviePath<br/>・Cookie gắn chữ kí Movie thì sẽ sử dụng movieSearchId.Response.movieSignatureCookie (cloudFrontPolicy, cloudFrontSignature, cloudFrontKeyPairId) mỗi lần <br/>　※**Không lưu** vào Cookie hay Session như [Hình user, hình người đăng]<br/>
・Chi tiết về cách chỉ định Cookie có gắn chữ kí được hiển thị bên dưới (**※Giống** với cách chỉ định của [Hình user, hình người đăng] đã nêu trên)<br/>　Cookie:CloudFront-Policy=XXXXX<br/>　Cookie:CloudFront-Signature=XXXXX<br/>　Cookie:CloudFront-Key-Pair-Id=XXXXX

### Nút [削除] (Delete)
・Trước khi chạy API xóa thì hiển thị dialog xác nhận [ec-00045] có hai nút 2 button (削除) (キャンセル)<br/>
　→Chọn [削除] thì chạy API xóa, chọn [キャンセル] thì đóng dialog, không làm gì cả<br/>・Sau khi chạy API xóa thì hiển thị message [ec-00037]<br/>　※Về thiết kế của POPUP thì xem hình của [タグ削除 (tag-delete-popup.md)]<br/>　※Chỉ trong trường hợp chỉ định cử động sau khi xóa ở các màn hình thì gắn cử động giống như dưới đây rồi xóa <br/>　　Hình dung như Sample2 dưới đây (※Suy cho cùng đây là mẫu)<br/>　　　https://webcake.stars.ne.jp/demo/jquery/jquery-animation-sample/

### POPUP
・Sau khi khởi động POPUP, nếu nhấn ra ngoài POPUP thì đóng POPUP lại

### Các lỗi ngoại lệ
※Khi phát sinh lỗi ngoại lệ, chuyển sang màn hình lỗi chung mà hiển thị các message dưới đây<br/><br/>
・Khi không có quyền truy cập (Lỗi 403)<br/>
　Hiển thị message [アクセスしようとした画面の権限がありません。]<br/>
・Khi không tồn tại màn hình (Lỗi 404)<br/>
　Hiển thị message [アクセスしようとした画面が見つかりません。]<br/>
　※Khi lỗi do truy cập vào id không tồn tại cũng chuyển đến màn hình này<br/>
・Khi phát sinh lỗi quan trọng (Lỗi 500)<br/>
　Hiển thị message [システムエラーが発生しました、システム管理者へお問い合わせください。]