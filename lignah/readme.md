# Ransomware Architecture

## 1. Malware Overview
악성코드(Malware)는 동작 방식, 감염 경로, 그리고 목적에 따라 분류

### 1.0. Terminology
* **Malware**는 일반적으로 **Malicious + Software**(악의적인 목적을 가진 소프트웨어)의 합성어로 설명
* 같은 악성코드라도 **전파 방식(How it spreads)**, **행위/목적(What it does)**, **초기 유입 경로(Where it entered)** 축이 다르면 대응 방식이 달라짐

### 1.1. Classification
아래 분류는 대표적인 예시이며, 실제 공격에서는 여러 특성이 결합된 형태(예: Trojan 형태로 유포되는 Ransomware)가 흔함

### 1.2. How it spreads (전파 방식)
* **Virus (바이러스):**
    * 스스로를 복제하여 다른 정상 파일(숙주, Host)을 감염시킴
    * 예: 파일 시스템 내의 실행파일을 찾아 EP(Entry Point)를 변조하거나 코드를 삽입하여 실행 시 함께 실행되도록 함
* **Worm (웜):**
    * 숙주 파일 없이 네트워크 패킷 등을 통해 스스로 전파(Self-propagating)
    * 파일 수정보다는 네트워크 대역폭 소모나 취약점 스캐닝이 주된 특징
* **Trojan (트로이 목마):**
    * 정상적인 프로그램(예: 게임 크랙, 유틸리티)으로 위장하여 사용자가 직접 실행하도록 유도하며 자가 복제 기능은 없음

### 1.3. What it does (행위/목적)
* **Ransomware:** 데이터/시스템 접근을 막고 금전을 요구
    * 핵심 목적: 가용성(Availability) 침해 후 협박/금전 요구
    * 대표 행위: 파일 암호화(Encryption), 확장자 변경, 복구 방해(백업/섀도우카피 삭제 시도 등), 랜섬노트 생성
    * 변형: 이중/삼중 갈취(암호화 + 데이터 탈취 + 유출 협박) 형태도 존재

* **Spyware:** 사용자/시스템 정보를 은밀히 수집
    * 핵심 목적: 자격 증명/개인정보/기업정보 탈취 및 추가 침해에 활용
    * 대표 수집 대상: 키 입력(키로깅), 클립보드, 브라우저 저장 비밀번호/쿠키/세션, 스크린샷, 메신저/메일 데이터
    * 동작 특성: 사용자 눈에 띄지 않게 백그라운드에서 실행, 장기 은닉(stealth)

* **Adware:** 광고 노출/리다이렉트 등으로 수익을 노림
    * 핵심 목적: 광고 클릭/노출 수익, 트래픽 유도, 제휴(affiliate) 수익
    * 대표 행위: 브라우저 홈/검색엔진 변경, 팝업/배너 삽입, 광고 SDK 번들, 원치 않는 프로그램(PUP) 설치 유도
    * 특징: 악성코드와 경계가 흐린 경우가 있어 “원치 않지만 동의된 설치” 형태로 들어오기도 함

* **Backdoor / RAT:** 원격 제어 채널을 열어 지속적 접근 제공
    * 핵심 목적: 재침투 없이도 지속적으로 시스템을 조종(지속성, Persistence)
    * 대표 기능(개념): 명령 실행, 파일 업/다운로드, 화면/입력 제어, 시스템 정보 수집, 추가 페이로드 로딩
    * 공격 흐름: 초기 침투 후 백도어로 장기 거점 확보 → 권한 상승/수평 이동 등으로 확장되는 경우 많음

* **Cryptojacking:** 피해자 리소스(CPU/GPU)를 이용해 암호화폐 채굴
    * 핵심 목적: 인프라 비용을 피해자에게 전가해 채굴 수익 확보
    * 대표 징후: 비정상적인 CPU/GPU 점유율 상승, 팬 소음/발열 증가, 전력 소모 증가, 시스템 성능 저하
    * 유입 형태: 서버/컨테이너 환경 취약점 악용, 브라우저 기반 스크립트, 번들 설치 등 다양한 형태 가능

### 1.4. Where it entered (초기 유입 경로)
* **Trojanized software:** 정상 프로그램/크랙/설치 파일로 위장(번들·공급망 포함)
    * 핵심 특징: 사용자가 “정상 설치/실행”이라고 믿고 직접 실행하게 만드는 형태
    * 대표 예시: 크랙/키젠, 가짜 설치 관리자, 정상 프로그램에 악성 모듈 번들, 서명된 설치 파일의 유통 경로 오염

* **Phishing email:** 첨부파일 또는 링크를 통해 실행/인증을 유도
    * 핵심 특징: 사회공학으로 사용자의 행동(클릭/실행/로그인)을 유도
    * 대표 예시: 문서 첨부(업무 문서 위장), 로그인 페이지 위장 링크, 배송/세금/결제 등 긴급성을 이용한 메시지

