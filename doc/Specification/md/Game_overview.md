# 概要
## ゲーム概要

プレイヤーを操作して敵を倒しながらステージを進み、
最後に出現するボスを撃破するとゲームクリアとなる
2D縦スクロールシューティングゲーム。

## 基本情報
| 項目 | 内容 |
|------|------|
| ゲームジャンル | 2Dシューティング |
| プレイ人数 | 1人 |
| 画面サイズ | 640×480px |
| 操作方法 | キーボード |
---
## 仕様書一覧

### 1. 概要
- ゲーム概要書(このファイル)

---

### 2. 図
- [シーン遷移図 : SceneTransition.drawio.png](/diaframs/SceneTransition.drawio.png)
- [タイトルシーンフロー : TitleScene_flow.drawio.png](/diaframs/TitleScene_flow.drawio.png)
- [ゲームシーンフロー : GameScene_flow.drawio.png](/diaframs/GameScene_flow.drawio.png)
- [リザルトシーンフロー : ResultScene_Flow.drawio.png](/diaframs/ResultScene_Flow.drawio.png)
- [プレイヤー状態遷移図 : PlayerState_Diagram.drawio.png](/diaframs/PlayerState_Diagram.drawio.png)
- [リザルト画面イメージ図 : ResultScreen.drawio.png](/diaframs/ResultScreen.drawio.png)

---

### 3. シーン
- [タイトルシーン : TitleScene_Specification](TitleScene_Specification.md)
- [ゲームシーン : GameScene_Specification.md](GameScene_Specification.md)
- [リザルトシーン : ResultScene_Specification](ResultScene_Specification.md)

---

### 4. オブジェクト

#### プレイヤー
- [プレイヤー : Player_Specification.md](Player_Specification.md)

#### 敵
- [通常敵 : NomalEnemy_Specification.md](NomalEnemy_Specification.md)
- [追従敵 : TraceEnemy_Specification.md](TraceEnemy_Specification.md)
- [チャージ敵 : ChargeEnemy_Specification.md](ChargeEnemy_Specification.md)
- ボス敵

#### アイテム
- アイテム

#### エフェクト
- エフェクト

#### 弾

#### プレイヤー弾
- 通常弾
- ミサイル弾
- スペシャル弾

#### 敵弾
- 通常敵弾
- ミニ敵弾

---

### 5. 管理クラス
- 敵管理
- アイテム管理
- エフェクト管理
- 弾管理
---

### 6. 使用データ
- 画像一覧
- BGM・SE一覧


---
## ゲームの流れ

本ゲームは、ゲーム開始からリザルトシーンまで一方向に進行するシーン構成となっています。基本的にプレイヤーが任意のシーンへ移動することはできず、ゲームの進行に合わせてシーンが遷移します。
- [シーン遷移図 : SceneTransition.drawio.png](/diaframs/SceneTransition.drawio.png)

#### タイトルシーン

ゲームを起動するとタイトルシーンから開始します。タイトル画像と操作説明画像を確認した後、ゲームシーンへ遷移しゲームを開始します。タイトル画像からゲーム開始への遷移は一方向のみで、タイトル画像、操作説明画像へ戻ることはできません。

- [タイトルシーン : TitleScene_Specification](TitleScene_Specification.md)

#### ゲームシーン

タイトルシーンからゲームを開始すると、ゲームシーンへ遷移します。ゲームシーンは本ゲームのメインとなるシーンであり、プレイヤーは自機を操作して敵を倒しながらゲームを進めます。プレイヤーは初期状態でゲームを開始します。ゲーム中にプレイヤーのHPが0になるとゲームオーバーとなり、リザルトシーンへ遷移します。

- [ゲームシーン : GameScene_Specification.md](GameScene_Specification.md)
- [プレイヤー : Player_Specification.md](Player_Specification.md)

ゲームは「通常ステージ」と「ボスステージ」の2段階で進行します。

ゲーム開始後は通常ステージから始まります。通常ステージでは雑魚敵が出現します。出現した雑魚敵が画面外へ退場または撃破されるとボス出現の演出が始まり、ボスステージへ遷移します。一度ボスステージへ移行すると、通常ステージへ戻ることはありません。

ボスステージではボス敵が出現し、ボスのHPを0にするとゲームクリアとなります。ボス撃破演出後、ゲームクリア画面を表示します。ゲームクリアでもリザルトシーンへ遷移します。

#### リザルトシーン

ゲームオーバー、またはゲームクリアになるとリザルトシーンへ遷移します。リザルトシーンでは、ゲーム中の経過時間と獲得スコアを表示します。

また、本ゲームで唯一シーンを選択できる場面であり、「タイトルシーンへ戻る」または「ゲームシーンを最初から開始する」のいずれかを選択できます。

- [リザルトシーン : ResultScene_Specification](ResultScene_Specification.md)

---
## ゲームルール

### クリア条件
  - ボスを倒す
    - ボス敵はボスステージで出現します。ボス敵HPがゼロになると撃破となります。
### ゲームオーバー条件 
- プレイヤーのライフが0になる
   - 敵の弾に被弾し、HPが0になった場合ゲームオーバーになります。 
   - 基本的に弾の種類関係なく3回の被弾でHPが0になります。
- [プレイヤー : Player_Specification.md](Player_Specification.md)

### スコア

プレイヤーは以下の場合スコアを獲得します。
- 敵に弾を当てる
- 敵を撃破
- アイテムの取得

獲得したスコアはゲーム中に加算され、
リザルトシーンで最終スコアとして表示されます。

### アイテム

敵を撃破するとアイテムをドロップします。
経験値と回復と無敵のアイテムがあります。

### プレイヤーの強化
- プレイヤーは敵を倒すと落とす経験値アイテムを使って弾の発射を強化していくことができます。
- 獲得した経験値(ショットパワー)によって、段階的に4パターンの発射の強化があります。
- [プレイヤー : Player_Specification.md](Player_Specification.md)

### 敵の出現
敵はゲームの進行に合わせて時間経過で出現します。ステージによって出現する敵が変わります
#### 通常ステージ
- 3種類雑魚敵が出現します。
- 出現するパターンが3つあり、ゲーム進行によってパターンも一方向を変化します。
#### ボスステージ
- ボス敵が出現します。
- 基本的にボス敵だけのステージで、ボス敵の召喚によって雑魚敵も出現します。
 
---
## システム操作(ゲームアプリの終了)

ESCAPEキーを押すと、どの条件下であってもゲームアプリケーションは強制終了します。

---
## 操作方法
- 移動：矢印キー
- 攻撃：SPACEキー(ショット)
- アクション：シフトキー（低速移動）
- [プレイヤー : Player_Specification.md](Player_Specification.md)
---
## デバックモード
デバッグ用機能を実装予定。
詳細仕様は別資料で確認できるようにします。

## 設計の意図と背景
### コンセプト
- 過去に制作したシューティングゲームを、一から作り直す。
- 作り直す際に追加する要素はなし
- 設計・実装・テストまで含めた成果物を制作する
### 構造の概要
- 各クラス間の依存を最小限にした疎結合な設計を目指す
- 他クラスへの依存を減らし、役割を明確にする
- 保守性と可読性の向上を目的とする
---
