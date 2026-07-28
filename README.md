### evar0801

Minecraft Forge mod開発と実運用サーバー運用を通じて、設計判断・障害対応・自律的なツール活用を独学で積み重ねてきました。専門学校でセキュリティを専攻中。

**ポートフォリオ → https://evar0801.github.io/**
作ったものと、その設計判断を1ページにまとめています（10分ほどで読めます）。

以下は3つの作品の要約です。

---

### 第1幕: [fc8weight](https://github.com/evar0801/fc8weight)

EpicFight連携の重量・筋力ゲートmod。小規模・単機能だからこそ、設計判断を隅々まで説明できる1本目です。武器ごとの「必要筋骨」1つから、装備可否・攻撃力ボーナス・移動速度ペナルティの3つを導きます。主軸は素材ティア表（ゲームの進行度に沿う）で、現実の比重モデルは**捨てずに降格させ**、約270modの環境で必ず出会う未知の武器へのフォールバックとして残しています。Mixin不使用の純イベント駆動、未知入力への安全な劣化(NaNフォールバック)まで、判断の理由を`docs/DESIGN_LOG.md`に記録しています。

### 第2幕: [ShauraDungeonMod](https://github.com/evar0801/ShauraDungeonMod)

約12,000行の大規模mod。Re:Zero「シャウラ」モチーフのダンジョンmodで、ボス演出設計・依存度による感情パラメータの分岐システム・ローカルLLM(Ollama)を使った自由会話レイヤーまで作り込んでいます。ローカルLLMは「マシンスペック・モデルの質・APIコスト」の3方向すべてで技術的な壁にぶつかり、そこから導いた結論を正直に書いています。

### 第3幕: MCP-IDS

ハッカソンにチームで参加した成果物（**実装は自分が担当**。最後の発表だけ区間で分け、内容を共有してメンバーに話してもらう形にしました）。MCP経由の**間接プロンプトインジェクション**を、エージェントと外部サーバーの間にプロキシを挟んで捕捉し、「外部データに紛れた**どの一文**が、**実際にどの危険なツール呼び出し**を引き起こしたか」を因果リンクで提示するフォレンジック・ツールです。プロキシ傍受＝NIDSの配置そのもので、専攻のネットワークセキュリティをエージェント通信へ輸入しています。

反実仮想リプレイ（注入あり100%発火／マスクすると0%）で因果を統計的に示し、検知はAgentDojo（注入27・正常97）でTPR 100% / FPR 6%。Base64・ゼロ幅文字による難読化は正規化層で捕捉しています。

**2026年7月29日に外部企業の評価を受ける予定**のため、リポジトリはそれまで非公開です。

---

### その他の自作mod

友人向けに実運用しているForgeサーバー（約270mod）のために書いた小規模companion mod群です。他modの想定外の挙動にぶつかったときは、AIエージェントにバイトコード解析をさせて原因を絞り込み、**原modのjarを一切改変せずMixin/Forgeイベントだけで解決する**スタイルで一貫しています。

| mod | 内容 |
|---|---|
| `epicfight_stamina_attack` | EpicFightの通常攻撃でスタミナを消費させ、不足時は攻撃をキャンセル |
| `wom_weapon_damage` | Weapons of Miracles固有武器のダメージバランス調整（jar非改変） |
| `cataclysm_dungeoneye_shim` | Cataclysmのクラス移動に伴う互換シム。旧パッケージ名を復元して依存modを救済 |
| `bu_armor_buff` | Bosses Unleashedの防具防御力をMixinで底上げ |
| `fc8cataweapons` | Cataclysm近接武器のダメージを進行段階別に再調整 |
| `fc8tomagic` | Traveloptics echo curioのバランス調整（マナ消費・耐久の仕様変更） |
| `fc8stance` | EpicFight向けDawnCraft風スタンス切替（攻撃/防御・熱量ループ） |
| `epicskillsfix` | epicskillsのtick処理のNPEクラッシュを止めるcompanion soft-fork |
| `fc8kit` | PST機動力サージのキーバインド等の小改善 |
| `fc8relickeep` | Curiosアイテムを死亡時も装備維持（Corpse mod非対応環境向け） |
| `fc8bossdmg` | 追跡対象ボスの全ダメージをconfig倍率でスケーリング |
| `fc8efnvfx` | EpicFight Nightfallのクライアント専用VFXをサーバーで無効化し、Distクラッシュを解消 |
| `fc8vanillanerf` | EpicFight戦闘モード外のバニラ近接ダメージを大幅減衰させるDawnCraft風ナーフ |
| `fc8sculkfix` | Sculk Sicknessのレンダリング判定にある演算子優先順位バグを修正 |

いずれも「他modのjarを直接改変せず、Mixin/Forgeイベントで挙動だけを差し替える」という同じ設計思想で書いています。

---

### フィードバック歓迎

各リポジトリのIssue/Discussionでの指摘・改善提案を歓迎します。
