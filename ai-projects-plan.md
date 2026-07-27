# AIエージェント/AX プロダクト立ち上げ計画

> 作成: 2026-07-09 / owner: hiroshi_takizawa / GitHub org: hiroshi57 (Public)
> ローカル配置: `C:/Users/hiroshi_takizawa/<repo>` / 差別化必須・模倣禁止
> ※案件は追加予定（「他の案件も追加します」）

## 開発順
6 → 5 → 1 → 4 → 2 → 3 → 7 → 8 → B/C系（順序未確定）

## タスク台帳

### 原案 1-8（成果: scaffold + 動く最小1機能）

| # | repo | 概要 | 差別化 | status |
|---|------|------|--------|--------|
| 1 | dify-rag-approval-agent | Dify社内RAG+承認フロー | 引用必須+監査ログ | ✅本番+尖った武器(規程改定差分追跡+回答陳腐化検知, test28) |
| 2 | tool-calling-agent-mvp | function callingツール操作 | ドライラン+可逆ログ | ✅本番+尖った武器(操作リスクスコアリング+承認ポリシー, test25) |
| 3 | agent-roi-poc | ROI導入前後比較PoC | 信頼区間+人間介入率 | ✅本番+外販強化(因果推論ROI:合成対照法+DID+プラセボ検定, test27) |
| 4 | context-rerank-search | RAG+リランキング検索 | 根拠説明+eval同梱 | ✅本番+尖った武器(反実仮想説明:なぜ他文書が負けたか, test21) |
| 5 | geo-audit-tool | 生成AI検索GEO診断 | 構造スコア+競合比較 | ✅本番+外販強化(日本語×業界別GEO+Share of Voice引用シェア時系列, test26) |
| 6 | ai-platform-template | AI基盤テンプレート ★土台 | LLM自動ルーティング+観測性 | ✅本番+外販強化(FinOps for LLM:月次コスト予測+予算アラート+予算内ルーティング, test31) |
| 7 | proactive-agent-ux | プロアクティブUX | 提案理由+ワンクリック | ✅本番+尖った武器(バンディット型提案ランキング Thompson, test23) |
| 8 | physical-ai-llm-demo | LLM×シミュレータ | プラン安全性検証 | ✅本番+尖った武器(形式的安全仕様エンジン:宣言的不変条件+反例, test32) |

### B/C系（成果: repo + 仕様書ドラフト → 承認後に実装）

| # | repo | 概要 | 差別化 | status |
|---|------|------|--------|--------|
| B1 | ax-audit-platform | AX診断→PoC見積自動化 | マーケ5業務プリセット+ドメイン知識 | ✅本番+尖った武器(業界ベンチマーク偏差値+ROI感度分析, test24) |
| B2 | ai-advisor-os | AI顧問OS 1人50社 | 顧問承認フロー+匿名ベンチマーク | ✅本番+尖った武器(顧問トリアージエンジン:リスク×価値で50社優先順位, test26) |
| B3 | d-airs-dashboard | AI定着スコアD-AIRS | 定着継続計測+介入効果測定 | ✅本番+尖った武器(定着将来予測+離脱早期予兆, test23) |
| B4 | matching-agent-engine | 対話型マッチング(アダプタ式) | 実在IDのみ+広告示唆還元 | ✅本番+尖った武器(成約寄与条件uplift分析→広告ターゲティング, test22) |
| C1 | dev-agent-platform | 開発エージェント生産性基盤 | AI寄与率計測→営業転用 | ✅本番+尖った武器(AI寄与の因果効果推定+ゲーミング検知, test23) |

**全13リポジトリ 差別化コア実装+push完了(2026-07-09)。B/C系の全機能拡張は承認後。**

全リポジトリ作成済み: 2026-07-09

### 追加案件（2026-07-24〜）

| # | repo | 概要 | 差別化 | status |
|---|------|------|--------|--------|
| A1 | corral | Claude Code/Codex 複数エージェントを1つの司令塔から統率するWebオーケストレーター | Orca/herdr等**海外7ツールを統合＋日本語化**。①Web司令塔ペイン ②台数一括起動＋broadcast（継続run方式でワンショットCLIの文脈を保持）③worktree隔離 ④差分レビュー→承認 ⑤**セキュリティ設計を最初から**（Hostヘッダ検証=DNSリバインディング遮断／x-corral-tokenでCSRF遮断／プロンプトをargv非経由=インジェクション不可）。一次情報で機能検証・日本語ドキュメント同梱 | ✅repo作成+push(2026-07-24) / Vercelデモ配信済 / server(Express+ws)+web(Vite+React) |

