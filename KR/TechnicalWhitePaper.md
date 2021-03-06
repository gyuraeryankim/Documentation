# EOS CHROME Technical White Paper v1.0

**Oct 24, 2018**

<!-- MarkdownTOC depth=4 autolink=true bracket=round list_bullets="-*+" -->

- [Introduction](#introduction)
  * [Blockchain Trilemma](#blockchain-trilemma)
- [Problems in EOS](#problems-in-eos)
  * [Asset Risk 1. The Whale Investors](#asset-risk-1-the-whale-investors)
  * [Asset Risk 2. Fixation of Block Producers](#asset-risk-2-fixation-of-block-producers)
  * [Asset Risk Summary](#asset-risk-summary)
  * [Voting Risk 1. Low-Voting Turnout](#voting-risk-1-low-voting-turnout)
  * [Voting Risk 2. Voting Mediators](#voting-risk-2-voting-mediators)
  * [Voting Risk Summary](#voting-risk-summary)
  * [Structural Risk 1. A Number of Block Producers](#structural-risk-1-a-number-of-block-producers)
  * [Structural Risk Summary](#structural-risk-summary)
  * [Summary of Problems in EOS](#summary-of-problems-in-eos)
- [The Proposal: EOS CHROME](#the-proposal-eos-chrome)
  * [Solutions](#solutions)
- [EOS CHROME: Burn and Earn Delegated Proof of Stake (B&E DPoS)](#eos-chrome-burn-and-earn-delegated-proof-of-stake-be-dpos)
  * [Separation of Asset and Utility](#separation-of-asset-and-utility)
  * [Combining Block Producers and dApp](#combining-block-producers-and-dapp)
  * [Burn and Earn](#burn-and-earn)
- [Inter-Contract Communication (ICC)](#inter-contract-communication-icc)
  * [Limitations of Smart Contract](limitations-of-smart-contract)
  * [IoT vs. ICC](#iot-vs-icc)
  * [Inter Contract Communication](#inter-contract-communicaton)
- [EOS CHROME Summary](#eos-chrome-summary)
- [Conclusion](#conclusion)
- [Roadmap](#roadmap)

Copyright © 2018 IBCT

DISCLAIMER: This eosChrome Technical White Paper v1 is for information purposes only. IBCT does not guarantee the accuracy of or the conclusions reached in this white paper, and this white paper is provided “as is”. IBCT does not make and expressly disclaims all representations and warranties, express, implied, statutory or otherwise, whatsoever, including, but not limited to: (i) warranties of merchantability, fitness for a particular purpose, suitability, usage, title or noninfringement; (ii) that the contents of this white paper are free from error; and (iii) that such contents will not infringe third-party rights. IBCT and its affiliates shall have no liability for damages of any kind arising out of the use, reference to, or reliance on this white paper or any of the content contained herein, even if advised of the possibility of such damages. In no event will IBCT or its affiliates be liable to any person or entity for any damages, losses, liabilities, costs or expenses of any kind, whether direct or indirect, consequential, compensatory, incidental, actual, exemplary, punitive or special for the use of, reference to, or reliance on this white paper or any of the content contained herein, including, without limitation, any loss of business, revenues, profits, data, use, goodwill or other intangible losses.


# Introduction
현재 많은 사람이 알고 있는 비트코인은 제 1세대 블록체인으로 개인의 익명성과 사생활 보호를 최고의 가치로 두는 Cypherpunk 정신에 근간을 둔다. 비트코인은 중재자 없는 개인 간 p2p금전 거래에 최초로 블록체인 기술이 적용된 사례라고 할 수 있다. 제 2 세대 블록체인으로 Vitalik Buterin에 의해 개발된 이더리움 블록체인 네트워크를 들 수 있다. 이더리움은 p2p 금전 거래만을 위한 1세대 비트코인 네트워크를 대폭 개선하여 기존 p2p 금전 거래와 더불어 스마트 컨트랙트라는 새로운 개념을 자체 블록체인 네트워크에 적용하였다. 이더리움의 스마트 컨트랙트는 블록체인 기술의 특징인 비가역성(irreversibility)과 불변성(immutability)을 활용하여 블록체인 내에 입력 된 프로그래밍 코드로, 입력된 코드가 특정 조건을 만족할 시 자동적으로 집행 되는 특징을 갖는다. 오늘 날, 전 세계 많은 사람들은 암호 화폐 p2p 거래에 제 1세대 블록체인과 제 2세대 블록체인으로 대표 되는 비트코인과 이더리움을 널리 사용하고 있지만, PoW (Proof of Work) 합의 알고리즘을 적용한 비트코인 블록체인과 PoW와 PoS (Proof of Stake)의 하이브리드 모델을 적용하고 있는 이더리움 블록체인의 기술적 한계를 체감하고 있다. 

## Blockchain Trilemma
현재 1세대, 2세대 블록체인이 직면한 기술적 한계의 대표적인 예로 네트워크가 확장됨에 따라 초당 거래 처리 속도 (TPS)가 크게 개선되지 못하는 확장성(Scalability) 문제를 꼽을 수 있다. 하지만 블록체인 기술의 확장성 문제를 해결 함에 있어서 발목을 잡는 두 가지 요소가 존재 하는데, 이는 바로 분산화 (Decentralization) 문제와 안정성 (Safety) 문제이다. 이러한 확장성, 분산화 그리고 안정성 문제를 포괄한 개념이 바로 블록체인의 Trilemma이다. 

블록체인의 Trilemma는 확장성, 분산화, 안정성 모두 양적(positive) 방향으로 개선 시킬 수 없고 일정 요소를 강화하면 다른 요소를 희생하는 등가 교환 구조와 같다. 예를 들어, 네트워크의 확장성을 확보하기 위해 기존보다 적은 수의 노드를 두어 보다 빠른 합의 과정을 구현할 수 있지만 노드의 수가 줄어들수록 네트워크 분산화 효과와 안정성이 줄어든다. 같은 맥락으로, 많은 수의 노드를 두어 네트워크 분산화와 안정성을 달성할 수 있지만 확장성이 줄어들게 된다. 

위와 같은 1세대, 2세대 블록체인의 트릴레마 문제를 해결하기 위해 제 3세대 블록체인 플랫폼, EOS가 출시 되었다. EOS란 과거 Bitshares, Steemit을 개발한블록체인 개발자 Dan Larimer가 Block.one과 함께 만든 제 3세대 블록체인이다. Delegated Proof of Stake, DPoS 방식의 합의 알고리즘을 사용하며 기존 1세대 블록체인 Bitcoin과 2세대 블록체인 Ethereum이 쉽게 해결하지 못한 Transaction Per Second (TPS) 문제를 획기적으로 개선했다는 평가를 받았으며, ‘The Ethereum Killer’라는 명칭까지 얻게 되었다. 

하지만 아직까지 EOS는 블록체인의 Trilemma 문제를 풀지 못했다. 현재의 EOS는 너무나 많은 문제점을 갖고 있으며 네트워크의 본질적인 구조적 변경 없이 블록체인의 Trilemma 문제를 해결할 수 없다. 이번 컨셉 페이퍼를 통해 EOS의 문제점을 자세히 살펴보고 블록체인의 Trilemma 문제 해결을 위한 새로운 대안, EOS Chrome 을  제안하고자 한다. 

# Problems in EOS


## Asset Risk 1. The Whale Investors 

<EOS 고래 투자자 현황>

현재 EOS가 직면한 첫 번째 자산 리스크는 소수의 고래 투자자 리스크이다. 현재 EOS 네트워크의  Block Producers (BP) 순위는 소수의 고래 투자자들에 의해 쉽게 좌지우지 될 수 있다. 실시간 BP 정보를 제공하는 eos.dapptools에 따르면 2018년 7월 23일 기준 21번째 BP 와 22번째 BP의 투표율 차이는 0.01%이다. 현재 EOS 네트워크 내 BP 투표를 진행 한 상위 10위 고래 투자자들이 전체 EOS 토큰 발행량의 5.66%를 보유하고 있는 것을 감안한다면 각 고래 투자자의 BP 투표 영향력은 매우 큰 것을 알 수 있다. 


<eos.dapptools 차트, 21위와 22위의 근소한 차이>


또한, EOS의 총괄 개발을 맡고 있는 Block.One사는 전체 EOS 발행량의 10%에 해당하는 EOS를 보유하고 있는데, 2018년 6월 28일 BP투표에 ‘active minority voting member,’ 즉 적극적인 소수 투표자로 참여하기로 결정 했음을 커뮤니티에 알렸다. 10%의 전체 보유량을 가진 Block.One의 투표 참여가 과연 ‘소수’의 투표권을 사용하는 것이라고 볼 수 있을까? 한국 시간 7월 6일 10시 50분 기준 현재 1위 BP의 득표량이 2.88%인 것을 감안한다면, Block.One의 투표 참여는 ‘적극적 소수’가 아닌 ‘절대적 다수’의 힘을 가지고 투표에 참여하는 셈이다. 이 역시 고래 리스크의 대표적인 예로 볼 수 있다. 


<Block.One의 증인 투표 참여 공지>


소수의 고래 투자자 리스크는 모종의 BP와 고래 투자자 간의 이면 계약 가능성을 내포한다. 

<BP 후보 eosDAC이 고래 투자자에게 보낸 메세지>

현재 EOS 헌법에 따라 BP 투표에 대한 보상 지급 행위를 금지하고 있지만, 이해 관계가 정확히 부합하는 소수의 고래 투자자와 BP의 사적인 연합은 막을 방도가 없다. EOS Canada의 Revenue Analysis에 따르면 1개의 EOS가격을 $5로 가정 했을때 21위 (선정된 BP) 와 22위 (선정되지 않은 BP 후보)의 월 수익 차이는 최대 $96,806 (약 1억 원)을 상회한다. 따라서, BP로 선정 되는 것은 모든 BP 후보가 바라는 일이며, 이는 소수의 고래 투자자의 영향력으로 충분히 상황이 바뀔 수 있기 때문에 소수의 고래 투자자들과 BP 후보들 간의 상호이익을 위한 이면 계약이 충분히 존재할 수 있다.


<Revenue Simulation / Analysis by EOS Canada>


## Asset Risk 2. Fixation of Block Producers

EOS의 두 번째 자산 리스크는 BP의 고착화이다. BP의 고착화란, 선출된 BP가 BP로서의 지위를 장기적으로 갖게 되는 경우를 말한다. EOS BP는 EOS 보유자들의 투표로 선출 된다. 현재 EOS는 메인넷 초기 단계로 BP의 변동이 비교적 자주 발생하고 있지만, EOS의 BP 투표 방식의 전신인 Steemit Witness 투표 시스템은 이미 상당 부분 BP의 고착화가 진행 된 상태이다. 물론, 선출 된 상위 21개의 BP가 제 역할을 성실히 수행하고 네트워크에 도움이 되는 방향으로 자신의 자원을 기여할 유인이 존재 한다. 하지만, 다른 한 편으로 BP의 고착화는 대기자 BP 후보들과 선출된 BP 간의 진입 장벽을 지속적으로 높이는 결과를 초래할 수 있다. 예를 들어, EOS 메인넷 초기 출범 이래 선출된 BP들은 투표에 비례하여 얻게 되는 보상 + BP 역할 수행을 함으로써 얻게되는 보상을 지급 받는 반면, 대기 BP 후보는 자신이 받은 투표에 비례하여 얻게되는 보상만 받게 된다. 심지어, 보상 수취액이 100 EOS 이하일 경우  BP후보는 보상을 수취할 수 없다. 따라서, 선출 된 BP는 선출되지 못한 대기 BP 후보에 비해 더 많은 자본을 축적 할 수 있고, 이렇게 축적 된 자본을 바탕으로 자신들의 생태계 내 경쟁력을 확보할 수 있다. 

그렇다면 왜 이런 현상이 일어나는 것일까? 첫째로, EOS BP 투표자의 입장에서 BP들을 구분하여 판단할 기준이 부족하다. BP들은 EOS 네트워크의 블록 생성과, Computation, Storage, RAM 등 하드웨어 자원을 제공하는 주체임을 감안해 볼 때, 이상적인 BP선출 기준으로 하드웨어 역량을 꼽을 수 있다. 그렇다면 다음의 예를 살펴 보자. 



<하드웨어 역량에 따른 투표 기준>

하드웨어 역량을 중요한 BP 선출 기준으로 산정할 경우 아래 두개의 BP 후보 중 누구에게 투표 하는 것이 현명한 선택일까? 숫자로 질을 평가 하자면 오른쪽의 BP후보가 왼쪽의 BP후보 보다 우위에 있고 EOS 네트워크의 확장성을 고려 하였을 때 오른쪽 BP 후보가 블록을 생성하는 것이 더욱 효율적이라고 판단할 수 있다. 하지만, 실제 BP 투표 결과는 반대로 나타났다. 오른쪽 BP 후보는 2018년 7월 2일 현재 64위를 기록하고 있는 EOSoCal 이고 왼쪽의 BP후보는 현재 1,2위를 다투는 Huobi다. 이것이 시사하는 바는, 현재 BP 선출 기준은 누가 양질의 하드웨어 자원을 제공하느냐에 있는 것이 아니라는 것이다. 대신, 왼쪽의 BP인 Huobi 는 거래소를 운영하는 주체로 이미 다수의 사람들에게 알려져 있다는 점을 감안 하면 마케팅 측면, 즉 BP의 인지도가 BP 선출에 큰 영향을 미치는 것을 추론할 수 있다. 

둘째로, 투표 참여자들의 낮은 투표 횟수는 BP 고착화를 악화 시킨다. 사람들이 매번 투표에 참가할 때 마다 자신들의 최대 투표 가능 횟수인 30번을 전부 사용하게 된다면 상위 21개의 BP 고착화를 어느정도 막을 수 있다. 하지만 현재 개인들의 평균 투표 횟수는 13회에 그치고 있다.



이미 EOS의 리더인 Dan Larimer는, “만약 당신이 최소 15개의 BP에게 투표를 하지 않는다면, 당신은 네트워크를 공격에 취약한 상태로 방치하는 것이다” 라며 투표에 대한 강력한 메시지를 커뮤니티에 전달한 바 있다. 하지만, 이는 활발한 BP투표를 위한 효과적인 방법은 고려치 않으면서 다수의 참여자들에게 네트워크 분산화의 책임을 전가하는 행위로 볼 수 밖에 없다. 투표자들이 번거로움을 감수하면서까지 30개의 변별력 없는 투표 행사를 장기적으로 지속할 이유가 없기 때문이다. 

앞으로 EOS 생태계 내에서 BP의 고착화 현상이 심화 되고 BP의 선출 기준이 ‘하드웨어 역량’이 아닌 다소 모호하고 과장에 취약한 ‘인지도'에 좌우 된다면, 선출된 EOS BP들이 얻는 블록 생성 보상 및 투표 보상은 고스란히 자신의 인지도 향상을 위한 마케팅에 투입 될 공산이 크다. 이렇게 된다면서 공공의 이익을 대변하고 EOS 인프라를 책임지고 운영해야 하는 BP 역할을 제대로 수행할 수 없게 된다는 점은 누구나 예상할 수 있다. 현재 다수의 BP들은 자신들의 로드맵을 통해 미래에 추가해 나갈 하드웨어 스펙을 공개 하였다. 하지만, 현 시점에 그들이 블록을 생성하기 위해 사용하고 있는 상세한 하드웨어 스펙은 찾아보기 힘들다는 점 역시 아이러니하다. 앞으로 EOS 네트워크가 활성화되고 확장됨에 따라 더 큰 권력이 BP들에게 집중 될 것으로 예상된다. 따라서, 자본과 인지도 등의 원인으로 고착화되어 가는 기존의 EOS BP선출 문제점을 해결해야만 진정으로 탈중앙화 된 블록체인 생태계를 만들 수 있다. 다양한 이해관점에서 BP로 출마하고 선출됨으로써 탈중앙화된 블록체인 권력구조를 유지할 수 있는 새로운 BP 선발기준과 방법이 필요하다. 

## Asset Risk Summary

소수의 고래 투자자가 블록 생성자 투표를 좌지우지 할 수 있다. 
보다 공정하고 다양성을 확보할 수 있는 BP 선정 기준이 존재하지 않는다면 시간이 갈 수록 블록 생성자는 변하지 않고 중앙화될 것이다. 

## Voting Risk 1. Low-Voting Turnout

EOS의 첫 번째 투표 리스크는 저조한 투표율이다. 한국 시간 기준 2018년 7월 2일 21시 15분 EOS Mainnet 투표율은 약 17.2%로 집계 되고 있다. EOS의 저조한 투표율은 크게 두 가지 이유를 들어 설명할 수 있다. 

첫 번째 이유는 투표에 대한 대중의 낮은 접근성이다. Scatter라는 비교적 편리한 Voting Tool이 존재 하지만 투표 등록 방식에 대한 번거로움이 완전히 해소 되었다고 볼 수는 없다. 다수의 EOS 보유자들과 접점에 있는 Bitfinex 가상화폐 거래소의 경우, 거래소 내부 가이드라인을 통해 EOS 보유자들에게 투표권을 행사할 수 있도록 조치를 취하고 있다. 하지만, 여전히 등록 절차의 번거로움이 존재하고 거래를 위한 유동 물량 확보를 위해 개인의 EOS 보유분 중 72%만을 투표에 사용할 수 있게 하는 등, 비효율적인 투표 방식을 사용하고 있다. 앞으로 이러한 투표 방식에 대한 접근성 문제는 보다 편리한 투표 시스템을 위한 UI/UX 개발을 통해 반드시 개선되어야 할 것이다. 

투표 방법의 낮은 접근성과 더불어 투표 관련 정보에 대한 낮은 접근성 역시 저조한 투표율의 이유다. 현재, EOS BP들에 대한 포괄적이고 한 눈에 비교 가능한 정보를 제공하는 주체가 존재하지 않는다. EOSwire 혹은 EOS BP Candidate Report를 참고 할 수 있지만 최소한의 기준을 만족하는 BP를 확인할 수 있을 뿐 그 이상의 변별력있는 구분은 제공하지 않고 있다.   
<EOS Wire Block Producer Compliance Report> 

 이 문제를 해결하기 위해 앞서 ‘자산 리스크 2’에서 지적한 BP간 선출 기준 부재 문제를 반드시 해결해야 한다. 결국, 제 아무리 뛰어난 BP 후보가 존재하더라도 현존하는 BP들과 비교 및 대조 되어 대중에게 어필하지 못한다면 BP로 선출 되기 힘들기 때문이다. 따라서, BP들에 대한 공정하고 객관적이며 변별력있는 Rating System이 반드시 필요하다. 

저조한 투표율의 두번째 이유로 개인이 BP 투표에 따르는 모든 간접 비용을 부담해야 한다는 점을 들 수 있다. 

첫째로, 모든 투표자는 원활한 투표를 진행하기 위해 자신의 Private Key 노출에 따르는 보안 부담을 져야 한다.한 예로, 2018년 4월 24일 Ethereum에서 가장 널리 사용되고 있는 Myetherwallet 지갑의 Domain Name Server redirecting (웹사이트로 유입되는 트래픽을 다른 곳으로 돌리는 방법)을 통해 해커는 Private Key를 사용하여 로그인 하는 Ethereum 사용자들의 자산을 갈취하는 사건이 발생하였다.  

 
<EOS 계정 활성화를 위한 Private Key 등록: Scatter>

둘째로, 투표를 진행 하기 위해 3일 동안 자신의 EOS를 Staking해야 하며 개인은 이에 따르는 기회 비용을 감수해야 한다. 기회 비용의 한 가지 예로, 투표의 영향력은 매년마다 반감기를 거치고 매주 영향력이 하락하는 구조이다. 따라서, 개인의 투표 영향력을 최대로 유지하기 위해 투표자들은 이상적으로 매주 투표를 진행 해야 하며, 이는 곧 기회비용의 증가를 의미 한다. 매주 투표를 진행한다고 가정 할 경우 투표를 진행할 때 마다 3일의 Staking기간을 거치게 되기 때문에, 해당 투표자는 매달 15일 정도의 기회 비용을 부담하게 된다. 


<EOS 투표 영향력 반감기 System 코드>

저조한 투표율의 세번째 이유로 투표 행위에 단기적인 동기 부여가 존재하지 않는다는 점을 들 수 있다. EOS 메인넷이 출범하기 전 부터 뜨겁게 논의 되었던 부분은 투표자들에게 투표에 대한 보상을 BP가 제공할 것인가 말 것인가에 대한 것이었다.     결국 EOS.IO 개발을 총괄 담당하는 Block One은 EOS 헌법 초안에서 밝힌 바와 같이 투표에 대한 어떠한 보상도 제공해서는 안된다는 문구를 ‘법제화' 하였다. 이러한 조치는 투표 유치를 위한 BP 간 과당경쟁을 막기 위한 것으로 판단 되지만, 투표자에게는 투표행위에 대한 동기 유인이 존재하지 않는  치명적인 단점을 갖게 된다. 

장기적으로 보았을 때, EOS 보유자들, 즉 투표자들이 좋은 BP를 선택하게 되면 전체 EOS의 가치는 높아지고, 그로 인해 EOS의 가격은 상승하게 된다. 반대로, 나쁜 BP를 선택하게 되면 EOS의 가치가 떨어지게 되어 EOS의 가격은 하락하게 되기 때문에, 투표자들은 좋은 BP를 선출할 유인이 존재한다. 하지만, 이러한 논리의 맹점은 좋은 BP가 선택 되어 네트워크 가치가 상승하게 되면 BP와 투표자 모두 이득을 얻는 구조지만, 나쁜 BP가 선택 되어 네트워크 가치가 떨어지게 되면 투표자들은 EOS 가격 하락으로 인해 BP와 BP후보들보다 더 큰 손해를 보는 구조이다. 왜냐하면, BP와 BP후보들은 EOS 블록체인에 대한 내,외부 평가 및 평판의 결과가 좋거나 나쁨에 관계 없이 지속적인 블록생성 보상 또는 투표 보상을 받기 때문이다. 

모든 EOS 생태계 참여자는 단기적인 유인과 장기적인 유인에 의해 움직이게 된다. 따라서, 각기 다른 이해관계를 가진 EOS 보유자들의 투표율을 제고하기 위해 투표에 대한 단기적 보상 역시 반드시 존재해야 한다.

저조한 투표율은 투표자들의 ‘합리적 무지’에 기인 한다고 볼 수 있다. 합리적 무지는 정보 수집에 드는 비용이 수집된 정보를 활용하여 얻게 되는 이익보다 높을 경우 발생하게 된다. 따라서, 애초에 정보를 수집하려는 수고로움을 회피하는 것이 더욱 합리적인 선택이 된다. 현재 EOS의 저조한 투표율은 투표를 하기 위해 투표자들이 부담하는 비용이 투표를 함으로써 얻게 되는 이익보다 현저히 높기 때문이다. 이를 해결하기 위해서는 BP 투표에 투표자가 부담하는 기회 비용, 보안 비용을 감소 시키거나, 투표자가 투표로부터 얻게 되는 직접적인 이익이 있어야만 적정수준의 투표율을 유지할 수 있을 것이다. 

## Voting Risk 2. Voting Mediators

현재 EOS에는 BP 투표를 중재하는 주체에 대한 리스크가 존재한다. 투표 중재자는 원활한 BP 투표를 위해 BP 후보 관련 정보를 대중에게 제공하는 역할을 수행한다. 투표 중재자의 첫 번째 리스크는, BP 후보가 투표 중재 서비스를 제공하는 경우이다. 투표 중재 서비스는 BP 정보의 공정한 분배를 전제로 진행 되어야 하지만 BP 후보가 투표 중재의 주체가 된다면 이야기는 달라진다. 예를 들어, BP 후보인 Liquideos는 원활한 투표를 위해 자체 투표 도구를 제공하는데 Default 값으로 본인들이 선택되어 있다. 
< Liquideos 투표 도구의 Default 값>

 또 다른 BP 후보이자 거래소를 운영하는 Bitfinex의 경우 자체 투표 도구와 자세한 가이드라인을 제시 하였는데 그들이 제시한 코드 예시 역시 Default 값으로 본인들이 입력되어 있다. 거래소의 경우 자신의 거래소 플랫폼을 사용하는 잠재적 투표자들을 대상으로 영향력을 행사할 방법이 거래소를 운영하지 않는 BP보다 더 많을 수 밖에 없다. 실제로 Bitfinex는 자체 창구를 통해 유입된 투표량(표의 남색 부분)이 자신의 전체 BP 투표량 중 가장 많은 부분을 차지하며, 자체 창구를 통해 유입된 투표는 여타 BP들 보다 Bitfinex를 지원하는 투표량이 가장 많다.  

<Top 21 BP, Bitfinex 투표 툴을 통해 유입된 투표량 비교: 남색 Bar>

이러한 EOS BP 투표 양상이 시사하는 바는 투표의 대상이 되는 주체가 투표 중재를 진행할 경우 투표자의 결정에 유의미한 영향을 미친다는 것이다. 현실 정치에 빗대어 보았을 경우 국회의원 후보자가 자체 투표 창구를 운영하는 것과 비슷한 상황인 것이다. Google Chrome Extension Voting Tool을 제공하는 Scatter를 사용 하더라도, 투표관련 정보를 조회하기 위해서는 다른 투표 중재자 창구를 통해야 한다는 점에서 투표 중재자 리스크로부터 자유롭지 못하다. 

BP가 투표 중재자 역할을 하지 않더라도 여전히 투표 중재자의 리스크가 존재한다. 투표 중재자인 제 3자와 BP간의 이면 계약이 가능하기 때문이다. 각자의 사적 이익을 추구하는 투표 중재자와 BP는 서로의 이익을 극대화 하기 위해 이면 계약을 체결 할 수 있다. 앞서 설명한 자산 리스크의 고래 투자자와 BP간 이면 계약 가능성은 고래 투자자의 투표를 유치하기 위한 직접적인 방법이었다면, 제 3자와 BP간의 이면 계약은 불특정 다수의 투표를 유치하기 위한 간접적인 방법으로 볼 수 있다. BP 후보들의 금전적 보상은 자신들이 받은 투표의 양에 비례한다. 따라서, 모든 BP들 및 BP 후보들은 더 많은 양의 투표 유치를 목표로 한다는 전제가 성립한다면, 중재자 리스크를 포함한 다양한 종류의 이면 계약 리스크가 충분히 존재할 수 있다. 

## Voting Risk Summary

저조한 투표율은 BP 투표자들이 얻는 이익이 BP 투표를 함으로써 부담해야 하는 비용보다 낮기 때문이다.?? 
투표 중재자와 투표를 받는 주체간의 명확하지 않은 이해 관계 

## Structural Risk 1. A Number of Block Producers

EOS의 메인넷 런칭 이래 다시 대두되고 있는 문제는 21개로 정해진 BP의 수 이다. 2018년 7월 기준 시가총액 8조 7천억원에 육박하는 이 방대한 네트워크 운영 권한을 왜 굳이 21개의  주체에게만 부여하는 것일까? 이 부분에 대해 Block.one의 CTO, Dan Larimer는 기술적인 근거가 아닌, 그의 과거 프로젝트인 Bitshares와 Steemit을 통해  얻은 경험적 통찰을 바탕으로 21개의 BP가 가장 효율적인 네트워크 퍼포먼스를 보였다고 말한다. 그는 EOS의 전신이 되는 Bitshares 2.0 출범 당시(2015년) BP의 역할을 수행하는 Bitshares의 Witnesses의 수는 101명에서 17명으로 줄일 것을 제안하였는데, 그 이유는 다음과 같다:

17명으로 줄이게 될 경우 한 달 네트워크 유지 비용을 $5,100으로 줄일 수 있다. (101개의 Witness를 유지하는 비용은 $30,000 정도 든다.)
투표자들이 이성적으로 판단하기에 적절한 수이다. 
정치적,지리적 다양성을 확보하기에 충분한 수이다. 
(2015년 9월 기준)https://www.blockchain.com/pools 에 나타나는 비트코인 채굴 풀 갯수보다 크다. 
(2015년 9월 기준)리플 네트워크의 Validators의 수와 비슷하다. 

그러면서도, EOS는 투표자들의 의중에 따라 더 많은 BP를 둘 수도, 더 적은 BP를 둘 수도 있음을 주장한다. 심지어, EOS 사용자 중 몇몇은 네트워크가 확장됨에 따라 BP의 수가 50개, 또는 100개로 늘어날 수 있다고 막연히 생각하는 경우도 더러 있다. 하지만, 추후 BP 수가 늘어나게 되는 것은 현실적으로 거의 불가능하다. 그 이유는 다음과 같다:

첫 째로, BP의 수가 늘어나게 되면 네트워크의 속도가 저하된다. EOS는 거래의 완결성을 보장하여 체인 분기를 막기 위해 DPoS Byzantine Fault Tolerance 합의 알고리즘을 사용하고 있다. DPoS BFT 방식은 거래의 완결성을 보장하기 위해 최소 ⅔ + 1의 BP들의 동의를 얻어야 하는데, BP의 수가 늘어나면 늘어날 수록 네트워크 Throughput이 줄어 드는 특징을 갖고 있다. 

<매년 새로 발행되는 EOS 분배 계획>

둘 째로, 기존 BP들은 21개의 BP 수를 유지할 유인이 크다. 21개의 BP로 운영되던 네트워크가 42개의 BP로 운영이 된다면 네트워크를 유지하기 위해 2배의 금전적 비용이 든다. EOS 블록체인은 매년 5%에 해당하는 새로운 EOS 를 생성하고 이 중 1%에 해당하는 EOS을 BP와 BP 후보자들에게 제공한다. 이 중 0.25%는 ‘블록 생성 보상’으로 선출된 BP에게만 주어지는데, BP의 수가 두 배로 늘어나게 되면 0.25% 의 블록 생성 보상은 반으로 줄어드는 셈이다. 따라서, 기존의 BP들은 자신들의 보상이 추가 BP 유입으로 인해 희석되는 것을 막고자 할 것이며, 이로 인해 BP간 정치적 분쟁 양상이 조장 될 가능성이 존재한다. 

기존 BP의 반대와 BFT의 기술적 특성을 고려할 경우, 앞으로, EOS 네트워크 BP의 수는 쉽게 변하지 않을 것으로 보인다. 따라서, EOS의 구조적 리스크는 앞서 설명한 자산 리스크 2의 ‘BP의 고착화’ 문제로 귀결되며, 추후 어떠한 소수 집단에 의한 네트워크 장악을 막기 위해 보다 더 현실적인 네트워크의 분산화 전략을 수립해야 할 것이다. 

## Structural Risk Summary

EOS 구조적 특성 상 초기 21개로 운영되는 BP의 수는 쉽게 변하지 않을 것이다. 

## Summary of Problems in EOS

<EOS 중앙화 Simulation>
<EOS 중앙화 사이클> 
지금까지 현재 EOS가 직면한 자산 리스크, 투표 리스크, 구조적 리스크에 대해 알아 보았다. 자산 리스크로 고래 투자자 문제와 BP의 고착화 문제, 투표 리스크로 저조한 투표율과 투표 중재자 문제, 그리고 구조적 리스크로 21명의 BP문제에 대해 살펴 보았다. 주목해야할 점은 자산, 투표, 구조적 리스크 모두 EOS 생태계 내의 영향력이 소수에게 집중 될 위험을 내포하고 있다는 것이다. 소수의 고래 투자자들에 의한 BP 투표 시스템 장악, 메인넷 초기에 선출된 BP들의 영향력 집중, 저조한 투표 참여율에 기인한 고래 투자자의 영향력 증가, 변별력 없는 BP 투표 기준이 가능케 한 투표 중재자의 영향력 증가, 생태계가 커지면 커질 수록 영향력이 더욱 집중되는 21개의 BP 구조는 전부 EOS의 ‘중앙화' 위험 을 경고하고 있다. 

1. 블록 생성자 투표에 대한 고래 투자자의 영향력 증가 
2. 장기적으로 심화되는 블록 생성자 고착화 문제
3. 상대적으로 높은 BP 투표 비용과 낮은 BP 투표 이익
4. 투표 중재 주체와 투표를 받는 주체의 이해 상충 문제
5. 21개로 고정된 수의 BP 문제

# The Proposal: EOS CHROME

## Solutions
소수의 코인 보유자가 BP 선출에 지배적인 영향력을 행사하는 것을 막기 위해 돈의 가치와 블록체인 서비스 기능적 가치를 분리해야 한다. 현재 EOS는 이 두 가지의 가치가 합쳐져 있는 구조이다. 따라서, 더 많은 돈을 가진 사람이 네트워크에 더 많은 영향력을 행사할 수 있게 된다. 돈의 가치와 기능적 가치가 분리 된다면 아무리 많은 돈을 가지고 네트워크에 참여하여도 실제 네트워크에서 제공하는 기능을 사용하지 않는 한 네트워크 내에 영향력은 제한된다. 

유동적인 BP 선출 구조를 가져야 한다. BP 선출 구조는 first come first serve (first occupy)로 진행 되어서는 안된다. 이를 해결하기 위해 BP 의 마케팅 파워와 변별력 없는 하드웨어 역량 외의 명확한 BP 선출 기준이 필요하다. 특히 다양한 투표자들의 이해관계를 유지시키면서 투표에 그 결과를 반영시키는 것이 필요하다. EOS Chrome에서는 BP가 제공하는 서비스 가치의 다양성이 투표에 반영될 수 있는 시스템 마련에 중점을 두고 있다.  

BP 투표자들이 투표를 통해 얻는 이익이 투표를 하기 위해 부담하는 비용보다 높아야 한다. 이를 위해 투표에 대한 보상이 존재해야 한다. 단, 돈의 가치와 기능적 가치가 분리 되는 구조 하에 투표에 대한 보상은 굳이 돈이 아니어도 된다. 대신, 사람들이 직접적으로 기능적 가치를 얻을 수 있는 네트워크 내 ‘기능(서비스) 보상’을 제공할 수 있다. 

변별력있는 BP 투표 기준의 존재해야 한다. 보다 명확한 투표 기준이 확립 된다면 BP간 변별력 없는 모호한 정보를 바탕으로 영향력을 행사하는 중재 주체가 존재할 유인이 없어진다. 대신, 누구든 확실한 BP 선출 기준으로 정형화되고 객관화된 정보를 제공하게 된다면 보다 공정한 BP 중재 생태계가 형성될 수 있을 것이다. 

<EOS 중앙화 70-Weeks Simulation>
<EOS Chrome 탈중앙화 70-Weeks Simulation>구조적으로 보다 신축적인 숫자의 BP 운영 방법이 강구되어야 한다. 다양한 플랫폼 간 BP의 이동이 가능한 연구가 필요하다. 

# EOS CHROME: Burn and Earn Delegated Proof of Stake (B&E DPoS)

EOS CHROME은 새로운 합의 알고리즘인 B&E DPoS를 사용한다. 위에서 설명한 EOS의 단점을 보강하기 위한 B&E DPoS는 세 가지 특징을 갖는다:

1. 자본과 기능의 분리 
2. BP와 Dapp의 연동
3. Burn & Earn

## Separation of Asset and Utility

<자본(EOS CHROME)과 기능(Chromite)의 분리>

EOS CHROME의 가장 큰 특징은 자본의 역할을 하는 EOS CHROME 코인 (CR) 과 기능적 역할을 수행하는 Chromite 코인 (CRM)의 분리이다. EOS CHROME의 ICO 참여자들은 ERC-20 기반의 EOS CHROME 코인을 받게 되며 추후 메인넷 런칭 이후 자체 EOS CHROME 블록체인 기반 CR 코인을 1:1 비율로 교환 가능하다. CR 코인의 가장 큰 특징은 최소 1,000 TPS의 속도로 거래 수수료 없이 p2p 전송이 가능하다는 것이다. CR 코인은 외부 거래소에 상장 되어 다양한 법정 통화 및 가상 화폐와 교환 가능하며, EOS CHROME 생태계 내에서 결제 수단으로 사용 된다. Chromite (CRM) 코인은 생태계 내에서 실제 B&E DPoS의 기능적인 부분을 수행한다. CRM 코인의 주 기능으로 BP 투표와 Dapp Coin 보상을 들 수 있다. 

생태계 내 자본의 역할을 수행하는 코인과 기능적 역할을 수행하는 코인의 분리를 통해 고래 투자자의 투기성 행동을 억제하는 효과를 얻을 수 있다. 아무리 많은 EOS CHROME 코인을 보유한 고래 투자자라 할 지라도 그의 투기성 행동은 외부 거래소의 가격 변동 외에 EOS CHROME 생태계 내부의 기능적 요소인 BP 투표 및 Dapp Coin 보상 수취에 직접적인 영향을 줄 수 없다. 투자자는 반드시 내부 거래소에서 시장의 힘으로 정해지는 교환 비율에 따라 EOS CHROME을 Chromite로 교환하여 BP Voting 및 Dapp Coin 보상을 얻을 수 있다. 

## Combining Block Producers and dApp

<Block Producer와 Dapp의 연동>

EOS CHROME B&E DPoS의 또 다른 특징은 모든 BP, 혹은 BP 후보들과 Dapp이 연동 된다는 점이다. BP가 직접 Dapp을 출시 할 수도 있고 기존의 유망한 Dapp을 선별하여 Partnership을 체결하는 방식으로 연동 가능하다. BP와 Dapp의 연동은 서비스 중심의 블록체인 생태계 구현에 매우 효과적인데, 이러한 구조의 장점은 다음과 같다: 

변별력 있는 BP 선별 기준 확립 
양질의 Dapp 서비스 개발 생태계 조성
역동적인 BP 선출 구조
첫째로, BP와 Dapp 서비스 간 연동을 통해 변별력 있는 BP 선별 기준을 확립할 수 있다. 기존 EOS의 하드웨어 기반 BP 선출 기준과 더불어 특정 BP가 제공하는 Dapp 서비스의 종류와 서비스 내용은 BP 투표자로 하여금 보다 변별력 있는 기준으로 해당 BP를 판단할 수 있게 한다. 이는, BP 투표자들이 EOS CHROME 블록체인 생태계 전반에 유익한 서비스를 제공하는 Dapp과 연동 되어 있는 BP를 별반 효용 없는 Dapp과 연동되어 있는 BP들 보다 더 매력적인 BP 투표 대상으로 판단할 수 있게 한다. 


<EOS CHROME BP 투표> 


둘째로, BP와 Dapp 서비스 간 연동은 장기적으로 양질의 Dapp 서비스 개발 생태계를 조성할 수 있다. BP 투표자들은 BP를 투표하기에 앞서 특정 BP가 제공하는 Dapp 서비스의 내용과 가능성을 판단하게 된다. 따라서, 훌륭한 Dapp 서비스를 제공하는 BP 후보는 BP로 선발될 가능성이 매우 높으며 BP로 선발 되면 BP 보상을 지속적인 Dapp 서비스 개발 및 개선에 재 투자할 유인이 매우 크다.

<BP 보상과 재투자>셋째로, BP와 Dapp 서비스 간 연동은 보다 역동적인 BP 선출 구조를 가능케 한다. 기존의 EOS BP 고착화 문제의 맹점은 네트워크 초창기에 BP 자리를 선점한 상위 BP의 순위가 바뀌지 않는다는 것이었다. 하지만 블록체인 네트워크의 발전 방향에 따라 BP 선출 또한 역동적인 구조를 가질 필요가 있다. BP와 Dapp의 서비스 간 연동은 특정 BP 후보의 마케팅 역량과 하드웨어 역량이 상위 BP 보다 열등하다 하여도 새롭고 창의적인 Dapp 로서비스로  투표자들의 관심을 끌 수 있다. 특정 BP 후보가 BP로 선출되지 못해도, 그들은 투표 보상을 수령하여 Dapp 개발을 지원할 수 있다. 

## Burn and Earn
EOS CHROME B&E DPoS의 핵심 개념인 Burn & Earn은 BP 투표를 통해 Dapp Coin 보상을 얻는 구조이다. 생태계 참여자들은 EOS CHROME 내 기능적 역할을 수행하는 Chromite 코인을 소각하여 BP 투표 권한을 얻을 수 있으며, BP 투표 권한을 행사하여 Dapp Coin 보상을 받게 된다. 투표자가 Chromite 코인을 소각하게 되면 30개의 다른 BP에게 투표 할 수 있는 권한이 부여 된다. 이후, 투표자는 자신이 원하는 Dapp 서비스와 연동 되어있는 BP를 투표 할 수 있으며 투표와 동시에 해당 BP가 제공하는  Dapp Coin을 보상으로 받을 수 있다. EOS CHROME의 독특한 Burn & Earn의 특징은 다음과 같다: 
고래 투자자의 생태계 영향력 집중 해소 
BP 투표에 대한 보상 제공 
BP 투표율 제고 


< Burn & Earn>


첫째로, Burn & Earn을 통해 생태계 내 고래 투자자의 영향력 집중을 해소 할 수 있다. 앞서, EOS의 자산 리스크 1: 고래 투자자 리스크에서 설명한 바와 같이, 현 EOS 생태계 내 BP 투표에 대한 고래 투자자의 영향력은 거의 절대적이다. 그들의 선택에 따라 BP 선출이 좌지우지되는 상황이 연출 되기 매우 쉬운 구조이며, 이러한 고래 투자자의 영향력은 이면 계약의 위험성을 내포하고 있다. 하지만, EOS CHROME의 Burn & Earn은 모든 참여자로 하여금 BP 투표를 진행하기 위해 자신의 Chromite 코인을 Burn, 즉 소각해야 한다. Chromite 코인을 소각하면 BP 투표권을 갖게 되지만 BP 투표권을 다시 Chromite 코인으로 교환할 수 없다. 때문에, 고래 투자자, 개미 투자자를 막론하고 모든 생태계 참여자는 자신의 BP 투표권 행사를 매우 신중히 진행해야 할 필요가 있다. 

둘째로, Burn & Earn은 BP 투표에 대한 보상을 제공한다. EOS CHROME에서 BP 투표에 참여하기 위해 Chromite 코인을 소각해야 하지만 1개의 Chromite 코인 소각을 통해 30 개의 다른 BP에게 투표를 할 수 있는 권한이 주어진다. 투표자는 30개의 투표 권한으로 자신이 원하는 Dapp 서비스를 제공하는 BP를 투표 할 수 있고, 투표를 진행함과 동시에  Dapp Coin을 보상으로 얻을 수 있다. 현재 EOS 역시 1 EOS 마다 30개의 투표 권한을 갖지만, 투표자들이 투표를 통해 얻을 수 있는 보상이 존재하지 않기 때문에 평균 13개의 투표 권한만 행사 하고 있는 실정이다. 투표자들의 낮은 투표 횟수는 자산 리스크 2: BP 고착화에서 언급한 바와 같이, BP 고착화를 심화시키는 주된 요인으로 작용 한다. 따라서, 네트워크의 적절한 분산화를 위해 모든 BP 투표자가 자신이 보유한 모든 BP 투표 권한을 반드시 행사할 수 있어야 한다. EOS CHROME의 Burn & Earn은 투표자들에게 Dapp Coin 보상을 제공함으로써 이러한 문제를 해결할 수 있다. 

셋째로, Burn & Earn은 BP 투표율을 높일 수 있다. Delegated Proof of Stake 합의 알고리즘이 네트워크 분산화를 달성하기 위해 반드시 필요한 것은 생태계 참여자들의 BP 투표 참여이다. 비록 블록을 생성하는 주체는 선발된 몇몇의 BP들이지만, 이들을 지지하고 감시하는 역할을 하는 주체는 투표자들이다. 따라서, 투표율이 낮다면, 네트워크를 지지하고 감시하는 수의 사람이 적다는 것을 의미하며, 이는 곧 BP들과 고래 투자자들의 네트워크 장악력을 높이는 결과를 낳게 된다. EOS CHROME의 Burn & Earn은 위 문제를 투표에 대한 보상을 제공함으로써 근본적으로 해결할 수 있다. 다른 이해 관계를 갖고 있는 다수의 BP 투표자들로 하여금 자신들의 투표 권한 행사가 Dapp Coin 보상으로 이어 진다면 자연스럽게 BP 투표율을 높일 수 있을 것이다. 

# Inter Contract Communication (ICC) 
EOS CHROME 생태계 설계에 있어서 반드시 풀어야 할 숙제는 실 생활에 적용 가능한 기술의 구현이다. 이는 보편적인 솔루션 제공을 위한 기존 블록체인 플랫폼 설계와 사뭇 다른 접근으로, 스마트 컨트랙트, dAPP, 사용자 UX 등의 복합적인 구조와 서비스에 대한 이해를 바탕으로 실 서비스의 구현을 목표로 하고 있다. EOS CHROME 생태계는 Dapp 서비스와 인간의 상호 관계가 존재하는 범주에 실용적인 서비스 구현을 궁극적인 목표로 제시한다. 따라서 EOS CHROME 생태계 참여자들은 inter-contract communication 즉, 자율 검증 컨트랙트를 통해 기존 스마트 컨트랙트 개념을 좀 더 심화하여 실 생활 적용 범위를 대폭 확장 할 수 있다. 

## Limitations of Smart Contract 
‘Disruption Hub’에 따르면 2018년 3월 기준 다양한 블록체인 네트워크 상에 적용될 수 있는 스마트 컨트랙트의 종류는 다음과 같다: 1. 보험. 2. 상품 생산 관리 3. 주택 담보 대출 4. 고용 계약 5. 저작권. 하지만 이러한 분류는 스마트 컨트랙트의 모든 이론적 가능성을 감안하였을 경우이며 현재 적용 가능한 부분은 매우 한정적이다. 2번 상품 생산 관리의 경우 Private 블록체인 네트워크 내에서 대부분의 기술적 구현이 가능하며 이를 제외한 1,3,4,5번의 스마트 컨트랙트 적용 사례는 ‘특정 계약 조건에 따른 자동 자금 집행’으로 모든 내용이 함축 된다. 실제로 대부분의 스마트 컨트랙트 적용 분야는 토큰 및 코인 거래와 같은 자금 거래와 이와 관련된 ESCROW 기능의 수행에 국한되어 있다.

## IoT vs. ICC


< IoT vs. ICC>

사물 인터넷이란 인간이 아닌 사물들이 인터넷을 통해 상호 연결될 수 있는 환경을 말한다. 예를 들어, 집 전체가 사물 인터넷으로 연결 되어있을 경우 매일 정해진 시간에 로봇 청소기가 청소를 시작하고, 청소를 시작함과 동시에 창문이 열려서 환기를 시키며, 환풍기가 저절로 돌아가는 환경을 상상해 볼 수 있다. 

하지만, 사물 인터넷 기술의 보급이 더딜 수 밖에 없었던 큰 이유 중 하나는 바로 보안 문제이다. 실제로 사물 인터넷 환경이 구축된 아파트 네트워크에 해커가 침입을 하여 한 여름날 에어컨을 사용하지 못하게 하는 피해 사례가 발생하기도 했다. 

IoT 생태계 구현에 있어서 또 다른 문제점은 바로 중앙화 된 단일 플랫폼 사업자 문제이다. 특정 IoT 플랫폼을 사용하는 기계는 다른 IoT 플랫폼과 쉽게 연동되지 않는다는 치명적인 단점이 존재한다. 자사의 제품 간 사물 인터넷 구현을 위해 설계된 IoT 플랫폼은 자연히 타사의 제품과의 연동에 배타적인 입장을 취할 수 밖에 없다. 예를 들어, 각기 다른 중앙화 플랫폼을 사용하는 Apple TV, Samsung 핸드폰, Xiao Mi 로봇 청소기의 경우 단일 플랫폼 기반의 IoT 생태계 구현에 있어서 많은 제약이 존재한다. 

반면, EOS CHROME ICC는 기존 IoT 적용에 있어서 문제되는 보안 문제와 단일 플랫폼 문제를 해결할 수 있다. 첫째로, EOS CHROME의 ICC 기술은 보안에 탁월한 분산장부 시스템인 블록체인 기술을 기반으로 구현된다. EOS CHROME의 BP들은 DPoS BFT 기반의 합의 알고리즘으로 매우 빠른 속도로 거래의 완결성을 보장하며 네트워크 공격자는 이미 발생한 거래를 조작하기 위해 천문학적인 금전적 비용을 부담해야 하는 구조를 갖고 있다. 

둘째로, ICC는 단일 플랫폼 문제를 해결할 수 있다. 블록체인 기술의 혁신은 제 3자의 개입 없이 신뢰 할 수 없는 불특정 다수와 거래를 가능케 했다는 점이다. 생태계 참여자들은 각자 다른 이해 관계를 가지고 네트워크에 참여 하며, 개인의 효용을 극대화 하기 위해 게임 이론과 경제학 유인 체계에 부합하는 행동을 하게 된다. 예를 들어, 생태계 참여자는 ICC 기술을 사용하여 자신에게 유익한 서비스를 제공하는 Dapp 간 정보 공유 및 권한 부여와 같은 기능을 적극 활용할 수 있다. 추후 inter-chain communication 기술 개발을 통해 다른 블록체인 네트워크와 교류 가능한 ICC 기술 구현이 가능해 질 것이다. 

## Inter Contract Communication

<EOS CHROME Inter Contract Communication>

EOS CHROME의 Inter Contract Communication는 기존 스마트 컨트랙트의 ‘자금 집행’을 뛰어 넘어 스마트 컨트랙트 간 상호 연동을 통해 특정 ‘권한’에 대한 접근 및 차단을 가능케 한다. 특정 단체 혹은 주체가 스마트 컨트랙트를 구현하고 제공함으로써 블록체인 내에서의 상호작용을 가능하게 함은 서비스의 필요에 따라 다양한 서비스의 제공이 가능한 환경을 제공할 수 있다. 특히 특정 주체에게 권한 부여가 가능하다는 것은 스마트 컨트랙트 기술을 통해 필요에 의한 정보의 제공이 가능하며, 개인정보 등에 민감한 서비스 제공에 적합하다. 뿐만 아니라, 정보를 제공하는 다양한 주체들의 이해관계를 충분히 스마트 컨트랙트로 구현이 가능하기 때문에 정보 제공자 뿐만 아니라, 제공자들과 관계된 이해관계자들간 다양한 수익 협력모델을 만들어 낼 수도 있다. 

# EOS CHROME Summary 
현재 EOS가 직면한 ‘생태계 내 영향력 집중’ 문제를 해결하기 위해 IBCT HK는 EOS CHROME 을 제안 한다. 
EOS CHROME은 Burn & Earn DPoS 합의 알고리즘을 사용 한다. 
B&E DPoS는 크게 세 가지 특징을 갖는다:
자본과 기능의 분리를 통해 투기 세력의 네트워크 장악을 제한 할 수 있다. 
BP와 Dapp의 연동하여 변별력 있는 BP 선별 기준을 확립하고, 선순환 Dapp 서비스 개발 생태계를 조성하며 역동적인 BP 선출 구조를 가질 수 있다. 
Burn & Earn을 통해 고래 투자자의 생태계 영향력 집중을 분산시키고, BP 투표에 대한 보상을 제공하여 네트워크 전반의 BP 투표율을 상승 시킨다. 
Inter Contract Communication 기술을 개발하여 단일 플랫폼 서비스의 한계를 극복하고 블록체인 기술과 스마트 컨트랙트의 장점을 극대화 한다. 

# Conclusion

탈중앙화는 절대로 포기해선 안되는 블록체인 기술의 매우 중요한 철학적 가치이자 이상이다. 결국 가상화폐가 전 세계 사람들을 열광시킨 이유도 블록체인 기술을 통해 개인자산에 대한 인정을 매개자 없이 구현한 것 때문이라고 볼 수 있다. EOS Chrome은 EOS가 가지고 있는 확장성의 장점을 유지하면서도 EOS의 BP와 투표시스템의 탈중앙 훼손을 극복할 수 있다. 나아가 EOS CHROME은 비탈릭 뷰테린이 언급한 블록체인 트릴레마 문제를 해결할 수 있는 새로운 블록체인 플랫폼의 기준을 제시하고자 한다. 

# Roadmap

## Research and Development (~2019)
EOS CHROME Private 테스트 넷 개발 완료
B&E DPoS POC 완료 및 시연
중국 내 EOS CHROME BP Testbed 구축 
개발 커뮤니티 등 기반조성(~2019년 상반기) 
EOS CHROME 글로벌 개발 커뮤니티 조성 
BP/Dapp 커뮤니티 조성 및 해커톤 개최
EOS CHROME 글로벌 Tech meet-up 개최
