# commands
## 目次
* かなとこの音
* 看板コマンド
* 花火
* 壊れない剣, 空エンチャ
* パーティクル
* コマンド本
* 鍵シリーズ

### かなとこの音
* /playsound random.anvil_land @p ~ ~ ~ 60 1.0
* \ｶｯｰﾝ/

### 看板コマンド
* [Sign Generater](https://minecraftcommand.science/command-sign-generator)

### 花火
* [fireworks generator](http://www.minecraftupdates.com/fireworks)

### 壊れない剣, 空エンチャ
* /give mizkun 276 1 0 {Unbreakable:true}
* 1.7のもの
* /give @p stick 1 0 {ench:[]}

### パーティクル
* パーティクル
* /execute @p[name=mizkun] ~ ~ ~  particle iconcrack_264 ~ ~1 ~ 1 1 1 0.01 1000
* /particle snowshovel ~ ~ ~ 0.2 0.4 0.2 0.8 100
* 魔法系のエフェクトはこれかな？
　　* /execute @p[score_isXX_min=1] ~ ~ ~  particle snowshovel ~ ~ ~ 0.2 0.4 0.2 0.8 100
* /particle iconcrack_264 ~ ~3 ~ 1 3 1 0.01 1000
* [参考](http://www61.atwiki.jp/mccmd/pages/58.html)

### コマンド本
* /give @p written_book 1 0 {author:"mizkun",title:"ver0.8.0998",pages:["{text:'',color:dark_gray,extra:[{text:'open a door             ',color:black,bold:false,clickEvent:{action:run_command,value:'/setblock -286 63 56 minecraft:redstone_block 0 replace'}},{text:'to MizkunHouse          ',color:black,bold:false,clickEvent:{action:run_command,value:'/tp -274.5 64 62'}},{text:'fire                        ',color:red,bold:false,clickEvent:{action:run_command,value:'/particle flame ~ ~0 ~ 1 1 1 0.05 100 @p'}},{text:'fordebbug                ',color:blue,bold:true,clickEvent:{action:run_command,value:'/give @p minecraft:stone_button'}}]}"]}
* ↑最新版
* そのうち追加します
* 実装してほしい魔法があれば連絡ください



### 鍵シリーズ
#### 鍵0_チェスト形式
* /testforblock XX YY ZZ chest -1 {Items:[{id:4451,Damage:0s,tag:{display:{Name:"HouseKey",},}}]}
* /give @p 4451 1 0 {display:{Name:HouseKey},ench:[]}
* **Ver1.7時代に作ったものなので動かないかも**
* チェスト内に指定のアイテムがあれば信号
  * ex) 指定敵のドロップアイテムをチェストにいれる

#### 鍵1_手に持っているアイテム
* /testfor @p[x, y, z,1] {SelectedItem:{id:"minecraft:CobbleStone",}}
* 指定のアイテムを現在指定していたら信号
  * ex) 鍵持ってボタン押すとドアが開く
  
#### 鍵2_看板チェック
* 看板コマンド参照
  * ドアの入力に赤石ブロック設置
  * ex) ボタンではなく看板が正解！
  
#### 鍵3_コマンド本
* コマンド本参照
  * ドアの入力に赤石ブロック設置
  * 呪文リストに解錠を入れよう。条件指定をしっかりすれば応用が効くかも
    * (装置)ドアの入力に鶏を置く→(本)付近の鶏の場所に赤石ブロック設置→(装置)ドア解錠とすれば各地のドアを開けられる本になるかも。ニワトリの声が聞こえたら本を使おう！みたいなアドベンチャー面白そう
 