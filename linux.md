# dpkg
- dpkg -l 　　　　　　　　　：インストール済みパッケージ情報の表示
  -  1文字目　u:未知　i:インストール済み　r:設定を残して削除　p:完全に削除
  -　2文字目　n:未インストール　i:インストール済み　c:未設定　u:展開されていない　f:設定失敗　h:インストール途中で失敗
  -　3文字目　ブランク:エラーなし　h:現在のバージョンと設定を変更しない　r:再インストールを要す　x:障害がある
- dpkg -I ファイル名.deb　：パッケージの情報を表示
- dpkg --contents　ファイル名.deb　：パッケージ内のファイルを表示
- dpkg -i ファイル名.deb　：インストール
- dpkg -s パッケージ　　　：パッケージ情報の表示
- dpkg -r パッケージ　　　：パッケージを削除
- dpkg --purge パッケージ ：関連ファイルを含めパッケージを削除

- debパッケージの種類　：　DFSGに従う
　- セクション：内容
　- Main:Debian Project公式
　- Contrib:
　- Non-Free:
　- Non-US/Main:
　- Non-US/NonFree:

　- stable:安定板
　- testing:テスト版
　- unstable:不安定版

# 高速なミラーサイトを検索する
- netselect [-vv] LIST
- netselect-apt   : sources.listファイルを生成　->　/etc/apt


# apt
- apt-get update
- apt-get check

- apt-cache search キーワード　　[--full]　　：キーワードを含むパッケージ情報を表示
- apt-cache show パッケージ　　　　　　　　　：インストールされているパッケージの情報を表示　　
- apt-cache showpkg  パッケージ　　　　　　　：インストールされているパッケージの詳細情報を表示　　
- apt-cache depends パッケージ　　　　　　　　：依存/競合情報を表示

- apt-get install パッケージ   ：依存パッケージも含めてインストールされる
　- 　/etc/apt/sources.listの情報を基にパッケージを検索

- apt-get -s upgrade / apt-get --no-act upgrade
- apt-get [-u] upgrade :-uを併用すると実行結果を表示
- apt-cdrom -d デバイス　add
- apt-get -u dist-upgrade

- apt-get remove パッケージ
- apt-get --purge remove パッケージ　　　：関連ファイルを含めてパッケージを削除する

