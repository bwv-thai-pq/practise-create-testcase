# S201-2_ユーザー表示

## Screen's image
![](./image/user-view.png)

## Screen access privileges
※Tham chiếu file [画面一覧] trên Google Drive

## Basic information
### Item list
| No. | Name | View | Type | Required | Max Chara | Validation | Default | API1(Res) |
| --- | ---- | ---- | ---- | -------- | --------- | ---------- | ------- | ---------- |
| 1 | 一覧に戻る | Y | link | - | - | - | - | - |
| 2 | ユーザー画像 | Y | image | - | - | - | - | user.imagePath |
| 3 | 氏名 | Y | text | - | - | - | - | user.name |
| 4 | 所属 | Y | text | - | - | - | - | user.organization.name |
| 4-1 | グループ | Y | text | - | - | - | - | user.userGroup.group.name |
| 4-2 | デフォルト公開グループ | Y | text | - | - | - | - | user.userDefaultGroup.group.name |
| 5 | E-mail | Y | text | - | - | - | - | user.email |
| 6 | 権限 | Y | text | - | - | - | - | user.authority |
| 6-1 | 管理者フラグ | Y | check | - | - | - | - | user.adminFlag |
| 6-2 | メール配信許可フラグ | Y | check | - | - | - | - | user.mailDeliveryPermit |
| 7 | 修正 | Y | button | - | - | - | - | - |
| 8 | 削除 | Y | button | - | - | - | - | - |
| - | ユーザー動画 | - | - | - | - | - | - | - |
| 9 | 投稿日付 | Y | text | - | - | - | - | userMovie.movie.createdAt |
| 10 | 動画 | Y | image | - | - | - | Mỗi hàng hiển thị 4 record | userMovie.movie.thumbnailPath |
| 11 | 動画名 | Y | text | - | - | - | - | userMovie.movie.title |
| 12 | ユーザー画像 | Y | image | - | - | - | - | user.imagePath |
| 13 | ユーザー名 | Y | text | - | - | - | - | user.name |
| 14 | いいね | Y | button | - | - | - | - | - |
| 15 | いいね数 | Y | text | - | - | - | - | userMovie.movieGoodCount |
| 16 | コメント | Y | button | - | - | - | - | - |
| 17 | コメント数 | Y | text | - | - | - | - | userMovie.movieCommentCount |
| 18 | 詳細 | Y | button | - | - | - | - | - |
| 19-1 | ☆おすすめ | Y | button | - | - | - | - | - |
| 19-2 | ★解除 | Y | button | - | - | - | - | - |
| 20 | 削除 | Y | button | - | - | - | - | - |
| 21 | 一覧に戻る | Y | link | - | - | - | - | - |

## In-screen item / Processing privileges control
Nothing

## Trigger processing content

| No. | Name | Action | Content |
| --- | ---- | ------ | ------- |
| 1 | 一覧に戻る | Khi nhấn | Chuyển sang màn hình [S201-1_ユーザー検索]　|
| 7 | 修正 | Khi nhấn | Chuyển sang màn hình [S201-4_ユーザー編集]　|
| 8 | 削除 | Khi nhấn | ※Tham chiếu mục [Nút [削除] (Delete)] trong file [common.md]<br/>→Về parameter của message thì set {1} = ユーザー　|
| 10 | 動画 | Khi nhấn | ・Trường hợp [userSearchId.Response.userMovie.movie.type] = 1 (ユーザー動画)<br/>　Chuyển sang màn hình [S108-1_動画表示] ở trạng thái [Movie của user]<br/>・Trường hợp [userSearchId.Response.userMovie.movie.type] = 2 (公式動画)<br/>　Chuyển sang màn hình [S108-1_動画表示] ở trạng thái [Movie official] |
| 16 | コメント | Khi nhấn | ・Trường hợp [userSearchId.Response.userMovie.movie.type] = 1 (ユーザー動画)<br/>　Chuyển sang màn hình [S108-1_動画表示] ở trạng thái [Movie của user]<br/>・Trường hợp [userSearchId.Response.userMovie.movie.type] = 2 (公式動画)<br/>　Chuyển sang màn hình [S108-1_動画表示] ở trạng thái [Movie official] |
| 17 | 詳細 | Khi nhấn | ・Trường hợp [userSearchId.Response.userMovie.movie.type] = 1 (ユーザー動画)<br/>　Chuyển sang màn hình [S108-1_動画表示] ở trạng thái [Movie của user]<br/>・Trường hợp [userSearchId.Response.userMovie.movie.type] = 2 (公式動画)<br/>　Chuyển sang màn hình [S108-1_動画表示] ở trạng thái [Movie official] |
| 20 | 削除 | Khi nhấn | ※Tham chiếu mục [Nút [削除] (Delete)] trong file [common.md]<br/>→Về parameter của message thì set {1} = 動画<br/>　※Có chỉ định cử động sau khi xóa |
| 21 | 一覧に戻る | Khi khởi động | Chuyển sang màn hình [S201-1_ユーザー検索] |

