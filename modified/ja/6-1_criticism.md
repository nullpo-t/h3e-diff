# さらなる情報

## よくある批判

### UDPは多くの企業や組織で動かない

多くの企業、運用者、組織は、昨今においてほとんどが攻撃に悪用されるという理由から、ポート53（DNSに使われる）以外のUDPトラフィックをブロックするか、帯域制限をかけています。
特に、いくつかの既存のUDPを使用するプロトコルとその実装は、大量のトラフィックを無関係な第三者に送るアンプ攻撃に対して脆弱であり続けています。

QUICではアンプ攻撃に対する軽減策を備えています。Initialパケットは1200バイト以上であること[^6-1_1]、クライアントからの応答を受け取っていない場合、リクエストの3倍よりも大きいサイズのデータをクライアントに送ってはならないとプロトコルで定められています。

[^6-1_1]: 編注: 足りない場合はパディングを行う必要があります

### UDPはカーネル内で遅い

少なくとも2018年において、これは正しいように思われます。
長い間、UDP転送のパフォーマンスは開発者が関心を向ける項目ではなかったため、果たしてどの程度遅いか、今後どのように発展していくかは分かりません。
ただ、ほとんどのクライアントにとって、この「遅さ」が気になることはないはずです。

### QUICはCPUを使いすぎる

前述の「UDPは遅い」と似ていますが、世界中で使われているTCPとTLSは長い年月をかけて成熟、改善、さらにはハードウェア支援を得ているので、そのように思えるのです。
したがって、時間が経つにつれ、この問題の改善が見込めます。
気にすべきは、このCPU使用率の増加がどれだけ利用者に悪影響を与えるかです。

### Googleの技術でしょ？

いいえ。Googleはインターネット規模でこのようなUDPを用いたプロトコルが優れた性能を示すことを証明し、初期仕様をIETFに提案しました。
それからは、多数の企業や組織から参加している個人が、ベンダーニュートラルなIETFでプロトコルの標準化に取り組んでいます。
Googleの従業員はもちろん参加していますが、他にもMozilla、Fastly、Cloudflare、Akamai、Microsoft、Facebook、Appleなど、インターネット上のトランスポートプロトコルの発展に興味を持つ多くの企業の従業員が参加しています。

### 小さすぎる改善だ

これは批判ではなく、一つの意見です。おそらくその通りで、HTTP/2のすぐ後の改善にしては小さすぎるかもしれません。
HTTP/3はパケットロスの多いネットワークで優れた性能を発揮し、高速なハンドシェイクによるレイテンシの改善は、計測値と体感の両方において見込めるでしょう。
しかし、それはサーバーやサービスでHTTP/3のサポートを提供するだけの価値があるでしょうか。
それはきっと、時間が、そして将来のパフォーマンス計測の結果が教えてくれるでしょう！