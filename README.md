#ConoHa備忘録
* ConoHaVPS 2g

 ##構築の流れ
  * テンプレートイメージを利用 // CentOS Ver.6.5 + WordPressのもの  
      まずはyum update    

  * rootで作業をするのはあまりよくないと書かれていたため新たに作業用ユーザーを追加する  
      $ adduser hoge // hogeの部分を改変  
      $ passwd hoge  
      $ gpasswd -a hoge wheel // User:hogeをGroup wheel に    

  * su及びsudoチェック  
      $ su hoge // hogeに切り替え  
      $ sudo echo "hoge"  
      hoge  
      $ su // root確認  
      $ su hoge // 以後基本的にUser:hogeで操作  
      $ id hoge  
      uid=500(hoge) gid=500(hoge) 所属グループ=500(hoge),10(wheel) // wheelチェック    

  * sudoers設定 // wheelのsudoコマンドを使用可能にする  
      $ visudo  
      /wheel // ファイル内を検索 nで次項へ  
      %wheel	ALL=(ALL)	ALL // コメントアウトを外す    

  * sshd編集  
      $ sudo vi /etc/ssh/sshd_config  
      Port 22 // コメントアウトを外す  
      Port 10022 // 追加  
      //Port 10022については後述参照のこと  
      RSAAuthentication yes //コメントアウト外す  
      PubkeyAuthentication yes //コメントアウト外す  
      AuthorizedKeysFile      .ssh/authorized_keys //コメントアウト外す    

      //パスワードでの認証を禁止(公開鍵認証のみ許可)  
      PermitEmptyPasswords no //コメントアウト  
      PasswordAuthentication no //そのまま    

      //チャレンジ/レスポンス認証を無効化する  
      //conohaサーバー側でsshd_configが書き換わらないようにするためのものらしい  
      ChallengeResponseAuthentication no //そのまま    

      //ログ出力レベルの指定  
      SyslogFacility AUTHPRIV //そのまま  
      LogLevel INFO //コメントアウト外した    

  * 再起動  
      sudo service sshd restart // reloadでもいけるかも？？  
      sudo reboot  

  * 補足説明(Port10022について)  
      Teratermにて接続する際  

      /etc/sysconfig/iptables  
      -A INPUT -p tcp -m tcp --dport 10022 -j ACCEPT  
      /etc/ssh/sshd_config  
      Port 10022  

     service sshd restart  
     service iptables restart  

  ##参考URL  
    *   Qiita(http://qiita.com/harapeko_wktk/items/ad4a2e0cb7f00fdfbf0d)  
    * QA@markit(http://qa.atmarkit.co.jp/q/3164)

