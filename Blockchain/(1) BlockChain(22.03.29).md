## 1. What is a BlockChain

➡️ 블록체인의 개요, 기초지식

<img width="600" alt="스크린샷 2022-03-27 오후 5 50 36" src="https://user-images.githubusercontent.com/95120267/160722537-00417cd1-4a7d-47d9-867e-710ad4fb4f6b.png">

- 블록의 구성 = 블록은 레코드이기 때문에 데이터를 갖고있다
- 첫번째 블록(= genesis block)
  - 블록체인이 초기화된 후 이 블록은 언제나 첫번째이기 때문에 genesis block이라고 부른다. (=절대로 바뀌는 경우는 없음)
  - 이 블록만이 첫번째 블록이며 다른 블록은 첫번째가 될 수 없다
  - 첫번쨰 블록이기 때문에, prev.Hash가 없는 유일한 블록 (prev.Hash=0)
- 블록체인이라고 불리는 이유 = 해시값을 통해 블록들이 암호화 링크로 연결되어있다 (=모든 블록은 각자의 Hash값을 가지고 있고, 이전 블록의 Hash값을 참조)
- 누군가가 n번 블록의 데이터를 조작하면 n번 블록의 해시값이 변하고 더이상 n+1번과 매칭이 되지않음으로써 n번블록이 조작되었다는것을 알 수 있다.

<hr />

## 2. Understanding SHA256 Hash

➡️ 암호화폐, SHA256해싱 알고리즘과 원리

- SHA : 안전한 해시알고리즘의 약자, 256 : 메모리를 차지하는 비트 수
- Hash의 길이 : 언제나 64자, 숫자+문자(16진법 해시이기때문에), 해시의 문자는 각각 4비트를 차지, 64자 \* 4비트 = 256비트
- 이 알고리즘이 텍스트 문서뿐만 아니라 어떤 디지털문서(영상,텍스트,오디오,실행파일,운영체제)에도 적용가능함<br />

### 해싱 알고리즘에는 5개의 요구조건이 있다<br />

1️⃣ One-Way(단방향이어야 한다.)<br />
  - 무조건 문서에서 해시로 가는 방향만 가능<br />
  - 해시를 바탕으로 문서를 복원하거나 역설계할 수 없다<br />

2️⃣ Deterministic (결정적이어야 한다.)<br />
  - 만약 동일한 문서를 해싱알고리즘에 적용하면 똑같은 해시값을 얻어야 함<br />

3️⃣ Fast Computation (빠른 연산)<br />

4️⃣ The Avalanche Effect (쇄도 효과)<br />
  - 동일한 문서에다가 아주작은 변형을 가했을때(=1비트의 변화라도 있었을 때) 해시값은 완전히 달라진다.<br />
  - 하나의 변화가 몇가지의 변화를 유발하고 그들이 더 많은 변화를 유발하고 이는 더더 많은 변화를 유발한다.<br />
  - (\*채굴관련 강의에서 이유에 대해 알아볼 예정)<br />

5️⃣ Must withstand collisions (충돌 저항성)<br />
  - 디지털 데이터의 양은 64자로 표현할 수 있는 다양한 조합의 숫자보다 훨씬 많다 (=비둘기집 원리)<br />
  - 알고리즘이 인위적인 충돌에 견딜 수 있어야 한다<br />

<hr />

## 3. Immutable Ledger(불변의 대장)

➡️ 다른 전통적인 원장과 비교했을 때 블록체인의 장점(ex. 블록체인의 기록 보관에 도입된 첫번째 보안계층)

<img width="600" alt="스크린샷 2022-03-27 오후 6 21 27" src="https://user-images.githubusercontent.com/95120267/160722767-760bfa2b-128e-40b8-9146-da17b4bdfc53.png">

- 누군가 특정 블록에 있는 데이터를 변경하려고 하면 그 블록에 있는 해시가 변경됨. <br />
  ~> 이는 암호화 링크가 더이상 작동하지 않는다는 뜻
- 바뀐 블록의 해시는 다음블록에 기록된 해시와 다르기때문에 일치하지 않아 다음블록도 변경해야하고 연쇄적으로 다 변경을 해야한다 (\*쇄도 효과)
- 즉 암호화 링크때문에 한 블록을 변경하면 그 뒤로 이어지는 모든 블록은 더이상 유효하지 않고 더이상 체인에 연결되어 있지 않아서 기록을 변경이 매우 어려움 <br />
  (= 컴포넌트가 계속 추가되는 방식으로 설계되어있기 때문에 체인에 있는 단일 블록의 변경은 불가능하다) <br />
  (= 한번 블록체인에 데이터가 기록되면 바꾸기 매우 어려움) <br />

<hr />

