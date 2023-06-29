# S201-4_ユーザー編集

## Screen's image
![](./image/user-edit.png)

## Screen access privileges
※Tham chiếu file [画面一覧] trên Google Drive

## Basic information
### Item list
| No. | Name | View | Type | Required | Max Chara | Validation | Default | API1(Res) | API2(Res) | API5(Res) | API3(Param) |
| --- | ---- | ---- | ---- | -------- | --------- | ---------- | ------- | ---------- |---------- | --- | --- |
| 1 | キャンセル (trên) | Y | button | - | - | - | - | - | - | - | - |
| 2 | 画像 | Y | image | - | - | - | - | user.imagePath | - | - | imageFile |
| 3 | ファイルを選択 | Y | file | - | - | - | - | - | - | - | - |
| 4 | 画像を削除 | Y | button | - | - | - | - | - | - | - | - |
| 5 | 氏名 | - | text | Y | 20 | ※Tham chiếu phần [Trigger processing content] bên dưới | - | user.name | - | - | name |
| 6 | 所属 | - | radio | Y | - | ※Tham chiếu phần [Trigger processing content] bên dưới | - | user.organization.name | name, lowOrganization.name | - | organizationId |
| 6-1 | グループ | - | check | - | - | - | - | user.userGroup.group.name | - | name | userGroupIdList |
| 6-2 | デフォルト公開グループ | - | check | - | - | - | - | user.defaultPublicGroup.group.name | - | name | defaultPublicGroupIdList |
| 7 | E-mail | - | text | Y | 50 | ※Tham chiếu phần [Trigger processing content] bên dưới | - | user.email | - | - | email |
| 8 | 新しいパスワード | - | pass | - | - | - | Hiển thị message [ec-00082] bên dưới ô nhập hạng mục này | - | - | - | password |
| 9 | 確認 | - | pass | - | - | ※Tham chiếu phần [Trigger processing content] bên dưới | - | - | - | - | - |
| 10 | 権限 | - | radio | Y | - | 1: 管理者<br/>2: ユーザー<br/>※Tham chiếu phần [Trigger processing content] bên dưới | - | user.authority | - | - | authority |
| 10-1 | 管理者フラグ | - | check | - | - | - | - | user.adminFlag | - | - | adminFlag |
| 10-2 | メール配信許可フラグ | - | check | - | - | - | - | user.mailDeliveryPermit | - | - | mailDeliveryPermit |
| 11 | 上書き保存 | Y | button | - | - | - | - | - | - | - | - |
| 12 | キャンセル (dưới) | Y | button | - | - | - | - | - | - | - | - |
| 13 | このユーザーを削除する | Y | button | - | - | - | - | - | - | - | - |

## In-screen item / Processing privileges control
| No. | Name | privileges | Content |
| --- | ---- | ---- | ---- |
| 10-1 | 管理者フラグ | 0 (システム管理者) | Không hiển thị với quyền hạn 1 (組織管理者), 2 (一般ユーザー) |
| 10-2 | メール配信許可フラグ | 0 (システム管理者) | Không hiển thị với quyền hạn 1 (組織管理者), 2 (一般ユーザー) |

## Trigger processing content

| No. | Name | Action | Content |
| --- | ---- | ------ | ------- |
| 1 | キャンセル (trên) | Khi nhấn | Chuyển sang màn hình [S201-1_ユーザー検索]　|
| 2 | 画像 | Sau khi chọn file bằng [ファイルを選択] | Hiển thị nội dung đã chọn vào vùng hiển thị hình ảnh　|
| 3 | ファイルを選択 | Khi nhấn | Hiển thị cửa sổ cho chọn file<br/>※Tham chiếu mục [Image file] trong file [common.md]　|
| 4 | 画像を削除 | Khi nhấn | Xóa file đang chọn |
| 5 | 氏名 | Khi focus-out | ・Khi focus-out, nếu chưa nhập gì thì hiển thị message [ec-00001], set {1} = 氏名<br/>・Khi nội dung nhập vượt quá max-length, hiển thị message [ec-00003], set {1} = 氏名, {2} = 20 |
| 6 | 所属 | Khi focus-out | ・Khi focus-out, nếu chưa chọn gì thì hiển thị message [ec-00001], set {1} = 所属 |
| 7 | E-mail | Khi focus-out | ・Khi focus-out, nếu chưa nhập gì thì hiển thị message [ec-00001], set {1} = E-mail<br/>・Khi nội dung nhập vượt quá max-length, hiển thị message [ec-00003], set {1} = E-mail}, {2} = 50<br/>・Khi nhập sai format (vi phạm chuẩn của RFC), hiển thị message [ec-00026], set {1} = E-mail |
| 8 | 新しいパスワード | Khi focus-out | ・Khi nhập ký tự khác chữ số tiếng Anh 1 byte hoặc khác ký hiệu, hiển thị message [ec-00028], set {1} = 新しいパスワード<br/>・Khi focus-out, nếu số ký tự nhập <= 7 ký tự thì hiển thị message [ec-00100], set {1} = 新しいパスワード |
| 9 | 確認 | Khi focus-out (※Chỉ khi hạng mục [新しいパスワード] có nhập) | ・Khi focus-out, nếu chưa nhập gì thì hiển thị message [ec-00001], set {1} = 確認 |
| 10 | 権限 | Khi focus-out | ・Khi focus-out, nếu chưa chọn gì thì hiển thị message [ec-00001], set {1} = 権限 |
| 11 | 上書き保存 | Khi nhấn | ・Trường hợp nội dung nhập ở [新しいパスワード] != [確認], hiển thị message [ec-00029], set {1} = 新しいパスワード, {2} = 確認 |
| 12 | キャンセル (dưới) | Khi nhấn | Chuyển sang màn hình [S201-1_ユーザー検索] |
| 13 | このユーザーを削除する | Khi nhấn | ※Tham chiếu mục [Nút [削除] (Delete)] trong file [common.md]<br/>→Về parameter của message thì set {1} = ユーザー |

