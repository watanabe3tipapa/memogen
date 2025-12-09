# MEMOGEN




## 使い方

### メモの作成
  - ブランチが main でない場合は URL 中の main を変更してください。
  - filename=docs/NEW_PAGE.md を希望のファイル名に変更してください。
  - value= の内容を編集する場合は URL エンコードして入れてください。
    例: "# タイトル\n\n本文" → "%23%20タイトル%0A%0A本文"
    ```bash
    echo "%23%20タイトル%0A%0A本文" | xclip -selection clipboard
    ```
   
---

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


<div>
  <a href="https://github.com/watanabe3tipapa/memogen/new/main?filename=docs/NEW_PAGE.md&value=%23%20新しい%20メモ%0A%0Aここに内容を記入してください。" target="_blank" rel="noopener">
    <button style="padding:8px 12px; background:#2563eb; color:#fff; border-radius:6px; border:none;">
      docs/ に新規作成（テンプレート）
    </button>
  </a>
</div>
```

---
