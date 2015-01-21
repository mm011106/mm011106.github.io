---
layout: page
title: "man mosquitto_sub"
date: 2014-12-06 0:00

comments: true
sharing: true
footer: false
---

[`mosquitto_sub(1)`](http://mosquitto.org/man/mosquitto_sub-1.html)

日本語：

----  

###名前
** mosquitto_sub **    トピックを購読するためのMQTTバージョン3.1クライアント

----  

###コマンド

mosquitto_sub [-A bind_address] [-c] [-d] [-h hostname] [-i client_id] [-I client id prefix] [-k keepalive time] [-p port number] [-q message QoS] [-R] [-S] [-N] [--quiet] [-v] [ [-u username] [-P password] ] [ --will-topic topic [--will-payload payload] [--will-qos qos] [--will-retain] ] [[ { --cafile file | --capath dir } [--cert file] [--key file] [--tls-version version] [--insecure] ] | [ --psk hex-key --psk-identity identity [--tls-version version] ]] [-T filter-out...] -t message-topic...

mosquitto_sub [--help] 

----

###概要

** mosquitto_sub **は、トピックを購読し受信したメッセージを印刷する、シンプルなMQTT3.1のクライアントです。

----

###オプション

- -A  
出て行く接続先をローカルのIP/ホスト名に固定します。
特定のインターフェイスとのネットワークコミュニケーションに制限する必要がある場合にこのオプションを使用してください。

- -c, - - disable-clean-session  
celan-sessionフラグを無効にします。これは、クライアントへのすべての購読をQoS1,2のメッセージの受信については維持するものです。クライアントが再接続をした時点で、溜まっていたメッセージが受信されます。  
このオプションを使う場合、`--id`オプションを使ってメッセージIDを手動でセットすることをおすすめします。

- \- - cafile  
信頼できるPEMエンコードされたCA認証**ファイルへのパス**を指定します。SSL通信を有効にするために使用されます。  `--capath`も参照のこと。

- \- - capath  
信頼できるPEMエンコードされたCA認証が入っている**ディレクトリへのパス**を指定します。SSL通信を有効にするために使用されます。  
`--capath`を正しく動作させるために、認証フィアル名の終わりは".crt"にしてください。さらに、`c_refresh <path to capath>`を認証ファイルの追加・削除ごとに実行してください。

- \- - cert  
サーバが必要とする場合、このクライアントのPEMエンコードされた認証があるファイルへのパスを指定します。　`--key`も参照のこと。

- \- - ciphers  
クライアントをサポートするためのopenSSLにコンパチブルなTLS　ciphersリストです。詳しくは`ciphers(1)`を見てください。

- -d, - - debug  
デバグメッセージを有効にします。

- \- - help  
使い方を表示します。

- -h, - - host  
接続するホストを指定します。デフォルトは`localhost`です。

- -i, - - id  
このクライアントのためのidで、デフォルトでは`mosquitto_sub`にクライアントのプロセスidがついたものです。`--id-prefix`オプションと同時には使えません。

- -I, - - id-prefix  
クライアントプロセスのプロセスｉｄを元にクライアントidを作るために使われるプリフィックスを指定します。`--id`オプションとは同時に使えません。

- \- - insecure  
証明書ベースの暗号化を行う場合、このオプションはサーバ証明にあるホスト名の確認を無効にします。これは、初期のサーバ設定をテストするのに便利ですが、たとえば、悪意のあるサードパーティよってDNSスプーリングが偽装されることを可能にします。このオプションは ** テストのためだけに ** 使用してください。このオプションを製品環境で使うことに陥ってしまうのなら、その構成はダメなもので暗号化の意味は全くありません。

- \-k, - - keepalive  
接続していて、機能しているということを知らせるための、ブローカへのPINGコマンドの発信間隔\[s\]を設定します。デフォルトでは60\[s\]です。

- \- - key  
サーバが必要とする場合、このクライアントのPEMエンコードされたプライベートキーファイルが入っている**ファイルへのパス**を指定します。`--cert`も見てください。

- -N  
印刷の時にペイロードに対して改行コードを付加しません。これによってペイロードを直接ほかのいくつものアプリケーションに対してストリーミングすることが可能です。`-v`オプションを使っていない時だけ動作します。  
(訳注：手元のmosquitto_subではこのオプションを指定するとエラーになります）

- -p, - - poart  
ポート番号を指定して、デフォルトのポート番号1883以外のポートに接続します。

- -P, - - pw  
ブローカに認証してもらうためのパスワードを提供します。`username`を指定しないでこのオプションを使うことは出来ません。このオプションにはMQTT v3.1をサポートしたブローカが必要です。`--username`オプションを参照。

- \- -psk  
TLS-PSK暗号化に使うため、ブローカに使われているものとマッチする16進のpre-shared-key（0xプリフィックスは不要）を提供します。`--psk-identity`も同時に提供される必要があります。

- \- -psk-identity  
TLS-PSKで使われるcleient identitiyです。ブローカの設定によってはusernameの代わりに使われます。


- -q, - -qos  
0,1,2のいずれかで受信するメッセージに期待するQoSを指定します。QoSについては`mqtt(7)`を参照してください。


- \- -quiet  
このオプションが与えられた場合、実行時のエラーは出力されません。無効なユーザ入力に対して出されるエラーメッセージはすべて抑止されます。(`--port` オプションをポート番号指定なしで使った場合など）

- -R  
このオプションが与えられた場合、リテインビットがセットされているメッセージを受信すると、そのメッセージは出力されません。リテインビットがセットされているメッセージは”古い”もので、いつ発行されたメッセージであるかわかりません。ワイルドカードでトピックを指定してパブリッシュを要求した場合、多くのリテインメッセージが含まれているはずです。このオプションはそのようなメッセージを抑止します。

- -S  
どのホストに接続するかを決めるためにSRVを参照します。-hオプションと同時に使われた場合、`_mqtt._tcp.<host>`を参照します。それ以外では`_mqtt._tcp.<local dns domain>`を参照します。

- -t, \- -topic  
購読するMQTTトピックです。MQTTトピックについては`mqtt(7)`を参照してください。複数のトピックを一度に購読するために繰り返し使われても構いません。

- -T, \- -filter-out  
フィルタにマッチするトピックの印刷を抑制します。ワイルドカードを使った購読でワイルドカードの一部分だけを印刷することを可能にします。  
例えば、"BBC"ツリーを購読していて"Radio 3"からの出力を見たくない時には  
`mosquitto_sub -t bbc/# -T bbc/radio3`  
のように設定します。このオプションは複数のトピックやトピックツリーを除外するために繰り返し使うことが可能です。

- \- -tls-version  
ブローカと接続するために使うTLSプロトコルのバージョンを選びます。選択肢は`tlsv1.2`　`tlsv1.1`　`tlsv1`です。  
デフォルトは`tlsv1.2`です。インストールされているopenSSLのバージョンが古いと`tlsv1`だけが有効かもしれません。これはブローカで使われているバージョンと一致する必要があります。

- -u, - -username  
ブローカに認証してもらうためのユーザ名を提供します。このオプションにはMQTT　v3.1をサポートするブローカが必要です。`--pw`オプションも参照してください。

- -v, - -verbose  
受信したメッセージを詳しく表示します。このオプションではメッセージを"topic payload"のように表示します。このオプションがない場合には"payload"のみの表示になります。

- \- -will-payload  
ブローカに保存されるメッセージを指定します。これはこのクライアントが予期せずに切断された場合送信されます。このオプションは`--will-topic`とともに指定される必要があります。

- \- -will-qos  
WillのQoSを指定します。デフォルトでは0になります。このオプションは`--will-topic`とともに指定される必要があります。

- \- -will-retain  
これが与えられた場合、クライアントが予期せずに切断された場合のメッセージはリテインメッセージとして扱われます。このオプションは`--will-topic`とともに指定される必要があります。

- \- -will-topic  
クライアントが予期せずに切断された場合のWillを送るトピックを指定します。

----

###Will（遺言）
`mosquitto_sub`はクライアントが予期せずに切断された場合のメッセージをブローカに登録することが出来ます。くわしくは`mqtt(7)`をご覧ください。

最小限必要なことは`--will-topic`オプションを使ってWill（遺言）を送り出す先のトピックを指定することです。これにより、リテインしない、長さ0のメッセージをQoS0で送信することになります。

その他のWill(遺言）パラメタを設定するために`--will-retain` `--will-payload` `--will-qos`オプションを調整してください。

----

###例

以下は本当にただの例です。トピックの購読指示はうまく動くかもしれませんが、何かを受信するためには、当該のトピックにデータが送られないといけません。

ローカルホストからQoS1で温度の情報を購読します。

	mosquitto_sub -t sensors/temperature -q 1

ハードディスクからの温度情報を複数の計算機・ハードディスクから購読します。この例ではそれぞれの計算機のハードディスクの温度が"sensors/machines/HOSTNAME/temperature/HD_NAME"に発行されている必要があります。

	mosquitto_sub -t sensors/machines/+/temperature/+

すべてのブローカのステータスメッセージを購読するには

	mosquitto_sub -v -t \$SYS/#


----

###バグ

**mosquitto_sub** のバグについての情報は[http://launchpad.net/mosquitto/]で見つかるかもしれません。

----

###こちらもご覧ください

 mqtt(7) , mosquitto_pub(1) , mosquitto(8) , libmosquitto(3) , mosquitto-tls(7) 

----

###謝辞

This product includes software developed by the OpenSSL Project for use in the OpenSSL Toolkit. (http://www.openssl.org/)

This product includes cryptographic software written by Eric Young (eay@cryptsoft.com)

This product includes software written by Tim Hudson (tjh@cryptsoft.com)

----

###著者

Roger Light <roger@atchoo.org>

