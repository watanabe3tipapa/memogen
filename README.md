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
      docs/ に新規作成（テンプレート）
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

## LICENSE

MIT License

---
