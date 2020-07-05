# reedbushスクリプト
## env.sh
環境変数の設定とかを行う。Pythonなら

```
. venv/bin/activate
```

などをよく入れたりする。

module load系のコマンドも書いたりする。

## interactive.sh

```
qsub interactive.sh
```

でインタラクティブモードで実行する。たいていインタラクティブモード開始後

```
cd $PBS_O_WORKDIR
```

で前の作業ディレクトリまで移動し

```
. env.sh
```

をして環境変数を読み込んだりする。

このあと、気になるプログラムの挙動を確かめたりする。

## run.sh

```
qsub run.sh
```

でジョブを実行する

#### #PBS -q h-short
h-short, h-large, l-short, l-largeなどがある。GPUの枚数や最大の実行時間制限とかが違う。性能自体はほとんど同じだと思う。詳しくはreedbushの仕様書をみて。

#### #PBS -l select=1:ncpus=1:mpiprocs=1:ompthreads=1
占拠するノード数、CPU数、プロセッサ数を指定する。ompthreadsはOpenMPで使われる環境変数っぽい。

#### #PBS -l walltime=02:00:00
実行時間を指定する。これを超えると打ち切られる。

#### #PBS -N run
ジョブの名前を指定する。rbstatするときに表示される名前
