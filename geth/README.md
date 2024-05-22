## 01. Geth 실행 

### Geth 설치

[Geth Etherenum](https://geth.ethereum.org/downloads)에 접속해 OS에 맞는 버전 다운로드

> 다양한 언어로 구현된 클라이언트

- `Eth1`에서는 실행과 합의를 둘 다 담당했지만,
  `Eth2`에서는 실행만 담당한다.
- 합의 클라이언트가 따로 있다.
- `Eth2` 합의 클라이언트

| Client | Language | OS | Networks |
| --- | --- | --- | --- |
| [Lighthouse](https://github.com/sigp/lighthouse) | Rust | Linux, Windows, macOS | Beacon Chain, Goerli, Pyrmont, Sepolia, Ropsten, and more |
| [Lodestar](https://github.com/ChainSafe/lodestar) | Typescript | Linux, Windows, macOS | Beacon Chain, Goerli, Sepolia, Ropsten, and more | 
| [Nimbus](https://github.com/status-im/nimbus-eth2) | Nim | Linux, Windows, macOS | Beacon Chain, Goerli, Sepolia, Ropsten, and more | 
| [Prysm](https://github.com/prysmaticlabs/prysm) | Go | Linux, Windows, macOS | Beacon Chain, Gnosis, Goerli, Pyrmont, Sepolia, Ropsten, and more | 
| [Teku](https://github.com/Consensys/teku) | Java | Linux, Windows, macOS | Beacon Chain, Gnosis, Goerli, Sepolia, Ropsten, and more | 


-----

1. Private 네트워크 실행을 위해 `genesis.json` 파일 생성

```json
{
  "config": {
    "chainId": 12345,
    "homesteadBlock": 0,
    "eip150Block": 0,
    "eip155Block": 0,
    "eip158Block": 0,
    "byzantiumBlock": 0,
    "constantinopleBlock": 0,
    "petersburgBlock": 0,
    "istanbulBlock": 0,
    "berlinBlock": 0,
    "clique": {
      "period": 5,
      "epoch": 30000
    }
  },
  "difficulty": "1",
  "gasLimit": "8000000",
  "alloc": {
    "7df9a875a174b3bc565e6424a0050ebc1b2d1d82": { "balance": "300000" },
    "f41c74c9ae680c1aa78f42e5647a62f353b7bdde": { "balance": "400000" }
  },
}
```

- `conig` : `chainId`와 합의 알고리즘, 하드포크 등을 설정할 수 있다.
- `difficulty` : 블록 생성 시의 난이도 (숫자가 높을수록 사용해야 하는 리소스가 증가)
- `gasLimit` : 블록 당 최대 가스 사용량 (숫자가 높을수록 블록에 더 많은 트랜잭션을 넣을 수 있음)
- `alloc`: 제네시스 블록에 미리 설정된 계정 (해당 계정은 미리 설정된 이더를 가짐)

2. 체인 스토리지 초기화

```bash
./geth --datadir ./data init ./genesis.json
```

3. Geth 실행

```bash
./geth --datadir ./data --http --http.api "admin, web3, eth, personal" console
```

- JS 콘솔도 같이 실행

<img width="403" alt="스크린샷 2024-05-23 01 39 11" src="https://github.com/kwhong95/learn-go-ethereum/assets/70752848/9c95e3d3-715d-43fc-932a-470b5dbed5d3">

- 노드 관련 실행 로그가 계속 업데이트
<img width="685" alt="스크린샷 2024-05-23 02 59 41" src="https://github.com/kwhong95/learn-go-ethereum/assets/70752848/0ab91e38-3cb7-4377-b256-931413800756">

4. `attach` 명령어로 커맨드를 입력할 수 있는 콘솔 생성

```bash
./geth attach http://127.0.0.1:8545
```

<img width="503" alt="스크린샷 2024-05-23 03 05 22" src="https://github.com/kwhong95/learn-go-ethereum/assets/70752848/8f9f2685-7582-41c1-b0d1-acdba37530e8">