> corral: GitHub https://github.com/hiroshi57/corral / ローカル `C:/Users/hiroshi_takizawa/corral` / デモ https://corral-tau.vercel.app
> **ターゲット顧客**: Claude Code/Codex を業務導入し始めた開発チーム・受託/SIer（複数エージェント並行運用でタブ管理・レビュー・セキュリティに不安がある層）。
> **課題**: ①並行運用の煩雑さ(タブ往復) ②レビュー/承認の属人化 ③ローカル実行のセキュリティ不安 ④海外ツールは英語UI。
> **収益仮説**: 個人=OSS無償 → チーム/企業向け有償(SSO・監査ログ・リモート接続・共有ワークスペース)。
> **進め方**: 原案1-8方式（動く最小＋差別化コアを先行実装。MVP稼働済 = server(Express+ws)+web(Vite+React)、DEMO/本番モード、継続run、セキュリティ標準装備）。
> ※本体はローカル常駐デーモン（実CLI起動・worktree操作）。Vercelは**ブラウザ内デモ**（VITE_CORRAL_DEMO=1）でUI/UX確認用。
> **外販ロードマップ（機能30提案・価格プラン）**: `corral/docs/productization.md`（GitHub: https://github.com/hiroshi57/corral/blob/main/docs/productization.md ）。
> **最優先5**: ①通知(Chatwork) ②エージェントFinOps ③生産性ダッシュボード ④マルチテナント ⑤SSO/RBAC。
> **フェーズ**: P1=SaaS土台(テナント/SSO/RBAC/監査ログ/課金) → P2=差別化(FinOps/ダッシュボード/Chatwork通知/インラインレビュー/PR自動化) → P3=エンプラ(クラウド実行/サンドボックス/オンプレVPC/ガードレール/マルチリポ)。
> **差別化の核**: 日本語ファースト＋国内コンプラ＋Chatwork / セキュリティ標準装備 / エージェントFinOps / 全エージェント中立ハブ。
> **進捗(2026-07-24)**: 最優先5を全実装・本番反映済。
>   ① 通知(Chatwork/Slack/アプリ内・通知センター) / ② FinOps(トークン・コスト計測/予算アラート/ハードキャップ) /
>   ③ 生産性ダッシュボード(KPI・状態内訳・案件別コスト・累積推移・将来予測・自動総評, recharts) /
>   ④ マルチテナント(**ワークスペース=案件**の器。全タスク/コスト/レビューを案件単位に分離) /
>   ⑤ 認証/RBAC(dev+Google OIDC・HMACセッション・owner/admin/member/viewer 権限マトリクスで API/UI ゲート)。
>   実機で 案件分離・401/403/404・viewer作成拒否 を検証。デモ https://corral-tau.vercel.app に反映。

## Vercel 本番デプロイ（2026-07-17・全12本 200 OK確認済み / レスポンシブ対応済み）

> standalone.html を静的公開。#2 tool-calling-agent-mvp はCLIツールのため対象外。
> 2026-07-17 レスポンシブ強化を全12本に注入・再デプロイ済み（@media max-width:640px / テーブル横スクロール / メトリクス縦積み / viewport）。本番反映を curl で確認済み。
> scope: takizawahiroshi-gmailcoms-projects / デプロイ元: `C:/Users/hiroshi_takizawa/vercel-deploys/`

| repo | 本番URL |
|------|---------|
| dify-rag-approval-agent | https://dify-rag-approval-agent.vercel.app |
| agent-roi-poc | https://agent-roi-poc.vercel.app |
| context-rerank-search | https://context-rerank-search.vercel.app |
| geo-audit-tool | https://geo-audit-tool-delta.vercel.app |
| ai-platform-template | https://ai-platform-template-ten.vercel.app |
| proactive-agent-ux | https://proactive-agent-ux.vercel.app |
| physical-ai-llm-demo | https://physical-ai-llm-demo.vercel.app |
| ax-audit-platform | https://ax-audit-platform.vercel.app |
| ai-advisor-os | https://ai-advisor-os-three.vercel.app |
| d-airs-dashboard | https://d-airs-dashboard.vercel.app |
| matching-agent-engine | https://matching-agent-engine.vercel.app |
| dev-agent-platform | https://dev-agent-platform.vercel.app |
| corral（デモ / 追加案件） | https://corral-tau.vercel.app |
