## Alt-svcによる接続開始

### Alt-svc

Alt-svc（Alternate service）ヘッダーとそれに対応する `ALT-SVC` HTTP/2フレームは、QUICや HTTP/3のために設計されたわけではありません。
これらはサーバーがクライアントに対して*「ちなみに、私は同じサービスをこのホスト、プロトコル、ポートでも実行していますよ」*と伝えるための、既に設計・作成されたメカニズムの一部です。
詳細は[RFC 7838](https://tools.ietf.org/html/rfc7838)を参照してください。

このようなAlt-svc応答を受け取ったクライアントは、自身が代替プロトコルをサポートしていて、更にそれを希望する場合、そのプロトコルを使用した接続をバックグラウンドで並列して行い、成功した場合は最初の接続のかわりにその接続に切り替えることができます。
最初の接続がHTTP/2またはHTTP/1を使用している場合、サーバーはクライアントに対してHTTP/3による再接続が可能であると伝えることができます。それは同じホストに対してかもしれませんし、そのオリジンを提供できる別のホストかもしれません。
このようなAlt-svc応答で与えられる情報には有効期限が設けられます。クライアントが、ある特定の期間だけ代替ホストに対して提案されたプロトコルを用いて後続のコネクションとリクエストを直接行うことを可能にするためです。

### 例

HTTPサーバーはレスポンスヘッダーに `Alt-Svc:` を含みます:

    Alt-Svc: h3=":50781"

これは、HTTP/3がこのレスポンスを返したものと同じホストのUDP 50781番ポートで使用可能であることを示します。
クライアントはその宛先に対してQUICコネクションの確立を試みることが可能で、成功した場合は最初のHTTPバージョンではなく、代替接続でオリジンと通信を続けることができます。