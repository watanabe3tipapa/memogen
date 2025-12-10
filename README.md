# MEMOGEN

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Version](https://img.shields.io/badge/version-0.1.0-green.svg)

---

## 使い方

### メモの作成について
  - ブランチが main でない場合は URL 中の main を変更してください。
  - filename=docs/NEW_PAGE.md を希望のファイル名に変更してください。
  - value= の内容を編集する場合は URL エンコードして入れてください。
    例: "# タイトル\n\n本文" → "%23%20タイトル%0A%0A本文"
    
  - （応用）ターミナルからクリップボードを使用して”新規作成”する方法もあります
    ```bash
    echo "%23%20タイトル%0A%0A本文" | xclip -selection clipboard
    ```
   
---

## 新規作成
<div>
  <a href="https://github.com/watanabe3tipapa/memogen/new/main?filename=docs/NEW_PAGE.md&value=%23%20新しい%20メモ%0A%0Aここに内容を記入してください。" target="_blank" rel="noopener">
    <button style="padding:8px 12px; background:#2563eb; color:#fff; border-radius:6px; border:none;">
    ➕ docs/ に新規作成（テンプレート）
    </button>
  </a>
</div>

---

＜しくみ＞
```html
<!-- README.md に貼るボタン：watanabe3tipapa/memogen 用 -->
<div>
  <a href="https://github.com/watanabe3tipapa/memogen/new/main?filename=docs/NEW_PAGE.md&value=%23%20新しい%20メモ%0A%0Aここに内容を記入してください。" target="_blank" rel="noopener">
    <button style="padding:8px 12px; background:#2563eb; color:#fff; border-radius:6px; border:none;">
      docs/ に新規作成（テンプレート）
    </button>
  </a>
</div>

<!-- 使い方メモ:
  - ブランチが main でない場合は URL 中の main を変更してください。
  - filename=docs/NEW_PAGE.md を希望のファイル名に変更してください。
  - value= の内容を編集する場合は URL エンコードして入れてください。
    例: "# タイトル\n\n本文" → "%23%20タイトル%0A%0A本文"
-->

```

## 新規作成（フロントマター付き）
<!-- README.md: docs/ に Front Matter 付きテンプレ作成ボタン -->
<div>
  <a href="https://github.com/watanabe3tipapa/memogen/new/main?filename=docs/new-post.md&value=%2D%2D%2D%0Atitle%3A%20%22%22%0Adate%3A%20%222025-12-09T00%3A00%3A00%2B09%3A00%22%0Atags%3A%20%5B%5D%0Adraft%3A%20false%0A%2D%2D%2D%0A%0A%23%20タイトル%0A%0Aここに本文を入力してください。" target="_blank" rel="noopener" style="display:inline-block; padding:8px 12px; background:#0366d6; color:#fff; border-radius:6px; text-decoration:none; font-weight:600;">
    ➕ docs/ に Front Matter テンプレで新規作成
  </a>
</div>


---

## こんな使い方も

手順（ブラウザで直接開いて動作確認する方法）:
下の URL をコピーする（既に OWNER/REPO は設定済み、ブランチは main、ファイル名は docs/new-post.md、テンプレ内容入り）。
https://github.com/watanabe3tipapa/memogen/new/main?filename=docs/new-post.md&value=%2D%2D%2D%0Atitle%3A%20%22%22%0Adate%3A%20%222025-12-09T00%3A00%3A00%2B09%3A00%22%0Atags%3A%20%5B%5D%0Adraft%3A%20false%0A%2D%2D%2D%0A%0A%23%20タイトル%0A%0Aここに本文を入力してください。
ブラウザでその URL を開く（GitHub にログインしていることを確認）。
開いたページでエディタが表示されるので、内容を確認・編集して「Commit new file」を押すと docs/new-post.md が作成されます。

---


## ローカル側への保存方法

リポジトリ watanabe3tipapa/memogen の指定フォルダを、リポジトリ内と同じディレクトリ構成でローカルにダウンロードします。
必要なら GITHUB_TOKEN を環境変数にセットして非公開リポジトリやレート上限対策に使えます。

### 使い方
ダウンロードしたいパスで次を実行します
- ファイルとして保存（例: download_folder.zsh）
- 実行権を付与: `chmod +x download_folder.zsh`
- 実行: `./download_folder.zsh`


スクリプト（zsh）は以下のとおり: download_folder.zsh

```
#!/usr/bin/env zsh
set -euo pipefail

# 設定: 必要に応じて書き換える
OWNER='watanabe3tipapa'
REPO='memogen'
TARGET_PATH='assets/images'   # ダウンロードしたいフォルダ（リポジトリ内パス）
DEST_DIR='.'                  # ローカルの保存先ルート（既定: カレントディレクトリ）
GITHUB_TOKEN=${GITHUB_TOKEN:-} # 任意: 環境変数にトークンを設定可能

# ヘッダ設定
if [[ -n "$GITHUB_TOKEN" ]]; then
  AUTH_HDR=(-H "Authorization: token $GITHUB_TOKEN")
else
  AUTH_HDR=()
fi

# デフォルトブランチ取得
DEFAULT_BRANCH=$(curl -s "${(@)AUTH_HDR}" "https://api.github.com/repos/$OWNER/$REPO" | jq -r .default_branch)
if [[ -z "$DEFAULT_BRANCH" || "$DEFAULT_BRANCH" == "null" ]]; then
  echo "Failed to get default branch" >&2
  exit 1
fi

# リポジトリツリーを再帰取得して対象パスのファイル一覧を抽出
paths=($(curl -s "${(@)AUTH_HDR}" "https://api.github.com/repos/$OWNER/$REPO/git/trees/$DEFAULT_BRANCH?recursive=1" \
  | jq -r --arg p "$TARGET_PATH/" '.tree[] | select(.type=="blob" and (.path | startswith($p))) | .path'))

if [[ ${#paths[@]} -eq 0 ]]; then
  echo "No files found under $TARGET_PATH" >&2
  exit 0
fi

# ダウンロードループ（公開リポジトリでは raw.githubusercontent.com を利用）
for path in "${paths[@]}"; do
  rel_path="${path}"                         # リポジトリ内の相対パス
  out_path="${DEST_DIR}/${rel_path}"
  out_dir=$(dirname -- "$out_path")
  mkdir -p -- "$out_dir"
  url="https://raw.githubusercontent.com/$OWNER/$REPO/$DEFAULT_BRANCH/$rel_path"
  echo "Downloading: $rel_path"
  # curl の失敗でスクリプト停止させる
  curl -sL -o "$out_path" "$url"
done

echo "Done. Downloaded ${#paths[@]} files to $DEST_DIR/$TARGET_PATH"

```

> 注意
非公開リポジトリとして使用する場合は GITHUB_TOKEN 環境変数を設定してください (export GITHUB_TOKEN="ghp_xxx")。raw.githubusercontent.com は非公開には使えないため、その場合は Contents API を使う追加処理が必要（要望があれば追加します）。
ファイル数が多い場合は並列ダウンロードや既存ファイルの差分チェックを導入してください。


---

## LICENSE

MIT License

---
