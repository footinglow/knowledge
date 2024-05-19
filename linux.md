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
- freeコマンド
  - total=kernel使用中+プロセス使用中+free
  - カーネル使用中=解放不可能+解放可能
  - available=free+カーネル使用中の解放可能
  - buff/cacheはカーネル使用中の一部。解放不可能部分と解放可能部分がある
  - used=total-free-buff/cache
  - buff/cacheはページキャッシュとバッファキャッシュに使用
    - アクセス速度が遅いストレージデバイス上のファイルデータのキャッシュ
    - dd if=/dev/zero of=testfile bs=1M count=1K

- sar -r 1
  - 継続的に見たい場合、freeコマンドより使いやすい
  - total=該当なし
  - free=kbmemfree
  - buff/cache=kbbuffer+kbcached
  - available=該当なし

- メモリの回収
  - カーネルのメモリ管理システムはfreeが少なくなると、カーネル使用中の中解放可能部分にあるbuff/cacheを解放してfreeを増やす
  - それでもfreeが足りない場合は、Out Of Memory OOMになる。
  - メモリ管理システムのOOM Killerが適当なプロセスを強制終了して空きメモリをつくる
  - dmesgにoom-kill:...のログで確認できる
  - ps auxのRSSはプロセスが使っているメモリ量
  - 「linuxにおけるOOM発生時の挙動」の記事
- 仮想記憶
  - 課題
    - メモリの断片化
    - マルチプロセスの実現が困難
    - 不正な領域へのアクセス
  - 仮想アドレスを用いて間接的にメモリにアクセスする
  - /proc/プロセスID/mapsは仮想アドレス
  - メモリはページ単位で管理4KiBなど
  - 1ページに対応するデータをページテーブルエントリ
  - ページテーブルはカーネルが作るが、仮想アドレスを物理アドレスに変換するのはCPU
  - ページにない場合、ページフォールトとなり、SIGSEGV
- プロセスへの新規メモリの割り当て
  - ①メモリ領域の割り当て
    - mmapシステムコール
  - ②メモリの割り当て
    - mmapで割り当てた仮想メモリへの最初のアクセスで物理メモリを割り当てる方式を、デマンドページングと呼ぶ
    - sar -B 1でページフォールト発生回数がわかる
- ページテーブルの階層化
  - x86_64アーキは4段階層
- ヒュージテーブル
  - 通常より大きなサイズのページを使うことで、ページテーブル数を減らし、ページテーブルに使うメモリサイズを減らす
- トランスペアレントヒュージページ
  - 自動的にヒュージページにする機能
  - ページを結合、分解するため性能が劣化することもある
  - /sys/kernel/mm/transparent_hugepage/enabled
  - 