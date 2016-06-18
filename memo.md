# ソースコード全体の構造
- main.hspの10～343行目がメインルーチン。
 - main.hspの66～234行目は変数宣言だが、定数と思わしき物も変数として宣言されている。  
また、配列宣言の端折り・命名規則の混同が見られる。
 - 236～343行目に種々のバッファを作成し、メイン画面も表示させている。
   - 236～241行目に「iniload」「dataCheck」「disinfoinit」「loadHistory」「drawString」がgosubされている。
   - 324・325行目に「ssmode」「hotkeycapsetting」がgosubされている。
   - 332行目に「sssetting」、336行目に「twiinit」がgosubされている。
- ファイルの結合の仕方は次の通り。太字はzip内に同梱されているもの
  - **main.hsp**の1～55行目
  - **kmodule.as**
  - **ImageFileModule2.as**
  - **inimodule.as**
  - **exdialog.as**
  - **TsubuyakiSoup_mod.hsp**
   - **tCup_mod.hsp**
    - **tCup_mod.hsp**の1～30行目
    - **mbase64.as**
    - encode.as
    - **tCup_mod.hsp**の34～1038行目
   - **TsubuyakiSoup_mod.hsp**の2～266行目
  - **key.hsp**
  - **jsonParse.as**
  - **main.hsp**の65～1982行目
  - **makelistmodule_Ver6_4.as**
  - **SubSource_iniFileOperation.hsp**
  - **SubSource_TwitterOperation.hsp**
  - **SubSource_DrawString.hsp**
  - **SubSource_make.hsp**

# コーディング規約
- コメントについて
 - 簡易コメントは「;」、通常コメントは「//」か「/*～*/」を使用する
 - 全体的にコメントが少ないため、処理内容を自力で読み取る必要がある
 - コメントアウトされたコードがそのまま残っている箇所がちらほら
- 命名規則について
 - 変数名はローワーキャメルケース(LCC)。ただし古いVerに書かれた変数はただの小文字なことも
 - ラベル名もLCC。ただし古いVerは(以下略)
 - 定数名はただの大文字(スネークケースではない)
- その他
 - TRUEやFALSEは使用されていないので、「if mode = 0」のようなコードが散見される

# 画面ID一覧
|画面ID|通称|種類|内容|
|------|----|----|----|
|0|メイン画面|screen|SS作成やオプション設定などはここ|
|1|リスト画面|screen|分割されたセル毎にドラッグなどの処理が可能|
|2|一覧モード出力用|buffer|画面ID15に書き込む前の前処理用|
|3|？|screen|publishAccessToken関数内で使われているが詳細不明|
|3|縮小処理用|buffer|リスト画面内でD&Dする際の表示用|
|4|背景コピー用|buffer|リスト画面内でD&Dする際の表示用|
|5|キャプチャ用|buffer|画面全体からBitBltでクロップして貼り付ける(保存用)|
|7|画像読み込み用|buffer|data2.pngを読み込むための画面|
|8|キャプチャ作成用|buffer|(未使用)|
|10|キャプチャ用|buffer|画面全体をBitBltして貼り付ける|
|11|手動選択重ね用画面|bgscr|艦これのFlash表示を選択するための画面|
|12|貼付け用文字列|buffer|「第一艦隊」などの文字画像|
|15|一覧画像用|buffer|ここに書き込んで一覧画像として出力する|
|16|リスト画面用文字列|buffer|「スクリーンショットを～」で始まる文字画像|
|17|Flash確認画面|screen|艦これのFlashが選択されたことを確認するための画面|
|19|ツイート用画面|screen|画像プレビュー・セット・投稿などが可能|
|21|ツイート画像読み込み用|buffer|読み込んでプレビュー用に表示する|

