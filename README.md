# テラフォーミング・マーズの棋譜の記法について

## はじめに
この方法で一度書いてみて、矛盾がなければいいよねの精神でやっていきたい。<br>
この文章の作者は非プログラマーなので、半角スペースとか`|`とかの置き方が正しい記法と違っていたら、こうしたほうがいいよとか言ってもらえると嬉しい。

## 記述の基本ルール、方針
- プログラミング記法やマークダウン記法にできるだけ合わせる。
    - 書きやすく、そのまま読んでも読みやすい、かつデータとして転用しやすいってのを重視したい。
- 効果が明示的であるものは略する。選択があることは記述。
    - この棋譜は物理ボードを広げて感想戦をすることを目的に作っている。実際に海洋タイルの隣接地に緑地タイルを置けば、2MCもらえるのは明らか。
- 左から読むことで、処理の順序が正しく追える。
- 特殊な処理は、個別に対応する。
    - 全部を記法に入れようとすると煩雑になりすぎるかも。
- 記法は英文法SVOC型とゲーム原文の記法を参考にする。
    - 主体者、アクション、相手、内容（数量、種類、座標）の順かな？

## 利点
- 1手番1行で記述するため、何手番行ったかが直感的に分かる。
- ほか。

## 棋譜の記述の仕方について
1手番につき1行で記述する。
```
CORPORATION : Action | Cost | Place | Interact | Benefit
```

例。書くとこんな感じ。
```
Gen 1
---
CREDICOR : Motion Rails | 3 Steel | City 21 | ECOLINE 3 plants | 1 microbe Tardigrades
CREDICOR : pass.
```
この順番で書けば処理順と同じになると思う。

### CORPORATION
企業の名前。誰の手番であるかを意味する。<br>
記述：企業は8文字に略する。6文字でもいいかと思ったけど、略しすぎると正しく読めない書けないが発生するかもしれないのと、8文字できれいに収まる企業が多いっぽいので。7文字以下の企業は半角スペースか`.`で調整したい。<br>
企業一覧と略称は多いので一番下を参照。

### Actions
ルールのアクションのこと。<br>
記述：内容は以下の通り。アクション名は略さない。大文字小文字も正確にしたほうがいいかも。
- Play a card
- Standard project
- Claim a milestone
- Fund an award
- Action on a blue card
- Convert plants
- Convert heat
- pass.

### Cost
そのアクションを使用するために支払うコスト。MCだけじゃなく、リソースでの支払いもできることに注意。<br>
`steel` `titanium` `heat` `microbe`<br>
記述：コストの支払いは通常MCであるため、MCの支払いは略する。`数量 リソースの種類` の順。<br>
特殊な支払いのみ表記。`3 Steel`なら3x2=6MCを支払いから減じるという意味。
- Spend MC
- Decrease
- Remove

### Place
設置するタイルのこと。<br>
`Ocean` `Greenery` `City` `Special`<br>
記述：種類 設置座標の順。座標はソロマーズの数え方を暫定で設定。でも緯度経度表記のほうがたぶんいい。<br>
海を2個多く場合などはどう記述する？`Ocean 4, Ocean 6`か、`Ocean 4,6`か。

### Interact
植物燃やしたり温熱産出量減らしたりするやつ。減ることを基本とする。<br>
`plants` `animals` `microbe`など<br>
記述：誰に 数量 リソースの種類　の順。

### Benefit
効果によって得られる利益。利益って表現でいいのか？<br>
gain,increace,raise,draw,addなどど書かれているもの。<br>
ただし、カード等に明示されていて選択制でないものは書かない。

## 特殊な表記
通常の表記では書ききれない、全てのゲーム中必ず起きるわけではない、などの理由があるもの。<br>
`Corporation Action` 企業カードによるアクション


## ヘッダー情報について
初期設定を入れる。マップ・時代・拡張・人数・各プレイヤーが選んだ企業、日付など。<br>
<br>
`map:Basic,Hellas,Elysium,`<br>
`era:sta,coop,`<br>
`expand:venus,prelude,colonies,turmoil`<br>
`players:1,2,3,4,5`<br>
`player1:ECOLINE,player2:TARSIS REPUBLIC`<br>
`date:2021-01-01 10:00-14:00`

## サンプル
```
Gen 0
---

Gen 1
---
CREDICOR : Motion Rails | 3 Steel | | |
CREDICOR : Virus | | 5 plants ECOLINE | |
ECOLINE  : Towing A Comet | 1 Titanium | Ocean 6 | |
ECOLINE  : pass.
CREDICOR : pass.
ECOLINE  : pass.

Gen 2
---
ECOLINE  : Tardigrades | | | |
ECOLINE  : Tardigrades | | | add 1 microbe |
VITOR    : Commercial District | | SP 34 |
```

- 基本
`THARSIS.` THARSIS REPUBLIC タルシス共和国
`MINING..` MINING GUILD 採掘ギルド
`INTERPLA` INTERPLANETARY CINEMATICS 惑星間シネマティクス
`PHOBOLOG` PHOBOLOG フォボログ
`STATURN.` SATURN SYSTEMS サターン・システムズ
`ECOLINE.` ECOLINE エコライン
`THORGATE` THORGATE トールゲート
`HELION..` HELION ヘリオン
`TERACTOR` TERACTOR テラクター
`UNITEDNA` UNITED NATIONS MARS INITIATIVE 国連火星動議
`INVENTRI` INVENTRIX インヴェントリクス
`CREDICOR` CREDICOR クレディコー
- 金星
`MORNING.` MORNING STAR INC. 明けの明星
`SELESTIC` SELESTIC セレスティック
`VIRON...` VIRON ヴァイロン
`MANUTECH` MANUTECH マニュテク
`APHRODIT` APHRODITE アフロディーテ
- プレリュード
`POINTLUN` POINT LUNA ポイントルナ
`CHEUNGSH` CHEUNG SHING MARS 城星マーズ
`VITOR...` VITOR ヴィトール
`ROBINSON` ROBINSON INDUSTRIES ロビンスン産業体
`VALLEYTR` VALLEY TRUST ヴァレー・トラスト
