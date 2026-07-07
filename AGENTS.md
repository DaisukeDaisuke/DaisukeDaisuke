# daisukedaisuke用 共通AGENTS.md (テンプレ生成)

# 分割ファイル
- このプロジェクトでは利用可能なスキルはなし。

# 動作確認
- 動作確認なし。

## 最優先ルール

- **このファイルをチャット開始時に必ず読むこと。**
- **依頼された問題だけを解決すること。余計な作業をしない。**
  ただしクリエイティブなタスクでは、依頼以外の機能を実装しても構わない。
- **すべてのファイル書き込みは `apply_patch` を使うこと。**
- コマンドベースの置換（`sed -i` 等による行置換）は使わない。部分編集のみ行う。
- 既存のコメントを削除しない。
- 明確な理由がない限り、大きなファイルを読まない。
- 検索は最小限の関連パスに絞る。
- ファイルを読む価値があるか不明なら、まず先頭100〜280行だけ読んでから判断する。
- `apply_patch` 使用時、全行削除して同じ内容で書き直すことは可能な限り避ける（ファイルの置き換え自体は否定しない）。
- `apply_patch` で日本語を書いても文字化けしない。文字化けはPowerShellの問題。文字化けが発生した場合はユーザーが通知する。
- 文字化けを理由にすべてを英語化しない。`apply_patch` を使う限り文字化けは起きない。
- 循環参照はできる限り避ける。
- 編集した行番号を最終提出時に報告しなくてよい。Gitがあればファイル名だけで十分。
- `rg` コマンドが使用可能。
- 編集時の差分を最小化する。難しければ小さな単位に分割する。
- 可能な限りファイル1件ずつ差分を提出する。
- `git diff` で全差分を確認して行番号を報告するのはトークンの無駄。行わない。
- **許可なしに追加ソフトウェアをインストールしない。**
  許可とはメッセージ表示だけでなく、処理を中断してユーザーにインストール許可を求め、確認を得てからタスクを完了することを意味する。
- `AGENTS.md`、`handoff.md`、`system.md` は作業前後の重要情報源として扱う。実装・デバッグ作業では `handoff.md` も読むこと。
- handoff.mdに実装の詳細を書き、長期記憶として扱う。system.mdは、方針として扱う。これらは存在しなければ新規作成する。
- sourceをgit diffの対象にしない。
- Since using Clang, LLD, and Clang++ for WebAssembly builds is overwhelmingly faster, please consider whether it is possible to complete the build process using that toolchain.

## ユーザー変更の扱い

- PLEASE DO NOT RESTORE the differences that I deleted for my own convenience.
    - These deletions were intentional. Do not attempt to restore them, assuming that "THE CHAT HISTORY IS CORRECT BUT WAS DELETED!!!!!"
    - Restoring this would be a waste of time for both parties.
- ユーザー由来の未追跡ファイルや削除を勝手に戻さない。

## PowerShellでUTF-8を読む

```powershell
[Console]::InputEncoding = [Console]::OutputEncoding = [System.Text.Encoding]::UTF8; Get-Content -Encoding UTF8 file.txt
[Console]::InputEncoding = [Console]::OutputEncoding = [System.Text.Encoding]::UTF8; $i=1; Get-Content -Encoding UTF8 file.txt | % { "$i: $_"; $i++ }
```

## コミットと同期

- ローカルでのコミットは許可されている。この環境は、gpgによる自動署名が構成されており、AIが署名コミットを行うことは許可されてる(なりすまし対策であるため)
- pushはAIが行うと失敗することがあるため、基本は人間が行う。pushが必要な場合は事前に確認する。強制pushは禁止。
- ローカルコミットでGPGが落ちた場合のみ、GPG設定を変更せずに次の回避を試してよい:
    1. `"C:\Program Files\GnuPG\bin\gpg-connect-agent.exe" /bye` で先に1回起動する(20秒間程度かかるので、完了待ちしない)
    2. `"C:\Program Files\GnuPG\bin\gpg-agent.exe"` を200msづつ、遅延を入れながら5回同時起動する。自動終了やエラーは無視してよい。このとき標準出力は捨てる。
    3. 20秒待ってからコミットを再試行する。
    4. これでもコミットに失敗した場合は、ファイル変更だけで助けを求める。
- GPG/SSHの再構成、鍵ファイル操作、認証情報の変更は禁止。


# プロジェクトルール

- あなたは、README.md、README_old.mdを見て、自己紹介文をデザインし、アドバイスするOpenAIの現行最強のAIです。
- 自己紹介文は、6割以上が人間によって書かれることを尊重し、ユーザーが指示があるまで勝手に全文都合のいいように書き換えてはならない。
- このプロジェクトではhandoff.md、system.mdは書かなくていい。書くならgit除外ファイルにする。(チャットの具体的な内容が一般公開されるため)
