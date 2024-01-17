# predicate-location_check
predicateのlocation_checkに関するデータパックサンプルになります。

詳しくはブログ記事『[【マイクラ】location_checkで場所の確認【predicate】](https://natsumake.com/location_check/)』を参考にしてください。

また、ブログ記事では解説していないjsonファイルも収録しています。

## 各項目と実装jsonファイルについての説明

前提として、基準となる座標はコマンドの実行場所となります。<br>
そのため、チャット欄で"if predicate"を指示したうえで実行した場合は、そのプレイヤーの足元の位置が参照されます。

### biome
```biome_check.json```が該当。<br>
コマンドの実行場所のバイオームをチェックしたうえで、判別。

<br>

実際に使用するコマンド例としてはこちら。

```{.copy}
/execute if predicate sample:biome_check run give @a diamond 1
```
（本データパックでは、平野にいる場合に成功するよう指示しています）

***

### block
```block_check.json```と```block_check_advanced.json```が該当。<br>
```block_check.json```は座標の調整を行っていないため、足（プレイヤーが持つ2マス分の高さの下のマス）と同じ座標にダイヤモンドブロックがある場合に成功します。

setblockコマンドなどで足と同じ高さにダイヤモンドブロックを設置してから試すこと。

<br>

実際に使用するコマンド例としてはこちら。

```{.copy}
/execute if predicate sample:block_check run give @a diamond 1
```

<br>

```block_check_advanced.json```は```block_check.json```との違いとして、offsetのyで-1を指定している。

offsetは参照する位置をずらす役割があるため、コマンドの実行場所から1マス下、つまりは足の1マス下である、足元のブロックを参照するようになる。

つまるところ、足元にダイヤモンドブロックがあれば成功する。<br>
（もちろんoffsetはxやzにも対応している）

<br>

実際に使用するコマンド例としてはこちら。

```{.copy}
/execute if predicate sample:block_check_advanced run give @a diamond 1
```

***

### dimension
```dimension_check.json```が該当。<br>
どのディメンジョンにいるのかで判別する。

<br>

実際に使用するコマンド例としてはこちら。

```{.copy}
/execute if predicate sample:dimension_check run give @a diamond 1
```
（本データパックでは、オーバーワールドにいる場合に成功するよう指示しています）

***

### fluid
```fluid_check.json```が該当。<br>
実行位置にマグマや水源、空気のどれがあるかを判別する。

<br>

実際に使用するコマンド例としてはこちら。

```{.copy}
/execute if predicate sample:fluid_check run give @a diamond 1
```
（本データパックでは、水がある場合に成功するよう指示しています）

***

### light
```light_check.json```が該当。<br>
明るさの値をもとに判別する。

基本的にはClient Lightの値を参照すればよいが、天候が悪い場合などには別途計算が必要になる。

<br>

実際に使用するコマンド例としてはこちら。

```{.copy}
/execute if predicate sample:light_check run give @a diamond 1
```
（本データパックでは、明るさレベルが0から10の間である場合に成功するよう指示しています）

***

### position
```position_check_perfect-match.json```と```position_check_range.json```が該当。<br>
指定した座標にいるかどうか。

#### 特定の値を指定する

特定の値だけを指示した場合は、その値とピッタリ合っていなければならない。<br>
XYZに10を指定した場合、XYZ全て0.0001もズレてはいけない。<br>
（正確にはマイクラが検知できないほどの微細なずれなら問題ないだろうが、まず「丁度に合わせなければならない」と思うこと）

<br>

実際に使用するコマンド例としてはこちら。

```{.copy}
/execute if predicate sample:position_check_perfect-match run give @a diamond 1
```
（本データパックでは、XYZ全て100を指示しています）

<br>

#### 値を範囲指定する

範囲指定をする場合は、minとmaxを指示する。<br>
10～100の範囲といった広範囲から僅かなズレも許容できるので、基本的には範囲を決めて使うことになるはず。

<br>

実際に使用するコマンド例としてはこちら。

```{.copy}
/execute if predicate sample:position_check_range run give @a diamond 1
```
（本データパックでは、XYZ全て10から100を指示しています）

***

### smokey
```smokey_check.json```が該当。<br>
指定した位置にあるブロックが焚き火や魂の焚き火などで煙に燻されているかどうか。

trueを選択していた場合は、燻されていることで成功。<br>
燻されていなければ、失敗となる。

falseが選択されている場合はその逆である。

<br>

実際に使用するコマンド例としてはこちら。<br>
（座標XYZ=10のブロックを対象に、燻されているかどうかを検知する）

```{.copy}
/execute positioned 10 10 10 if predicate sample:smokey_check run give @a diamond 1
```

***

### structure
```structure_check.json```が該当。<br>
指示した構造物（ストラクチャー）にいれば、if predicateが成功する。

ストラクチャーは高さを決められているので、上空すぎる場合などは範囲外となる。

<br>

実際に使用するコマンド例としてはこちら。

```{.copy}
/execute if predicate sample:structure_check run give @a diamond 1
```
