# 電閃－DENSEN－｜インフラ構成ドキュメント

**作成日**: 2026年4月14日  
**更新日**: 2026年4月15日  
**管理者**: アンタレス  
**原則**: finance-appとは完全分離・独立運用

---

## 1. ローカルフォルダ構成（確定）

```
C:\Users\User\OneDrive\デスクトップ\densen-project\   ← 電閃プロジェクト大本
├── biribiri-quiz-app\     ← ビリビリ⚡クイズ専用フォルダ（独立git）
│   └── index.html
├── densen-site\           ← 電閃メインサイト（独立git）
│   ├── index.html
│   ├── about.html
│   ├── links.html
│   ├── knowledge\
│   │   └── index.html
│   └── css\
│       └── style.css
├── docs\
│   ├── infrastructure.md  ← このファイル
│   └── project-context.md
├── assets\
└── README.md
```

> **注意**: `biribiri-quiz-app/` と `densen-site/` はそれぞれ独立した `.git` を持つ別リポジトリ。
> densen-project ルートの `.git`（biribiri-quiz GitHub）とは別管理。

---

## 2. インフラ全体構成

| レイヤ | サービス | アカウント/プロジェクト名 | 状態 |
|---|---|---|---|
| ソース管理 | GitHub | `100antares8/biribiri-quiz`（biribiri-quiz-appの中身） | ✅ 運用中 |
| ソース管理 | GitHub | `100antares8/densen-site`（メインサイト） | ✅ リポジトリ作成済み |
| ホスティング | Vercel | `biribiri-quiz` プロジェクト | ✅ 運用中 |
| ホスティング | Vercel | `densen-site` プロジェクト | 🔲 デプロイ待ち |
| DB・認証 | Supabase | DENSEN専用（新規作成） | 🔲 必要時に作成 |
| SNS | X（Twitter） | @densen_ai | ✅ 運用中 |
| Google | Googleアカウント | DENSEN専用 | ✅ 分離運用中 |

---

## 3. 公開URL一覧

| コンテンツ | URL | 状態 |
|---|---|---|
| ビリビリ⚡クイズ v0.1 beta | https://biribiri-quiz.vercel.app/biribiri-quiz-app/ | ⚠️ Vercel設定更新待ち |
| 電閃－DENSEN－メインサイト | https://densen-site.vercel.app/ | 🔲 デプロイ待ち |

> **biribiri-quiz**: フォルダ名を `biribiri-quiz` → `biribiri-quiz-app` に変更したため、
> Vercelのプロジェクト設定（Root Directory）を `biribiri-quiz-app` に更新が必要。

---

## 4. GitHub構成

| リポジトリ | ローカルフォルダ | 用途 | 状態 |
|---|---|---|---|
| `100antares8/biribiri-quiz` | `densen-project/biribiri-quiz-app/` | ビリビリ⚡クイズ | ✅ 運用中 |
| `100antares8/densen-site` | `densen-project/densen-site/` | 電閃メインサイト | ✅ リポジトリ作成済み |

---

## 5. Vercel構成

| Vercelプロジェクト | GitHubリポジトリ | Root Directory | URL |
|---|---|---|---|
| `biribiri-quiz` | `biribiri-quiz` | `biribiri-quiz-app` ⚠️要更新 | `biribiri-quiz.vercel.app` |
| `densen-site` | `densen-site` | `/`（ルート） | `densen-site.vercel.app` 🔲 |

---

## 6. Supabase利用方針

### 基本方針
- **finance-appのSupabaseとは完全別アカウント or 別プロジェクトで管理**
- DENSEN専用Supabaseプロジェクトを新規作成して利用する
- 今すぐは不要。必要になったタイミングで作成する

### 導入タイミング（目安）

| フェーズ | 機能 | Supabase用途 |
|---|---|---|
| PH0（現在） | ビリビリクイズ静的版 | **不要** |
| PH1 | クイズスコア保存・ランキング | PostgreSQL（スコアテーブル） |
| PH1 | メインサイト会員登録 | Auth（認証） |
| PH2 | 有料コンテンツ・購入履歴 | PostgreSQL + Storage |
| PH3 | SaaS化・総合ハブ | フル活用 |

### 作成時の手順メモ（未実施）
1. https://supabase.com で新規アカウント作成（DENSEN専用Googleアカウントで登録）
2. プロジェクト名: `densen-site`
3. Regionは `Northeast Asia (Tokyo)` を選択
4. finance-appのSupabaseとは**絶対に混在させない**

---

## 7. 分離原則（最重要）

> **電閃－DENSEN－のインフラは、finance-appを含む他プロジェクトと一切共有しない。**
> GitHubリポジトリ・Vercelプロジェクト・SupabaseプロジェクトはすべてDENSEN専用を新規作成して使用する。

---

## 8. 更新履歴

| 日付 | 内容 |
|---|---|
| 2026-04-14 | ドキュメント新規作成。GitHub・Vercel・Supabase分離方針を確定。biribiri-quiz公開完了。 |
| 2026-04-15 | フォルダ構成更新。biribiri-quiz → biribiri-quiz-app にリネーム。densen-site作成・densen-project内に配置。 |

---

*電閃－DENSEN－｜インフラ構成ドキュメント*  
*© 2026 Antares Eight — 内部資料*
