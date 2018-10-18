# Cosmos中关于验证节点（Validator）的一些概念

主要译自https://cosmos.network/docs/validators/validator-faq.html

## Validator的职责
能够无间断地正确运行：
	* 及时升级，保证软件版本正确，修复bug
	* 不掉线
	* 私钥安全
积极参与社区治理：对每一个proposal都进行投票（包括修改gas limit等操作性参数的交易、对社区规范的修正等），每次validator不投票都会受到一点小小的惩罚（slashing）

## 持有股权的动机
* token的通胀，促使atom持有者绑定股权
* 获得打块的奖励；
* 获得交易费用

## 成为Validator的动机
* 由于commission的存在，Validator能获得比delegator更高比率的收益；
* 主导社区治理

## 对Validator实行惩罚的条件
* 双重签名（double signing）：Validator在A链和B链上的同一高度上为分别块签名，如果被A链发现，则会在A链上受到惩罚
* 不可达(unavailability)：如果链上最新的X个块上都没有validator的签名，该validator会被以X的边际值进行惩罚，如果X的值超过一个临界值Y，则该validator会被解绑（unbonding）
* 不投票（non-voting）：每次validator不投票都会受到一点小小的惩罚

## 成为Validator
通过发送“create-validator”交易，任何节点（任何时间），其股权池在所有validator中排名进入当年席位数，都可能成为validator
该交易需要的字段：
* 公钥：相关联的私钥用于prevote和precommit。这种方式要求节点作为validator和作为流动资金所有者拥有不同的account
* validator地址：应用层面地址
* validator name（moniker）
* 网站（可选）
* 描述（可选）
* 初始commission rate，Validator获得的收益，分红给委派者的浮动比率，是一个百分比。计算方法详见"利益分配"一节
* 最大commission rate，validator能承受的最大commission
* commission增长率：validator的commission最大的日增长率
* 准备金（最小自绑定股权Minimum self-bond amount）：validator始终持有的最小atom数量。如果低于这个数值，validator的整个股权池（staking pool，包括其自身和委派者所绑定的atom）将会被解绑。
cosmos并没有设置成为validator的自绑定量门槛，仅根据股权池排名来确定是否失去validator身份。Validator自绑定股权不是必须的，它可以全部股权都来自delegator。但往往Validator需要有一部分自绑定股权，以免被delegator绑架。因此“create-validator”交易中的准备金，对于Validator是一种安全机制。
* 初始自绑定股权（ Initial self-bond amount）：validator初始拥有并希望绑定的atom数量。

## 创世验证节点（genesis validator）
在创世块中，作为validator的节点将会在创世交易中标识为候选节点，构成：
* 已经初始配给了一定atom的投资人；
* 参与testnet、代码开发、评审的社区参与者

Cosmos Network上线前夕将考验投资参与者的能力，以便寻找执行者。现在即是成为Cosmos validator的关键时间节点。
目前对想成为validator节点的建议：
* 尽快加入testnet
* 展示对validator节点部署、迁移、安全实践的能力
* 具有网络监控的工具和能力
* 创建网页/社交平台主页在atom社区刷存在感
* 参与validators的讨论群组
群组
https://riot.im/app/#/room/#cosmos_validators:matrix.org
http://t.me/cosmosproject

在testnet中能够保持长时间稳定在线的validator候选人可以保留在创世validator的席位。
截至2018-10-17，testnet有88个validator（详见https://explorecosmos.network/validators），在运行第一年(year 0)中将会有100个validator席位。
cosmos对validator席位的逐年规划：
Year 0: 100
Year 1: 113
Year 2: 127
Year 3: 144
Year 4: 163
Year 5: 184
Year 6: 208
Year 7: 235
Year 8: 265
Year 9: 300
Year 10: 300

## Validator的状态转换
### 绑定（bonded）：
活跃，能参与共识，能够被奖惩。
股权池低于准备金或者排名掉出席位数，或者主动发送unbonding交易（收益变现）后将会转为unbonding
### 解绑中（unbonding）：
非活跃、不能参与共识、不能获得奖励，但依然可能因作恶而受到惩罚。
可以通过发送“rebond”尝试重新激活绑定；如果没有重新绑定，unbonding状态超过3周才会转换到unbonded；
### 已解绑（unbonded）：
非活跃、不能共识、不能获得奖惩。
这个状态下依然可以被委派，也可以随时解除委派。

## 委派（delegating）
成为创世候选人的主要要求是你的部署能够被cosmos社区理解，以便潜在的委派者（delegator）可以评估哪些validator值得他们下注手中的atom。
通过Cosmos Voyager，委派者可以将atom投资给validator，以便获得相应收益（按照validator设置的commission rate），同时承担相应责任。被委派的validator会增长staking power，staking power的增长意味着在共识和社区统治中更大的权重（weight）。validator并非拥有了委派者的atom，但如果validator作恶，委派者的股权会被按比例削减。

这要求委派者尽力调研他们希望投资的validator，并分散投资多个validator。同时长期主动监控validator的动态，从而参与社区治理。

## Validator的权重（weight）
权重表明validator是否活跃、能够执行打块（propose）的频率。

* validator的股权池stake pool = valiator自己绑定的stake + delegator对该validator投资的stake
* validator的权重weight = 该validator自己的股权池 / 全部validator的股权池

cosmos上线第一年将会按权重排序，权重最高的前100名validator会成为活跃validator。如果validator双重签名（作恶）、经常掉线或者不参与社区治理，他们本身及其他用户委派给他们的atom将会被销毁/消减。

## 利益分配
### block provisions
#### validator之间：
block provision奖励并非流向proposer，而是cosmos network上所有Validator依据权重分配。能够保证打块行为不会导致其权重变化。

#### validator和delegator之间：
由validator自绑定占其股权池的比例和commision决定。

例：
validator个数10，权重相等，commission rate=1%，每个validator自绑定20%股权
打块奖励1000atoms，按照权重每validator+delegators奖励100，分配：

commission = 100 * (1 - 20%) * 1% = 0.8 atoms  
validator收益 = 100 * 20% + commission = 20.8 atoms
delegator总收益 = 100*80% - commission = 79.2 atoms

### Fee
负责打块的proposer能够获得额外的收益，但必须符合较严格的要求：precommit阶段需要有2/3的validator投票通过，proposer才能打块，而多于2/3投票，才将会为proposer带来额外收益。而往往收集更多的投票，需要proposer付出更多的时间代价，这就要求proposer寻找到合适的平衡点。
多于2/3投票给proposer带来的收益是线性的：从2/3到1，额外的收益从1%到5%

例：
validator个数10，权重相等，commission rate=1%，每个validator自绑定20%股权
现在打了一个块，收到1025.51020408 atom的fee
首先，扣掉2%的税。扣掉的税保存在预留池（reserve pool），还剩下1005个atom。
假如proposer在块中收集到了100%validator的签名，则获得fee的5%的，对其他未打块的validator收益R有
9R+R+R*5% = 1005
则 R=100

对于proposer：
proposer及其delegator收到 R * (1 + 5%) = 105 atom
commission 105 * 80% * 1% = 0.84 atom
proposer得到 105 * 20% + commission = 21.84 atom
delegator得到 105 * * 80% - commission = 83.16 atom

对于非proposer的validator：
validator及其delegator得到 R = 100 atom
validator得到 100 * 20% + commission = 20.8 atom
delegator得到 100 * 80% - commission = 79.2 atom 
