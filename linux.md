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

- dpkg-query -W|grep ^lib

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
# プロセス
- sar -p 0 1 1     core#0のuser/kernel実行率を1秒に一回
- taskset -c 0 コマンド　　core#0でコマンド実行
- strace -T -o コマンド　　システムコール所要時間μsec
- ASLR address Space Layout Randomization
- ASLRに対応しているプログラムはPIE Position Independent executable
- posixspawnで子プロセス生成
- pstree -p
- ps -aux     u：ユーザが読みやすく
- 
- signal
  - SIGINT  ctrl-c
  - ディフォルトはSIGTERM
  - man 7 signal
  - SIGKILLで終了しないのは、uninterruptible sleep状態。ps auxでDのことが多いが、ユーザにはどうにもならないことが多い。
- バックグラウンドジョブ　jobsで表示　[1]がジョブ番号
- セッション:ログインセッションsshなども。
  - pty／数字
  - ps ajx  →SID
  - SIGHUP:セッションハングアップ
  - nohupコマンド
  - bashのdisown組み込みコマンド
- プロセスグループ
  - kill -100  PGID100のプロセス群へのシグナル
  - ps auxで+表示はフォアグラウンドプロセスグループ
  - バックグラウンドプロセスグループが端末操作しようとするとSIGSTOPを受けたような状態
- デーモンdaemon
  - 常駐プロセス、独自のセッション
  - ps ajxで親がinitで
  - SIDが?
# プロセススケジューラ
- time コマンド　　:コマンドを実行して実行時間測定結果を表示。コマンドとその子プロセスの値を合計して表示する。マルチコアの場合、それぞれのcoreの実行時間を加算するため、実時間と異なる。
- /sys/kernel/debug/sched/latency_nsのレイテンシターゲットの期間内に、各プロセスがCPU時間を得られる。
- マルチコアの場合はもう少し複雑で、core数、nice値、待ちプロセス数などで変わる
- sar -P 0 １ 1→%niceは優先度を0から高くしたプロセスがユーザーモードで実行している時間の割合
- ターンアラウンドタイム
- スループット
- SMT無効: echo on>/sys/devices/system/cpu/smt/control
# メモリ管理システム