* **Removable media:** USB 등 이동식 매체를 통한 유입/확산
    * 핵심 특징: 네트워크가 분리된 환경에서도 물리 매체를 통해 전파 가능
    * 대표 예시: 문서/바이너리 위장 파일, 단축아이콘/폴더 위장 등 사용자 오인 유도, 내부망으로의 확산 매개

* **MitM (Man-in-the-Middle):** 통신을 가로채 악성 내용 주입/변조
    * 핵심 특징: 사용자가 접속한 “정상 트래픽”을 중간에서 바꾸어 악성 페이로드가 전달되는 상황
    * 대표 예시: 업데이트/다운로드 트래픽 변조, 보안 설정 다운그레이드 유도, 공용 네트워크 환경에서의 트래픽 변조

* **Drive-by Download:** 취약한 브라우저/플러그인 등을 통해 비인지 다운로드/실행
    * 핵심 특징: 사용자의 명시적 실행 의도가 없어도 취약점으로 코드 실행/다운로드가 이어질 수 있음
    * 대표 예시: 취약한 웹 구성요소를 악용한 감염, 방문만으로 페이로드가 전달되는 공격(e.g., 워터링 홀)

* **Supply chain attack:** 배포/업데이트 체인 오염을 통한 대규모 유입
    * 핵심 특징: 신뢰된 공급자/업데이트 경로를 악용해 “정상 업데이트”처럼 배포되는 형태
    * 대표 예시: 업데이트 서버 침해, 빌드 파이프라인/배포 아티팩트 오염, 서드파티 라이브러리(의존성) 변조

---

## 2. PNG File Structure Analysis
랜섬웨어는 파일을 암호화할 때 확장자뿐만 아니라 **File Signature(Magic Number)**를 확인하여 정확한 타겟을 식별

### 2.1. Signature (8 Bytes)
PNG 파일은 항상 다음 8바이트로 시작함. 이 중 1바이트라도 다르면 운영체제에서 이미지로 인식 못함
> `89 50 4E 47 0D 0A 1A 0A`

### 2.2. Chunk Structure
Signature 이후의 모든 데이터는 **Chunk(청크)** 단위로 구성
`Length(4B)` + `Type(4B)` + `Data(Variable)` + `CRC32(4B)`

**구조 (C Struct):**
```c
struct Chunk {
    unsigned int length;
    char        type[4];
    unsigned char *data;
    unsigned int    crc;
};
```


### 2.3. Critical Chunks (필수 청크)
이미지 렌더링에 반드시 필요한 청크들

#### **(1) IHDR (Image Header)**
이미지의 크기, 색상 타입, 압축 방식 등 핵심 메타데이터 포함

* **Bit Depth (비트 깊이):**
    * **정의:** 하나의 색상 채널(Channel)이 가질 수 있는 정보량을 비트 수로 표현한 것
    * **계산:** `08` (8 bit)일 경우, $2^8 = 256$ 단계(농도) 표현
    * **RGB 예시:** Red(8bit) + Green(8bit) + Blue(8bit) = 총 **24bit** 크기의 픽셀
    * **표현력:** $256 \times 256 \times 256 \approx 16,777,216$ (약 1600만 컬러, TrueColor)
    * 만약 Bit Depth가 `16`이라면 $2^{16} = 65,536$ 단계 표현으로 더 정밀한 색 표현 가능

* **Color Type (색상 타입):**
    * `00`: Grayscale (흑백)
    * `02`: TrueColor (RGB 3채널 구성, 일반적인 이미지)
    * `03`: Indexed Color (Palette 사용, 1채널 구성)

* **Compression Method:** 현재 표준에서는 `00` (Deflate/zlib)만 사용
    * Deflate: `LZ77(반복 문자열 치환)` + `Huffman Coding(가변 길이 부호화)` 조합인 압축 알고리즘
    * zlib/gzip: Deflate 데이터를 감싸는 래퍼 포맷(헤더 + 체크섬 등) 계열, PNG IDAT는 보통 zlib 스트림 형태
* **Filter Method:** `00` (Adaptive Filtering)만 사용
* **Interlace Method:**
    * `00`: **None** (위에서 아래로 순차적 로딩)
    * `01`: **Adam7** (이미지를 7번에 걸쳐 흐릿한 상태에서 점차 선명해지는 방식으로 로딩)

#### **(2) PLTE (Palette)**
IHDR의 Color Type이 `03` (Indexed Color)일 경우 필수적으로 존재해야 하는 색상표 청크

