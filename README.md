# diceol
eosforce 上部署的一个骰子游戏，挺无聊的。支持scatter/麦子钱包，给大家作个参考吧。  

没有使用EOS提供的两次提交随机种子的方式，而是通过链外resolver定期结算。每隔12秒的block的hash值，被resolver作为随机种子灌入合约，结算。  

单次投注，用block hash拼接上投注id，然后计算sh256,然后按字节累加求和，对100求模后+1,得到结果。  

多人投注，用block hash计算sh256,然后按字节累加求和，对10或者100求模,得到结果。  

上述过程简单，不如全部在链上有公信力。但是因为上述流程和数据都是可以追查的，还是比较可信的。  

为了尽快结算，所以结算没有等到块不可逆。如果要等到不可逆块，预计需要90秒以上的延时，更难接受。  

由于会以接入节点提供的未到不可逆的块的hash作为随机种子，所以，可能出现个别结算使用的block hash，和最终链上不可逆块的hash值不一致。  

这点应该不是大问题，首先这个hash也是源于某个节点计算出来的，也具有足够的随机性和公信力；其次，使用resolve，可以在本地记录指定节点的历史block hash值以进行检查，也是可以事后验证的。  

这个游戏目前反应速度比较慢，因为web和结算不在一起，延时至少12秒以上，也不想改进了，谢谢大家理解。  

我一直不喜欢菠菜游戏，这次做出来这个主要是练练手吧，以后还是想做点有实际价值的应用。区块链的未来，不能靠这种菠菜应用。  

这个游戏在盈亏平衡点的数学期望基础上，扣了2%的奖金，这样玩家将以大约51%甚至更高的概率持续亏钱下去，千万不要侥幸。本来想加上投注历史总额限制，但是需要消耗不少内存，所以放弃了。希望大家能够自我控制住，不要沉迷这种低级游戏，也希望帮大家看清楚菠菜游戏的本质，毕竟亏1000个EOSForce也才100块钱，比亏1000个EOS后才醒悟过来好多了吧。  

这里有一篇在EOSBet上输了11万EOS的玩家的哭诉，希望大家引以为戒，小玩怡情即可。  

[Dapp顶级玩家自述输掉11万EOS](https://mp.weixin.qq.com/s?__biz=MzU3Njc0Njk5OQ==&mid=2247483659&idx=1&sn=5a9ded0b0ba8c58e168b8a4cadcd516d&chksm=fd0e6593ca79ec85014d0a7f7f329d316e20e0d271ec847e73032320cb4203b44a0261721d4a&mpshare=1&scene=1&srcid=1020aoB0xA1ExXjBLtwoVPF2#rd)
