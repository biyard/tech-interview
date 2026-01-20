## Comparison of Bitcoin and Ethereum ... and BTCFI(Babylon)


### Basics   

1. Blockchain은 무엇일까? :  State + Network

## Core Components of Blockchain network 

1.    State
2.    Transaction
3.    Block   
4.    Script/VM 
5.    Consensus Mechanism 
6.    Finality

Lastly BTCFI   

## State 


### CS에서의 state란? 

‘state‘는 특정 시점에서 시스템이 가지고 있는 정보의 집합을 말합니다. 이 정보는 프로그램의 변수 값, 사용자 인터페이스의 상태, 메모리의 내용 등 다양한 형태를 가질 수 있습니다.

<img src="https://github.com/user-attachments/assets/f971a784-d8f1-42dc-99cc-b483c65f6945" width="60%" alt="Image">

### Bitcoin의 State
**UTXO = Unspent Transaction Output**  
비트코인의 State란 네트워크에 존재하는 UTXO들의 전체 집합

<img src="https://github.com/user-attachments/assets/e8dd23bf-63ef-4871-954e-763420ae6108" width="60%" alt="Bitcoin UTXO Model">

### Ethereum의 State
이더리움의 State란 네트워크에 존재하는 모든 Account의 State의 집합입니다.
EOA(Externally Owned Account), CA(Contract Account)로 구분합니다. 

<img src="https://github.com/user-attachments/assets/de1413e0-25e6-4ca6-a57e-e283a20428b7" width="60%" alt="Ethereum Account Model">

## Transaction 


### transaction이란? 

블록체인에서 'transaction'은 데이터베이스의 상태를 변화시키는 작업의 모음입니다. 

### Bitcoin의 Transaction 

UTXO(Unspent Transaction Output)를 input으로 받아서 새로운 UTXO를 output으로 생성합니다. 비트코인의 거래는 이전 거래의 미사용 출력을 소비하고 새로운 출력을 생성하는 방식으로 작동합니다.

<img src="https://github.com/user-attachments/assets/d4a9f5ed-0f18-4626-ae2f-2c7be8c17046" width="60%" alt="Bitcoin Transaction Model">

#### Transaction 구조:
- **입력(Input)**: 이전 트랜잭션의 UTXO를 참조하며, 해당 UTXO를 소비할 권한이 있음을 증명하는 서명을 포함
- **출력(Output)**: 새로운 UTXO를 생성하며, 금액과 소유자의 공개키 해시(주소)를 포함
- **서명(Signature)**: 트랜잭션 소유권 및 유효성 검증을 위한 암호화 서명
- **locktime**: 트랜잭션이 블록체인에 포함될 수 있는 가장 빠른 시간을 지정하는 값

### Ethereum의 Transaction 

이더리움의 트랜잭션은 EOA(Externally Owned Account)에서 암호화 서명된 명령입니다. 계정 기반 모델을 사용하여 계정 상태를 직접 변경합니다.

<img src="https://github.com/user-attachments/assets/d06a40b6-325f-42e6-8401-6bf37a4c125f" width="50%" alt="Ethereum Transaction Model">

#### Transaction 구조:

- **from**: 트랜잭션을 서명할 발신자의 주소입니다. 컨트랙트 계정(CA)은 트랜잭션을 보낼 수 없으므로 반드시 EOA여야 합니다.
- **to**: 수신 주소입니다. EOA일 경우 단순 가치 전송, CA일 경우 스마트 컨트랙트 코드 실행을 의미합니다.
- **signature**: 발신자의 개인 키로 생성된 트랜잭션 승인 서명으로, 트랜잭션의 진위성을 증명합니다.
- **nonce**: 계정에서 발생한 트랜잭션 수를 나타내는 순차적 카운터로, 이중 지불을 방지하고 트랜잭션 순서를 보장합니다.
- **value**: 발신자에서 수신자로 전송할 ETH의 양(wei 단위, 1ETH = 10^18 wei)입니다.
- **input data**: 스마트 컨트랙트 함수 호출 및 파라미터 등을 포함할 수 있는 선택적 데이터 필드입니다.
- **gasLimit**: 트랜잭션 실행에 사용할 수 있는 최대 가스 양으로, 초과 시 트랜잭션이 실패합니다.
- **maxPriorityFeePerGas**: 검증자에게 지급할 팁(우선순위 수수료)의 최대 가격입니다.
- **maxFeePerGas**: 트랜잭션에 지불할 의사가 있는 단위 가스당 최대 수수료로, 기본 수수료와 우선순위 수수료를 모두 포함합니다.

