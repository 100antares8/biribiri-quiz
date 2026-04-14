# 電閃－DENSEN－｜インフラ構成ドキュメント

**作成日**: 2026年4月14日  
**管理者**: アンタレス  
**原則**: finance-appとは完全分離・独立運用

---

## 1. インフラ全体構成

| レイヤ | サービス | アカウント/プロジェクト名 | 状態 |
|---|---|---|---|
| ソース管理 | GitHub | `100antares8 / biribiri-quiz` | ✅ 運用中 |
| ホスティング | Vercel | `biribiri-quiz`プロジェクト | ✅ 運用中 |
| DB・認証 | Supabase | DENSEN専用（新規作成） | 🔲 必要時に作成 |
| SNS | X（Twitter） | @densen_ai | ✅ 運用中 |
| Google | Googleアカウント | DENSEN専用 | ✅ 分離運用中 |

---

## 2. 公開URL一覧

| コンテンツ | URL | 状態 |
|---|---|---|
| ビリビリ⚡クイズ v0.1 beta | https://biribiri-quiz.vercel.app/biribiri-quiz/ | ✅ 公開中 |
| 電閃－DENSEN－メインサイト | 未作成 | 🔲 PH1以降 |

---

## 3. Supabase利用方針

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
2. プロジェクト名: `densen-project`
3. Regionは `Northeast Asia (Tokyo)` を選択
4. finance-appのSupabaseとは**絶対に混在させない**

---

## 4. GitHub構成

| リポジトリ | 用途 | 状態 |
|---|---|---|
| `biribiri-quiz` | ビリビリ⚡クイズ（テスト版・初心者Version） | ✅ 運用中 |
| `densen-project` | 電閃メインサイト＆スマホアプリ（予定） | 🔲 PH1で作成 |

---

## 5. Vercel構成

| Vercelプロジェクト | 対応GitHubリポジトリ | ドメイン |
|---|---|---|
| `biribiri-quiz` | `biribiri-quiz` | `biribiri-quiz.vercel.app` |
| `densen-project`（予定） | `densen-project`（予定） | `densen-project.vercel.app`（予定） |

---

## 6. 分離原則（最重要）

> **電閃－DENSEN－のインフラは、finance-appを含む他プロジェクトと一切共有しない。**
> GitHubリポジトリ・Vercelプロジェクト・SupabaseプロジェクトはすべてDENSEN専用を新規作成して使用する。

---

## 7. 更新履歴

| 日付 | 内容 |
|---|---|
| 2026-04-14 | ドキュメント新規作成。GitHub・Vercel・Supabase分離方針を確定。biribiri-quiz公開完了。 |

---

*電閃－DENSEN－｜インフラ構成ドキュメント*  
*© 2026 Antares Eight — 内部資料*
