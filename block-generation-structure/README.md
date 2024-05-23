## 04. block 생성과 구조

### Block 
>  블록체인에서 데이터를 담는 공간
- 현재 블록의 해싱된 값을 다음 블록에 넣어주며 체이닝
- 블록은 특정한 규칙(합의 알고리즘)에 의해 정해진 노드가 생성
- POW(작업 증명)의 경우 특정한 값을 찾기 위해 GPU 리소스와 전기료가 사용된다. 블록체인에선 그에 대한 보상으로 리워드를 준다. 이 과정을 Mining(마이닝)이라고 한다.

#### Mining(마이닝)
> geth 에선 마이닝을 통해 블록을 생성할 수 있다.

![image](https://github.com/kwhong95/learn-go-ethereum/assets/70752848/b302f6ba-87ce-4378-8943-f0ad4800c4bb)

만약, geth에서 지갑을 생성하지 않고 마이닝을 진행하면 다음과 같은 에러가 출력된다.

![image](https://github.com/kwhong95/learn-go-ethereum/assets/70752848/40e69dc5-ff09-474b-a119-fb0c3474e217)

보상을 받을 지갑을 etherbase 혹은 coinbase라고 한다.
geth에서 처음으로 지갑을 생성하면, coinbase가 된다.

<img width="851" alt="스크린샷 2024-05-23 23 46 54" src="https://github.com/kwhong95/learn-go-ethereum/assets/70752848/bee98094-ac3c-4a05-9977-f87463f6f510">

#### blockNumber
> 현재 블록의 수를 불러옵니다.

![image](https://github.com/kwhong95/learn-go-ethereum/assets/70752848/99d18ba9-89d8-4404-821e-69c063bcba60)

#### getBlock(blockNumber: number)
> blockNember에 해당하는 블록의 정보를 가져옵니다.

![image](https://github.com/kwhong95/learn-go-ethereum/assets/70752848/fc1b9398-e4a5-4ae4-a3f9-023db5952de2)

- `miner` : coinbase
- `mixHash`, `nonce` : POW Mining 시 계산을 위해 사용하는 값
- `number` : 현재 블록이 몇 번째 블록인지 나타내는 값
- `parentHash` : 이전 블록의 해시 값
- `receiptsRoot` : 현재 블록에 포함된 트랜잭션 `receipts`을 해싱한 값
- `sha3Uncles` : 현재 블록의 Uncle 블록들의 해시 값
- `size`: 블록의 크기
- `stateRoot` : account 상태 정보가 모여 있는 머클트리의 루트 노드에 대한 해시 값
- `timestamp` : 블록이 생성된 시간; 단, 노드 환경에 따라 값이 달라져 정확하지 않을 수 있음
- `totalDifficulty` : 해당 블록까지의 난이도를 합한 값
- `transactions` : 블록에 포함된 트랜잭션
- `transactionsRoot`: 트랜잭션이 모인 머클트리 루트 노드에 대한 해시 값
- `uncles` : 현재 블록의 Uncle Block들

#### [Geth 소스 코드] Block 구조체

![image](https://github.com/kwhong95/learn-go-ethereum/assets/70752848/5f142adb-68d2-452d-96b2-cfa7ab50e09f)

이전에 봤던 구조에서 보이지 않는 부분은 대부분 `Header`에 담겨 있다.


![image](https://github.com/kwhong95/learn-go-ethereum/assets/70752848/eab5c636-5c42-4f5a-baa4-2728f42678c6)