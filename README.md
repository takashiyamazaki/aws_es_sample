fluentdを利用してAWS ESにダミーログを流し込むサンプルプログラム

# 準備
## gemのインストール
~~~
gem install fluentd
gem install apache-loggen
~~~
## fluentd.confの修正
~~~
・・・
###  ダミーログを出力するパス
path /your/path/dummy-httpd-access.log
・・・
### AWS ESのドメイン
host search-xxxxxx-xxxxxx.us-west-2.es.amazonaws.com
・・・
~~~

# 起動
~~~
git clone https://github.com/takashiyamazaki/aws_es_sample.git
cd aws_es_sample
fluentd -c fluend.conf

（別のターミナルを開いて）
apache-loggen --rate=10 --limit=100 --progress /your/path/dummy-httpd-access.log
~~~

# 確認
* AWSのマネージメントコンソールでAWS ESのページを開き、Kibanaを開く。
* インデックスの指定があるので httpd-* と入力し、時間のキーを @timestamp にする。
