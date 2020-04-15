---
documentclass: ltjsarticle
output: pdf_document
figPrefix: '図.'
figureTitle: 図
tableTitle: 表
tblPrefix: '表.'
---

# 詳解 Communication Suite 機能編



## 目次

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [詳解 Communication Suite 機能編](#詳解-communication-suite-機能編)
	- [目次](#目次)
	- [序章 トレーニングにあたって](#序章-)
		- [トレーニングの目的](#目的)
		- [トレーニング中の諸注意](#中諸注意)
	- [第1章 OperatorAgent](#第1章-operatoragent)
		- [1-1. OperatorAgent のログイン](#1-1-operatoragent-)
			- [1-1-1. OperatorAgent でログインすることの意味](#1-1-1-operatoragent-意味)
			- [1-1-2. OperatorAgent のログインに関連する ControlCenter の詳細設定項目](#1-1-2-operatoragent-関連-controlcenter-詳細設定項目)
			- [1-1-3. プロジェクトの選択](#1-1-3-選択)
			- [1-1-4. 統合 Windows 認証](#1-1-4-統合-windows-認証)
			- [1-1-5. OperatorAgent 自動ログイン（統合 Windows 認証を利用しない）](#1-1-5-operatoragent-自動統合-windows-認証利用)
			- [1-1-6. 本節のまとめ](#1-1-6-本節)
		- [1-2. OperatorAgent のメイン画面](#1-2-operatoragent-画面)
			- [1-2-1.OperatorAgent メニュー](#1-2-1operatoragent-)
			- [1-2-2. 通話表示機能](#1-2-2-通話表示機能)
			- [1-2-3. 通話終了後の機能](#1-2-3-通話終了後機能)
			- [1-2-4. OperatorAgent の起動・終了時の動作](#1-2-4-operatoragent-起動終了時動作)
			- [1-2-5. OperatorAgent からのコマンド実行](#1-2-5-operatoragent-実行)
			- [1-2-6. コマンドラインからの OperatorAgent 操作](#1-2-6-operatoragent-操作)
			- [1-2-7. OperatorAgent のインストール](#1-2-7-operatoragent-)

<!-- /TOC -->

## 序章 トレーニングにあたって

### トレーニングの目的

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

[@fig:login] は、OperatorAgent の基本的なログイン画面となります。

![基本のログイン画面](images/1-1-operatoragent-baselogin.png){#fig:login width=400px}

#### 1-1-2. OperatorAgent のログインに関連する ControlCenter の詳細設定項目

No. | 設定項目名       | デフォルト値 | 内容 |
---:|------------------|--------------|------|
1   |  ユーザーIDの保存 | false        | 最後にログイン成功した ユーザ ID を保存する |
2   |  パスワードの保存 | false        | 最後にログイン成功したパスワードを保存する |
3   |  自動ログイン | false        | 保存済みのユーザ ID とパスワード（と内線番号）で自動ログインする |
4   |  内線番号の指定 | false        | ログインダイアログに内線番号入力欄を表示する |
5   |  内線番号の情報が必要かどうか | S        | R = 必須, S = サーバ版では必須, N = 入力しない |
6   |  内線番号の保存 | false        | 最後にログイン成功した内線番号を保存する |

: 詳細設定 設定分 : OperatorAgent - ログイン {#tbl:table}  

 - [@tbl:table] の No.4 『内線番号の指定』 を **"true"** にすることで、ログインダイアログに内線番号入力欄が追加されます。（[@fig:naisenari]。VDI 等のシンクライアント環境で、クライアント PC と電話機を固定で紐付けできない場合に有効です。）  

![内線番号入力可能なログイン画面](images/2020/02/1-1-operatoragent-naisenlogin.png){#fig:naisenari width=400px}

  - OperatorAgent のインストール時に内線番号を指定している場合には、指定番号が内線番号入力欄に表示されます。（[@tbl:table] の No.6 『内線番号の保存』 が **"false"** の場合も表示されます。）  
  変更すると、ログイン出来なくなったり、他の席の電話番号と紐付けされてしまうので注意してください。
  - [@tbl:table] の No.4 『内線番号の指定』 が **"false"** の場合でも、インストール時に内線番号が指定されていない場合で、かつ [@tbl:table] の No.5 『内線番号の情報が必要かどうか』 が "S" でかつサーバ版利用時 or "R" の場合には、内線番号入力欄が強制的に表示されます。
  - [@tbl:table] の No.1 ユーザID は、  

    ```
    %USERPROFILE%/AppData/Local/Advanced_Media,_Inc/OperatorAgent.exe_StrongName_(長い文字列)/(バージョン番号)/user.config  
    ```
  の **LoginSettings/@LatestLoginUserId** に保存されます。 [^2] （この設定値は最後にログインに成功したユーザIDとなります。）

   - [@tbl:table]  の No.2 ログインパスワードは、Windows の  
	 [コントロールパネル] → [ユーザー アカウント] → [資格情報マネージャー]  
  に自動入力されたユーザIDに対応するパスワードが保存されます。（ [@fig:shikaku]。この設定値は最後にログインに成功したパスワードとなります。）  

![資格情報マネージャーのログイン情報](images/1-1-win_shikaku.png){#fig:shikaku width=500px}  

   - [@tbl:table]  の No.6 内線番号は、  

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
- [1-1-2. OperatorAgent のログイン機能に関連する ControlCenter の詳細設定項目](#1-1-2-operatoragent-機能関連-controlcenter-詳細設定項目)  ：  [@tbl:table] の No.3 『自動ログイン』 が有効になっている場合には、統合 Windows 認証 を利用していなくてもログイン処理を省略可能です。  
	<br />  

	```plantuml
	@startuml
	skinparam {
	defaultFontName BIZ UDPゴシック
	}
	skinparam backgroundColor #fffacd
	skinparam activity  {
	BackgroundColor #afeeee
	BorderColor #000080
	}
	title アクティビティ図.1 [OA 自動ログイン判定]\n


	start
	:OperatorAgent 起動;
	if (内線番号の情報が必要かどうか) then (不要 ： 設定値『N』)
	else (\n必要)
		if (設定値 『S』 or 『R』) then (設定値『S』)
			if (サーバ版？) then (\nYES)
				if (内線番号) then (\n未入力)
					-ログインダイアログ表示
					end
				else (自動入力済)
				endif
			else (クライアント版)
			endif
		else (設定値『R』)
			if (内線番号) then (\n未入力)
				-ログインダイアログ表示
				end
			else (自動入力済)
			endif
		endif
	endif
	if (\nユーザIDとパスワードの両方が\n自動入力されている\n) then (YES)
		if (自動ログインの設定は有効か？) then (有効)
		else (\n無効)
		  -ログインダイアログ表示
			end
		endif
	else (いずれかもしくは両方が未入力)
		if (\nコマンドライン実行(※) で、引数により\nユーザIDとパスワードが設定されている\n) then (YES)
			if (自動ログインの設定は有効か？) then (有効)
			else (\n無効)
			  -ログインダイアログ表示
				end
			endif
		else
			-ログインダイアログ表示
			end
		endif
	endif
	#plum:自動ログイン実行;
	floating note right: ※ コマンドライン引数については \n 1-2-6. コマンドラインからの OperatorAgent 操作 \nを参照して下さい。
	@enduml
	```

	<br />
- [@tbl:oalogin] は、OperatorAgent の正常系ログインエラーをまとめたものです。（異常系は含んでいません。）

	No. | 事由                 | ログインダイアログのメッセージ       | デバッグログへの出力 |
---:|---------------------|------------------|--------------|
1   | ユーザ ID 誤り | OperatorAgent サービスにログインできませんでした | ステータス: 43031 ユーザID 'XXX'、またはパスワードが違います。 |
2   | パスワード誤り | OperatorAgent サービスにログインできませんでした | ステータス: 43031 ユーザID 'XXX'、またはパスワードが違います。 |
3   | 内線番号誤り | OperatorAgent サービスにログインできませんでした | ステータス: 42601 指定した内線番号 'NNN' は削除されたか、登録されていません。 |
4   | 所属プロジェクト無し | 所属するプロジェクトがありません | 出力無し|
5   | OperatorAgent の利用権限無し | OperatorAgent サービスにログインできませんでした | ステータス: 43207 権限のあるプロジェクトがありません。 |
6   | ユーザの有効期限切れ | OperatorAgent サービスにログインできませんでした | ステータス: 43031 ユーザID 'XXX'、またはパスワードが違います。 |
7   | ユーザの重複ログイン | このユーザは他の PC で利用中です | 43204 ユーザは別のホストからすでにログインしています。 |
8   | 内線番号の重複ログイン | OperatorAgent サービスにログインできませんでした | ステータス: 43205 指定された回線は現在使用されています。 |
9   | Communication Suite ユーザ未登録 | OperatorAgent サービスにログインできませんでした | このエラーは、IIS に入力されたユーザー名またはパスワードが無効であるか、または IIS がユーザーを認証するのためにそのユーザー名およびパスワードを使用できないときに発生します。 |
10   | ライセンス違反 | OperatorAgent サービスにログインできませんでした | 【要確認】 ステータス: XXXXX ○○○。 |  

	: OperatorAgent のログイン失敗事由 {#tbl:oalogin}  

	※ [@tbl:oalogin] の No.1、No.2 は **フォーム認証利用時のみ** のエラーとなります。  
※  [@tbl:oalogin] の No.9 は **統合 Windows 認証利用時のみ** のエラーとなります。


#### 1-1-6. 本節のまとめ
  - [ ] OperatorAgent でのログインに関わる設定項目について理解ができた。  
- [ ] OperatorAgent でのログインが単に認証しているだけでは無いことが理解できた。
- [ ] OperatorAgent の自動ログインについて理解ができた。  
- [ ] OperatorAgent にログインできないときに原因の切り分けができそうだ。

<div style="page-break-before:always"></div>

<hr/>

### 1-2. OperatorAgent のメイン画面
#### 1-2-1.OperatorAgent メニュー

  ![OperatorAgent メイン画面（起動直後）](images/2-1-operatoragentMain.png){#fig:mainblank width=600px}

![OperatorAgent メニュー](images/1-2-oa_header.png){#fig:oa_header width=600px}

  1. OperatorAgent バージョン確認  
  画面の左上の OperatorAgent ロゴを右クリックすると表示されるメニュー（[@fig:logoclick]）から OperatorAgent のバージョンを確認することができます。（[@fig:oaversion]）  

  ![バージョンの確認方法](images/2-1-operatoragent_versionmenu.png){#fig:logoclick width=400px}  

  ![バージョンの確認方法](images/2-1-operatoragent_version.png){#fig:oaversion width=400px}  

  2. 通話リスト  
  指定した検索条件に適合する SpeechVisualizer の通話詳細へのリンクをリストアップします。[@tbl:oa_conlist] は、通話リストに関連する ControlCenter の詳細設定項目です。  

		No. | 設定分類                 | 設定項目名       | デフォルト値 | 内容 |
---:|---------------------|------------------|--------------|------|
1   | OperatorAgent - 通話 | 検索条件 | mine:* d:1d | 今日の自分の通話 |
2   | OperatorAgent - 通話 | 最大表示件数 | 20 | 上位 20 件まで |

		: OperatorAgent - 通話リストの設定 {#tbl:oa_conlist}  

		※ 検索条件の書式は SpeechVisualizer の通話検索条件と同じ書式が利用できます。

  3. マイクエリ  
SpeechVisualizer の通話検索機能で設定したマイクエリへのリンク（マイクエリの条件で検索した状態の検索画面へのリンク）をリストアップします。
 4. メッセージ  
 チャット機能です。  

    **`利用のヒント`**  

    オペレータ同士のチャットは禁止し、座席表モニタ中の SV とのチャットのみ許可したい場合には、ロールに  **『OperatorAgent からのメッセージ送信』** 権限（[@fig:role_message]） が付与されていない場合、OperatorAgent からユーザを検索・指定しての能動的なメッセージ送信ができません。  
		権限がある場合（[@fig:message_authok]）には、宛先入力欄でユーザ検索・指定してのメッセージ送信ができますが、権限が無い場合には宛先を指定できない（[@fig:message_authng]）ため、能動的なメッセージ送信ができません。  
		権限が無い場合でも、座席表モニタ中の SV からの受信メッセージに対する返信は可能です。（[@fig:operatoragent_messagewindow]）また、SV とのチャット履歴がのこっている時間（受信後24時間以内）であれば、メッセージ受信履歴からの宛先指定が可能です。（[@fig:message_authngrireki]）

![メッセージ送信権限](images/1-2-role_message.png){#fig:role_message width=500px}  

![メッセージ送信権限有り](images/2-1-message_authok.png){#fig:message_authok width=300px}  

![メッセージ送信権限無し](images/2-1-message_authng.png){#fig:message_authng width=300px}  

![受信メッセージへの返信](images/2-1-operatoragent_messagewindow.png){#fig:operatoragent_messagewindow width=400px}

![メッセージ送受信履歴あり](images/2-1-message_authngrireki.png){#fig:message_authngrireki width=300px}  


No. | 設定分類                 | 設定項目名       | デフォルト値 | 内容 |
---:|:--------------------|------------------|--------------|------|
1   | OperatorAgent - メッセージ | Enter キーでメッセージを送信 | true | false の場合には改行します |
2   | OperatorAgent - メッセージ | ヘルプ対応時にメッセージウインドウを自動的に開く | true | SV がヘルプ対応操作を行ったことがメッセージとして通知されます |  

: OperatorAgent - メッセージの詳細設定項目 {#tbl:oa_message_con}  


`メッセージの保存期間`  
---
- メッセージは、通話中にも非通話時にも送受信が可能です。  
  - 通話中のメッセージ - 通話の属性情報として扱われます。通話データが削除されるタイミングで消去されます。
  - 非通話中のメッセージ - 単純チャット情報として扱われます。24時間後に消去されます。  

  **通話中のメッセージも非通話中のメッセージも閲覧する機能はありません。**  

5. お知らせ  
  ControlCenter のお知らせ管理で登録されたお知らせのリストです。

	No. | 設定分類                 | 設定項目名       | デフォルト値 | 内容 |
---:|:--------------------|:-----------------|------------:|:-----|
1   | OperatorAgent - お知らせ | 更新間隔 | 3600 | 単位は秒 |
2   | OperatorAgent - お知らせ | 最大表示件数 | 20 | 上位 20 件まで |

	: OperatorAgent - お知らせの詳細設定項目 {#tbl:oa_news_con}  

  6. コンディション（感情メータ）  

  ![オペレータコンディション](images/2-1-Condition.png){#fig:Condtiong width=300px}  

- 直近1時間分の通話のオペレータ感情の **ポジティブ・ネガティブ（nemesysco.qa5.excitement）**  の平均値をメータ表示しています。左に振れると "ネガティブ"、右に振れると "ポジティブ" という判断になります。[@tbl:oa_condition_con]  はコンディションに関連する ControlCenter の詳細設定項目です。

	No. | 設定分類                 | 設定項目名       | デフォルト値 | 内容 |
---:|---------------------|------------------|--------------|------|
1   | OperatorAgent - 感情解析 | コンディションの表示 | true | false で表示しない |
2   | OperatorAgent - 感情解析 | コンディションのレッドゾーンの閾値 | 1.0 | 隠し項目 |
3| 共通 - 感情解析  | 感情解析の使用  | true  |  false = 感情解析に関するあらゆる UI を表示しない |  

	: OperatorAgent - コンディションの詳細設定項目 {#tbl:oa_condition_con}  

7. ログインユーザプロファイル
- ログインユーザ名表示部分をクリックするとプロフィール機能が利用できます。  
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
4 | 保留解除 | RealTimeRecorder でモニタ内線番号の通話保留中、保留解除を検出時に通知されます。 | [@fig:startobi]  
5 | 通話切替 | RealTimeRecorder でモニタ内線番号の録音中、録音対象の RTP の MediaResource が切り替わったときに通知されます。 | [@fig:kirikaeobi]  

	: 通話イベントの種類 {#tbl:callevent}

![通話イベント ： 通話開始 ＆ 通話終了](images/2-1-通話開始.png){#fig:startobi width=500px}

![通話イベント ： 保留開始 ＆ 保留解除](images/2-1-保留.png){#fig:holdobi width=500px}

![通話イベント ： 通話切替](images/2-1-通話切替.png){#fig:kirikaeobi width=500px}  

<!-- 【要確認】![](images/Tips.jpg){width=50px}  
OperatorAgent は Internet Explorer の設定を利用して通信します。  
インターネットオプションの設定でプロキシが設定されている場合、状態通知がブロックされます。  
対処としてプロキシの例外リストにWEBサーバ のIPアドレスを登録する方法があります。    -->

- 認識結果  
認識結果は StreamingRecognizer から OperatorAgent へ送信されます。  
通話内容は単語ごとにテキスト化され、順番に送信されますが、後から認識した単語によって既に表示されている単語が置き換わることもあります。発話単位で吹出で表現されます。発話の区切りは無音が一定時間以上（【要確認】 一定時間）継続することで行われます。（[@fig:hatuwa]）  


	<br/>  

	- 緑の吹出は、録音対象の電話機を主体として、送話音声の認識結果になります。送話側音声の認識は、認識オプション設定のオペレータタブに設定されたエンジンモードで処理されます。（[@fig:txengine]）  

		<br/>  

	- オレンジの吹出は、録音対象の電話機を主体として受話音声の認識結果となります。受話側音声の認識は、認識オプション設定のカスタマタブに設定されたエンジンモードで処理されます。（[@fig:rxengine]）  

 ![認識結果の表示](images/2-1-通話内容.png){#fig:hatuwa width=500px}  

 ![送話音声認識用エンジンモード](images/1-2-tx_engine.png){#fig:txengine width=400px}  

 ![受話音声認識用エンジンモード](images/1-2-rx_engine.png){#fig:rxengine width=400px}  

- 通話内容ビューの表示不具合のトラブルシューティング  



	<br/>  

	**区分 A ： 通話イベントが表示されない**  
　このケースは通話録音設定の不備か、スパンデータの不備による可能性が疑われます。（[@tbl:kubunA]）  

	<br/>  

	**区分 B ： 通話イベントのみ表示され、認識結果が表示されない**  
　このケースは通話録音・認識は正常に完了しているにも関わらず、 <br />　　**OperatorAgent と StreamingRecognizer 間の通信に不備がある** 可能性が疑われます。  
　ただし、各種設定の不備の可能性が無いわけではありません。

	<br />  

	**区分 C ： その他**  
　その他、よくある、通話内容表示不具合の例についてです。  

	No. | 原因| 対処 |
----:|---------|-------|
1 | RealTimeRecorder で通話録音ができていない | サーバ版であれば各種設定とパケットキャプチャの状況、クライアント版の場合には各種設定と録音デバイス関連を確認してください。  
2 | サーバ版の場合 OperatorAgent でログインしている内線番号と通話中の内線番号が一致していない | OperatorAgent ログイン時に設定する内線番号と通話する電話機の内線番号は一致させてください。  
3 | データベースの ServiceBroker が無効になっている | 有効化してください。  

	: 区分 A の主な原因と対処の目安 {#tbl:kubunA}

	No. | 原因| 対処 |
----:|---------|-------|
1 | OperatorAgent と StreamingRecognizer 間の接続が確立していない可能性があります。 | ノード管理で設定している、StreamingRecognizer の HTTP のポートに対して、OperatorAgent がアクセスできる状況にあるかを確認してください。  
2 | 認識オプションが未設定の可能性があります| 認識オプションの設定を実施してください。  
3 | 大規模な認識処理遅延が発生している可能性があります | 認識オプションの設定を実施してください。  

	: 区分 B の主な原因と対処の目安 {#tbl:kubunB}

	No. | 症状 | 原因| 対処 |
----:|---------|---|-------|
1 | クライアント版（コンバージャー録音）で、通話していないのに 『通話開始』 と 『通話終了』 繰り返し表示される | コンバージャーの調整不足です | 恐らく無音がとれない電話機なので、有音 + 短い通話録音を切り捨てる設定にしてください  
2 | クライアント版（コンバージャー録音）で、保留したタイミングで 『通話終了』 イベントが表示されてしまう | コンバージャー録音の性能限界の可能性があります | その時点のコンバージャー調整値では保留とオンフック状態の判別ができていません。調整によって解消する可能性もありますが、概ね IP  電話機の場合には保留とオンフックの判断はつかないようです。  
3 | 認識結果の表示が遅延する（業務開始直後、オペレータのみ） | クライアント認識版では顕著に現れる症状ですが、StreamingRecognizer が初回認識処理時に認識オプションに沿って、各種設定やエンジンモードのロードを行うため | 仕様かつ、1日の最初の通話でしか発生しませんので特に対処は必要ないですが  
4 | 認識結果の表示が遅延する（通話開始直後） | 通話冒頭の 30 秒間は、通話環境の音響を学習しています。エンジンモードの音響モデルの情報と環境の音響情報の乖離が激しい場合、認識負荷があがるため冒頭30秒程度オペレータの認識結果の表示が遅延することがあります。 | 無線 ヘッドセットを利用しているケースなどで起きがちです。その場合、有線ヘッドセットに変えるなどで症状が改善します。  

	: 区分 C の主な症状及び原因と対処の目安 {#tbl:kubunC}

  - 仕様となります。初回認識処理時にはテキスト化に利用するエンジンモードや  
  追加登録した辞書単語等の各種設定をダウンロードしているためです。


2. 通話情報ビュー   
通話中のオペレータの通話情報が表示されます。   
この情報は通話相手によって変わらない情報のみを表示します。（[@fig:callinfo] ）  
  `自分の電話番号`・・・自番号  
  `自分のID　　　`・・・エージェントID  

![通話情報の画面](images/2-1-通話情報.png){#fig:callinfo width=300px}  

3. 通話相手ビュー  
 通話状態や通話相手の情報を表示します。   
この情報は通話相手ごとに作成されます。（[@fig:callpartner] ）  

 ![通話相手の画面](images/2-1-通話相手.png){#fig:callpartner width=250px}  

[@tbl:callb] は、通話情報ビュー、通話相手ビューの設定項目です。
ControlCenter の詳細設定に設定項目があります。

  No. | 設定タブ項目 | 設定項目名                | 設定内容      |
  ----:|---------------------|------------------|--------------|
  1   |OperatorAgent - 通話 | 表示する通話属性の一覧 | （通話属性識別名）＝（名称)で指定  

: OperatorAgent 表示する通話属性の設定 {#tbl:callb}  

[@tbl:callb2] は、表示する通話属性で利用可能な通話属性の一覧です。(通話プロバイダにより利用できる通話属性が異なります。)

 No. | 通話属性識別名 | 名称                | Amazon Connect	      | Avaya AES    | Avaya     | SIP CIC     | SIP CTstage    |SIP OAI     | SIP T-Server      |
 ----:|---------------------|------------------|--------------|--------------|--------------|--------------|--------------|--------------|--------------|
 1   |amivoice.common.description | 備考 |  |  |  |  |  |  |  |
 2   |amivoice.common.direction | 向き|〇|〇|〇|〇|〇|〇|〇|
 3   |amivoice.common.linetype | 通話回線種別 |  |〇|  |〇|〇|〇|〇|
 4   |amivoice.common.summary| 要約 |   |  |  |  |  |  |  |
 5   |amivoice.common.headline| 見出し |   |  |  |  |  |  |  |
 6   |amivoice.common.mark | マーク |   |  |  |  |  |  |  |
 7   |amivoice.common.operator.key | 自分の識別名 |〇|〇|  |〇|〇|  |  |
 8   |amivoice.common.operator.name| 自分の名称|〇|  |  |  |〇|  |  |
 9   |amivoice.common.operator.phonenumber| 自番号 |〇|〇|〇|〇|〇|〇|〇|
 10   |amivoice.common.operator.group| 自分の所属グループ |〇|  |  |  |〇|  |  |
 11   |amivoice.common.operator.hostname | 自分のホスト名 |   |  |  |  |〇|  |  |
 12   |amivoice.common.customer.key | 相手の識別名 |   |  |  |〇|〇|  |  |
 13   |amivoice.common.customer.name | 相手の名称 |   |  |  |  |〇|  |  |
 14   |amivoice.common.customer.phonenumber| 相手番号|〇|〇|〇|〇|〇|〇|〇|
 15   |amivoice.common.customer.gender | 相手の性別 |   |  |  |  |  |  |  |
 16  |amivoice.common.telephony.dialin.phonenumber | ダイヤルイン番号 |   |  |  |〇|〇|〇|  |
 17   |amivoice.common.telephony.called.phonenumber | 掛先番号 |  |〇|〇|  |  |  |  |
 18   |amivoice.common.telephony.alerting.phonenumber | 呼出先番号|   |〇|  |  |  |  |  |
 19   |amivoice.common.telephony.trunk.group | トランクグループ |  |〇|  |〇|〇|〇|〇|
 20   |amivoice.common.telephony.trunk.member| トランクメンバ|  |〇|  |  |  |〇|  |
 21   |amivoice.common.telephony.queue.phonenumber| 通話キュー番号|   |〇|  |〇|  |  |  |
 22   |amivoice.common.telephony.transfer.source.key | 転送元識別名 |   |  |  |  |〇|  |  |
 23   |amivoice.common.telephony.transfer.source.name | 転送元名称 |   |  |  |  |〇|〇|  |
 24   |amivoice.common.telephony.transfer.source.phonenumber | 転送元番号 |   |〇|  |  |〇|  |〇|
 25   |amivoice.common.telephony.transfer.destination.key| 転送先識別名 |   |  |  |  |〇|  |  |
 26   |amivoice.common.telephony.transfer.destination.name | 転送先名称 |   |  |  |  |〇|  |  |
 27   |amivoice.common.telephony.transfer.destination.phonenumber | 転送先番号 |   |〇|  |  |〇|〇|〇|
 28   |amivoice.common.telephony.monitoring.target.key | モニタリング対象識別名 |   |  |  |〇|  |  |  |
 29   |amivoice.common.telephony.monitoring.target.name| モニタリング対象名称 |   |  |  |〇|  |  |  |
 30   |amivoice.common.telephony.monitoring.target.phonenumber| モニタリング対象番号 |   |  |  |〇|  |  |  |
 31   |amivoice.common.telephony.monitoring.target.type | 	モニタリング種別  |   |  |  |〇|  |  |  |
 32   |amivoice.common.reference.global.id | グローバル参照用のID |〇|〇|  | 〇|〇|  |〇|
 33   |amivoice.common.reference.global.url | グローバル参照用のURL |   |  |  |  |  |  |  |
 34   |amivoice.common.reference.local.id| ローカル参照用のID |   |〇|  |〇|  |  |  |
 35   |amivoice.common.reference.local.url| ローカル参照用のURL |   |  |  |  |  |  |  |
 36   |amivoice.common.reference.site.id | サイト参照用のID|   |  |  |  |  |  |  |
 37   |amivoice.common.reference.site.url| サイト参照用のURL |   |  |  |  |  |  |  |
 38   |amivoice.common.reference.private.id| プライベート参照用のID |   |  |  |  |  |  |  |
 39   |amivoice.common.reference.private.url | プライベート参照用のURL |   |  |  |  |  |  |  |
 40   |amivoice.common.recording.limit| 録音制限時間到達 |   |  |  |  |  |  |  |
 41   |amivoice.common.recording.split| 録音分割 |   |  |  |  |  |  |  |
 42   |amivoice.common.recording.split.previous| 録音分割された直前の通話 |   |  |  |  |  |  |  |
 43   |amivoice.common.reference.recording.id | 録音区間参照用のID |   |  |  |  |  |  |  |
 44   |amivoice.common.reference.recording.url | 録音区間参照用のURL |   |  |  |  |  |  |  |
 45   |amivoice.common.telephony.distributing.phonenumber| 受電グループ番号|  |〇|  |  |  |  |  |
 46   |amivoice.common.telephony.ivr.duration| IVR 応対時間 |   |〇|  |  |  |  |  |
 47   |amivoice.common.telephony.queue.duration | 待ち時間 |   |〇|  |  |  |  |  |

: OperatorAgent 表示する通話属性で利用可能な通話属性一覧 {#tbl:callb2}  


![](images/Tips.jpg){width=50px}  
相手の性別 は通話プロバイダから情報を取得するのではなく、性別識別用エンジンにて判断しています。   
[@tbl:seibetuenjin] は性別識別エンジンに関連する設定項目となり、ControlCenter/認識管理/認識オプション にあります。   

 No. | 設定タブ項目 | 設定項目名                | 内容      |
 ----:|---------------------|------------------|--------------|
 1   |カスタマタブ | 性別識別 | 性別識別を利用するかどうか   
 2   |カスタマタブ | 性別識別用エンジンモード | 性別識別用エンジンを登録
 3   |カスタマタブ | 性別識別の閾値| 性別識別の判定に使用する閾値   
 4   |カスタマタブ | 性別識別に使用する発話時間（最大） | 性別識別の判定に使用する発話時間の最大値   
 5   |カスタマタブ | 性別識別に使用する発話時間（最小） | 性別識別の判定に使用する発話時間の最小値

: カスタマ 性別識別用エンジン設定 {#tbl:seibetuenjin}  

オペレータ側は性別識別用エンジンで性別を判断していません。   
オペレータ側は ControlCenter/ユーザ管理/ ユーザごとのユーザ管理 - 詳細 設定の性別から判断しています。（ [@fig:usrprofile]）  

![ユーザ管理](images/2-1-ユーザ管理.png){#fig:usrprofile width=350px}  


4. 通話状態ビュー   
通話状態にあわせてアイコンや時間が変化します。（ [@fig:callstate]）  

![通話状態](images/2-1-通話状態.png){#fig:callstate width=250px}  

  `利用のヒント`  
通話状態に表示される時間はキャプチャサーバの時刻を参照しています。  

- 通話時間・・・録音開始 / 録音終了時刻から取得
- 保留・・・SIPまたはCTIイベントから取得

5. 通話フィルタビュー   
登録したキーワードがテキスト化された場合に様々なアクションを実行できる機能です。  （ [@fig:callfilter1]）  （ [@fig:callfilter2]）  

 ![OperatorAgent 上の通話フィルタ画面](images/2-1-通話フィルタ1.png){#fig:callfilter1 width=250px}  


 ![OperatorAgent 通話フィルタポップアップ画面](images/2-1-通話フィルタ2.png){#fig:callfilter2 width=250px}  



 `利用のヒント`   
通話フィルタはリアルタイムでレスポンスを返すことを重視した設計となっており、発動条件としては以下になります。  

- 登録したキーワードを検知したタイミング
- 認識結果が確定前の（※）  
（※）前後の文字の繋がりにより、最終的に認識結果が変わる場合があります。

つまり、１つのセグメント（発話）が完了するまで通話フィルタの処理を待つわけではなく  
キーワードを検知したタイミングですぐに処理が実行されます。  

[@tbl:callfilter] は、通話フィルタの ControlCenter の詳細設定項目です。  

  No. | 設定タブ項目 | 設定項目名                | 内容      |
 ----:|---------------------|------------------|--------------|
 1   |OperatorAgent - 通知メッセージ |通話フィルタの通知時間の倍率 (短め) | 通話フィルタの通知時間に対して通話時間レベルの「短め」とする時間を倍率で指定   
 2   |OperatorAgent - 通知メッセージ | 通話フィルタの通知時間の倍率 (長め)| 通話フィルタの通知時間に対して通話時間レベルの「長め」とする時間を倍率で指定
 3   |OperatorAgent - 通知メッセージ | 通話フィルタの通知時間レベル| 通話フィルタの表示時間を「0（普通）」とした場合に「-1（短め）」に表示するか「1（長め）」に表示するかを指定  
 4   |OperatorAgent - 通知メッセージ | 通話フィルタの表示時間|通話フィルタ検出時の通知メッセージの表示時間（秒）  
 5   |OperatorAgent - 通知メッセージ | 一度に通知する通話フィルタの対象発話数| OperatorAgent起動時に、検出済みの通話フィルタが大量に表示されるのを防止する機能。「-1」を指定した場合、通話内でそれまで検知した全ての通話フィルタの通知メッセージを表示  
 6   |共通 - 通話フィルタインポート | 通話フィルタインポートリクエストタイムアウト| インポート失敗を防ぐことを目的とした機能。有効値は「120以上の整数」

: OperatorAgent 通話フィルタの設定 {#tbl:callfilter}  

- 通話フィルタのトラブルシューティング  
<br>
	**区分 A ： 通話フィルタで設定したキーワードがテキスト化されたのにコマンドが実行されない**  
実行コマンドが Windows上で実行できないものが登録されているかの可能性があります。  
該当PCの「ファイル名を指定して実行」から登録したコマンドが実行できるか確認してください。

	**区分 B ： 〇〇〇の拡張子ファイルを呼び出すことができない**  
区分Aと同様に「ファイル名を指定して実行」から実行コマンドを確認してください。  
またブラウザに対象の拡張子が関連付けられているかを確認してください。


 6. ヘルプ    
OperatorAgent から SpeechVisualizer の座席表に登録したヘルプ要求理由でアラート通知する機能です。([@fig:helpb]）  

 ![ヘルプボタン](images/2-1-ヘルプ.png){#fig:helpb width=200px}  

  `利用上の注意`  
ヘルプを利用するには ControlCenter/モニタリング/ヘルプ要求理由管理、ヘルプ要求解除理由に登録が必要です。   
ヘルプ要求理由管理が登録されていない場合にはOperatorAgentの画面にヘルプボタンは表示されません。   

`利用のヒント`   
ヘルプ要求後のヘルプ解除は ControlCenter の設定で特定条件で自動終了することができます。  

- 通話前にヘルプ要求を実施、通話を開始した場合にヘルプ要求を自動解除
- 通話中にヘルプ要求を実施、通話終了後にヘルプ要求を自動解除


[@tbl:help] は、ヘルプに関する ControlCenter の詳細設定項目は以下です。

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

7. 感情解析ポップアップ   
オペレータとカスタマの通話中の発話をリアルタイムで感情を数値化して表示する機能です。  
この感情解析 ([@fig:emo]) は StreamingRecognizer から取得して表示しています。  

  ![感情解析ポップアップ画面](images/2-1-感情解析.png){#fig:emo width=250px}

通話終了後には通話の開始から通話終了までの感情のサマリ値([@fig:emosama])が表示されます。  

![感情解析のサマリ画面](images/2-1-感情解析2.png){#fig:emosama width=350px}  

[@tbl:emopop] は、表示する感情の設定項目です。ControlCenter の詳細設定項目にあります。  

No. | 設定分類| 設定項目名                | 設定内容      |
  ----:|---------------------|------------------|--------------|
  1   |OperatorAgent - 感情解析| 表示する感情（オペレータ）| （感情解析識別名）＝（感情名)で指定   
  2   |OperatorAgent - 感情解析| 表示する感情（カスタマ） | （感情解析識別名）＝（感情名)で指定  |  

: OperatorAgent の感情解析ポップアップ {#tbl:emopop}  


 `表示する感情の注意事項`   
 **表示する感情を変更する場合には詳細設定の 「保存する感情スコア」 の設定変更も必要です。   
 保存する感情スコアに設定されていない感情は感情値が取得できず、感情解析ポップアップに対象の感情が表示されません。**  

[@tbl:emoscore] は、保存する感情スコアの設定項目です。ControlCenter の詳細設定項目にあります。  

  No. | 設定分類| 設定項目名                | 設定内容      |
  ----:|---------------------|------------------|--------------|
  1   |共通 - 感情解析| 保存する感情スコア| （感情解析識別名）.（話者)で指定    

: 保存する感情スコア {#tbl:emoscore}  

 `表示する感情の注意点`   
**表示する感情はデータベースのパフォーマンスの観点からデフォルトで登録されている８つまでの感情に抑えるように設計が必要です。  
  「保存する感情スコア」に設定した感情のみが感情のサマリ値（最小/平均/最大/開始/終了）をデータベースに保存します。  
  発話単位の感情値は取得されています。 Emotion ファイルに保存されます。**


[@tbl:emolist] は、「表示する感情」、「保存する感情スコア」で利用可能な感情一覧です。ControlCenter の詳細設定項目にあります。

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

#### 1-2-3. 通話終了後の機能

1. SpeechVisualizer ボタン  
OperatorAgent 上に表示されている通話の SpeechVisualizer の通話詳細画面を呼び出します。 ([@fig:opsv])  

 ![SpeechVisualizer ボタン](images/2-1-opsv.png){#fig:opsv width=100px}  

　　`利用のヒント`  
　　Speech Visualizer ボタンは条件を満たしたタイミングで活性化されます。  
　　ボタンが活性化される条件としては以下です。  
　　・通話が終了していること  
　　・StreamingRecognizer の通話アップロードが完了していること  

　　[@tbl:svshort] は、「SpeechVisualizer を開く」 際に起動するブラウザを指定する設定です。  
　　設定は ControlCenter の詳細設定の項目にあります。  


No. | 設定分類| 設定項目名                | 設定内容      |
----:|---------------------|------------------|--------------|
1   |OperatorAgent - Web| SpeechVisualizer を表示するウェブブラウザ|SpeechVisualizer を表示するウェブブラウザのパスを指定  

: OperatorAgent SpeechVisualizerを表示するブラウザ設定 {#tbl:svshort}  


2. 通話終了後に通話属性を設定する  
通話終了後に通話に紐づく通話属性を追加することができる機能です。  
通話終了後、([@fig:callp2])がポップアップ表示されて通話属性を登録することが可能です。  


![手動通話属性の入力画面](images/2-1-通話属性ポップアップ画面.png){#fig:callp2 width=200px}  




No. | 設定分類| 設定項目名                | 設定内容      |
----:|---------------------|------------------|--------------|
1   |OperatorAgent - 通話| 通話終了後に手動で通話属性を設定可能にする|True で手動通話属性の設定可能  
2  |共通 - 通話| 手動で設定可能な通話属性|手動で設定可能な通話属性を指定  

手動で追加可能な通話属性は（[1-2-2. 通話表示機能　表 11: OperatorAgent 表示する通話属性で利用可能な通話属性一覧](#1-2-2. 通話表示機能) 参照。）  



#### 1-2-4. OperatorAgent の起動・終了時の動作  

1. OperatorAgent 起動時の処理  
- OperatorAgent の自動更新処理  
  OperatorAgent を起動すると、ログインダイアログが表示される前に自身のバージョンとサーバ側のバージョンの比較を行います。  
<br/>
  - OperatorAgent のバージョンがサーバのバージョンより古い場合には、自動的に更新処理が行われ OperatorAgent がサーバ側のバージョンに合わせてバージョンアップします。この更新処理はメジャーバージョンアップ時を除き、正常なバージョンアップが機能として保証されています。  
<br/>
  - OperatorAgent のバージョンがサーバのバージョンより新しい場合も同様に自動的に更新処理が行われ、 OperatorAgent がサーバ側のバージョンに合わせてバージョンダウンします。  
	    ただし、この更新処理は OperatorAgent の更新内容等によっては、正常なバージョンダウンが保証されない場合があります。（その場合には、一度 OperatorAgent をアンインストールして、古いバージョンの OperatorAgent を新規インストールしてください。）  
  自動バージョンダウン処理がサポートされるかどうかは、バージョンアップの内容次第です。切り戻し時の作業内容を検討する際には、リリースノートを確認するか、サポートへお問合せください。  
	<br />
	![](images/NOTICE.png){width=50px}
  　自動更新では処理中に **Windows Script Host （WSH）** の vbs がいくつか実行されます。（[@tbl:vbslist]）  
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

    **※ \@数字_モジュール_処理名.vbs のファイルは、特定の処理を行う (不要になったファイルの削除や、不具合修正のための処理とか) 為にあるので、以降のバージョンで追加になる可能性があります。**  

	<br/>  

	![](images/Tips.jpg){width=50px}
		　OperatorAgent をコマンドラインから引数付きで起動することで自動更新を抑制できます。（[1-2-6. コマンドラインからの OperatorAgent 操作](#1-2-6-operatoragent-操作) 参照。）  

<br/>

- ライセンス引当  
    処理詳細は【要確認】  

<br />

- メインウィンドウの表示について  
メインウィンドウの表示は、 [@tbl:oa_window] の項目の設定値を判断して行われます。  
<br />
	- 初回起動  
    	1. `C:\Users\%UserName%\AppData\Local\Advanced_Media,_Inc` に設定ファイルが無ければ、初回起動時として動作します。  
    	2. [@tbl:oa_window] の  No.2 の設定値を判断し、ウィンドウ表示を制御します。  
  - 通常起動  
	1. `C:\Users\%UserName%\AppData\Local\Advanced_Media,_Inc` に設定ファイルが有れば、通常起動として動作します。  
	2. [@tbl:oa_window] の  No.1 の設定値を判断し、ウィンドウ表示を制御します。  
	3. 表示しない設定の場合、[@tbl:oa_window] の  No.3 の設定値を判断し、タスクバー or 通知領域に情報を表示します。  

	No. | 設定分類| 設定項目名                | デフォルト値  | 内容 |
----:|---------------------|------------------|------|----|
1   | OperatorAgent - 起動時動作 | 起動時にウィンドウを表示状態に戻す | true | OperatorAgent 起動毎に、終了時のウィンドウ状態に依存せずメインウィンドウを画面表示状態に戻します。false の場合には、OperatorAgent の終了時の状態を引き継ぎます。
2   | OperatorAgent - 起動時動作 | 初回起動時にウィンドウを表示状態にする | true | 初回起動時の メインウィンドウの表示状態を設定します。オペレータさんに基本的に画面を一度も見せたくない場合などに false 設定しておきます。  
3   | OperatorAgent - 全般 | 閉じたときにタスクバーに表示しない | False | true にするとメインウィンドウの　× ボタンでウィンドウを閉じたときに、通知領域にのみアイコンが表示されます。  

	: OperatorAgent のウィンドウ表示に関わる詳細設定項目 {#tbl:oa_window}  


	```plantuml
	@startuml
	skinparam {
	defaultFontName BIZ UDPゴシック
	}
	skinparam backgroundColor #fffacd
	skinparam activity  {
	BackgroundColor #afeeee
	BorderColor #000080
	}
	title アクティビティ図.2 [OA ウィンドウ表示判定]\n

	start;
	-[#black]-> OperatorAgent 起動;
	if (設定ファイルあり) then
	  -[#blue]-> True : 通常起動;
		if (\n初回起動時に\nウィンドウを表示状態にする\n) then
			-[#blue]-> \nTrue;
			:OperatorAgent ウィンドウ表示;
			-[#black]->
			end;
		endif
	else
	  -> False : 初回起動処理;
			if (\n初回起動時に\nウィンドウを表示状態にする\n) then
				-[#blue]-> \nTrue;
				:OperatorAgent ウィンドウ表示;
				-[#black]->
				end;
			endif
	endif
	if (\n閉じたときに\nタスクバーに表示しない\n) then
		-[#blue]-> \nTrue;
		:OperatorAgent を最小化し、\n通知領域に格納;
		-[#black]->
	else
		-> \nFalse;
		:OperatorAgent を\n最小化してタスクバー表示;
		-[#black]->
	endif
	-[#black]->
	end;
	@enduml
	```

2. OperatorAgent 終了時の処理  
  - ログオフ処理  
  ControlCenter にレジストされた、OperatorAgent のログイン情報（ユーザ・座席表の位置・内線番号との関連付け）などをリリースします。  
  OperatorAgent を VDI オプション付きでインストールしている場合には、ライセンスのリリースも実施します。

	<br />
	![](images/NOTICE.png){width=50px}
　OperatorAgent を手動で終了せずに PC のシャットダウンを行った場合、PC がシャットダウンシーケンス開始を検出した OperatorAgent は自身も終了処理を実施します。さらに、終了処理が完了するまでの OS が完全にシャットダウンすることを待機させます。  
	ただし、OS 側でも各種終了処理が並行で実施されるため、OperatorAgent が ControlCenter と通信しログオフ処理を完了する前に OS の通信デバイスが停止している可能性があります。その場合、OperatorAgent のログイン情報が ControlCenter 上に残り続けます。  
ControlCenter は各 OperatorAgent の生存確認のための通信を実施しており、【要確認】  （[@tbl:oaping]） ControlCenter にレジストされた OperatorAgent のログイン情報はリリースされます。  
ControlCenter 上での OperatorAgent のログイン情報は、ControlCenter のモニタリングメニューの `『ログイン状況』` 機能で確認できます。  
SpeechVisualizer の座席表機能では、タイムアウトした OperatorAgent の座席にはタイムアウトアイコンが表示されます。([@fig:ismto])  
この状態は、該当座席に対して新たな OperatorAgent がログインすることで解消されます。それまではタイムアウト済みの OperatorAgent からのレジスト情報が表示され続けます。  

	![座席表でのタイムアウト表示](images/1-2-ism_to.png){#fig:ismto width=250px}  

	No. | 設定項目名                | デフォルト値  | 内容 |
----:|------------------|------|----|
1   | データ送信最長間隔 | 90000（ミリ秒） | 【要確認】  
2   | 再接続間隔 | 60000（ミリ秒） | 【要確認】  
3   | 受信タイムアウト | 120000（ミリ秒） | 【要確認】  

	: 詳細設定 項目分類 『OperatorAgent - 状態通知』 {#tbl:oaping}

#### 1-2-5. OperatorAgent からのコマンド実行
  - OperatorAgent からは、詳細設定項目（[@tbl:oacommand]）を設定することで指定したタイミングでコマンドを実行することができます。

	No. | 設定項目名
	---:|------------------
	1   |  OperatorAgent起動時に実行するコマンド
	2   | OperatorAgent終了時に実行するコマンド
	3   | ログアウト直後に実行するコマンド
	4   | ログイン直後に実行するコマンド
	5   | 通話開始直後に実行するコマンド
	6   | 通話終了直後に実行するコマンド

	: OperatorAgent コマンド実行 {#tbl:oacommand}

      - コマンド は任意で指定可能で、  
        1. Exe ファイルなどのアプリケーション  
        2. Bat or Cmd などの実行可能ファイル  
        3. ファイル名 or フォルダパス  
        4. URL  

      	などを適宜指定します。  
				基本的には、Windows の 『ファイル名を指定して実行』 で上記を指定したときと同じ挙動になります。  
				この機能で保証されるのは、指定コマンドの実行であって、**期待した結果が得られるかどうかではありません**。  
  <br />
  - [@tbl:oacommand] から実行するコマンドには、以下の書式で通話から取得できる情報を付加することが可能です。  
  記述するフォーマットは以下の通りです。  

	```
	${'メインキー文字列', 'サブキー文字列', 'オプション'}
	```  

	通話関連情報の場合は、メインキーは 『call』 に固定されます。  

	```
	${call, 'サブキー'}
	```  

	通話情報の会話識別子をそのままコマンドの引数として使用したい場合は  

	```
	${call, Key}
	```  

	と記述します。  
	実際に コマンドとして利用するには、  

	```
	http://webserver/SpeechVisualizer/Detail.aspx?key=${call, Key}
	```  

	のように記述します。

	オプションに **_urlencode_** を指定すると、値が URLエンコードされます。(※一部例外あり)  

	```
	http://webserver/SpeechVisualizer/Detail.aspx?key=${call, Key, urlencode}
	```  

	![](images/NOTICE.png){width=50px}
	　本機能では、`$` は特殊文字として予約されています。  
	コマンドの設定で `$` を文字として使用したい場合は、`\` でエスケープしてください。  
	同様に `"` や `\` も特殊文字ですので、文字として使用する場合は `\` でエスケープしてください。  
	<br />
	指定可能な **サブキー** は（[@tbl:commandsubkey]）の通りです。

	No. | サブキー名 | 置換される値 | [@tbl:callb2] との対応 | 備考
	---:|---------------|---|---|--
	1   |  Key | 会話識別子 | - |
	2   |  ConversationKey | 会話識別子 | - |
	3   |  ProjectName | プロジェクト名 | - |
	4   |  UserKey | ユーザID | - | Communication Suite へのログイン情報
	5   |  LineKey | 内線番号 | - |
	6   |  Date | 通話開始日時 | - | 日時系は、urlencode の指定ができません。代わりに [カスタム日時形式文字列](https://docs.microsoft.com/ja-jp/dotnet/standard/base-types/custom-date-and-time-format-strings?redirectedfrom=MSDN) の指定が可能です。<br />${call, StartDateTime, yyyy-MM-dd}
	7   |  StartDate | 通話開始日時 | - | 日時系
	8   |  StartDateTime | 通話開始日時 | - | 日時系
	9   |  EndDate | 通話終了日時 | - | 日時系
	10   |  EndDateTime | 通話終了日時 | - | 日時系
	11   |  Duration | 通話時間(秒) | - |
	12   |  HoldDuration | 累積保留時間(秒) | - |
	13   |  HoldCount | 保留回数 | - |
	14   |  DetailViewUrl | 詳細表示のURL | - |
	15   |  OperatorPhoneNumber | 自番号 | No.9 |
	16   |  OperatorPhoneLabel | 自分のID | No.8 | 電話基盤へのログイン情報
	17   |  OperatorGroup | 受電グループ | No.10 | 受電スキル
	18   |  OperatorHostName | 自分のホスト名 | No.11 | 【要確認】
	19   |  Direction | 通話の向き | No.2 |
	20   |  LineType | 通話種別 | No.3 |
	21   |  CustomerPhoneNumber | 相手番号 | No.14 |
	22   |  CustomerPhoneLabel | 相手の名称 | No.13 |
	23   |  TrunkGroup | トランクグループ | No.19 |
	24   |  TrunkMember | トランクメンバ | No.20 |
	25   |  CalledPhoneNumber | ダイヤル番号 | No.17 |
	26   |  AlertingPhoneNumber | 呼出先番号 | No.18 |
	27   |  QueuePhoneNumber | キュー番号 | No.21 |
	28   |  DialInPhoneNumber | ダイヤルイン番号 | No.16 |
	29   |  TransferSourcePhoneNumber | 転送元番号 | No.24 |
	30   |  TransferSourceLabel | 転送元名称 | No.23 |
	31   |  TransferDestinationPhoneNumber | 転送先番号 | No.27 |
	32   |  TransferDestinationLabel | 転送先名称 | No.26 |
	33   |  MonitoringType | モニタリング種別 | No.31 |
	34   |  MonitoringPhoneNumber | モニタリング対象の内線番号 | No.30 |
	35   |  MonitoringLabel | モニタリング対象の名称 | No.29 |
	36   |  GlobalReferenceId | グローバル参照用の ID | No.32 |
	37   |  GlobalReferenceUrl | グローバル参照用の URL | No.33 |
	38   |  LocalReferenceId | ローカル参照用の ID | No.34 |
	39   |  LocalReferenceUrl | ローカル参照用の URL | No.35 |
	40   |  SiteReferenceId | サイト参照用の ID | No.36 |
	41   |  SiteReferenceUrl | サイト参照用の URL | No.37 |
	42   |  PrivateReferenceId | プライベート参照用の ID | No.38 |
	43   |  PrivateReferenceUrl | プライベート参照用の URL | No.39 |   

	: サブキーの一覧 {#tbl:commandsubkey}  

	サブキーの指定に制限はありませんが、有用な値に置換できるかは利用している通話プロバイダと電話機基盤の設定によります。

#### 1-2-6. コマンドラインからの OperatorAgent 操作
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
6| 言語の指定 | --culture=[カルチャ名(\<languagecode2>-\<country/regioncode2>)] |  
7| 起動中のOAを終了 | --exit |  

	: OperatorAgent のコマンドラインオプション {#tbl:oa-option}  

	![](images/Tips.jpg){width=50px}  
	No.1. 一時的に OperatorAgent の接続先をステージング環境に向けたいときなどに利用します。  
	No.2. No.3 のパスワードと組み合わせて、統合 Windows 認証 を利用することなく自動ログインを可能にします。  
	No.3. No.2 のユーザID と組み合わせて、統合 Windows 認証 を利用することなく自動ログインを可能にします。  
	No.4. 一時的に設定済みの内線番号ではない電話機と組み合わせてテストするときなどに指定します。  
	No.5. なんらかの事情で OperatorAgent の自動バージョンアップをさせたくない場合に指定します。  
	No.6. 【要確認】  
	No.7. 端末の操作が著しく限定されている。<br />　 　 かつ、端末シャットダウン時に実行中のアプリケーションの全終了が条件の環境で利用しています。

#### 1-2-7. OperatorAgent のインストール
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
	3 | RealTimeRecorder\Converger | 通話プロバイダで、音声デバイス方式でコンバージャーを利用する場合に必要です。具体的になにが行われるかは 【要確認】  
	4 | RealTimeRecorder\PacketCapture | 【要確認】  
	5 | RealTimeRecorder\PacketCapture\Avaya | 【要確認】  
	6 | RealTimeRecorder\CTILink | CTI 連携用の DLL をインストールします。  
	7 | StreamingRecognizer | PC のサービスとして StreamingRecognizer をインストールします。クライアント版を利用する場合には必要です。  
	8 | ConvergerTool | コンバージャー調整ツールをインストールします。  

	: OperatorAgent インストール時に選択可能なコンポーネント {#tbl:oainstallcomponent}

	No.| task_name | 内容  
	--:|---|--
	1 | DesktopIcon | デスクトップにアイコンを作成します。  
	2 | RegisterStartup | スタートアップに登録します。  

	: OperatorAgent インストールタスク {#tbl:oainstalltasks}

	![](images/Tips.jpg){width=50px}　OperatorAgent は、⼀つの PC にインストールフォルダを変えて複数インストールすることが可能です。  
	PC に複数の OperatorAgent をインストールしている場合、コントロールパネルの 「アプリケーションの追加と削除 (プログラムと機能)」 からアンインストールできるのは、一番最後にインストールしたインスタンスだけです。それ以外のインスタンスをアンインストールする場合、 インストールフォルダ直下の `『uninstall\unins000.exe』` を実⾏してください。