**구조 (C Struct):**
```c
struct PaletteEntry {
    uint8_t R;  // Red
    uint8_t G;  // Green
    uint8_t B;  // Blue
} palette[256];
```

* **동작 원리:** TrueColor(Type 2)는 픽셀당 3바이트(RGB)를 직접 저장하지만, Indexed(Type 3)는 색상표의 **인덱스(번호) 1바이트**만 저장
* **뷰 방식:** 뷰어는 IDAT의 데이터(번호)를 읽고, PLTE 청크에서 해당 번호의 RGB 값을 찾아 화면에 렌더링
* **장점:** 용량이 획기적으로 줄어듦 (픽셀당 3Byte → 1Byte)
* **용도:** 도트 그래픽, 안티에일리어싱이 없는 QR코드, 임베디드 GUI, 레트로 게임 등 메모리 대역폭 절약이 필요한 환경

#### **(3) IDAT (Image Data)**
실제 이미지 픽셀 데이터가 저장되는 공간으로, 여러 개의 IDAT 청크로 분할 가능. IDAT 데이터는 zlib 라이브러리를 통해 압축

**zlib이란?**

zlib은 두 가지 의미로 함께 언급됨

* **오픈소스 압축 라이브러리:** Deflate 기반의 압축/해제 기능을 제공하는 대표적인 C 라이브러리
* **(zlib) 래퍼 포맷:** Deflate 비트스트림을 그대로 쓰지 않고, **헤더 + (압축 데이터) + Adler-32 체크섬** 형태로 감싼(wrapping) 스트림 포맷을 의미하기도 함

PNG의 IDAT는 내부적으로 Deflate를 사용하지만, 실제로는 “zlib 스트림(래퍼 포맷)” 형태로 담기는 경우가 일반적이라 `zlib.decompress()`로 해제 가능

**목적:** 데이터의 중복을 제거하여 용량을 줄임

**Filter Algorithm (전처리):**

zlib 압축 효율을 극대화하기 위해, 압축 전 데이터를 수학적으로 가공하는 과정

인접한 픽셀끼리는 색상 값이 비슷하다는 점을 이용하여, 절대값 대신 차이값(Delta)을 저장 (e.g., 10, 20, 30 → 10, +10, +10) -> 중복 데이터 증가로 압축률 상승

| 필터 타입 | 이름 | 동작 원리 (수식) | 설명 |
|---:|---|---|---|
| 0 | None | Raw | 데이터 변환 없음. 픽셀 값 그대로 저장 |
| 1 | Sub | Current - Left | 바로 왼쪽 픽셀과의 차이값 저장 |
| 2 | Up | Current - Up | 바로 위쪽 픽셀과의 차이값 저장 |
| 3 | Average | Current - (Left+Up)/2 | 왼쪽과 위쪽의 평균과의 차이값 저장 |
| 4 | Paeth | PaethPredictor(L, U, LU) | 왼쪽, 위, 대각선 위 중 가장 가까운 값을 예측하여 뺌 |


IDAT 추출 및 압축 해제 (Python):

```py
import zlib

# HxD에서 복사한 IDAT 청크의 '데이터' 부분 (Length, Type, CRC 제외)
hex_data = "18 57 63 F8 FF FF 3F 00 05 FE 02 FE"
compressed_data = bytes.fromhex(hex_data)

# 압축 해제 - zlib 헤더(18 57)와 Adler32 체크섬을 포함하여 해제
raw_data = zlib.decompress(compressed_data)

print(f"Raw Data (Hex): {raw_data.hex().upper()}")
# 출력 결과: 00FFFFFF (맨 앞 00은 필터타입, 뒤의 FFFFFF는 RGB 값)
# 만약 가로 2px이라면: 00FFFFFF000000 (Filter + White + Black)
```

#### **(4) IEND (Image Trailer)**
이미지 데이터 스트림의 논리적인 끝을 의미

데이터 필드가 없으므로(Length = 0), CRC 값은 항상 고정

Fixed Byte: `00 00 00 00 49 45 4E 44 AE 42 60 82`

### 2.4. Ancillary Chunks (보조 청크)
필수는 아니지만 이미지의 품질이나 메타데이터를 담당. 삭제해도 이미지는 보이지만, 이름을 바꾸거나 구조를 훼손하면 파일이 깨짐

* **sRGB:** 표준 RGB 색 공간 정보
* **gAMA:** 모니터 환경에 따른 감마 보정 값
* **pHYs (Physical Pixel Dimensions):** 물리적 해상도(DPI) 정보. 인쇄 크기 등을 결정


## 3. Error Checksum Algorithms

PNG 파일은 데이터 무결성을 위해 두 가지 종류의 체크섬을 사용

### 3.1. CRC32 (Cyclic Redundancy Check)
용도: PNG의 **각 청크(Chunk)**가 깨졌는지 검증 (파일 구조 관점)

