# meteo
meteo is a roswell script that picks weather forcast data up 

from Japan Meteorological Agency and shows it on your command line.

気象庁の天気予報データをコマンドラインに表示するツール

this script named from meteorological phenomenon.

このスクリプトは気象という英語から名付けました。

as you know there are some tweets on this(2021) Feb,
we became able to pickup json data from JMA web site.

今年（２０２１年）２月にtweetがあったように、
気象庁のサイトからJSONデータを持ってくる事が出来るようになりました。

## setup
this guidance made for linux users.

※この説明は主にlinux user向けです。

this library can install by roswell from github repository as the follow line.

roswellを使って、githubのこのリポジトリからダイレクトに

~/.roswell/local-projects/

以下にダウンロードし、以下の通り操作します。

```shell
$ ros install biofermin2/meteo
$ cd ~/.roswell/local-projects/biofermin2/meteo
$ ros build meteo.ros
$ mv meteo ~/.roswell/bin/
```

that's that.

以上で、meteoコマンドが使えるようになります。

## usage
if you execute meteo command as the follow line,
you can check the weather forcast these 3 days with symbol.

シェルのコマンドライン上で下記の通り実行すると、
今日、明日、明後日までの天気予報がお天気マークと共に表示されます。

```shell
;; you can designate your municipality even if it is alphabet. but sometimes it cause some errors.so please see the solutions below.
;; 調べたい市町村名を漢字で入力して下さい。（ひらがなやアルファベットでも可能ですが、同音の別の市町村を引っ張ってくる可能性があります。）
$ meteo <your municipality>[enter]
((☁ . "くもり　所により　雨　で　雷を伴う")(☁ . "くもり　所により　夕方　まで　雨　で　雷を伴う")(☁☼ . "くもり　時々　晴れ")) ;weather info
;; ((today)(tomorrow)(day after tomorrow))
```
the usage of the options is as follows.

オプションの使い方は下記の通りです。

### help

ヘルプの表示

```shell
$ meteo -h
```

### version info

バージョン情報の表示

```shell
$ meteo -v
```
### weather maps

各種天気図の取得

```shell
$ meteo -m number ;(number:1〜4)
```

     1: asia-pacific region monochrome

     2: asia-pacific region color

     3: around Japan monochrome

     4: around Japan color

it starts download above weather map png file.

then you can check it by your favorite viewer.

     1:アジア太平洋域（白黒）
     
     2:アジア太平洋域（カラー）
     
     3:日本周辺（白黒）
     
     4:日本周辺（カラー）

上記の天気図をダウンロードします。

例えばこういう感じにshell scriptと組み合わせてみます。

```shell
$ for i in {1..4};do; meteo -t $i;done
$ ls *.png
around-Japan-color-2021-12-07.png  around-Japan-mono-2021-12-07.png  asia-pacific-color-2021-12-07.png  asia-pacific-mono-2021-12-07.png 
```

png形式の画像なのでお好みの描画ソフトでご覧下さい。
（xdg-openの行のコメントを外せば、デフォルトのviewerで
自動的に見る事が出来ます。外部アプリケーション依存のため
ソース内ではコメントアウトしてあります。）

The sub-options are also used as follows.

また、サブオプションは下記のように使います。

### detail info

詳細情報の表示

```shell
$ meteo <municipality> -d
```

### area info

エリア情報の表示

```
$ meteo <municipality> -a
```

例えば、能登の輪島市の場合、通常”輪島市"で検索かければ表示出来ますが、

わざと”わじまし”で詳細情報を見たとしましょう。

```shell
$ meteo わじまし -d
((☼ . 晴れ) (☼→☁ . 晴れ 昼過ぎ から 時々 くもり) (☁☔ . くもり 時々 雨))            ; weather info
((WAVES (1メートル 1メートル |1メートル 後 2メートル|) WINDS                         ;detail info
  (|西の風 後 東の風| |南東の風 後 東の風| |東の風 後 北西の風 やや強く|) WEATHERS
  (晴れ |晴れ 昼過ぎ から 時々 くもり| |くもり 時々 雨|) WEATHERCODES (100 110 203) AREA
  (CODE 380030 NAME 南予))
 (POPS (0 0 0 0 0) AREA (CODE 380030 NAME 南予)))
 ```
 
 一番最後の行でAREAのところが南予となっているのが、わかると思います。
 
 能登の輪島市を検索したい場合、エリア情報でもう一度検索します。
 
 ```shell
 $ meteo わじまし -a
((☼ . 晴れ) (☼→☁ . 晴れ 昼過ぎ から 時々 くもり) (☁☔ . くもり 時々 雨)) ; weather info
((PARENT 380032 KANA うわじまし ENNAME UWAJIMA CITY NAME 宇和島市)     ;area info
 (PARENT 170021 KANA わじまし ENNAME WAJIMA CITY NAME 輪島市))
 ```
 
このようにひらがなで検索すると、”わじまし”ではなく上側に位置する”うわじまし”の方の

天気を調べにいってる事がわかるかと思います。また漢字であっても同一市町村名やその

市町村を含む市町村名の場合、同様に調べたい地域と別の地域を調べてしまう可能性もあります。

そこで、このような場合、エリア情報のPARENTに表示される番号を入力します。

この場合、能登の輪島市は170021です。

```shell
$ meteo 170021
((☼ . 晴れ) (☼☁ . 晴れ 時々 くもり) (☼→☔ . 晴れ 後 一時 雨))
```

またひらがなではく、エリア情報にあるアルファベットでの検索も

出来ますが、ひらがなと同様に同一の発音、あるいはその発音を含む都市を

間違えて検索する場合があるので、お気をつけ下さい。

