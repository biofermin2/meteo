# meteo
meteo is a roswell script that picks weather forcast data up from Japan Meteorological Agency and shows it on your command line.

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
以下にダウンロードします。

```shell
$ ros install biofermin2/meteo
```

meteo.rosというファイルを自分の好きなパスに設定して上げます。

```shell
sudo ln -s ~/.roswell/local-projects/biofermin2/meteo/meteo.ros <your path>
```
that's that.

以上で、meteoスクリプトが使えるようになります。

## usage
シェルのコマンドライン上で下記の通り実行すると、

今日、明日、明後日までの天気予報がお天気マークと共に表示されます。

```shell
;; 調べたい市町村名を漢字で入力して下さい。（ひらがなやアルファベットでも可能ですが、同音の別の市町村を引っ張ってくる可能性があります。）
$ meteo <your municipality>[enter]
(☁ . "くもり　所により　雨　で　雷を伴う")(☁ . "くもり　所により　夕方　まで　雨　で　雷を伴う")(☁☼ . "くもり　時々　晴れ")
```

### update history
[2021-11-28] 0.1.1 ヘルプの追加

[2021-11-27] 0.1.0 全国の市町村に対応。（但し、同一市町村名など未対応）　

[2021-11-15] 0.0.1 能登バージョンのみ作成。meteoとして公開

[2021-08-05] 0.0.0 開発スタート（開発コード:weather)

### todo
- ~~全国エリアに対応出来るようにする~~ [2021-11-27]対応済
- ~~ヘルプを追加する~~ [2021-11-28]対応済
