##  엉클 블록(Uncle Block)

> 블록체인은 탈중앙화된 장부로 누구나(조건에 맞으면) 블록을 만들고 전파할 수 있다. 다수의 노드들이 전파받은 블록을 받으며 유지된다. 

그런데 만약, 동시에 같은 번호의 블록을 받는다면?

여기서 어떤 블록은 받아들여지고 어떤 블록은 탈락된다. 이때 탈락된 블록을 바로 **엉클 블록(Uncle Block)** 이라고 한다.

![image](https://github.com/kwhong95/learn-go-ethereum/assets/70752848/2c89647b-1e7c-45bb-b211-5a9890047fb1)

Uncle Block은 블록체인 네트워크에서 거의 동시에 유효한 블록을 채굴하여 네트워크에 전파한 결과, 일시적인 분기로 인해 체인에 포함되지 못한 블록을 의미한다. 이 블록은 유효하지만 최종 체인에 포함되지 못한 블록으로, 특히 이더리움과 같은 일부 블록체인 네트워크에서 보상 구조와 보안 향상을 위해 유용하게 참조된다.

### Uncle Block의 형성 과정

1. **Nonce 찾기**
- 각 노드는 특정 조건(예: 해시 값의 앞자리가 특정 개수의 0)을 만족하는 해시 값을 찾기 위해 `nonce` 값을 변경하면서 작업 증명을 시도한다.

2. **동시 채굴**
- 거의 동시에 두 개 이상의 노드가 유효한 `nonce` 값을 찾아 유효한 블록을 생성하고, 이를 네트워크에 전파할 수 있다.
- 예를 들어, 노드 3와 노드 5가 각각 블록 A와 블록 B를 거의 동시에 발견하고 전파한다.

3. **네트워크 분기**

- 일부 노드들은 블록 A를 먼저 수신하고 이를 블록체인에 추가한다.
- 다른 일부 노드들은 블록 B를 먼저 수신하고 이를 블록체인에 추가한다.
이로 인해 일시적인 체인 분기가 발생한다.

4. **새로운 블록 추가**

- 네트워크는 새로 채굴된 블록이 어느 체인을 연장하느냐에 따라 체인을 선택한다. 예를 들어, 새로운 블록이 블록 A를 기반으로 채굴되면, 블록 A의 체인이 선택되고 블록 B는 버려진다.
- 반대로, 새로운 블록이 블록 B를 기반으로 채굴되면, 블록 B의 체인이 선택되고 블록 A는 버려집니다.

5. **Uncle Block 처리**

- 체인에 포함되지 못한 블록(이 경우 블록 A 또는 블록 B)은 **Uncle Block**으로 간주된다.
- 이더리움에서는 **Uncle Block**을 참조하여 일부 보상을 받을 수 있습니다. 이는 체인 보안성을 높이고 채굴자의 노력을 보상하기 위해 설계되었습니다.

### 이더리움의 PoS(지분증명) 전환

이더리움은 '더 머지(The Merge)'(PoS 전환) 업그레이드를 통해 더 이상 PoW 기반 채굴이 필요 없어 **Uncle Block** 의 개념이 사라졌다.