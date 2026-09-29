# Playground 設置ルール

このドキュメントを、今後このリポジトリへWebゲームやインタラクティブ試作を追加するときの正本とする。

## 目的

ChatGPTなどで生成したHTML/JavaScript作品を、iPhoneを含む通常ブラウザからHTTPSで実行できる形にする。

ChatGPTの添付HTML、iOSの「ファイル」アプリ、Quick Lookは最終実行環境として扱わない。

## ディレクトリ規約

```text
/
├─ index.html
├─ README.md
├─ docs/
│  └─ DEPLOYMENT_RULES.md
└─ games/
   └─ <slug>/
      └─ index.html
```

- 新作は原則 `games/<slug>/index.html`
- slugは英小文字・数字・ハイフン
- 作品ごとに独立したディレクトリを作る
- 既存作品を上書きして別作品にしない

## ランチャー更新

作品追加時はルート `index.html` に必ず以下を追加する。

- タイトル
- 1〜2行の簡単な説明
- `./games/<slug>/` へのリンク

ランチャーは「作品一覧」として軽量に保つ。

## 実装ルール

- 単純な試作は単一 `index.html` 完結を優先
- 外部ライブラリは必要な場合だけ使い、依存理由を明記
- リンク・アセットはGitHub Pages配下で壊れにくい相対URLを優先
- iPhone Safariのタッチ操作を考慮する
- PC操作がある場合もスマホ用UIを用意する
- JavaScript必須作品には、起動確認用のboot markerを置く
- `localStorage` 等のブラウザAPIは例外で全体停止しないよう防御する

## boot marker

例:

```html
<span id="status">起動中…</span>
<script>
document.getElementById("status").textContent = "● READY";
</script>
```

READYにならない場合は、ゲームロジックより先にJavaScript実行環境を疑う。

## 完了条件

新作の設置完了は、ファイルをGitHubへ置いた時点ではない。

1. GitHubへ追加
2. GitHub Pagesへ反映
3. ランチャーから遷移できる
4. JavaScriptが起動する
5. iPhone Safariで主要操作ができる
6. PCブラウザでも主要操作ができる

ここまで確認して完了とする。

## 正規URL

- ランチャー: `https://1000kaipon.github.io/kaipon-playground/`
- 作品: `https://1000kaipon.github.io/kaipon-playground/games/<slug>/`

最終配布時は添付HTMLではなく、このHTTPS URLを案内する。

## 追加時のAI向け手順

1. このファイルを読む
2. 既存 `index.html` を読む
3. 新作slugを決める
4. `games/<slug>/index.html` を作る
5. ルートランチャーへカードを追加
6. 相対リンクを確認
7. GitHub Pagesの反映を確認
8. iPhone Safariで実動確認
