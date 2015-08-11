# [WIP] octpng-spec
specifications for delta_z = 8 png tile as meta tile for tile existence

タイルデータの所在を示すタイルデータとして、minZoom - 8 のズームレベルに PNG 画像タイルを作成し、
その各画素が minZoom のタイルデータの所在を示すようにする。その PNG 画像タイルを octpng タイル
と呼ぶことにする。

# 実装

参照実装は、mapreduce でスケールすることを見込みつつ、map.rb と reduce.rb を UNIX sort で
つなぐ構成を考える。コマンドラインは次のような形になるだろう。

```
$ ruby map.rb somewhere/mokuroku.csv.gz 15 | sort | ruby reduce.rb
```

map の第二引数は、元のデータの minZoom とする。元のデータの minZoom のタイルをスキャンして
minZoom - 8 （ここでは z=7）のデータを作成する。

# 課題
<strike>octpng タイルは、画像タイルのオーバーズーミングを活用して表示することになるが、
1画素が128pxに拡大されるような delta_z= 7 のオーバーズーミングをした時に、
ブラウザによって画像拡大のアルゴリズムが異なることが影響してくるかもしれない。</strike>

→ CSS の image-rendering プロパティをサポートしているブラウザであれば問題ないことが分かった。

# ChangeLog
- 2015-07-23 開始
- 2015-08-10 http://hfu.github.io/octpng-bin/ でコンセプト実証

# See also
- http://github.com/hfu/octpng-bin
