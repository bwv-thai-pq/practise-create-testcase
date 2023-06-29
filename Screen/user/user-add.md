# S201-3_ユーザー登録

## Screen's image
※Do không có hình minh họa màn hình nên dùng tạm hình minh họa của màn hình [S201-4_User edit]
![](./image/user-add.png)

## Screen access privileges
※Tham chiếu file [画面一覧] trên Google Drive

## Basic information
### Item list
| No. | Name | View | Type | Required | Max Chara | Validation | Default | API1(Res) | API3(Res) | API2(Param) |
| --- | ---- | ---- | ---- | -------- | --------- | ---------- | ------- | ------------ | ------------ | ------------ |
| 1 | キャンセル (trên) | Y | button | - | - | - | - | - | - | - |
| 2 | 画像 | Y | image | - | - | - | Hiển thị hình mặc định trên Mock | - | - | imageFile |
| 3 | ファイルを選択 | Y | file | - | - | - | - | - | - | - |
| 3-1 | 画像を削除 | Y | button | - | - | - | - | - | - | - |
| 4 | 氏名 | - | text | Y | 20 | ※Tham chiếu phần [Trigger processing content] bên dưới | - | - | - | name |
| 5 | 所属 | - | radio | Y | - | ※Tham chiếu phần [Trigger processing content] bên dưới | - | organization.name, organization.lowOrganization.name | - | organizationId |
| 5-1 | グループ | - | check | - | - | - | - | - | name | userGroupIdList |
| 5-2 | デフォルト公開グループ | - | check | - | - | - | - | - | name | defaultPublicGroupIdList |
| 6 | E-mail | - | text | Y | 50 | ※Tham chiếu phần [Trigger processing content] bên dưới | - | - | - | email |
| 7 | パスワード | - | pass | Y | - | ※Tham chiếu phần [Trigger processing content] bên dưới | - | - | - | password |
| 8 | 確認 | - | pass | Y | - | ※Tham chiếu phần [Trigger processing content] bên dưới | - | - | - | - |
| 9 | 権限 | - | radio | Y | - | 1: 管理者<br/>2: ユーザー<br/>※Tham chiếu phần [Trigger processing content] bên dưới | - | - | - | authority |
| 9-1 | 管理者フラグ | - | check | - | - | - | - | - | - | adminFlag |
| 9-2 | メール配信許可フラグ | - | check | - | - | - | - | - | - | mailDeliveryPermit |
| 10 | 追加 | Y | button | - | - | - | - | - | - | - |
| 11 | キャンセル (dưới) | Y | button | - | - | - | - | - | - | - |

## In-screen item / Processing privileges control
| No. | Name | privileges | Content |
| --- | ---- | ---- | ---- |
| 9-1 | 管理者フラグ | 0 (システム管理者) | Không hiển thị với quyền hạn 1 (組織管理者), 2 (一般ユーザー) |
| 9-2 | メール配信許可フラグ | 0 (システム管理者) | Không hiển thị với quyền hạn 1 (組織管理者), 2 (一般ユーザー) |

## Trigger processing content

| No. | Name | Action | Content |
| --- | ---- | ------ | ------- |
| 1 | キャンセル (trên) | Khi nhấn | Chuyển sang màn hình [S201-1_ユーザー検索]　|
| 2 | 画像 | Sau khi chọn file bằng [ファイルを選択] | Hiển thị nội dung đã chọn vào vùng hiển thị hình ảnh　|
| 3 | ファイルを選択 | Khi nhấn | Hiển thị cửa sổ cho chọn file<br/>※Tham chiếu mục [Image file] trong file [common.md]　|
| 3-1 | 画像を削除 | Khi nhấn | Xóa file đang chọn |
| 4 | 氏名 | Khi focus-out | ・Khi focus-out, nếu chưa nhập gì thì hiển thị message [ec-00001], set {1} = 氏名<br/>・Khi nội dung nhập vượt quá max-length, hiển thị message [ec-00003], set {1} = 氏名, {2} = 20 |
| 5 | 所属 | Khi focus-out | ・Khi focus-out, nếu chưa chọn gì thì hiển thị message [ec-00001], set {1} = 所属 |
| 6 | E-mail | Khi focus-out | ・Khi focus-out, nếu chưa nhập gì thì hiển thị message [ec-00001], set {1} = E-mail<br/>・Khi nội dung nhập vượt quá max-length, hiển thị message [ec-00003], set {1} = E-mail}, {2} = 50<br/>・Khi nhập sai format (vi phạm chuẩn của RFC), hiển thị message [ec-00026], set {1} = E-mail |
| 7 | パスワード | Khi focus-out | ・Khi focus-out, nếu chưa nhập gì thì hiển thị message [ec-00001], set {1} = パスワード<br/>・Khi nhập ký tự khác chữ số tiếng Anh 1 byte hoặc khác ký hiệu, hiển thị message [ec-00028], set {1} = パスワード<br/>・Khi focus-out, nếu số ký tự nhập <= 7 ký tự thì hiển thị message [ec-00100], set {1} = パスワード |
| 8 | 確認 | Khi focus-out | ・Khi focus-out, nếu chưa nhập gì thì hiển thị message [ec-00001], set {1} = 確認 |
| 9 | 権限 | Khi focus-out | ・Khi focus-out, nếu chưa chọn gì thì hiển thị message [ec-00001], set {1} = 権限 |
| 10 | 追加 | Khi nhấn | ・Trường hợp nội dung nhập ở [パスワード] != [確認], hiển thị message [ec-00029], set {1} = パスワード, {2} = 確認 |
| 11 | キャンセル (dưới) | Khi nhấn | Chuyển sang màn hình [S201-1_ユーザー検索] |

## Use API
| No. | Name | Action | API name | Param | Content |
| --- | ---- | ------ | -------- | ----- | ------- |
| 5 | 所属 | Khi khởi động | organizationSearch | - | ・Chạy API [organizationSearch (API1)]<br/>Trường hợp failure<br/>　Dừng lại ở màn hình này, hiển thị message API trả về<br/>Trường hợp success<br/>　Phản ánh giá trị trả về vào các hạng mục trên màn hình |
| 5-1 | グループ | Khi khởi động | groupSearch | [needsAll] =  1 (Yes) | ・Chạy API [groupSearch (API3)]<br/>Trường hợp failure<br/>　Dừng lại ở màn hình này, hiển thị message API trả về<br/>Trường hợp success<br/>　Phản ánh giá trị trả về vào các hạng mục trên màn hình |
| 5-2 | デフォルト公開グループ | Khi khởi động | groupSearch | [needsAll] =  1 (Yes) | ・Chạy API [groupSearch (API3)]<br/>Trường hợp failure<br/>　Dừng lại ở màn hình này, hiển thị message API trả về<br/>Trường hợp success<br/>　Phản ánh giá trị trả về vào các hạng mục trên màn hình |
| 10 | 追加 | Khi nhấn | userCreate | ※Tham chiếu phần [Basic information] bên trên | ・Chạy API [userCreate (API2)]<br/>Trường hợp failure<br/>　Dừng lại ở màn hình này, hiển thị message API trả về<br/>Trường hợp success<br/>　Chuyển sang màn hình [S201-2_ユーザー表示] |

### organizationSearch (API1)
Nothing

### userCreate (API2)
Nothing

### groupSearch (API3)
Nothing