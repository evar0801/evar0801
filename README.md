### evar0801

Tech.C 1年・スーパーホワイトハッカー専攻。

AI（Claude Code）に任せる範囲と任せない範囲を、ルールではなく仕組みで決めて運用しています。
その上で、友人と遊ぶゲームサーバーの運用と、Minecraft / Valheim の Mod 開発をしています。

**作ったものと、その設計判断 → [evar0801.github.io](https://evar0801.github.io/)**
10分ほどで読める1ページにまとめています。コードより先に、こちらを読んでいただくのが早いです。

[![筋骨が足りず攻撃がキャンセルされた場面](https://raw.githubusercontent.com/evar0801/evar0801.github.io/main/ogp.jpg)](https://evar0801.github.io/)

<sub>筋骨5のキャラクターが鉄の剣（要求10）を振ろうとした場面。攻撃は発生せず、画面下に警告だけが出る。</sub>

---

## いま動かしているもの

| 作品 | 何をするものか | 最初に開くなら |
|---|---|---|
| **[respawnkeeper](https://github.com/evar0801/respawnkeeper)**<br><sub>PowerShell ／ Windows</sub> | ゲームサーバーが落ちたら、**1回目で原因を特定**し、直せるものだけ直して起こし直す。直せないものは止まって人を待つ。友人の Minecraft サーバーのために作り、Valheim へ広げた | [README](https://github.com/evar0801/respawnkeeper#readme)<br><sub>落ちたとき中で何が起きるか</sub> |
| **[brownie](https://github.com/evar0801/brownie)**<br><sub>Python ／ git worktree</sub> | 席を外している間、溜めた作業を**作業票1枚＝使い捨ての Claude Code セッション**で進める。司令塔は LLM ではなく Python。外への送信・公開・削除などの線は機械が持つ | [README](https://github.com/evar0801/brownie#readme)<br><sub>なぜ作ったか・一晩の流れ</sub> |

## 以前に作ったもの

リポジトリ全体を読む必要はありません。右の列が、それぞれ一番見せたい場所です。

| 作品 | 何をするものか | 最初に開くなら |
|---|---|---|
| **[fc8weight](https://github.com/evar0801/fc8weight)**<br><sub>Java ／ Forge 1.20.1</sub> | 装備に重さと筋力要求を足す Mod。武器ごとの「必要筋骨」1つから、**装備できるか・攻撃力・移動速度**の3つを導く | [docs/DESIGN_LOG.md](https://github.com/evar0801/fc8weight/blob/main/docs/DESIGN_LOG.md)<br><sub>捨てた案と、使われなくなったコードの死因まで</sub> |
| **[ShauraDungeonMod](https://github.com/evar0801/ShauraDungeonMod)**<br><sub>Java ／ 約12,000行</sub> | 専用の異世界とボス戦、感情パラメータによる物語分岐。中心に置いたローカルLLMの会話は**3方向すべてで壁にぶつかり**、その結論まで書いた | [README](https://github.com/evar0801/ShauraDungeonMod#readme)<br><sub>作りたかったものと、詰んだ理由</sub> |
| **[MCP-IDS](https://github.com/atmatsuda/techc_hack7)**<br><sub>Python ／ ハッカソン</sub> | AI エージェントが外部の文章に仕込まれた命令に騙される瞬間を、**通信を傍受して捕まえる**。実装は自分が担当 | [viewer/index.html](https://github.com/atmatsuda/techc_hack7/blob/main/viewer/index.html)<br><sub>ダウンロードしてブラウザで開くだけのデモ</sub> |

MCP-IDS はチームのリポジトリにあります。実装を誰が書いたかは[コミット履歴](https://github.com/atmatsuda/techc_hack7/commits/main/)で確認できます。

---

## 運用しているもの

約270個の Mod を入れた Forge サーバーを、友人6人が遊べる状態で維持しています。
上の fc8weight も、そこで実際に動いているものです。

運用の中でぶつかった問題を直すために書いた小さな Mod が、ほかに14個あります。
他の Mod が想定外の動きをしたときは、**そのファイルを一切書き換えず、Mixin と Forge のイベントだけで挙動を差し替える**という同じやり方で通しました。

<details>
<summary>自作 companion mod（14個）</summary>

<br>

| mod | 内容 |
|---|---|
| `epicfight_stamina_attack` | EpicFight の通常攻撃でスタミナを消費させ、不足時は攻撃をキャンセル |
| `wom_weapon_damage` | Weapons of Miracles 固有武器のダメージバランス調整（jar 非改変） |
| `cataclysm_dungeoneye_shim` | Cataclysm のクラス移動に伴う互換シム。旧パッケージ名を復元して依存 mod を救済 |
| `bu_armor_buff` | Bosses Unleashed の防具防御力を Mixin で底上げ |
| `fc8cataweapons` | Cataclysm 近接武器のダメージを進行段階別に再調整 |
| `fc8tomagic` | Traveloptics echo curio のバランス調整（マナ消費・耐久の仕様変更） |
| `fc8stance` | EpicFight 向け DawnCraft 風スタンス切替（攻撃/防御・熱量ループ） |
| `epicskillsfix` | epicskills の tick 処理の NPE クラッシュを止める companion soft-fork |
| `fc8kit` | PST 機動力サージのキーバインド等の小改善 |
| `fc8relickeep` | Curios アイテムを死亡時も装備維持（Corpse mod 非対応環境向け） |
| `fc8bossdmg` | 追跡対象ボスの全ダメージを config 倍率でスケーリング |
| `fc8efnvfx` | EpicFight Nightfall のクライアント専用 VFX をサーバーで無効化し、Dist クラッシュを解消 |
| `fc8vanillanerf` | EpicFight 戦闘モード外のバニラ近接ダメージを大幅減衰させる DawnCraft 風ナーフ |
| `fc8sculkfix` | Sculk Sickness のレンダリング判定にある演算子優先順位バグを修正 |

</details>

---

## 進め方 — AI が書いたコードに、自分が何をしているか

プログラミングを本格的に始めたのは最近ですが、Java も Python も **AI と一緒になら書ける**段階です。
AI が出すコードは動きはしますが、**そのまま使うと冗長になり、あとで直せなくなります。**
自分が実際に手を入れているのは、次の3つです。

| | 具体例 |
|---|---|
| **構造を作り直す** | 移動速度のペナルティが6系統あり、それぞれに上限が付いていた。掛け算で合成されるため **6つ同時に効くと実質停止**すると分かり、「合成してから1回だけ上限を掛ける」形に作り直した（[fc8weight](https://github.com/evar0801/fc8weight)） |
| **判定のしかたを変える** | 攻撃力ボーナスの実装で **バニラのツルハシが「誰も装備できない攻撃力30の武器」**になった。「しきい値で道具と武器を分ける」案は、鉄のツルハシが閾値と同値だと分かった時点で捨て、**型で判定する方式**に切り替えた |
| **AI に渡す前提を管理する** | 各プロジェクトに `CLAUDE.md`（前提・禁止事項）と `DECISIONS.md`（判断ログ）を置き、AI に渡す文脈を明文化。**採用した案だけでなく、捨てた案と、使われなくなったコードがなぜ死んだのか**まで残す |

**サーバーログ解析 API**（非公開）は、**AI に実装コードを書かせないルール**で始めました。
Mod 開発で環境構築まで AI に任せ、自分の理解が追いつかない部分が残ったためです。
ただ、提出の期限に間に合わず、自分の判断でそのルールを外して AI に実装させました。
理解が進んだからではなく間に合わなかったから外した、という経緯も判断ログに残しています。

---

指摘・改善提案は各リポジトリの Issue で歓迎します。
kazu.evar81@gmail.com
