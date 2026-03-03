# Git ワークフローガイドライン

このドキュメントは、このリポジトリで使用するブランチ戦略とコミットメッセージの規則を定義しています。

---

## 目次

1. [ブランチ戦略](#ブランチ戦略)
2. [コミットメッセージ規則](#コミットメッセージ規則)
3. [英語の単語・フレーズ集](#英語の単語フレーズ集)

---

## ブランチ戦略

### 概要

ブランチは**ユニット単位**で切り、コミットでそのユニット内の学習ステップを記録します。
ブランチ = 学習の「章」、コミット = 「ページ」というイメージです。

```
main
 └── study/android-basics-compose/unit1
 └── study/android-basics-compose/unit2
 └── docs/update-readme
 └── fix/unit2-dice-not-rolling
```

### ブランチの種類

| プレフィックス | 使うタイミング | 例 |
|---|---|---|
| `study/` | コースのユニットを学習するとき（メインのブランチ種別） | `study/android-basics-compose/unit3` |
| `fix/` | バグや誤った動作を修正するとき | `fix/unit2-dice-not-rolling` |
| `docs/` | ドキュメントのみの変更 | `docs/update-readme-structure` |
| `chore/` | メンテナンス作業（整理・設定変更など） | `chore/remove-unused-imports` |

### 命名ルール

- **小文字とハイフン**のみ使用する。スペース・アンダースコア・大文字は使わない。
- `study/` ブランチにはコース略称とユニット番号を含める:
  `study/<コース略称>/unit<番号>`
- **短く、かつ内容が伝わる**名前にする。

```
✅  study/android-basics-compose/unit1
✅  study/android-basics-compose/unit2
✅  fix/unit1-text-overflow
✅  docs/add-git-workflow
❌  Study/Unit1
❌  unit1_branch
❌  my-branch
```

### 基本的な作業フロー

```
# 1. main から新しいユニット用ブランチを作成する
git switch main
git pull
git switch -c study/android-basics-compose/unit3

# 2. 学習を進めながら、ステップごとにこまめにコミットする
git add .
git commit -m "feat(unit3/tip-time): add TipTime project initial setup"
git commit -m "feat(unit3/tip-time): add text fields for bill and tip input"
git commit -m "feat(unit3/tip-time): implement tip calculation logic"

# 3. ユニット内の全プロジェクトが完了したら完了コミットを積む
git commit -m "chore(unit3): complete unit3 — all projects done"

# 4. main にマージする
git switch main
git merge --no-ff study/android-basics-compose/unit3

# 5. マージ後はブランチを削除する
git branch -d study/android-basics-compose/unit3
```

> 💡 **進捗確認のヒント:** `chore(unitN): complete unitN` というコミットを規則化しておくと、
> `git log --oneline --grep="complete unit"` で全ユニットの完了履歴を一覧できます。

---

## コミットメッセージ規則

このリポジトリは **[Conventional Commits](https://www.conventionalcommits.org/)** の仕様に従います。

### フォーマット

```
<type>(<scope>): <subject>

[任意: 本文]

[任意: フッター]
```

### タイプ一覧

| タイプ | 使うタイミング |
|---|---|
| `feat` | 新しいコードや機能を追加するとき |
| `fix` | バグを修正するとき |
| `docs` | ドキュメントのみの変更（README、コメントなど） |
| `style` | ロジックに影響しない書式変更（空白など） |
| `refactor` | バグ修正や機能追加を伴わないコードの再構成 |
| `chore` | ビルドスクリプト・設定・依存ライブラリの更新、**ユニット完了の記録** |
| `test` | テストの追加・更新 |

### スコープ（任意）

ユニット / プロジェクト名をスコープに使うと文脈が明確になります。

```
feat(unit2/dice-roller): add dice image using Image composable
fix(unit1/happy-birthday): correct text alignment on small screens
chore(unit2): complete unit2 — all projects done
docs(readme): update repository structure section
```

### subject（件名）のルール

- **命令形**で書く。過去形・進行形は使わない。
  - ✅ `add roll button` / ❌ `added roll button`
  - ✅ `fix layout padding` / ❌ `fixed layout padding`
- 最初の文字は**小文字**にする。
- 末尾に**ピリオドをつけない**。
- **72文字以内**に収める。

### 記述例

学習の流れに沿ったコミットのイメージです：

```
# ユニット開始
chore(unit2): start unit2 — Building App UI

# プロジェクトの実装ステップをこまめに記録する
feat(unit2/dice-roller): add initial project setup
feat(unit2/dice-roller): add dice image display using Image composable
feat(unit2/dice-roller): add roll button with click handler
feat(unit2/dice-roller): connect button click to random dice result
refactor(unit2/dice-roller): extract DiceWithButtonAndImage into separate composable
fix(unit2/dice-roller): fix dice image not updating on first tap

# ユニット完了
chore(unit2): complete unit2 — all projects done
```

---

## 英語の単語・フレーズ集

コミットメッセージを英語で書くための参考ガイドです。

### 動詞 — コミットメッセージの核となる言葉

**命令形**（`-ed` や `-ing` を付けない原形）で使います。

| 動詞 | 意味 | 例 |
|---|---|---|
| `add` | 新しいものを追加する | `add loading spinner to dice roller` |
| `remove` | 削除する | `remove unused color resources` |
| `fix` | バグや誤りを直す | `fix crash when rolling dice twice` |
| `update` | 既存のものを更新する | `update min SDK version to 24` |
| `change` | 何かを変更する | `change button color to primary` |
| `rename` | 名前を変える | `rename GreetingText to BirthdayMessage` |
| `move` | 場所を移動する | `move theme files to ui/theme directory` |
| `refactor` | 動作を変えずにコードを整理する | `refactor dice logic into ViewModel` |
| `extract` | 一部を切り出す | `extract composable into separate file` |
| `implement` | 機能を実装する | `implement click handler for roll button` |
| `replace` | 置き換える | `replace hardcoded string with string resource` |
| `simplify` | シンプルにする | `simplify padding logic in layout` |
| `correct` | 間違いを正す | `correct typo in greeting message` |
| `improve` | 改善する | `improve readability of MainActivity` |
| `apply` | 適用する | `apply Material3 theme to app` |

### 名詞 — スコープや件名でよく使う言葉

| 単語 | 意味 |
|---|---|
| `layout` | レイアウト |
| `composable` | Compose の UI コンポーネント |
| `viewmodel` | ViewModel |
| `state` | 状態 |
| `button` | ボタン |
| `image` | 画像 |
| `text` | テキスト |
| `padding` | 余白 |
| `color` | 色 |
| `theme` | テーマ |
| `resource` | リソース |
| `string resource` | strings.xml の文字列リソース |
| `drawable` | 画像などの Drawable リソース |
| `dependency` | 依存ライブラリ |
| `build config` | ビルド設定 |
| `crash` | クラッシュ |
| `typo` | タイプミス |
| `comment` | コメント |
| `import` | import 文 |
| `handler` | イベントハンドラ |
| `callback` | コールバック |

### よく使うフレーズ

| フレーズ | 使うタイミング |
|---|---|
| `based on course material` | コース内容に基づいて実装したとき |
| `following best practices` | ベストプラクティスに沿って変更したとき |
| `as per unit N` | Unit N の内容に従って実装したとき |
| `for readability` | 可読性向上のための変更 |
| `to avoid hardcoded values` | ハードコーディングを避けるための変更 |
| `per lint warning` | lint の警告に対応したとき |
| `initial project setup` | プロジェクトを作成した最初のコミット |
| `start unitN — <unit title>` | ユニットの学習を開始するとき |
| `complete unitN — all projects done` | ユニット内の全プロジェクトが完了したとき |

### 本文（任意の詳細説明）

1行の件名だけでは説明しきれない場合は、空行を挟んで本文を追加します。

```
refactor(unit2/dice-roller): extract dice result logic into separate function

Moved the dice result calculation out of the onClick lambda and into a
named function `rollDice()` to improve readability and make the logic
easier to test in the future.
```

---

> 💡 **ヒント:** コミットメッセージの英語表現に迷ったときは、やったことを日本語で GitHub Copilot に伝えてみてください。適切な英語のコミットメッセージを提案してくれます。
