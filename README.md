# meteo
meteo is a roswell script that picks weather forcast data up from Japan Meteorological Agency and shows it on your command line.

気象庁の天気予報データをコマンドラインに表示するツール

this script named from meteorological phenomenon.

このスクリプトは気象という英語から名付けました。

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

meteoという実行ファイルを自分の好きなパスに設定して上げます。

```shell
sudo ln -s ~/.roswell/local-projects/biofermin2/meteo/meteo <your path>
```
that's it.

以上で、meteoスクリプトが使えるようになります。

## usage
シェルのコマンドライン上でmeteoと実行すると、

今日、明日、明後日までの天気予報がお天気マークと共に表示されます。

```shell
$ meteo[enter]
(☁ . "くもり　所により　雨　で　雷を伴う")(☁ . "くもり　所により　夕方　まで　雨　で　雷を伴う")(☁☼ . "くもり　時々　晴れ")
```

### update history
[2021-11-15] 0.0.1 能登バージョンのみ作成。meteoとして公開
[2021-08-05] 0.0.0 開発スタート（開発コード:weather)

### todo
- 全国エリアに対応出来るようにする
- ヘルプを追加する
