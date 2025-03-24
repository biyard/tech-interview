## Comparison of Bitcoin and Ethereum ... and BTCFI 


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
Consensus Mechanism을 통해 블록체인이 탈중앙을 어떻게 달성했는지와 P2P네트워크가 어떻게 상태에 대한 합의를 이루는지를 이해할 수 있습니다. 

즉 블록체인의 State + Network 의 Network를 온전히 이해할 수 있습니다. 

Consensus Mechanism은 네트워크의 참여자(노드)들이 동일한 State에 합의하는 방법입니다. 어떤 블록이 다음 블록으로 체인에 추가될지를 정하는 약속으로 봐도 무방합니다. 비트코인과 이더리움은 서로 다른 합의 메커니즘을 채택하고 있습니다. 

 
### Bitcoin의 Consensus Mechanism: Proof of Work (PoW)

비트코인은 작업 증명(Proof of Work) 방식을 사용합니다. 이는 네트워크 참여자(채굴자)가 복잡한 수학 문제를 풀어 블록을 생성하는 방식입니다.
블록에 있는 Nonce값을 조정하면 해시가 다르게 나온다는 점을 이용하여 특정 수보다 작은 값을 찾는 과정을 반복. 

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

![Bitcoin PoW Consensus](https://github.com/user-attachments/assets/c7ad1c4e-1d95-4e56-b7c5-a2f7e3c65f90)













 
