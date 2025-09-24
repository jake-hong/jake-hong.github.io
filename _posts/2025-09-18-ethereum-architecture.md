---
layout: post
title: "이더리움 아키텍처와 EVM 동작 원리"
date: 2025-09-18 16:00:00 +0900
categories: [blockchain]
tags: [ethereum, evm, blockchain, architecture, web3]
description: "이더리움의 핵심 구조와 EVM의 동작 원리를 깊이 있게 분석합니다."
---

## 이더리움 아키텍처 개요

이더리움은 단순한 암호화폐가 아닌 **분산 컴퓨팅 플랫폼**입니다. 스마트 컨트랙트를 실행할 수 있는 가상 머신인 EVM(Ethereum Virtual Machine)을 중심으로 구성되어 있습니다.

## EVM (Ethereum Virtual Machine)

### 1. EVM의 역할

- **스마트 컨트랙트 실행**: Solidity로 작성된 코드를 바이트코드로 컴파일하여 실행
- **가스 계산**: 연산 비용을 가스 단위로 측정
- **상태 관리**: 블록체인의 상태를 저장하고 업데이트

### 2. EVM 스택 구조

```
┌─────────────────┐
│   Stack (1024)  │ ← 연산에 사용되는 임시 데이터
├─────────────────┤
│   Memory        │ ← 함수 호출 중 임시 저장소
├─────────────────┤
│   Storage       │ ← 영구 저장소 (가장 비쌈)
├─────────────────┤
│   Calldata      │ ← 함수 호출 시 전달된 데이터
└─────────────────┘
```

### 3. 가스 메커니즘

```solidity
// 가스 소비 예시
uint256 public value;  // Storage: 20,000 gas
function setValue(uint256 _value) public {
    value = _value;    // Storage write: 20,000 gas
}
```

## 이더리움 네트워크 구조

### 1. 노드 유형

- **Full Node**: 전체 블록체인 데이터 저장
- **Archive Node**: 모든 과거 상태 저장
- **Light Node**: 헤더만 저장 (SPV)

### 2. 합의 메커니즘

**이전 (PoW)**:
- 마이너들이 해시 퍼즐을 풀어 블록 생성
- 높은 에너지 소비, 느린 처리 속도

**현재 (PoS)**:
- 검증자들이 ETH를 스테이킹하여 블록 검증
- 에너지 효율적, 빠른 처리 속도

## 트랜잭션 처리 과정

1. **트랜잭션 생성**: 사용자가 서명하여 생성
2. **메모리 풀**: 대기 중인 트랜잭션들
3. **블록 생성**: 검증자가 트랜잭션들을 블록에 포함
4. **실행**: EVM에서 스마트 컨트랙트 실행
5. **상태 업데이트**: 결과를 블록체인에 기록

## 실제 구현 예시

### 간단한 스마트 컨트랙트

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SimpleStorage {
    uint256 private storedData;

    event DataStored(uint256 indexed data);

    function set(uint256 x) public {
        storedData = x;
        emit DataStored(x);
    }

    function get() public view returns (uint256) {
        return storedData;
    }
}
```

## 최적화 전략

### 1. 가스 최적화

- **Packed Structs**: 여러 변수를 하나의 슬롯에 저장
- **Events**: 로그는 Storage보다 저렴
- **Libraries**: 재사용 가능한 코드 분리

### 2. 보안 고려사항

- **Reentrancy**: 재진입 공격 방지
- **Integer Overflow**: SafeMath 사용
- **Access Control**: 적절한 권한 관리

## 성능 비교

| 특성 | 이더리움 | Polygon | Arbitrum |
|------|----------|---------|----------|
| TPS | ~15 | ~7,000 | ~4,000 |
| 가스비 | 높음 | 낮음 | 낮음 |
| 보안 | 높음 | 중간 | 높음 |

## 미래 전망

- **EIP-4844 (Proto-Danksharding)**: L2 확장성 개선
- **Account Abstraction**: 사용자 경험 향상
- **Zero-Knowledge Proofs**: 프라이버시 강화