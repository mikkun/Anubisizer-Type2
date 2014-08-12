Anubisizer-Type2 - 暇をもてあましたアヌビス神の遊び
===================================================

Anubisizer-Type2とは
--------------------

「＠IT自分戦略研究所」にてコラム[『101回死んだエンジニア』](http://el.jibun.atmarkit.co.jp/101sini/)を執筆されているAnubisさんの主催による、2014年7月26日に大阪で行われたハッカソン[「暇をもてあましたアヌビス神の遊び CLIのツールをガリガリ書く会 ----Part 2--」](https://atnd.org/events/53802)にて出された課題「CSVファイル加工用のフィルタコマンドを作成せよ」に対する成果となるべく、sedやAWKを用いて作成したシェルスクリプト群です(課題の詳細については[仕様書.txt](https://github.com/mikkun/Anubisizer-Type2/blob/master/docs/仕様書.txt)を参照してください)。

作成したシェルスクリプト
------------------------

**Anubisizer-Type2**において、メインとなるシェルスクリプトは下記の3つです。

* [convert\_header](https://github.com/mikkun/Anubisizer-Type2/blob/master/convert_header) - CSVのファイルを見出し付きの表形式(HTML)にコンバートする

        convert_header -f <CSVファイル> [-k] -t <タイトル1,タイトル2...>
            -f CSVファイルを指定
            -k 結合する前のフィールドも合わせて出力
            -t 2つ以上のタイトルを指定。指定した順番でフィールドを結合する

* [convert\_html](https://github.com/mikkun/Anubisizer-Type2/blob/master/convert_html) - CSVのファイルをHTMLの表形式にコンバートする

        convert_html -f <CSVファイル> [-k] -t <タイトル1,タイトル2...>
            -f CSVファイルを指定
            -k 結合する前のフィールドも合わせて出力
            -t 2つ以上のタイトルを指定。指定した順番でフィールドを結合する

* [convert\_list](https://github.com/mikkun/Anubisizer-Type2/blob/master/convert_list) - CSVのファイルをリストの形式(JSON)にコンバートする

        convert_list -f <CSVファイル> [-k] [-r|-s] -t <タイトル1,タイトル2...> [-y]
            -f CSVファイルを指定
            -k 結合する前のフィールドも合わせて出力
            -r 降順にソートして出力
            -s 昇順にソートして出力。-rと同時に使用した場合は-sが優先
            -t 2つ以上のタイトルを指定。指定した順番でフィールドを結合する
            -y YAML形式で出力(実験的機能)

以下のシェルスクリプト群は、上記のシェルスクリプトが内部から呼び出すことを目的として作成しましたが、単体でも使用することができます。

* [make\_csv\_tree](https://github.com/mikkun/Anubisizer-Type2/blob/master/make_csv_tree) - CSVファイルのデータをツリー構造にて出力する

        make_csv_tree -f <CSVファイル> [-y]
            -f CSVファイルを指定
            -y YAML形式で出力

* [merge\_csv\_fields](https://github.com/mikkun/Anubisizer-Type2/blob/master/merge_csv_fields) - CSVファイルのフィールドを指定した順番で結合する

        merge_csv_fields -f <CSVファイル> [-k|-o] [-r|-s] -t <タイトル1,タイトル2...>
            -f CSVファイルを指定
            -k 結合する前のフィールドも合わせて出力
            -o 結合したフィールドのみ出力。-kと同時に使用した場合は-oが優先
            -r 降順にソートして出力
            -s 昇順にソートして出力。-rと同時に使用した場合は-sが優先
            -t 2つ以上のタイトルを指定。指定した順番でフィールドを結合する

* [swap\_csv\_fields](https://github.com/mikkun/Anubisizer-Type2/blob/master/swap_csv_fields) - CSVファイルのフィールドを指定した順番に並び替える

        swap_csv_fields -f <CSVファイル> [-r|-s] -t <タイトル1,タイトル2...>
            -f CSVファイルを指定
            -r 降順にソートして出力
            -s 昇順にソートして出力。-rと同時に使用した場合は-sが優先
            -t タイトルを指定。指定した順番でフィールドを並び替える

コマンドとしての使用例
----------------------

以下の使用例について、実行結果のファイルは[examplesディレクトリ](https://github.com/mikkun/Anubisizer-Type2/tree/master/examples)にあります。

1. [Data.csv](https://github.com/mikkun/Anubisizer-Type2/blob/master/examples/Data.csv)を入力ファイルに指定した例:

        $ ./convert_header -f examples/Data.csv -t 'ホスト名,ルーター' -k > examples/Data-convert_header-k.html
        $ ./convert_html -f examples/Data.csv -t 'ホスト名,ルーター' > examples/Data-convert_html.html
        $ ./convert_list -f examples/Data.csv -t 'ホスト名,ルーター' > examples/Data-convert_list.json
        $ ./convert_list -f examples/Data.csv -t 'ホスト名,ルーター' -kr > examples/Data-convert_list-kr.json
        $ ./convert_list -f examples/Data.csv -t 'ホスト名,ルーター' -sy > examples/Data-convert_list-sy.yml
        $ ./make_csv_tree -f examples/Data.csv -y > examples/Data-make_csv_tree-y.yml

2. [売上.csv](https://github.com/mikkun/Anubisizer-Type2/blob/master/examples/売上.csv)を入力ファイルに指定した例:

        $ ./convert_header -f examples/売上.csv -t '統括エリア,分類' > examples/売上-convert_header.html
        $ ./convert_html -f examples/売上.csv -t '分類,単価,商品名' -k > examples/売上-convert_html-k.html

**注意: 入力ファイルではなく標準入力を各コマンドに読み込ませる場合は、-fオプションを使わないでください。**

関連情報について
----------------

ハッカソン「暇をもてあましたアヌビス神の遊び」に関する情報は、Twitterのハッシュタグ[#AnubisGG](https://twitter.com/hashtag/anubisgg)で知ることができます。

また、このハッカソンでの課題に対する成果としては、当リポジトリの他に

* kunst1080さんによる[AnubisGG](https://github.com/kunst1080/AnubisGG)のGitHubリポジトリ
* nmrmsysさんによる[AnubisGG02](https://github.com/nmrmsys/AnubisGG02)のGitHubリポジトリ

などがありますので、これらも併せてご覧ください。

ライセンスおよび著作権表示
--------------------------

いずれのシェルスクリプトについても、適用ライセンスは[GPLv3以降](https://www.gnu.org/licenses/gpl.html)です。シェルスクリプト以外のファイルに対しては、それぞれの適用ライセンスに準拠します。

------------------------------------------------------------------------------

Copyright (C) 2014 [KUSANAGI Mitsuhisa](https://github.com/mikkun)

    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program.  If not, see <http://www.gnu.org/licenses/>.
