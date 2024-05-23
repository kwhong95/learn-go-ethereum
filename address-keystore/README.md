## address와 keystore

> 보통 블록체인은 분산원장기술로 코인이나 자산을 송금하고 받을 때 사용


- `0x`로 시작하며 40자리의 16진수로 이루어짐
- [SECP256K1 타원곡선(디지털 서명 알고리즘)](https://m.blog.naver.com/aepkoreanet/221178375642)을 사용해 생성 → **Generator point(G)**
- K: 공개키, k: 개인키, G: 생성자점 
  - `K = k * G `
  - 즉, 공개키를 공개해도 개인키를 알 수 없음
- Address 생성
  - 개인키에서 파생된 공개키를 [Keccak-256](http://wiki.hash.kr/index.php/Keccak-256)으로 해싱하면 나오는 값의 끝 20Byte가 Address 값이 된다.
  - 즉, Address는 공개키에서 파생된 값
  - 노드 콘솔에서 `personal.newAccount("<Password>")` → Address 생성

  ![image](https://github.com/kwhong95/learn-go-ethereum/assets/70752848/81045f5c-7e0b-4ad1-8fc7-075164d5bf5d)


#### keystore(키스토어) - Wallet

![image](https://github.com/kwhong95/learn-go-ethereum/assets/70752848/dfed9df9-48c5-4fc8-96fb-466674c7bed8)

- `address` : 생성한 지갑의 주소
- `cipher` : 개인 키 암호화에 사용한 알고리즘
- `ciphertext` : 암호화 된 개인키
- `cipherparams` : 암호화 알고리즘에 사용한 매개변수
- `kdf` : keystore 암호화에 사용한 알고리즘
- `kdfparams` : `kdf` 암호화에 필요한 파라미터
- `mac` : keystore 의 Password를 암호화한 값과 개인 키를 암호화한 값을 해싱한 값(사용자 검증)

