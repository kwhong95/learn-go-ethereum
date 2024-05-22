## 02. 기본 명령어

### 1. account

1. 새로운 계정 생성

- geth 파일이 있는 디렉토리에서 다음과 같은 명령어를 실행

```bash 
./geth --datadir ./data account new   
```

- 비밀번호와 비밀번호 확인을 입력

```
Your new account is locked with a password. Please give a password. Do not forget this password.
Password: 

.
.
.

Repeat password: 
```

정상적으로 계정이 생성된 후,

`./data/keystore/` 내부에 계정이 생성된 걸 확인

```
Your new key was generated

Public address of the key:   0x2Cba5d138deb46078eb02e92CCe6D7190766CD72
Path of the secret key file: data/keystore/UTC--2024-05-22T18-20-59.483096000Z--2cba5d138deb46078eb02e92cce6d7190766cd72
```


2. 계정 비밀번호 변경

가장 처음으로 만든 계정이므로 0번 인덱스 지정

```bash
./geth --datadir ./data account update 0  
```

기존에 생성할 때 입력한 비밀번호를 입력

```bash
Unlocking account 0 | Attempt 1/3
Password: 
```

새로운 비밀번호를 설정

```bash
INFO [05-23|03:43:03.025] Unlocked account                         address=0x2Cba5d138deb46078eb02e92CCe6D7190766CD72
Please give a new password. Do not forget this password.
Password: 
Repeat password: 
```

3. 계정 리스트 확인

먼저 리스트를 확인하기 전에 계정을 1개 더 생성해봅니다.

다음 명령어로 계정 리스트를 확인할 수 있습니다.

```bash
./geth --datadir ./data account list
```

가장 최근 계정부터 리스트가 출력됩니다.

```bash
INFO [05-23|03:48:06.814] Maximum peer count                       ETH=50 total=50
Account #0: {2cba5d138deb46078eb02e92cce6d7190766cd72} keystore:///Users/kwhong95/sources/learn-go-ethereum/basic-command/data/keystore/UTC--2024-05-22T18-20-59.483096000Z--2cba5d138deb46078eb02e92cce6d7190766cd72
Account #1: {5546df6faa763f79f3985b88112dfa19e0ca461c} keystore:///Users/kwhong95/sources/learn-go-ethereum/basic-command/data/keystore/UTC--2024-05-22T18-48-01.770515000Z--5546df6faa763f79f3985b88112dfa19e0ca461c
```

### 2. attach

먼저, geth 실행 

```bash
./geth --datadir ./data --http --http.api "admin, web3, eth, personal" console
```

`attach` 명령어로 접근

```bash
./geth attach http://127.0.0.1:<Endpoint>
```

다음과 같이 노드에 접근해 콘솔창 활용 가능

``` bash
Welcome to the Geth JavaScript console!

instance: Geth/v1.13.15-stable-c5ba367e/darwin-amd64/go1.21.6
at block: 0 (Thu Jan 01 1970 09:00:00 GMT+0900 (KST))
 datadir: /Users/kwhong95/sources/learn-go-ethereum/basic-command/data
 modules: admin:1.0 eth:1.0 personal:1.0 rpc:1.0 web3:1.0

To exit, press ctrl-d or type exit
> 
```


### 3. config

> 설정파일을 지정하여 geth 실행

```bash
./geth --config ./geth-config.toml
```

![image](https://github.com/kwhong95/learn-go-ethereum/assets/70752848/ad5ac4d9-9f9d-4d71-ba11-f66237ec4cc4)


### 4. datadir

> geth 실행 시 체인 데이터를 저장하는 디렉토리 지정

```bash
./geth --datadir ./data
```

### 5. syncmode, gcmode

> geth로 노드를 실행할 때 네트워크에 참여하는 방식을 지정

```bash
./geth --syncmode "full"
./geth --syncmode "snap"
./geth --syncmode "light"
```

```bash
./geth --gcmode "archive"
```

### 6. network

> 네트워크 지정

```bash
./geth --mainnet ## default
./geth --goerli 
./geth --sepolia 
```

### 7. unlock

> geth에서 사용할 address 활성화

```bash
./geth --unlock 0
./geth --unlock 0 --password ./password
./geth --allow-insecure-unlock
```

### 8. 통신

> 외부에서 http, websocket 통신으로 geth에 접근할 수 있도록 설정

```bash
./geth --http
./geth --http.api "admin, web3, eth, txpool, personal, ethash, miner, net" 
./geth --http.corsdomain "*"
./geth --http.addr "0.0.0.0"
./geth --http.port "8545"
```

```bash
./geth --ws
./geth --ws.api "admin, web3, eth, txpool, personal, ethash, miner, net"
./geth --ws.origins "*"
./geth --ws.addr "0.0.0.0"
./geth --ws.pot "8546"
```

### 9. reset, backup

```bash
./geth removedb
```

```bash 
./geth export ./backup 0 1000 
./geth import ./backup
```

### console command 

> 자주 사용하는 eth method

<img width="865" alt="스크린샷 2024-05-23 05 37 16" src="https://github.com/kwhong95/learn-go-ethereum/assets/70752848/30bd9559-0d89-41fd-acf8-0b74b1113d18">

