PaperTester
===========

##概要
Windows標準機能のみ(VBA未使用)に依存する為、セキュアな環境でも導入できます。
InternetExplorer(IE)/EXEの操作内容をExcelテスト仕様書（PaperTester.xlsx）に記入していくと、
ワークシート関数で自動操作用のVBScriptコードを生成します。
生成されたコードをテンプレートコード（Execute_PaperTester.vbs）に埋め込み実行する事で、
IE/EXE操作用ライブラリ(PaperTester.vbs)が呼び出され、IE/EXEが自動操作されます。
又、スクリーンショットとSQL文の実行結果がエビデンス記録ブック（EvidenceTemplate.xlsx）に貼り付けられます。

##デモ
[demoフォルダ](https://github.com/nezuQ/PaperTester/tree/master/demo)をWindowsPCにダウンロードし、Execute_PaperTester.vbsをダブルクリックして下さい。
IEが起動し、[デモ用のWebページ](http://bl.ocks.org/nezuQ/raw/9719897/)の画面項目が自動操作されます。
又、メモ帳が起動し、自動操作されます。
その後、スクリーンショットやダミーデータベース（_database.xlsx）の値がエビデンス記録ブック（EvidenceTemplate.xlsx）に貼り付けられます。

※注意1……[デモ用のWebページ](http://bl.ocks.org/nezuQ/raw/9719897/)のポップアップを許可して下さい。
[→参考サイト](http://windows.microsoft.com/ja-JP/windows-vista/Internet-Explorer-Pop-up-Blocker-frequently-asked-questions?SignedIn=1)。

※注意2……64bit版OSの場合は_database.xlsxをExecute_PaperTester.vbs実行前に開いて下さい。

##依存ソフトウェア
 * Windows OS（Windows7 32bit版 推奨）
 * Microsoft Office
 * Internet Explorer

##使い方
 1. PaperTester.xlsxの書き方
   1. テストケース名を記入する。テストケース番号は自動的に割り当てられます。
   2. 確認内容・想定結果を記入する。
   3. 操作名・引数を記入する。入力できる値はdataシートに説明があります。
   4. その他項目を任意で記入する。
 2. Execute_PaperTester.vbsへのコードの埋め込み方
   1. PaperTester.xlsxの操作コマンド列の値を一括でコピーし、Execute_PaperTester.vbsの"本処理"の箇所に貼り付ける。
   2. 同ファイルの"設定値"の箇所にある pt.ConnectionString に接続文字列を記入する。※SQL文を発行しない場合は未記入にする。
   3. 上書き保存する。
 3. テスト（IE/EXE自動操作）の実行方法
   1. Execute_PaperTester.vbsをダブルクリックする。
   2. IE/EXE起動時にIEが最前面に来なかった場合は、IE/EXEをクリックし、最前面に移動する。
   3. 終了メッセージのポップアップを待つ。

##操作コマンド一覧(PaperTester.vbs)

 * IEを開く  
OpenIE  
 * IEを取得する（最初のもの）  
GetIE 0
 * IEを取得する（最後のもの）  
GetIE -1
 * EXEを起動する  
Run "%0"
 * IE/EXEを閉じる  
Quit
 * 戻る  
GoBack
 * 全画面表示を行う  
FullScreen
 * 全画面表示を止める  
NormalScreen
 * 画面を最大化する  
MaximumWindow
 * 画面を最小化する  
MinimumWindow
 * 画面を標準表示にする  
NormalWindow
 * 待機する  
Sleep %0
 * URLで遷移する  
Navigate "%0"
 * 次のIEをアクティブにする  
ActivateNextIE
 * 前のIEをアクティブにする  
ActivateBeforeIE
 * 指定フレームをアクティブにする  
ActivateFrame %0
 * 元ドキュメントをアクティブにする  
ActivateDocument
 * フォーカスを当てる  
Focus "%0"
 * 入力する（Value使用）  
ValueInput "%0"
 * 入力する（Copy&Paste使用）  
PasteInput "%0"
 * 入力する（SendKeys使用）  
KeyInput "%0"
 * クリックする  
Click "%0"
 * 文字列をペーストする  
Paste "%0"
 * キー入力する  
SendKeys "%0"
 * スクリーンショットを撮る（画面全体）  
FullScreenShot "%0"
 * スクリーンショットを撮る（アクティブ画面のみ）  
ScreenShot "%0"
 * スクリーンショットを撮る（画面全体, 表示箇所のみ）  
FullScreenShot4VisibleArea "%0"
 * スクリーンショットを撮る（アクティブ画面のみ, 表示箇所のみ）  
ScreenShot4VisibleArea "%0"
 * SQL文を発行する  
ExecuteSQL "%0"
 * 画面項目を検証する（検証NG時は処理中断）  
ValidateAttribute "%0"
 * 画面項目を検証する（検証NG時は処理続行）  
Record2ValidateAttribute "%0"
 * 画面タイトルを検証する（検証NG時は処理中断）  
ValidateTitle "%0"
 * 画面タイトルを検証する（検証NG時は処理続行）  
Record2ValidateTitle "%0"
 * Javascriptを実行する  
ExecuteJS "%0"

##ライセンス
 * MITライセンス

##TODO
 * EXEのウィンドウにフォーカスする処理が不安定になっている。その為、対象外のウィンドウを誤って操作してしまう事がある。
 * EXEの場合は一部コマンド（ex.Paste, SendKeys, FullScreenShot4VisibleArea）のみしか利用できない。
 * クリップボードが空でない時、スクリーンショットが失敗する事がある。
 * 指定要素内のスクロールを行いながらスクリーンショットを撮る「ElementScreenShot」コマンドが欲しい。
 * アクティブ画面のスクリーンショットを撮る「ScreenShot(ScreenShot4VisibleArea)」コマンドで不明なエラーが発生する。

##関連ページ
Qiita - Excelスクショ問題の解決策を現役エンジニアが本気で考えた。  
http://qiita.com/nezuq/items/d2ff540cdba00d41bfda  
http://qiita.com/nezuq/items/8b9438108b5195a3c0bf  
Qiita - Excel単体テスト仕様書からIE自動操作用のVBSコードを自動生成する。  
http://qiita.com/nezuq/items/21d191b3f0e494d78215