## 4. Distributed P2P Network (분산 P2P 네트워크)

➡️ 블록체인 원장 배포를 통해 두번쨰 보안계층을 도입하여 관련 기술의 신뢰성을 높일 수 있다

- P2P시스템에는 많은 컴퓨터가 상호연결되어있음
- 블록체인은 하나의 컴퓨터 시스템에 보관하는 대신 수천대의 컴퓨터에 복사됨(모든 것은 암호키와 같은 것으로 연결되어 있다->모듈강의에 더 자세히 다룰예정 그래서 식별자를 통하지 않으면 정확한 이름을 얻을수없음)
- 모든 컴퓨터에 있는 모든 트랜잭션에 대한 정보는 누구나 컴퓨터로 변경가능
- 한번 블록이 추가되면 네트워크를 통해 정보가 전달되고 모든 컴퓨터가 그 블록을 가질 때까지 네트워크를 통해 계속 추가됨(네트워크 크기에 따라 시간 다름)
- 누군가가 어떤 컴퓨터에 접속하여 블록체인을 해킹했다면(뒤로 오는 모든 블록들까지) 분산 P2P네트워크는 모두 끊임없이 동기화되는 특성(=피어가 일치하는지 확인)이 있기에 피어가 일치하지 않다는 문제를 확인하게 된다.<br />
- 그러면 해당 컴퓨터에 있는 블록체인에 신호를 보내 해킹당했다는 것을 알아차림 -> 자동적으로 연결된 컴퓨터들 값 중에서 기존값을 복사하여 해킹된 컴퓨터의 블록이 복구가 됨
- 따라서 해커는 하나의 컴퓨터나 블록체인을 해킹,값변경을 할 수 없음, 모든 블록체인을 동시에 공격해야 가능한 일
- 블록체인이 내 컴퓨터에 있는지는 중요하지 않음, 블록체인을 통해 개인정보를 얻을 수 없는 한(=이름이나 주소 같은 것이 아닌 식별자로 표시되는 한) 내 컴퓨터에 없어도 상관없다
- 이로써 보안이 제일 좋아진다. <br />
  1단계보안 = 해시암호문<br />
  2단계보안 = 분산 P2P네트워크<br />
  그리고 합의 프로토콜 등을 통해 블록체인을 강력하게 만드는 보안 층이 더 많아진다.

<hr />

## 5. How Mining Works(Part1: The Nonce)

➡️ 채굴이 어떻게 이루어지는지, 블록체인에서 변수인 논스

<img width="600" alt="스크린샷 2022-03-28 오후 9 17 13" src="https://user-images.githubusercontent.com/95120267/160722700-199da425-9e57-4e30-b171-1651972925ac.png">

- 블록의 구성 = 블록 번호, 데이터(여러개의 TX), 이전 해시, 현재 해시
- 현재 블록의 해시는 어떻게 구하는가? = 블록 번호, 데이터, 이전 해시를 해싱알고리즘에 넣으면 이에 해달하는 해시를 도출해냄
- Nonce(논스:한번만 사용되는 숫자) : 이 필드가 채굴에서 가장 중요한 사항, 모든사람들이 이 필드를 바꾸는 작업을 수행 -> 이를 이해하기 위해서는 무엇이 해시를 제어하는지 알아야 함
- 무엇이 해시를 제어하는가? = 블록 번호, _논스_, 데이터, 이전 해시
- ⭐️ 해시를 제어할 수는 없지만, 논스를 바꾸면서 해시를 변화시킬 수 있음 / 논스를 임의로 조정해서 해시에 다양성을 줄 수 있음
- 해시풀(smallest =0000...000, largest=FFFF...FFF)

<hr />

## 6. How Mining Works(Part2: The cryptographic puzzle)

➡️ 암호화 퍼즐

- Hash = Number (16진수, 0~9,A=10,B=11,C=12,D=13,E=14,F=15)
- 16진수를 10진수로 변환가능(모든 숫자는 16진수 체계에서 더 높은 값을 인코딩함)
- 해시중에는 선행제로로 시작하는 해시도 존재함 (=0이많을수록 작은수)
- 채굴방법은 기본적으로 블록체인 시스템이나 알고리즘이 대상을 설정하는 것 (즉, 채굴자들이 특정한 해시를 달성하도록 설정한 대상이 있다)
- 논스를 바꿔서 현재블록의 Hash를 변경하여 블록에 추가한다. (블록추가에 성공된 논스 = 골든논스)
- Hash는 쇄도효과가 특징이다.
- 채굴의 원리 = target값 아래에 있는 해시를 구하기까지 논스를 지속적으로 변경하는 것

<hr />

## 7. Byzantine Fault Tolerance

