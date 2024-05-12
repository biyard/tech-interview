# 2024-1 IS 08. Cryptography (Misc. & Applications)

## Cryptographic Hash Functions

임의의 크기의 데이터를 고정된 크기의 string으로 변환한다. (효율적)

태그와 디지털 서명의 크기는 작아야 함

- ex.
    
    정보 유출의 방지를 위해 salt와 함께 사용
    
    타임스탬핑 (누가 더 일찍 비밀을 발견했는 지 증명)
    
    메세지 인증 코드
    
    디지털 서명
    
- **Requirements for Cryptographic Hash Functions**
    
    **One-wayness (단방향성)**: 
    
    계산하기 쉽고 속도가 빠르다
    
    hash(m) = h 인 h에 대해 m값을 역계산은 할 수 없음
    
    → 손실 압축
    
    ![Untitled](2024-1%20IS%2008%20Cryptography%20(Misc%20&%20Applications)%2064941e6a00ce4b1586f8e838a6518c78/Untitled.png)
    
    **Collision resistance (충돌 저항성)**: 해시 함수가 안전한것으로 자격을 갖추기 위해서 가장 중요한 속성
    
    **Second pre-image resistance (Weak collision resistance)**
    
    주어진 Input m1에 대해 hash(m1) = hash(m2)인 m2를 찾기가 힘들다
    
    m1만 주어짐
    
    ![Untitled](2024-1%20IS%2008%20Cryptography%20(Misc%20&%20Applications)%2064941e6a00ce4b1586f8e838a6518c78/Untitled%201.png)
    
    **Collision resistance (Strong collision resistance)**
    
    임의의 두 메세지 m1, m2를 선정했을 때 hash(m1) = hash(m2) 일 확률이 극히 낮다.
    
    m1, m2 둘다 주어짐
    
    ![Untitled](2024-1%20IS%2008%20Cryptography%20(Misc%20&%20Applications)%2064941e6a00ce4b1586f8e838a6518c78/Untitled%202.png)
    
    정보를 숨기는 기능을 하지 않음 (dictionary table attack)
    
    Key와 같은 의존성이 없다.
    
    - **Hash Collision Attack Scenario**
        
        비대칭 암호화로 pdf파일을 하는데 오랜 시간이 걸림 → 1차 해시를 생성해서 보안을 유지
        
        이브는동일한 해시값을 가지는 1.pdf와 2.pdf를 만들었다.
        
        앨리스는 1.pdf에 대하여 서명했다.
        
        이브는 1.pdf에 대한 사인을 2.pdf에 첨부했다. (attack)
        

## **Building Crypt Hash Functions**

