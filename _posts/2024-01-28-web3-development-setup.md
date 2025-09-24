---
layout: post
title: "Web3 개발 환경 구축 가이드 - 완벽한 시작"
date: 2025-09-22 10:00:00 +0900
categories: [web3]
tags: [web3, ethereum, development, setup, truffle, hardhat]
description: "Web3 개발을 위한 완벽한 환경 설정과 도구 가이드입니다."
---

Web3 개발을 시작하기 위해 필요한 모든 도구와 환경을 설정하는 방법을 정리했습니다.

## 🛠️ 필수 도구 설치

### 1. Node.js 및 npm

```bash
# Node.js LTS 버전 설치 (18.x 이상 권장)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
nvm install 18
nvm use 18
```

### 2. Git 설정

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

## 🔧 개발 도구 설치

### 1. Hardhat (추천)

```bash
# 프로젝트 초기화
mkdir my-web3-project
cd my-web3-project
npm init -y

# Hardhat 설치
npm install --save-dev hardhat
npx hardhat init
```

### 2. Truffle (대안)

```bash
# Truffle 글로벌 설치
npm install -g truffle

# 프로젝트 초기화
truffle init
```

### 3. Web3 라이브러리

```bash
# Web3.js
npm install web3

# ethers.js (더 현대적)
npm install ethers

# OpenZeppelin 컨트랙트
npm install @openzeppelin/contracts
```

## 🌐 테스트넷 설정

### 1. MetaMask 설치 및 설정

1. [MetaMask](https://metamask.io/) 브라우저 확장 프로그램 설치
2. 지갑 생성 및 시드 구문 백업
3. 테스트넷 추가:
   - **Sepolia**: `https://sepolia.infura.io/v3/YOUR_PROJECT_ID`
   - **Goerli**: `https://goerli.infura.io/v3/YOUR_PROJECT_ID`

### 2. 테스트 이더 받기

- [Sepolia Faucet](https://sepoliafaucet.com/)
- [Goerli Faucet](https://goerlifaucet.com/)

## 📁 프로젝트 구조

```
my-web3-project/
├── contracts/           # 스마트 컨트랙트
│   ├── MyContract.sol
│   └── Migrations.sol
├── scripts/            # 배포 스크립트
│   └── deploy.js
├── test/               # 테스트 파일
│   └── MyContract.test.js
├── hardhat.config.js   # Hardhat 설정
└── package.json
```

## ⚙️ Hardhat 설정

```javascript
// hardhat.config.js
require("@nomicfoundation/hardhat-toolbox");

module.exports = {
  solidity: "0.8.19",
  networks: {
    sepolia: {
      url: `https://sepolia.infura.io/v3/${INFURA_PROJECT_ID}`,
      accounts: [PRIVATE_KEY]
    }
  }
};
```

## 🚀 첫 번째 스마트 컨트랙트

```solidity
// contracts/HelloWorld.sol
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract HelloWorld {
    string public message;
    
    constructor(string memory _message) {
        message = _message;
    }
    
    function updateMessage(string memory _newMessage) public {
        message = _newMessage;
    }
}
```

## 🧪 테스트 작성

```javascript
// test/HelloWorld.test.js
const { expect } = require("chai");
const { ethers } = require("hardhat");

describe("HelloWorld", function () {
  it("Should return the right message", async function () {
    const HelloWorld = await ethers.getContractFactory("HelloWorld");
    const helloWorld = await HelloWorld.deploy("Hello, Web3!");
    
    expect(await helloWorld.message()).to.equal("Hello, Web3!");
  });
});
```

## 📦 배포 스크립트

```javascript
// scripts/deploy.js
async function main() {
  const HelloWorld = await ethers.getContractFactory("HelloWorld");
  const helloWorld = await HelloWorld.deploy("Hello, Web3!");
  
  await helloWorld.deployed();
  
  console.log("HelloWorld deployed to:", helloWorld.address);
}

main()
  .then(() => process.exit(0))
  .catch((error) => {
    console.error(error);
    process.exit(1);
  });
```

## 🔍 유용한 명령어

```bash
# 컴파일
npx hardhat compile

# 테스트 실행
npx hardhat test

# 로컬 네트워크 실행
npx hardhat node

# 배포
npx hardhat run scripts/deploy.js --network sepolia

# 컨트랙트 검증
npx hardhat verify --network sepolia CONTRACT_ADDRESS "Hello, Web3!"
```

## 🛡️ 보안 체크리스트

- [ ] Private Key를 코드에 하드코딩하지 않음
- [ ] .env 파일을 .gitignore에 추가
- [ ] 테스트넷에서 충분한 테스트 수행
- [ ] OpenZeppelin 라이브러리 활용
- [ ] 코드 감사 도구 사용 (Slither, Mythril)

## 📚 추가 학습 자료

- [Hardhat Documentation](https://hardhat.org/docs)
- [OpenZeppelin Contracts](https://docs.openzeppelin.com/contracts/)
- [Ethereum Developer Resources](https://ethereum.org/en/developers/)
- [Web3.js Documentation](https://web3js.readthedocs.io/)

## 🎯 다음 단계

1. **ERC-20 토큰 구현**
2. **NFT 컬렉션 개발**
3. **DeFi 프로토콜 분석**
4. **프론트엔드 연동 (React + Web3)**

Web3 개발의 세계에 오신 것을 환영합니다! 🚀
