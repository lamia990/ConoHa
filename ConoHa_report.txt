14/11/13
ConoHa 登録(メモリ2Gプラン)
───────────────────────────
User:lamia // Group Wheel傘下
adduser hoge
passwd hoge
対話式
───────────────────────────
yum update // 最新版への更新
Port 22 to 10022 // # vi /ect/ssh/sshd_config
		 // # <- コメントアウト
		 // 10022の使用確認後に22を閉じる
───────────────────────────
sudoers設定(wheelがsudoコマンドを使えるように)

$ visudo
/wheel //ファイル内を検索 nで次へ。
%wheel        ALL=(ALL)       ALL //コメントアウトを外す
───────────────────────────
su及びsudoコマンドチェック

$ su hoge //hogeに切り替え
$ sudo echo "hoge"
hoge
$ su //rootになれるのを確認
$ su hoge //今後はhogeで操作
───────────────────────────
$ service sshd restart
$ service iptables restart
───────────────────────────
//パスワードでの認証を禁止(公開鍵認証のみ許可)
PermitEmptyPasswords no //コメントアウト
PasswordAuthentication no //そのまま
───────────────────────────
Teratermからssh接続を試みるも失敗
 // Port22へのアクセスは通ったが、Port10022へのアクセスは拒否
 // 鍵認証方式で初回ログインを試みたのをパスフレーズ認証に切り替えると通った(Port22)
 // Port10022へのアクセスが課題

URL
http://qiita.com/harapeko_wktk/items/ad4a2e0cb7f00fdfbf0

******************************************************

14/11/14
Teratermからの接続を再度試みるも失敗
iptablesをいじれば通ることが判明

/etc/sysconfig/iptables
-A INPUT -p tcp -m tcp --dport 10022 -j ACCEPT
↑を追記

その後sshd_configにて
Port10022を通す

後にsshdとiptablesをrestart

URL
http://qa.atmarkit.co.jp/q/3164
───────────────────────────