## Use API
| No. | Name | Action | API name | Param | Content |
| --- | ---- | ------ | -------- | ----- | ------- |
| - | - | Khi khởi động | userSearchId | [id] = URL parameter | ・Chạy API [userSearchId (API1)]<br/>Trường hợp failure<br/>　Dừng lại ở màn hình này, hiển thị message API trả về<br/>Trường hợp success<br/>　Phản ánh giá trị trả về vào các hạng mục trên màn hình<br/>　※Tham chiếu phần [Basic information] bên trên |
| 6 | 所属 | Khi khởi động | organizationSearch | - | ・Chạy API [organizationSearch (API2)]<br/>Trường hợp failure<br/>　Dừng lại ở màn hình này, hiển thị message API trả về<br/>Trường hợp success<br/>　Phản ánh giá trị trả về vào các hạng mục trên màn hình<br/>　※Tham chiếu phần [Basic information] bên trên |
| 6-1 | グループ | Khi khởi động | groupSearch | [needsAll] =  1 (Yes) | ・Chạy API [groupSearch (API5)]<br/>Trường hợp failure<br/>　Dừng lại ở màn hình này, hiển thị message API trả về<br/>Trường hợp success<br/>　Phản ánh giá trị trả về vào các hạng mục trên màn hình<br/>　※Tham chiếu phần [Basic information] bên trên |
| 6-2 | デフォルト公開グループ | Khi khởi động | groupSearch | [needsAll] =  1 (Yes) | ・Chạy API [groupSearch (API5)]<br/>Trường hợp failure<br/>　Dừng lại ở màn hình này, hiển thị message API trả về<br/>Trường hợp success<br/>　Phản ánh giá trị trả về vào các hạng mục trên màn hình<br/>　※Tham chiếu phần [Basic information] bên trên |
| 11 | 上書き保存 | Khi nhấn | userUpdate | [id] = URL parameter<br/>Các parameter dưới đây thì set nội dung tuân theo quy tắc dưới đây<br/>Trường hợp user.authority mà API [userSearchId] trả về = 0 (システム管理者)<br/>　[authority] = user.authority mà API [userSearchId] trả về<br/>Trường hợp không thay đổi [画像]<br/>　[imageFile] = blank<br/>　[needsImageDelete] = blank<br/>Trường hợp có thay đổi [画像]<br/>　[imageFile] = Tham chiếu phần [Basic information] bên trên<br/>Trường hợp xóa [画像]<br/>　[needsImageDelete] = 1 (Yes)<br/>※Các hạng mục khác thì tham chiếu phần [Basic information] bên trên | ・Chạy API [userUpdate (API3)]<br/>Trường hợp failure<br/>　Dừng lại ở màn hình này, hiển thị message API trả về<br/>Trường hợp success<br/>　Chuyển sang màn hình [S201-2_ユーザー表示] |
| 13 | このユーザーを削除する | Khi nhấn | userDelete | [id] = user.id của user bị nhấn nút | ・Chạy API [userDelete (API4)]<br/>Trường hợp failure<br/>　Dừng lại ở màn hình này, hiển thị message API trả về<br/>Trường hợp success<br/>・ Nếu [URLパラメータ] = [login.Response.id]<br/>Sau khi nhấn nút [削除] trên POPUP, hiển thị modal có message [ec-00085] và button [OK] ※Thiết kế của modal thì tham chiếu file [common.md]<br/>　→ Sau khi nhấn [OK], chuyển sang màn hình [S100-1_ログイン]<br/>・Nếu [URLパラメータ] != [login.Response.id]<br/>　Chuyển sang màn hình [S201-1_ユーザー検索] |

### userSearchId (API1)
| No. | Name | Content |
| --- | -- | --- |
| 1 | 画像 | ※Tham chiếu mục [Hình user, hình người đăng] trong file [common.md] |
| 10 | 権限 | Trường hợp user.authority mà API [userSearchId] trả về = 0 (システム管理者), disable hạng mục này |

### organizationSearch (API2)
Nothing

### userUpdate (API3)
Nothing

### userDelete (API4)
Nothing

### groupSearch (API5)
Nothing