위치: 모든 청크의 마지막 4바이트

특징: 데이터가 1비트만 달라져도 결과가 완전히 달라짐

```py
import zlib
# IHDR 청크 예시 (Type + Data)
hex_data = bytes.fromhex("49 48 44 52 00 00 00 01 00 00 00 01 08 02 00 00 00")
print(f"{zlib.crc32(hex_data):08X}")
# 907753DE
```

### 3.2. Adler-32
용도: zlib 압축 스트림 내의 데이터가 제대로 복구되었는지 검증 (데이터 관점)

위치: IDAT 청크 데이터(Compressed Stream)의 맨 마지막 4바이트

특징: CRC32보다 연산 속도는 빠르지만, 신뢰성은 낮음

### 3.3. Checksum vs. Cryptographic Integrity
CRC32/Adler-32 같은 체크섬은 **전송 오류/파일 손상 탐지**에는 유용하나, **악의적인 변조**를 막는 용도로 설계되지 않음

* **Checksum(CRC/Adler)의 목표:** 우발적 오류(노이즈, 저장장치 오류 등)를 높은 확률로 검출
* **암호학적 무결성의 목표:** 공격자가 메시지를 의도적으로 바꿔도 위조가 어렵게 만들기
* **대표 기법:**
    * **MAC(HMAC 등):** 공유 비밀키 기반 무결성/인증
    * **Digital Signature:** 개인키로 서명하고 공개키로 검증
    * **AEAD(GCM, ChaCha20-Poly1305 등):** 암호화 + 무결성(인증)을 한 번에 제공

## 4. Ransomware Execution Mechanics

### 4.1. Network & In-Memory Execution (Fileless)
Architecture: Server(Attacker) - Client(Victim) 구조. TCP/IP 소켓 통신

**Dropper vs. In-Memory Loader:**

단순 Dropper는 악성 파일을 디스크에 생성(Drop)하고 실행

본 프로젝트의 기법은 Fileless 방식으로, 서버가 .exe 파일을 바이트 스트림(Hex string)으로 전송하면 클라이언트의 디스크에 저장되지 않고 RAM에 직접 할당하여 실행됨

**API:**
* `VirtualAlloc(PAGE_EXECUTE_READWRITE)`: 실행 가능한 메모리 공간 할당
* `recv()`, `memcpy()`: 소켓 데이터를 메모리에 복사
* `CreateThread()` / Function Pointer: 해당 메모리 주소(EP)로 실행 흐름 전환

### 4.2. Encryption Strategy
Targeting: 파일 시그니처 매칭을 통해 특정 포맷(DOCX 등)만 선별적으로 암호화. (DOCX는 ZIP 기반이므로 PK 헤더)

**Multi-threading (Thread Pool):**

수많은 파일을 순차적(Single Thread)으로 암호화하면 속도가 느려 탐지될 가능성이 높음

Thread Pool을 구성하여 CPU 자원을 최대한 활용, 다수의 파일을 병렬로 고속 암호화

### 4.3. Cryptography

암호학적 배경

#### 4.3.1. Symmetric vs. Asymmetric

* **대칭키(Symmetric):** 같은 키로 암호화/복호화
    * 장점: 빠르고 대용량 데이터(파일) 처리에 적합
    * 키 문제: 키를 안전하게 전달/보관해야 함
* **비대칭키(Asymmetric):** 공개키로 암호화(또는 검증), 개인키로 복호화(또는 서명)
    * 장점: 키 배포가 비교적 용이(공개키 공개 가능)
    * 단점: 대용량 데이터에 직접 쓰기엔 느림

#### 4.3.2. Hybrid Encryption

* 데이터(큰 파일)는 **대칭키로 빠르게** 처리
* 그 대칭키는 **비대칭키로 보호**

이 구조는 성능(대칭키) + 키 관리(비대칭키)의 트레이드오프를 동시에 만족시킴

#### 4.3.3. AEAD (Authenticated Encryption with Associated Data)

암호화와 인증/무결성을 같이 제공하는 방식

* 암호화만으로는 **바뀌었는지**를 보장하지 못하는 경우가 많음
* ciphertext가 조금이라도 바뀌면 복호화 실패
    * 대표 예시: AES-GCM, ChaCha20-Poly1305

#### 4.3.4. Confidentiality, Integrity
* **기밀성(Confidentiality):** 내용을 못 보게 함(암호화)
* **무결성(Integrity):** 내용이 바뀌면 탐지 가능해야 함

#### 4.3.5. **복구 불가능성**이 생기는 이유

암호학적으로 안전한 설계는 키가 없으면 복호화가 불가능해야함

그래서 **암호화 강도**외에 **키 관리(키의 위치와 소유자)**가 결과를 좌우함