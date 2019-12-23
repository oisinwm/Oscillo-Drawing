# オシロお絵描き
## 概要
これは、オシロスコープに256\*256の点描画を表示するシステムです。
![Sample image](https://pbs.twimg.com/media/DuN4ZdfVsAAuScb?format=jpg&name=small)
<blockquote class="twitter-tweet"><p lang="ja" dir="ltr"><a href="https://twitter.com/hashtag/%E4%BB%8A%E6%97%A5%E3%81%AE%E7%89%A9%E7%90%86%E9%83%A8?src=hash&amp;ref_src=twsrc%5Etfw">#今日の物理部</a><br>今日のと言っても昨日のですが<br>もうそろそろ高2生(78期)引退ということで、そろそろオシロお絵かき計画も集大成といったところです。<br>手始めにまずこれを。<br><br>アニメ「少女終末旅行」OPの「動く、動く」MVをオシロスコープで表示してみました。 <a href="https://t.co/SufvPvsq2e">pic.twitter.com/SufvPvsq2e</a></p>&mdash; 【公式】六甲学院物理部 (@RokkoPhysics) <a href="https://twitter.com/RokkoPhysics/status/1188304401108094978?ref_src=twsrc%5Etfw">October 27, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
## 動作環境
### ハードウェア
RaspberryPi3B,3B+(4Bは未確認、多分動く)
OSはRaspbian、他にWiringPiが入っている必要あり。
### オシロスコープ
帯域5MHz以上、2chでX-Yモードがあるタイプ
(アナログ推奨、デジタルでも動くはず)
## まず最初に
### D/Aコンバーターを作ろう
このオシロお絵描きには、２基の8bitD/Aコンバーターが必要です。ラダー抵抗型をお勧めします。
### D/Aコンバーターをラズパイと繋ごう
このプログラムはWiringPiを使っています。ピン配置は以下の通り。
![ラズパイのピン配置](http://homunet.sakura.ne.jp/wp/wp-content/uploads/2016/02/e04b2f5a506284f6b1cbb3b41b93d4d9.png)
これを、以下の通りにD/Aコンバーターと繋ぎます。

| X軸 |     | Y軸 |     |
| --- | --- | --- | --- |
| BCM | D/A | BCM | D/A |
| 17  | 0   | 2   | 0   |
| 18  | 1   | 3   | 1   |
| 27  | 2   | 8   | 2   |
| 22  | 3   | 7   | 3   |
| 23  | 4   | 10  | 4   |
| 24  | 5   | 9   | 5   |
| 25  | 6   | 11  | 14  |
| 4   | 7   | 14  | 7   |

### オシロスコープの設定
1.オシロスコープをX-Yモードにする。  
2.グランドレベルの光点の位置をオシロスコープの左下端に移す。  
3.両チャンネルに5V入力時の光点を右上端にあわせる。  
## オシロお絵描きの動かし方
### 特殊オシロお絵描き(oscillooekaki,oscillodoga)
#### oscillooekaki
オシロスコープに静止画を表示します。実行時の"ファイル名"にdataの中に入れたosdファイルを指定します。
#### oscillodoga
オシロスコープに動画を表示します。実行時の"ファイル名"にdataの中に入れたosdファイルを指定します。"framerate"にフレームレートを入力しす。
フレームレートは浮動小数点型に対応しています。
### 表示データの生成
以下のリンクからデータを生成できます。
https://itoho.wjg.jp/osirooekaki
### 汎用オシロお絵描き
oscillo_template.cを元に任意の図形をオシロスコープに表示するプログラムを作る事ができます。
oscillo_function.hでサポートされている関数を使う事ができます。コンパイル時にはwiringPiとマスライブラリーを指定する必要があります。
oscillo_tetrisは使用例です。