## Use API
| No. | Name | Action | API name | Param | Content |
| --- | ---- | ------ | -------- | ----- | ------- |
| - | - | Khi khởi động | userSearchId | [id] = URL parameter | ・Chạy API [userSearchId (API1)]<br/>Trường hợp failure<br/>　Dừng lại ở màn hình này, hiển thị message API trả về<br/>Trường hợp success<br/>　Phản ánh giá trị trả về vào các hạng mục trên màn hình<br/>　※Tham chiếu phần [Basic information] bên trên |
| 8 | 削除 | Khi nhấn | userDelete | [id] = URL parameter | ・Chạy API [userDelete (API2)]<br/>Trường hợp failure<br/>　Dừng lại ở màn hình này, hiển thị message API trả về<br/>Trường hợp success<br/>・ Nếu [URLパラメータ] = [login.Response.id]<br/>Sau khi nhấn nút [削除] trên POPUP, hiển thị modal có message [ec-00085] và button [OK] ※Thiết kế của modal thì tham chiếu file [common.md]<br/>　→ Sau khi nhấn [OK], chuyển sang màn hình [S100-1_ログイン]<br/>・Nếu [URLパラメータ] != [login.Response.id]<br/>　Chuyển sang màn hình [S201-1_ユーザー検索] |
| 14 | いいね | Khi nhấn (ở trạng thái chưa nhấn like) | movieGoodCreate | [movieId] = movie.id của video bị nhấn nút | ・Chạy API [movieGoodCreate (API3)]<br/>Trường hợp failure<br/>　Dừng lại ở màn hình này, hiển thị message API trả về<br/>Trường hợp success<br/>　Hiển thị màu vàng lên hạng mục tương ứng, +1 vào hạng mục [いいね数] |
|  |  | Khi nhấn (ở trạng thái đã nhấn like) | movieGoodDelete | [movieId] = movie.id của video bị nhấn nút | ・Chạy API [movieGoodDelete (API4)]<br/>Trường hợp failure<br/>　Dừng lại ở màn hình này, hiển thị message API trả về<br/>Trường hợp success<br/>　Hiển thị màu xám lên hạng mục tương ứng, -1 vào hạng mục [いいね数] |
| 19-1 | ☆おすすめ | Khi nhấn | movieRecommendUpdate | [id] = movie.id của video bị nhấn nút<br/>[recommend] = 1 (Yes) | ・Chạy API [movieRecommendUpdate (API5)]<br/>Trường hợp failure<br/>　Dừng lại ở màn hình này, hiển thị message API trả về<br/>Trường hợp success<br/>　Ẩn hạng mục này, hiển thị hạng mục [★解除] |
| 19-2 | ★解除 | Khi nhấn |  | [id] = movie.id của video bị nhấn nút<br/>[recommend] = 0 (No) | ・Chạy API [movieRecommendUpdate (API5)]<br/>Trường hợp failure<br/>　Dừng lại ở màn hình này, hiển thị message API trả về<br/>Trường hợp success<br/>　Ẩn hạng mục này, hiển thị hạng mục [★おすすめ] |
| 20 | 削除 | Khi nhấn | movieDelete | [id] = movie.id của video bị nhấn nút | ・Chạy API [movieDelete (API6)]<br/>Trường hợp failure<br/>　Dừng lại ở màn hình này, hiển thị message API trả về<br/>Trường hợp success<br/>　Nothing special |

### userSearchId (API1)
| No. | Name | Content |
| --- | -- | --- |
| 2 | ユーザー画像 | ※Tham chiếu mục [Hình user, hình người đăng] trong file [common.md] |
| 6 | 権限 | ・Trường hợp user.authority = 0, hiển thị chữ "システム管理者" (※Tuy nhiên, về quyền hạn 0:システム管理者, do không có luồng chuyển đến màn hình này chỉ có cách vào bằng link trực tiếp, nên về cơ bản nghĩ là ít người nhìn thấy)<br/>・Trường hợp user.authority = 1, hiển thị chữ "管理者"<br/>・Trường hợp user.authority = 2, hiển thị chữ "ユーザー" |
| 10 | 動画 | ※Tham chiếu mục [Hình user, hình người đăng] trong file [common.md]<br/><br/>Trường hợp [userMovie.movie.thumbnailPath] = NULL or vì lý do nào đó mà không get được hình thì hiển thị file [thumb-error.svg] |
| 11 | 動画名 | Trường hợp userMovie.playedMovie = 1 (Yes), hiển thị hạng mục này màu xám |
| 12 | ユーザー画像 | ※Tham chiếu mục [Hình user, hình người đăng] trong file [common.md] |
| 14 | いいね | Trường hợp userMovie.yourGood = 1 (Yes), hiển thị hạng mục này màu vàng |
| 19-1 | ☆おすすめ | Trường hợp userMovie.movie.recommend = 0 (No), hiển thị |
| 19-2 | ★解除 | Trường hợp userMovie.movie.recommend = 1 (Yes), hiển thị |

### userDelete (API2)
Nothing

### movieGoodCreate (API3)
Nothing

### movieGoodDelete (API4)
Nothing

### movieRecommendUpdate (API5)
Nothing

### movieDelete (API6)
Nothing
