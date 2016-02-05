# Tasks
## やりたいことリスト
* スコアボード練習
* MP実装
* TP魔法化
* 魔法
* 雷の矢

### スコアボード練習
#### 方針
* スコアボード追加→ある入力でplayer.scoreboad=1→そのplayerをtp

#### 実装
##### コマンド/コマンドブロック
* スコアボード追加
  * /scoreboard objectives add istoMizHouse dummy
* istoMizHouse(スコアボード)を1にする
  * /scoreboard players set @p istoMizHouse 1
* istoMizHouse=1のプレイヤーを検知(正確には1以上) // コマンドブロックA
  * /scoreboard players test @p istoMizHouse 1
* istoMizHouseが1のプレイヤーをtpする
  * /tp @p[score_istoMizHouse_min=1] -296 76 63
* istoMizHouseが1のプレイヤーにメッセージ
  * /title @p[score_istoMizHouse_min=1] title {text:"DON'T MOVE!!",color:red}
* istoMizHouseを0にする
  * /scoreboard players set @p istoMizHouse 0


### MP実装
#### 方針
* スコアボード追加→0<=x<=200(暫定)の間1/tickで増え続ける
* 0<=x<=200のプレイヤーに追加の方がよい？<-こっちから実装

#### 実装
* スコアボード追加
  * /scoreboard objectives add MP dummy
* スコアボード表示
  * /scoreboard objectives setdisplay sidebar MP
* (スコアボードの表示を消すとき)
  * /scoreboard objectives setdisplay sidebar
* MPを0にする(初期化)
  * /scoreboard players set @p MP 0
* x : MP | 0<=x<=200 のプレイヤーに対し, MPを回復
  * /scoreboard players add @p[score_MP=200, score_MP_min=0] MP 1


### TP魔法化
#### 方針
* istoMizHouse追加→istoMizHouse=1のプレイヤーに対してMP比較
  * MP>=5 -> TP -> istoMizHouse=0
  * MP< 5 -> 足りないメッセージ -> istoMizHouse=0

#### 実装
* istoMizHouse追加
  * /scoreboard objectives add istoMizHouse dummy
* istoMizHouse=1にする // 入力
  * /scoreboard players set @p istoMizHouse 1
* MPの比較(MP>=5)
  * /scoreboard players test @p[score_istoMizHouse_min=1] MP 5
  * istoMizHouse=1のplayerに対して,MP>=5ならば信号
* MPの比較(MP<5)
  * /scoreboard players test @p[score_istoMizHouse_min=1] MP 0 4
  * istoMizHouse=1のplayerに対して,MP<5ならば信号(0<MP<4)
* MP>=5 -> MP減らす -> tp
  * /scoreboard players remove @p[score_istoMizHouse_min=1] MP 5
  * /tellraw @p[score_istoMizHouse_min=1] {text:"Welcome, Back!!", color:blue,bold:true}
  * /tp @p[score_istoMizHouse_min=1] -274.5 64 62
* MP<5 -> メッセージ
  * /tellraw @p[score_istoMizHouse_min=1] {text:"You Gain Warped!!", color:dark_purple,bold:true}
* istoMizHouse=0にする
  * /scoreboard players set @p[score_istoMizHouse_min=1] istoMizHouse 0


### 魔法
#### 方針
* スコアボードにMPを追加
* MPを消費して各種コマンド実行が可能になる
* MPは時間で増えていく
* 魔法を使う時の処理
  * RDS設置→MPが必要数以下ならば足りない  
      →必要数以上ならばコマンド実行→MP消費
* 本はできればTier:1みたいに、少しずつレベルアップしたいよね

#### 使えそうなコマンド
* /scoreboard players test <プレイヤー名> <スコア名> <最小値> [最大値]
  * 最大値以下なら信号発火

#### 実装する魔法
* tp to mizhouse
* 家の鍵あける
* ゴーレム
* 火の玉
* 雷の矢

### 矢がささると雷が落ちる
#### 方針
* 矢={display:{name="thunder"}}的なラベル貼り
* 矢を飛ばす→着地点に着雷
  * 着地点付近に火がつく問題
    * summon ~ ~+1 ~で対応できる？/火を付けないような雷ってNBTでできるのか
  * 着地点以外の方法は？
    * フラグA：矢が飛んでいる間1
    * フラグB : フラグA=1->ダメージを食らったmobに対して1
    * フラグBのmobにsummon lightning
* 矢を飛ばす方法
  * directionをどうやったら自然にできるか
    * ユーザの目線取得する？重そう...
* 矢について
  * パーティクルを出すのはできそう
  * どうせなら、透明な矢+パーティクルにしたい

#### 使えそうなコマンド
* /summon Fireball ~ ~1 ~ {Motion:[0.0,0.0,0.0],direction:[0.0,0.0,0.0],ExplosionPower:5}
* /scoreboard players set @a isApple 1 {Item:{id:minecraft:apple,tag:{display:{Name:"毒リンゴ"}}}} // 特定のアイテムにscore
* /execute @e[score_isApple_min=1] ~ ~ ~ summon LightningBolt // 処理


