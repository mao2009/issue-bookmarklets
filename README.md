# issue-bookmarklets

ブラウザのブックマークから、Issue（チケット）の情報を特定の形式でクリップボードにコピーするためのブックマークレット集です。
主に **Git のブランチ名** としてそのまま利用することを想定したフォーマットに変換します。

## 使い方

1. 以下の各サービス用のコードをコピーします。
2. ブラウザのブックマークを作成し、URL欄にコピーしたコードを貼り付けて保存します。
3. 対象の Issue 画面を開いた状態で、保存したブックマークをクリックすると実行されます。

---

## Redmine 用

チケット番号とタイトルを取得し、`#1234_チケットタイトル` の形式でコピーします。
（スペースは `_` に、`/` は `.` に置換されます）

```javascript
javascript:(function(){function getRedmineIssueTitle(){const re=/#.*?$/;const ticket=re.exec(document.querySelector("#content h2").textContent);const el=document.querySelector(".subject h3");return ticket+"_"+el.textContent.replace(/\s+/g,"_").replace(/\//g,".");}try{const title=getRedmineIssueTitle();const ta=document.createElement("textarea");ta.value=title;document.body.appendChild(ta);ta.select();document.execCommand("copy");ta.remove();alert("Copied for branch name: "+title);}catch(e){alert("Error: "+e.message);} })();
```

---

## GitHub 用

Issue 番号とタイトルを取得し、`#123_タイトル` の形式でコピーします。

```javascript
javascript:(function(){function getGithubIssueTitle(){const ticket=document.querySelector(".HeaderViewer-module__issueNumberLink__FiaRk").textContent;const el=document.querySelector(".markdown-title");return ticket+"_"+el.textContent.trim().replace(/\s+/g,"_").replace(/\//g,".");}try{const title=getGithubIssueTitle();const ta=document.createElement("textarea");ta.value=title;document.body.appendChild(ta);ta.select();document.execCommand("copy");ta.remove();alert("Copied for branch name: "+title);}catch(e){alert("Error: "+e.message);} })();
```

### 例
- **Issue/チケット番号**: 1234
- **タイトル**: サンプルタイトル
- **取得（コピー）内容**: `#1234_サンプルタイトル`

---

## ライセンス
MIT License - Copyright (c) 2026 mao2009