[SHA1 / SHA2 알고리즘](https://m.blog.naver.com/vjhh0712v/221453210356)

- **Merkle-Damgård Construction**
    
    ![Untitled](2024-1%20IS%2008%20Cryptography%20(Misc%20&%20Applications)%2064941e6a00ce4b1586f8e838a6518c78/Untitled%203.png)
    
    메세지를 고정된 크기의 블록으로 나눈다 (padding 포함)
    
    압축함수 f(체인 변수 (IV로부터 시작해서), 메세지 블록) ⇒ 다음 체인 변수
    
    - MD5 (Message digest algorithm)
        
        안전하지 않음
        
        collision attack이 많이 보고되었다
        
        pre-image attacks이 이론적으로 가능하다
        
        보안적인 목적으로 사용되지 않는다.
        
        의도치 않은 corruption으로부터(예를들어 라우터를 거치면서 데이터 손실) 데이터 무결성을 검증하는 데에 사용 (체크섬)
        
    - Secure Hashing Algorithms(SHA-Family)
        
        인텔은 하드웨어에 sha 작업을 포함할 수 있게 x86 아키텍처를 확장함 (그만큼 빈번한 작업)
        
        - SHA-1
            
            1995년에 NSA에 의해 발명됨
            
            output: 160bit
            
            block size: 512bit (한번에 512bits을 처리)
            
            sha-1 충돌
            
        - SHA-2
            
            NSA에 의해 발명됨
            
            SHA-256 outputs 32 bytes
            
            SHA-512 outputs 64 bytes
            

## Digital Signatures

[디지털 서명](https://ko.wikipedia.org/wiki/디지털_서명)

네트워크에서 송신자의 신원을 증명하는 방법

실제 서명 X

해당 작업을 가속화 하는데에 해시가 사용

충돌 X, 보안문제 X, 메세지 경량화, 속도 향상

- Ex.
    
    앨리스는 어떤 메세지 M의 송신자가 자신임을 모두에게 증명하고 싶어한다.
    
    S는 시크릿키 암호화, P는 퍼블릭키 복호화
    
    Alice: Sa(hash(M)) -> SigM 과 M ⇒ bob
    
    Bob: hash(M) =? Pa(SigM) (**signature verification**)
    
    Eve가 M을 M’으로 변조한다면?
    
    Bob: hash(M’) =? PA(SigM) → hash(M’) ≠ hash(M) (해시 함수가 암호학적으로 안전하다는 가정 하에)
    

## Message Authentication Codes (MAC)

[해싱(Hashing)을 활용한 HMAC(Hash based Message Authentication Code)](https://m.blog.naver.com/techtrip/221723355441)

[Hash Length extension attack - 길이 확장 공격](https://eine.tistory.com/entry/Hash-Length-extension-attack-길이-확장-공격)

통신 시 양 당사자 간에 공유된 단일 비밀키 하나가 있다고 가정 (대칭 키 암호화)

목표: 메세지의 **Authenticity**, **integrity** 검증

암호화된 메세지에 MAC를 첨부 → 수신자는 MAC를 검증하는 과정

공격자가 임의의 메세지에 대해 신자가 생성한 MAC을 계산할 수 없어야 한다.

- Hash-based MAC (HMAC)
    - **H ( message )**
        
        안전하지 않음(해시에는 보안 기능이 없기 때문에)
        
        Secret-independent - 공격자는 메세지와 해시 값을 모두 변경할 수 있다.
        
        모두가 해당 MAC 값을 계산할 수 있음
        
        one-time pad를 사용해서 암호화된 메세지는 무결성 공격에 취약하다 (신뢰하기 어려움)
        
        plain text에 예측가능한 변화를 줄 수 있음
        
    - **H ( key || message )**
        
        해시 함수에 key 종속성 추가
        
        H가 Merkle-Damgård construction 구조를 사용하는 해시 함수라면 length extension attack이 가능하다
        
        ![뒤에 메세지 블록을 덧붙여서 추가 연쇄작용 발생 가능](2024-1%20IS%2008%20Cryptography%20(Misc%20&%20Applications)%2064941e6a00ce4b1586f8e838a6518c78/Untitled%204.png)
        
        뒤에 메세지 블록을 덧붙여서 추가 연쇄작용 발생 가능
        
        공격자는 메세지 끝에 다른 메세지를 연결할 수 있음 → 생성된 해시값을 사용하여 전체 메세지에 대한 최종 해시 값을 계산할 수 있음
        
        공격자는 Key값을 모르고 메세지, 메세지 해싱 값 만으로도 원하는 메세지를 injection 가능하다.
        
        메세지를 완전 대체하는 것은 불가능
        
    - **Hash-based MAC (HMAC)**
        
        ![opad, ipad는 상수, 서로 다른 값](2024-1%20IS%2008%20Cryptography%20(Misc%20&%20Applications)%2064941e6a00ce4b1586f8e838a6518c78/Untitled%205.png)
        
        opad, ipad는 상수, 서로 다른 값
        
        HMAC는 MAC이 요구하는 것보다 더 강력한 보안 보장을 제공
        
        HMAC는 key의 의존된 메시지에 대한 정보를 표시하지 않음
        
        공격자는 key를 모르면 해시를 다시 생성할 수 없음 → length extension attack이 불가능 (내부해시, 외부해시가 따로 있어서)
        
        해싱 → 메세지 확장 기능 제거
        
    - HMAC vs. Digital Signatures
        
        
        **HMAC**
        
        데이터 무결성 검증에 초점을 둠
        
        공격자가 Shared secret key에 대한 접근을 할 수 없게 해야 함
        
        송, 수신자가 동일한 secret key로 검증 과정을 거침
        
        **Digital Signatures**
        
        송신자 검증에 초점을 둠
        
        송신자의 secret key에 대한 접근을 할 수 없게 해야 함
        
        송신자는 secret key, 수신자는 Public Key를 사용하여 검증 과정을 거침
        

---

## Public-Key Infrastructure (PKI)

[Out-of-Band 데이터 통신](https://www.joinc.co.kr/w/Site/Network_Programing/Documents/Out_Of_Band)

[Out Of Band (OOB data)](https://blog.naver.com/sanghun0318/220399680353)

공개키를 신뢰할 수 있는 방법은?

**MitM attack** : 공격자가 중간 전달과정에서 공개키를 자신의 것으로 대체할 수 있다.

Diffie-Hellman 이전의 공격방식

송신자: M → sender Pub key 암호화 → C

공격자: C → sender Sec key 복호화 → M / M’ → receiver Pub key 암호화 → C’

수신자: C’ → receiver Sec key 복호화 → M’

**키 배포를 위해서 Certificate Authority (CA)의 서명을 binding**

![Untitled](2024-1%20IS%2008%20Cryptography%20(Misc%20&%20Applications)%2064941e6a00ce4b1586f8e838a6518c78/Untitled%206.png)

1. Delegate/Centralization 방식
    
    **Public-Key Infrastructure** (Roots of trust)
    
2. Decentralization 방식
    
    Web of trust (X)
    
- **Public-Key Infrastructure (PKI)**
    
    **Digital Certificates (디지털 인증서)**: ID와 Pub key 간의 binding
    
    Certificate Authority (CA)에 의해 서명 및 발급됨 → binding을 서명하는데 사용된 개인 키는 CA가 소유
    
    Pub key의 실제 소유권자인지 인증하는 역할 (공개 키의 구속력, 소유권을 증명)
    
    해당 인증서에 해당하는 비밀키가 유출 될 겅우 CA가 인증서를 취소함
    
    Expired, Revoked 되었는지 확인하는 과정을 거침
    
    **Certificate Authorities (CAs)**: Identity 확인 및 Certificates**를** 발급하는 기관
    
    여러개의 인증 기관이 있고 CA간의 계층 구조가 있음 → 다른 CAs의 바인딩에 서명하는 방식으로 신뢰할 수 있는 다른 CAs에게 위임할 수 있음
    
    최상위 인증 기관 뿐만 아니라 여러 local CA가 있다.
    
    **out of the band** 에서 인증 발생
    
    Https(TLS/SSL)가 PKI를 사용
    
    Root CAs: local CAs를 신뢰하지 않더라도 Root CAs는 신뢰할 수 있어야 한다.
    
    다음 단계의 인증기관에게 해당 인증기관이 신뢰할 만한지 타고 가다보면 최종적으로 Root CAs는 신뢰할 수 있어야한다.
    
    OS 혹은 소프트웨어로 배포됨 (windows에서 certmgr)
    
    운영체제를 열면 신뢰할 수 있는 모든 인증기관을 확인할 수 있음
    
- **Digital Certificate Creation**
    
    ![Untitled](2024-1%20IS%2008%20Cryptography%20(Misc%20&%20Applications)%2064941e6a00ce4b1586f8e838a6518c78/Untitled%207.png)
    
    대역 외의 인증기관이 신원을 확인 → 검증 → 신원 파일에 인증기관의 디지털 서명이 추가됨
    
    은행 사용시 공동인증서가 필요
    
    스마트폰 인증 시 인증 기관이 인증서를 발급하고 SNS메세지를 통해 스마트폰 소유자가 본인임을 확인 → 해당 인증서를 통해 out of band 인증과정을 거치지 않고 사용 가능
    
    ![Untitled](2024-1%20IS%2008%20Cryptography%20(Misc%20&%20Applications)%2064941e6a00ce4b1586f8e838a6518c78/Untitled%208.png)
    
    인증서를 확인했다 → 해당 서버에 대한 엑세스가 어떤식으로든 납치되지 않았다는 것을 의미
    
    웹 서버 인증 시에 HTTPS 프로토콜 사용 ⇒ TLS사용 ⇒ PKI를 사용한다는 것을 의미
    
- **Authenticated Key Exchange**
    
    ![Untitled](2024-1%20IS%2008%20Cryptography%20(Misc%20&%20Applications)%2064941e6a00ce4b1586f8e838a6518c78/Untitled%209.png)
    
    **Ephemeral key**: 세션을 연결할 때마다 Diffie Hellman 과정에 의해 생성되는 임시 키
    
    1. User → Web server : 유저의 임시 공개키 쌍 중 하나 전달
    2. 웹 서버는 자신의 long-term 비밀키로 자신의 임시 공개키에 서명
    3. Web server → user : CA에 의해 발급된 인증서 + 웹서버의 임시 공개키 + Web server long-term Secret key로 암호화(서명)한 웹서버의 임시 공개키
    4. User가 전달받은 임시 키의 진위여부 확인
        1. 암호화된 웹서버의 임시 공개키를 서버의 long-term 공개키로 복호화하여 전달받은 임시 키와 비교
        2. 전달받은 인증서가 어떤 인증기관에서 서명되었는 지, 인증서가 일치하는 지 등등 검증
    5. 각각 전달받은 임시키 쌍으로 Shared Secret 생성
    6. AED와 같은 대량 암호화 통신 수행
    
- **TLS(Transport Layer Security) Handshake**
    
    ![Untitled](2024-1%20IS%2008%20Cryptography%20(Misc%20&%20Applications)%2064941e6a00ce4b1586f8e838a6518c78/Untitled%2010.png)
    
    핸드셰이킹 과정에서 **cipher suites**이 결정 됨 (shared secret)
    
    키 교환 및 shared secret 설정 하는 128비트 대칭 암호화 방식 (GCM 에서 해시가 필요시 SHA256을 사용)
    
    Key exchange algorithm
    
    Authentication algorithm
    
    Bulk encryption algorithm
    
    Hash algorithm
    
- **bad usecase of hybrid (asymmetric and symmetric) cryptography**
    
    ![Untitled](2024-1%20IS%2008%20Cryptography%20(Misc%20&%20Applications)%2064941e6a00ce4b1586f8e838a6518c78/Untitled%2011.png)
    
    랜섬웨어에 대칭키 암호화 방식만 사용 될 경우 키를 reverse engineering 할 수 있음 → 하이브리드 암호화 (대칭키 + 비대칭키)
    
    **Wannacrypt**: 랜섬웨어, 멀웨어 툴
    
    모든 파일을 암호화하는 데에 몇시간 넘게 걸림 (랜섬웨어에는 속도가 중요하다)
    
    1. **서버 공개키**만 저장 
    2. **클라이언트별 개인/공개키** 쌍을 생성 
    3. **서버 공개키**로 **클라이언트 개인 키**를 암호화 후 **개인 키** 원본을 버림(**dump**) 
        
        → **원본 개인키**는 **서버 개인키**로만 확인 가능
        
    4. 감염시킬 모든 파일에 대해 **공개/개인키** 쌍 생성
    5. **클라이언트 별 공개키**를 사용하여 **파일별 대칭 키 쌍**을 암호화 후 원본을 버림(**dump**)
        
        → 해당 시점에서 파일을 암호화 하는 데에 사용된 **대칭 키**를 복구 가능한데, 파일별로 **대칭키**를 생성 후 바로 버리기 때문에 중간에 알아채더라도 복구 할 방법이 없다.
        
    
    감염된 파일을 복호화 할 수 있는 **개인키**는 **클라이언트별 개인키**로 복호화 해서 얻을 수 있으며, **클라이언트별 개인키**는 **서버 개인키**로 복호화 해서 얻을 수 있다.
    
- **good use of asymmetric cryptography: Verified Boot**
    
    ![Untitled](2024-1%20IS%2008%20Cryptography%20(Misc%20&%20Applications)%2064941e6a00ce4b1586f8e838a6518c78/Untitled%2012.png)
    
    안드로이드 스마트폰 부트체인
    
    안드로이드 부팅 시 구글이 서명한 이미지를 실행한다. (스마트폰 내의 구글의 공개 키가 내장되어있음)
    
    - **Verified Boot 가 모든 코드를 신뢰할 수 있는 소스(개인키 보유자)의 것임을 검증하는 과정**
        1. CPU가 read-only 저장소에서 1단계 부트로더(BL1)의 전원을 켜고 로드
        2. BL1은 저장소에서 BL2를 찾아 메모리에 로드
        3. ROTPK(Root of Trust Public Key)를 사용하여 메모리상의 BL2의 무결성을 검증
            
            구글의 공개 키 사용
            
        4. 무결성 확인 시 BL2는 secure / non-secure worlds 를 분리하고 최대 3개의 3단계 부트로더(BL3)를 메모리에 로드
        5. BL3-3 은 non-secure OS kernel을 로드