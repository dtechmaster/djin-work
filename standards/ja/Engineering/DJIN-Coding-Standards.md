# DJIN Tech — コーディング基準

> 明確な構造。関数型パラダイム。関数を通じたシンプルさ。コアにZod。人間が読める。

---

## コードスタイル

### Composition API & TypeScript のみ

* `<script setup lang="ts">` を使用
* 明示的に正当化されない限り、Options API を混在させない。

### 関数宣言

* ❌ 匿名関数を避ける: `const x = () => {}`
* ✅ 名前付き関数を使用: `function x() {}`

### #region ブロック

* `// #region` と `// #endregion` を一貫して使用
* `.ts`、`.vue`、およびテンプレートブロックで機能

```vue
<template>
  <!--#region Feature A -->
  <div>{{ sayHello() }}</div>
  <!--#endregion Feature A -->
</template>

<script setup lang="ts">
//#region Imports
import nuxt from 'nuxt'
//#endregion

//#region Feature A
const greeting = 'Hello World!'
function say(str: string) { return str }
function sayHello() { return say(greeting) }
//#endregion
</script>
```

> 💡 VS Code: `[CTRL+K CTRL+8]` ですべての領域を折りたたむ

### Logger の使用

* 存在しない場合、ロギングを処理する `Logger` クラスコンポーザブルを作成
* Logger には常に `log`、`info`、`warn`、`error` メソッドが必要
* ログは `[INFO][YYYY-MM-DD HH:MM:SS][File:Line] Message` のように人間が読める形式であるべき
* すべての `console.log` を `Logger.log` に置き換える

---

### Null許容プログラミング

* すべての値がnullまたはundefinedである可能性があると想定する — 特にネストされたもの
  → 何も信頼しない、自分のコードでさえも。
* ランタイムエラーを避けるためにオプショナルチェーン（`?.`）を一貫して使用
  → `user?.profile?.address?.street`
* Nullish Coalescing（`??`）またはデフォルトファクトリーを使用してフォールバック値を提供
  → `const name = user?.profile?.name ?? 'ゲスト'`
* UIで例外をスローしないでください — 代わりに:

  * `v-if`、`v-else`、またはスケルトン/ローディングコンポーネントを使用
  * データが欠けている場合、ボタンや入力を無効化
  * 明確な検証または警告メッセージを表示
* 楽観的なものよりも防御的な計算プロパティを優先
  → 必要に応じて安全なフォールバックまたはtry/catchガードでラップ
* TypeScriptでも型を深く信頼しないでください — 構造はランタイムで壊れる可能性があります（例：APIまたはlocalStorageから）

---

## アーキテクチャパターン

### ブラックボックスパラダイム

* 絶対に必要でない限り、グローバル状態またはクラスのような構造を避ける
* クラスベースのロジックよりもコンポジションを優先
* すべては関数、オブジェクト、コンポーネント、またはコンポーザブルです。クラス継承なし
* 絶対に必要でない限り、グローバル状態またはクラスのような構造を避ける

### ユーティリティ構造

汎用ロジックを `utils/` に整理:

* `arrays.ts`
* `objects.ts`
* `japanese.ts`
* など

重複を避けるため、新しいユーティリティを実装する前に確認してください。

### コンポーザブル

`useX()` 規約を避けてください。グローバル `$` プレフィックス付きコンポーザブルを使用:

```ts
export default const $myComposable = {
  foo() {
    return 'bar'
  }
} as const
```

* デフォルトエクスポートされた `const` として宣言する必要があります
* `$` で始まる必要があります

---

## Zod を SST（Single Source of Truth）として

### 原則

Zod はシステム内のすべてのインターフェースを定義します:

* バリデーション
* 型
* Props
* シェイプベースのロジック

### インターフェースの種類

| タイプ     | ユースケース                                   | 例                       |
|----------|-------------------------------------------|---------------------------|
| System   | ページ、コンポーネント、コンポーザブル                    | `z.system.pageSchema`     |
| Database | PostgreSQL構造、バリデーション、マイグレーション           | `z.database.userSchema`   |

### メリット

* 同じスキーマから型とpropsを抽出
* 一貫したロジックの中心的な場所
* インターフェースの重複を排除
* システムインターフェースからデータベース構造を構築し、Steve Jobsの哲学を適用できる（`"ユーザーの視点から開発を開始し、その後技術を開発する"`）

共有スキーマをグローバルにアクセス可能なフォルダーに保存し、すべてのレイヤーで再利用します。

### ファイルサイズ

* ファイルは簡潔で、小さく、焦点を絞ったものに保つべきです。ファイルが大きすぎる場合は、小さなファイルに分割する必要があります。`理想的には`、各ファイルには単一の目的があり、2000行未満である必要があります。`理想的には`。

### 命名規則

* インターフェースには `I`、型には `T`、propsには `P` を使用
* インターフェース、型、propsには `camelCase` を使用
* データベースの列、テーブル、マイグレーションには `snake_case` を使用
* 環境変数と設定ファイルには `snake_case` を使用
* 環境変数には `ENV_` プレフィックス、設定ファイルには `CONFIG_` プレフィックスを使用

---

## 実行原則

> コーディング前に常に計画
> "まず問題を解決してください。それからコードを書いてください。" — John Johnson
> "悪いプログラマーはコードを心配する。良いプログラマーはデータ構造とその関係を心配する。" — Linus Torvalds

## CLI

* CLIには常にDenoを使用
* 依存関係管理の問題を避けるためにCLIにはDenoの `npm specifiers` を使用 (https://deno.com/blog/not-using-npm-specifiers-doing-it-wrong)

## テスト

* CLIツール、ユーティリティ、およびコア機能が簡潔で意味がある場合は**常にテストを書く**
* テストはシンプルで、焦点を絞り、主なユースケースをカバーする必要があります
* `Deno.test()` でDenoの組み込みテストフレームワークを使用
* **テスト組織**:
  - プロジェクトルートに `tests/` フォルダーを作成
  - テストファイルは `*.test.ts` という名前で `tests/` フォルダーに配置
  - ソース構造を反映: `src/foo.ts` → `tests/foo.test.ts`
  - CLIプロジェクトの場合、メインテストは `tests/main.test.ts` に配置
* テストの焦点:
  - CLI引数の解析と検証
  - エラー処理とエッジケース
  - 環境変数の読み込み
  - コアビジネスロジック関数
* テストを保守可能に保つ - テストが複雑になった場合、テスト対象のコードのリファクタリングを検討
* テストは高速で独立している必要があります - 可能な限り外部依存やファイルシステムの変更なし

---

## その他のリソース

* 参照用に `./DJIN-standards.md` を使用
* 参照用に `./SYSTEM_SPECS.md` を使用
* 参照用に `./EXECUTION_PLAN.md` を使用
