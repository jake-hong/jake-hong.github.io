---
layout: post
title: "Solidity 기본 문법과 스마트 컨트랙트 구조"
date: 2025-09-05 10:00:00 +0900
categories: [blockchain]
tags: [solidity, ethereum, smart-contract, web3]
description: "Solidity의 기본 문법과 스마트 컨트랙트 구조를 정리했습니다."
---

## 오늘 배운 것

### 1. Solidity 기본 문법

```solidity
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

### 2. 주요 데이터 타입

- **uint**: 양의 정수 (uint8, uint256 등)
- **int**: 정수 (int8, int256 등)
- **bool**: 불린값
- **address**: 이더리움 주소
- **string**: 문자열
- **bytes**: 바이트 배열

### 3. 함수 제어자

- **public**: 외부에서 호출 가능
- **private**: 컨트랙트 내부에서만 호출 가능
- **internal**: 상속받은 컨트랙트에서도 호출 가능
- **external**: 외부에서만 호출 가능

### 4. 상태 변수 제어자

- **view**: 상태를 읽기만 함
- **pure**: 상태를 읽거나 쓰지 않음
- **payable**: 이더를 받을 수 있음

## 핵심 포인트

1. **가스 최적화**: 불필요한 연산을 피하고 효율적인 코드 작성
2. **보안**: 재진입 공격, 오버플로우 등 보안 취약점 주의
3. **이벤트**: 중요한 상태 변화를 로그로 기록

## 다음 학습 계획

- OpenZeppelin 라이브러리 사용법
- ERC-20 토큰 구현
- DeFi 프로토콜 분석