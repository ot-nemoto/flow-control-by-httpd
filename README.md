# flow-control-by-httpd

## 概要

- httpdに流量制限を設定し検証

|Path|Method|流量制限|HTTPステータス|備考|
|--|--|--|--|--|
|/en/1.html|GET|-|-|-|
|/jp/1.html|GET|BandWidth:10240,MaxConnection:10|429||
|/jp/2.html|GET|BandWidth:10240,MaxConnection:10|429|Basic認証|
|/1/|GET|-|-||
|/2/|GET|BandWidth:10240,MaxConnection:10|429||
|/3/|GET|BandWidth:10240,MaxConnection:10|429|Basic認証|

- appは[サンプルwar](https://tomcat.apache.org/tomcat-7.0-doc/appdev/sample/sample.war)

## 環境構築

*build*

```sh
docker-compose build
```

*deploy*

```sh
docker-compose up -d
```

## 参考

- webのdocker build時に、`apxs -i -a -c mod_bw.c` でmod_bwをインストールすると全てのモジュールを読み込む直前にに、mod_bwの読み込みを行うように設 定ファイルを更新する

```conf
LoadModule bw_module          /usr/lib64/httpd/modules/mod_bw.so
#
Include conf.modules.d/*.conf
```

- これが `Include conf.modules.d/*.conf` の後ろに手動で定義をすると、ajpによるtomcatとの連携の前に、流量制限がかかるなるので注意
  - refs: https://detail.chiebukuro.yahoo.co.jp/qa/question_detail/q1351734178