## Block 


### Block이란?  

블록체인의 "블록"은 블록체인 기술의 핵심 요소로, 여러 트랜잭션의 데이터를 하나로 묶은 데이터 단위입니다. 

블록체인의 각 블록은 다음과 같은 구조를 가집니다:

트랜잭션 데이터: 블록에 저장된 거래 정보(예: 송신자, 수신자, 금액 등).
블록 헤더:
이전 블록의 해시 값: 이전 블록의 고유한 암호화 값(해시).
현재 블록의 해시 값: 현재 블록의 트랜잭션 데이터와 헤더 정보를 기반으로 생성된 고유한 암호화 값.

블록체인에서는 이전 블록의 해시 값을 현재 블록에 포함하게 하여 체인의 구조를 만들도록 설계되었습니다. 

![image](https://github.com/user-attachments/assets/b14ae95d-14a4-43e0-8e1e-b63b077d8d32)


이전 블록의 해시 값을 현재 블록이 의존하는만큼 한번 블록에 들어가 체인이 형성된 블록을 바꾸는 것을 거의 불가능에 가깝게 만듭니다. 

---






## Script/EVM

여기까지만 보면 단순합니다. 하지만 비트코인과 이더리움은 각각 script와 VM을 통해 보다 복잡한 작업을 수행 가능하게 합니다.

### Bitcoin Script

비트코인은 Script라는 간단한 스택 기반 프로그래밍 언어를 사용합니다. 이는 의도적으로 튜링 불완전(Turing incomplete)하게 설계되어 있어 복잡한 루프나 조건문을 지원하지 않습니다.

#### 주요 특징:
- **스택 기반**: 데이터는 스택에 푸시되고 연산자가 스택에서 데이터를 가져와 처리합니다.
- **간단한 명령어 세트**: OP_DUP, OP_HASH160, OP_EQUALVERIFY 등 약 100개 정도의 명령어를 제공합니다.
- **제한된 기능성**: 무한 루프를 방지하기 위해 의도적으로 제한된 기능을 제공합니다.
- **주요 용도**: 주로 트랜잭션 출력의 잠금 및 해제 조건을 정의하는 데 사용됩니다.

#### 사용 사례:
- P2PKH (Pay to Public Key Hash): 가장 일반적인 트랜잭션 유형으로, 공개키 해시에 대한 지불을 구현합니다.
- P2SH (Pay to Script Hash): 더 복잡한 스크립트를 해시로 참조하여 사용합니다.
- 멀티시그(Multisig): 여러 서명이 필요한 트랜잭션을 구현합니다.
- 타임락(Timelock): 특정 시간이 지나야 사용할 수 있는 자금을 구현합니다.

<img width="394" alt="Image" src="https://github.com/user-attachments/assets/e1724dad-8cac-4766-97f8-e27eefe0d5d4">

<img width="510" alt="Image" src="https://github.com/user-attachments/assets/322011b7-6937-4538-811a-cbc8845201e0" />


### Ethereum Virtual Machine (EVM)

이더리움은 완전한 튜링 완전(Turing complete) 가상 머신인 EVM을 제공하여 복잡한 스마트 컨트랙트 실행을 가능하게 합니다.

#### 주요 특징:
- **스택 기반 가상 머신**: 256비트 워드 크기를 사용하는 스택 기반 아키텍처입니다.
- **튜링 완전성**: 무한 루프와 같은 복잡한 연산을 지원하며, 가스(Gas) 시스템을 통해 실행 비용을 제한합니다.
- **가스 시스템**: 각 연산에는 가스 비용이 할당되어 있어, 무한 루프와 같은 문제를 경제적으로 제한합니다.

EVM을 기반으로 이더리움의 State 데이터에 접근 가능한 Smart Contract라는 Program을 온체인화 시킬 수 있게 되었습니다. 
DAPP 등이 가능한 이유는 EVM이 Turing Complete 하기 때문이고, 이더리움에서 DeFi가 가능하게 해줍니다. 

뒤에 설명할 BTCFI에서 비트코인의 새로운 유틸리티 부여를 위해 왜 튜링 완전한 가상 머신을 갖고 있는 네트워크가 필수인지를 이해할 수 있습니다. 


## Consensus Mechanism

여태까지의 내용은 처음에 언급한 블록체인의 정의인 State + Network 중에서 State와 관련된 부분만 다루었다고 볼 수 있습니다. 
Consensus Mechanism을 통해 블록체인이 탈중앙을 어떻게 달성했는지와 P2P 네트워크가 어떻게 상태에 대한 합의를 이루는지를 이해할 수 있습니다. 

즉, 블록체인의 State + Network의 **Network**를 온전히 이해할 수 있습니다. 

Consensus Mechanism은 네트워크의 참여자(노드)들이 동일한 State에 합의하는 방법입니다. **어떤 블록이 다음 블록으로 체인에 추가될지를 정하는 약속**으로 봐도 무방합니다. 비트코인과 이더리움은 서로 다른 합의 메커니즘을 채택하고 있습니다. 

---

### Bitcoin의 Consensus Mechanism: Proof of Work (PoW)

비트코인은 작업 증명(Proof of Work) 방식을 사용합니다. 이는 네트워크 참여자(채굴자)가 복잡한 수학 문제를 풀어 블록을 생성하는 방식입니다.
블록에 있는 Nonce 값을 조정하면 해시가 다르게 나온다는 점을 이용하여 **특정 수보다 작은 값을 찾는 과정을 반복**합니다.



#### 주요 특징:
- **에너지 집약적**: 많은 컴퓨팅 파워와 전기를 소비합니다.
- **높은 보안성**: 네트워크를 공격하려면 전체 네트워크 해시파워의 51% 이상을 확보해야 합니다.
- **탈중앙화**: 누구나 채굴에 참여할 수 있어 높은 수준의 탈중앙화를 유지합니다.
- **난이도 조정**: 약 2주마다 블록 생성 시간이 10분을 유지하도록 난이도가 자동 조정됩니다.

#### 작동 방식:
1. 채굴자들은 이전 블록 해시, 트랜잭션 데이터, 논스(nonce) 값을 조합하여 해시 함수에 입력합니다.
2. 목표는 특정 조건(예: 특정 수의 선행 0비트)을 만족하는 해시 값을 찾는 것입니다.
3. 유효한 해시를 찾은 채굴자는 새 블록을 네트워크에 전파하고 블록 보상을 받습니다.
4. 다른 노드들은 해당 해시가 조건을 만족하는지 쉽게 검증할 수 있습니다.

![Bitcoin PoW Consensus](https://github.com/user-attachments/assets/bc710d45-aaa6-45a2-b114-406ef77186b4)

---

### Ethereum의 Consensus Mechanism: Proof of Stake (PoS)

### PoS(Proof-of-Stake)

![image](https://github.com/user-attachments/assets/f8a837d1-27a0-41a1-9817-e94b31469f87)




지분 증명(Proof-of-Stake)은 검증자들이 네트워크에 자신의 지분을 예치하여 검증자로서의 자격을 얻고, 부정직하게 행동할 경우 그 지분을 잃을 수 있는 위험을 감수하는 방식입니다. 
이더리움의 지분 증명에서는 검증자들이 ETH를 스마트 계약에 스테이킹합니다. 검증자는 네트워크에 전파되는 새로운 블록이 유효한지 확인하고, 새로운 블록을 생성하여 전파하는 역할을 합니다.
만약 검증자가 네트워크를 속이려 한다면(예를 들어, 한 번에 여러 블록을 제안하거나 상충되는 인증을 보내는 경우), 스테이킹한 ETH의 일부 또는 전부가 몰수될 수 있습니다.


작업 증명(Proof-of-Work)에서는 블록 생성 시점이 채굴 난이도에 따라 결정되지만, 지분 증명(Proof-of-Stake)에서는 일정한 속도로 진행됩니다. 지분 증명 이더리움에서 시간은 slots(12초)과 epochs(32 slots)으로 나뉩니다. 매 slot마다 무작위로 선택된 검증자가 [블록 제안자(Block Proposer)로 선정됩니다. 이 검증자는 새로운 블록을 생성하고 이를 네트워크의 다른 노드들에게 전파합니다.



### Validators

검증자로 참여하기 위해 사용자는 최소한 32 ETH를 deposit contract에 입금하고, 실행 클라이언트 (execution client), 합의 클라이언트 (consensus client), 검증자 클라이언트(validator client)라는 세 가지 소프트웨어를 실행해야 합니다.
활성화된 검증자는 이더리움 네트워크의 다른 peer로부터 새로운 블록을 받습니다. 검증자는 블록에 포함된 트랜잭션을 다시 실행하여 peer로부터 제안된 상태 변경이 유효한지 확인합니다. 새로 제안된 블록이 유효하다고 검증되면, 해당 블록을 지지한다는 투표(인증)를 네트워크에 전파합니다.


![Image](https://github.com/user-attachments/assets/99fe3b25-3fba-4003-80d0-cfe8a071de21)


작업 증명(Proof-of-Work)에서는 블록 생성 시점이 채굴 난이도에 따라 결정되지만, 지분 증명(Proof-of-Stake)에서는 일정한 속도로 진행됩니다. 지분 증명 이더리움에서 시간은 slots(12초)과 epochs(32 slots)으로 나뉩니다. 
매 slot마다 무작위로 선택된 검증자가 블록 제안자(Block Proposer)로 선정됩니다. 이 검증자는 새로운 블록을 생성하고 이를 네트워크의 다른 노드들에게 전파합니다.


![image](https://github.com/user-attachments/assets/fff13c2c-5e14-43e3-b649-64b23f5f085a)

이더리움에서는 매 slot마다 무작위로 선택된 검증자 위원회가 제안된 블록의 유효성을 결정하는 투표를 합니다. 매 epoch마다 검증자들은 slot들에 균등하게 배정되고, 각 slot에서 검증자들은 여러 위원회 중 하나에 속하게 됩니다. 즉, 하나의 epoch에서 각 검증자는 오직 하나의 위원회에만 속할 수 있습니다. 그리고 매 slot마다 해당 slot에 배정된 위원회 중 하나가 랜덤하게 선정되어 제안된 블록을 검증합니다. 예를 들어, 16,384명의 검증자가 있다면 하나의 epoch는 32개의 slot으로 구성되므로 각 slot에는 512명의 검증자가 랜덤하게 배정됩니다. 이 512명의 검증자들은 위원회 최소 인원 기준인 128명에 맞춰 4개의 위원회로 나누어집니다. 이 4개의 위원회 중 랜덤하게 선정된 하나의 위원회가 블록 검증을 합니다. 전체 검증자 집합을 위원회로 나누는 것은 네트워크 부하를 관리 가능한 수준으로 유지하기 위해 중요합니다.


### Block Proposer

Proposer는 새로운 블록을 생성하는 Validator로, Validator 중 한 명이 이 역할을 수행합니다. 지분 증명(Proof of Stake, PoS)에서 블록 생성자는 자신의 지분에 비례한 확률로 새로운 블록을 생성할 권리를 얻습니다. 즉, Validator가 네트워크에 예치한 지분이 많을수록 블록을 제안할 확률이 높아집니다.


![image](https://github.com/user-attachments/assets/875d0da1-7df0-4687-bbe7-b9aa16bc84e8)

## Finality

### Fork 란?

중앙화된 주체가 없는 P2P 네트워크 특성상 노드들이 각기 다른 네트워크의 상태를 주장하는 Fork가 일어날 수 있습니다. 비트코인의 같은 경우 동시에 다른 노드들이 채굴을 하게 된 경우, 혹은 네트워크 지연이나 통신 오류로 인해 Fork가 발생할 수 있습니다.  
이때, 네트워크의 일부는 한 블록을, 다른 부분은 다른 블록을 받아들이면서 잠시 두 개의 체인이 공존하게 됩니다.  
이러한 상황에서는 네트워크가 일시적으로 두 개 이상의 가능한 State를 가지게 되어 블록체인이 분리될 수 있습니다.

---
### Canonical Chain

Fork가 발생했을 때, 블록체인 네트워크는 여러 개의 체인을 가지게 됩니다. 이때, 네트워크는 합의 알고리즘을 통해 **Canonical Chain(정식 체인)**을 선택합니다. 정식 체인은 네트워크에서 유효하고 신뢰할 수 있는 체인으로 간주되는 체인을 의미하며, 네트워크 전체가 이를 따르게 됩니다.

---

### Fork 상태에서 Canonical Chain 선택 과정

#### 1. **Fork 발생**
- 네트워크 지연, 통신 오류, 또는 동시에 여러 블록이 생성되는 경우, 블록체인은 여러 갈래로 분기됩니다.
- 이로 인해 네트워크는 일시적으로 여러 개의 체인을 가지게 됩니다.

#### 2. **Longest Chain Rule**
- 비트코인과 같은 PoW 기반 네트워크에서는 **Longest Chain Rule**을 사용하여 가장 긴 체인을 정식 체인으로 선택합니다.
- 시간이 지남에 따라 한 체인이 더 많은 블록을 추가하며 길어지게 되고, 나머지 체인은 폐기됩니다.

#### 3. **Finality와 Canonical Chain**
- 이더리움과 같은 PoS 기반 네트워크에서는 **Finality** 메커니즘을 통해 정식 체인을 선택합니다.
- 검증자들의 투표를 통해 특정 체인이 정당화되고 최종화되면서, 네트워크는 해당 체인을 Canonical Chain으로 인정합니다.

---

### Canonical Chain의 특징

1. **일관성 보장**
   - 네트워크의 모든 노드가 동일한 체인을 따르도록 보장합니다.
   - 이를 통해 블록체인의 상태가 일관되게 유지됩니다.

2. **변경 불가능성**
   - Canonical Chain으로 선택된 체인의 블록들은 Finality를 통해 변경 불가능한 상태가 됩니다.
   - 이는 네트워크의 신뢰성을 높이는 핵심 요소입니다.

3. **폐기된 체인**
   - Canonical Chain으로 선택되지 않은 체인은 **Orphan Chain(고아 체인)** 또는 **Stale Chain(낡은 체인)** 으로 간주되어 폐기됩니다.
   - 이러한 체인의 블록과 트랜잭션은 네트워크에서 무효화됩니다.



### Bitcoin의 Finality

비트코인에서는 Finality(최종성)가 확률적으로 달성됩니다. 이는 네트워크에서 생성된 블록이 체인에 추가된 후, 해당 블록 위에 더 많은 블록이 쌓일수록 해당 블록이 폐기될 가능성이 낮아지는 것을 의미합니다.

#### **확률적 파이널리티와 Longest Chain Rule**
- 비트코인은 **Longest Chain Rule**을 사용하여 포크가 발생했을 때 가장 긴 체인을 유효한 체인으로 간주합니다.
- 시간이 지나면서 특정 체인이 다른 체인보다 길어지면, 해당 체인이 네트워크의 표준 체인으로 받아들여지고, 다른 체인은 폐기됩니다.
- 따라서, 블록이 체인에 추가된 후 일정 수의 블록이 더 쌓이면, 해당 블록이 최종적으로 변경되지 않을 확률이 높아집니다.

#### **6-Block Confirmation**
- 일반적으로 비트코인 네트워크에서는 하나의 트랜잭션이 안전하다고 간주되기 위해 **6개의 블록 확인(confirmation)** 이 필요합니다.
- 이는 네트워크에서 6개의 블록이 해당 트랜잭션을 포함한 블록 위에 추가되었을 때, 해당 트랜잭션이 변경될 가능성이 거의 없음을 보장합니다.


<img width="170" alt="image" src="https://github.com/user-attachments/assets/18c08fe5-cca7-420f-83b9-89b2dde078d2" />



---

### Ethereum의 Finality

이더리움의 Finality는 비트코인의 확률적 파이널리티와 달리, **결정적 파이널리티(deterministic finality)** 를 제공합니다. 이는 특정 블록이 네트워크에서 최종적으로 확정되었을 때, 해당 블록이 절대 변경되지 않음을 의미합니다.

#### **캐스퍼 프로토콜**
- 이더리움은 **Proof-of-Stake(PoS)** 기반의 **캐스퍼 프로토콜**을 사용하여 Finality를 달성합니다.
- 캐스퍼는 매 32개의 블록(1 에포크)마다 여러 포크 중 하나를 선택하고, 이를 '확정'하는 **체크포인트(checkpoint)**를 생성합니다.

![image](https://github.com/user-attachments/assets/21cd1fe6-1079-4877-8499-a220c7679828)

#### **체크포인트와 검증**
- 네트워크의 검증자들은 각 에포크가 진행되는 동안 투표를 통해 여러 포크 중 하나의 자식 블록을 선택하고 이를 **정당화(Justified)** 합니다.
- 이후, 동일한 경로에서 다음 체크포인트가 네트워크의 66% 이상의 동의를 받으면, 그 이전의 체크포인트는 **최종화(Finalized)** 되어 더 이상 변경할 수 없게 됩니다.

---

### Supermajority Link

**Supermajority Link**는 두 체크포인트 사이에 형성되며, 이는 각각의 체크포인트가 차례대로 전체 스테이킹된 이더리움(ETH)의 3분의 2 이상의 동의를 받을 때 발생합니다.

#### **작동 방식**
1. **첫 번째 체크포인트**는 검증자들의 투표를 통해 정당화됩니다.
2. 두 번째 체크포인트가 66% 이상의 동의를 받으면, 두 체크포인트 사이의 **Supermajority Link**가 형성됩니다.
3. 이 링크가 형성되면, 첫 번째 체크포인트는 **최종화(Finalized)** 상태가 됩니다.

#### **최종화의 의미**
- 최종화된 블록은 더 이상 변경될 수 없습니다.
- 두 체크포인트 사이의 모든 블록도 최종화되며, 해당 블록에 포함된 트랜잭션도 변경 불가능한 상태로 확정됩니다.

---

### Finality의 중요성
- **보안 강화**: 최종화된 블록은 변경될 수 없으므로, 네트워크 공격의 가능성을 줄입니다.
- **사용자 신뢰**: 사용자와 애플리케이션은 최종화된 트랜잭션을 신뢰할 수 있습니다.
- **포크 해결**: 네트워크가 하나의 일관된 체인을 유지하도록 보장합니다.

--- 


## BTCFI(Babylon)

### Introduction to Babylon ### 


BTCFI는 비트코인의 가치와 유틸리티를 확장하기 위한 새로운 금융 생태계입니다. 비트코인은 뛰어난 보안성과 탈중앙화를 제공하지만, 스마트 컨트랙트 기능이 제한적이어서 DeFi(탈중앙화 금융) 애플리케이션을 구축하는 데 한계가 있었습니다. BTCFI는 이러한 한계를 극복하고 비트코인을 현대 금융 시스템에 통합하는 솔루션을 제공합니다.

비트코인의 유동성을 활용하기 위해 다양한 방법이 제시되고 있는데 이 중 Babylon이 제시한 방법을 살펴보겠습니다. 

Babylon은 비트코인의 유동성을 POS체인에 Staking을 하며 활용도를 찾아냈습니다. 


### Bitcoin Staking Problem  ###

비트코인을 다른 POS체인에 Staking을 하기위해서는 두개 중 하나의 방법을 택해야 됩니다. 

1. Bridging to PoS chain.
   -> 비트코인 자산을 bridge 솔루션을 이용하여 wbtc를 pos체인에 올리는 방법입니다. 이 방법의 문제점은 bridge 솔루션 자체의 안정성을 보장하기 힘들다는 것입니다.
      bridge를 하기 위해서는 중앙의 주체를 믿거나 multisig bridge comittee를 이용해야 하는데 둘다 안정성을 보장받기 어렵습니다. 

2. Remote staking from Bitcoin chain
   -> 비트코인을 bridge하지 않기 위해 babylon이 선택한 방법으로 비트코인의 타임락 script를 이용하여 일정기간동안 비트코인의 소유자가 비트코인을 사용할 수 없게 잠그고,
      소비자 PoS 체인에서 프로토콜 위반이 발생할 경우 스테이크를 슬래싱하는 방식입니다. 

      이 방식의 문제점은 script가 제한된 bitcoin에서 스테이킹된 금액을 슬래싱 할 방법이 없다는 것인데요 바빌론 네트워크는 슬래싱을 구현하기 위해 EOTS라는 암호학 기법을 사용하였습니다.


### 바빌론에서 비트코인을 PoS체인에 스테이킹 하는 과정 ### 
앨리스는 1 비트코인을 가지고 있으며 이를 PoS 체인에 스테이킹하고 싶다고 가정하면, 과정은 다음과 같이 진행됩니다:

스테이킹 계약 시작
먼저 앨리스는 비트코인 체인에 스테이킹 트랜잭션을 전송하여 자신의 비트코인을 셀프 커스터디 볼트(자기 관리형 금고)에 잠금으로써 스테이킹 계약을 체결합니다.

비트코인 잠금 해제 방법
잠긴 비트코인은 앨리스의 개인 키를 사용하여 다음 두 가지 방법 중 하나로만 잠금 해제될 수 있습니다:

1. 앨리스가 언본딩(unbonding) 트랜잭션을 발행하면, 비트코인은 잠금 해제되어 3일 후에 앨리스에게 반환됩니다.

2. 앨리스가 슬래싱(slashing) 트랜잭션을 발행하면, 비트코인은 소각 주소(burn address)로 전송됩니다.

PoS 체인 검증 시작
이 스테이킹 트랜잭션이 비트코인 체인에 나타나면, 앨리스는 자신의 키를 사용하여 PoS 블록에 서명함으로써 PoS 체인의 검증을 시작할 수 있습니다.



<img width="823" alt="image" src="https://github.com/user-attachments/assets/15d68bba-db21-46b6-94dd-7f5328448495" />


### EOTS ### 

EOTS (Extractable one-time signatures)는 슬래싱을 구현하기 위해 사용되는 signature입니다. 

EOTS가 바빌론에서 어떻게 작동하는지 확인해봅시다. 


![image](https://github.com/user-attachments/assets/259cdd64-f61e-4945-a087-bbdec1a05c53)



#### 1. EOTS Randomness(무작위 값) 생성: ####

EOTS Manager는 FP(Finality Provider)가 블록에 최종적으로 서명할 때 사용할 무작위 값을 생성한다. 이 무작위 값은 FP의 비밀 키를 안전하게 보호하기 위한 중요한 요소이다.

#### 2. EOTS Public Randomness 전달: #### 

생성된 무작위 값은 EOTS Manager에 의해 FP에게 전달된다. FP는 이 값을 사용하여 최종적으로 블록에 서명하게 된다. 
이 값은 서명 과정에서 FP의 비밀 키를 보호하는 데 중요한 역할을 하며, 만약 이중 서명이 발생할 경우 퍼블릭 키와 쌍을 이루는 비밀 키를 자동으로 노출시켜 악의적 검증자(악의적인 FP)에 대한 슬래싱 트랜잭션을 작동시킨다. 

#### 3. EOTS Public Randomness와 Finality Vote 커밋: #### 

FP는 최종성 투표 결과를 EOTS Public Randomness와 함께 블록체인에 커밋한다. 이를 통해 블록의 최종성을 확정하고, 이중 서명을 방지한다. 이 과정은 Babylon 프로토콜의 보안을 강화하고, FP의 서명 오류를 최소화하는 역할을 한다.

#### 4. Covenant Committee와의 협력: #### 

Covenant Committee는 FP가 비트코인을 언본딩(스테이킹 해제)하려고 할 때 중요한 검증 역할을 수행한다. FP가 언본딩을 요청하면, Covenant Committee는 이 요청이 올바른지 확인하고, 언본딩이 제대로 이루어졌는지 검증한다. 이 과정에서 Covenant Committee는 EOTS Manager와 협력하여 트랜잭션이 정확하게 처리되었는지 확인한 후, 언본딩을 승인한다. 이를 통해 언본딩 과정에서의 보안성을 높인다.


이더리움 PoS의 Gasper 와의 차이점.. 뇌피셜 

( tendermint는 블록마다 2/3 vote를 받아서 finality를 보장받는 구조이기 때문에 더블 보팅만 잘 막으면 된다. 
surround voting까지 막아야 하는 이더리움과 다름 = 그렇기에 EOTS로 슬래싱 메커니즘 구현이 가능했다. ) 

### Bitcoin Stamping ### 

비트코인 네트워크와 PoS체인이 긴밀하게 동기화되어야 합니다.
비트코인 타임스탬핑 기술을 통해 PoS 블록 해시와 블록에 투표하는 스테이커 세트를 비트코인 체인에 기록합니다.

Babylon 네트워크가 비트코인과, PoS체인간 중재자로 작용하여 여러 유틸리티를 제공합니다. 


### Architecture ### 

<img width="823" alt="image" src="https://github.com/user-attachments/assets/ba5ac982-7cd0-4011-848b-2f3ba236879e" />

#### 3계층 아키텍처와 네트워크 효과 ####
바빌론 체인을 둘 사이에 두어 Bitcoin 네트워크에서 제공하기 힘든 timestamping기능을 제공합니다. 
Cosmos-SDK 기반 바빌론체인을 만들어 IBC(inter blockchain communication)를 통해 PoS체인과 교류할 수 있습니다. 

바빌론 체인이 컨트롤 플레인 역할을 하며, 비트코인과 데이터 플레인(PoS 체인들) 간의 상호작용을 가능하게 함
이 아키텍처는 네트워크 효과를 가져오고 상호운용성 가능성을 열어줌
예를 들어, 바빌론 체인에 기록된 두 PoS 체인의 최종성 상태를 기반으로 PoS 체인 간 트랜잭션을 정산할 수 있음

<img width="750" alt="image" src="https://github.com/user-attachments/assets/c931bb23-77f6-4a75-9089-2264497f39bb" />






