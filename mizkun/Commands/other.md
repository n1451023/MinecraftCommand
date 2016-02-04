# other
## 目次
* ドアの挙動
* 高速クロック
* 入力を一度だけ検知

### ドアの挙動
#### 実装したもの
* 入力：高速クロックでの検知/コマンド本/コマンド看板により赤石設置
* 下のパルス回路から信号発進
* コマンドブロック1に
  * /fill XX1 YY1 ZZ1 XX2 YY2 ZZ2 minecraft:air // ドアオープン
* 遅延させてコマンドブロック2に
  * /fill XX1 YY1 ZZ1 XX2 YY2 ZZ2 minecraft:stone // ドアクローズ

### 高速クロック
* /setblock XX YY ZZ minecraft:stone 0 replace
* /setblock XX YY ZZ minecraft:redstone_block 0 replace
* これを一箇所にまとめると高速クロック化
  * もろもろの検知に
  
### 入力を一度だけ検知
* /setblock XX YY ZZ minecraft:redstone_block 0 replace // 入力
* /fill XX YY ZZ XX YY ZZ minecraft:air
* 赤石ブロックの隣に置くことで即座に消される=パルス化