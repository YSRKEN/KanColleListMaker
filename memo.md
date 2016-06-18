# ソースコード全体の構造
- main.hspの10～343行目がメインルーチン。
 - main.hspの66～234行目は変数宣言だが、定数と思わしき物も変数として宣言されている。  
また、配列宣言の端折り・命名規則の混同が見られる。
 - 236～343行目に種々のバッファを作成し、メイン画面も表示させている。
   - 236～241行目に「iniload」「dataCheck」「disinfoinit」「loadHistory」「drawString」がgosubされている。
   - 324・325行目に「ssmode」「hotkeycapsetting」がgosubされている。
   - 332行目に「sssetting」、336行目に「twiinit」がgosubされている。

- 以下、画面ID・サブルーチン・モジュール毎の概要を示す。

|サブルーチン名|ファイル名|処理内容|イベント駆動|
|--------------|----------|--------|------------|
|adummy|main.hsp|ダミー(そのままサブルーチンsetmodeが実行される)|button|
|dataCheck|SubSource_iniFileOperation.hsp|読み込んだ設定を正規化する処理|-|
|disinfoinit|main.hsp|ディスプレイの座標、およびウィンドウハンドルを取得する|-|
|drawString|SubSource_DrawString.hsp|攻略編成モードで貼り付けるための画像を作成する|-|
|en_d|main.hsp|タイトルバーの×ボタンを押した際の処理|onexit|
|getText|||oncmd(WM_COMMAND)|
|hotkey|||oncmd(WM_HOTKEY)|
|iniload|SubSource_iniFileOperation.hsp|iniファイルを読み込む処理|-|
|listdrag|||oncmd(WM_LBUTTONDOWN)|
|loadHistory|SubSource_iniFileOperation.hsp|SSのファイル名一覧を取得する|-|
|OnDropFiles|||oncmd(WM_DROPFILES)|
|rideCursor|||oncmd(WM_MOUSEMOVE)|
|setmode|||oncmd(WM_COMMAND)|
|sscaptcha|||oncmd(0x0113)|
|ssmode|||-|
|sssetting|||-|
|twiinit|||-|
|twiwindowimage|||oncmd(0x0201)|
|windowsize|||oncmd(WM_SIZING)|

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