# サブルーチン一覧
|サブルーチン名|ファイル名|処理内容|イベント駆動|
|--------------|----------|--------|------------|
|addcaptcha|main.hsp|リスト画面にSSを追加する処理|-|
|adummy|main.hsp|ダミー(そのままサブルーチンsetmodeが実行される)|button(main.hsp)|
|colorCange1|SubSource_DrawString.hsp|第一艦隊文字色を変更する|button(main.hsp)|
|colorCange2|SubSource_DrawString.hsp|第二艦隊文字色を変更する|button(main.hsp)|
|colorCange3|SubSource_DrawString.hsp|第三艦隊文字色を変更する|button(main.hsp)|
|colorCange4|SubSource_DrawString.hsp|第四艦隊文字色を変更する|button(main.hsp)|
|dataCheck|SubSource_iniFileOperation.hsp|読み込んだ設定を正規化する処理|-|
|disinfoinit|main.hsp|ディスプレイの座標、およびウィンドウハンドルを取得する|-|
|draw|main.hsp||-|
|drawColor|SubSource_DrawString.hsp|各艦隊の文字色をメイン画面でプレビューする|-|
|drawString|SubSource_DrawString.hsp|攻略編成モードで貼り付けるための画像を作成する|-|
|en_d|main.hsp|タイトルバーの×ボタンを押した際の処理|onexit|
|getText|SubSource_TwitterOperation.hsp|ツイート文字数を取得し、残文字数を表示する|oncmd(WM_COMMAND)|
|hotkey|main.hsp|ホットキーを押された際にSSを保存する|oncmd(WM_HOTKEY)|
|hotkeycapsetting|main.hsp|ホットキーの設定を反映する|-|
|iniload|SubSource_iniFileOperation.hsp|iniファイルを読み込む処理|-|
|inisave|SubSource_iniFileOperation.hsp|iniファイルに書き込む処理|-|
|intervalshotsavedialog|main.hsp|連続キャプチャの保存先を指定する|button(main.hsp)|
|list|main.hsp|艦娘一覧モード用の初期化|-|
|listchange|main.hsp|リスト画面の状態が変化した際の処理|-|
|listdrag|main.hsp|リスト画面内でD&Dした際の処理|oncmd(WM_LBUTTONDOWN)|
|listsavedialog|main.hsp|一覧の保存先を指定する|button(main.hsp)|
|listsavefopen|main.hsp|リストの保存先を開く|button(main.hsp)|
|loadHistory|SubSource_iniFileOperation.hsp|SSのファイル名一覧を取得する|-|
|make|SubSource_make.hsp|一覧画像を作成する|button(main.hsp)|
|OnDropFiles|main.hsp|ファイルをD&Dした際の処理|oncmd(WM_DROPFILES)|
|openbrowser|SubSource_TwitterOperation.hsp|Webブラウザを指定アドレスで開く|button(SubSource_TwitterOperation.hsp)|
|option|main.hsp|オプション画面用の初期化|-|
|picHistoryAddStack|SubSource_TwitterOperation.hsp|SSを投稿用にセットする|button(SubSource_TwitterOperation.hsp)|
|picHistoryBack|SubSource_TwitterOperation.hsp|SS一覧を←方向に捲る|button(SubSource_TwitterOperation.hsp)|
|picHistoryNext|SubSource_TwitterOperation.hsp|SS一覧を→方向に捲る|button(SubSource_TwitterOperation.hsp)|
|rideCursor|SubSource_TwitterOperation.hsp|ツイート前に画像にマウスを翳すとプレビューを表示させる処理|oncmd(WM_MOUSEMOVE)|
|seqcap|main.hsp|連続キャプチャ用の処理|button(main.hsp)|
|setmode|main.hsp|各実行モード向けに処理を振り分ける|oncmd(WM_COMMAND)|
|sscaptcha|main.hsp|SSを保存する|oncmd(WM_TIMER), button(main.hsp)|
|ssmode|main.hsp|SSキャプチャモード用の初期化|-|
|sssavedialog|main.hsp|SSの保存先を指定する|button(main.hsp)|
|sssavefopen|main.hsp|SSの保存先を開く|button(main.hsp)|
|sssetting|main.hsp|キャプチャ座標を取得する|button(main.hsp)|
|tweet_|SubSource_TwitterOperation.hsp|実際の投稿処理|button(SubSource_TwitterOperation.hsp)|
|TweetWindow|SubSource_TwitterOperation.hsp|ツイート用画面を表示する|-|
|TweetWindowDraw|SubSource_TwitterOperation.hsp|ツイート用画面を描画する|-|
|twiinit|SubSource_TwitterOperation.hsp|アクセストークンがあるならセットし、GUIを表示する。そうでない場合は認証画面を表示する。|-|
|twioauthok|SubSource_TwitterOperation.hsp|トークンが正常に機能するかチェックする|button(SubSource_TwitterOperation.hsp)|
|twireset|SubSource_TwitterOperation.hsp|トークン設定をリセットする|button(main.hsp)|
|twiwindowimage|SubSource_TwitterOperation.hsp|マウスクリックを検知し、画像に番号を付ける|oncmd(WM_LBUTTONDOWN)|
|windowsize|main.hsp|一覧編集用ウィンドウのサイズを調整する|oncmd(WM_SIZING)|
|windowsSizeChange|main.hsp|SSキャプチャモードで「↑」「↓」を押した際の処理|button(main.hsp)|
|yabumiupload|main.hsp|YabumiUploader.exeを利用してSSをアップロードする|button(main.hsp)|
|yabumiuploaderdialog|main.hsp|YabumiUploader.exeの場所を指定する|button(main.hsp)|

# モジュール一覧

|モジュール名|ファイル名|概要|
|------------|----------|----|
|無名(7行目)|exdialog.as|フォルダ参照用のモジュール|
|無名(1行目)|inimodule.as|iniファイルを操作するためのモジュール|
|無名(29行目)|makelistmodule_Ver6_4.as|chgbm関数用のモジュール？|
|無名(883行目)|tCup_mod.hsp|文字列操作用の小規模モジュール|
|無名(8行目)|TsubuyakiSoup_mod.hsp|ツイート用のモジュールその2|
|_machinebase64_|mbase64.as|マシン語でBase64エンコードするためのモジュール|
|ImageModule2|ImageModule2.as|画像処理用モジュール(by 衣日和)|
|jsonParse|jsonParse.as|JSONを解析するためのモジュール|
|kmodule|kmodule.as|各種雑多な関数群？|
|makelistmodule|makelistmodule_Ver6_4.as|艦これの画面の座標を取得するためのモジュール|
|mod_vpx|makelistmodule_Ver6_4.as|VRAM経由で画像にアクセスするためのモジュール|
|R4HBGC_C|makelistmodule_Ver6_4.as|？|
|tCup|tCup_mod.hsp|ツイート用のモジュールで、TsubuyakiSoup_mod.hspと合わせて使う|