➡️ 수학개념인 비잔틴 내결함성 또는 비잔틴 장군 문제에 대해 배움, 이를 블록체인에 적용하는 법, 이 개념이 분산시스템에서 왜 중요한지 알아봄, 이렇게 되면 합의 프로토콜을 다루기에 좋은상태가 됨

- 비잔틴 내결함성 = 탈중앙화 시스템에서도 아주 중요한 특징, 전달된 정보에 대한 다수결의 알고리즘, 장군들은 전달된 정보에 기반해 의사결정을 내림
- 이 알고리즘이 작동하려면 1/3미만의 반역자가 있어야한다

<hr />

## 8. Consensus Protocol (Part1. Defense against attackers)

➡️ 함의 프로토콜이 공격자로부터 블록체인을 보호하는 데에 어떤 도움이 되는지
➡️ Proof-of-Work(Pow),Proof-of-Stake(PoS),Other

- 체인의 끝에 블록을 놓고 고의적으로 새로운 블록을 추가하려고 할 때, 해결을 어떻게함?
- 블록이 추가되면 모든 것을 확인한 후 수용/기각만 할 수 있다.
- 이 암호화퍼즐은 해결하기도 쉽고 입증하기도 쉬움

- 채굴과 입증의 차이점
- 채굴 : 반복성, 암호화퍼즐을 풀어야하고 논스의 다양한 변형을 거치고 해시도 확인해야 함<br />
  (논스를 통해 올바른 해시를 얻기 위한 무차별 대입을 하는 것)
- 입증 : 일치하는지만 확인하면 됨

<hr />

## 9. Consensus Protocol (Part2. Competing chains) : 작업증명(PoW)

➡️ 대형 (일체형)블록체인의 경우 전세계적으로 분산되어 있어서 특히 서로 멀리 떨어진 노드 사이에 지연이 발생할 수 있다, 그리고 서로 멀리떨어진 두 노드가 동시에 채굴에 성공할 수도 있음(시간차로인해) ~> 계속 블록증가하는 방법에 관한 합의가 필요함
➡️ 합의 프로토콜이 어떻게 블록체인 내 경쟁체인을 다루는지, 무슨일이 벌어지는지, 블록체인이 전 세계에 분포되어 있음에도 발전할 수 있는 이유와 노드 사이에서의 시간 지연적인 비효율이 어디서 발생하는지

<img width="600" alt="스크린샷 2022-03-30 오전 7 59 02" src="https://user-images.githubusercontent.com/95120267/160722380-d737758c-a02b-4d1d-a379-4600a448c836.png">

- 만약 같은시간에 3번체인에 2개의 블록이 등록될 경우, 합의 프로토콜이 필요함
- 인근의 노드들에게 2개의 블록들 중 하나가 네트워크를 통해 전달된다(시간차있음)
- 그 다음블록이 추가되기전까지는 3번블록에는 2가지버전이 존재하고있는 상태


<img width="600" alt="스크린샷 2022-03-30 오전 8 05 32" src="https://user-images.githubusercontent.com/95120267/160722407-f0b54cf3-a56d-4047-830a-5182d25d20c6.png">

- 어느쪽이든 4번째 블록을 먼저 추가하면 그 체인이 이김 (longest chain is king), 블록이 가장 많은 체인이 이기고 다른 체인을 교체하게 됨
- 가장 높은 해싱파워를 가진 네트워크에서 가장 긴 체인을 생성
- 블록체인에서의 합의프로토콜 = 51%의 해싱파워를 가졌거나 50% 이상의 해싱파워를 가진 체인이 이김
- 체인에 등록되지 못한 블록 = Orphaned Block(고아 블록)

<hr />

## 10. 정리

- 블록체인은 지속적으로 커지는 탈중앙화된 불변원장(O)
- 블록체인은 SHA256 암호화 함수를 검증하는 알고리즘(O)

- 블록체인의 "분산 P2P 네트워크"적 성격은 이 기술의 보안을 어떻게 향상?
- 네트워크의 모든 참가자는 전체블록체인의 사본을 가지고 있으며 모든 참가자는 동기화된다 <br />
  따라서 공격자가 네트워크의 컴퓨터 중 하나에서 블록체인을 수정하면 블록체인의 사본 하나만 수정된다.<br />
  네트워크는 이를 보고 네트워크의 블록체인 중 다수인 버전과 비교하여 매우 빠르게 가짜버전을 정상화시킴

- 비트코인 채굴 : 채굴은 비트코인 네트워크가 설정한 특정대상 임계값 아래에 해시 값을 생성하는 논스 값을 찾는 것
- 합의 프로토콜 : 분산 네트워크 참가자 간의 합의를 달성하는 데 사용되는 프로세스


## [출처](https://www.udemy.com/course/best-blockchain-az/)