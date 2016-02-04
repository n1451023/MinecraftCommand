# Tasks
## やりたいことリスト
* 魔法
* 雷の矢

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


