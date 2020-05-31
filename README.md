# jinsei

履歴書ついでにいままでやってきたことを記載します。  
仕事以外の活動も記載していきたいので年月順に記載していきます。

## 目次

- [基本情報](#基本情報)
- [いままで](#いままで)
  - [2007/4~2010/3](#2007420103)
    - [高校生活](#高校生活)
    - [モバゲータウンにはまる。](#モバゲータウンにはまる。)
      - [掲示板の背景色をオレンジ変えるバグについて](#掲示板の背景色をオレンジ変えるバグについて)
      - [ガラケーのブラウザで遊ぶ](#ガラケーのブラウザで遊ぶ)

## 基本情報

|              |                                  |
| ------------ | -------------------------------- |
| 氏名         | 五十嵐翔 (Syo Igarashi))         |
| Twitter      | https://twitter.com/syo_igarashi |
| Qiita        | https://qiita.com/igara          |
| はてなブログ | https://igara1119.hatenablog.com |
| 個人サイト   | https://syonet.work              |

## いままで

### 2007/4~2010/3

#### 高校生活

本当は福島県立福島西高等学校を希望していたが滑り止めで「**福島成蹊高等学校**」という学校に入学した。  
中学生の頃から数学が得意で、入試試験の数学では満点取ったという栄光がある。他の教科は軒並みな点数だった気がする。  
学校名に「成蹊」と入っているが某学校法人とのつながりはない。由来は中国の漢詩からきているらしい。  
元々は女子校であったが、入学した年が男女共学になった年なので実は共学になっての第 1 期生だったりする。  
入学して 2 年生か 3 年生になった頃、中高一貫校として中学校も設立された。

「普通科」と有名大学に進学するための「特進科」というので学科が分かれており、特進科だと部活動に参加できないので普通科を選択した。  
部活は硬式テニスをやった。中学生の時、バレーボールをやっていたのでバレーボール部に入りたかったが、男子部員がいなかったため中学からの友人と一緒にテニスをやるようになったという経緯がある。  
数学得意なので理系である数学 Ⅲ, 数学 C, 物理と国語, 英語を中心に勉強をした。

あと余談で生徒に影響があった話でもないが在学中にあったこととして、私立校なので理事長（経営者）がおり、その理事長が別で経営しているタクシー会社のストライキがあったりで理事長が変わるというのがあった。

#### モバゲータウンにはまる。

ガラケーを持ち始めて自分の自由に閲覧できるインターネットを得る。  
当時 SNS が出始めな時だった。SNS の出会いで事件が出たのもこのぐらいの時期だった。

この動画にある内容だが文字として記載されているものがなかったのでこちらに記載する。  
動画  
https://youtu.be/pHGNT1lUloo?list=PLJt3Ieir9SpzpSkkfJkOQBq4qjz0xJ9YF&t=609

高校生の時に携帯電話でゲームができ、電子掲示板の書き込みもできるモバゲータウンに登録したらダダハマりしてしまった。  
どういったところにハマったというとモバゲータウン内のサークル（コミュニティ）である。
学生の集まりのようなサークルで馴れ合うのもよかったが、特にモバゲータウンをハックしようというサークルが一番ハマった。

その時のサークルとして下記のものになる。

トレジャーハンター缶詰め改  
http://yahoo-mbga.jp/group/3087661

ＷＥＢツール\[2nd\]  
http://yahoo-mbga.jp/group/30505794

たまたま掲示板の背景色をオレンジ 1 色に変えるバグを見てしまい、他にもいろいろ試してみようと集ったものが上記のサークルで興味を持ってしまったというのがあった。

##### 掲示板の背景色をオレンジ変えるバグについて

掲示板の投稿する時に掲示板のタイトルに特殊な文字を使用すると起こるバグだった。  
URI 上で使用できない文字列を用いる時、パーセントエンコードを行う。

例えば 🐣 が EZweb 絵文字コードで ％ef％34 という 16 進数を用いたコードポイントとしたらどこかしら絵文字が設定されていない欠番が存在する。  
あと当時は、EZweb、i モードで絵文字の統一化ができていない時代なので端末によっては文字化けが発生するというものもあった。  
当時のサービスでは文字コードが違くてもある程度同じ絵文字を出力しようとフレームワーク（MobaSiF）でやろうとしていたが、 ％ef％91 というコードが対策されていなかった。
結果としてパーセントのエスケープをやっていなかったので前後にある HTML の文字列も巻き込んでスタイルを崩せてしまったようなものだった気がする。

その時の HTML と CSS がどんな感じだったかも曖昧で。

```html
<div style="background: red;">${掲示板のタイトル}</div>
<div>
  ...
</div>
```

となっていたのが下記のようになり、div の閉じがなくなって掲示板の内容全体にスタイルが当たってしまうみたいな現象だった。

```html
<div style="background: red;">
  ?/div>
  <div>
    ...
  </div>
</div>
```

上記、認識違そうだったら連絡いただけると嬉しい。

##### ガラケーのブラウザで遊ぶ

上記のバグとの遭遇により、どうやってガラケーのサイトに XSS のようなを行うことができたのだろうかと興味を持ち始める。  
サークルの人に聞いて Openwave ブラウザ(Ezweb)でもソースを抽出する方法があることを知った。

- form のデータを抽出する。  
  投稿しましたというページでブックマークするとなぜか form で送信したデータが残ったままになる。  
  ブックマークの URL を別の Web ページにすることでリクエストしたデータを抽出ができる。  
  POST 抽出ツールと呼んでいた。
- HTML をテキスト出力する。  
  HTML を表示する URL を img タグで読み込んだ後、a タグで HTML の URL を開くとなぜかテキスト表示される。  
  PC 制限突破ツールと呼んでいた。

といった手法を用いて自分ツールを作ってみたのが下記のサイトになる。

高校生時代に作成したサイトのアーカイブ  
https://megalodon.jp/?url=http%3A%2F%2Fsameha.biz%2F%3Fakama

怪盗ロワイヤルで自動に挨拶するようなツールを作って部活の友達に教えたり、
リンク切れなものがあるがモバゲー風にカスタムした（スタイルのみ変更した）掲示板なども作った。
