---
documentclass: ltjsarticle
output: pdf_document
figPrefix: '図.'
figureTitle: 図
tableTitle: 表
tblPrefix: '表.'
eqnPrefix: '式'
equationTitle: '式.'
---

# 詳解 Communication Suite 機能編



## 目次

<!-- TOC START min:2 max:3 link:true asterisk:false update:true -->
- [目次](#目次)
- [序章 トレーニングにあたって](#序章-トレーニングにあたって)
	- [トレーニング中の諸注意](#トレーニング中の諸注意)
- [第1章 OperatorAgent](#第1章-operatoragent)
	- [1-1. OperatorAgent のログイン](#1-1-operatoragent-のログイン)
	- [1-2. OperatorAgent のメイン画面](#1-2-operatoragent-のメイン画面)
	- [1-3. OperatorAgent と ControlCenter の通信](#1-3-operatoragent-と-controlcenter-の通信)
	- [1-4. OperatorAgent の起動・終了時の動作](#1-4-operatoragent-の起動終了時の動作)
	- [1-5. OperatorAgent からのコマンド実行](#1-5-operatoragent-からのコマンド実行)
	- [1-6. コマンドラインからの OperatorAgent 操作](#1-6-コマンドラインからの-operatoragent-操作)
	- [1-7 OperatorAgent のインストール](#1-7-operatoragent-のインストール)
- [第2章 SpeechVisualizer](#第2章-speechvisualizer)
	- [2-1. SpeechVisualizer のログイン](#2-1-speechvisualizer-のログイン)
	- [2-2. SpeechVisualizer ホーム画面](#2-2-speechvisualizer-ホーム画面)
	- [2-3. SpeechVisualizer 通話検索](#2-3-speechvisualizer-通話検索)
	- [2-4. SpeechVisualizer 通話詳細](#2-4-speechvisualizer-通話詳細)
	- [2-5. SpeechVisualizer 座席表](#2-5-speechvisualizer-座席表)
- [第3章 ControlCenter](#第3章-controlcenter)
	- [3-1. ControlCenter のログイン](#3-1-controlcenter-のログイン)
	- [3-2. ControlCenter ホーム](#3-2-controlcenter-ホーム)
	- [3-3. ログイン状況](#3-3-ログイン状況)
	- [3-4. ノード管理](#3-4-ノード管理)
	- [3-5. 認識オプションの設定](#3-5-認識オプションの設定)
	- [3-6. エクスポート](#3-6-エクスポート)
	- [3-7. ライセンス状況](#3-7-ライセンス状況)
	- [3-8. レポート](#3-8-レポート)
	- [3-9. メンテナンスモード](#3-9-メンテナンスモード)
- [第4章 RealtimeRecoder](#第4章-realtimerecoder)
	- [4-1. 通話録音機能](#4-1-通話録音機能)
	- [4-2. 配信機能](#4-2-配信機能)
<!-- TOC END -->

## 序章 トレーニングにあたって
 トレーニングの目的

- SI パートナー様及び Communication Suite ユーザ様に、Communication Suite の 各種機能を詳細に解説します。

### トレーニング中の諸注意
- 本トレーニングの受講資料及び内容を貴社外へ共有・配布することは禁止となります。
- 本トレーニングの内容の撮影・録音は原則として禁止となります。
- 一部、受講中の資料を補足した板書の内容などの撮影は可能ですが、講師の許可を得た上でお願い致します。
- 本資料の記載内容は、現時点（2020年03月 Communication Suite Ver3.6）での内容となります。  
  今後にリリースされるバージョンでは、記載内容が保証されない場合も生じます。

<div style="page-break-before:always"></div>

<hr/>

## 第1章 OperatorAgent

### 1-1. OperatorAgent のログイン
#### 1-1-1. OperatorAgent でログインすることの意味  

1. ユーザアカウントの認証（ユーザID と パスワード）  
2. ユーザアカウント権限のチェック  
3. ユーザと通話（内線番号）の関連付け  
4. 通話とプロジェクトの関連付け  
5. クライアント PC を OperatorAgent ノードとして ControlCenter にレジスト  
	<br />
	[@fig:login] は、OperatorAgent の基本的なログイン画面となります。  

	![基本のログイン画面](images/1-1-operatoragent-baselogin.png){#fig:login width=400px}

#### 1-1-2. OperatorAgent のログインに関連する ControlCenter の詳細設定項目

No. | 設定項目名       | デフォルト値 | 内容 |
---:|------------------|--------------|------|
1   |  ユーザIDの保存 | false        | true の場合、最後にログイン成功した ユーザID を保存する |
2   |  パスワードの保存 | false        | true の場合、最後にログイン成功したパスワードを保存する |
3   |  自動ログイン | false        | true の場合、保存済みのユーザID とパスワード（と内線番号）で自動ログインする |
4   |  内線番号の指定 | false        | true の場合、ログインダイアログに内線番号入力欄を表示する |
5   |  内線番号の情報が必要かどうか | S        | R = 必須, S = サーバ版では必須, N = 入力しない |
6   |  内線番号の保存 | false        | true の場合、最後にログイン成功した内線番号を保存する |

: 詳細設定 設定分類 : OperatorAgent - ログイン {#tbl:table}  

 - 『内線番号の指定』 を **"true"** にすることで、ログインダイアログに内線番号入力欄が追加されます。（[@fig:naisenari]。VDI 等のシンクライアント環境で、クライアント PC と電話機を固定で紐付けできない場合に有効です。）  

![内線番号入力可能なログイン画面](images/2020/02/1-1-operatoragent-naisenlogin.png){#fig:naisenari width=400px}

  - OperatorAgent のインストール時に内線番号を指定している場合には、指定番号が内線番号入力欄に表示されます。『内線番号の保存』 が **"false"** の場合も表示されます。）  
  変更すると、ログイン出来なくなったり、他の席の電話番号と紐付けされてしまうので注意してください。
  - 『内線番号の指定』 が **"false"** の場合でも、インストール時に内線番号が指定されていない場合で、かつ 『内線番号の情報が必要かどうか』 が "S" でかつサーバ版利用時 or "R" の場合には、内線番号入力欄が強制的に表示されます。
  - 『ユーザIDの保存』 が true の場合、ユーザIDは、  

    ```
    %USERPROFILE%/AppData/Local/Advanced_Media,_Inc/OperatorAgent.exe_StrongName_(長い文字列)/(バージョン番号)/user.config  
    ```
  の **LoginSettings/@LatestLoginUserId** に保存されます。 [^2] （この設定値は最後にログインに成功したユーザIDとなります。）

   - 『パスワードの保存』 が true の場合、ログインパスワードは、Windows の  
	 [コントロールパネル] → [ユーザー アカウント] → [資格情報マネージャー]  
  に自動入力されたユーザID に対応するパスワードが保存されます。（ [@fig:shikaku]。この設定値は最後にログインに成功したパスワードとなります。）  

![資格情報マネージャーのログイン情報](images/1-1-win_shikaku.png){#fig:shikaku width=500px}  

   - 『内線番号の保存』 が true の場合、内線番号は、  

       ```
       %USERPROFILE%/AppData/Local/Advanced_Media,_Inc/OperatorAgent.exe_StrongName_(長い文字列)/(バージョン番号)/user.config  
       ```
  の **LoginSettings/@LatestLoginLineKey** に保存されます。（この設定値は最後にログインに成功した内線番号となります。）

[^2]:最後に

#### 1-1-3. プロジェクトの選択
- ログインするユーザが複数のプロジェクトに所属している場合には、ログインダイアログに続けてプロジェクト選択ダイアログが表示されます。([@fig:project])

![プロジェクト選択画面](images/2020/02/1-1-operatoragent-projectchoice.png){#fig:project width=400px}

#### 1-1-4. 統合 Windows 認証

 - 統合 Windows 認証機能を有効化している場合には、ログイン画面は表示されません。ただし、通常ログイン同様、ユーザが複数プロジェクトに所属していれば、[1-1-3. プロジェクトの選択](#1-1-3-選択) ： [@fig:project] のダイアログが表示されます。
 - インストール時に内線番号が指定されていない場合には、内線番号入力ダイアログ（[@fig:naisen]）が追加表示されます。  

![内線番号入力ダイアログ](images/1-1-operatoragentLogin_naisenonly.png){#fig:naisen width=400px}

- 統合 Windows 認証を利用するための Communication Suite 上の設定はありません。  
  ただし、IIS に追加の設定が必要です。  
	1. OS の "機能と役割の追加" から IIS - Web サーバ - セキュリティ 設定で **Windows 認証** を有効化してください。([@fig:role])
	2. IIS マネージャーの Web サイトの設定で、ControlCenter と SpeechVisualizer のそれぞれのサイトの認証の設定を以下の図と同様に変更します。（[@fig:siteconfig]）  

![機能と役割の追加](images/1-1-IIS_role_windowslogin.png){#fig:role width=400px}

![Web サイトの設定](images/1-1-IIS_sitegonfig_login.png){#fig:siteconfig width=400px}

#### 1-1-5. OperatorAgent 自動ログイン（統合 Windows 認証を利用しない）
- [1-1-2. OperatorAgent のログイン機能に関連する ControlCenter の詳細設定項目](#1-1-2-operatoragent-機能関連-controlcenter-詳細設定項目)  ：  [@tbl:table] の 『自動ログイン』 が有効になっている場合には、統合 Windows 認証 を利用していなくてもログイン処理を省略可能です。  
	<br />  

	```plantuml
	@startuml

	skinparam {
		shadowing false
		defaultFontName "Segoe UI, BIZ UDPゴシック, sans-serif"
		BackgroundColor #afeeee
		ArrowColor black
	}

	skinparam activity  {
		BorderColor #000000
		DiamondBorderColor #008000
		BackgroundColor #ffffff
	}
	title アクティビティ図.1 [OA 自動ログイン判定]\n

	start
	:OperatorAgent 起動;
	if (内線番号情報が不要) then
		-[#blue]-> 　Yes ： 不要;
	else
		-[#red]-> No ： 不要ではない;
		if (内線番号必須) then
			-[#blue]-> Yes;
			if (内線番号入力済) then
				-[#blue]-> Yes;
			else
				-[#red]-> \nNo ： 未入力;
				:ログインダイアログ表示;
				end
			endif
		else
			-[#red]-> RR がローカルで動いていない場合に必要;
			if (サーバ認識構成) then
			-[#blue]-> \nYes;
				if (内線番号入力済) then
					-[#blue]-> Yes ： 入力済;
				else
					-[#red]-> \nNo ： 未入力;
					:ログインダイアログ表示;
					end
				endif
			else
				-[#red]-> \nNo ： クライアント\n認識構成;
			endif
		endif
	endif
	if (\nユーザIDとパスワードの両方が\n自動入力されている\n) then
		-[#blue]-> \nYes;
		if (自動ログインの設定は有効か？) then
			-[#blue]-> \nYes;
		else
			-[#red]-> \nNo;
			:ログインダイアログ表示;
			end
		endif
	else
		-[#red]-> No : いずれかもしくは両方が未入力;
		if (\nコマンドライン実行(※) で、引数により\nユーザIDとパスワードが設定されている\n) then
			-[#blue]-> Yes;
			if (自動ログインの設定は有効か？) then
				-[#blue]-> Yes;
			else
				-[#red]-> \n No ： 無効;
				:ログインダイアログ表示;
				end
			endif
		else
			-[#red]-> \n No ： 無効;
			:ログインダイアログ表示;
			end
		endif
	endif
	#dbff00:自動ログイン実行;
	floating note right: ※ コマンドライン引数については \n 1-2-6. コマンドラインからの OperatorAgent 操作 \nを参照して下さい。
	@enduml
	```

	<br />
- [@tbl:oalogin] は、OperatorAgent の正常系ログインエラーをまとめたものです。（異常系は含んでいません。）

	No. | 事由                 | ログインダイアログのメッセージ       | デバッグログへの出力 |
---:|---------------------|------------------|--------------|
1   | ユーザID 誤り | OperatorAgent サービスにログインできませんでした | ステータス: 43031 ユーザID 'XXX'、またはパスワードが違います。 |
2   | パスワード誤り | OperatorAgent サービスにログインできませんでした | ステータス: 43031 ユーザID 'XXX'、またはパスワードが違います。 |
3   | 内線番号誤り | OperatorAgent サービスにログインできませんでした | ステータス: 42601 指定した内線番号 'NNN' は削除されたか、登録されていません。 |
4   | 所属プロジェクト無し | 所属するプロジェクトがありません | 出力無し|
5   | OperatorAgent の利用権限無し | OperatorAgent サービスにログインできませんでした | ステータス: 43207 権限のあるプロジェクトがありません。 |
6   | ユーザの有効期限切れ | OperatorAgent サービスにログインできませんでした | ステータス: 43031 ユーザID 'XXX'、またはパスワードが違います。 |
7   | ユーザの重複ログイン | このユーザは他の PC で利用中です | 43204 ユーザは別のホストからすでにログインしています。 |
8   | 内線番号の重複ログイン | OperatorAgent サービスにログインできませんでした | ステータス: 43205 指定された回線は現在使用されています。 |
9   | Communication Suite ユーザ未登録 | OperatorAgent サービスにログインできませんでした | このエラーは、IIS に入力されたユーザ名またはパスワードが無効であるか、または IIS がユーザを認証するのためにそのユーザ名およびパスワードを使用できないときに発生します。 |
10   | ライセンス違反 | OperatorAgent サービスにログインできませんでした |ステータス: 40421 クライアントライセンス (インスタンス種別コード: 'OA') のライセンス数が余っていません。 |  

	: OperatorAgent のログイン失敗事由 {#tbl:oalogin}  

	※ 『ユーザID 誤り』、『パスワード誤り』 は **フォーム認証利用時のみ** のエラーとなります。  
	※ 『Communication Suite ユーザ未登録』 は **統合 Windows 認証利用時のみ** のエラーとなります。


#### 1-1-6. 本項のまとめ
- [ ] OperatorAgent でのログインに関わる設定項目について理解ができた。  
- [ ] OperatorAgent でのログインが単に認証しているだけでは無いことが理解できた。
- [ ] OperatorAgent の自動ログインについて理解ができた。  
- [ ] OperatorAgent にログインできないときに原因の切り分けができそうだ。

<div style="page-break-before:always"></div>

<hr/>

### 1-2. OperatorAgent のメイン画面
#### 1-2-1.OperatorAgent メニュー
OpertorAgentのメニュー画面について解説いたします、[@fig:mainblank] はメイン画面、[@fig:oa_header] はOpertorAgentのメニューです。  

![OperatorAgent メイン画面（起動直後）](images/2-1-operatoragentMain.png){#fig:mainblank width=600px}

![OperatorAgent メニュー](images/1-2-oa_header.png){#fig:oa_header width=600px  }

1. OperatorAgent バージョン確認  
  画面の左上の OperatorAgent ロゴを右クリックすると表示されるメニュー（[@fig:logoclick]）から OperatorAgent のバージョンを確認することができます。（[@fig:oaversion]）  

	![バージョンの確認方法](images/2-1-operatoragent_versionmenu.png){#fig:logoclick width=400px}  

	![バージョンの確認方法](images/2-1-operatoragent_version.png){#fig:oaversion width=400px}  

1. 通話リスト  
指定した検索条件に適合する SpeechVisualizer の通話詳細へのリンクをリストアップします。[@tbl:oa_conlist] は、通話リストに関連する ControlCenter の詳細設定項目です。  

	No. | 設定分類                 | 設定項目名       | デフォルト値 | 内容 |
	---:|---------------------|------------------|--------------|------|
	1   | OperatorAgent - 通話 | 検索条件 | mine:* d:1d | 今日の自分の通話 |
	2   | OperatorAgent - 通話 | 最大表示件数 | 20 | 上位 20 件まで |

	: OperatorAgent - 通話リストの設定 {#tbl:oa_conlist}  

	※ 検索条件の書式は SpeechVisualizer の通話検索条件と同じ書式が利用できます。  
	[@tbl:svshort] は、OperatorAgent から、SpeechVisualizer の機能にリンクするための設定項目です。

	No. | 設定分類| 設定項目名                | 設定内容      |
	----:|---------------------|------------------|--------------|
	1   |OperatorAgent - Web| SpeechVisualizer を表示するウェブブラウザ| SpeechVisualizer を利用するウェブブラウザの実行ファイルのパスを指定  
	2   | 共通 - システム | SpeechVisualizer の URL | OperatorAgent からは、この URL にアクセスします。  

	: OperatorAgent SpeechVisualizerを表示するブラウザ設定 {#tbl:svshort}  

1. マイクエリ  
SpeechVisualizer の通話検索機能で設定したマイクエリへのリンク（マイクエリの条件で検索した状態の検索画面へのリンク）をリストアップします。  

1. メッセージ  
チャット機能です。  

	![](images/Tips.jpg){width=50px}　 オペレータ同士のチャットは禁止し、座席表モニタ中の SV とのチャットのみ許可したい場合には、ロールに  **『OperatorAgent からのメッセージ送信』** 権限（[@fig:role_message]） を付与しないでください。その場合、OperatorAgent からユーザを検索・指定しての能動的なメッセージ送信ができません。  

	![メッセージ送信権限](images/1-2-role_message.png){#fig:role_message width=500px}  

	権限がある場合（[@fig:message_authok]）には、宛先入力欄でユーザ検索・指定してのメッセージ送信ができますが、権限が無い場合には宛先を指定できない（[@fig:message_authng]）ため、能動的なメッセージ送信ができません。  

	![メッセージ送信権限有り](images/2-1-message_authok.png){#fig:message_authok width=300px}  

	![メッセージ送信権限無し](images/2-1-message_authng.png){#fig:message_authng width=300px}  

	権限が無い場合でも、座席表モニタ中の SV からの受信メッセージに対する返信は可能です。（[@fig:operatoragent_messagewindow]）また、SV とのチャット履歴が残っている間（受信後24時間以内）であれば、メッセージ受信履歴からの宛先指定が可能です。（[@fig:message_authngrireki]）

	![受信メッセージへの返信](images/2-1-operatoragent_messagewindow.png){#fig:operatoragent_messagewindow width=400px}

	![メッセージ送受信履歴あり](images/2-1-message_authngrireki.png){#fig:message_authngrireki width=300px}  

	No. | 設定分類                 | 設定項目名       | デフォルト値 | 内容 |
	---:|:--------------------|------------------|--------------|------|
	1   | OperatorAgent - メッセージ | Enter キーでメッセージを送信 | true | false の場合には改行します |
	2   | OperatorAgent - メッセージ | ヘルプ対応時にメッセージウインドウを自動的に開く | true | SV がヘルプ対応操作を行ったことがメッセージとして通知されます |  

	: OperatorAgent - メッセージの詳細設定項目 {#tbl:oa_message_con}  


	![](images/Check.png){width=50px}　`メッセージの保存期間`  
	- メッセージは、通話中にも非通話時にも送受信が可能です。  
	- 通話中のメッセージ - 通話の属性情報として扱われます。通話データが削除されるタイミングで消去されます。
	- 非通話中のメッセージ - 単純チャット情報として扱われます。24時間後に消去されます。  

	<br />
	![](images/NOTICE.png){width=50px}　**通話中のメッセージも非通話中のメッセージも閲覧する機能はありません。**  

1. お知らせ  
ControlCenter のお知らせ管理で登録されたお知らせのリストです。  

	No. | 設定分類                 | 設定項目名       | デフォルト値 | 内容 |
	---:|:--------------------|:-----------------|------------:|:-----|
	1   | OperatorAgent - お知らせ | 更新間隔 | 3600 | 単位は秒 |
	2   | OperatorAgent - お知らせ | 最大表示件数 | 20 | 上位 20 件まで |

	: OperatorAgent - お知らせの詳細設定項目 {#tbl:oa_news_con}  

1. コンディション（感情メータ）  

	![オペレータコンディション](images/2-1-Condition.png){#fig:Condtiong width=300px}  

   	- 直近1時間分の通話のオペレータ感情の **ポジティブ・ネガティブ（nemesysco.qa5.excitement）**  の平均値をメータ表示しています。左に振れると "ネガティブ"、右に振れると "ポジティブ" という判断になります。[@tbl:oa_condition_con]  はコンディションに関連する ControlCenter の詳細設定項目です。

		No. | 設定分類                 | 設定項目名       | デフォルト値 | 内容 |
		---:|---------------------|------------------|--------------|------|
		1   | OperatorAgent - 感情解析 | コンディションの表示 | true | false で表示しない |
		2   | OperatorAgent - 感情解析 | コンディションのレッドゾーンの閾値 | 1.0 | 隠し項目 |
		3| 共通 - 感情解析  | 感情解析の使用  | true  |  false = 感情解析に関するあらゆる UI を表示しない |  

		: OperatorAgent - コンディションの詳細設定項目 {#tbl:oa_condition_con}  

1. ログインユーザプロファイル  
ログインユーザ名表示部分をクリックするとプロフィール機能が利用できます。  

	![ログイン情報](images/2-1-logininfo.png){#fig:logininfo width=300px}  

	- プロフィールタブ（[@fig:oa_profile]）  
ログイン情報の表示・画像の設定・削除・パスワード変更（関連する詳細設定項目は [@tbl:oa_pwchange_con]）が実施できます。  

		![プロフィール](images/2-1-profile.png){#fig:oa_profile width=300px}  

		No. | 設定分類                 | 設定項目名       | デフォルト値 | 内容 |
		---:|---------------------|------------------|--------------|------|
		1   | 共通  - セキュリティ | パスワードのポリシー | 未定義 | パスワードのフォーマット定義 |
		2   | 共通  - セキュリティ | パスワードの最小桁数 | 1 |  |

		: OperatorAgent - パスワード変更の詳細設定項目 {#tbl:oa_pwchange_con}  

	- 設定タブ（[@fig:oa_user_con]）  
ControlCenter の詳細設定で設定された OperatorAgent の振る舞いを個人用にカスタマイズできます。  
[@tbl:oa_user_con] は、表示項目と詳細設定項目の対応表です。

		![OperatorAgent ユーザ設定](images/2-1-config.png){#fig:oa_user_con width=300px}  

		No. | 設定タブ項目 | 設定分類                 | 設定項目名       |
		----:|---------------------|------------------|--------------|
		1   | 起動時にウィンドウを表示 | OperatorAgent - 起動時動作 | 起動時にウィンドウを表示状態に戻す |
		2   | 閉じたときにタスクバーに表示しない | OperatorAgent - 全般 | 閉じたときにタスクバーに表示しない |
		3   | 感情解析ポップアップを自動表示 | OperatorAgent - 通知メッセージ | 感情解析の自動表示 |
		4   | 通話フィルタの通知時間 | OperatorAgent - 通知メッセージ | 通話フィルタの通知時間レベル |
		5   | チャンネル名を含める | OperatorAgent - 通話全文コピー | コピー時にチャンネル名を含める |
		6   | 発話開始時間を含める | OperatorAgent - 通話全文コピー | コピー時に開始時間を含める |
		7   | 発話終端時間を含める | OperatorAgent - 通話全文コピー | 終了時間を含めるか |
		8   | Enter キーで送信 | OperatorAgent - メッセージ | Enter キーでメッセージを送信 |

		: OperatorAgent - ユーザ設定項目と詳細設定項目の対応 {#tbl:oa_user_con}  

<div style="page-break-before:always"></div>

<hr/>

#### 1-2-2. 通話表示機能

1. 通話内容ビュー  
OperatorAgent にログインした内線番号(モニタ内線番号)の通話の認識結果と関連する通話イベントを表示します。  

	- 通話イベント  
通話イベント（[@tbl:callevent]）は ControlCenter から OperatorAgent へ通知されます。  

		No. | イベント | 詳細 | 参考 |
		----:|---------|-------|---|
		1 | 通話開始 | RealTimeRecorder でモニタ内線番号の通話開始を検出時に通知されます。 | [@fig:startobi]  
		2 | 通話終了 | RealTimeRecorder でモニタ内線番号の通話終了を検出時に通知されます。 | [@fig:startobi]  
		3 | 保留開始 | RealTimeRecorder でモニタ内線番号の録音中に保留開始を検出時に通知されます。 | [@fig:holdobi]  
		4 | 保留解除 | RealTimeRecorder でモニタ内線番号の通話保留中、保留解除を検出時に通知されます。 | [@fig:holdobi]  
		5 | 保留終了 | RealTimeRecorder でモニタ内線番号の通話保留中に通話切断時に通知されます。 | [@fig:holdobi]  
		6 | 通話切替 | RealTimeRecorder でモニタ内線番号の録音中、録音対象の RTP の MediaResource が切り替わったときに通知されます。 | [@fig:kirikaeobi]  
		7 | 通話エラー | 通話録音がエラーになった場合に通知されます。 | [@fig:tuuwaerror]  
		8 | 保留エラー | 保留中に 『通話エラー』 が発生した場合に通知されます。 | [@fig:holdobi]  

		: 通話イベントの種類 {#tbl:callevent}

		![](images/Check.png){width=50px}　通話エラーの発生条件  

		- 通話中にパケットドロップ等により想定外に通話が終了となった場合 (呼制御を行っている TCP のパケットが欠落したり、RTP タイムアウトが発生したり 等)  
		- 通話中に未対応のパケットを受信したり、予想されないシーケンスの CTI イベントを受信したりし、それにより内部でエラーが発生した場合 (未知の状況が発生しても、ハンドリングできれば、単に無視されて通話エラーとはならない)  
		- 通話中に未対応のパケットを受信したり、予想されないシーケンスの CTI イベントを受信したりし、それにより通話の状態（このケースでは録音状態）が継続出来なくなり、通話の状態をリセットした場合  
		- 通話中に RealTimeRecorder が停止した (クラッシュも含む) 場合 (すぐには通話エラーにならない場合も多い。その場合は次の RealTimeRecorder を起動した時に通話エラーとなる)

		![通話イベント ： 通話開始 ＆ 通話終了](images/2-1-通話開始.png){#fig:startobi width=500px}

		![通話イベント ： 保留開始 ＆ 保留解除 ＆ 保留終了＆ 保留エラー](images/2-1-保留.png){#fig:holdobi width=500px}

		![通話イベント ： 通話切替](images/2-1-通話切替.png){#fig:kirikaeobi width=500px}  

		![通話イベント ： 通話エラー](images/2-1-通話エラー.png){#fig:tuuwaerror width=500px}  

	- 認識結果  
認識結果は StreamingRecognizer から OperatorAgent へ送信されます。  
通話内容は単語ごとにテキスト化され、順番に送信されますが、後から認識した単語によって既に表示されている単語が置き換わることもあります。発話単位で吹出で表現されます。発話の区切りは無音区間（セグメンタの音圧しきい値を下回った区間）が **0.5秒** 以上継続することで行われます。（[@fig:hatuwa]）  

		![認識結果の表示](images/2-1-通話内容.png){#fig:hatuwa width=500px}  

		- 緑の吹出は、録音対象の電話機を主体として、送話音声の認識結果になります。送話側音声は、認識オプション設定のオペレータタブに設定されたエンジンモードでテキスト化されます。（[@fig:txengine]）  

			![送話音声認識用エンジンモード](images/1-2-tx_engine.png){#fig:txengine width=400px}  

		- オレンジの吹出は、録音対象の電話機を主体として受話音声の認識結果となります。受話側音声は、認識オプション設定のカスタマタブに設定されたエンジンモードでテキスト化されます。（[@fig:rxengine]）  

			![受話音声認識用エンジンモード](images/1-2-rx_engine.png){#fig:rxengine width=400px}  

	- 通話内容ビューの表示不具合のトラブルシューティング  

  		1. 通話イベントが表示されない（**区分A**）  
このケースは通話録音設定の不備か、スパンデータの不備による可能性が疑われます。  

			No. | 原因| 対処 |
			----:|---------|-------|
			1 | RealTimeRecorder で通話録音ができていない | サーバ版であれば各種設定とパケットキャプチャの状況、クライアント版の場合には各種設定と録音デバイス関連を確認してください。  
			2 | サーバ版の場合 OperatorAgent でログインしている内線番号と通話中の内線番号が一致していない | OperatorAgent ログイン時に設定する内線番号と通話する電話機の内線番号は一致させてください。  
			3 | データベースの ServiceBroker が無効になっている | 有効化してください。  

			: 区分 A の主な原因と対処の目安 {#tbl:kubunA}

  		1. 通話イベントのみ表示され、認識結果が表示されない（**区分B**）  
このケースは通話録音・認識は正常に完了しているにも関わらず、**OperatorAgent と StreamingRecognizer 間の通信に不備がある** 可能性が疑われます。  
ただし、各種設定の不備が完全に否定されるわけではありません。

			No. | 原因| 対処 |
			-:|---------|------------|
			1 | OperatorAgent と StreamingRecognizer 間の接続が確立していない可能性があります。 | ノード管理で設定している、StreamingRecognizer の HTTP のポートに対して、OperatorAgent がアクセスできる状況にあるかを確認してください。  
			2 | 認識オプションが未設定の可能性があります| 認識オプションの設定を実施してください。  
			3 | 大規模な認識処理遅延が発生している可能性があります | 認識オプションの設定を実施してください。  

			: 区分 B の主な原因と対処の目安 {#tbl:kubunB}

  		1. その他（**区分C**）  
その他、よくある、通話内容表示不具合の例についてです。  

			No. | 症状 | 原因| 対処 |
			----:|---------|---|-------|
			1 | クライアント版（コンバージャー録音）で、通話していないのに 『通話開始』 と 『通話終了』 繰り返し表示される | コンバージャーの調整不足です | 恐らく無音がとれない電話機なので、有音 + 短い通話録音を切り捨てる設定にしてください  
			2 | クライアント版（コンバージャー録音）で、保留したタイミングで 『通話終了』 イベントが表示されてしまう | コンバージャー録音の性能限界の可能性があります | その時点のコンバージャー調整値では保留とオンフック状態の判別ができていません。調整によって解消する可能性もありますが、概ね IP  電話機の場合には保留とオンフックの判断はつかないようです。  
			3 | 認識結果の表示が遅延する（業務開始直後、オペレータのみ） | クライアント認識版では顕著に現れる症状ですが、StreamingRecognizer が初回認識処理時に認識オプションに沿って、各種設定やエンジンモードのロードを行うためです。 | 仕様であり、限定的にしか発生しませんので特に対処は必要はありません。気になるようであれば業務開始前にダミー通話を実施するようにしてください。  
			4 | 認識結果の表示が遅延する（通話開始直後） | 通話冒頭の 30 秒間は、通話環境の音響を学習しています。エンジンモードの音響モデルの情報と環境の音響情報の乖離が激しい場合、認識負荷があがるため冒頭30秒程度オペレータの認識結果の表示が遅延することがあります。 | 無線 ヘッドセットを利用しているケースなどで起きがちです。その場合、有線ヘッドセットに変えるなどで症状が改善します。  

			: 区分 C の主な症状及び原因と対処の目安 {#tbl:kubunC}

1. 通話情報ビュー  
通話相手によって変わらないオペレータ情報のみを表示します。（[@fig:callinfo]）  
ここに表示される通話属性は  
	- 自分の電話番号  
	- 自分のID  
	- CU識別名  
	- 相手の名前  

	になります。  

	![通話情報の画面](images/2-1-通話情報.png){#fig:callinfo width=250px}  

	No. | 表示情報 |説明                | 備考      |
	----:|---------------------|------------------|--------------|
	1   |自分の電話番号 | 通話属性 の `自番号 `から情報を表示します。 | `自番号 `が取得可能な環境であればデフォルト設定で表示されます。  
	2   |自分のID |通話属性の `自分の識別名 `から情報を表示します。| `自分の識別名`が取得可能な環境であればデフォルト設定で表示されます。

	: 通話情報ビューの詳細 {#tbl:callview}  


1. 通話相手ビュー  
この情報（[@fig:callpartner]）は通話相手ごとに作成され、通話状態や通話相手の情報を表示します。   

	![通話相手の画面 （左図：単体相手　右図：通話相手が変わった場合）](images/2-1-通話相手.png){#fig:callpartner width=500px}  

	通話情報ビュー、通話相手ビューで表示する通話属性は ControlCenter 詳細設定の [@tbl:callb] を編集して構成します。  

	No. | 設定タブ項目 | 設定項目名                | 設定内容      |
	----:|---------------------|------------------|--------------|
	1   |OperatorAgent - 通話 | 表示する通話属性の一覧 |[@tbl:callb2] の（通話属性識別名）＝（名称)で指定  

	: OperatorAgent 表示する通話属性の設定 {#tbl:callb}  


	表示する通話属性を追加する書式は以下です。複数追加する場合は、改行区切りで記述します。  

	```
	amivoice.common.operator.key=自分の識別名
	amivoice.common.operator.phonenumber=自番号
	amivoice.common.customer.phonenumber=相手番号
	amivoice.common.customer.gender=相手の性別
	```


	[@tbl:callb2] は、表示する通話属性で使用可能な通話属性の一覧です。  
	OAに 〇 が付いているものはデフォルトで OperatorAgent で表示される通話属性です。  
	補足：設定可否の説明　〇：優に設定可、●：自動設定されない環境で設定可、△：設定非推奨、×：設定不可

	No. | 通話属性識別名 | 名称                |検索条件<br>(SV) | 検索結果<br>(SV)  | 通話詳細<br>(SV)  | 通話印刷<br>(SV) | OA |座席表 |  Amazon Connect	      | Avaya AES    | Avaya PD   |Avaya    | CIC     | CTstage  |SV9500<br>OAI | SV9500<br>T-Server   |設定<br>可否|備考|
	---:|---------------------|------------------|--------------|--------------|--------------|--------------|--------------|--------------|--------------|--------------|--------------|--------------|--------------|------|----|----|---|---|
	1   |amivoice.common.description | 備考 |×  |  |  |  |  |  |  |  |  |  |  | |  |  | △ |用途未定  |
	2   |amivoice.common.direction | 向き |〇|〇|〇|〇|〇|〇|〇|〇|〇|〇|〇|〇|〇|〇|●|  |
	3   |amivoice.common.linetype | 通話回線種別 |  |〇|〇|〇|〇|〇|  |〇|〇|  |〇|〇|〇| 〇|● |  |
	4   |amivoice.common.summary| 要約 |×|  | 〇|  |  |  |  |  |  |  |  | |  |  |△| 用途未定|
	5   |amivoice.common.headline| 見出し |  |〇|  |  |  |  |  |  |  |  |  | |  |  |×|  |
	6   |amivoice.common.mark | マーク |  |〇|〇|〇|〇|〇|  |  |  |  |  | |  |  | ×|  |
	7   |amivoice.common.operator.key | 自分の識別名 |  |〇|〇| 〇|〇 |〇|  |  | 〇|〇|  |  |  |〇|●|エージェントID、オペレータIDの取得 |
	8   |amivoice.common.operator.name| 自分の名称 |  | 〇|〇|〇|  |〇|〇|  |〇|  |  | 〇 |  |  | ●|  |
	9   |amivoice.common.operator.phonenumber| 自番号 |〇|〇|〇|〇|〇|〇|〇|〇|〇|〇|〇|〇|〇|〇|●|  |
	10   |amivoice.common.operator.group| 自分の所属グループ |  |〇|〇|  |  |  |〇|  |  |  |  | |  |  | ●|  |
	11   |amivoice.common.operator.hostname | 自分のホスト名 |  |  |〇|  |  |  |  |  |  |  |  | 〇|  |  |  ●  |
	12   |amivoice.common.customer.key | 相手の識別名 |  |〇|〇|〇|  |  |  |  |  |  | 〇 |〇 |  |  |●  |内線相手を取得  |
	13   |amivoice.common.customer.name | 相手の名称 |  |〇|〇|〇|  |〇|  |  |  |  |  |〇|  |  |●|内線相手を取得  |
	14   |amivoice.common.customer.phonenumber| 相手番号|〇|〇|〇|〇|〇|〇|〇|〇|〇|〇|〇|〇|〇|〇|●|  |
	15   |amivoice.common.customer.gender | 相手の性別 |〇|〇|〇|〇|  |  |  |  |  |  |  | |  |  | ●|認識処理の性別識別を取得  |
	16  |amivoice.common.telephony.dialin.phonenumber | ダイヤルイン番号 |  |〇|〇|〇|  |  |  |  |  |  | 〇 |〇 | 〇|  |● |  |
	17   |amivoice.common.telephony.called.phonenumber | 掛先番号 | 〇 |〇| 〇| 〇|  |  |  | 〇 | 〇|  |  | |  |  | ● |  |
	18   |amivoice.common.telephony.alerting.phonenumber | 呼出先番号 |〇 |〇 | 〇|〇|  |  |  |〇 |  |  |  | |  |  | ●|  |
	19   |amivoice.common.telephony.trunk.group | トランクグループ |  |〇|〇 |  |  |  |  |〇 |  |  |〇|〇|〇|〇|●|  |
	20   |amivoice.common.telephony.trunk.member| トランクメンバ |  | 〇|〇 |  |  |  |  |〇 |〇|  |  |  |〇|  | ●|  |
	21   |amivoice.common.telephony.queue.phonenumber| キュー番号 |〇|〇|〇|〇|  |  |  | 〇|〇|  |〇|  |  |〇|●| スキルを取得 |
	22   |amivoice.common.telephony.transfer.source.key | 転送元識別名 |  |〇|〇|  |  |  |  |  |  |  |  |〇|  |  |●|転送元オペレータIDを取得  |
	23   |amivoice.common.telephony.transfer.source.name | 転送元名称 |  |〇|〇|  |  |  |  |  |  |  |  |〇|〇|  |●|転送元オペレータ名を取得|
	24   |amivoice.common.telephony.transfer.source.phonenumber | 転送元番号 |〇|〇|〇|  |  |  |  |〇|  |  |  |〇 |  |〇|●|  |
	25   |amivoice.common.telephony.transfer.destination.key| 転送先識別名 |  |〇|〇|  |  |  |  |  |  |  |  |〇|  |  | ●|転送先オペレータIDを取得  |
	26   |amivoice.common.telephony.transfer.destination.name | 転送先名称 |  |〇|〇|  |  |  |  |  |  |  |  |〇 |  |  | ● |転送先オペレータ名を取得|
	27   |amivoice.common.telephony.transfer.destination.phonenumber | 転送先番号 |〇|〇| 〇 |  |  |  |  |〇|  |  | |〇 |〇 |〇|● |  |
	28   |amivoice.common.telephony.monitoring.target.key | モニタリング対象識別名 |  |  | 〇|  |  |  |  |  |  |  |〇|  |  |  | ●|  |
	29   |amivoice.common.telephony.monitoring.target.name| モニタリング対象名称  |  |  | 〇|  |  |  |  |  |  |  |〇 |  |  |  |●|  |
	30   |amivoice.common.telephony.monitoring.target.phonenumber| モニタリング対象番号  |  |  | 〇|  |  |  |  |  |  |  |〇|  |  |  |●|  |
	31   |amivoice.common.telephony.monitoring.target.type | 	モニタリング種別 |  |  |〇|  |  |  |  |  |  |  |〇|  |  |  | ●|  |
	32   |amivoice.common.reference.global.id | グローバル参照用のID |  |  |〇|  |  |  |〇|〇|〇|  |〇|〇|  |〇|●|AvayaのUCID,CTstageのCallIDを取得|
	33   |amivoice.common.reference.global.url | グローバル参照用のURL |  |  |〇|  |  |  |  |  |  |  |  | |  |  |〇|  |
	34   |amivoice.common.reference.local.id| ローカル参照用のID |  |  |〇|  |  |  |  |  |  |  |〇|  |  |  | ● |Avaya CallIDを取得  |
	35   |amivoice.common.reference.local.url| ローカル参照用のURL |  |  |〇|  |  |  |  |  |  |  |  | |  |  |〇|  |
	36   |amivoice.common.reference.site.id | サイト参照用のID |  |  |〇|  |  |  |  |  |  |  |  | |  |  |〇|  |
	37   |amivoice.common.reference.site.url| サイト参照用のURL |  |  |〇|  |  |  |  |  |  |  |  | |  |  |〇|  |
	38   |amivoice.common.reference.private.id| プライベート参照用のID |  |  |〇|  |  |  |  |  |  |  |  | |  |  |〇|  |
	39   |amivoice.common.reference.private.url | プライベート参照用のURL |  |  |〇|  |  |  |  |  |  |  |  | |  |  |〇|  |
	40   |amivoice.common.recording.limit| 録音制限時間到達 |  |  |〇|  |  |  |  |  |  |  |  | |  |  |×|録音時間制限に到達した場合  |
	41   |amivoice.common.recording.split| 録音分割 |  |  |〇|  |  |  |  |  |  |  |  | |  |  |×|録音時間制限に到達し、通話分割された場合  |
	42   |amivoice.common.recording.split.previous| 録音分割された直前の通話 |  |  |〇|  |  |  |  |  |  |  |  | |  |  |×|録音時間制限に到達し、通話分割された場合 |
	43   |amivoice.common.reference.recording.id | 録音区間参照用のID |  |  |  |  |  |  |  |  |  |  |  | |  |  |  |  |
	44   |amivoice.common.reference.recording.url | 録音区間参照用のURL |  |  |  |  |  |  |  |  |  |  |  | |  |  |  |  |
	45   |amivoice.common.telephony.distributing.phonenumber| 受電グループ番号 |  |〇|〇|〇|  |  |  |〇|  |  |  | |  |  |●|Avaya AESのみ取得可  |
	46   |amivoice.common.telephony.ivr.duration| IVR 応対時間 |  |  |〇|  |  |  |  | 〇 |  |  |  | |  |  |●| Avaya AESのみ取得可 |
	47   |amivoice.common.telephony.queue.duration | 待ち時間 |  |〇|〇|〇|  |  |  |〇|  |  |  | |  |  |●|Avaya AESのみ取得可  |

	: 利用可能な通話属性一覧 {#tbl:callb2}  

	![](images/Check.png){width=50px}　相手番号や掛先番号の通話属性は IN （着信）と OUT （発信） で表示される内容が変わるケースがあります。相手番号の例として ACD（着信個自動分配装置）を利用している環境では、着信時に別の番号を経由してから内線番号に着信するため、相手番号の通話属性としてはACDのVDNが表示されます。（CTI連携で回避可能なケースもあります） OUT（発信）の場合は実際に掛けた番号が相手番号に入ります。  
<br>
1. 性別識別  
	性別識別の判定方法は録音対象の電話機を主体として、送話と受話で異なります。  

	- 送話側  
	ControlCenter / システム管理 / ユーザ管理 - 詳細 の性別（ [@fig:usrprofile]） から判定しています。  

	![ユーザ管理 - 詳細](images/2-1-ユーザ管理.png){#fig:usrprofile width=350px}  

	- 受話側  
	性別識別用エンジンを利用して判定しています。  
	受話側の性別識別エンジンの設定項目は ControlCenter / 認識管理 / 認識オプションの設定（[@tbl:seibetuenjin]）を編集して構成します。  

		No. | 設定タブ項目 | 設定項目名                | 内容      |
		----:|---------------------|------------------|--------------|
		1   |カスタマタブ | 性別識別 | 性別識別を利用するかどうか   
		2   |カスタマタブ | 性別識別用エンジンモード | 性別識別用エンジンを登録
		3   |カスタマタブ | 性別識別の閾値| 性別識別の判定に使用する閾値   
		4   |カスタマタブ | 性別識別に使用する発話時間（最大） | 性別識別の判定に使用する発話時間の最大値
		5   |カスタマタブ | 性別識別に使用する発話時間（最小） | 性別識別の判定に使用する発話時間の最小値

		: 性別識別用エンジン設定 {#tbl:seibetuenjin}  

1. 通話状態ビュー  
通話状態にあわせて表示が変化します。（ [@fig:callstate]）  
	- 電話アイコン・・・通話開始前・通話開始 / 通話終了・保留中でアイコン表示変わります。
	- 通話時間・・・RealTimeRecoder の録音開始 / 終了を基準として Operator Agent 上 の PC 時刻をもとに時間を表示します。

	![通話状態](images/2-1-通話状態.png){#fig:callstate width=250px}  

1. 通話フィルタビュー（[@fig:callfilter1]） と 通話フィルタの通知メッセージ（[@fig:callfilter2]）  

	![OperatorAgent 上の通話フィルタビュー](images/2-1-通話フィルタ1.png){#fig:callfilter1 width=250px}  

	![通話フィルタの通知メッセージ](images/2-1-通話フィルタ2.png){#fig:callfilter2 width=250px}  

	通話フィルタ関関連の詳細設定項目は [@tbl:callfilter] を参照してください。  

	No. | 設定タブ項目 | 設定項目名                | 内容      |
	----:|---------------------|------------------|--------------|
	1   |OperatorAgent - コマンド実行 |通話フィルタの検出時に実行するコマンド|（[@tbl:oacommand]）を参照
	2   |OperatorAgent - コマンド実行 |通話フィルタの手動コマンド実行後に実行するコマンド|（[@tbl:oacommand]）を参照
	3   |OperatorAgent - 通知メッセージ |通話フィルタの通知時間の倍率 (短め) | No.5の通話フィルタの通知時間に対して通話時間レベルの「短め」とする時間を倍率で指定します。<br> 例） 設定値が0.5の場合はNo.5の通話フィルタの表示時間の0.5倍の時間で表示します。
	4   |OperatorAgent - 通知メッセージ | 通話フィルタの通知時間の倍率 (長め)|No.5の通話フィルタの通知時間に対して通話時間レベルの「長め」とする時間を倍率で指定します。<br> 例）設定値が1.5の場合はNo.5の通話フィルタの表示時間の1.5倍の時間で表示します。
	5   |OperatorAgent - 通知メッセージ | 通話フィルタの通知時間レベル| No.5の通話フィルタの表示時間を「0（普通）」とした場合に「-1（短め）」に表示するか「1（長め）」に表示するかを指定  
	6   |OperatorAgent - 通知メッセージ | 通話フィルタの表示時間|通話フィルタ検出時に通知メッセージを表示する時間（秒）  
	7   |OperatorAgent - 通知メッセージ | 一度に通知する通話フィルタの対象発話数| 通話中にOperatorAgentを起動すると、それまでに発話された通話内容がすべて表示されるため、その際に検出済みの通話フィルタ数を制限する機能。「-1」を指定した場合、通話内でそれまで検知した全ての通話フィルタの通知メッセージを表示  
	8   |共通 - 通話フィルタインポート | 通話フィルタインポートリクエストタイムアウト| 大量の通話フィルタをインポートした際に処理の途中でタイムアウトが発生してインポートが失敗するケースがあり、タイムアウト期間を延ばすことで処理が最後まで継続することを目的とした機能。タイムアウト期間を延ばすことで、大量の通話フィルタをインポートすることが可能ですが、インポート処理中はDBの負荷が高くなり、リアルタイム機能のレスポンスに影響が発生する可能性があります。

	: OperatorAgent 通話フィルタの設定 {#tbl:callfilter}  

	- 通話フィルタの適用タイミングは、通話フィルタの設定状況によります。（ [@fig:callfilter3] ）  

		- 発話中・・・認識結果の確定前のタイミングで適用されます。  
確定前なので、最終的な認識結果には、検出したキーワードが採用されない可能性もあります。  
ただし、リアルタイム性には優れています。  
		- 発話終了時・・・認識結果の確定後のタイミングで適用されます。  
検出したキーワードが、認識結果に採用されることが保証されます。  
ただし、確定タイミング次第では通知タイミングが会話のテンポより遅延する可能性もあり、必要なタイミングで通知されない（通知が遅い）という使い勝手の悪さが生じる可能性もあります。  

	![通話フィルタ適用タイミングの設定](images/2-1-通話フィルタ3.png){#fig:callfilter3 width=500px}  

	![](images/Tips.jpg){width=50px}　通話フィルタのコマンドからは、オプション変数を利用した構文が便利です。  
	オプション変数の詳細は [1-5. OperatorAgent からのコマンド実行](#1-5-operatoragent-からのコマンド実行) を参照してください。  
	通話フィルタの実行コマンドから有効なメインキーについては、[@tbl:filtermainkey] を参照してください。  

	通話情報<br />（call） | 通話フィルタ情報<br />（filterinfo） | 検出通話フィルタ情報<br />（filterdetection） | 実行コマンド情報<br />（executedcommand） | OperatorAgent 情報<br />（oa） |
	|:-:|:---:|:----:|:---:|:-------:|
	○ | ○ | ○ | × | △ |
	: 通話フィルタから指定可能なオプション変数のメインキー {#tbl:filtermainkey}

	- 通話フィルタに関するトラブルシューティング  
通話フィルタが想定したように動作しない場合、[@tbl:filtertrouble] を参考にシューティングしてください。  

		No. | 症状 | 原因 | 対処 |
		-:|-------|-----|-----|
		1 | キーワードがテキスト化されているのに通話フィルタが検出されない | 設定ミスの可能性 | 通話フィルタの検出トリガーのうち、キーワード以外の設定項目を確認してください。<br />特に、『検出対象回線種別』 を正確に取得できない環境では、"不明" の指定が必須となります。  
		2 | キーワードがテキスト化されていないのに通話フィルタが検出されている | 設定による仕様 | 音声認識処理の仕様となりますが、一度テキスト化された文字列が後からテキスト化された文字列によって置換される場合があるためです。<br />回避するには、通話フィルタ設定項目の 『適用タイミング』 を "発話終了時" に設定してください。（検出タイミングが遅延するリスクがあります。）  
		3 | 通話フィルタは検出されているが、通知されない | 設定による仕様 | 通話フィルタの設定項目の 『通知』 の設定内容を確認してください。  
		4 | 通話フィルタの通知はされるが、指定したコマンドが実行されない | コマンドの設定ミスの可能性 | 該当 PC の 「ファイル名を指定して実行」 から登録したコマンドが実行できるか確認してください。できない場合には、なんらかの対処が必要です。  

		: 通話フィルタのトラブルシューティング {#tbl:filtertrouble}

1. ヘルプ  

	![ヘルプボタン](images/2-1-ヘルプ.png){#fig:helpb width=200px}  

	ヘルプ要求 / ヘルプ解除理由管理に関する ControlCenter の詳細設定項目は[@tbl:help]を編集して構成します。

	No. | 設定分類| 設定項目名                | 内容      |
	----:|---------------------|------------------|--------------|
	1   |OperatorAgent - メッセージ | ヘルプ対応時にメッセージウインドウを自動的に開く | ヘルプ応答時にメッセージウインドウを自動的に開くかどうか   
	2   |OperatorAgent - 通知メッセージ | ヘルプの解除理由選択の表示時間|ヘルプ要求の自動解除後にヘルプ解除理由を表示する時間    
	3   |OperatorAgent - 通知メッセージ | ヘルプを案内する感情解析の通話重要度の閾値 |感情解析のポップアップ画面にヘルプボタンを表示する通話重要度の閾値  
	4   |OperatorAgent - 通知メッセージ  |ヘルプ中のクローズ |ヘルプ中の通知メッセージをユーザがクローズできるかどうか
	5   |OperatorAgent - 通知メッセージ  |ヘルプ中の表示 | ヘルプ要求時の通知メッセージを表示するかどうか
	6   |OperatorAgent - 通話  |通話開始時にヘルプを解除する |通話開始時にヘルプ要求中だった場合、自動で解除するかどうか
	7   |OperatorAgent - 通話  |通話終了時にヘルプを解除する |通話終了時にヘルプ要求中だった場合、解除するかどうか  

	: OperatorAgent ヘルプ設定 {#tbl:help}  


	`利用上の注意`  
	ヘルプボタン（[@fig:helpb]）を利用するには、ヘルプ要求 / ヘルプ解除理由の登録が必要です。  
	ヘルプ要求理由管理が登録されていない場合には OperatorAgent の画面にヘルプボタンは表示されません。  

	<br />

	![](images/Tips.jpg){width=50px}　ヘルプ要求後のヘルプ解除は ControlCenter の設定で特定条件で自動終了することができます。  
	- 通話前にヘルプ要求を実施、通話を開始した場合にヘルプ要求を自動解除
	- 通話中にヘルプ要求を実施、通話終了後にヘルプ要求を自動解除

	<br />



1. 感情解析  
送話と受話側の発話内容をリアルタイムで感情に数値化して表示します。  
音声データをもとに感情解析を行っており、テキストデータを解析対象としていません。  
<br>

	- OperatorAgent の感情解析機能の一覧です。([@fig:emo0]) ([@fig:emo1])([@fig:emo２])([@fig:emo3])  

		![オペレータのコンディション](images/2-1-感情バロメーター.png){#fig:emo0 width=150px}

		![発話に紐づく感情](images/2-1-通話感情.png){#fig:emo1 width=450px}

		![感情解析ポップアップ画面](images/2-1-感情解析.png){#fig:emo２ width=250px}

		![感情解析のサマリ画面](images/2-1-感情解析2.png){#fig:emo3 width=350px}  


		([@fig:emo1])([@fig:emo２])([@fig:emo3])  は ControlCenter 詳細設定の[@tbl:emopop] を編集して構成します。  
		([@fig:emo0]) の設定については[1-2. OperatorAgent のメイン画面]の 6. コンディション（感情メータ）を参照。


		No. | 設定分類| 設定項目名                | 設定内容      |
		----:|---------------------|------------------|--------------|
		1   |OperatorAgent - 感情解析| 表示する感情（オペレータ）| 感情解析識別名 \| label＝感情名 で指定  
		2   |OperatorAgent - 感情解析| 表示する感情（カスタマ） | 感情解析識別名 \| label＝感情名 で指定 |  

		: OperatorAgent の表示する感情設定 {#tbl:emopop}  

		例）怒りの感情を設定する。複数ある場合は改行区切りで登録。

		```
		nemesysco.qa5.angry|label=怒り
		```



		![](images/Check.png){width=50px}　 「表示する感情」を変更する場合には詳細設定の 「保存する感情スコア」 の設定変更も必要です。  
		**「保存する感情スコア」に設定されていないものは感情値が取得できず、対象感情が表示されません。**  

		保存する感情スコアは ControlCenter の詳細設定項目は[@tbl:emoscore] を編集して構成します。  

		No. | 設定分類| 設定項目名                | 設定内容      |
		----:|---------------------|------------------|--------------|
		1   |共通 - 感情解析| 保存する感情スコア| （感情解析識別名）.（話者)で指定<br>話者：op = オペレータ cu = カスタマ

		: 保存する感情スコア {#tbl:emoscore}  

		例）オペレータ側は快適、カスタマ側は怒りの感情を設定する。複数ある場合は改行区切りで登録。

		```
		nemesysco.qa5.hesitation.comfort.op
		nemesysco.qa5.angry.cu
		```

		![](images/Check.png){width=50px}　**「保存する感情スコア」はデータベースのパフォーマンスの観点から、オペレータ、カスタマを含めて８つまでの感情に抑えて設計してください。**  「保存する感情スコア」に設定した感情のみデータベース内に感情のサマリ値（最小/平均/最大/開始/終了）を保存します。  発話単位の感情値は「保存する感情スコア」の設定に関係なく、すべての感情を取得しており Emotion ファイルに保存されています。  

		<br />

		「表示する感情」と「保存する感情スコア」で利用可能な感情一覧は[@tbl:emolist] の通りです。  

		No. | 感情解析識別名| 感情名                | 複合型| 説明 |
		----:|---------------------|------------------|----------|---------|
		1   |nemesysco.qa5.angry      |怒り         |  |どのくらい怒っているかを示す値      |
		2   |nemesysco.qa5.concentration     |集中         |  |どのくらい集中しているかを示す値      |
		3   |nemesysco.qa5.embarrassment      |不快         |  |どのくらい不快に感じているかを示す値      |
		4   |nemesysco.qa5.excitement      |ポジティブ・ネガティブ |〇  |値が小さいい場合はネガティブ　値が大きい場合はポジティブを示す値      |
		5   |nemesysco.qa5.excitement.positive      |ポジティブ         |  |どのくらいポジティブかを示す値      |
		6   |nemesysco.qa5.excitement.negative      |ネガティブ         |  |どのくらいネガティブかを示す値      |
		7   |nemesysco.qa5.hesitation      |後悔・快適         |〇  |値が小さい場合は快適　値が大きい場合は後悔を示す値      |
		8   |nemesysco.qa5.hesitation.regret      |後悔         |  |どのくらい後悔していると感じているかを分析した値      |
		9   |nemesysco.qa5.hesitation.comfort      |快適         |  |どのくらい快適と感じているかを分析した値      |
		10   |nemesysco.qa5.imaginationactivity      |イメージ         |  |記憶や映像化された何かから記憶を思い出している事を示す値      |
		11   |nemesysco.qa5.intensivethinking      |思考         |  |集中して考えていることを示す値      |
		12   |nemesysco.qa5.content      |喜び         |  |どのくらい嬉しいかを示す値      |
		13   |nemesysco.qa5.savorarousalfactor      |興味         |  |会話に対する深い関心、覚醒要因を示す値      |
		14   |nemesysco.qa5.upset      |悲しみ         |  |どのくらい悲しいかを示す値      |
		15   |nemesysco.qa5.extremestate      |感情変化の極端さ         |  |感情活動が全体的にどのくらい極端かを示す値      |
		16   |nemesysco.qa5.stress      |恐怖         |  |どのくらい神経質になっているかを示す（ストレスを感じているか） 参考値：1～14 緊張・神経質 15以上 恐怖      |
		17   |nemesysco.qa5.uncertainty      | 確信無し・有り        |〇  |値が小さい場合は確信　値が大きい場合は不確かな発言として示す値 参考値：15未満 確信 15以上 不安・不確か |
		18   |nemesysco.qa5.uncertainty.uncertainty      |確信無し         |  |どのくらい不確かな発言かを示す値 |
		19   |nemesysco.qa5.uncertainty.certainty      |確信有り         |  |どのくらい確信がある発言かを示す値|
		20   |nemesysco.qa5.energy      |エネルギッシュ・疲労         |〇  |値が小さい場合は疲労　値が大きい場合は精力的であるかを示す値 参考値：1 飽きている・疲労　4未満 退屈・疲労　5～9 通常　10以上 精力的       |
		21   |nemesysco.qa5.energy.energetic      |エネルギッシュ         |  |どのくらい精力的かを示す値     |
		22  |nemesysco.qa5.energy.tired      |疲労         |  |どのくらい疲労しているかを示す値      |
		23   |nemesysco.qa5.brainpower      |脳活動のサマリ         |  |脳の感情的・論理的プロセスの全体的な概要。主に研究目的で使用される。      |
		24   |nemesysco.qa5.emotionalcognitiveratio      |感情的・論理的         |〇  |話題について感情的・論理的のどちらに基づいて話をしているかの全体的な概要。値が小さい場合は論理的、大きい場合は感情的を示す。      |
		25   |nemesysco.qa5.emotionalcognitiveratio.emotional      |感情的         |  |感情的に話をしているかを示す値      |
		26   |nemesysco.qa5.emotionalcognitiveratio.cognitive      |論理的         |  |論理的に話をしているかを示す値      |
		27   |nemesysco.qa5.amplitude      |思考深さ         |  |音量を示している値（利用実績なしのため、実用性不明）      |
		28  |nemesysco.qa5.voiceenergy      |音のエネルギー         |  |音の強さ（Energy）を示す値      |
		29   |nemesysco.qa5.voicevolume      |ボリューム         |  |「音のエネルギー」とは別の計算方法で算出した音の強さ(Volume)を示す値      |
		30   |nemesysco.qa5.anticipation      |期待         |  |期待・興味を示す値      |
		31   |nemesysco.qa5.dissatisfaction      |不満         |  |不満かどうかを示す値      |
		32   |nemesysco.qa5.callpriority      |通話重要度         |  |通話の中で重要と思われる箇所を複数の感情から算出して値を示す      |
		33   |nemesysco.qa5.agentscore      |エージェントスコア         |  |関連するいくつかの感情の要約を示す。値が大きいほど、変化の度合いが激しいことを示す。      |
		34  |nemesysco.qa5.emotionlevel      |感情レベル         |  |利用用途については検討中      |
		35   |nemesysco.qa5.logicallevel      |倫理的レベル         |  |利用用途については検討中      |
		36   |nemesysco.qa5.hesitantlevel      |困惑レベル         |  |利用用途については検討中      |
		37   |nemesysco.qa5.stresslevel      |緊張レベル         |  |利用用途については検討中      |
		38   |nemesysco.qa5.energeticlevel      |活動レベル         |  |利用用途については検討中      |
		39   |nemesysco.qa5.thinkinglevel      |思考レベル         |  |利用用途については検討中      |
		40  |nemesysco.qa5.passionlevel      |情熱レベル         |  |利用用途については検討中      |
		41   |nemesysco.qa5.concentrationlevel      |集中レベル         |  |利用用途については検討中      |
		42   |nemesysco.qa5.shylevel      |疑いレベル         |  |利用用途については検討中      |
		43   |nemesysco.qa5.anticipationlevel      |期待レベル         |  |利用用途については検討中      |

		: 利用可能な感情一覧 {#tbl:emolist}

	- 感情解析の通知  
	感情解析の通知に関する設定は ControlCenter の詳細設定項目の[@tbl:emotuuchi] を編集して構成します。  

		No. | 設定分類| 設定項目名                | 設定内容      |
		----:|---------------------|------------------|--------------|
		1   |OperatorAgent - 通知メッセージ|ヘルプを案内する感情解析の通話重要度の閾値|設定した通話重要度の値を検知した際に感情解析ポップアップ画面にヘルプボタンを表示
		2   |OperatorAgent - 通知メッセージ|感情解析の自動表示|感情解析ポップアップ画面の表示可否を指定
		3   |OperatorAgent - 通知メッセージ|通話終了後の感情解析の表示時間|通話終了後、感情解析ポップアップ画面を表示する時間を指定|

		: OperatorAgent - 通知メッセージ設定 {#tbl:emotuuchi}  

#### 1-2-3. 通話終了後の機能

1. SpeechVisualizer ボタン（[@fig:opsv]）  
OperatorAgent 上で表示されている通話の SpeechVisualizer の通話詳細画面を呼び出します。  
ボタンは、通話開始前や通話中は非活性状態にあり、操作できません。  
該当通話の認識結果のアップロードが、StreamingRecognizer から ControlCenter に対して完了すると、その旨が ControlCenter から OperatorAgent に通知されることにより活性化します。（認識エラーとなった通話や、アップロードに失敗した通話の場合には活性化しません。）

 	![SpeechVisualizer ボタン](images/2-1-opsv.png){#fig:opsv width=100px}  

2. 通話終了後に通話属性を設定する  
通話終了後に通話に紐づく通話属性を追加することができる機能です。  
通話終了後、[@fig:callp2] がポップアップ表示されて通話属性を登録することが可能です。通話リストからも登録できます。  

	![手動通話属性の入力画面](images/2-1-通話属性ポップアップ画面2.png){#fig:callp2 width=450px}  

	手動で通話属性を追加するための ControlCenter の詳細設定項目は、@tbl:tuuwazokusei を編集して構成します。

	No. | 設定分類| 設定項目名                | 設定内容      |
	----:|---------------------|------------------|--------------|
	1   |OperatorAgent - 通話| 通話終了後に手動で通話属性を設定可能にする|True で手動通話属性の設定可能  
	2  |共通 - 通話| 手動で設定可能な通話属性|手動で設定可能な通話属性を指定  

	: 手動で追加する通話属性の設定 {#tbl:tuuwazokusei}

	例） OperatorAgent から手動で登録可能な通話属性として通話属性の「サイト参照用のID」 を指定する。

	```
	amivoice.common.reference.site.id
	```

	追加可能な通話属性は（[1-2-2. [@tbl:callb2]: 利用可能な通話属性一覧](#1-2-2. 通話表示機能) 参照。）  

### 1-3. OperatorAgent と ControlCenter の通信  
ControlCenter と OperatorAgent は、2種類の通信経路で接続されています。  

1. ログイン（状態）を管理する通信経路  
ControlCenter は、 ログイン中の OperatorAgent が通信可能な状態にあるかを、OperatorAgent からのリクエストの有無で判断しています。  
ヘルプ通知やメッセージ送信など機能によるリクエストが発生しない場合、OperatorAgent は、[@tbl:oaping] の 『ログイン維持の通知間隔』 毎に Ping のようなリクエストを ControlCenter に送信します。  
その Ping リクエスト を受信することで、ControlCenter はログイン中の OperatorAgent の死活監視を行っています。  
	- OperatorAgent のログインタイムアウト  
ControlCenter はログイン中の OperatorAgent から、[@tbl:oaping] の 『ログイン状況タイムアウト』 の設定値を超えて新しいリクエストがない場合には、該当の OperatorAgent を `ログインタイムアウト` の状態として管理します。  
各 OperatorAgent が ControlCenter からどのように見えているのかは、ControlCenter のモニタリングメニューの 『ログイン状況』 機能で確認できます。  
SpeechVisualizer の座席表機能では、タイムアウトした OperatorAgent の座席にはタイムアウトアイコンが表示されます。([@fig:ismto])  

		![](images/Check.png){width=50px}　この状態は、該当座席に対して新たな OperatorAgent がログインすることで解消されます。それまではタイムアウト済みの OperatorAgent からのレジスト情報が表示され続けます。  

		![座席表でのタイムアウト表示](images/1-2-ism_to.png){#fig:ismto width=250px}  

1. 状態通知のための通信経路  
都度リクエストが発生するログイン管理の通信経路とは別に、ControlCenter から OperatorAgent へ各種イベント（[@tbl:callevent] など）を通知するための通信経路が存在します。  
OperatorAgent から ControlCenter へのリクエストとはなりますが、ControlCenter から OperatorAgent に通知するべきイベントが発生する毎に、ControlCenter から非同期にレスポンスされる通信（HTTP Comet）となります。  
ControlCenter からは特に通知すべきイベントが無い場合でも、[@tbl:callevent] の 『データ送信最長間隔』 毎に接続の維持のためのレスポンスが行われます。  
	- 状態通知通信の受信タイムアウト  
OperatorAgent では、[@tbl:callevent] の 『受信タイムアウト』 以上、状態通知のレスポンスが無い場合、状態通知通信の接続に問題が発生（接続が切断）したと判断し、既存の接続を破棄して再接続処理を行います。  
再接続に失敗した場合には、[@tbl:callevent] の 『再接続間隔』 毎に再接続処理が繰り返されます。  
		![](images/Check.png){width=50px}　ControlCenter との接続断を通知した場合、OperatorAgent は 通知ポップアップ にてその旨をユーザに通知しますが、通知ポップアップは、接続断だと判断された瞬間には通知されず、その直後の再接続処理に失敗したタイミングで通知されます。

	No. | 設定分類 | 設定項目名                | デフォルト値  | 特記 |
	----:|----------|--------|------|----|
	1   | OperatorAgent - 状態通知 | データ送信最長間隔 | 90000（ミリ秒） |   
	2   | OperatorAgent - 状態通知 | 再接続間隔 | 60000（ミリ秒） |   
	3   | OperatorAgent - 状態通知 | 受信タイムアウト | 120000（ミリ秒） |   
	4   | 共通 - セキュリティ | ログイン維持の通知間隔 | 180       |   
	5   | 共通 - セキュリティ | ログイン状況タイムアウト | 600        |   

	: ControlCenter と OperatorAgent の通信 {#tbl:oaping}

	![](images/NOTICE.png){width=50px}　上記の仕様により、[@tbl:callevent] の設定値を変更する場合には、  
	- 『ログイン状況タイムアウト』 > 『ログイン維持の通知間隔』  
	- 『受信タイムアウト』 > 『データ送信最長間隔』  

	が成り立つように配慮する必要があります。（極力変更しないようにしてください。）  


### 1-4. OperatorAgent の起動・終了時の動作  

1. OperatorAgent 起動時の処理  
	- OperatorAgent の自動更新処理  
OperatorAgent を起動すると、ログインダイアログが表示される前に自身のバージョンとサーバ側のバージョンの比較を行います。  
	- OperatorAgent のバージョンがサーバのバージョンより古い場合には、自動的に更新処理が行われ OperatorAgent がサーバ側のバージョンに合わせてバージョンアップします。この更新処理はメジャーバージョンアップ時を除き、正常なバージョンアップが機能として保証されています。  
	- OperatorAgent のバージョンがサーバのバージョンより新しい場合も同様に自動的に更新処理が行われ、 OperatorAgent がサーバ側のバージョンに合わせてバージョンダウンします。  
ただし、この更新処理は OperatorAgent の更新内容等によっては、正常なバージョンダウンが保証されない場合があります。（その場合には、一度 OperatorAgent をアンインストールして、古いバージョンの OperatorAgent を新規インストールしてください。）  
自動バージョンダウン処理がサポートされるかどうかは、バージョンアップの内容次第です。切り戻し時の作業内容を検討する際には、リリースノートを確認するか、サポートへお問合せください。  

		<br />

		![](images/NOTICE.png){width=50px} 　自動更新では処理中に **Windows Script Host （WSH）** の vbs がいくつか実行されます。（[@tbl:vbslist]）  
		セキュリティソフトによって、WSH の実行が阻害されてしまう環境では、自動更新処理が正常に行われません。（インストーラによるインストールでもバージョンアップインストールでも、WSH は実行されます。）  

		No. | ファイル名 | 説明  |
		----|---------------------|------------------|
		1   | moduleindexbuilder.vbs | バージョン毎にファイルのハッシュ値が**必ず変更になります**。 |
		2   | @301_RR_CTILink_RegAsm.vbs | バージョン毎にファイルのハッシュ値の変更はありませんが将来のバージョンで削除となる可能性はあります。 |
		3   | @341_RR_RemoveFiles.vbs | バージョン毎にファイルのハッシュ値の変更はありませんが将来のバージョンで削除となる可能性はあります。 |
		4   | @341_SR_RemoveFiles.vbs | バージョン毎にファイルのハッシュ値の変更はありませんが将来のバージョンで削除となる可能性はあります。 |
		5   | @352_SR_Web_RemoveFiles.vbs | バージョン毎にファイルのハッシュ値の変更はありませんが将来のバージョンで削除となる可能性はあります。 |
		6   | @Updater.vbs | ファイルが更新されていればハッシュ値も変更になります。 |

		: OperatorAgent のアップデート時に実行される vbs のリスト {#tbl:vbslist}  

		※ **\@数字_モジュール_処理名.vbs** のファイルは、特定の処理を行う (不要になったファイルの削除や、不具合修正のための処理とか) 為にあるので、以降のバージョンで追加になる可能性があります。  

		<br/>  

		![](images/Tips.jpg){width=50px}　OperatorAgent をコマンドラインから引数付きで起動することで自動更新を抑制できます。（[1-6. コマンドラインからの OperatorAgent 操作](#1-6. コマンドラインからの OperatorAgent 操作) 参照。）  

		<br/>

	- ライセンス引当  
OperatorAgent がインストールされた PC 毎にライセンスの引当が行われます。引当のタイミングは、該当の PC で、  
ログイン処理を実施したタイミングです。  
通常は、PC 毎に1回実施されますが、VDI オプション または RDS オプション指定時には、ログイン処理毎に行われます。
	- メインウィンドウの表示について  
メインウィンドウの表示は、 [@tbl:oa_window] の項目の設定値を判断して行われます。  
		- 初回起動  
			1. `C:\Users\%UserName%\AppData\Local\Advanced_Media,_Inc` に設定ファイルが無ければ、初回起動時として動作します。  
			2. 『初回起動時にウィンドウを表示状態にする』 の設定値を判断し、ウィンドウ表示を制御します。  
		- 通常起動  
			1. `C:\Users\%UserName%\AppData\Local\Advanced_Media,_Inc` に設定ファイルが有れば、通常起動として動作します。  
			2. 『起動時にウィンドウを表示状態に戻す』 の設定値を判断し、ウィンドウ表示を制御します。  
			3. 表示しない設定の場合、『閉じたときにタスクバーに表示しない』 の設定値を判断し、タスクバー or 通知領域に情報を表示します。  

		No. | 設定分類| 設定項目名                | デフォルト値  | 内容 |
		----:|---------------------|------------------|------|----|
		1   | OperatorAgent - 起動時動作 | 起動時にウィンドウを表示状態に戻す | true | OperatorAgent 起動毎に、終了時のウィンドウ状態に依存せずメインウィンドウを画面表示状態に戻します。false の場合には、OperatorAgent の終了時の状態を引き継ぎます。
		2   | OperatorAgent - 起動時動作 | 初回起動時にウィンドウを表示状態にする | true | 初回起動時の メインウィンドウの表示状態を設定します。オペレータさんに基本的に画面を一度も見せたくない場合などに false 設定しておきます。  
		3   | OperatorAgent - 全般 | 閉じたときにタスクバーに表示しない | False | true にするとメインウィンドウの　× ボタンでウィンドウを閉じたときに、通知領域にのみアイコンが表示されます。  

		: OperatorAgent のウィンドウ表示に関わる詳細設定項目 {#tbl:oa_window}  


		```plantuml
		@startuml

		skinparam {
			shadowing false
			defaultFontName "Segoe UI, BIZ UDPゴシック, sans-serif"
			BackgroundColor #afeeee
			ArrowColor black
		}

		skinparam activity  {
			BorderColor #000000
			DiamondBorderColor #008000
			BackgroundColor #ffffff
		}

		title アクティビティ図.2 [OA ウィンドウ表示判定]\n

		start;
		-[#black]-> OperatorAgent 起動;
		if (設定ファイルあり) then
		  -[#blue]-> True : 通常起動;
			if (\n起動時に\nウィンドウを表示状態に戻す\n) then
				-[#blue]-> \nTrue;
				:OperatorAgent ウィンドウ表示;
				end;
			else
				-[#red]-> \nFalse;
			endif
		else
			-[#red]-> \nFalse : 初回起動処理;
				if (\n初回起動時に\nウィンドウを表示状態にする\n) then
					-[#blue]-> \nTrue;
					:OperatorAgent ウィンドウ表示;
					end;
				else
					-[#red]-> \nFalse;
				endif
		endif
		if (\n閉じたときに\nタスクバーに表示しない\n) then
			-[#blue]-> \nTrue;
			:OperatorAgent を最小化し、\n通知領域に格納;
		else
			-[#red]-> \nFalse;
			:OperatorAgent を\n最小化してタスクバー表示;
			-[#black]->
		endif
		end;
		@enduml
		```

1. OperatorAgent 終了時の処理  
	- ログオフ処理  
ControlCenter にレジストされた、OperatorAgent のログイン情報（ユーザ・座席表の位置・内線番号との関連付け）などをリリースします。  

		![](images/NOTICE.png){width=50px}　OperatorAgent を手動で終了せずに PC のシャットダウンを行った場合、PC のシャットダウンシーケンス開始を検出した OperatorAgent は自身も終了処理を実施します。さらに、終了処理が完了するまで OS が完全にシャットダウンすることを待機させます。  
		ただし、OS 側でも各種終了処理が並行で実施されるため、OperatorAgent が ControlCenter と通信しログオフ処理を完了する前に OS の通信デバイスが停止している可能性があります。その場合、OperatorAgent のログイン情報が ControlCenter 上に残り続けます。（その後、[1-3. OperatorAgent と ControlCenter の通信](#1-3-operatoragent-と-controlcenter-の通信) の 1 の仕様に従い、OperatorAgent の状態がタイムアウトになります。）  

		![](images/Check.png){width=50px}　OperatorAgent を RDS or VDI オプション付きでインストールしている場合、ライセンスのリリースはログオフとは同期して処理されません。  
		ControlCenter の 『ライセンス状況』・『ログイン状況』 の表示時に、ログアウトやタイムアウトの状態になったライセンスを解放しています。  

### 1-5. OperatorAgent からのコマンド実行
- OperatorAgent からは、詳細設定項目（[@tbl:oacommand]）を設定することで特定のタイミングでコマンドを実行することができます。

	No. | 設定分類 | 設定項目名 | 通話情報<br />（call） | 通話フィルタ情報<br />（filterinfo） | 検出通話フィルタ情報<br />（filterdetection） | 実行コマンド情報<br />（executedcommand） | OperatorAgent 情報<br />（oa） |
	---:|---|---|:---:|:---:|:---:|:---:|:---:|
	1  | OperatorAgent - コマンド実行 | OperatorAgent起動時に実行するコマンド | × | × | × | × | × |
	2  | OperatorAgent - コマンド実行 | OperatorAgent終了時に実行するコマンド | × | × | × | × |  × |
	3  | OperatorAgent - コマンド実行 | ログイン直後に実行するコマンド | × | × | × | × | △ |
	4  | OperatorAgent - コマンド実行 | ログアウト直後に実行するコマンド | × | × | × | × | △ |
	5  | OperatorAgent - コマンド実行 | 通話開始直後に実行するコマンド | ○ | × | × | × | △ |
	6  | OperatorAgent - コマンド実行 | 通話終了直後に実行するコマンド | ○ | × | × | × | △ |
	7  | OperatorAgent - コマンド実行 | 通話フィルタの検出時に実行するコマンド | ○ | ○ | ○ | × | △ |
	8  | OperatorAgent - コマンド実行 | 通話フィルタの手動コマンド実行後に実行するコマンド | ○ | ○ | ○ | ○ | △ |
	9  | OperatorAgent - メニュー        | 通話内容の検索エンジン | × | × | × | × | ○ |

	: OperatorAgent コマンド実行と指定可能なオプション変数 {#tbl:oacommand}

	△ は サブキー "SearchString" を除いて利用が可能です。  

	<br / >

- コマンド は任意で指定可能で、  
	1. Exe ファイルなどのアプリケーション  
	2. Bat or Cmd などの実行可能ファイル  
	3. ファイル名 or フォルダパス  
	4. URL  

	などを適宜指定します。  
	基本的には、Windows の 『ファイル名を指定して実行』 で上記を指定したときと同じ挙動になります。  
	この機能で保証されるのは、指定コマンドの実行であって、**期待した結果が得られるかどうかではありません**。

	<br />

- [@tbl:oacommand] から実行するコマンドには、オプション変数が利用できます。  
オプション変数を利用することで、コマンドに様々な情報を付加することが可能です。  
記述するフォーマットは以下の通りです。  

	```
	${'メインキー文字列', 'サブキー文字列', 'オプション'}
	```  

	例えば、通話情報の ユーザID を取得したい場合には、  

	```
	${call, UserKey}
	```  

	オプションに urlencode を指定すると、値が URL エンコードされ置き換えられます。(※ 一部例外あり)  
	通話情報の会話識別子をそのままコマンドの引数として使用したい場合は以下のように記述します。  

	```
	http://webserver/SpeechVisualizer/Detail.aspx?key=${call, Key, urlencode}
	```  

	![](images/NOTICE.png){width=50px}
	　本機能では、`$` は特殊文字として予約されています。  
	コマンドの設定で `$` を文字として使用したい場合は、`\` でエスケープしてください。  
	同様に `"` や `\` も特殊文字ですので、文字として使用する場合は `\` でエスケープしてください。  
	<br />

- オプション変数のメインキーとサブキー
オプション変数で指定できるメインキーは用途毎に以下の種類が用意されています。  
オプション変数が有効な値を返却可能なタイミングは一定ではありませんので、[@tbl:oacommand] を確認してください。  
各メインキーで利用できるサブキーの一覧は、[@tbl:commandsubkey] を参照してください。  

	1. 通話情報 (call)
通話に関する情報が取得出来ます。  
		- サブキー 『EndDate』 / 『EndDateTime』 と 『Duration』 について  
『通話開始直後に実行するコマンド』 に指定すると、空文字列になります。  
		- サブキー 『HoldDuration』 と 『HoldCount』 について  
『通話開始直後に実行するコマンド』 に指定すると、 "0" になります。  
		<br />  

		![](images/NOTICE.png){width=50px}  

		- 通話開始時には、その時点で判明している範囲で値が設定されます。CTI 連携などで通話開始よりわずかでも遅く設定されている場合、値は設定されていません。  
		- 通話終了時には、一番優先度が高い相手の情報が設定されます。  
			1. 通話回線種別が、外線＞内線＞会議＞不明の順で優先されます。  
			1. 同じ通話回線種別の場合は、先に通話を開始した相手が優先されます。  
		- フィルタ検出時には、検出した瞬間の相手の情報が設定されます。これは、後で手動でコマンドを実行しても変化することはありません。  
	1. 通話フィルタ情報 (filterinfo)  
通話フィルタに関する情報が取得出来ます。  
	1. 検出通話フィルタ情報 (filterdetection)  
検出通話フィルタに関する情報が取得出来ます。  
	1. 実行コマンド情報 (executedcommand)  
実行コマンドに関する情報が取得出来ます。  
	1. OperatorAgent 情報 (oa)  
OperatorAgent に関する情報が取得出来ます。  

	No. | メインキー | サブキー名 | 置換される値 | [@tbl:callb2] との対応 | 備考
	---:|-------|--------|---|---|--
	1   | call | Key | 会話識別子 | - |
	2   | call | ConversationKey | 会話識別子 | - |
	3   | call | ProjectName | プロジェクト名 | - |
	4   | call | UserKey | ユーザID | - | Communication Suite へのログイン情報
	5   | call | LineKey | 内線番号 | - |
	6   | call | Date | 通話開始日時 | - | 日時系は、urlencode の指定ができません。代わりに [カスタム日時形式文字列](https://docs.microsoft.com/ja-jp/dotnet/standard/base-types/custom-date-and-time-format-strings?redirectedfrom=MSDN) の指定が可能です。<br />${call, StartDateTime, yyyy-MM-dd}
	7   | call | StartDate | 通話開始日時 | - | 日時系
	8   | call | StartDateTime | 通話開始日時 | - | 日時系
	9   | call | EndDate | 通話終了日時 | - | 日時系
	10   | call | EndDateTime | 通話終了日時 | - | 日時系
	11   | call |Duration | 通話時間(秒) | - |
	12   | call |HoldDuration | 累積保留時間(秒) | - |
	13   | call |HoldCount | 保留回数 | - |
	14   | call |DetailViewUrl | 詳細表示のURL | - |
	15   | call |OperatorPhoneNumber | 自番号 | No.9 |
	16   | call |OperatorPhoneLabel | 自分のID | No.8 | 電話基盤へのログイン情報
	17   | call |OperatorGroup | 受電グループ | No.10 | 受電スキル
	18   | call |OperatorHostName | 自分のホスト名 | No.11 | コントロールフォンが動作している PC の ホスト名（[@tbl:callb2] 参照）
	19   | call | Direction | 通話の向き | No.2 |
	20   | call | LineType | 通話種別 | No.3 |
	21   | call | CustomerPhoneNumber | 相手番号 | No.14 |
	22   | call | CustomerPhoneLabel | 相手の名称 | No.13 |
	23   | call | TrunkGroup | トランクグループ | No.19 |
	24   | call | TrunkMember | トランクメンバ | No.20 |
	25   | call | CalledPhoneNumber | ダイヤル番号 | No.17 |
	26   | call | AlertingPhoneNumber | 呼出先番号 | No.18 |
	27   | call | QueuePhoneNumber | キュー番号 | No.21 |
	28   | call | DialInPhoneNumber | ダイヤルイン番号 | No.16 |
	29   | call | TransferSourcePhoneNumber | 転送元番号 | No.24 |
	30   | call | TransferSourceLabel | 転送元名称 | No.23 |
	31   | call | TransferDestinationPhoneNumber | 転送先番号 | No.27 |
	32   | call | TransferDestinationLabel | 転送先名称 | No.26 |
	33   | call | MonitoringType | モニタリング種別 | No.31 |
	34   | call | MonitoringPhoneNumber | モニタリング対象の内線番号 | No.30 |
	35   | call | MonitoringLabel | モニタリング対象の名称 | No.29 |
	36   | call | GlobalReferenceId | グローバル参照用の ID | No.32 |
	37   | call | GlobalReferenceUrl | グローバル参照用の URL | No.33 |
	38   | call | LocalReferenceId | ローカル参照用の ID | No.34 |
	39   | call | LocalReferenceUrl | ローカル参照用の URL | No.35 |
	40   | call | SiteReferenceId | サイト参照用の ID | No.36 |
	41   | call | SiteReferenceUrl | サイト参照用の URL | No.37 |
	42   | call | PrivateReferenceId | プライベート参照用の ID | No.38 |
	43   | call | PrivateReferenceUrl | プライベート参照用の URL | No.39 |
	44   | filterinfo | ConversationFilterId | 通話フィルタID |  |
	45   | filterinfo | ConversationFilterName | 通話フィルタ名称 |  |
	46   | filterinfo | ConversationDescription | 通話フィルタの説明 |  |
	47   | filterinfo | ActionCommands | アクションコマンドの一覧 |  | 複数のオブジェクトが配列として格納されています。添字を使って複数の中から１つを指定して、さらに下位の値を指定してください。<br /> 例） ${filterinfo, ActionCommands[0].CommandName} |
	48   | filterinfo | **（下位）** CommandName | コマンド名称 |  | ActionCommands の下位コマンド
	49   | filterinfo | **（下位）** ActionCommand | 実行するコマンド |  | ActionCommands の下位コマンド
	50   | filterinfo | ActionAttributes | アクション属性の一覧 |  | 複数のオブジェクトが配列として格納されています。添字を使って複数の中から１つを指定して、さらに下位の値を指定してください。<br />  例） ${filterinfo, ActionAttributes[0].ConversationAttributeKey}
	51   | filterinfo | **（下位）** ConversationAttributeKey | アクション属性識別名 |  | ActionAttributes の下位コマンド
	52   | filterinfo | **（下位）** ConversationAttributeValue | アクション属性値 |  | ActionAttributes の下位コマンド
	53   | filterinfo | **（下位）** Priority | 優先度 |  | ActionAttributes の下位コマンド
	54   | filterinfo | ActionTags | アクションタグの一覧(配列) |  | 複数のオブジェクトが配列として格納されています。添字を使って複数の中から１つを指定して、さらに下位の値を指定してください。<br /> 例) ${filterinfo, ActionTags[0].ConversationTagName}
	55   | filterinfo | **（下位）** ConversationTagName | 通話タグ名称 |  | ActionTags の下位コマンド
	56   | filterdetection | SegmentNo | セグメント番号 |  |
	57   | filterdetection | ConversationFilterId | 通話フィルタID |  |
	58   | filterdetection | ConversationFilterName | 通話フィルタ名称 |  |
	59   | filterdetection | ChannelType | チャンネル種別 |  |
	60   | filterdetection | StartTime | 通話の開始位置からの、検出の開始位置を表すミリ秒 |  |
	61  | filterdetection | EndTime | 通話の開始位置からの、検出の終了位置を表すミリ秒 |  |
	62  | filterdetection | DetectionString | 検出文字列 |  |
	63  | executedcommand | CommandName | コマンド名称 |  |
	64  | executedcommand | ActionCommand | 実行したコマンド |  |
	65  | oa | project | プロジェクト名 |  |
	66  | oa | line | 内線番号 |  |
	67  | oa | user | ユーザ識別名 |  |
	68  | oa | name | ユーザ名 |  |
	69  | oa | email | E メールアドレス |  |
	70  | oa | SearchString | 検索文字列 |  | 設定出来るのは [@tbl:oacommand] の 『通話内容の検索エンジン』 のみです。

	: サブキーの一覧 {#tbl:commandsubkey}  

### 1-6. コマンドラインからの OperatorAgent 操作
- OperatorAgent は、コマンドラインから  

	```
	インストールパス\OperatorAgent.exe --オプション＝値（-オプション 値）
	```  
	のように起動（終了）できます。  
	[@tbl:oa-option] はコマンドラインで指定可能なオプションの一覧です。  

	No.| 内容 | オプション名 | 短いオプション名  
	--:|---|---|--
	1| ControlCenterの指定 | --server=[ControlCenterURL] | -s [ControlCenterURL]  
	2| ユーザIDの指定 | --user=[ユーザID] | -u [ユーザID]  
	3| パスワードの指定 | --password=[パスワード] | -p [パスワード]  
	4| 内線番号の指定 | --line=[内線番号] | -l [内線番号]  
	5| 自動アップデート禁止 | --disable-update |  
	6| 言語の指定 | --culture=languagecode2-country/regioncode2 |  
	7| 起動中のOAを終了 | --exit |  

	: OperatorAgent のコマンドラインオプション {#tbl:oa-option}  

	![](images/Tips.jpg){width=50px}  
	- 『ControlCenterの指定』 は、一時的に OperatorAgent の接続先を開発環境に向けたいときなどに利用します。  
	- 『ユーザIDの指定』 と 『パスワードの指定』 を同時に組合せることにより、統合 Windows 認証 を利用することなく自動ログインを可能にします。  
	- 『内線番号の指定』 は、一時的に設定済みの内線番号ではない電話機と組み合わせてテストするときなどに指定します。  
	- 『自動アップデートの禁止』 不具合があることがわかっている OperatorAgent に自動バージョンアップをさせたくない場合などに指定します。  
	- 『言語の指定』  
OperatorAgent の表示言語を切替えます。  
以下は書式例です。主な言語コードと国コードの組み合わせは、[@tbl:gengo] を参照してください。  

		```
		--culture=ja-JP
		--culture=en-US
		```

		No.| コード | 言語 | 国  
		--:|---|--|--
		1 | ar-AE | アラビア語 | アラブ首長国連邦
		2 | ar-SA | アラビア語 | サウジアラビア
		3 | it-IT | イタリア語 | イタリア
		4 | id-ID | インドネシア語 | インドネシア
		5 | ii-CN | イ語 | 中国
		6 | uz-Cyrl | ウズベク語 | キリル
		7 | es-ES | スペイン語 | スペイン
		8 | es-MX | スペイン語 | メキシコ
		9 | th-TH | タイ語 | タイ
		10 | de-DE | ドイツ語 | ドイツ
		11 | fr-FR | フランス語 | フランス
		12 | bn-IN | ベンガル語 | インド
		13 | pt-BR | ポルトガル語 | ブラジル
		14 | pt-PT | ポルトガル語 | ポルトガル
		15 | ru-RU | ロシア語 | ロシア
		16 | en-AU | 英語 | オーストラリア
		17 | en-CA | 英語 | カナダ
		18 | en-GB | 英語 | 英国
		19 | en-US | 英語 | 米国
		20 | dsb-DE | 下ソルブ語 | ドイツ
		21 | ko-KR | 韓国語 | 韓国
		22 | zh-CN | 中国語 | 簡体字、中国
		23 | ja-JP | 日本語 | 日本

		: 言語コードと国コード {#tbl:gengo}

	- 『起動中のOAを終了』 は、端末の操作が著しく限定されている。かつ、端末シャットダウン時に実行中のアプリケーションの全終了が条件の環境で利用しています。  

### 1-7 OperatorAgent のインストール
- OperatorAgent は、インストーラを通常起動してウィザード形式で手動インストールする方法と、インストーラ実行時に引数付きで起動し自動インストールする方法と2種類のインストールがサポートされています。  
- 自動インストール時に引数指定するオプション（[@tbl:oainstalloption]）次第ではサイレントインストールが可能です。  

	No.| オプション | 内容  
	--:|---|--
	1 | /SILENT | インストールの進捗を示すウィンドウ以外表示されなくなります。 ウィザードによる指定が出来なくなるので、必要なオプションを指定する必要があります。  
	2 | /VERYSILENT | すべてのウィンドウが表示されなくなります。 ウィザードによる指定が出来なくなるので、必要なオプションを指定する必要があります。  
	3 | /SUPPRESSMSGBOXES | 表示されるメッセージボックスを抑制します。/SILENT または /VERYSILENT オプションを指定したときのみ効果があります。  
	4 | /LOG | インストールのログが、ユーザのテンポラリフォルダ内に作成されます。  
	5 | /LOG="filename" | インストールのログが、filename に指定されたファイルに作成されます。  
	6 | /NOCANCEL | キャンセルボタンと閉じるボタンがクリックできなくなります。/SILENT オプションと同時に指定すれば、インストール中にキャンセルされなくなります。  
	7 | /NORESTART | 再起動が必要の場合でも、再起動しなくなります。  
	8 | /RESTARTEXITCODE=exit_code | 再起動が必要な場合に返す終了コードを指定します。この指定が無いと 0 が返ります。 通常は /NORESTART オプションと共に使用します。  
	9 | /CLOSEAPPLICATIONS | OperatorAgent やコンバージャ調整ツールが起動している場合に、それらのアプリケーションを終了します。（以下 10 ～12 を指定しない場合この挙動となります。）  
	10 | /NOCLOSEAPPLICATIONS | OperatorAgent やコンバージャ調整ツールが起動している場合に、それらのアプリケーションを終了せずにインストールを試みます。  
	11 | /FORCECLOSEAPPLICATIONS | OperatorAgent やコンバージャ調整ツールが起動している場合に、それらのアプリケーションを強制的に終了します。  
	12 | /RESTARTAPPLICATIONS | インストーラが終了させたアプリケーションを、インストール完了後に起動します。 `/CLOSEAPPLICATIONS` オプションと共に使⽤します。  
	13 | /LOADINF="filename" | インストーラが、指定した filename より設定を読み込んで実行します。/SAVEINFO コマンドにより保存したファイルを使用できます。  
	14 | /SAVEINF="filename" | インストール中に指定した設定を filename に保存します。  
	15 | /DIR="x:\dirname" | インストール先のディレクトリを指定します。これは「インストール先の指定」画面のインストールフォルダに相当します。  
	16 | /GROUP="folder name" | プログラムグループを指定します。 これは「プログラムグループの指定」画面のプログラムグループ名に相当します。  
	17 | /NOICONS | プログラムグループを作成しなくなります。 これは「プログラムグループの指定」画面の「プログラムグループを作成しない」にチェックを入れるのに相当します。  
	18 | /TYPE=type_name | インストールするコンポーネントのセットを指定します。 これは「コンポーネントの選択」画面のコンボボックスによる選択に相当します。 指定できる値は [@tbl:oainstalltype] の通りです。  
	19 | /COMPONENTS="component_names" | インストールするコンポーネントを指定します。カンマ「,」で区切ることにより複数指定できます。 ここで指定されたコンポーネントだけがインストールされます。 これは「コンポーネントの選択」画面のチェックボックスによる選択に相当します。 指定できる値は [@tbl:oainstallcomponent] の通りです。  
	20 | /TASKS="task_names" | 実行するタスクを指定します。カンマ「,」で区切ることにより複数指定できます。 ここで指定されたタスクだけが実行されます。 これは「追加タスクの選択」画面のチェックボックスによる選択に相当します。 指定できる値は [@tbl:oainstalltasks] の通りです。  
	21 | /MERGETASKS="task_names" | 実行するタスクを指定します。カンマ「,」で区切ることにより複数指定できます。 /TASKS オプションと似ていますが、デフォルトでチェックされているタスクと、このオプションで指定されたタスクが実行されます。  
	22 | /LicenseNumber=license_number | ライセンス番号を指定します。 これは「ユーザ情報」画面の「ライセンス情報」に相当します。  
	23 | /InstallKey=install_key | インストールキーを指定します。 これは「ユーザ情報」画面の「インストールキー」に相当します。  
	24 | /LogPath=log_folder | Communication Suite のログの出力先のフォルダを指定します。 これは「ログ出力先の指定」画面の「ログ出力先」に相当します。  
	25 | /ControlCenterServerUrl=controlcenter_url | 接続する ControlCenter サーバのURLを指定します。 これは「サーバURLの指定」画⾯の「サーバURL」に相当します。 どのコンポーネントをインストールする場合でも必須となります。  
	26 | /NodeGroup=nodegroup_name | 使⽤するノードグループを指定します。 これは「ノードグループ名の指定」画⾯の「ノードグループ名」に相当します。 RealTimeRecorder または StreamingRecognizer をインストールする場合は必須となります。インストールするコンポーネントに RealTimeRecorder、StreamingRecognizer が含まれていない場合は無視されます。  
	27 | /LineNo=line_key | 端末で使⽤する内線番号を指定します。 これは「内線番号の指定」画⾯の「内線番号」に相当します。OperatorAgent をインストールせずに RealTimeRecorder または StreamingRecognizer をインストールする場合は必須となります。 インストールするコンポーネントに OperatorAgent、RealTimeRecorder、StreamingRecognizer が含まれていない場合は無視されます。  
	28 | /RDS=1 | RemoteDesktop を使った仮想環境3にインストールする場合に指定します。これにより、⾃動アップデートは動作しなくなり、OperatorAgent でログイン中のみ OperatorAgent のライセンスが消費されます。 インストールするコンポーネントに、RealTimeRecorder、StreamingRecognizer 等のクライアント録⾳、クライアント認識に関係するコンポーネントを含めることは出来ません。この引数を指定してインストールした場合、アップデートインストール時には必ずこの引数を指定してアップデートする必要があります。  
	29 | /VDI=1 | VDI を使った仮想環境にインストールする場合に指定します。これにより、通常通り⾃動アップデートは動作しますが、OperatorAgent でログイン中のみ OperatorAgent のライセンスが消費されます。 インストールするコンポーネントに、RealTimeRecorder、StreamingRecognizer 等のクライアント録⾳、クライアント認識に関係するコンポーネントを含めることは出来ません。この引数を指定してインストールした場合、アップデートインストール時には必ずこの引数を指定してアップデートする必要があります。  

	: OperatorAgent インストールオプション {#tbl:oainstalloption}

	No.| type_name | 内容  
	--:|---|--
	1 | full | フルインストールします。  
	2 | oa | OperatorAgent のみをインストールします。  
	3 | rc | コンバージャー版 OperatorAgent をインストールします。  
	4 | rp | クライアントパケットキャプチャ版 OperatorAgent をインストールします。  

	: OperatorAgent のインストールタイプ {#tbl:oainstalltype}

	No.| Component | 内容  
	--:|---|--
	1 | OperatorAgent | 全ての通話プロバイダで必要です。  
	2 | RealTimeRecorder | PCのサービスとして RealTimeRecorder をインストールします。クライアント版を利用する場合には必要です。  
	3 | RealTimeRecorder\Converger | 通話プロバイダで、音声デバイス方式でコンバージャーを利用する場合に必要です。コンバージャーを制御するための DLL などがインストールされます。  
	4 | RealTimeRecorder\PacketCapture |SLC 及び クライアントパケットキャプチャ形式で録音する場合に必要です。パケットキャプチャのライブラリがインストールされます。  
	5 | RealTimeRecorder\PacketCapture\Avaya | SLC 及び クライアントパケットキャプチャ形式で、通話プロバイダで Avaya 電卓する場合に必要です。No 4 と合わせて、Avaya パケットキャプチャ のライブラリが追加インストールされます。  
	6 | RealTimeRecorder\CTILink | CTI 連携用の DLL をインストールします。  
	7 | StreamingRecognizer | PC のサービスとして StreamingRecognizer をインストールします。クライアント版を利用する場合には必要です。  
	8 | ConvergerTool | コンバージャー調整ツールをインストールします。コンバージャー方式での録音処理に必須ではありませんが、コンバージャーの調整には必要です。  

	: OperatorAgent インストール時に選択可能なコンポーネント {#tbl:oainstallcomponent}

	No.| task_name | 内容  
	--:|---|--
	1 | DesktopIcon | デスクトップにアイコンを作成します。  
	2 | RegisterStartup | スタートアップに登録します。  

	: OperatorAgent インストールタスク {#tbl:oainstalltasks}

	![](images/Tips.jpg){width=50px}　OperatorAgent は、⼀つの PC にインストールフォルダを変えて複数インストールすることが可能です。  
	PC に複数の OperatorAgent をインストールしている場合、コントロールパネルの 「アプリケーションの追加と削除 (プログラムと機能)」 からアンインストールできるのは、一番最後にインストールしたインスタンスだけです。それ以外のインスタンスをアンインストールする場合、 インストールフォルダ直下の `『uninstall\unins000.exe』` を実⾏してください。  
	<br />
- OperatorAgent インストーラ内で実行される **WSH**  
	[@tbl:vbslist] は、自動バージョン時に実行される vbs のリストですが、インストーラでインストールする場合には、[@tbl:vbslist] とは別に、`XsltExec.wsf` が実行されます。vbs ファイルではありませんが、内部で WSH を実行しているため、セキュリティソフトの仕様によっては実行がブロックされてしまい、正常なインストールができません。

	<div style="page-break-before:always"></div>

	<hr/>

## 第2章 SpeechVisualizer

### 2-1. SpeechVisualizer のログイン

#### 2-1-1. SpeechVisualizer のログインに関連する ControlCenter の詳細設定項目
  - [@tbl:svlogin] は、SpeechVisualizer のログインに関わる詳細設定項目です。設定分類は、**共通 - セキュリティ** となります。

	No. | 設定項目名       | デフォルト値 | 内容 |
	---:|------------------|--------------|------|
	1   |  ログイン状態の維持 | false        | ブラウザに保存された Cookie を永続化するための入力項目がログイン画面に追加される |  

	: 詳細設定 : SpeechVisualizer のログインに関わる設定 {#tbl:svlogin}  

	![](images/NOTICE.png){width=50px}　『ログイン状態の維持』 を true に設定すると、ログイン画面に 『ブラウザを終了してもログインを維持する』 というチェックボックスが表示されます。その項目にチェックをつけてからログインするとこで、ユーザの Cookie が永続化されます。  
	永続化された状態では、ブラウザを終了してもログイン状態が維持され続けます。この状態を解除するには、SpeechVisualizer 画面のログオフボタンから手動で明示的なログオフ操作を行うか、ブラウザに保存された Cookie の情報を削除するか、ログイン情報が保存されているユーザのパスワードを変更する必要があります。  

#### 2-1-2. SpeechVisualizer へのログイン方法  
  1. フォーム認証  
	     SpeechVisualizer のログイン画面から手動で入力したログイン情報か、ブラウザに保存された有効期限内の Cookie の情報でログインします。（※ Cookie の情報を利用する場合には、ログイン画面は表示されません。）  
  2. 統合 Windows 認証  
	SpeechVisualizer の Web アプリケーショの認証設定で、**Windows 認証** が適切に有効化されている場合、ログイン画面は表示されず、自動的にログインします。
  3. OperatorAgent 連携  
  OperatorAgent の各種機能から SpeechVisualizer を呼び出します。（呼出のための設定は、[@tbl:svshort] を参照してください。）  
	このログイン方法では、手動ログイン操作は発生せずに自動でログイン処理が実施されますが、上記の2つと異なる第3 のログイン方法ではなく、実際には有効になっている 『フォーム認証』 か 『統合 Windows 認証』 いずれかのログインが裏側で実行されています。  
<br />

		```plantuml
		@startuml

		skinparam {
			shadowing false
			defaultFontName "Segoe UI, BIZ UDPゴシック, sans-serif"
			BackgroundColor #afeeee
			ArrowColor black
		}

		skinparam activity  {
			BorderColor #000000
			DiamondBorderColor #008000
			BackgroundColor #ffffff
		}

		title アクティビティ図.3 [SpeechVisualizer ログイン]\n

		start;
		-[#black]-> SpeechVisualizer にアクセス;
		if (\n認証 Cookie が有効期限内\n) then
			-[#blue]-> Yes;
			:SpeechVisualizer 起動;
			end;
		else
		-[#red]-> No;
				if (\n統合 Windows 認証\n) then
					-[#blue]-> \nYes;
					:SpeechVisualizer 起動;
					end;
				else
					-[#red]-> No;
					:フォーム認証;
				endif
		endif
		if (\nOperatorAgent 連携起動\n) then
			-[#blue]-> 　Yes;
		else
			-[#red]-> \nNo;
			:ログイン画面表示 ＆ \n手動ログイン処理;
		endif
		:SpeechVisualizer 起動;
		end;
		@enduml
		```

#### 2-1-3. SpeechVisualizer ログインタイムアウトについて  
- [@tbl:svloginto] は、SpeechVisualizer のログインタイムアウトに関わる詳細設定項目です。設定分類は全て、『共通 - セキュリティ』 です。

	No. | 設定項目名       | デフォルト値 | 内容 |
	---:|------------------|--------------|------|
	1   |  ブラウザログインタイムアウト | 1800        | 認証 Cookie の生存期間です。生存期間が設定時間の半分未満となった状態で、サーバにアクセスすることで設定値にリセットされます。  
	2   |  ブラウザログインを継続するための通知間隔 | 20        | 『ブラウザログインタイムアウト』 が発生しないようにするために定期的にリクエストを送信する間隔を定義しています（**座席表のみで利用されます。**） |

	: SpeechVisualizer ブラウザログインタイムアウト {#tbl:svloginto}

### 2-2. SpeechVisualizer ホーム画面  
- SpeechVisualizer ホーム画面の詳細設定項目は、[@tbl:svhomepara] です。

	No. | 設定分類 | 設定項目名       | 設定値 |内容
	---:|------------------|--------------|------|--
	1  | SpeechVisualizer - ホーム | ホームモジュールのプロバイダ |  2-2-1 参照 | ホーム画面にガジェットを提供します。  
	2  | SpeechVisualizer - ホーム | ホーム画面のレイアウト (配置情報)  | 2-2-2 参照 | ガジェット名と設定項目をもとに配置情報を指定します。 |  
	3   | SpeechVisualizer - ホーム   | ホームモジュールの自動再読込間隔  | 600000 |各ホームモジュールが自動で再読込を行う場合の間隔の設定します。単位は「ミリ秒」、有効値「1以上の整数」を指定。 |
	4   | SpeechVisualizer - ホーム | 感情の遷移モジュールに表示する感情スコア |  2-2-3 参照 | 『感情の遷移』ガジェットに表示する感情を指定。   |
	5   | SpeechVisualizer - ホーム  |重要な通話モジュールに表示するグラフの色   |   | <font color="red">未実装の機能の設定項目のため、変更しないでください。</font>   |
	6  | SpeechVisualizer - ホーム | 通話一覧モジュールに表示する感情スコア  | 2-2-3 参照 | 『感情解析結果の表示』の設定を有するガジェット名に表示する感情を指定。   |

	: ホームモジュールと詳細設定との対応 {#tbl:svhomepara}

#### 2-2-1. SpeechVisualizer ホーム画面のガジェットとプロバイダ

- ホーム画面に表示する、ガジェットを提供するのが 『プロバイダ』 です。  
[@tbl:svhomepara] の『ホームモジュールのプロバイダ』 の設定書式は以下です。

	```
	Profile
	Link
	Announcement
	・・・中略・・・
	Score
	QualityEvaluationTemplate
	AgentSkill
	```

	プロバイダ名を改行区切りで記述します。  設定可能なプロバイダ名は [@tbl:homeprovider] を参照してください。

	No. | ガジェット名       | プロバイダ名 | デフォルトでの画面配置 |内容 |
	---:|------------------|--------------|------|------|
	1 |プロフィール |Profile |〇|自分のプロフィールを表示します。|
	2 |リンク |Link |〇|リンクの一覧を表示します。|
	3 |お知らせ |Announcement |〇|お知らせの一覧を表示します。|
	4 |自分の通話 |MyRecentConversation |〇|自分の通話の一覧を表示します。|
	5 |自分の通話(IN) |MyRecentConversation ||自分のINBOUND通話の一覧を表示します。|
	6 |自分の通話(OUT) |MyRecentConversation ||自分のOUTBOUND通話の一覧を表示します。|
	7 |所属プロジェクトの通話 |ProjectRecentConversation |〇|自分が所属しているプロジェクトの通話の一覧を表示します。|
	8 |所属プロジェクトの通話(IN) |ProjectRecentConversation ||自分が所属しているプロジェクトのINBOUND通話の一覧を表示します。|
	9 |所属プロジェクトの通話(OUT) |ProjectRecentConversation ||自分が所属しているプロジェクトのOUTBOUND通話の一覧を表示します。|
	10 |自分が最近再生した通話 |RecentHistory |〇|自分が再生した通話の一覧を表示します。|
	11 |自分が最近参照した通話 |RecentHistory |〇|自分が参照した通話の一覧を表示します。|
	12 |自分が最近編集した通話 |RecentHistory |〇|自分が編集した通話の一覧を表示します。|
	13 |自分の通話に対する最近のコメント |RecentComment |〇|自分の通話に対するコメントの一覧を表示します。|
	14 |自分が最近投稿したコメント |RecentComment ||自分が通話に対して投稿したコメントの一覧を表示します。|
	15 |お気に入り |Favorite |〇|自分のお気に入りの通話を表示します。|
	16 |評価の遷移 |RatingCurve |〇|自分の通話に対する評価グラフを表示します。|
	17 |感情の遷移 |EmotionCurve ||任意のユーザの感情グラフを表示します。|
	18 |マイクエリ |MyQuery ||任意のマイクエリを検索条件にして取得した通話の一覧を表示します。|
	19 |通話スコアリング |Score ||任意の通話スコアリングが適応された通話の一覧を表示します。|
	20 |通話品質評価テンプレート |QualityEvaluationTemplate ||任意の通話品質評価テンプレートによって評価された通話の一覧を表示します。|
	21 |スキル |AgentSkill ||任意のスキルに関連する情報をグラフ化したものを表示します。|
	22 | 重要な通話 |HighCallPriorityConversation ||<font color="red">未実装のプロバイダのため指定しないでください。</font> |

	: モジュールとプロバイダの対応 {#tbl:homeprovider}


#### 2-2-2. SpeechVisualizer ホーム画面のレイアウト情報

- ホーム画面のガジェット配置を設定できます。

	[@tbl:svhomepara] の『ホーム画面のレイアウト (配置情報)』 の設定書式は以下です。

	```
	Profile,Link,RatingCurve,Announcement;MyRecent,RecentComment,Favorite;ProjectRecent,MyRecentViewHistory,MyRecentPlayHistory,MyRecentEditHistory
	```
	[@fig:home_defaultlayout] は上記のデフォルト設定の状態で初回ログインしたユーザのガジェットレイアウトです。

	![デフォルト設定のホーム画面レイアウト](images/2-2-home_defaultlayout.png){#fig:home_defaultlayout width=700px}

	記載されたガジェットは右から順にホーム画面右側の上部から配置されます。複数のガジェットを配置する場合は`,`で区切りで記述します。ガジェットは一つ前のガジェットの下部に追加されていきます。`;`で区切ることで1つ左に列を追加することができます(最大3列まで)。

	配置情報で使われるガジェット名は[@tbl:homeprovider]で記載したプロバイダ名と一部内容が異なります。設定可能なガジェット名は[@tbl:layoutgadget]を参照してください。

	No. | ガジェット名       | プロバイダ名 | レイアウト設定上のガジェット名 |
	---:|------------------|--------------|------|
	1 |プロフィール | Profile | Profile |
	2 |リンク | Link | Link |
	3 |お知らせ | Announcement | Announcement |
	4 |自分の通話 | MyRecentConversation | MyRecent |
	5 |自分の通話(IN) | MyRecentConversation | MyRecentInbound |
	6 |自分の通話(OUT) | MyRecentConversation | MyRecentOutbound |
	7 |所属プロジェクトの通話 | ProjectRecentConversation | ProjectRecent |
	8 |所属プロジェクトの通話 (IN) | ProjectRecentConversation | ProjectRecentInbound |
	9 |所属プロジェクトの通話 (OUT) | ProjectRecentConversation | ProjectRecentOutbound |
	10 |自分が最近再生した通話 | RecentHistory | MyRecentPlayHistory |
	11 |自分が最近参照した通話 | RecentHistory | MyRecentViewHistory |
	12 |自分が最近編集した通話 | RecentHistory | MyRecentEditHistory |
	13 |自分の通話に対する最近のコメント | RecentComment | RecentComment |
	14 |自分が最近投稿したコメント | RecentComment | RecentPostComment |
	15 |お気に入り | Favorite | Favorite |
	16 |評価の遷移 | RatingCurve | RatingCurve |
	17 |感情の遷移 | EmotionCurve | emotionCurve |
	18 |マイクエリ | MyQuery | MyQuery |
	19 |通話スコアリング | Score | Score |
	20 |通話品質評価テンプレート |QualityEvaluationTemplate | QualityEvaluation |
	21 |スキル |AgentSkill | AgentSkill |

	: レイアウト設定上のガジェット名とプロバイダ名の一覧 {#tbl:layoutgadget}


	![](images/NOTICE.png){width=50px}　『ホーム画面のレイアウト (配置情報)』の設定で配置の対象となるのは『ホームモジュールのプロバイダ』で設定した『プロバイダ』のガジェットのみです。『プロバイダ』に追加済みでも『マイクエリ』ガジェットは SpeechVisualizer のマイクエリ機能、『通話スコアリング』、『通話品質評価テンプレート』、『スキル』ガジェットについてはそれぞれ ControlCenter で設定済みの場合のみ表示されます。

	<br />

	![](images/check.png){width=50px}　『ホーム画面のレイアウト (配置情報)』はシステム全体のデフォルト設定とユーザごとの個人設定が有ります。ユーザがホーム画面の設定・レイアウト変更を行うまでは、デフォルト設定が適用されます。設定・レイアウト変更を行った際に、ユーザごとの個人設定が作成され、個人設定の内容が優先されるようになります。個人設定は、ユーザが設定・レイアウト変更を行った場合のみ更新されます。

	<br />

	![](images/Tips.jpg){width=50px}　ガジェットは、固有のプロパティを持っています。レイアウト時にプロパティの設定値を指定することも可能です。各ガジェットの固有のプロパティと書式情報は後述いたします。
	『マイクエリ』、『通話スコアリング』、『通話品質評価テンプレート』、『スキル』ガジェットはガジェット名の後に`-`と数字を記載して表示したい項目を指定する必要があります。それぞれ作成した項目順に1から割り当てられます。

	<br />

	1. プロフィール〈Profile〉 【[@fig:home_profile]】  
『Profile』はレイアウト時に以下の書式で、2つのプロパティについて定義することができます。

		```
		Profile::0
		```
		![プロフィールガジェットと設定項目](images/2-2-home_profile.png){#fig:home_profile width=400px}  

		No. | 設定項目      | デフォルトの設定 |設定内容
		---:|------|------------------|-  |  
		1  | 将来の実装のための予約  | 未設定  | 将来の実装のための予約 |  
		2  |自動更新の有効化   | 0  |0:無効化,1:有効化   |  

		: プロフィールガジェットの書式説明 {#tbl:svhomeprofile}  

 	1. リンク〈Link〉  
リンクガジェットはレイアウト時のプロパティはありません。

 	1. お知らせ〈Announcement〉 【[@fig:home_info]】  
『Announcement』はレイアウト時に以下の書式で、2つのプロパティについて定義することができます。

		```
		Announcement:5:0
		```

		![お知らせガジェットと設定項目](images/2-2-home_info.png){#fig:home_info width=500px}

		No. | 設定項目      | デフォルトの設定 |設定内容|
		---:|------|------------------|-  |   
		1  |表示件数の選択   |  5 | UI上は5,10,20件から選択、詳細設定では1~20件で設定可能です。  |    
		2  |既読のお知らせの表示   | 0  |0:表示しない,1:表示する   |   
  	:お知らせガジェットの書式説明 {#tbl:svhomeinfo}

 	1. 自分の通話〈MyRecent〉【[@fig:home_myrecent]】  
『MyRecent』はレイアウト時に以下の書式で、6つのプロパティについて定義することができます。

		```
		MyRecent:5:0::::1
		```

		![自分の通話ガジェットと設定項目](images/2-2-home_myrecent.png){#fig:home_myrecent width=500px}

		No. | 設定項目      | デフォルトの設定 |設定内容|
		---:|------|------------------|-  |   
		1  |表示件数の選択   |  5 | UI上は5,10,20件から選択、詳細設定では1~20件で設定可能です。  |    
		2  |自動更新の有効化   | 0  | 0:無効化,1:有効化   |   
		3  |将来の実装のための予約   | 未設定  | 将来の実装のための予約  
		4  |将来の実装のための予約   | 未設定  | 将来の実装のための予約    
		5  |将来の実装のための予約   | 未設定  | 将来の実装のための予約
		6  |感情解析結果の表示   | 1  | 0:表示しない,1:表示する   |   
		:自分の通話ガジェットの書式説明 {#tbl:svhomemyrecent}



 	1. 自分の通話(IN) 〈MyRecentInbound〉【[@fig:home_myrecentinbound]】  
『MyRecentInbound』はレイアウト時に以下の書式で、6つのプロパティについて定義することができます。

		```
		MyRecentInbound:5:0::::1
		```

		![自分の通話(IN)ガジェットと設定項目](images/2-2-home_myrecentinbound.png){#fig:home_myrecentinbound width=400px}

		No. | 設定項目      | デフォルトの設定 |設定内容|
		---:|------|------------------|-  |     
		1  |表示件数の選択   |  5 | UI上は5,10,20件から選択、詳細設定では1~20件で設定可能です。  |    
		2  |自動更新の有効化   | 0  |0:無効化,1:有効化   |   
		3  |将来の実装のための予約   | 未設定  | 将来の実装のための予約  
		4  |将来の実装のための予約   | 未設定  | 将来の実装のための予約    
		5  |将来の実装のための予約   | 未設定  | 将来の実装のための予約
		6  |感情解析結果の表示   | 1  |0:表示しない,1:表示する   |   
		:自分の通話(IN)ガジェットの書式説明 {#tbl:svhomemyrecentinbound}

 	1. 自分の通話(OUT) 〈MyRecentOutbound〉【[@fig:home_myrecentoutbound]】  
『MyRecentOutbound』はレイアウト時に以下の書式で、6つのプロパティについて定義することができます。

		```
		MyRecentOutbound:5:0::::1
		```

		![自分の通話(OUT)ガジェットと設定項目](images/2-2-home_myrecentoutbound.png){#fig:home_myrecentoutbound width=400px}

		No. | 設定項目      | デフォルトの設定 |設定内容|
		---:|------|------------------|-  |   
		1  |表示件数の選択   |  5 | UI上は5,10,20件から選択、詳細設定では1~20件で設定可能です。  |    
		2  |自動更新の有効化   | 0  |0:無効化,1:有効化   |   
		3  |将来の実装のための予約   | 未設定  | 将来の実装のための予約  
		4  |将来の実装のための予約   | 未設定  | 将来の実装のための予約    
		5  |将来の実装のための予約   | 未設定  | 将来の実装のための予約
		6  |感情解析結果の表示   | 1  |0:表示しない,1:表示する   |   
		:自分の通話(OUT)ガジェットの書式説明 {#tbl:svhomemyrecentoutbound}

 	1. 所属プロジェクトの通話〈ProjectRecent〉【[@fig:home_projectrecent]】  
『ProjectRecent』はレイアウト時に以下の書式で、6つのプロパティについて定義することができます。

		```
		ProjectRecent:5:0:::1:1
		```

		![所属プロジェクトの通話ガジェットと設定項目](images/2-2-home_projectrecent.png){#fig:home_projectrecent width=400px}

		No. | 設定項目      | デフォルトの設定 |設定内容|
		---:|------|------------------|-  |    
		1  |表示件数の選択   |  5 | UI上は5,10,20件から選択、詳細設定では1~20件で設定可能です。  |    
		2  |自動更新の有効化   | 0  |0:無効化,1:有効化   |   
		3  |将来の実装のための予約   | 未設定  | 将来の実装のための予約     
		4  |将来の実装のための予約   | 未設定  | 将来の実装のための予約
		5  |カラムの表示   |1|1:オペレータ名で表示,2:内線番号で表示   |  
		6  |感情解析結果の表示   | 1  |0:表示しない,1:表示する   |   
		:所属プロジェクトの通話ガジェットの書式説明 {#tbl:svhomeprojectrecent}


 	1. 所属プロジェクトの通話(IN)〈ProjectRecentInbound〉【[@fig:home_projectrecentinbound]】  
『ProjectRecentInbound』はレイアウト時に以下の書式で、6つのプロパティについて定義することができます。

		```
		ProjectRecentInbound:5:0:::1:1
		```

		![所属プロジェクトの通話(IN)ガジェットと設定項目](images/2-2-home_projectrecentinbound.png){#fig:home_projectrecentinbound width=400px}

		No. | 設定項目      | デフォルトの設定 |設定内容|
		---:|------|------------------|-  |   
		1  |表示件数の選択   |  5 | UI上は5,10,20件から選択、詳細設定では1~20件で設定可能です。  |    
		2  |自動更新の有効化   | 0  |0:無効化,1:有効化   |   
		3  |将来の実装のための予約   | 未設定  | 将来の実装のための予約    
		4  |将来の実装のための予約   | 未設定  | 将来の実装のための予約
		5  |カラムの表示   |1|1:オペレータ名で表示,2:内線番号で表示   |  
		6  |感情解析結果の表示   | 1  |0:表示しない,1:表示する   |   
		:所属プロジェクトの通話(IN)ガジェットの書式説明 {#tbl:svhomeprojectrecentInbound}

 	1. 所属プロジェクトの通話(OUT)〈ProjectRecentOutbound〉【[@fig:home_projectrecentoutbound]】  
『ProjectRecentOutbound』はレイアウト時に以下の書式で、6つのプロパティについて定義することができます。

		```
		ProjectRecentOutbound:5:0:::1:1
		```

		![所属プロジェクトの通話(OUT)ガジェットと設定項目](images/2-2-home_projectrecentoutbound.png){#fig:home_projectrecentoutbound width=400px}

		No. | 設定項目      | デフォルトの設定 |設定内容|
		---:|------|------------------|-  |   
		1   |表示件数の選択   |  5 | UI上は5,10,20件から選択、詳細設定では1~20件で設定可能です。  |    
		2  |自動更新の有効化   | 0  |0:無効化,1:有効化   |   
		3   |将来の実装のための予約   | 未設定  | 将来の実装のための予約     
		4   |将来の実装のための予約   | 未設定  | 将来の実装のための予約
		5   |カラムの表示   | 1 |1:オペレータ名で表示,2:内線番号で表示   |  
		6  |感情解析結果の表示   | 1  |0:表示しない,1:表示する   |   
		:所属プロジェクト(OUT)の通話ガジェットの書式説明 {#tbl:svhomeprojectrecentoutbound}

 	1. 自分が最近再生した通話 〈MyRecentPlayHistory〉【[@fig:home_myrecentplayhistory]】  
『MyRecentPlayHistory』はレイアウト時に以下の書式で、6つのプロパティについて定義することができます。

		```
		MyRecentPlayHistory:5:0:::1:1
		```

		![自分が最近再生した通話ガジェットと設定項目](images/2-2-home_myrecentplayhistory.png){#fig:home_myrecentplayhistory width=400px}

		No. | 設定項目      | デフォルトの設定 |設定内容|
		---:|------|------------------|-  |   
		1  |表示件数の選択   |  5 | UI上は5,10,20件から選択、詳細設定では1~20件で設定可能です。  |    
		2  |自動更新の有効化   | 0  | 0:無効化,1:有効化   |     
		3  |将来の実装のための予約   | 未設定  | 将来の実装のための予約    
		4  |将来の実装のための予約   | 未設定  | 将来の実装のための予約
		5  |カラムの表示   | 1 | 1:オペレータ名で表示,2:内線番号で表示 |  
		6  |感情解析結果の表示   | 1  | 0:表示しない,1:表示する   |  
		:自分が最近再生した通話ガジェットの書式説明 {#tbl:svhomemyrecentplayhistory}

 	1. 自分が最近参照した通話 〈MyRecentViewHistory〉【[@fig:home_myrecentviewhistory]】  
『MyRecentViewHistory』はレイアウト時に以下の書式で、6つのプロパティについて定義することができます。  

		```
		MyRecentViewHistory:5:0:::1:1
		```

		![自分が最近参照した通話ガジェットと設定項目](images/2-2-home_myrecentviewhistory.png){#fig:home_myrecentviewhistory width=400px}

		No. | 設定項目      | デフォルトの設定 |設定内容|
		---:|------|------------------|-  |    
		1  |表示件数の選択   |  5 | UI上は5,10,20件から選択、詳細設定では1~20件で設定可能です。  |    
		2  |自動更新の有効化   | 0  |0:無効化,1:有効化   |    
		3  |将来の実装のための予約   | 未設定  | 将来の実装のための予約     
		4  |将来の実装のための予約   | 未設定  | 将来の実装のための予約
		5  |カラムの表示   |1|1:オペレータ名で表示,2:内線番号で表示  |  
		6  |感情解析結果の表示   | 1  |0:表示しない,1:表示する   |  
		:自分が最近参照した通話ガジェットの書式説明 {#tbl:svhomemyrecentviewhistory}

 	1. 自分が最近編集した通話 〈MyRecentEditHistory〉【[@fig:home_myrecentedithistory]】  
『MyRecentEditHistory』はレイアウト時に以下の書式で、6つのプロパティについて定義することができます。  

		```
		MyRecentEditHistory:5:0:::1:1
		```

		![自分が最近編集した通話ガジェットと設定項目](images/2-2-home_myrecentedithistory.png){#fig:home_myrecentedithistory width=400px}

		No. | 設定項目      | デフォルトの設定 |設定内容|
		---:|------|------------------|-  |   
		1  |表示件数の選択   |  5 | UI上は5,10,20件から選択、詳細設定では1~20件で設定可能です。  |    
		2  |自動更新の有効化   | 0  |0:無効化,1:有効化   |     
		3  |将来の実装のための予約   | 未設定  | 将来の実装のための予約    
		4  |将来の実装のための予約   | 未設定  | 将来の実装のための予約
		5  |カラムの表示   |1|1:オペレータ名で表示,2:内線番号で表示 |  
		6  |感情解析結果の表示   | 1  |0:表示しない,1:表示する   |  
		:自分が最近編集した通話ガジェットの書式説明 {#tbl:svhomemyrecentedithistory}

 	1. 自分の通話に対する最近のコメント 〈RecentComment〉【[@fig:home_recentcomment]】  
『RecentComment』はレイアウト時に以下の書式で、3つのプロパティについて定義することができます。  

		```
		RecentComment:5:0:
		```

		![自分の通話に対する最近のコメントガジェットと設定項目](images/2-2-home_recentcomment.png){#fig:home_recentcomment width=400px}

		No. | 設定項目      | デフォルトの設定 |設定内容|
		---:|------|------------------|-  |   
		1  |表示件数の選択   |  5 | UI上は5,10,20件から選択、詳細設定では1~20件で設定可能です。  |    
		2  |自動更新の有効化   | 0  |0:無効化,1:有効化   |     
		3   |将来の実装のための予約   | 未設定  | 将来の実装のための予約|   
		:自分の通話に対する最近のコメントガジェットの書式説明 {#tbl:svhomerecentcomment}


 	1. 自分が最近投稿したコメント 〈RecentPostComment〉【[@fig:home_recentpostcomment]】  
『RecentPostComment』はレイアウト時に以下の書式で、3つのプロパティについて定義することができます。  

		```
		RecentPostComment:5:1:0
		```

		![自分が最近投稿したコメントガジェットと設定項目](images/2-2-home_recentpostcomment.png){#fig:home_recentpostcomment width=400px}

		No. | 設定項目      | デフォルトの設定 |設定内容|
		---:|------|------------------|-  |   
		1  |表示件数の選択   |  5 | UI上は5,10,20件から選択、詳細設定では1~20件で設定可能です。  |    
		2  |自動更新の有効化   | 0  |0:無効化,1:有効化   |     
		3  |カラムの表示   |1|1:オペレータ名で表示,2:内線番号で表示 |   
		:自分が最近参照した通話ガジェットの書式説明 {#tbl:svhomerecentpostcomment}

 	1. お気に入り 〈Favorite〉【[@fig:home_favorite]】  
『Favorite』はレイアウト時に以下の書式で、2つのプロパティについて定義することができます。  

		```
		Favorite:1:1
		```

		![お気に入りガジェットと設定項目](images/2-2-home_favorite.png){#fig:home_favorite width=400px}

		No. | 設定項目      | デフォルトの設定 |設定内容|
		---:|------|------------------|-  |   
		1  |カラムの表示   |1|1:オペレータ名で表示,2:内線番号で表示 |   
		2  |感情解析結果の表示   | 1  |0:表示しない,1:表示する    |  
		:お気に入りガジェットの書式説明 {#tbl:svhomefavorite}

 	1. 評価の遷移  〈RatingCurve〉【[@fig:home_ratingcurve]】  
『RatingCurve』はレイアウト時に以下の書式で、3つのプロパティについて定義することができます。  

		```
		RatingCurve:6:M:1
		```

		![評価の遷移ガジェットと設定項目](images/2-2-home_ratingcurve.png){#fig:home_ratingcurve width=400px}

		No. | 設定項目      | デフォルトの設定 |設定内容|
		---:|------|------------------|-  |   
		1  |表示するX軸スケール(数値)   |6|UIで選択した場合は5,6,7,10,12,14のいずれかになります。詳細設定では任意の数字を指定が可能です。 |   
		2  |表示するX軸スケール(単位)   | M  |D:日,W:週,M:月    |  
		3  | ガジェットの大きさ | 1  |1:狭い,2:普通,3:広い   |  
		:評価の遷移ガジェットの書式説明 {#tbl:svhomeratingcurve}

		![](images/Check.png){width=50px}　『評価の遷移』で扱う「評価点数」は通話詳細から通話に対してコメントをつける際に設定できる点数(星の数)です。グラフにはX軸スケール単位内の(評価点数合計 ÷ 評価件数)で算出される1.0～5.0までの評価点数の平均値が表示されます。

 	1. 感情の遷移 〈emotionCurve〉【[@fig:home_emotioncurve]】  
『emotionCurve』はレイアウト時に以下の書式で、4つのプロパティについて定義することができます。  

		```
		emotionCurve:6:H:1:user01%2user02%2C・・・
		```

		![感情の遷移ガジェットと設定項目](images/2-2-home_emotioncurve.png){#fig:home_emotioncurve width=400px}

		No. | 設定項目      | デフォルトの設定 |設定内容|
		---:|------|------------------|-  |   
		1  |表示する横軸スケール(数値)   |6|UIで選択した場合は12,14のどちらかになります。詳細設定では任意の数字で指定が可能です。 |   
		2  |表示する横軸スケール(単位)   | H  |H:時,D:日    |  
		3  |自動更新の有効化   | 0  |0:無効化,1:有効化    |  
		4  |ユーザID   |   |感情の推移を確認したいユーザのIDを記載します。複数ユーザを設定する場合には、ユーザIDの間に`%2C`と記載します。   |  
		:感情の遷移ガジェットの書式説明 {#tbl:svhomeemotioncurve}

 	1. マイクエリ 〈MyQuery〉【[@fig:home_myquery]】  
『MyQuery』はレイアウト時に以下の書式で、6つのプロパティについて定義することができます。  

		```
		MyQuery-1:5:0:::1:1
		```

		![マイクエリガジェットと設定項目](images/2-2-home_myquery.png){#fig:home_myquery width=400px}

		No. | 設定項目      | デフォルトの設定 |設定内容|
		---:|------|------------------|-  |  
		1   |表示件数の選択   |  5 | UI上は5,10,20件から選択、詳細設定では1~20件で設定可能です。  |  
		2  |自動更新の有効化   | 0  |0:無効化,1:有効化   |  
		3   |将来の実装のための予約   | 未設定  | 将来の実装のための予約  
		4   |将来の実装のための予約   | 未設定  | 将来の実装のための予約  
		5   |カラムの表示   |1|1:オペレータ名で表示,2:内線番号で表示 |  
		6  |感情解析結果の表示   | 1  |0:表示しない,1:表示する   |  
		:マイクエリガジェットの書式説明 {#tbl:svhomemyquery}


 	1. 通話スコアリング 〈Score〉【[@fig:home_score]】  
『Score』はレイアウト時に以下の書式で、6つのプロパティについて定義することができます。  

		```
		Score-1:5:0:1::1:1
		```

		![通話スコアリングガジェットと設定項目](images/2-2-home_score.png){#fig:home_score width=400px}

		No. | 設定項目      | デフォルトの設定 |設定内容|
		---:|------|------------------|-  |    
		1  |表示件数の選択   |  5 | UI上は5,10,20件から選択、詳細設定では1~20件で設定可能です。  |    
		2  |自動更新の有効化   | 0  |0:無効化,1:有効化   |     
		3  |対象期間   | 1  |UI上は今日のみ(1) 、昨日から(2)、過去7日（7）のみ。詳細設定では任意の数字で指定が可能です。   
		4  |将来の実装のための予約   | 未設定  | 将来の実装のための予約
		5  |カラムの表示   |1|1:オペレータ名で表示,2:内線番号で表示 |  
		6  |感情解析結果の表示   | 1  |0:表示しない,1:表示する   |  
		:通話スコアリングガジェットの書式説明 {#tbl:svhomescore}

 	1. 通話品質評価テンプレート 〈QualityEvaluation〉【[@fig:home_qualityevaluation]】  
『QualityEvaluation』はレイアウト時に以下の書式で、6つのプロパティについて定義することができます。  

		```
		QualityEvaluation-1:5:0:1:1:1:1
		```

		![通話品質評価テンプレートガジェットと設定項目](images/2-2-home_qualityevaluation.png){#fig:home_qualityevaluation width=400px}

		No. | 設定項目      | デフォルトの設定 |設定内容|
		---:|------|------------------|-  |    
		1  |表示件数の選択   |  5 | UI上は5,10,20件から選択、詳細設定では1~20件で設定可能です。  |    
		2  |自動更新の有効化   | 0  |0:無効化,1:有効化   |     
		3  |対象期間   | 1  |UI上は今日のみ(1) 、昨日から(2)、過去7日（7）のみ。詳細設定では任意の数字で指定が可能です。   
		4  |ソート条件   | 1  |1:得点の高い順,2:得点の低い順
		5  |カラムの表示   |1|1:オペレータ名で表示,2:内線番号で表示 |  
		6  |感情解析結果の表示   | 1  |0:表示しない,1:表示する   |  
		:通話品質評価テンプレートガジェットの書式説明 {#tbl:svhomequalityevaluation}

 	1. スキル 〈MyRecentEditHistory〉【[@fig:home_agentskill]】  
『AgentSkill』はレイアウト時に以下の書式で、1つのプロパティについて定義することができます。  

		```
		AgentSkill-1:1
		```

		No. | 設定項目      | デフォルトの設定 |設定内容
		---:|------|------------------|-  |    
		1  |自動更新の有効化   | 0  |0:無効化,1:有効化   |   

		: スキルガジェットの書式説明 {#tbl:svhomeagentskill}

		![通話品質評価テンプレートガジェットと設定項目](images/2-2-home_agentskill.png){#fig:home_agentskill width=400px}

#### 2-2-3. ホーム画面での感情解析表示
- 感情が使用されているガジェットは、表示する感情を詳細設定から設定することができます。
[@tbl:svhomepara] の『感情の遷移モジュールに表示する感情スコア』『通話一覧モジュールに表示する感情スコア』 の設定書式は以下です。

	```
	nemesysco.qa5.callpriority.op.max
	nemesysco.qa5.excitement.positive.op.avg
	nemesysco.qa5.energy.energetic.op.avg
	```
	表示したい感情スコア識別名と設定値を改行区切りで記述します。
	感情スコア識別名については、[1-2-2. 通話表示機能　[@tbl:emoscore]: 保存する感情スコア](#1-2-2. 通話表示機能) を参照してください。**表示可能な感情スコアは『保存する感情スコア』に定義された感情のみです。**
	定義されていない感情スコアを設定した場合は無視されます。

	設定可能な値は 最大値(max),最小値（min）,平均値(ave),開始値(start),終了値(end)の5つです。

	デフォルトで用意されている配色とラベル名を変更したい場合は以下の設定書式が使用できます。

	```
	感情スコア識別名|color=6桁のHTMLカラーコード|label=ラベル名称
	例：nemesysco.qa5.angry.op.max|color=FF0000|label=OPの怒り(最大値)
	```
	デフォルトで定義されているラベル名称とカラーコードは [@tbl:emocolor] を参照してください。。

	No. |ラベル名称 |対応するHTMLカラーコード |デフォルトの色
	---:|------|------------------|:-:|
	1 |怒り |FF0000 |<font color="#FF0000">■</font>
	2 |集中 |1E90FF |<font color="#1E90FF">■</font>
	3 |不快 |000000 |<font color="#000000">■</font>
	4 |ポジティブ・ネガティブ |996600 |<font color="#996600">■</font>
	5 |ポジティブ |EF5611 |<font color="#EF5611">■</font>
	6 |ネガティブ |2A4496 |<font color="#2A4496">■</font>
	7 |後悔・快適 |666600 |<font color="#666600">■</font>
	8 |後悔 |333300 |<font color="#333300">■</font>
	9 |快適 |F41C40 |<font color="#F41C40">■</font>
	10 |イメージ |6666FF |<font color="#6666FF">■</font>
	11 |思考 |0033FF |<font color="#0033FF">■</font>
	12 |喜び |FF66CC |<font color="#FF66CC">■</font>
	13 |興味 |99CC00 |<font color="#99CC00">■</font>
	14 |悲しみ |00CC99 |<font color="#00CC99">■</font>
	15 |感情変化の極端さ |6600CC |<font color="#6600CC">■</font>
	16 |恐怖 |000099 |<font color="#000099">■</font>
	17 |確信無し・有り |CC3300 |<font color="#CC3300">■</font>
	18 |確信無し |3366CC |<font color="#3366CC">■</font>
	19 |確信有り |990000 |<font color="#990000">■</font>
	20 |エネルギッシュ・疲労 |FCC800 |<font color="#FCC800">■</font>
	21 |エネルギッシュ |EA2700 |<font color="#EA2700">■</font>
	22 |疲労 |003366 |<font color="#003366">■</font>
	23 |脳活動のサマリ |FFFF00 |<font color="#FFFF00">■</font>
	24 |感情的・論理的 |33CC33 |<font color="#33CC33">■</font>
	25 |感情的 |660066 |<font color="#660066">■</font>
	26 |論理的 |006666 |<font color="#006666">■</font>
	27 |思慮深さ |D9D9D9 |<font color="#D9D9D9">■</font>
	28 |音のエネルギー |FFE025 |<font color="#FFE025">■</font>
	29 |ボリューム |FFB689 |<font color="#FFB689">■</font>
	30 |期待 |FF7F00 |<font color="#FF7F00">■</font>
	31 |不満 |666666 |<font color="#666666">■</font>
	32 |通話重要度 |008000 |<font color="#008000">■</font>
	33 |エージェントスコア |D9D9D9 |<font color="#D9D9D9">■</font>
	34 |感情レベル |A9D08E |<font color="#A9D08E">■</font>
	35 |論理的レベル |9BC2E6 |<font color="#9BC2E6">■</font>
	36 |困惑レベル |1E90FF |<font color="#1E90FF">■</font>
	37 |緊張レベル |FFE699 |<font color="#FFE699">■</font>
	38 |活動レベル |FF6565 |<font color="#FF6565">■</font>
	39 |思考レベル |97E4FF |<font color="#97E4FF">■</font>
	40 |情熱レベル |DE0000 |<font color="#DE0000">■</font>
	41 |集中レベル |8497B0 |<font color="#8497B0">■</font>
	42 |疑いレベル |BF8F00 |<font color="#BF8F00">■</font>
	43 |期待レベル |FFCCFF |<font color="#FFCCFF">■</font>
	:ラベル名称とカラーコードの対応 {#tbl:emocolor}


### 2-3. SpeechVisualizer 通話検索  
Communication Suite の通話検索は、検索条件 UI に各種条件を設定するのではなく、検索モジュールを操作し、検索クエリを生成し、通話を検索する仕様となっています。  

- 検索モジュール  
検索クエリを作るための通話検索画面の UI です。 『プロバイダ』 を組み合わせて構成します。（[@fig:provider]、[@fig:provider2]）  

- プロバイダ  
検索モジュールに機能を提供します。以下の3種類のプロバイダが存在します。  
	1. 検索条件  
検索クエリに、検索条件を追加します。
	2. 検索結果のソート条件  
検索クエリに、検索結果のソート条件を追加します。
	3. マイクエリパネル  
よく利用する検索クエリをお気に入り登録します。

	![ 検索ウィンドウ](images/2-3-検索モジュールのプロバイダ.png){#fig:provider width=600px}  

	![ マイクエリパネル](images/2-3-マイクエリ.png){#fig:provider2 width=200px}  

#### 2-3-1. 検索モジュールのプロバイダ  

- 検索モジュールのプロバイダは、ControlCenter 詳細設定の [@tbl:provider0] の項目を編集して構成します。  

	No. | 設定項目名       | 設定値 | 内容 |
	-:|---------|---------|---------------|
	1   |  検索モジュールのプロバイダ  | 下記書式参照  | 検索モジュールを提供するプロバイダを一定書式で記述します。利用可能なプロバイダは [@tbl:provider] を参照してください。
	: 表示する検索モジュールのプロバイダ設定 {#tbl:provider0}

	検索モジュールのプロバイダは以下の書式（利用するプロバイダを改行区切り）で記述します。  

	```
	ProjectCondition  
	DteRangeCondition  
	TimeRangeCondition  
	DurationCondition  
	```

	![](images/Check.png){width=50px}　設定で、上から記述した順番通りに検索モジュール上にプロバイダアイコンが左から右へ並んで表示されます。  
	設定値として記述しなかったプロバイダはアイコンが非表示となり、該当項目の検索クエリも利用できません。  

	No. | 検索条件       | プロバイダ名| 検索クエリ （半角・全角不問）
	-:|-----|-------|----------------------------|
	1   |  プロジェクト  |ProjectCondition|p
	2   |  検索対象の日付  | DateRangeCondition|d
	3   |  検索対象の時間帯  | TimeRangeCondition |t
	4   |  通話時間  | DurationCondition |ct
	5   |  保留時間  | HoldDurationCondition |hold
		6   |  オペレータ  | OperatorCondition |op
		7   |  最終更新者  | EditorCondition|ed
		8   |  電話番号  |TelCondition|tel
		9   |  通話タグ  |TagCondition |tag
		10   |  通話フィルタ  |FilterCondition|f
		11  |  通話の向き  | DirectionCondition |cd
		12   |  相手の性別  | GenderCondition |ge
		13   |  通話スコアリング  | ScoreCondition|score
		14   |  通話品質評価  |QualityEvaluationCondition |qe
		15   |  ソート順  | SortCondition|[@tbl:keylist] 並び順で利用可能な検索クエリの一覧を参照
		16   |  マイクエリ  | MyQueryPanel |
		17  |  自分の通話  | MineCondition |
		18  |  お気に入りの通話  |FavoriteCondition|
		19  |  通話の操作履歴  | HistoryCondition|

	: デフォルト設定の検索モジュールのプロバイダ一覧 {#tbl:provider}  

	- 通話属性を検索プロバイダに追加する  
		書式は以下です。各項目識別名は \| で区切ります。接頭語以外は順不同です。  
		例）Avaya の ユニバーサルコール ID を検索条件に追加  

		```
		AttributeCondition|prefixes=ucid|attributes=amivoice.common.reference.global.id|iconName=person1|lessQueryLabel=UCIDの一部を入力してください...|iconLabel=UCID|autoCompleteLength=0
		```

		通話属性プロバイダの書式の各項目は[@tbl:provider3] の通りです。 『アイコン名』に関しては、
	表 64 で補足します。

		No. | 識別名       | 名称| 値 | 説明      |省略可否|
		---:|------------------|--------------|------|------|------|
		1   |  AttributeCondition | 接頭語        | なし| 項目を追加する際の定型文です。| ×|
		2   |  attributes | 通話属性識別名        | 文字列 | 通話検索条件に追加する通話属性識別子です。通話属性識別名は CommunicationSuite 内で通話属性毎に設定されているユニークな識別名です。使用可能な通話属性については（[1-2-2.　[@tbl:callb2] : 利用可能な通話属性一覧](#1-2-2. 通話表示機能) 参照。）  を参照してください。ただし、番号系の情報は、デフォルトプロバイダ 『電話番号』 をカスタマイズして追加します。（後述） | ×|
		3   |  prefixes| プレフィックス        | 文字列| 通話検索条件を識別するクエリ文字列です。| ×|
		4   |  iconName | アイコン名        | 文字列| 検索プロバイダとして表示するアイコンを [@tbl:icon1] から指定します。 | 〇|
		5   |  lessQueryLabel | 説明文        |文字列| 通話検索条件入力欄にプレフィックスを入力した際に表示される説明文です。| 〇|
		6   |  iconLabel | アイコンラベル        | 文字列|話検索入力欄のアイコンをマウスオーバーした時に表示される名称です。複数の通話検索条件で同じアイコン名を指定した場合、通話検索条件入力欄で該当のアイコンをマウスオーバーした際に表示されるのは設定順が上のものがアイコンラベルとなります。複数の通話検索条件で同じアイコン名を指定した場合、該当のアイコンをクリックすることで通話検索条件のアイコンラベルが複数表示されて選択クリックすることで任意の通話検索条件を選択することができます。| 〇|
		7   |  autoCompleteLength | オートコンプリートを表示させるまでの文字数        | 整数| オートコンプリートが表示されるまでに入力する文字数です。値を 0 にすると指定した通話属性で紐づいている値が最大15件自動表示されます。| 〇|

		: 追加する通話属性の書式 {#tbl:provider3}

		No. | 利用可能なアイコン      | アイコンの種類| アイコン名
		---:|:------------------:|--------------|------|
		1   | ![](images/2-3-icon1.png){#fig:aaa width=20px} | 人物        | person1|
		2   | ![](images/2-3-icon2.png){#fig:aaa width=20px} | 電話1       | tel1|
		3   | ![](images/2-3-icon3.png){#fig:aaa width=20px} | 電話2        | tel2|
		4   | ![](images/2-3-icon4.png){#fig:aaa width=20px} | 電話3        | tel3|
		5   | ![](images/2-3-icon5.png){#fig:aaa width=20px} |  星1        | star1
		6   | ![](images/2-3-icon6.png){#fig:aaa width=20px} | 星2       | star2|
		7   | ![](images/2-3-icon7.png){#fig:aaa width=20px}  | 吹き出し1        | balloon1|
		8   | ![](images/2-3-icon8.png){#fig:aaa width=20px} | 吹き出し2       | balloon2|

		: 利用可能なアイコン {#tbl:icon1}

		![](images/Tips.jpg){width=50px}　通話属性を検索モジュールに追加する際、同じアイコン名（iconName）を指定すると、検索モジュール上では一つのアイコンでまとめて表示されます。  
	例） Avaya の ユニバーサルコール ID と コール ID を一つのアイコンにまとめた場合 (検索モジュールのイメージは [@fig:denwa2] を参照してください。)  

		```
		AttributeCondition| iconName=tel1 | prefixes=ucid   | attributes=amivoice.common.reference.global.id | lessQueryLabel=UCIDの一部を入力してください...  | iconLabel=UCID
		AttributeCondition| iconName=tel1 | prefixes=callid | attributes=amivoice.common.reference.local.id  | lessQueryLabel=CALLIDの一部を入力してください...| iconLabel=CALLID
		```
		![1つのアイコンに複数のプロバイダを追加する](images/2-3-追加プロバイダまとめ.png){#fig:denwa2 width=300px}  

	- デフォルトプロバイダ 『電話番号』 をカスタマイズする  
	『電話番号』 プロバイダに、通話属性を追加する場合にはより簡単な書式で指定が可能です。  

		```
		TelCondition | targets=*all*,*op,cu*,line*,queue*
		```

		『TelCondition』 に `target` プロパティを指定し、利用する通話属性を `,` 区切りで列挙します。 `target` に指定可能な通話属性は、[@tbl:zokuseikey] を参照してください。  
		TelCondition のみを記述した場合、

		```
		TelCondition | targets=*all*,*op,cu*,line*
		```
		として表示されます。  

		![『キュー番号』を追加時の結果](images/2-3-電話番号1.png){#fig:denwa1 width=300px}  

		![](images/Tips.jpg){width=50px}　target に 指定した通話属性に `*` を付加すると、付加する位置により前方一致（line\*）、後方一致（\*line）、部分一致（\*line\*） で検索できるようになります。  

		No. | 属性       | 検索条件|利用可否| [@tbl:callb2] 通話属性識別名との対比
		---:|------------------|--------------|----------|---------|
		1   | all| 通常         |デフォルト設定で利用可  |項目なし  
		2   | op| 自番号      |デフォルト設定で利用可 |No.9
		3   | cu | 相手番号       |デフォルト設定で利用可   |No.14  
		4   | line| 内線番号      |デフォルト設定で利用可   |項目なし   
		5   | called | 掛先番号        |  |No.17  
		6   | alerting | 呼出先番号       |  |No.18  
		7   |  queue| キュー番号       |  |No.21  
		8   |  dialin| ダイヤルイン番号        |  |No.16  
		9   |  ts| 転送元番号 検索        |  |No.23  
		10   | td| 転送先番号 検索      |  |No.27   

		: 電話番号に追加可能な属性 {#tbl:zokuseikey}  

	- ソートプロバイダ  
		[@fig:narabijun] はソート条件を指定するイメージです。  

		![並び順の画面](images/2-3-並び順.png){#fig:narabijun width=500px}  

		ソートプロバイダの設定は ControlCenter 詳細設定の。 @tbl:narabi を編集して構成します。

		No. | 設定項目名       | 設定値 | 内容 |
		---:|-----------|----------|-------------------------|
		1   |  SpeechVisualizer - 通話検索  | 検索で使用する並び順 | 検索で使用するソート順です。検索条件として利用しないプロバイダがあればソート順からも削除しておくと整合性がとれます。  |

		: 検索結果のソート順の設定 {#tbl:narabi}

		@tbl:narabi の書式は以下です。上から記述した順番通りに [@fig:narabijun] のようにリスト表示されます。  

		```
		date
		dater
		time
		・・・
		```

		[@tbl:keylist] は並び順で利用可能な検索クエリの一覧です。

		No. |検索クエリ       | 利用可否| 検索条件|
		-:|-----|-------|----|
		1   |date |デフォルト設定で利用可 |date - 通話開始日時順（古い通話開始日時が先頭）
		2   |dater |デフォルト設定で利用可    |dater - 通話開始日時順の逆順（新しい通話開始日時が先頭）
		3   |time|デフォルト設定で利用可    |time - 通話時間順（短い通話時間が先頭）
		4   |timer |デフォルト設定で利用可 |timer - 通話時間の逆順（長い通話時間が先頭）
		5   |httime |デフォルト設定で利用可    |httime - 合計保留時間順（合計保留時間が長い通話が先頭）
		6   |httimer |デフォルト設定で利用可    |httimer - 合計保留時間の逆順（合計保留時間が短い通話が先頭）
		7   |hmtime |デフォルト設定で利用可 |hmtime - 最大保留時間順（最大保留時間が長い通話が先頭）
		8   |hmtimer |デフォルト設定で利用可    |hmtimer - 最大保留時間の逆順（最大保留時間が短い通話が先頭）
		9   |update |デフォルト設定で利用可    |update - 最終更新日時順（古い最終更新日時が先頭）
		10   |updater |デフォルト設定で利用可 |updater - 最終更新日時の逆順（新しい最終更新日時が先頭）
		11   |optel|デフォルト設定で利用可    |optel - 自番号順（オペレータ側の電話番号順）
		12   |optelr |デフォルト設定で利用可    |opter - 自番号の逆順（オペレータ側の電話番号の逆順）
		13   |cutel |デフォルト設定で利用可    |cutel - 相手番号順（カスタマ側の電話番号順）
		14   |cutelr|デフォルト設定で利用可    |cutelr - 相手番号の逆順（カスタマ側の電話番号の逆順）
		15   |ext |デフォルト設定で利用可    |ext - 内線番号順（オペレータの内線番号順）
		16   |extr |デフォルト設定で利用可    |extr - 内線番号の逆順（オペレータの内線番号の逆順）
		17   |rate |デフォルト設定で利用可    |rate - 評価順（高い評価が先頭）
		18   |rater |デフォルト設定で利用可    |rater - 評価の逆順（低い評価が先頭）
		19   |qe |デフォルト設定で利用可    |qe - 品質評価結果順（品質評価結果のポイントが高い順）
		20   |qer|デフォルト設定で利用可    |qer - 品質評価結果の逆順（品質評価結果のポイントが低い順）
		21   |rank|デフォルト設定で利用可    |rank - キーワードランク（キーワードにより適合した順）
		22   |score|   |score - 通話スコア順（通話スコアリングによるスコアが高い順）
		23   |scorer|   |scorer - 通話スコアの逆順（通話スコアリングによるスコアが低い順）

		: 並び順で利用可能な検索クエリの一覧 {#tbl:keylist}  

#### 2-3-2. 検索クエリの仕様  
検索モジュールを操作することにより、検索モジュール内の検索ウィンドウに `検索クエリ` が構成されます。  
検索プロバイダとして指定して表示される各種アイコンは、検索条件を指定するための UI ではなく、
検索クエリを生成するための補助部品となります。  
検索クエリの仕様さえ把握していれば、検索ウィンドウに直接 `検索クエリ` を入力することでも通話検索を実行できます。

1. 基本のクエリ  

	```
	<検索条件クエリ>:<検索値>
	```
	例） プロジェクト名 "インバウンド"を検索条件にした場合  

	```
	p:インバウンド
	```

	![](images/Tips.jpg){width=50px}　基本の検索クエリ以外でも、指定可能な検索クエリが用意されているものがあります。 @tbl:kensakuquery1 参照  
	例）プロジェクトの場合は `p`が基本の検索クエリですが、他にも,`pj`,`proj`,`project` で指定することが可能です。  
<br>

	No. | 基本の検索クエリ       |指定可能
	-:|-----|-------|
	1   |  p  |`pj` `proj` `project`
	2   |  d  |`date` `daterange`
	3   |  t  |`time` `timerange`
	4   | op   |`operator` `user`
	5   | ed |`editor` `edituser` `editoperator`
	6   |  tel |`telephone` `phone` `phonenumber`
	7   | f   |`filter`
	8   | cd   |`direction` `calldirection`
	9   | ge   |`sex` `gender`
	10   |score   |`bayes`
	11   | qe   |`qualityevaluation`

	: 指定可能な検索クエリ一覧 {#tbl:kensakuquery1}  



	@tbl:kensakuquery2 は製品マニュアルで公開していない利用可能な検索クエリです。  

	No. | 検索条件|検索クエリ|説明
	---:|-----------------|--------------|------------|
	1   | 所属プロジェクト        |myproject|自分の所属するプロジェクトを検索
	2   | オペレータID           |opid        |オペレータIDを検索
	3   | 自分の通話         |mine       |自分の通話を検索
	4   | 最終更新者ID         |edid        |最終更新者のオペレータIDを検索
	5   | お気に入り              |favorite         |お気に入りの通話を検索
	6   | 通話の操作履歴              |history  |自分の操作履歴を検索<br>再生履歴の書式・・・ history:再生<br>編集履歴の書式・・・history:編集<br>表示履歴の書式・・・history:表示  

	: 公開していない利用可能な検索クエリ {#tbl:kensakuquery2}  

1. 条件の組み合わせ  
	基本のクエリを複数組み合わせて、複数検索条件を指定して **AND 検索** することができます。  
	基本のクエリをスペースで連結します。  

	```
	<検索条件クエリ1>:<検索値1> <スペース> <検索条件クエリ2>:<検索値2>
	```

	例） 「オペレータ」と「通話の日付」の検索クエリを組み合わせた場合 （ope-A の今日の通話を検索）  

	```
	op:ope-A d:1d
	```

1. 検索条件のオプション  
[@tbl:option1] は1つの検索条件内で利用可能なオプションです。  

	No. | オプション     |説明
	---:|-----------------|----------|
	1   | OR 検索 | 検索値を複数指定できます。検索値を `,（カンマ）` 区切りで複数指定します。
	2   | NOT 検索 | 検索値の除外検索ができます。検索値の先頭に `-（ハイフン）` を付加します。

	: 検索条件のオプション {#tbl:option1}

	- OR 検索  
例） プロジェクト名 "インバウンド" と "アウトバウンド" を検索条件にする

		```
		p:インバウンド,アウトバウンド
		```

	- NOT 検索  
例） プロジェクト名 "インバウンド" 以外のプロジェクトを検索する  

		```
		p:-インバウンド
		```

1. フリーワード検索  
フリーワードを検索条件にする場合には、基本クエリとは仕様が異なります。  
検索条件に指定したい単語を直接検索クエリに記述します。  
フリーワード検索は、基本のクエリと組み合わせが可能です。

	<br />  

	例） 認識結果に 「りんご」 が含まれる通話を検索する

	```
	りんご
	```

	例） プロジェクト名 "インバウンド" で、認識結果に 「りんご」 が含まれる通話を検索する

	```
	p:インバウンド りんご
	```


	- フリーワード検索のオプション  

		- 論理和（OR 検索）  
例） 「りんご」 または 「みかん」 のいずれかの単語を含む通話を検索

			```
			りんご or みかん
			```

		- 論理積（AND 検索）  
例） 「りんご」 と 「みかん」 の両方の単語を含む通話を検索  

			```
			りんご　みかん
			```

		- 論理否定（NOT 検索）  
例） 「りんご」 の単語は含まず、「みかん」の単語が含む通話を検索  

			```
			-りんご みかん
			```

			![](images/NOTICE.png){width=50px}　フリーワードは NOT 検索のみでは指定できません。（検索クエリとして評価されず、検索時に無視されます。必ず上記例のように NOT 演算子を付加しないフリーワードを指定して利用してください。）  

			<br>

1. フリーワード検索のアーキテクチャ  
Microsoft© SQL Server のフルテキスト検索の機能を利用しています。（`SQL Full-text Filter Daemon Launcher (MSSQLSERVER)`） サービスの起動が必要です。  

	- フリーワードの対象  
	検索可能な文字列は フルテキスト検索の仕様（ワードブレーカー）で選定された **単語** が対象となります。  
"コールセンター" を含む通話を検索したい場合に有効なクエリは、  

		```
		コールセンター
		コールセンタ
		コールセンターの（助詞）
		```

		です。
		末尾の "ー" の有無は、ステミング機能により同一単語として解釈されます。  
		助詞 "の" はノイズワード（最新の SQLServer では `ストップワード`）の仕様によって検索クエリとして評価されません。  
		ノイズワードとは、 SQL Server が、頻繁に出現しすぎて検索に役立たないと判断し、インデックスを作成しない文字列になります。  
		SQLServer のバージョンにより、内部で定義されたノイズワードの定義に違いがあるようです。  
		基本的には、後発バージョンの方が、パフォーマンスが向上しているためかノイズワードの定義が緩和（登録数が少ない）されている傾向があります。

		<br />

		単純な文字列検索ではないため、"ルセン" などのフルテキスト検索のワードブレーカーが、単語 として認識していない文字列には、インデックスが作成されないため、検索ができません。

		<br />

		![](images/Tips.jpg){width=50px}　フリーワード検索実行時、検索文字列にノイズワードが含まれている場合には以下のようなメッセージが画面に表示されます。  
		1. キーワードにノイズワードが含まれていたため検索が行われませんでした。  
このメッセージが表示された場合、内部では2つの処理結果のパターンが存在します。  
			- 検索文字列がノイズワードのみで構成されていて、検索処理が行われなかった  
			- 検索文字列にノイズワードが含まれていて、ノイズワードを無視して検索処理を実行したが、検索結果件数が 0 だった  
		1. キーワードにノイズワードが含まれていたため無視しました。  
検索文字列にノイズワードが含まれていて、ノイズワードを無視して検索処理を実行し、検索結果件数が 1 件以上だった  

		1 の後者のパターンは、メッセージに対して若干ずれた挙動となっています。

	<br>

1. クエリ文字列の最大長  
検索クエリで指定可能なクエリの長さは、ベースの URL を含めた場合、 IIS の 「要求フィルター」の設定（[@fig:youkyuft] ）に依存しています。（デフォルト 2046 バイトまで。）  
ベースの URL 部分を含めない場合、クエリに指定可能な最大長は 464 バイト です。  
クエリ文字列の最大長を超えた場合には、検索実行時に ASP.NET のエラーページにリダイレクトされます。  
クライアント PC からのアクセス時にはローカル環境に ASP.NET のエラーページのリソースが存在しないため、404 エラーとなって表示されます。

	![IIS 要求フィルターの設定画面](images/2-3-要求フィルター.png){#fig:youkyuft width=500px}  

1. 検索条件入力時の候補検索の仕組み  
各種検索プロバイダは、検索条件を入力時に、入力された文字（列）を元に条件の候補をリストアップして表示する機能を持っています。  
候補のソースは、検索プロバイダに対応する管理機能となります。（ユーザ系であればユーザ管理に登録されたデータ、削除・有効期間切れは対象外になります。）  
管理機能が存在しない情報、内線番号以外の電話番号情報や UCID などは、通話属性が対象となります。（内線番号は内線番号管理に登録されたものとなります。）  

	- 候補表示時の件数とソート順  
表示件数に関する設定は [@tbl:koho] の詳細設定の設定分類 『SpeechVisualizer - オートコンプリート』 となります。  

		<br / >  

		入力値が 『最小文字数』 に達すると、データベースで検索を行います。そのとき取得する件数が 『ユーザ最大検索件数』・『通話属性最大検索件数』・『電話番号最大検索件数』 となります。（検索プロバイダによって変わります。）  
		その中の上位 『表示数』 件を候補表示します。  
		検索値の入力を続けると、既に取得されている件数の中からさらに、上位 『表示数』 件で絞り込みを行い候補を表示します。  
		例として、[@tbl:koho] の値が全てデフォルト値だった場合、検索条件で1文字目を入力するとデータベースから1000件取得し、上位15件を表示します。続けて、2文字目が入力されると、その1000件から絞り込んた結果の上位15件を表示します。  
		この処理の関係上、通話データのように元データが多い場合には、最初の1000件から候補が漏れてしまい表示されないことがありますが、現在の実装による制限事項となります。  
		デフォルト値で狙った候補が表示されない場合には、『最小文字数』 と 『各種最大検索件数』 の値を調整することで対応してください。  

		No. | 設定項目名 | デフォルト値 | 特記
		---:|----------------------|---------------:|---
		1   | 最小文字数 | 1 |  
		2   | ユーザ最大検索件数 | 1000 |  
		3   | 通話属性最大検索件数 | 1000 |  
		4   | 電話番号最大検索件数 | 1000 |  
		5   | 表示数 | 15 |  

		: SpeechVisualizer - オートコンプリート {#tbl:koho}

		ソート順は電話番号系も含め、基本的には文字列順 (ユーザであればユーザ識別名順) となっていますが、各種管理画面からの設定で「並び順」のプロパティを持っているものは、その並び順となります。（ただし、並び順を持ったデータの多くが、システム全体やプロジェクト毎にデータを作成することができ、登録区分毎に並び順を持っているので実際にはかなり適当な順番で表示されているように見えます。）  

		![](images/Tips.jpg){width=50px}　ユーザ系のオートコンプリートは、ユーザID 以外にユーザ名の一部でも反応します。  

#### 2-3-3. 通話検索結果
- 検索結果に関わる詳細設定項目は [@tbl:kekka1] です。  

	No. | 設定分類      | 設定項目名 | 内容|
	---:|-----------|------------|----------------|
	1   |  SpeechVisualizer - 通話検索  | 1ページ中に表示する件数 |検索画面の1ページ中に表示する通話の件数です。 [@fig:kekka3] の赤枠で囲った単位が対象です。  
	2   |  SpeechVisualizer - 通話検索 | 前後に表示するページ数 |1ページに表示する件数を超える検索結果の場合にページ移動のためにボタン [@fig:kekka4] の数を指定します。有効値は「1～20」です。  
	3   |  SpeechVisualizer - 通話検索  | 検索結果に表示する追加の通話属性|利用可能な通話属性は @tbl:callb2 を参照。<br>書式は下記参照。（複数追加する場合は改行で区切る）

	: 検索結果に関連する詳細設定項目 {#tbl:kekka1}


 1.  1ページ中に表示する件数（ [@fig:kekka3]）  

		![1ページ中に表示する件数](images/2-3-検索結果3.png){#fig:kekka3 width=800px}  

 2.  前後に表示するページ（ [@fig:kekka4]）  

		![ページ移動ボタン](images/2-3-検索結果4.png){#fig:kekka4 width=500px}

 3.  検索結果に表示する追加の通話属性（ [@fig:kekka5]）  

		![通話に紐づいた通話属性](images/2-3-検索結果5.png){#fig:kekka5 width=800px}  

		[@tbl:kekka1] の検索結果に表示する追加の通話属性は「通話属性識別名=ラベル」という形で定義します。

		例） 検索結果に表示する通話に「ダイヤルイン番号」を表示する

		```
		amivoice.common.telephony.called.phonenumber=ダイヤルイン番号
		```

		検索結果で表示可能な通話属性一覧は @tbl:callb2 を参照ください。  
		検索結果に 〇 が付いているものはデフォルト設定で通話検索結果に表示可能な通話属性です。  
<br>

 4.  検索結果に表示される通話内容（ [@fig:kekka6]、[@fig:kekka7]）  
独自仕様で通話内容を要約（不要語の削除や単語の省略化）して450～500文字文字程度で表示します。通話開始からが対象となり、既定の文字列に達すると言葉足らずであっても、そこで表示が終わりになります。

		![検索結果に表示される通話内容](images/2-3-検索結果2.png){#fig:kekka6 width=700px}  

		![実際の通話内容](images/2-3-検索結果6.png){#fig:kekka7 width=600px}  



#### 2-3-4. 通話検索の対象となる通話データ
- 通話データが以下２つの条件を満たすと検索結果に表示されるようになります。  

	1. RealTimeRecorder の録音完了アップロードが終了している(MediaScriber で連携した音声ファイルは、録音開始時点で、録音完了済みとして扱われる)  
	1. 録音が完了した（エラー終了ではない）会話録音ファイルが存在する（会話録音 = 保留操作等で区切られた録音単位）

### 2-4. SpeechVisualizer 通話詳細  

#### 2-4-1. 通話詳細の画面構成
- 通話詳細は 『通話内容ビュー』 と 『通話情報ビュー』 で構成されています。（[@fig:calldetail])  
各通話の通話詳細は、 RealtimeRecoder の通話開始アップロード後からアクセス可能となります。  
ただし、この時点ではシステムのどこからもアクセスするリンクは生成されていない状態のため URL を引数含めて直接入力しない限りはアクセスできません。また、[@fig:calldetail] のような完全な表示ではなく、通話内容ビューに何も表示されていない状態となります。  
後続の処理で、
	- RealTimeRecorder の通話終了アップロード → 通話検索結果表示  
	- StreamingRecognizer の認識完了アップロード → 通話内容ビュー表示  

	と状態が変わって行きます。  

	![通話詳細](images/2-4_detail.png){#fig:calldetail width=600px}  

	通話詳細のURLは、引数に会話識別子 (ConversationKey) を指定する必要があります。
	会話識別子により 通話データを一意に識別可能になります。  
	以下は、通話詳細の URL の書式例です。  

	```
	http://"Webサーバのホスト名もしくはIPアドレス"/SpeechVisualizer/Detail.aspx?key="通話識別子"
	```

	![](images/Tips.jpg){width=50px}　URL末尾に`#revision=”版数”`を追加することで版数を指定しての表示が可能です。省略した場合は最新版が表示されます。

####  2-4-2. 通話詳細の設定
1. [@tbl:detaildc] は、通話詳細の主な詳細設定です。

	No. | 設定分類 | 設定項目名       | デフォルト値 |特記事項
	---:|------------------|--------------|------|--
	1 | SpeechVisualizer - 通話詳細 |クイック編集 |FALSE |
	2 | SpeechVisualizer - 通話詳細 |コピー時にチャンネル名を含める |TRUE |
	3 | SpeechVisualizer - 通話詳細 |コピー時に開始時間を含める |TRUE |
	4 | SpeechVisualizer - 通話詳細 |コピー時に終端時間を含める |TRUE |
	5 | SpeechVisualizer - 通話詳細 |コピー時のオペレータラベルの文字列 |オペレータ |
	6 | SpeechVisualizer - 通話詳細 |コピー時のオペレータラベルを名前にする |FALSE |
	7 | SpeechVisualizer - 通話詳細 |コピー時のカスタマラベルの文字列 |カスタマ |
	8 | SpeechVisualizer - 通話詳細 |コピー時の時間フォーマット |0 |0:相対時間,1:絶対時間
	9 | SpeechVisualizer - 通話詳細 |シークバーに追随して感情解析を表示する |FALSE |
	10 | SpeechVisualizer - 通話詳細 |スクロールロック |FALSE |
	11 | SpeechVisualizer - 通話詳細 |セグメントを再生する場合に前後にもたせる余裕の秒数 |0.3 |(隠し項目)
	12 | SpeechVisualizer - 通話詳細 |デフォルトの拡大率 |0 |
	13 | SpeechVisualizer - 通話詳細 |ページ表示時に自動的に再生する |FALSE |
	14 | SpeechVisualizer - 通話詳細 |リピート再生 |FALSE |
	15 | SpeechVisualizer - 通話詳細 |感情解析を表示 |TRUE |
	16 | SpeechVisualizer - 通話詳細 |再生ボリューム |50,50;1,1 |
	17 | SpeechVisualizer - 通話詳細 |再生速度 |1 |
	18 | SpeechVisualizer - 通話詳細 |通話詳細に表示する感情解析階調線の数 |3 |2-4-3参照
	19 | SpeechVisualizer - 通話詳細 |通話詳細のアコーディオンに表示する感情スコア |2-4-4参照 |
	20 | SpeechVisualizer - 通話詳細 |通話詳細の折れ線グラフに表示する感情（オペレータ） |2-4-3参照 |
	21 | SpeechVisualizer - 通話詳細 |通話詳細の折れ線グラフに表示する感情（カスタマ） |2-4-3参照 |
	22 | SpeechVisualizer - 通話詳細 |通話情報に表示する追加の通話属性 |2-4-4参照 |
	23 | SpeechVisualizer - 通話詳細 |波形が表示可能な最大サンプル数 | 27000 | ※ 1
	24 | SpeechVisualizer - 通話詳細 |波形を表示 |TRUE |
	25 | SpeechVisualizer - 通話詳細 |話者アイコンを表示 |TRUE |

	: 座席表の詳細設定 {#tbl:detaildc}

	![](images/Check.png){width=50px} ※ 1 サンプル数、≒ **dot 数** です。  
	この設定項目は、通話詳細画面の波形を描画するのに必要な上下方向の長さ（高さ）のしきい値となります。  
	デフォルトでは、27000 dot を超える長さの波形の場合には描画されません。  
	ただし、この設定値は通話内容ビューの拡大率に対する相対的な値となりますので、絶対的に何分以上の通話なら表示しないという指定ではありません。  
	ちなみに、27000 dot は、デフォルトの表示倍率で 30分程度となりますが、通話内容ビューを拡大すると、波形表示可能な通話時間は短くなり、逆に縮小すると、波形表示可能な通話時間は長くなります。  
	<br />
1. ユーザ毎にカスタマイズが可能な設定  
	通話詳細の UI （[@fig:detailcustom]）からは、いくつかの詳細設定項目の個人別カスタム設定が可能です。

	![通話詳細個人設定](images/2-4_detail_custom.png){#fig:detailcustom width=200px}

	No. | 画面 UI  | デフォルト値 | [@tbl:detaildc] との関連 | 詳細
	---:|------------------------------------------------|--------------|---------|--
	1 | ページ表示時に自動的に再生する | 再生しない  | No.13 『ページ表示時に自動的に再生する』 |  
	2 | 通話全文コピーにチャンネル名を含める  | 含める  | No.2 『コピー時にチャンネル名を含める』|
	3 | 通話全文コピーに開始時間を含める  | 含める  | No.3 『コピー時に開始時間を含める』 |  
	4 | 通話全文コピーに終端時間を含める  | 含める  | No.4 『コピー時に終端時間を含める』 |  
	5 | 通話全文コピーで時間を絶対時間にする  | 相対時間にする  | No.8 『コピー時の時間フォーマット』 |  
	6 | 発話のクリックで編集を可能にする | 可能にしない  | No.1 『クイック編集』 |   
	7 | 波形を表示する  | 表示する  | No.23 『波形を表示』  |  
	8 | 感情解析を表示する  | 表示する  | No.15 『感情解析を表示』  |   
	9 | 話者アイコンを表示する  | 表示する  | No.24 『話者アイコンを表示』  |
	10 | 設定を保存   | ー  | 無し  | ユーザで変更後にクリックで設定反映  |

	: 通話詳細 UI からの設定のカスタマイズ {#tbl:detailui}

	![](images/Check.png){width=50px}　詳細設定で指定する場合も、通話詳細画面の UI からカスタマイズする場合でも、表示・非表示を切り替える項目は、利用を制限するための機能としては利用できません。  

	![](images/Tips.jpg){width=50px}　通話詳細の画面描画や再生時の動作が重たい場合、『波形を表示する』、『感情解析を表示する』、『話者アイコンを表示する』 を非表示設定にすることを推奨します。（必要に応じて、確認したい情報を表示に切り替えてください。）  

####  2-4-3. 通話内容ビューの表示と操作
通話内容ビューには認識テキストおよび感情が表示されます。 （[@fig:detailcallcontent]）

![通話内容ビュー](images/2-4_detail_callcontent.png){#fig:detailcallcontent width=400px}

1. 通話内容ビューでの通話イベント表示

	通話詳細の内容ビューには、[1-2-2. 通話表示機能](#1-2-2. 通話表示機能)と同様にRealTimeRecoderから連携された通話イベントが通話相手側に緑吹き出しで表示されます。
	[@tbl:detailevent] はSpeechvisualizerとOpertorAgentイベント名称の関連です。

	No.|SpeechVisualizerでのイベント名称|OpertorAgentでのイベント名称|備考
	---:|--------------|---------|--
	1 | 通話開始|通話開始|
	2 | 通話終了|通話終了<br/>通話エラー|通話詳細側は通話エラーでも通話終了と表記される
	3 | 保留開始|保留開始|
	4 | 保留解除|保留解除|
	5 | 保留終了|保留終了|
	6 | 転送完了|保留終了| 会話相手の通話属性として、転送先の情報 (amivoice.common.telephony.transfer.destination.phonenumber または amivoice.common.telephony.transfer.destination.name) が設定されていると「転送完了」との表記になります。
	7 | 保留エラー|保留エラー|
	:Speechvisualizerでの 通話イベント {#tbl:detailevent}

	![](images/Check.png){width=50px}　MediaScriber では、通話中イベントは連携されないため、保留を含めて通話中イベント情報は通話データに残りません。  
	リアルタイム認識構成においても、実際に起こったイベント通りに通話中イベントを表示できるかどうかは、呼制御通信の仕様や CTI イベントの仕様に依存します。  

1. 通話内容ビューに表示される感情  
以下の2箇所に表示されます。  
	- 通話内容ビュー : オペレータとカスタマの感情の時系列折れ線グラフ  
	- シークバー : 感情の時系列階調線  
表示する感情は [@tbl:detaildc] の 『通話詳細の折れ線グラフに表示する感情（オペレータ）』 ・ 『通話詳細の折れ線グラフに表示する感情（カスタマ）』 を参照しています。  
設定書式は以下です。  

		```
		nemesysco.qa5.callpriority
		nemesysco.qa5.excitement.positive
		nemesysco.qa5.energy.energetic
		```

		表示したい感情解析識別名を改行区切りで記述します。  
		設定値の上から順に 『通話詳細に表示する感情解析階調線の数』 だけ表示されます。  
		感情解析識別名については、[1-2-2. 通話表示機能　[@tbl:emolist]: 利用可能な感情一覧](#1-2-2. 通話表示機能) を参照してください。  
		デフォルトで用意されている配色とラベル名、線の太さ、点の形（circle もしくは square）を変更したい場合は以下の設定書式が使用できます。  

		```
		感情解析項目識別名|color=色を表す6桁の16進数|upperLabel=名称(数値高)|lowerLabel=名称(数値低)|border=線の太さ(整数値)|symbol=点の形(circle, square)
		例：nemesysco.qa5.excitement|color=EF5611|upperLabel=ポジティブ|lowerLabel=ネガティブ|border=2|symbol=square
		```
		デフォルトで定義されているラベル名称とカラーコードは [2-2-4. ホーム画面での感情解析表示　[@tbl:emocolor] ： ラベル名称とカラーコードの対応](#2-2-3.ホーム画面での感情解析表示)を参照してください。

		![](images/Check.png){width=50px}　『通話詳細の折れ線グラフに表示する感情（オペレータ）』 ・ 『通話詳細の折れ線グラフに表示する感情（カスタマ）』 の表示に使用される感情は 『Emotion』 フォルダに格納される拡張子『emo』のファイルのデータが使用されます。emo形式ファイルは表示可能な全感情の時系列データで構成されており、[@tbl:emoscore] の『保存する感情スコア』の設定にない感情であっても指定・表示が可能です。

		<br />  

		![](images/Check.png){width=50px}　『通話詳細に表示する感情解析階調線の数』 は、表示する感情が無くても、設定値分だけ表示領域を確保する仕様となっています。  
		そのため設定値を大きくするとテキストや波形表示領域を圧迫し、通話詳細画面表示が崩れてしまいます。([@fig:detailcallcontentng])  
		基本的には、表示数は変更せずに必要な情報に絞って活用してください。  

	![感情解析階調線の数を「256」とした場合](images/2-4_detail_callcontent_emong.png){#fig:detailcallcontentng width=400px}

1. 通話内容ビューのトラブルシューティング

	- 音声が再生できない

		No. | 原因| 対処 |
		----:|---------|-------|
		1 | wma ファイルにアクセスできない | wma ファイルがない、格納フォルダにアクセス制限がかかっている、NW の問題等が考えられます。wma ファイルの有無をご確認いただいたのち、セキュリティを確認してみてください。  
		2 | 非対応のブラウザを利用している | IE11 で実行してください。  
		3 | WindowsMediaPlayer がインストールされていない | 再生には WindowMediaPlayer が使用されます。インストールを実施してください。  
		4 | IE の WindowMediaPlayer アドオンが有効になっていない | インストールされていてもアドオンが有効化されていない場合は実行できません。IE の 「アドオンの管理」 から有効化してください。  

		: 音声再生のトラブルシューティング {#tbl:audioplaytrouble}

		![](images/Check.png){width=50px}　セキュアな通信下では、通話詳細画面へ遷移後、初回の音声再生は**ダウンロードが完了した後に通話の冒頭から再生されます**。途中再生を選択していても必ず冒頭から再生されます。

	- 波形が表示されない

		No. | 原因| 対処 |
		----:|---------|-------|
		1 | wavファイルにアクセスできない |wavファイルがない、格納フォルダにアクセス制限がかかっている、NWの問題等が考えられます。wavファイルの有無をご確認いただいたのち、セキュリティを確認してみてください。  
		2 | 『波形が表示可能な最大サンプル数』を超過している |おおよそ通話時間が30分の通話前後から、設定により波形表示が省略されます。| [@tbl:detaildc] の『波形が表示可能な最大サンプル数』の設定値を増やすことで表示できる上限を増やすことができますが、表示負荷とトレードオフになります。  
		3 | 波形の表示がOFFになっている   |環境によってデフォルトで表示しない設定にしている場合があります。通話詳細の UI （[@fig:detailcustom]）から表示設定に切り替えてください。  

		: 波形表示のトラブルシューティング {#tbl:waveviewtrouble}

####  2-4-4. 通話情報ビュー

1. 版数管理  
通話詳細では認識テキストを世代管理しています。  
内容は以下の通りです。  

	- 第1版  
		初回テキスト化時に作成されます。  
		通話テキストエクスポート時に『編集前の認識結果』としてエクスポートが可能です。  
		第1版の更新者は(StreamingRecognizer)となります。

	- 第2版以降  
		以下の操作を実施するたびに版数が追加・更新されます。  
		- 通話内容ビューからテキストを編集し、編集内容を確定する。  
		- 通話詳細画面から通話マスク機能を利用する。  
		- 通話の再認識を実施する。  

		また第1版からの編集内容が通話情報ビューの 『編集内容タブ』 に記載されます。  

	- 最新版  
		最後に作成された版が最新版となります。  
		通話テキストエクスポート時に 『認識結果』 としてエクスポートされます。  
		最新版でのみ認識テキストの修正と SpeechVisualize 上での通話マスク機能が利用可能です。  

		![](images/Tips.jpg){width=50px}　通話マスク機能を利用した場合、すべての版で同じ箇所がマスクされます。ただし、通話の再認識を実施した場合は **再認識以降の版でのみ** テキストのマスクが実施されます。  

		<br / >

1. 基本タブの項目について

	任意の通話属性が付与されている通話の場合、[1-2-2. 通話表示機能](#1-2-2. 通話表示機能) の [@tbl:callb2] の 『通話詳細』 列の **〇** の内容が項目としてデフォルトで表示されます。  
	項目名については[@tbl:detaildc] の 『通話情報に表示する追加の通話属性』 から変更が可能です。『通話情報に表示する追加の通話属性』 の設定書式は以下の通りです。

	```
	amivoice.common.reference.global.id=UCID
	amivoice.common.customer.name=名前
	amivoice.common.customer.phonenumber=電話番号
	amivoice.common.customer.gender=性別
	```
`"通話属性"="項目名"` の形式で改行区切りで記載します。

	![](images/Tips.jpg){width=50px}　 [@tbl:callb2] の 『通話詳細』 列で 〇 が付いていないものも追加可能です。ただし、『通話詳細』 に 〇 が付いていない項目は通話詳細上では設定が推奨されない項目になります。

	![](images/Tips.jpg){width=50px}　 項目 『録音サーバ』 および 『認識サーバ』 には、それぞれ録音および認識で使用されたサーバノードの 『ノード識別名』 が記載されます。  
	通話に紐づいた調査やログ回収を実施する場合には、この項目を確認することでどの録音・認識プロセスが使用されたか確認することができます。

1. 認識タブからの再認識

	通話詳細からの再認識の実行は下記条件を満たした場合にのみ実行できます。  
	- 指定フォルダに該当通話の通話識別名をファイル名としている再認識用音声 ( raw 形式 ) ファイルが存在する。
	- 実行ユーザに『再認識の登録』権限が付与されている。

	[@tbl:detailcallrecognition]は再認識用音声に関連する設定です。

	No. | 設定分類 | 設定項目名       | デフォルト値 |特記事項
	---:|------------------|--------------|------|--
	1 | RealTimeRecorder - 録音音声 | データ削除条件 |0(データ保存期間に従う) |
	2 | RealTimeRecorder - 録音音声 | データ保存期間 |7日 |0は設定NG
	: 再認識用音声の設定 {#tbl:detailcallrecognition}

	『データの削除条件』を満たす、もしくは『データの保存期間』を過ぎた場合は、再認識用音声は削除されます。
	再認識の設定は、通話詳細上で設定できる内容とControlCenter「認識オプションの設定」のプロジェクト単位の設定内容をもとに実行されます。  
	![](images/Check.png){width=50px}　raw形式音声ファイルは通話データと紐づいています。移動や切り取り、削除等を実施すると関連付けがなくなってしまいます。その場合、同じ場所に全く同じデータを再配置しても再認識は実施できなくなるため、直接ファイルを操作する場合はご注意ください。

1. 感情タブの表示内容
	感情が使用されているガジェットは、表示する感情を詳細設定から設定することができます。
[@tbl:detaildc] の 『通話詳細のアコーディオンに表示する感情スコア』 の設定書式は以下です。

	```
	nemesysco.qa5.callpriority.op
	nemesysco.qa5.excitement.positive.op
	nemesysco.qa5.energy.energetic.op
	nemesysco.qa5.callpriority.cu
	nemesysco.qa5.angry.cu
	nemesysco.qa5.content.cu
	nemesysco.qa5.embarrassment.cu
	nemesysco.qa5.anticipation.cu
	```
	表示したい感情スコア識別名と設定値を改行区切りで記述します。
	感情スコア識別名については、[1-2-2. 通話表示機能　[@tbl:emoscore]: 保存する感情スコア](#1-2-2. 通話表示機能) を参照してください。**表示可能な感情スコアは『保存する感情スコア』に定義された感情のみです。**
	定義されていない感情スコアを設定した場合は無視されます。

	デフォルトで用意されている配色とラベル名を変更したい場合は以下の設定書式が使用できます。

	```
	感情スコア識別名|color=6桁のHTMLカラーコード|label=ラベル名称
	例：nemesysco.qa5.angry.op|color=FF0000|label=OPの怒り
	```
	デフォルトで定義されているラベル名称とカラーコードは[2-2-3. ホーム画面での感情解析表示　 [@tbl:emocolor] : ラベル名称とカラーコードの対応](#2-2-3. ホーム画面での感情解析表示)を参照してください。

1. メッセージタブに表示されるメッセージについて

	メッセージタブには、**その通話中にメッセージ機能を利用してやり取りされていた内容のみ** が表示されます。
	表示メッセージは通話に紐づけられて保存されており、通話データ削除を合わせて、メッセージも削除されます。


### 2-5. SpeechVisualizer 座席表

#### 2-5-1. メインビュー
- 座席表は、座席モジュールを配置することで機能します。（[@fig:seatmap]）  
座席のレイアウトは、  
	- 拠点別  
	- 拠点-フロア別  
	- 拠点-フロア-業務別  

	など、ある程度大きな範囲で作成して、複数のモニタリングユーザで共有する運用を想定して機能実装しています。  
	モニタリングユーザ毎にレイアウトを用意することによるシステム的な障害はありませんが、運用が煩雑になります。  

	![座席表](images/2-5_seatmap.png){#fig:seatmap width=700px}  

	![](images/Tips.jpg){width=50px}　座席表のレイアウト変更は、画面の UI からだけではなく、座席表管理画面のエクスポート機能で出力できる、`map` ファイルを直接編集することでも実施できます。  
	このファイルは、テキストベースのファイルで UTF-8 の文字コードのファイルとなります。  
	正式なファイルフォーマットは非公開ですので、CSS 等のスキルがある方であれば **自己責任** で直接編集して頂いても問題ありません。  

#### 2-5-2. 座席表の設定
1. 詳細設定項目（[@tbl:seatmapdc]）  
設定分類は全て `座席表 - 詳細` です。

	No. | 設定項目名                                     | デフォルト値 | 特記事項
	---:|------------------------------------------------|--------------|---------
	  1 | Enter キーでメッセージを送信                                |     true         | 座席表画面の設定機能からユーザ毎にカスタマイズが可能です。
	  2 | データ送信最長間隔(状態通知)                              |     90000         | SpeechVisualizer が状態通知通信が維持されていることを通知するための最長間隔
	  3 | データ送信最長間隔(認識結果通知)                       |     90000         | StreamingRecognizer が認識結果通知通信が維持されていることを通知するための最長間隔
	  4 | デスクトップ通知レベル                                          |    999          | IE では 『音での通知』 になります。
	  5 | ピン留め時にメッセージパネルを開く                     |    false          |
	  6 | ピン留め時に認識結果パネルを開く                       |     true          |
	  7 | モニタリング対象タイムアウト                                  |    720          | {隠し項目} OperatorAgent が、自分をモニタしている座席表のタイムアウト判定をするための時間（No.9 とセットの項目）
	  8 | モニタリング対象更新間隔                                      |    300          | モニタリングリストの情報をサーバにアップロードする間隔
	  9 | 音声のバッファ時間                                                 |   0           | -
	 10 | 音声モニタリングの連続再生                                   |   false           | 座席表画面の設定機能からユーザ毎にカスタマイズが可能です。
	 11 | 古い形式のログを削除する                                      |   false           |
	 12 | 座席の認識結果を表示                                            |   true           | 座席表画面の設定機能からユーザ毎にカスタマイズが可能です。
	 13 | 再生ボリューム                                                         |  50,50,1,1            | 座席表画面の設定機能からユーザ毎にカスタマイズが可能です。
	 14 | 再接続間隔(状態通知)                                             |   60000           | 状態通知の受信タイムアウトが発生した際に、座席表が SpeechVisualizer に再接続を実施する間隔
	 15 | 再接続間隔(認識結果通知)                                      |   60000           | 認識結果通知の受信タイムアウトが発生した際に、座席表が StreamingRecognizer に再接続を実施する間隔
	 16 | 受信タイムアウト(状態通知)                                      |   120000           | SpeechVisualizer との状態通知通信が無効になったと判断する時間
	 17 | 受信タイムアウト(認識結果通知)                              |    120000          | StreamingRecognizer との認識結果通知通信が無効になったと判断する時間
	 18 | 接続待ち時間(認識結果通知)                                   |     5000          | StreamingRecognizer へのリクエストをまとめて行うための調整値
	 19 | 接続待ち追加時間のランダム値(認識結果通知)       |    2000          | [StreamingRecognizer へのリクエストをまとめて行うための調整値
	 20 | 通知音（アラート）                                                     |    ~/Resources/Notification/notification-alert.mp3          |
	 21 | 通知音（ヘルプ）                                                        |  ~/Resources/Notification/notification-help.mp3            |
	 22 | 通知音（未読メッセージ）                                          |   ~/Resources/Notification/notification-message.mp3           |
	 23 | 通話終了後の表示切替遅延時間                              |   10           |
	 24 | 認識結果に表示する感情（オペレータ）                     |    後述          |
	 25 | 認識結果に表示する感情（カスタマ）                        |   後述           |
	 26 | 表示する通話属性の一覧                                          |  -            |

	: 座席表の詳細設定 {#tbl:seatmapdc}

1. ユーザ毎にカスタマイズが可能な設定  
	座席表の UI （[@fig:seatmapcustom]）からは、いくつかの詳細設定項目の個人別カスタム設定が可能です。  

	![座席表画面個人設定](images/2-5_seatmap_custm.png){#fig:seatmapcustom width=400px}

	No. | 画面 UI  | デフォルト値 | [@tbl:seatmapdc] との関連 | 詳細
	---:|------------------------------------------------|--------------|---------|--
	1 | 音での通知（デスクトップ通知）  | 通知しない  | No.15 『デスクトップ通知レベル』 |  
	2 | ピン留め時の操作  | 認識結果パネルを開く  | No.6 『ピン留め時にメッセージパネルを開く』<br />No. 7 『ピン留め時に認識結果パネルを開く』  
	3 | 連続再生  | 無効  | No.16 『音声モニタリングの連続再生』 |  
	4 | Enter キーでメッセージを送信  | 有効  | No.1 『Enter キーでメッセージを送信』 |  
	5 | 座席の認識結果を表示  | 有効  | No.18 『座席の認識結果を表示』 |  
	6 | ボリュームコントロール  | ope / cus ともに 50%  | No.20 『再生ボリューム』 | 音声モニタリング時のボリューム  

	: 座席表 UI からの設定のカスタマイズ {#tbl:seatmapui}

#### 2-5-3. 座席表画面と通知の仕組  

座席表では、2種類の状態通知通信が管理されています。  
状態通知の基本的な仕組みについては、[1-3. OperatorAgent と ControlCenter の通信](#1-3-operatoragent-と-controlcenter-の通信) の 2. 状態通知のための通信経路 を参照してください。  
座席表の状態通知は、以下の2種類です。  

1. 状態通知  
座席表と SpeechVisualizer 間の通信 (ユーザのログインや、通話開始等のイベント)となります。  
関連設定は、[@tbl:seatmapdc] の  

	- 『データ送信最長間隔(状態通知)』  
	- 『受信タイムアウト(状態通知)』  
	- 『再接続間隔(状態通知)』  

	です。

1. 認識結果通知  
座席表と StreamingRecognizer 間の通信 (認識結果の取得)となります。（利用状態により ControlCenter を経由することもあります。）  
関連設定は、[@tbl:seatmapdc] の  

	- 『データ送信最長間隔(認識結果通知)』  
	- 『受信タイムアウト(認識結果通知)』  
	- 『再接続間隔(認識結果通知)』  

	です。

	認識結果通知通信では、接続時に指定した通話に対する認識結果しか取得出来ません。同じ StreamingRecognizer で別の通話の認識が始まった場合、既存の通信を切断し、新たに二つの通話を指定して通信を行う必要があります。この再接続は StreamingRecognizer 側の負荷が高めの処理になります。  
	StreamingRecognizer の負荷軽減のため、リクエストを減らすために、近い時間帯で始まった通話に対しては、なるべく一つにまとめてリクエストすることを期待し、認識が開始されてすぐに StreamingRecognizer に接続にいくのでは無く、少し待機して (別の通話が始まるかを待って) から接続に行きます。  
	そのための設定が、[@tbl:seatmapdc] の 『接続待ち時間(認識結果通知)』 と 『接続待ち追加時間のランダム値(認識結果通知)』 になります。  

これらの通知通信は、`Comet` という非同期通信で実装されています。  


```plantuml
@startuml
autonumber "00"

skinparam {
	shadowing false
	defaultFontName "Segoe UI, BIZ UDPゴシック, sans-serif"
	BackgroundColor #afeeee
	ParticipantBorderColor black
	LifeLineBorderColor black
	SequenceLifeLineBorderColor black
	ArrowColor black
	ActorBorderColor black
}

title シーケンス図.1 [座席モジュール Comet による非同期通信]\n

participant "座席モジュール\n内線番号 : 1000" as 1000
participant "StreamingRecognizer" as sr
participant "ControlCenter" as cc

1000 -[#red]>> cc ++ : モニタ開始要求
cc <-] : 通話開始\n（内線番号 1000）
1000 <<-[#red]- cc : 状態変更通知 <b>[通話開始]
1000 -> 1000 : 画面描画 <b>[通話開始]
1000 -[#blue]>> sr ++ : モニタリングテキスト要求

loop 音声が終わるまで
	sr -> sr : テキスト化
	1000 <<-[#blue]- sr : 認識結果通知
	1000 -> 1000 : 画面描画 <b>[認識結果]
end
cc <-] : 通話終了\n（内線番号 1000）
1000 <<-[#red]- cc : 状態変更通知 <b>[通話終了]
1000 -> 1000 : 画面描画 <b>[通話終了]
deactivate sr

@enduml
```

- 座席モジュールに対する通知通信は該当座席が画面に表示中のみ、表示サイズに応じて通知されます。  
座席表をズームアウトすると、座席モジュールに表示できる情報種別・量は減ります。  
認識結果テキストも表示可能な情報分のみを通信し、テキストが表示されない大きさまでズームアウトした場合には、認識結果通知通信は行いません。非ピン留め状態では、テキストの遡りはできません。（[@fig:seatsize]）  

	![](images/Tips.jpg){width=50px}　座席レイアウトを作成する際には、座席モジュールは少し大きめに作成するのがコツです。利用環境に合わせる必要があるので、定量的な数値を示すことは難しいですが **デフォルトの拡大率にて1画面に座席モジュールが10個見える程度** が適正なサイズとなります。  
	目安として、[@fig:seatsize] を参考にレイアウトしてください。  

	![座席モジュールサイズと表示内容](images/2-5_seatsize.png){#fig:seatsize width=400px}

	1. 拡大率デフォルトで10席表示 : 左の画像（表示されるセグメントは5～6個程度）  
	1. 拡大率を2段階縮小して1画面20席表示 : 中央の画像（表示されるセグメントは１個）  
	1. 拡大率を5段階縮小して1画面30席以上の表示 : 右の画像（セグメントは表示不可）  

	座席モジュールが多数1画面に表示された状態で、各座席モジュールに表示される発話テキストの量が多いとブラウザの負荷があがり、`PC 全体の処理が重たくなる可能性があります。`  
 - 座席モジュールをピン留め状態にすると、継続している通話のテキスト全文を通信し取得します。（[@fig:seatclip]）  
ピン留め操作実施時の詳細設定項目は、 [@tbl:seatmapdc] の 『ピン留め時にメッセージパネルを開く』 と 『ピン留め時に認識結果パネルを開く』 です。  

	![ピン留めした座席モジュール](images/2-5_seat_clip.png){#fig:seatclip width=300px}

 - アラートは座席モジュール上にのみ表示され、目視確認を行います。そのため、表示範囲外の座席モジュールのアラートは確認することができません。ただし、モニタリングリストを設定することにより有効化される 『通知リスト』 に対しては、表示範囲外の座席モジュールのアラートも通知されます。  
	![](images/Tips.jpg){width=50px}　画面を常に注視していなくても、アラートの発生をモニタするために、『通知リスト』 へ発報時に音声を再生することが可能です。発報音声に関わる詳細設定は [@tbl:seatmapdc] の 『通知音（アラート）』、『通知音（ヘルプ）』、『通知音（未読メッセージ）』 です。

	No. | 通信種別 | Destination | Protocol | 内容
	---:|------------------|--------------|-------|-------
	1   | 通常通信 | RealTimeRecorder  | RTSP | 音声モニタリングの通信です。デフォルトの通信ポートは 10554 ですが、`ノード管理 - ノード詳細 - RealTimeRecorder タブ` の 『ストリーミングポート番号』 を編集することで変更できます。関連する詳細設定は、 [@tbl:seatmapdc] の 『音声のバッファ時間』、『音声モニタリングの連続再生』、『再生ボリューム』 です。一部の設定は画面 UI からも変更可能です。  
	2   | 通常通信 | SpeechVisualizer | HTTP | 機能利用時に発生する通常の HTTP リクエストの他に、ブラウザタイムアウト延長のための Ping 通信を含みます。[@tbl:svlogin]の 『ブラウザログインを継続するための通知間隔』 で変更します。この仕組により、座席表画面を表示してあれば、タイムアウトすることはありません。ただし、PC が何らかの理由で通信が利用できない場合は例外となります。  
	3   | 状態変更通知 | SpeechVisualizer | HTTP | 画面全体の状態変更通知（モニタリングリスト・通知リスト・メッセージ受信・Avaya ステータス関連、通話関連イベント、各種アラート、ヘルプ、フォロー情報）  
	4   | 認識結果通知 | StreamingRecognizer | HTTP | テキストモニタリング、No. 5 とは状況の応じて使い分けられます。  
	5   | 認識結果通知 | SpeechVisualizer | HTTP | テキストモニタリング、No. 4 とは状況に応じて使い分けられます。  

	: 座席表通信一覧 {#tbl:sm_comm}

 - [@tbl:seatmapdc] の 『デスクトップ通知レベル』 について
この設定は、アラートやメッセージを受信した場合に、ブラウザの画面描画以外への通知先を増やす（デスクトップ通知）ものですが、利用するブラウザによって挙動が異なります。  

	1. Internet Explorer の場合  
デスクトップ通知の機能が実装されていません。  
座席表 UI の設定ダイアログでは、『音での通知』 という項目に変更され、設定レベルにより、音声鳴動での通知が追加されます。  
	1. Chrome、Edge（Chromium ベース） の場合  
		- SpeechVisualizer を HTTP で利用している場合  
Internet Explorer と同様、デスクトップ通知は利用できず音声鳴動での通知が追加されますが、UI 上の文言は 『デクトップ通知』 のままです。  
		- SpeechVisualizer を HTTPS で利用している場合  
設定レベルに応じて、デスクトップ通知が実行されます。（サーバ証明書は、警告の出ない状態で利用する必要があります。）
	1. Firefox の場合  
設定レベルに応じて、デスクトップ通知が実行されます。


#### 2-5-4. 座席モジュール
座席モジュールには以下の2つのタイプがあります。  
種類は、座席表管理で座席モジュールを配置する際に決定します。

1. 内線番号タイプ  
2. ユーザID タイプ  
	<br />
	![](images/Tips.jpg){width=50px}　内線番号タイプ と ユーザID タイプの座席モジュールの使い所  
座席（PC） と 電話機（内線番号）に静的にリンクしているケースでは、内線番号タイプを利用してください。（コンバージャー利用時でも、OperatorAgent インストール時に設定することをおすすめします。）  
フリーアドレスで、かつ PC 電話（ソフトフォン）を利用していて、PC と内線番号が動的にリンクするケース（AmazonConnect は例外で、動的リンクのケースですが Communication Suite の機能で内線番号タイプでの運用が可能です。）でのみ、ユーザID タイプの利用を想定しています。  

- 座席モジュールへの感情解析情報の表示  
表示のための設定は、[@tbl:seatmapdc] の 『認識結果に表示する感情（オペレータ）』、『認識結果に表示する感情（カスタマ）』 を参照してください。  
設定内容に関しては、 2-2-3. ホーム画面での感情解析表示 を参照してください。  

- 座席モジュールへの通話属性情報の表示  
表示のための設定は、[@tbl:seatmapdc] の 『表示する通話属性の一覧』 を参照してください。  
設定内容に関しては、2-3-3. 通話検索の結果 の 1. 通話属性 を参照してください。  

- 座席表と OperatorAgent  
座席表で、モニタリングリストを設定している場合、座席モジュールに対応する OperatorAgent には、モニタされていることが通知されています。  

#### 2-5-5. 座席表画面のログ
座席表画面は、クライアント側の実装量が多く、問題発生時にサーバ側のログだけでは原因究明に及ばないケースがあります。  
そのため、ブラウザの機能を利用することで、クライアント側に座席表動作時のログをテンポラリで保存しておき、必要時にログをダウンロードする機能が実装されています。  

- 座席表ログの取得方法  

	```
	http://serverhost/SpeechVisualizer/LogSave.aspx  
	```

	にアクセスし、`ログをファイルに保存` ボタンを押下すると生成されるリンクを右クリックし、リンク先を保存します。

- ログ出力のオプション  
通常は、座席表画面にアクセスし、表示しているだけでログが蓄積されます。  
より詳細なログを出力したい場合には、座席表画面を開く際に、以下のようにオプションをつけてアクセスします。  

	```
	http://serverhost/SpeechVisualizer/Monitor.aspx?--script-logger=debug  
	```

	出力されるログがデバッグ用に細かい粒度で出力されます。

- ログの出力場所など  
座席表ログは、ローカルPC上の特殊な領域に保存されます。（Communication Suite では制御できません。）  
特殊な領域とは、ブラウザに実装されている `ローカルストレージ` と定義されたスペースです。  
`ローカルストレージ` の仕様に関しては、ブラウザ毎に異なります。（以下は参考情報として Internet Explorer 11 のローカルストレージの仕様となります。）  

	```
	出力パス : C:\Users\ユーザ名\AppData\LocalLow\Microsoft\Internet Explorer\DOMStore\0FOJP942
	出力形式 : XML形式
	保存の限界 : 5242880 Bytes （キー名含む）
	手動削除の方法 : オプション ⇒ 「全般」タブ ⇒ 閲覧の履歴の削除にて、「クッキーとWebサイトデータ」を選択して削除後、IEを再起動する。
	```

	![](images/NOTICE.png){width=50px}　`ローカルストレージ` は、設定により利用を制限することが可能です。ログの出力ができない場合には、ローカルストレージが有効化されているか確認する必要があります。（以下は参考情報として、Internet Explorer11 及び Microsoft Edge で `ローカルストレージ` の設定を有効化する方法です。）  

	```
	1. [インターネットオプション] を開く
	2. [詳細設定] タブを開く
	3. セキュリティの [DOMストレージを有効にする] にチェックを入れる
	4. [OK] をクリックする
	5. Windows (PC) を再起動する
	```
	Chrome （Chromium 版 Edge） 及び Firefox では、バージョン毎にメニュー構成等が大きく異るケースがあるため、都度調査してください。

<div style="page-break-before:always"></div>

<hr/>

## 第3章 ControlCenter

### 3-1. ControlCenter のログイン

ControlCenterのログイン仕様については[2-1. SpeechVisualizer のログイン](#2-1. SpeechVisualizer のログイン)と同様となります。

### 3-2. ControlCenter ホーム

- ControlCenter ホーム画面の詳細設定項目は、[@tbl:cchomepara] です。

	No. | 設定分類 | 設定項目名       | 設定値 |内容
	---:|------------------|--------------|------|--
	1  | ControlCenter - ホーム | ホームモジュールのプロバイダ |  3-2-1 参照 | ホーム画面にガジェットを提供します。  
	2  | ControlCenter - ホーム | ホーム画面のレイアウト (配置情報)  | 3-2-2 参照 | ガジェット名と設定項目をもとに配置情報を指定します。 |  
	3  | ControlCenter - ホーム   | ホームモジュールの自動再読込間隔  | 600000 |各ホームモジュールが自動で再読込を行う場合の間隔の設定します。単位は「ミリ秒」、有効値「1以上の整数」を指定。 |

	: ホームモジュールと詳細設定との対応 {#tbl:cchomepara}

#### 3-2-1. ControlCenter ホーム画面のガジェットとプロバイダ

- ホーム画面に表示する、ガジェットを提供するのが 『プロバイダ』 です。  
[@tbl:cchomepara] の『ホームモジュールのプロバイダ』 の設定書式は以下です。

	```
	Profile
	Link
	Announcement
	```

	プロバイダ名を改行区切りで記述します。  設定可能なプロバイダ名は[2-2-1. SpeechVisualizer ホーム画面のガジェットとプロバイダ](#2-2-1. SpeechVisualizer ホーム画面のガジェットとプロバイダ)の [@tbl:homeprovider] 記載の『プロフィール』と『リンク』、『お知らせ』のみになります。


#### 3-2-2. ControlCenter ホーム画面のレイアウト情報

- ホーム画面のガジェット配置を設定できます。

	[@tbl:cchomepara] の『ホーム画面のレイアウト (配置情報)』 の設定書式は以下です。

	```
	Profile;Link;Announcement
	```
	記載されたガジェットは右から順にホーム画面右側の上部から配置されます。複数のガジェットを配置する場合は`,`で区切りで記述します。ガジェットは一つ前のガジェットの下部に追加されていきます。`;`で区切ることで1つ左に列を追加することができます(最大3列まで)。


	[@fig:cchome_defaultlayout] は上記のデフォルト設定の状態で初回ログインしたユーザのガジェットレイアウトです。

	![デフォルト設定のホーム画面レイアウト](images/3-2-home_defaultlayout.png){#fig:cchome_defaultlayout width=700px}


	その他、注意点は[2-2-2. SpeechVisualizer ホーム画面のレイアウト情報](#2-2-2. SpeechVisualizer ホーム画面のレイアウト情報) と同様です。


### 3-3. ログイン状況
プロジェクト別に、所属ユーザの OperatorAgent でのログイン状況の確認する機能です。

#### 3-3-1. ログイン状態の無効化
- この状態は、OperatorAgent でログイン状態にあるユーザのログイン状態を無効化（ログイン有効期限切れ）にする機能です。（[@fig:forcelogout] の 操作列のゴミ箱アイコン）  

![ログイン状態の無効化](images/3-3-1_loginstatus.png){#fig:forcelogout width=800px}  

- ログイン状態の無効化とは、サーバに保存されているログイン情報を有効期限切れとして扱う操作になります。  
この操作を実施することで、OperatorAgent が強制的に終了するわけではありません。  
強制ログオフ状態になったユーザ（OperatorAgent） の状態は以下の方法で確認できます。  

	1. ログイン状況画面  
![ログイン状況画面でログインを無効化されたユーザ](images/3-3_login-Timeout.png){#fig:lstimeout width=250px}  

	2. 座席表（座席モジュール）  
![ログイン状況画面でログインを無効化されたユーザ](images/3-3_sm-Timeout.png){#fig:smtimeout width=200px}  

- 強制ログオフの利用用途  
OperatorAgent の仕様として、  

	1. 同一ユーザで複数の OperatorAgent の起動ができない
	2. 同一内線番号を指定して、複数の OperatorAgent の起動ができない

	が挙げられます。  
	ログイン状態を無効化している間に、別の端末の OperatorAgent でログインしなおしたり、誤って指定された内線番号をリリースさせることができます。  
	**ログインを無効化された OperatorAgent は、上記の操作が発生すると自動的にシャットダウンされます**。

- ログインを無効化された OperatorAgent の挙動  
ログインの無効化操作のみでは、ログイン中の OperatorAgent は終了せず、動作を継続します。  
そのため、以下の動作を実施することにより、ログイン状態が再度有効化します。  

	1. メッセージ機能の利用  
		- メッセージの送信  
OperatorAgent からメッセージを送信することで、座席表ステータスとログイン状況のログイン状態は再び有効化します。  
		- メッセージの受信  
座席表から、タイムアウト状態の座席モジュールにメッセージを送信し、OperatorAgent 側で正常に受信した場合、座席表ステータスのみログイン状態が有効化します。
	1. 通話開始  
該当 OperatorAgent でログイン時に指定した内線番号で通話が開始すると、座席表及びログイン状況のログイン状態は有効化します。

### 3-4. ノード管理


#### 3-4-1. 各種プロセスの操作

1. プロセスの停止・開始  
	サービスを操作することなく、サービスのプロセス自体を操作します。  
	- サービス操作と比較した場合のメリット
		1. サービスの死活監視エージェントに発報されることなく、該当のアプリケーションの再起動が可能  
		1. サーバそのものにリモートデスクトップなどの必要が無い  
	- サービス操作と比較した場合のデメリット  
		1. サービスが停止している状態では操作ができない  
		1. 実装の不具合などにより、停止できない場合がある  
		1. 実装の不具合などにより、サービス開始と同等の初期化効果が無いことある  
1. 設定再読込  
	サービス再起動や上記のプロセス再起動を伴わずに、サービスプロセスの振る舞いに関する設定情報のリロードが実行できます。  
	- 設定再読込のメリット  
		1. サービスアプリケーションが停止状態にならないため、運用しながら設定をリロード可能
		1. クライアント版でも利用可能、全席に対して作用する
	- 設定再読込のデメリット  
		1. 全ての設定をリロードできるわけでは無い
		1. 設定反映に時間がかかる場合がある  
	- 設定再読込処理の負荷分散  
設定再読込処理を実行すると、設定取得しなおす必要がある旨が ControlCenter から RealTimeRecorder と StreamingRecognizer に通知されます。  
その際、Web サーバのネットワーク I/O ・ DB の負荷、ネットワーク帯域への負荷を考慮し、各クライアントが一斉にアクセスしないよう、ランダムアクセスする仕組みが実装されています。  
クライアント認識構成では、各クライアントは、設定取得通知を受信してから、[@tbl:random] の 『設定再読込遅延』 の設定値の間にランダムで待機したのちに設定データをリクエストします。  
ControlCenter へのアクセスが WAN を跨ぐケースでは、NW 速度などを考慮し、必要であれば 『設定再読込遅延』 を伸ばすなどして対応してください。  

		![](images/NOTICE.png){width=50px}　サーバ認識構成では、[@tbl:random] の設定値は利用されず、それぞれのプロセスが 0 ～ 3 秒の間でランダムに待機してから ControlCenter へ設定データをリクエストします。  
		ただし、大規模なサーバ構成の場合には、StreamingRecognizer プロセスは相当数になることが見込まれかつ、エンジンモード変更の際には、数十 MB のファイルが通信されることになります。  
		エンジンモード変更時には、StreamingRecognizer を1プロセスづつ手動で再起動するなどの対応を検討することも必要です。  

		No. | 設定分類 | 設定項目名       | デフォルト値 |特記事項
		---:|------------------|--------------|------|--
		1 | 共通 - サービス | 設定再読込遅延 | 5分 |  

		: クライアント認識構成の設定再読み込み時のランダムアクセス設定値 {#tbl:random}  

#### 3-4-2. 録音・認識状況

1. 認識キューの状態遷移

	```plantuml
	@startuml

	skinparam {
		shadowing false
		defaultFontName "Segoe UI, BIZ UDPゴシック, sans-serif"
		BackgroundColor #afeeee
		StateBackgroundColor white
		ParticipantBorderColor black
		ArrowColor black
		StateBorderColor black
	}

	title ステートチャート図.1 [リアルタイム処理の認識キューの状態遷移]\n

	[*] -> 認識前 : RR の通話開始\nアップロード
	認識前 --> 認識待機中 : CC からの認識依頼通知
	認識待機中 --> 認識中 : SR の認識開始\nアップロード\n通話継続中
	state "認識中（B）" as バッチ
	認識待機中 --> バッチ : SR の認識開始\nアップロード\n通話終了（異常系）
	バッチ : 認識要求種別はバッチ
	バッチ --> バッチ : テキスト化
	認識中 --> 認識完了 : 認識処理の正常終了
	バッチ --> 認識完了 : 認識処理の正常終了
	認識完了 --> [*] : SR の認識完了\nアップロード
	認識完了 --> FailedQueue : アップロード失敗（異常）
	FailedQueue : ステータスは認識完了
	認識完了 --> 認識完了 : アップロード失敗（正常）\nリトライを繰り返す
	認識中 --> 認識エラー : 処理エラー
	バッチ --> 認識エラー : 処理エラー

	state 認識中 {
	  state "認識中（R）" as real
	  state "認識中（B）_疑" as batch
	  batch : 認識要求種別はリアルタイム
	  real --> real : テキスト化
	  real --> batch : RR の通話終了\nアップロード
		batch --> batch : テキスト化
	}

	note right of FailedQueue
	  SR は、認識完了アップロードが失敗すると、
	  CC からのレスポンスのエラー内容を判断し、
	  アップロードをリトライし続けても
	  成功する見込みが無いと判断すると、
	  認識完了のステータスは変えずに
	  該当のアップロードデータを
	  Failed Queue フォルダへ移動する。
	end note

	@enduml
	```

	<br />

	- バッチ認識  
広義のバッチ認識 と狭義のバッチ認識 があります。  
狭義としてのバッチ認識は、MediaScriber での処理や復旧認識のように認識処理開始時点で既にテキスト化対象の通話が終了しており、認識音源に静的な音声ファイルを利用する処理です。この場合、認識要求種別が **バッチ** になります。（通話詳細の図いれるか？）  
認識要求種別が **バッチ** の場合には、StreamingRecognizer のノード設定の <font color="blue">『バッチ認識』</font> の設定値に従って処理されます。  
対して、ノード管理画面での認識中（B）は、広義として解釈します。  
これは、認識処理が通話中に行われているものをリアルタイム認識（認識中（R））として、それ以外は全てバッチ処理（認識中（B））とする考え方です。  
この中には、ステートチャート図.1 の "認識中（B）\_疑" が含まれます。  
"認識中（B）\_疑" は、RealTimeRecorder の通話録音は終了しているが、該当通話の認識処理が未完了の状態を指しています。この認識の認識要求種別は、 **リアルタイム** になります。そのため、この認識処理は StreamingRecognizer のノード設定の <font color="blue">『バッチ認識』</font> ではなく、<font color="red">『リアルタイム認識』</font> の設定値に従って処理されます。（StreamingRecognizer ノードの 『バッチ認識 - 最大同時認識数』 の **上限を越えて動作します。**）  

	- 認識中（B）\_疑  
リアルタイム認識であっても、通話終了前に認識処理が完了することはありませんので、この状態が 100% 異常であると断定することはできません。  
ただし、正常なパフォーマンスがキープされていてれば、認識中（B）\_疑 の状態が通話終了後 5 秒以上継続することは考えにくいです。  
その場合には、何らかの原因で認識処理のパフォーマンスが悪化している可能性があります。  

	<br />

	```plantuml
	@startuml

	skinparam {
		shadowing false
		defaultFontName "Segoe UI, BIZ UDPゴシック, sans-serif"
		BackgroundColor #fffacd
		StateBackgroundColor white
		ParticipantBorderColor black
		ArrowColor black
		StateBorderColor black
	}

	title ステートチャート図.2 [バッチ処理の認識キューの状態遷移]\n

	[*] -> 認識前 : RR の通話開始\nアップロード
	認識前 --> 認識待機中 : CC からの認識依頼通知
	state "認識中（B）" as バッチ
	認識待機中 --> バッチ : SR の認識開始\nアップロード
	バッチ : 認識要求種別はバッチ
	バッチ --> バッチ : テキスト化
	バッチ --> 認識完了 : 認識処理の正常終了
	認識完了 --> [*] : SR の認識完了\nアップロード
	認識完了 --> FailedQueue : アップロード失敗（異常）
	FailedQueue : ステータスは認識完了
	認識完了 --> 認識完了 : アップロード失敗（正常）\nリトライを繰り返す
	バッチ --> 認識エラー : 処理エラー

	note right of FailedQueue
	  SR は、認識完了アップロードが失敗すると、
	  CC からのレスポンスのエラー内容を判断し、
	  アップロードをリトライし続けても
	  成功する見込みが無いと判断すると、
	  認識完了のステータスは変えずに
	  該当のアップロードデータを
	  Failed Queue フォルダへ移動する。
	end note

	@enduml
	```

1. 各列のカウント数とシステム異常の把握
	- 録/認  
リアルタイム認識構成では、  
		$$ 録音カウント = 認識カウント $$ {#eq:rokunin}  

		となっているのが正常なカウント数です。（録音と認識のカウントのインクリメント・デクリメントのタイミングは同時ではないので若干のタイムラグはあります。）  
		ただし、サーバリアルタイム認識構成で、RealTimeRecorder を "N重化" している場合には、  

		$$ 録音カウント = 認識カウント × N $$ {#eq:rokunin2}

		が正常なカウント数になります。  
		逆に上記の数式が成り立っていない場合、状態の調査を行うべきだと考えます。  
		<br />
		録音カウントは、認識キューのステータスには全く依存せず、RealTimeRecorder で録音処理中の件数を表示します。  
		認識カウントは、認識キューのステータス 『認識中』 の件数を表示していますが、認識要求種別の区別は行いませんので、『認識中（<font color="red">R</font>/<font color="blue">B</font>）』 の合計値となります。  
		MediaScriber では、録音カウンタは回らないため、この項目からは動作していることがわかるだけで正常性や異常性を読み取ることはできません。

	- 認識前  
MediaScriber や復旧認識が動作している場合には、認識待機中（<font color="blue">B</font>） のカウンタが回るのは、想定の動作となります。（StreamingRecognizer の 『バッチ認識 - 最大同時認識数』 の合計以内であれば。）  
認識待機中（<font color="red">R</font>） がカウントアップされる場合、  
		1. 同時認識ライセンス数  
		1. StreamingRecognizer ノードの 『リアルタイム認識 - 最大同時認識数』 の設定値  
のいずれかに問題があることが疑われます。  
この状態が続くと、徐々に 認識中（B）\_疑 が増え続け、リアルタイムの通話の認識に StreamingRecognizer が割り当てられなくなり（認識中(<font color="red">R</font>) の数値がカウントアップされなくなります。)、システム障害に繋がります。  

	- 認識待機中  
この数値は顕著に変動しません。  
	- 認識中  
		- 認識中（<font color="red">R</font>） のカウント数  
[@eq:rokunin] or [@eq:rokunin2] が成り立っていれば、カウント数が増えていても問題はありません。  
そうでは無い場合、例えば、コールセンターの業務時間外などでもカウントが "0" にならない状態のときは、システム状況の調査をお薦めします。  

		- 認識中（<font color="blue">B</font>） のカウント数  
			- MediaScriber or 復旧処理中にカウンタが回るのは、正常の動作です。  
			- リアルタイム認識サーバ構成の稼働中に、このカウンタが回っている場合には、システム異常が発生していると考えらえれます。  
ケース的には以下の2例が考えられます。  
				1. DB でデッドロックが大量に発生し、DB パフォーマンスが低下している状態  
RealTimeRecorder の **通話開始アップロード** の処理が大幅に遅延し、認識キューのステータスが認識中（<font color="red">R</font>） にスムースに移行されなくなることが起因となります。  
Ver 3.2 未満でかつ、規模が大きい事例（同時 200通話以上）で顕著に発生します。  
					- 発生事象  
OperatorAgent や 座席表のリアルタイムテキストの配信ががシステム全体で遅延していきます。最終的にはほぼ全ての認識がリアルタイムで処理されなくなります。  
						ノード管理画面上では、認識中（<font color="red">R</font>） の数値がカウントアップされなくなり、システム全体の認識キューがバッチ認識（認識中（<font color="blue">B</font>））で処理されていきます。  
この場合のバッチ認識には、認識中（<font color="blue">B</font>）\_疑 の通話も多く含まれます。
					- 解消方法  
暫定的には、新しい通話が発生しなくなり、カウンタが "0" になれば、正常稼働の状態になります。  
ただし、システム全体の負荷があがることによって再度同じ状態になります。  
緊急にリアルタイム認識処理を復旧させたい場合に、SR のプロセスを部分的に徐々に停止しながら様子を見ます。どこかのタイミングで滞留数値が下がり始め、認識中（<font color="red">R</font>） のカウンタが増加しはじめます。  
恒久的に改善には、より DB パフォーマンスが改善された上位の Communication Suite のバージョンにアップデートするしかありません。
				1. StreamingRecognizer の認識処理が遅延する状態  
認識サーバのスペック不足により、一部の StreamingRecognizer のプロセスに、十分なハードウェアリソースを割り当てできなくなり、処理能力が大幅に低下することにより、多数の認識キューのステータスが 認識中（<font color="blue">B</font>）\_疑 に陥ってしまう状態です。
					- 発生事象  
全席ではありませんが、5割強程度の席の OperatorAgent でテキスト化が遅延します。通話終了後も認識処理が続きます。座席表の座席モジュールのリアルタイムテキストも同様の表示となります。  
					- 解消方法  
認識サーバの負荷を HW スペックに合わせて下げることで、認識中（<font color="blue">B</font>） のカウンタの滞留が徐々に解消されます。  
ただし、認識サーバの負荷を下げるには、RealTimeRecorder での録音数を減らす以外に無いため、運用中の解消は難しいです。  
恒久対応としては、認識サーバの増設が考えられますが、StreamingRecognizer の設定の見直しや、認識サーバの CPU リソースのチューニングが有効なケースもあります。（StreamingRecognizer 及び認識サーバのチューニングは、【要確認】（章番号などはあとから記載）StreamingRecognizer の章で後述します。）  

	- 認識完了  
<font color="red">R</font> と <font color="blue">B</font> で違いはなく、認識完了後に StreamingRecognizer から ControlCenter への認識完了のアップロード処理が滞っている場合に数値がカウントアップされて滞留します。  
構築当初で発生するケースとしては、ControlCenter - 詳細設定の 『設定分類 : 共通 - 記憶領域』 （[@tbl:kioku]）の設定ミスや未設定が原因となることが多いです。  

		No. | 設定項目名 | デフォルト値 | 特記事項
		-----:|----------------|-----------------|---------------
		1 | 再生に使用する音声ファイルのベースディレクトリのパス | ${cs, InstallRoot}\Audio\Playing |  
		2 | 波形の表示に使用する音声 (波形) ファイルのベースディレクトリのパス | ${cs, InstallRoot}\Audio\WaveShape |  
		3 | 感情解析結果ファイルのベースディレクトリのパス | ${cs, InstallRoot}\Audio\Emotion |  
		4 | 再生に使用する音声ファイルのアクセスに認証が必要かどうか | false |  
		5 | 波形の表示に使用する音声 (波形) ファイルのアクセスに認証が必要かどうか | false |  
		6 | 感情解析結果ファイルのアクセスに認証が必要かどうか | false |  
		7 | 記憶領域のアクセスに使用するユーザ | - |  
		8 | 記憶領域のアクセスに使用するパスワード | - |  

		: 設定分類 : 共通 - 記憶領域 {#tbl:kioku}

		運用中に発生する場合では、NAS や SAN のハードウェア障害・記憶領域の容量不足などが原因として考えられますが、後者の場合、データパージの仕組みにも問題が発生していることが考えられますので、併せて確認することを推奨します。  

		- 認識完了アップロードエラーについて  
		1. ネットワーク接続の問題が疑われると判断したケース  
StreamingRecognizer と他のサーバ間でネットワーク的に繋がらない等の場合、以下の間隔で処理をリトライします。  
			`3秒, 10秒, 30秒, 1分` 以降は、1分間隔  
		1. サーバの高負荷高負荷状態が疑われると判断したケース  
IIS からの HTTP レスポンスステータスコード が **503** 等の場合、以下の間隔で処理をリトライします。  
			`5分, 10分, 30分` 以降は、30分間隔  
		1. リトライしても成功の見込みが無いと判断したケース  
アップロードデータを、リトライ処理の対象にならない **アップロード失敗フォルダ** へと移動します。  
バージョンにより、他の不具合修正などとの兼ね合いで都度微調整されますので明確に線引できませんが、現行バージョンでは、以下事例は本ケースに含まれます。（他にも条件は存在します。）  
			- 認識結果をアップロードしようとしたが、DB に通話情報が無かった。  
			- 認識結果をアップロードしようとしたが、アップロードデータが壊れていた。  

			アップロード失敗フォルダに移動されたデータは自動復旧されません。  
アップロードエラーの原因に対処し、再度アップロードデータを通常のアップロードフォルダへ戻し、該当の StreamingRecognizer プロセスを再起動する必要があります。  
		1. それ以外のケース  
サーバ側で発生した予期しないエラー (DB 接続エラー、不具合によるエラーなど)をハンドリングした場合には、以下の間隔で処理をリトライします。  
			`3秒, 10秒, 1分, 5分, 10分, 1時間, 6時間, 24時間` 以降は、24時間間隔  

		StreamingRecognizer は一部のファイル作成処理ができなかった場合や、アップロード時に認識結果以外のファイルが無くなっていた場合でも、認識結果があればできる限り (存在するファイルのみを使用して) アップロードします。（通話詳細画面では認識結果しかないケース、波形表示のみ無いケースなどが発生する可能性があります。）  
		これら、部分アップロードが実行された場合、欠損したファイルがアップロードフォルダに補完されても部分的にリトライ処理は行われません。  
		該当の StreamingRecognizer のプロセスが再起動時にアップロード可能なデータが存在するとみなされた場合には、該当通話に対する再アップロードが実施されます。  

- 認識エラー  
StreamingRecognizer で認識処理中に処理を継続できない事象が発生した場合にこのステータスになります。  
認識エラーが発生するケースは、
	- 認識依頼を受けた StreamingRecognizer が、RealTimeRecorder に RTSP 接続できなかった場合  
この事例のみになります。  
![](images/Check.png){width=50px}　「認識エラー」 は、TaskRunner の `RecognitionQueueRecovery` で復旧する必要があります。（復旧するかどうかは原因を調査する必要があります。）  
復旧処理は再認識処理を伴いますので、該当通話の RealTimeRecorder の復旧用音声データ（Raw ファイル）が必要になります。  
Raw ファイルの保存期間はデフォルトで7日間（[@tbl:rr_raw]）ですので、復旧が必要なら早めの実施を推奨します。  
<br />  

	以下、『認識エラー』 にはなりませんが、特殊なケースをまとめたものになります。  
	1. StreamingRecognizer が認識依頼を受けた時点で、該当認識キューの通話を録音中の RealTimeRecorder が停止していた場合  
このケースでは、認識キューは削除されます。  
StreamingRecognizer 上ではエラーハンドリングされず、処理依頼がなかったことになります。  
復旧するには、「再認識」をかける必要がありますが、RealTimeRecorder 上に復旧用音源が残っているかにかかっています。
	1. StreamingRecognizer が認識処理中、RealTimeRecorder との接続が切れてしまった場合  
RealTimeRecorder 側の録音エラー（[1-2-2. 通話表示機能](#1-2-2. 通話表示機能)）や、RealTimeRecorder のクラッシュも含みます。  
認識処理としては、音源を受信できていた範囲で正常終了となります。  
RealTimeRecorder の通話終了アップロードが実行されれば、StreamingRecognizer から認識完了アップロードも実行されます。  
RTSP 通信の一時的な不通など、 NW 障害が原因の場合、通話録音は完全に行われていても、認識処理が不完全に終了していることもあります。  
不完全認識の場合、自動で復旧は行われませんので「再認識」処理により、不足している認識結果の補完する必要がありますが、本ケースでは、通話のステータスが正常終了になっていますので該当通話を特定するのが難しい状況になります。  
	1. StreamingRecognizer が認識処理中に停止した場合  
StreamingRecognizer のクラッシュや、認識エンジンモードの不具合なども含みます。  
該当の StreamingRecognizer の再起動時に、該当通話の認識キューは、『認識前』に戻ります。RealTimeRecorder 側の復旧用音源含めて認識が可能な状態であれば自動的に復旧します。

	<br />
	![](images/Check.png){width=50px}　「再認識」による復旧は、通話詳細の再認識機能か、TaskRunner の `RecognitionEnQueue` で実施可能です。（復旧するかどうかは原因を調査する必要があります。）  
	該当通話の RealTimeRecorder の復旧用音声データ（Raw ファイル）が必要になることは、自動で行われる復旧と同様です。  

	No. | 設定分類 | 設定項目名 | デフォルト値
	-----:|-------------|-----------------|---------------
	1 | RealTimeRecorder - 録音音声 | データ保存期間 | 7

	: RealTimeRecorder - 復旧用音声（Raw ファイル） の保存期間 {#tbl:rr_raw}

### 3-5. 認識オプションの設定  

#### 3-5-1. システム共通設定とプロジェクト別設定
認識オプションの設定は、システム共通の設定と各プロジェクト別に指定することができます。  
どちらで設定しても効果は変わりません。

![](images/NOTICE.png){width=50px}　認識オプションが未設定の場合、通話の録音は正常に行われますが、認識処理が実施されません。  
【要動作検証】 認識オプションが未設定の場合、通話の認識時にエラーが出力されないため、運用中に発生すると原因の特定が難しいことがあります。  

![](images/Tips.jpg){width=50px}　システム共通設定を設定しておくことのメリットとして、運用開始時に存在しなかった新規プロジェクトを運用中に作成しても個別に認識オプションの設定をすることなく運用することができます。  
システム共通設定は可能な限り設定するようにしてください。

#### 3-5-2. 表記の正規化

AmiVoice© のテキスト化処理の仕様で、半角文字の出力ができません。  
必要に応じて、テキスト出力時に半角に変換する必要があります。  
認識結果の見栄えを良くするために、基本的にはこのオプションは有効化する必要があります。  

- 表記の正規化を有効にすることで半角に変換されるキャラクター

	`アラビア数字`

- 表記の正規化を有効にしても全角表示を免れないキャラクター

	```
	".", ",", "+", "-", "=", "%", "&", "(", ")", "~", "<", ">", ";", "?", "!", "/", "\", "$", "#", "@", "'", "[", "]", "*"
	```

	![](images/Tips.jpg){width=50px}　表記の正規化を有効にしても全角となってしまうキャラクターの定義は、
	ControlCenter などの UI から変更することはできませんが、データベースに定義されています。  
	DB のレコードをクエリなどで修正することで半角に変換することが可能です。

#### 3-5-3. 音響学習

音響学習は、通話中に通話音声とリアルタイムに生成される認識結果を利用して、音響モデルを話者にアダプテーションする機能です。  
教師無し学習を行うため、全ての認識結果を利用することは適切ではないので、設定項目 『音響学習に使用する最低信頼度』 に設定した信頼度を元に、該当の認識結果をアダプテーションデータに利用するか否かを決定します。（認識結果の信頼度がしきい値以上であればアダプテーションデータとして採用します。）  
学習方法は、

1. 恒久的  
アダプテーションデータは、話者（ユーザ）に紐付いて保存されます。  
話せば話すほど、話者の音響特性にアダプテーションされ、誤認識が改善され認識精度の向上が見込めます。  

	![](images/NOTICE.png){width=50px}  

	1. GMM 音響モデルエンジンでのみ利用できます。それ以外のエンジンで利用するとアダプテーションは行われません。  
	1. ユーザデータに紐付いて保存されます。OperatorAgent を利用していないときには学習されません。  
	1. OperatorAgent にログイン中のユーザと別のユーザで通話を実施してしまうと、異なる特徴にアダプテーションしてしまうため、認識精度の低下に繋がります。  
	![](images/Check.png){width=50px}　アダプテーションデータはユーザ詳細画面の 『音響学習の削除』 を押すとクリアされます。（[@fig:onkyo_clear]）

	![アダプテーションデータの削除](images/3-5_user_profile.png){#fig:onkyo_clear width=400px}

2. 一時的  
アダプテーションデータのライフサイクルがアダプテーションを実施した通話のみに限定されます。  
通話が進むにつれて精度の誤認識が改善され、向上効果が見込めます。  
あらゆる音響モデルで利用可能です。


#### 3-5-4. 感情解析

感情解析に関わるオプションは以下の4つです。  

1. 感情解析  
感情解析処理の有効化・無効化を指定します。  
特別な理由で感情解析ライセンスを未所持のまま、システムを利用する場合には必ず **無効** にしてください。
1. 感情解析で無視する冒頭区間  
この機能は以下のような理由で設定します。  
	- 感情解析のライセンスを無駄に消費しないために、短い通話では感情解析処理を実施しないようにする  
	- より精度の高い感情解析処理を実施したい  
	通話の冒頭では、リンギング音・フック音などのノイズが入りやすく適切ではない感情データが混入しがちです。冒頭の感情解析を行わないことによりより正確な感情解析情報が残せます。  
1. 感情解析の開始区間  
感情解析値の平均値を算出するための開始時間  
1. 感情解析の終了区間  
感情解析値の平均値を算出するための終了時間  
	<br />

	上記 2 ～ 4 を図示したものが以下の [@fig:option_emotion] です。

	![感情解析の平均値算出に利用される発話区間](images/3-5_R_Option_Emotion.png){#fig:option_emotion width=700px}

**※ 感情解析の開始・終了区間はオペレータとカスタマで別の値を設定した場合は正しく動作しません。両方で同じ値で設定してご利用ください。**  


### 3-6. エクスポート


### 3-7. ライセンス状況

#### 3-7-1. Communication Suite ライセンス  
- Communication Suite ライセンス  
	登録されているライセンスは ControlCenter / システム管理 / ライセンス状況のホーム画面より確認できます。  
	各ライセンスの説明は[@tbl:riyouLicense] の通りです。  

	No. | ライセンス名 | 説明
	--:|-----------------|---------------------------|
	1 | AmiVoice Communication Suite Core |Core ライセンスです。<br>算出根拠：AmiVoiceCommunicationSuite データベース毎に1ライセンス必要です。  |  
	2 | AmiVoice OperatorAgent サーバ版 | サーバ版で OperatorAgent を利用するライセンスです。<br>算出根拠：OperatorAgent をインストールするPCの台数分必要です。<br>※仮想環境で利用する場合は<br>ライセンスのカウント方式を **インストール台数** から **同時起動数** に変更できます。<br>仮想環境算出根拠：OperatorAgent の同時起動数分。（No.3 のRealTimeRecorder のライセンス数分は最低限ライセンスを購入して頂く必要があります）
	3 | AmiVoice RealTimeRecorder |サーバ版で録音するためのライセンスです。<br>算出根拠：録音対象としてシステムに登録する内線番号の数だけ必要です。
	4 | AmiVoice StreamingRecognizer |サーバ版で音声認識するためのライセンスです。<br>算出根拠：同時認識する数だけ必要です。（最大同時通話数とイコール）
	5 | AmiVoice OperatorAgent コンバージャ版 |クライアント版で OperatorAgent を利用するライセンスです。本ライセンスに録音認識するためのライセンスも含まれています。<br>算出根拠：OperatorAgent をインストールするPCの台数分必要です。
	6 | AmiVoice MediaScriber | MediaScriber で音声認識するためのライセンスです。<br>本ライセンスに録音認識するためのライセンスも含まれています。<br>算出根拠：認識完了までの時間（要件）により、ライセンス数が変わります。最大録音時間 ÷ 認識処理実施時間

	: Communication Suiteライセンス一覧 {#tbl:riyouLicense}

- ライセンスの使用  

	No. | ライセンス名 |ライセンスの使用タイミング
	--:|-----------------|---------------------------|
	1 | AmiVoice Communication Suite Core |なし（あとでもう少し書く）  |  
	2 | AmiVoice OperatorAgent サーバ版 |OperatorAgent インストール PC で初回ログイン処理を実施したタイミングで PC 毎に1つ使用。仮想環境の場合はライセンス使用を同時ログイン処理毎に変更可能。|  
	3 | AmiVoice RealTimeRecorder |「内線番号管理」に内線番号を追加する毎に1つ使用  |  
	3 | AmiVoice StreamingRecognizer |ノード管理 - ノード詳細の「リアルタイム認識 - 最大同時処理数」の設定値分のライセンスを使用  |  
	3 | AmiVoice OperatorAgent コンバージャ版 |OperatorAgent インストール PC で初回ログイン処理を実施したタイミングで PC 毎に1つ使用 |  


	![](images/Tips.jpg){width=50px}　下記ライセンスは見積もり上のみの記載であり、「ライセンス状況」の画面には表示されません。  
	- AmiVoice RealTimeRecorder（冗長）  
	- AmiVoice Web Client API （ランタイム）  
	- AmiVoice Json API（ランタイム）  
	- AmiVoice Client SDK（ランタイム）  
<br>
- CommunicationSuite ライセンスの登録  
	ライセンスの登録時にはライセンスファイルが必要です。TaskRunner の`LicenseRegister` コマンドを実行してチャレンジコードを発行します。  
	チャレンジコードに対応するワンタイムパスワードを専用IVRより取得してライセンスを有効化します。  
	- ワンタイムパスワード専用IVR  
	連絡先：050-3160-0203  
	パートナーコード：xxxx （パートナー様ごとに用意されている番号をご利用ください）  

#### 3-7-2. 感情解析ライセンス

- 感情解析ライセンス管理  

	購入ライセンスに合わせて使用可能なライセンス数が月単位で決まっています。使用可能なライセンス数は  
	ContronCenter / システム管理 / ライセンス状況 /感情解析ライセンス管理 から確認できます。（[@fig:kanjo]）  
	今月の感情解析通話数は毎月1日の午前 9 時にリセットされて「 0 」に戻ります。  
	ライセンス数を超過した場合は翌月のライセンスリセットまで、それ以降の通話は感情解析されません。  

	![感情解析ライセンス管理 画面](images/2-1-感情ライセンス.png){#fig:kanjo width=800px}  

- 感情解析ライセンス数の算出式  
	- 購入が必要なライセンス数の算出根拠となる数値  
	1. サーバ版 / クライアント版の場合  
	サーバ版は RealTimeRecorder ライセンス数 1 につき、 3,000 回の感情解析処理 / 月 で提供されます。  
	クライアント版は OperatorAgent ライセンス数 1 につき、3,000 回の感情解析処理 / 月 で提供されます。  
	1. MediaScriber の場合  
	MediaScriber ライセンスの最初の1ライセンス のみ 30,000 回の感情解析処理 / 月で提供されます。  
	※ 以降1ライセンス追加ごとに 3,000 ずつ追加されます。  
	![](images/Tips.jpg){width=50px}　RaalTimeRecorder 1ライセンスごとに処理可能なライセンス数を管理しているわけではなく、発行されたライセンス数の合計をもとに、月ごとに処理可能なライセンス数が管理されます。  
<br>
- 使用ライセンス  
	録音開始した通話を **StreamingRecognizer が認識開始したタイミング** でライセンスが使用されます。  
	通話時に電話機操作を実施しなければ基本的には1ライセンスの使用です  
	電話機操作を実施した場合のライセンス使用は[@fig:kanjoz2] の通りです。  

	![電話機操作時の感情解析ライセンスの使用](images/3-7-kanjoz.png){#fig:kanjoz2 width=1000px}

	![](images/Check.png){width=50px}　電話機操作を実施しなかった場合でもライセンスが複数使用するケースがあります。（関連設定は [@tbl:kanjouLicense1] 参照）
	- 「1通話の最大録音時間」機能により通話が複数に分割された場合
	- 　再認識した通話（認識オプションで「感情解析が未処理の場合のみ有効」ではなく、「有効」の場合）
	- 「短い通話と判断する通話時間」機能によって結果的に通話は作成されずキャンセルされたが、認識処理が行われた場合

	![](images/Tips.jpg){width=50px}　ライセンス使用の例外として認識オプションの「感情解析で無視する冒頭区間」の範囲内で通話が終了した場合には感情解析ライセンスは使用されません。（[3-5-4. 感情解析の「感情解析で無視する冒頭区間」を参照](#3-5-4. 感情解析参照)）  


	No. | 設定分類 | 設定項目名 | 説明
	--:|-------------|------|----------------------------|
	1 |RealTimeRecorder - 録音音声 | 1通話の最大録音時間 |以下2つより選択<br>0（録音終了）<br>1（別の通話として継続）  
	2 |RealTimeRecorder - 録音音声 | 最大録音時間を超えたときの扱い |No.1の設定で1（別の通話として継続）を選択した場合に設定値（秒）を超えると通話が分割されます。  |  
	3 |RealTimeRecorder - 録音音声 | 短い通話と判断する通話時間  |設定値（ミリ秒）以下の通話時間の通話は作成されません。

	: ContolCenter 詳細設定の感情解析ライセンス使用に関連する設定 {#tbl:kanjouLicense1}  

- 感情解析ライセンスの登録  
	TaskRunner の`NemesyscoPreparation --regist` コマンドを実行して感情解析システムIDを発行します。  
	アクティベーションコード入手後、[@fig:kanjo] 感情解析ライセンス画面の「アクティベート」ボタンよりアクティベーションコードを入力して感情解析ライセンスを登録します。感情解析ライセンスは ControlCenter をインストールするWEBサーバごとに登録が必要です。ロードバランサなどでWEBサーバを冗長化する場合には、それぞれのWEBサーバに感情解析ライセンスを半分ずつに分けて登録します。  
<br>
	登録時の用途によって提供されるアクティベーションコードのフォーマットが異なります。  
	-  新規登録時（無期限のライセンス）`NMSF:XXXXXXXXXX:PNMS!XXXXXXXXXXXXXXXXXXX:QA021000166`
	-  新規登録時（期限付きライセンス）`NMSF:XXXXXXXXXX:PNMS!XXXXXXXXXXXXXXXXXXX:QA021000166:ZNMS!XXXXXXXXXXXXXXXXXXX`
	-  増席 / 期限延長（追加ライセンス） `PNMS!XXXXXXXXXXXXXXXXXXX`

	![](images/Check.png){width=50px}　アクティベーション登録直後は [@fig:kanjo] の状態欄が	![](images/3-7-tokei.png){width=25px} の「アクティベーション待ち」となり  
	その後の新規通話で感情解析が行われた時に ![](images/3-7-tokei2.png){width=20px}  「アクティベーション済」となり使用ライセンス数が表示されます。  

	<br />



### 3-8. レポート
CommnicationSuite のアカウントに関する履歴を表示します。  

#### 3-8-1. レポートの保存  
- レポートの保存先  
	CommunicationSuiteデータベース（Data.mdf, Index.ndf, LargeObject.ndf）に保存されます。  
	どれか１つのファイルのみに保存されるわけではありません。  
<br>
- レポートの保存期間  
  レポートの保存期間はログイン履歴と通話操作履歴で異なります。
	- ログイン履歴・・・削除されることはありません。
	- 通話操作履歴・・・TaskRunner の削除処理で操作履歴の対象通話が削除されると操作履歴も削除されます。


### 3-9. メンテナンスモード


## 第4章 RealtimeRecoder

### 4-1. 通話録音機能

#### 4-1-1. 通話プロバイダ

##### サーバパケットキャプチャ

1. Avaya  
1. Avaya AES
1. Avaya APC  
Avaya Proactive Contact のイベントドリブンで、録音を制御します。  
1. SIP
1. SIP CTstage連携
1. SIP T-Server連携
1. SIP OAI連携
1. SIP CIC連携
1. RTP  
呼制御プロトコルを解析しないため、通話イベントの判定ができません。  
利用シーンは、RealTimeRecorder が解析に対応していない呼制御プロトコルを利用している電話環境下に限定されます。  

	- 制限事項
		- 保留イベントの検出ができないため  
		　保留関連のアラート機能は利用できません  
		　保留関連の評価項目（通話品質評価機能）が利用できません  
		　保留関連のレポート機能が利用できません  
		　保留毎に通話録音が停止するため、通話データの件数と通話件数と一致しません  
		- 内線通話を録音することができません  
RealTimeRecorder で内線通話のパケットをキャプチャしないようにするには、

1. RTP AES

##### サーバアクティブ録音
1. Amazon Connect連携

##### クライアントパケットキャプチャ
1. Avaya
1. SIP
1. SLC を利用する場合

##### 音声デバイス型
1. コンバージャー
1. その他音声デバイス

##### 音声デバイス型


#### 4-1-2. パケットキャプチャ


#### 4-1-3. 拡張設定


#### 4-1-4. 録音音声

### 4-2. 配信機能

#### 4-2-1. RTSP サーバ
#### 4-2-2. 音声データのステートチャート
