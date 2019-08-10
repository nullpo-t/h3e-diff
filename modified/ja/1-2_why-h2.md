## HTTP/2、覚えていますか？

HTTP/2の仕様、[RFC 7540](https://httpwg.org/specs/rfc7540.html)は2015年5月に公開され、インターネットおよびWorld Wide Webに広く展開・実装されてきました。
2018年初頭において、世界のトップ1000のウェブサイトの約40%はHTTP/2で動作し、Firefoxが発行したHTTPSリクエストのうち約70%がHTTP/2のレスポンスを返され、すべての主要なブラウザやサーバー、プロキシがHTTP/2をサポートしています。
HTTP/2はHTTP/1が持つ大量の欠点に対処しており、導入することでHTTPユーザーはWeb開発者を大いに煩わせる多くのその場しのぎの回避策を使わずに済みます。

HTTP/2の主要な特徴の一つは、多重化（multiplexing）です。
複数の論理的なストリームを単一のTCPコネクションで転送することで、輻輳制御の効果を飛躍的に向上させます。
ユーザーがTCPを効率よく使用できるようになることで回線を帯域幅いっぱいに使えるようになり、TCPコネクションが長持ちします。
結果として、以前より頻繁に最高速で通信できるようになります。
加えて、ヘッダー圧縮は使用する帯域幅を小さくします。

HTTP/2では、ブラウザが各ホストに対して確立するTCPコネクションの数は、以前のHTTPの6個とは異なり、*単一*であることが一般的です。
実際、HTTP/2で使用されるコネクションの統合と「デシャーディング」は、さらにコネクション数を減らすことがあります。
HTTP/2はHTTPにおけるhead-of-lineブロッキング問題[^1-2_1]を解消します。

![HTTP/2マン](../images/h2-man.jpg){height=6cm}

[^1-2_1]: クライアントは、過去のリクエストの応答を取得し終わるまで、次のリクエストを送信できないこと

\newpage