```shell 
$ meteo wajima -a
((☼ . 晴れ) (☼→☁ . 晴れ 昼過ぎ から 時々 くもり) (☁☔ . くもり 時々 雨))
((PARENT 380032 KANA うわじまし ENNAME UWAJIMA CITY NAME 宇和島市)
 (PARENT 170021 KANA わじまし ENNAME WAJIMA CITY NAME 輪島市)
 (PARENT 110011 KANA かわじままち ENNAME KAWAJIMA TOWN NAME 川島町))
```

またこの様なトラブルを防ぐために英語表記の際、頭文字を大文字で書いたり、

CityかTownまで明記する事によって防げます。ただCityやTownを付ける場合、

サブオプションは使えませんのでご注意下さい。

```shell
$ meteo Wajima -a 
((☼ . 晴れ) (☼☁ . 晴れ 時々 くもり) (☼→☔ . 晴れ 後 一時 雨))
((PARENT 170021 KANA わじまし ENNAME WAJIMA CITY NAME 輪島市))

$ meteo Wajima City -a 
((☼ . 晴れ) (☼☁ . 晴れ 時々 くもり) (☼→☔ . 晴れ 後 一時 雨))
```

上記をまとめると、より確実な順は

```
PARENTナンバー＞漢字＞頭文字が大文字のアルファベット＞ひらがな・頭文字も小文字のアルファベット
```

となります。（但し、衛星画像、ナウキャスト画像は漢字のみに対応）

エリア情報を元に検索をかけるので、エリア情報内にない表記（カタカナなど）で検索をかけても

エラーとなります。

### satellite image

衛星画像の取得

```shell
$ meteo <municipality> -s n
```

n means number. you should select a number from the below.

     1:inframed image
    
     2:visible image
     
     3:water-vapor image
     
     4:truecolor image
     
     5:cloud-top image

nは数字を表します。以下の中から希望の数値を選択して下さい。

    1:赤外線画像
    
    2:可視画像
    
    3:水蒸気画像
    
    4:truecolor再現画像
    
    5:雲頂強調画像
  
但し、この機能についてはアメダスのデータを元に緯度経度情報を取得し、

計算しているため、アメダスが設置されていない地域は衛星図が見れません。

その場合、より大きな地域の名前をご指定下さい。

### nowcast image
ナウキャスト画像の表示
※ナウキャスト画像については国土地理院の地理院タイル画像を利用しております。

```shell
$ meteo <municipality> -n z [map-type]
;; z is zoom level number 2〜8
;; map-type is optional argument
```
zoomレベルによっては、エラーが出る場合もあります。6あたりがオススメです。

map-typeに指定出来るのは以下の候補

;; 地図の種類　map-type zoom-level

;; 標準地図 std 5-18

;; 淡色地図 pale 5-18

;; English english 5-11

;; 数値地図25000（土地条件） lcm25k_2012 10-16

;; 土地条件図（初期整備版） lcm25k 14-16

;; 沿岸海域土地条件図 ccm1 （平成元年以降） ccm2 （昭和63年以前） 14-16

;; 白地図 blank 5-14

;; x 写真 seamlessphoto 2-18

;; 世界衛星モザイク画像 modis 2-8

;; x 全国ランドサットモザイク画像 lndst 2-15

;; 色別標高図 relief 5-15

;; アナグリフ anaglyphmap_color anaglyphmap_gray 2-16

;; 陰影起伏図 hillshademap 2-16

;; 傾斜量図 slopemap 3-15

;; 全国傾斜量区分図（雪崩関連） slopezone1map 3-15

xは試してダメだったもの。

詳細は以下の国土地理院タイル一覧ページ参照。

https://maps.gsi.go.jp/development/ichiran.html


その他捕捉記事はqiitaにもまとめたので、もしよろしければご参照下さい。

[Common Lispで天気予報スクリプトを作ってみた〜気象庁編〜](https://qiita.com/biofermin2/items/22634286290e779c36d5)

### update history
[2022-07-02] 0.3.0 unioのver.3対応修正。

[2022-06-11] 0.2.6 area-infoに県名を追加。unioの新オプション利用による改変。

[2022-05-25] 0.2.5 unioのアップデートに対応。

[2021-01-05] 0.2.4 ナウキャスト画像のベースマップ切り替えオプションの追加。

[2022-01-02] 0.2.3 天気図まわりのリファクタリング。

[2021-12-31] 0.2.2 ナウキャスト画像表示機能追加。

[2021-12-31] 0.2.1 URLまわりの修正。

[2021-12-30] 0.2.0 ひまわり衛星画像を表示出来るように機能追加。

[2021-12-26] 0.1.9 対象外のエリアへのエラーメッセージ追加。base-urlを２つのグローバル変数からそれぞれ同じ名前のローカル変数に変更。

[2021-12-20] 0.1.8 ハッシュテーブルを導入、select-infoをselect-valueに改める。

[2021-12-19] 0.1.7 select-infoの追加。area-infoの選択をわかりやすくする。

[2021-12-12] 0.1.6 お天気マークデータを気象庁のjsonデータから全部追加。

[2021-12-12] 0.1.5 応急処置版のupper-codesに書き換え。同名地域を選択可能に変更。

[2021-12-11] 0.1.4 天気図の自動表示のソースコードをコメントアウトして追加。

[2021-12-08] 0.1.3 鹿児島県内エラー問題対応。

[2021-12-07] 0.1.2 天気図のダウンロードオプションの追加。

[2021-11-28] 0.1.1 ヘルプの追加。サブオプションの追加。

[2021-11-27] 0.1.0 全国の市町村に対応。（但し、同一市町村名など未対応）←[2021-11-28]対応方法追加

[2021-11-15] 0.0.1 能登バージョンのみ作成。meteoとして公開

[2021-08-05] 0.0.0 開発スタート（開発コード:weather)

