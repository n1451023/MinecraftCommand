# Tasks
## やりたいことリスト
* スコアボード練習
* MP実装
* TP魔法化
* Fire_ball
* 魔法
* 雷の矢
* 雷を召喚するアイテム
* 旅人の杖

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

### Fire_Ball
#### 方針
* isFireBall追加→isFireBall=1のプレイヤーに対してMP比較
  * MP>=30 -> TP -> isFireBall=0
  * MP< 30 -> 足りないメッセージ -> isFireBall=0

#### 実装
* isFireBall追加
  * /scoreboard objectives add isFireBall dummy
* isFireBall=1にする //入力
  * /scoreboard players set @p isFireBall 1
* MPの比較(MP>=5)
  * /scoreboard players test @p[score_isFireBall_min=1] MP 30
  * isFireBall=1のplayerに対して,MP>=5ならば信号
* MPの比較(MP<5)
  * /scoreboard players test @p[score_isFireBall_min=1] MP 0 29
  * isFireBall=1のplayerに対して,MP<5ならば信号(0<MP<4)
* MP>=30 -> MP減らす -> tp
  * /scoreboard players remove @p[score_isFireBall_min=1] MP 30
  * /tellraw @p[score_isFireBall_min=1] {text:"Welcome, Back!!", color:blue,bold:true}
  * /execute @p[score_isFireBall_min=1] ~ ~ ~ summon Fireball ~ ~ ~ {Motion:[0.0,0.0,0.0],direction:[0.0,0.0,0.0],ExplosionPower:0}
* MP<30 -> メッセージ
  * /tellraw @p[score_isFireBall_min=1] {text:"You Gain Warped!!", color:dark_purple,bold:true}
* isFireBall=0にする
  * /scoreboard players set @p[score_isFireBall_min=1] isFireBall 0


  

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

### 投げると雷が落ちる
#### 方針
* 1


*/give mizkun minecraft:snowball 1 0 {display:{Name:"poi"}}
* 



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
* /execute @e[score_isApple_min=1] ~ ~ ~ summon ~ ~ ~ LightningBolt // 処理

### 雷を召喚するアイテム
#### 方針
* アイテム(ネザースター、名前を特殊なものに)
* アイテムが地面に落ちたら雷発火

#### 実装
* アイテム
  * /give @p minecraft:nether_star 1 0 {display:{Name:"LightningStar", ench:[]}}
* 検知
 * /scoreboard players set @a isApple 1 {Item:{id:minecraft:nether_star,tag:{display:{Name:"毒リンゴ"}}}} // 特定のアイテムにscore
 * /testfor @e[Item:{display:{Name:"LightningStar", ench:[]}},Onground:true]
 * /testfor @e[type=Item] {OnGround:true,Item:{id:minecraft:nether_star,tag:{display:{Name:"LightningStar"}}}}
* /execute @e[type=Item] {OnGround:true,Item:{id:minecraft:nether_star,tag:{display:{Name:"LightningStar"}}}} ~ ~ ~ summon ~ ~ ~ LightningBolt


### 旅人の杖
#### 方針
* 26方向を検知してショートワープ
  * それぞれについて方向を検知→正しい方向にショートワープ
  
#### Ver1
##### 東西南北で検知
* 北 rym=134,ry=-135
  * tp ~ ~ ~3
* 東 rym=-134,ry=-45
  * tp ~3 ~ ~
* 南 rym=-44,ry=45
  * tp ~ ~ ~-3
* 西 rym=44,ry=135
  * tp ~-3 ~ ~

### 本のコピー
#### 方針
* Book&Quilを持ってLV40ならばコピー
* コピーしたい本をチェストにいれる
* コピーされる本(Book&Quil)を指定の場所にセット
* お互いが検知されればコピー開始
* 下の宝箱にコピーされた本が！

#### 実装
* 本がはいったチェストの検知
  * testforblock x y z minecraft:chest -1
{Items:[{id:minecraft:enchanted_book",Count:1b}]}
* Book&Quilを置く場所(ArmorStand)
 * /summon ArmorStand ~0.1 ~0.2 ~ {Invisible:1b,NoBasePlate:1b,NoGravity:1b,ShowArms:1b,Rotation:[90f],Equipment:[{id:"enchanted_book",Count:1b},{},{},{},{}],Pose:{Body:[90f,0f,90f],LeftLeg:[173f,0f,0f],RightLeg:[43f,152f,27f],LeftArm:[20f,0f,0f],RightArm:[0f,270f,247f]}}
* Book&Quilを置く場所(ArmorStand)の検知
 * /testfor @e[type=ArmorStand,r=5] {Equipment:[{id:"minecraft:writable_book"}]}
* 経験値の検知
 * /testfor @p[r=5,lm=40]
* 経験値を減らす
 * /xp -40L @p[r=5,lm=40]
* コピーの実行
 * /clone A(x,y,z) A(x,y,z) B(x,y,z)



#### おまけ
* 空中に本が浮いてる！！
  * /summon ArmorStand ~0.1 ~0.2 ~ {Invisible:1b,NoBasePlate:1b,NoGravity:1b,ShowArms:1b,Rotation:[90f],Equipment:[{id:"writable_book",Count:1b},{},{},{},{}],Pose:{Body:[90f,0f,90f],LeftLeg:[173f,0f,0f],RightLeg:[43f,152f,27f],LeftArm:[20f,0f,0f],RightArm:[0f,270f,247f]}}
* 本がコピーされる時のパーティクル
 * /particle enchantmenttable -284 66 50 0.2 0.1 0.2 0.1 2
* エンティティ化したエンチャ本の検知
 * @e[type=Item] {Item:{id:minecraft:enchanted_book}}で検知できる？
 * testforで検知成功
* selectorを使って同じものを装備させられるか
   * /summon ArmorStand ~0.1 ~0.2 ~ {Invisible:1b,NoBasePlate:1b,NoGravity:1b,ShowArms:1b,Rotation:[90f],Equipment:[{id:{"selector":"e[type=Item]"},Count:1b},{},{},{},{}],Pose:{Body:[90f,0f,90f],LeftLeg:[173f,0f,0f],RightLeg:[43f,152f,27f],LeftArm:[20f,0f,0f],RightArm:[0f,270f,247f]}}
* チェスト内に本があることを検知→コピー→ホッパーで取り出してドロッパーでエンティティ化→tpして台座に。適宜killして自然に
