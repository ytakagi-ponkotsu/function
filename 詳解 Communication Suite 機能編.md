---
documentclass: ltjsarticle
output: pdf_document
figPrefix: '図.'
figureTitle: 図
tableTitle: 表
tblPrefix: '表.'
---

# 詳解 Communication Suite 機能編
## 誰も知らない Communication Suite の謎

## 目次
<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [詳解 Communication Suite 機能編](#詳解-communication-suite-機能編)
	- [誰も知らない Communication Suite の謎](#誰知-communication-suite-謎)
	- [目次](#目次)
	- [序章 トレーニングにあたって](#序章-)
		- [トレーニングの目的](#目的)
		- [トレーニング中の諸注意](#中諸注意)
	- [第1章 OperatorAgent](#第1章-operatoragent)
		- [1-1. OperatorAgent のログイン](#1-1-operatoragent-)
			- [1-1-1. OperatorAgent でログインすることの意味](#1-1-1-operatoragent-意味)
			- [1-1-2. OperatorAgent のログイン機能に関連する ControlCenter の詳細設定項目](#1-1-2-operatoragent-機能関連-controlcenter-詳細設定項目)
			- [1-1-3. プロジェクトの選択](#1-1-3-選択)
			- [1-1-4. 統合 Windows 認証](#1-1-4-統合-windows-認証)
			- [1-1-5. OperatorAgent 自動ログイン（統合 Windows 認証を利用しない）](#1-1-5-operatoragent-自動統合-windows-認証利用)
			- [1-1-5. OperatorAgent へのログイン失敗事由](#1-1-5-operatoragent-失敗事由)
			- [1-1-6. 1-1 のまとめ](#1-1-6-1-1-)
		- [1-2. OperatorAgent のメイン画面](#1-2-operatoragent-画面)
			- [1-2-1. メイン画面機能](#1-2-1-画面機能)
			- [1-2-2. メイン画面機能 - 通話中の機能](#1-2-2-画面機能-通話中機能)
			- [1-2-2. メイン画面機能 - 通話中の機能](#1-2-2-画面機能-通話中機能)
			- [1-2-3. メイン画面機能 - 通話終了後の機能](#1-2-3-画面機能-通話終了後機能)
			- [1-2-４. OperatorAgent の起動・終了時の動作](#1-2-operatoragent-起動終了時動作)
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

![基本のログイン画面](images/1-1-operatoragent-baselogin.png){#fig:login width=50%}

#### 1-1-2. OperatorAgent のログインに関連する ControlCenter の詳細設定項目

No. | 設定項目名       | デフォルト値 | 内容 |
---:|------------------|--------------|------|
1   |  ユーザーIDの保存 | false        | 最後にログイン成功した ユーザ ID を保存する |
2   |  パスワードの保存 | false        | 最後にログイン成功したパスワードを保存する |
3   |  自動ログイン | false        | 保存済みのユーザ ID とパスワード（と内線番号）で自動ログインする |
4   |  内線番号の指定 | false        | ログインダイアログに内線番号入力欄を表示する |
5   |  内線番号の情報が必要かどうか | S        | R = 必須, S = サーバ版では必須, N = 入力しない |
6   |  内線番号の保存 | false        | 最後にログイン成功した内線番号を保存する |

: 詳細設定 設定分類 : OperatorAgent - ログイン {#tbl:table}  

 - [@tbl:table] の No.4 『内線番号の指定』 を **"true"** にすることで、ログインダイアログに内線番号入力欄が追加されます。（[@fig:naisenari]。VDI 等のシンクライアント環境で、クライアント PC と電話機を固定で紐付けできない場合に有効です。）  

![内線番号入力可能なログイン画面](images/2020/02/1-1-operatoragent-naisenlogin.png){#fig:naisenari width=50%}

  - OperatorAgent のインストール時に内線番号を指定している場合には、指定番号が内線番号入力欄に表示されます。（[@tbl:table] の No.6 『内線番号の保存』 が **"false"** の場合も表示されます。）  
  変更すると、ログイン出来なくなったり、他の席の電話番号と紐付けされてしまうので注意してください。
  - [@tbl:table] の No.4 『内線番号の指定』 が **"false"** の場合でも、インストール時に内線番号が指定されていない場合で、かつ [@tbl:table] の No.5 『内線番号の情報が必要かどうか』 が "S" でかつサーバ版利用時 or "R" の場合には、内線番号入力欄が強制的に表示されます。
   - [@tbl:table] の No.1 ユーザID は、  
**`%USERPROFILE%/AppData/Local/Advanced_Media,_Inc/OperatorAgent.exe_StrongName_(長い文字列)/(バージョン番号)/user.config`**  
  の **LoginSettings/@LatestLoginUserId** に保存されます。 [^2] （この設定値は最後にログインに成功したユーザIDとなります。）

   - [@tbl:table]  の No.2 ログインパスワードは、Windows の  
	 [コントロールパネル] → [ユーザー アカウント] → [資格情報マネージャー]  
  に自動入力されたユーザIDに対応するパスワードが保存されます。（ [@fig:shikaku]。この設定値は最後にログインに成功したパスワードとなります。）  

![資格情報マネージャーのログイン情報](images/1-1-win_shikaku.png){#fig:shikaku width=65%}  

   - [@tbl:table]  の No.6 内線番号は、  
	 **`%USERPROFILE%/AppData/Local/Advanced_Media,_Inc/OperatorAgent.exe_StrongName_(長い文字列)/(バージョン番号)/user.config`**  
	 の **LoginSettings/@LatestLoginLineKey** に保存されます。（この設定値は最後にログインに成功した内線番号となります。）

[^2]:最後に

#### 1-1-3. プロジェクトの選択
- ログインするユーザが複数のプロジェクトに所属している場合には、ログインダイアログに続けてプロジェクト選択ダイアログが表示されます。([@fig:project])

![プロジェクト選択画面](images/2020/02/1-1-operatoragent-projectchoice.png){#fig:project width=50%}

#### 1-1-4. 統合 Windows 認証

 - 統合 Windows 認証機能を有効化している場合には、ログイン画面は表示されません。ただし、通常ログイン同様、ユーザが複数プロジェクトに所属していれば、[1-1-3. プロジェクトの選択](#1-1-3-選択) ： [@fig:project] のダイアログが表示されます。
 - インストール時に内線番号が指定されていない場合には、内線番号入力ダイアログ（[@fig:naisen]）が追加表示されます。  

![内線番号入力ダイアログ](images/1-1-operatoragentLogin_naisenonly.png){#fig:naisen width=50%}

- 統合 Windows 認証を利用するための Communication Suite 上の設定はありません。  
  ただし、IIS に追加の設定が必要です。  
	1. OS の "機能と役割の追加" から IIS - Web サーバ - セキュリティ 設定で **Windows 認証** を有効化してください。([@fig:role])
	2. IIS マネージャーの Web サイトの設定で、ControlCenter と SpeechVisualizer のそれぞれのサイトの認証の設定を以下の図と同様に変更します。（[@fig:siteconfig]）  

![機能と役割の追加](images/1-1-IIS_role_windowslogin.png){#fig:role width=50%}

![Web サイトの設定](images/1-1-IIS_sitegonfig_login.png){#fig:siteconfig width=50%}

#### 1-1-5. OperatorAgent 自動ログイン（統合 Windows 認証を利用しない）
- [1-1-2. OperatorAgent のログイン機能に関連する ControlCenter の詳細設定項目](#1-1-2-operatoragent-機能関連-controlcenter-詳細設定項目)  ：  [@tbl:table] の No.3 『自動ログイン』 が有効になっている場合には、統合 Windows 認証 を利用していなくてもログイン処理を省略可能です。


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
title アクティビティ図.1 [OA 自動ログイン判定]


start
:OperatorAgent 起動;
if (内線番号の情報が必要かどうか) then (不要 ： 設定値『N』)
else (必要)
	if (設定値 『S』 or 『R』) then (設定値『S』)
		if (サーバ版？) then (YES)
			if (内線番号) then (未入力)
				-ログインダイアログ表示
				end
			else (自動入力済)
			endif
		else (クライアント版)
		endif
	else (設定値『R』)
		if (内線番号) then (未入力)
			-ログインダイアログ表示
			end
		else (自動入力済)
		endif
	endif
endif
if (ユーザIDとパスワードの両方が\n自動入力されている) then (YES)
	if (自動ログインの設定は有効か？) then (有効)
	else (無効)
	  -ログインダイアログ表示
		end
	endif
else (いずれかもしくは両方が未入力)
	if (コマンドライン実行(※) で、引数により\nユーザIDとパスワードが設定されている) then (YES)
		if (自動ログインの設定は有効か？) then (有効)
		else (無効)
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

#### 1-1-5. OperatorAgent へのログイン失敗事由
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

  ![OperatorAgent メイン画面（起動直後）](images/2-1-operatoragentMain.png){#fig:mainblank width=70%}

![OperatorAgent メニュー](images/1-2-oa_header.png){#fig:oa_header width=70%}

  1. OperatorAgent バージョン確認  
  画面の左上の OperatorAgent ロゴを右クリックすると表示されるメニュー（[@fig:logoclick]）から OperatorAgent のバージョンを確認することができます。（[@fig:oaversion]）  

  ![バージョンの確認方法](images/2-1-operatoragent_versionmenu.png){#fig:logoclick width=60%}  

  ![バージョンの確認方法](images/2-1-operatoragent_version.png){#fig:oaversion width=60%}  

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

![メッセージ送信権限](images/1-2-role_message.png){#fig:role_message width=60%}  

![メッセージ送信権限有り](images/2-1-message_authok.png){#fig:message_authok width=40%}  

![メッセージ送信権限無し](images/2-1-message_authng.png){#fig:message_authng width=40%}  

![受信メッセージへの返信](images/2-1-operatoragent_messagewindow.png){#fig:operatoragent_messagewindow width=50%}

![メッセージ送受信履歴あり](images/2-1-message_authngrireki.png){#fig:message_authngrireki width=40%}  


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

  ![オペレータコンディション](images/2-1-Condition.png){#fig:Condtiong width=40%}  

- 直近1時間分の通話のオペレータ感情の **ポジティブ・ネガティブ（nemesysco.qa5.excitement）**  の平均値をメータ表示しています。左に振れると "ネガティブ"、右に振れると "ポジティブ" という判断になります。[@tbl:oa_condition_con]  はコンディションに関連する ControlCenter の詳細設定項目です。

	No. | 設定分類                 | 設定項目名       | デフォルト値 | 内容 |
---:|---------------------|------------------|--------------|------|
1   | OperatorAgent - 感情解析 | コンディションの表示 | true | false で表示しない |
2   | OperatorAgent - 感情解析 | コンディションのレッドゾーンの閾値 | 1.0 | 隠し項目 |
3| 共通 - 感情解析  | 感情解析の使用  | true  |  false = 感情解析に関するあらゆる UI を表示しない |  

	: OperatorAgent - コンディションの詳細設定項目 {#tbl:oa_condition_con}  

7. ログインユーザプロファイル
- ログインユーザ名表示部分をクリックするとプロフィール機能が利用できます。  
![ログイン情報](images/2-1-logininfo.png){#fig:logininfo width=40%}  

- プロフィールタブ（[@fig:oa_profile]）  
ログイン情報の表示・画像の設定・削除・パスワード変更（関連する詳細設定項目は [@tbl:oa_pwchange_con]）が実施できます。  


![プロフィール](images/2-1-profile.png){#fig:oa_profile width=40%}  

No. | 設定分類                 | 設定項目名       | デフォルト値 | 内容 |
---:|---------------------|------------------|--------------|------|
1   | 共通  - セキュリティ | パスワードのポリシー | 未定義 | パスワードのフォーマット定義 |
2   | 共通  - セキュリティ | パスワードの最小桁数 | 1 |  |

: OperatorAgent - パスワード変更の詳細設定項目 {#tbl:oa_pwchange_con}  

- 設定タブ（[@fig:oa_user_con]）  
ControlCenter の詳細設定で設定された OperatorAgent の振る舞いを個人用にカスタマイズできます。  
[@tbl:oa_user_con] は、表示項目と詳細設定項目の対応表です。

 ![OperatorAgent ユーザ設定](images/2-1-config.png){#fig:oa_user_con}  

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

#### 1-2-2. メイン画面機能 - 通話中の機能

1. 通話内容  
OperatorAgentにログイン中の内線番号に関する通話のイベントが表示されます。  
<br/>
 	1. 状態通知  
対象内線の通話状態を通知します。この通知は ControlCenter から OperatorAgent に対して http を経由して通知されます。  
状態通知として表示されるイベントは次の通りです。  
`通話開始 / 通話終了`・・・OperatorAgentでログインした内線番号で通話が開始/終了した際に通知します。（[@fig:startobi] ）  

![通話開始/通話終了の状態通知](images/2-1-通話開始.png){#fig:startobi width=60% height=60%}  

  `保留 / 保留解除`・・・オペレータ側で保留/保留解除をした際に通知します。（[@fig:holdobi] ）  
**※ 保留の状態通知はSIP or CTI の情報から判断しており、通話プロバイダによっては検知することができません。**

![保留/保留解除の状態通知](images/2-1-保留.png){#fig:holdobi width=60% height=60%}  

  `通話切替`・・・通話相手が切り替わった際に検知します。（[@fig:kirikaeobi] ）  
**※ 録音対象としていたRTPパケットが切り替わったときに発生します。**

![通話切替の状態通知](images/2-1-通話切替.png){#fig:kirikaeobi width=60% height=60%}  

②認識結果  
通話開始後、StreamingRecognizer から認識結果を取得して送話と受話の認識結果（[@fig:hatuwa] ）を表示します。  

 ![認識結果の画面](images/2-1-通話内容.png){#fig:hatuwa width=60% height=60%}  

送話と受話で使用する音声認識エンジンは異なります。  
ControlCenter - 認識オプションの設定で使用する音声認識エンジンを設定します。  

 No. | 設定タブ項目 | 設定項目名                | 設定値      |
 ----:|---------------------|------------------|--------------|
 1   | オペレータ | 音声認識用エンジンモード | AMI提供のオペレータ用音声認識エンジンを登録 |
 2   | カスタマ | 音声認識用エンジンモード | AMI提供のカスタマ用音声認識エンジンを登録 |  


`よくある質問`  

- **通話開始の状態通知が表示されない**  
  - 対象内線で録音ができていない  
  - OperatorAgent でログインしている内線番号と通話中の内線番号が一致していない  
  - OperatorAgent をプロキシ経由で利用している



- **通話開始・通話終了の帯は表示されるが、テキスト結果が表示されない**  
  - クライアント端末から StreamingRecognizer のHTTPポートに接続ができていない  
  - ControlCenter - 認識オプションの音声認識エンジンモードが設定されていない   

- **OperatorAgent起動後の最初の通話で認識結果が遅れて表示される**  
  - 仕様となります。初回認識処理時にはテキスト化に利用するエンジンモードや  
  追加登録した辞書単語等の各種設定をダウンロードしているためです。

#### 1-2-3. メイン画面機能 - 通話中の機能






2. 通話情報   
通話中のオペレータの通話情報が表示されます。   
この情報は通話属性が取得できる場合に（[@fig:callinfo] ）のように通話相手によって変更されない情報のみを表示します。  
  `自分の電話番号`・・・自番号  
  `自分のID`・・・エージェントID  

![通話情報の画面](images/2-1-通話情報.png){#fig:callinfo width=30% height=30%}  

3. 通話相手  
 通話状態や通話相手の情報を表示します。（[@fig:callpartner] ）   
この情報は通話相手が切り替わる度に、話者単位で作成されます。  
取得可能な情報は通話プロバイダにより異なります。  

 ![通話相手の画面](images/2-1-通話相手.png){#fig:callpartner width=20% height=15%}  

 `補足情報 1`   
 相手の性別 は通話プロバイダから情報を取得するのではなく、性別識別用エンジンにて判断しています。   
 相手の性別 に関連する設定項目は ControlCenter/認識管理/認識オプション にあります。   

 No. | 設定タブ項目 | 設定項目名                | 内容      |
 ----:|---------------------|------------------|--------------|
 1   |カスタマタブ | 性別識別 | 性別識別を利用するかどうか   
 2   |カスタマタブ | 性別識別用エンジンモード | 性別識別用エンジンを登録
 3   |カスタマタブ | 性別識別の閾値| 性別識別の判定に使用する閾値   
 4   |カスタマタブ | 性別識別に使用する発話時間（最大） | 性別識別の判定に使用する発話時間の最大値   
 5   |カスタマタブ | 性別識別に使用する発話時間（最小） | 性別識別の判定に使用する発話時間の最小値

  `補足情報 2`   
オペレータ側の性別判断は性別識別用エンジンを利用していません。   
オペレータ側の性別判断は ControlCenter/ユーザ管理/ のユーザごとのユーザ管理 - 詳細 設定の性別から判断しています。

通話情報、通話相手の ControlCenter の詳細設定項目は以下です。   

 No. | 設定タブ項目 | 設定項目名                | 設定内容      |
 ----:|---------------------|------------------|--------------|
 1   |OperatorAgent - 通話 | 表示する通話属性の一覧 | （通話属性キー）＝（表示ラベル名)で指定します。   

利用可能な設定値は以下です。(通話プロバイダにより取得できる属性が異なります。)

No. | 通話属性キー | 表示ラベル名                | Amazon Connect	      | Avaya AES    | Avaya     | SIP CIC     | SIP CTstage    |SIP OAI     | SIP T-Server      |
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



4. 通話状態   
通話状態にあわせてアイコンや時間が変化します。（ [@fig:callstate]）  

![通話状態](images/2-1-通話状態.png){#fig:callstate width=25% height=25%}  



 `利用のヒント`  
通話状態に表示される時刻（通話時間や保留時間）は〇〇から情報を取得して時間を表示しています。

5. 通話フィルタ   
登録したキーワードがテキスト化された場合に様々なアクションを実行できる機能です。（ [@fig:callfilter]）  

 ![OperatorAgentメイン画面の通話フィルタ画面](images/2-1-通話フィルタ.png){#fig:callfilter width=25% height=25%}  

 通話フィルタの ControlCenter の詳細設定項目は以下です。   

  No. | 設定タブ項目 | 設定項目名                | 内容      |
 ----:|---------------------|------------------|--------------|
 1   |OperatorAgent - 通知メッセージ |通話フィルタの通知時間の倍率 (短め) | 通話フィルタの通知時間に対して通話時間レベルの「短め」とする時間を倍率で指定   
 2   |OperatorAgent - 通知メッセージ | 通話フィルタの通知時間の倍率 (長め)| 通話フィルタの通知時間に対して通話時間レベルの「長め」とする時間を倍率で指定
 3   |OperatorAgent - 通知メッセージ | 通話フィルタの通知時間レベル| 通話フィルタの表示時間を「0（普通）」とした場合に「-1（短め）」に表示するか「1（長め）」に表示するかを指定  
 4   |OperatorAgent - 通知メッセージ | 通話フィルタの表示時間|通話フィルタ検出時の通知メッセージの表示時間（秒）  
 5   |OperatorAgent - 通知メッセージ | 一度に通知する通話フィルタの対象発話数| OperatorAgent起動時に、検出済みの通話フィルタが大量に表示されるのを防止する機能。「-1」を指定した場合、通話内でそれまで検知した全ての通話フィルタの通知メッセージを表示  
 6   |共通 - 通話フィルタインポート | 通話フィルタインポートリクエストタイムアウト| インポート時にタイムアウトの有効値を増やすことによりインポート失敗を防ぐことを目的とした機能。有効値は「120以上の整数」

  `利用のヒント`   
通話フィルタはリアルタイムでレスポンスを返すことを重視した設計となっており、通話フィルタの発動条件としては以下になります。  

- 登録したキーワードを検知したタイミング
- 認識結果が確定前の状態（※）  
（※）前後の文字の繋がりにより、最終的に認識結果が変更される場合があります。

つまり、１つのセグメント（発話）が終了するまで通話フィルタの処理が実行されないわけではなく、キーワードを検知したタイミングで処理が実行されます。  

  `よくある質問`

- **通話開始の状態通知が表示されない**  
	  - 対象内線で録音ができていない  
	  - OperatorAgent でログインしている内線番号と通話中の内線番号が一致していない  
	  - OperatorAgent をプロキシ経由で利用している















 6. ヘルプ    
OperatorAgent から SpeechVisualizer の座席表に登録したテンプレートでアラート通知する機能です。   

`利用のヒント`  
ヘルプを利用するには ControlCenter/モニタリング/ヘルプ要求理由管理、ヘルプ要求解除理由にテンプレートの登録が必要です。   
テンプレートを登録していない場合には OperatorAgentの画面左下部にヘルプのアイコン([@fig:helpb]）は表示されません。   

 ![ヘルプのアイコン](images/2-1-ヘルプ.png){#fig:helpb width=20% height=20%}  



 ヘルプの ControlCenter の詳細設定項目は以下です。

 No. | 設定分類| 設定項目名                | 内容      |
----|---------------------|------------------|--------------|
1   |OperatorAgent - メッセージ | ヘルプ対応時にメッセージウインドウを自動的に開く | ヘルプ応答時にメッセージウインドウを自動的に開く   
2   |OperatorAgent - 通知メッセージ | ヘルプの解除理由選択の表示時間|ヘルプ要求の自動解除後にヘルプ解除理由のテンプレートを表示する時間    
3   |OperatorAgent - 通知メッセージ | ヘルプを案内する感情解析の通話重要度の閾値 | あああ（よくわからない）   
4   |OperatorAgent - 通知メッセージ  |ヘルプ中のクローズ | あああ（よくわからない）
5   |OperatorAgent - 通知メッセージ  |ヘルプ中の表示 | ヘルプ要求時の通知メッセージを表示するかどうか

 `利用のヒント`   
 OperatorAgent のヘルプ通知が SpeechVisualizer の座席表に通知されない場合には  
 ControlCenter からの状態通知を OperatorAgent がなにかしらの理由で受信できていないことが原因です。

7. 感情解析ポップアップ   
オペレータとカスタマの通話中の発話をリアルタイムで感情を数値化して表示する機能です。  
この感情解析([@fig:emo])は StreamingRecognizer から取得して表示しています。  

  ![感情解析ポップアップ画面](images/2-1-感情解析.png){#fig:emo width=25% height=25%}

通話終了後には通話の開始から通話終了までの感情のサマリ値([@fig:emosama])が表示されます。  

![感情解析のサマリ画面](images/2-1-感情解析2.png){#fig:emosama width=35% height=35%}  

感情解析ポップアップに表示する感情一覧は ControlCenter の詳細設定項目にあります。   

No. | 設定分類| 設定項目名                | 内容      |
  ----|---------------------|------------------|--------------|
  1   |OperatorAgent - 感情解析| 表示する感情（オペレータ）| オペレータで解析する感情を登録   
  2   |OperatorAgent - 感情解析| 表示する感情（カスタマ） |カスタマで解析する感情を登録    

 `利用のヒント`   
 表示する感情を変更する場合には詳細設定の 「保存する感情スコア」 の設定変更も必要です。   
 保存する感情スコアに設定されていない感情は感情値が取得できず、感情解析ポップアップにその感情が表示されません。   

  No. | 設定分類| 設定項目名                | 内容      |
  ----|---------------------|------------------|--------------|
  1   |共通 - 感情解析| 保存する感情スコア| オペレータ、カスタマで解析する感情を登録   

 `表示する感情の注意点`   
**表示する感情はパフォーマンスの観点からデフォルトで登録されている８つまでの感情に抑えるようにしてください。**   
  保存する感情スコアに設定した感情のみが感情のサマリ値（最小/平均/最大/開始/終了）をデータベースに保存します。  
  表示する感情スコアに登録されていない感情は発話単位の感情値のみがデータベースに保存されます。   



#### 1-2-4. メイン画面機能 - 通話終了後の機能

#### 1-2-5. OperatorAgent の起動・終了時の動作
1. OperatorAgent 起動時の処理  
  - OperatorAgent の自動更新処理  
  OperatorAgent を起動すると、ログインダイアログが表示される前に自身のバージョンとサーバ側のバージョンの比較を行います。  
    - OperatorAgent のバージョンがサーバのバージョンより古い場合には、自動的に更新処理が行われ OperatorAgent が自動的にバージョンアップします。この更新処理は機能として、正常なバージョンアップがされることが保証されています。  

    - OperatorAgent のバージョンがサーバのバージョンより新しい場合も同様に自動更新処理が行われ、 OperatorAgent の自動バージョンダウン処理が行われますが、この処理は機能によって正常更新が保証されない場合があります。  
  バージョンダウン処理がサポートされるかどうかは、そのときのバージョン次第です。必要がある場合には、サポートへお問合せください。  
  #### `更新処理の注意事項`  
  更新処理には、 **Windows Script Host （WSH）** の vbs がいくつか実行されます。セキュリティソフトによって、WSH の実行が阻害されてしまう環境では、自動更新処理が正常に行われません。（インストーラによる初期インストールでもバージョンアップインストールでも、WSH は実行されます。）  
  自動更新処理で実行されるスクリプトは以下です。

    No. | ファイル名 | 説明  |
    ----|---------------------|------------------|
 1   | moduleindexbuilder.vbs | バージョン毎にファイルのハッシュ値が**必ず変更になります**。 |
 2   | @301_RR_CTILink_RegAsm.vbs | バージョン毎にファイルのハッシュ値の変更はありませんが将来のバージョンで削除となる可能性はあります。 |
 3   | @341_RR_RemoveFiles.vbs | バージョン毎にファイルのハッシュ値の変更はありませんが将来のバージョンで削除となる可能性はあります。 |
 4   | @341_SR_RemoveFiles.vbs | バージョン毎にファイルのハッシュ値の変更はありませんが将来のバージョンで削除となる可能性はあります。 |
 5   | @352_SR_Web_RemoveFiles.vbs | バージョン毎にファイルのハッシュ値の変更はありませんが将来のバージョンで削除となる可能性はあります。 |
 6   | @Updater.vbs | ファイルが更新されていればハッシュ値も変更になります。 |

    **※** 「@数字_モジュール_処理名.vbs」のファイルは、自動アップデート時に特定の処理を行う (不要になったファイルの削除や、不具合修正のための処理とか) 為にあるので、以降のバージョンで追加になる可能性があります。
  - ライセンス引当  
    処理詳細は【要確認】  

2. OperatorAgent 終了時の処理  
  - ログオフ処理  
  ControlCenter にレジストされた、OperatorAgent のレジスト情報（ユーザ・座席表の位置・内線番号との関連付け）などをリリースします。  
  OperatorAgent を VDI オプション付きでインストールしている場合には、ライセンスのリリースも実施します。

#### 1-2-6. OperatorAgent からのコマンド実行
  - あ
  - あ
  - あ

#### 1-2-7. コマンドラインからの OperatorAgent 操作
  1. OperatorAgent をコマンドラインから起動する
  OperatorAgent は、コマンドラインから
```
  インストールパス\OperatorAgent.exe
```
  のように起動できます。  

  2. OperatorAgent をコマンドラインから終了する  


#### 1-2-8. OperatorAgent のインストール
