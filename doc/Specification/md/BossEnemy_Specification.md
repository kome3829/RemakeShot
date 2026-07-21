# BossEnemy（ボス敵）仕様書
## 概要と設計意図
### 役割
- ゲームの最終目標：ボスステージで待ち受けている最強の敵オブジェクト、ボス敵の撃破がゲームクリアの条件になっています。
- HP連動型の行動変化：雑魚敵とは異なり、残りHPに応じて「移動パターン」と「攻撃（弾幕）パターン」が段階的に変化します。
- UIとの連動：ボスステージでは、画面上部に専用の残りHPに連動したHPバーを表示し、プレイヤーに伝えます。
- 
### 設計意図
- 更新・描画・初期化を自身で管理する。他のクラスに依存しない設計。
- ボステージでのボスとの戦闘がゲームの主軸としています。この部分で楽しませるように考えてゲームを作成しています。
- ボス敵は基本的にボステージでの一騎打ちを想定した敵です
- HPの割合によってボスの状態を管理して、移動、攻撃のパターンを変化させています。
- 
---

## 基本パラメータ（初期設定）
start関数で設定される、自機の基本性能を記載します
### 初期位置
ボスステージのみ出現します。
| ステージ | 出現位置 | 使用定数 | 座標 (X, Y) |
|----------|----------|----------|------------|
| ボスステージ（BOSS_STAGE） | 中央上部（画面外上部） | ` CUT_HALF_VALUE(MAX_SCREEN_WIDTH)`, `BOSS_POP_Y`| (320, 0) |


### 当たり判定・判定のサイズ
- プレイヤー弾限定の当たり判定であり、その他のオブジェクトとは判定をとりません。

#### サイズ
表示画像サイズと同じサイズの正方形です。常に一定でゲーム内で変わることはないです。
| 項目 | 値 | 使用定数 |
|:-----:|:----:|:----------:|
|横幅 | 96 |  `ENEMY_BOSS_WIDTH` |
|縦幅 | 84 |  `ENEMY_BOSS_HEIGHT` |
### 移動速度
### 初期ライフ


---

## 出現処理（pop）


---

## 移動仕様

---

## 攻撃仕様
### 弾発射処理

---

## ダメージ処理
## 表示(描画仕様)

### 表示要素
mDamageCoolDown が true の間表示
### 描画補足

---

## 補足・テクニカル事項

## 使用定数一覧

| 定数名 | 値 | 内容 |
|:-------|:--:|:-----|
| `BOSS_MAX_HP` | 3000 | ボス敵の最大体力 |
| `ENEMY_BOSS_WIDTH` | 96 | ボス敵の画像横幅 |
| `ENEMY_BOSS_HEIGHT` | 84 | ボス敵の画像縦幅 |
| `BOSS_HP_BER_MAXWIDTH` | 315 | HPバーの最大表示幅 |
| `ALPHA_MAX` | 255 | 透過度の最大値（通常表示時） |
| `FADE_ALPHA_STEP` | 25 | ワープ・撃破時の透過度減少量 |
| `HIT_RANGE_MARGIN_X` | 4 | 当たり判定の横方向余白 |
| `HIT_RANGE_MARGIN_Y` | 10 | 当たり判定の縦方向余白 |
| `BOSS_HP_PER_MAX` | 100 | 第1フェーズ開始（HP 100%） |
| `BOSS_HP_PER_PHASE1_END` | 75 | 第1フェーズ終了・第2移行 |
| `BOSS_HP_PER_PHASE2_END` | 50 | 第2フェーズ終了・第3移行 |
| `BOSS_HP_PER_PHASE3_END` | 25 | 第3フェーズ終了・最終移行 |
| `BOSS_HP_PER_DEFEAT` | 0 | 撃破判定（HP 0%） |
| `BOSS_ENEMY_SPD` | 5.0f | ボス敵の基本移動速度 |
| `START_MOVE_DELAY_FRAME` | 30 | 行動切り替え時の移動開始ディレイ |
| `START_MOVE_DAMAGE` | 30 | 行動切り替え時に強制的に減算するHP量 |
| `BOSS_CENTER_POSITION_Y` | 100 | 中央待機時のY座標 |
| `BOSS_WARP_LEFT_POINT_X` | 100 | 巡回・ワープ地点（左）のX座標 |
| `BOSS_WARP_LEFT_POINT_Y` | 220 | 巡回・ワープ地点（左）のY座標 |
| `BOSS_WARP_BOTTOM_POINT_X` | 320 | 巡回・ワープ地点（下）のX座標 |
| `BOSS_WARP_BOTTOM_POINT_Y` | 250 | 巡回・ワープ地点（下）のY座標 |
| `BOSS_WARP_RIGHT_POINT_X` | 500 | 巡回・ワープ地点（右）のX座標 |
| `BOSS_WARP_RIGHT_POINT_Y` | 220 | 巡回・ワープ地点（右）のY座標 |
| `BOSS_WARP_TOP_POINT_X` | 320 | 巡回・ワープ地点（上）のX座標 |
| `BOSS_WARP_TOP_POINT_Y` | 100 | 巡回・ワープ地点（上）のY座標 |
| `BOSS_MINI_SHOT_INTERVAL_FRAME` | 30 | ミニ弾の基本発射間隔 |
| `BOSS_MINI_SHOT_AMOUNT` | 12 | ミニ弾の同時発射数（円状弾幕） |
| `BOSS_MINI_BURST_INTERVAL_FRAME` | 4 | 連射ミニ弾の発射間隔 |
| `BOSS_NOMAL_SHOT_INTERVAL_FRAME` | 120 | 通常弾の発射間隔 |
| `BOSS_NOMAL_SHOT_AMOUNT` | 30 | 通常弾の同時発射数（30方向弾） |
| `CHARGE_EFFECT_INTERVAL` | 40 | チャージ演出のリピート間隔 |
| `CHARGE_END_FRAME_BOSS` | 240 | チャージフェーズの終了フレーム |
| `SHOT_STOP_INTERVAL` | 40 | ワープ前などの攻撃停止期間 |
| `SUMMON_LEFT_NOMAL_ENEMY_X` | 10 | 通常敵召喚位置（左） |
| `SUMMON_LEFT_TRACE_ENEMY_X` | 50 | 追従敵召喚位置（左） |
| `SUMMON_LEFT_CHARGE_ENEMY_X` | 30 | チャージ敵召喚位置（左） |
| `SUMMON_RIGHT_NOMAL_ENEMY_X` | 580 | 通常敵召喚位置（右） |
| `SUMMON_ENEMY_Y` | 0 | 雑魚敵召喚時の初期Y座標（画面外上部） |
| `BOSS_MAX_BOMB_COUNT` | 20 | 撃破演出時の最大爆発数 |
| `DEFEAT_EXPLOSION_INTERVAL_FRAME` | 15 | 撃破演出の爆発間隔 |
| `WARP_TRIGGER_FRAME_BOSS` | 334 | 第3フェーズでのワープ開始タイミング |
| `SUMMON_ENEMY_SET_FRAME` | 10 | 最終フェーズでの召喚フラグセットタイミング |
---
