# MathCards Ver. 1.5.0 — MathLive ローダー修正

## 修正内容

以前の MathLive の読み込みは `mathlive.min.js` と `window.MathfieldElement` に依存していました。今回は ES モジュールを動的に読み込み、`customElements.get('math-field')` で登録を確認する方式に変更しました。読み込み先はローカル vendor → jsDelivr ESM → esm.sh の順です。エラーの詳細も表示します。

**重要：この配布物には MathLive 本体を同梱できていません。** この実行環境からパッケージ配布サイトへの DNS 接続ができなかったためです。CDNが利用できるネットワークでは視覚的数式編集を試せますが、完全オフライン対応はまだ完成していません。KaTeXも引き続きCDN依存です。

## 起動

このフォルダ内で `python3 -m http.server 8000` を実行し、`http://localhost:8000` を開いてください。画面に `Ver. 1.5.0` と表示されることを確認してください。以前のサービスワーカーの影響がある場合は、Chrome開発者ツールの Application → Service Workers から旧ワーカーを解除し、ページを再読み込みしてください。

## オフライン MathLive の導入（手動）

`vendor/mathlive.min.mjs` に **MathLive 0.104.2 のブラウザ向けESモジュール版（依存アセットも含む）** を配置してください。MathLiveの配布形式によってはフォント等の追加ファイルと参照パス調整が必要です。単に任意のJSを改名しても動作するとは限りません。

既存データは IndexedDB に保存されます。更新前のJSONバックアップを推奨します。
