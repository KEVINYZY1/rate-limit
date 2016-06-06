# Rate Limiter

降级和限流是面对大流量必不可少的神兵利器. 流量控制算法就是通过网络整形或者速率控制来解决此类问题.

## 流量控制算法
* 令牌桶算法
* 漏桶算法

**令牌桶算法**
1. 每秒会有 r 个令牌放入桶中，或者说，每过 1/r 秒桶中增加一个令牌
2. 桶中最多存放 b 个令牌，如果桶满了，新放入的令牌会被丢弃
3. 当一个 n 字节的数据包到达时，消耗 n 个令牌，然后发送该数据包
4. 如果桶中可用令牌小于 n，则该数据包将被缓存或丢弃

![](./token_bucket.JPG)

**漏桶算法**
1. 数据被填充到桶中,并以固定速率注入网络中,而不管数据流的突发性
2. 如果桶是空的,不做任何事情
3. 主机在每一个时间片向网络注入一个数据包,因此产生一致的数据流

![漏桶算法](./Leaky_bucket_analogy.JPG)

这两个算法是有区别的:
`漏桶算法`能够强行限制数据的传输速率,而`令牌桶`算法在能够限制数据的平均传输速率外,还允许某种程度的突发传输.