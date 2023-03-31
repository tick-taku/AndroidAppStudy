# ペパカレ Android

ペパカレ Android 学習カリキュラムのテキスト用リポジトリです。

## URL

https://pages.git.pepabo.com/pepabo/pepabo-college-android/

## ローカルで確認する場合

MkDocs を使っています。

### Python のインストール

Python 製のツールなので Python をインストールしてないかたはここから。3.10 でしか動作確認していません。

```
$ brew install python3

# たぶん brew で入れたら入ってると思いますがない場合は pip を別途インストールします
$ curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
$ python3 get-pip.py

$ pip -v
pip 22.2.2 from /opt/homebrew/lib/python3.10/site-packages/pip (python 3.10)
```

### MkDocs のインストール

MkDocs の拡張の mkdocs-material を使っているのでインストールしてください。

`pip install mkdocs-material`

### ローカル環境の起動

`mkdocs.yml` がある階層で `mkdocs serve` を叩きます。
起動できたら localhost の URL がダンプされるのでアクセスすると見れます。
