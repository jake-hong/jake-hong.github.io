---
layout: post
title: "JavaScript Closure 완벽 이해하기"
date: 2025-09-10 11:00:00 +0900
categories: [javascript]
tags: [javascript, closure, fundamentals]
description: "JavaScript의 클로저 개념을 예제와 함께 정리했습니다."
---

## Closure란?

클로저는 함수와 그 함수가 선언될 당시의 렉시컬 환경의 조합이다.

### 기본 예제

```javascript
function outerFunction(x) {
  // 외부 함수의 변수

  function innerFunction(y) {
    // 내부 함수에서 외부 함수의 변수에 접근
    console.log(x + y);
  }

  return innerFunction;
}

const myFunction = outerFunction(10);
myFunction(5); // 15
```

### 실용적인 활용

```javascript
function createCounter() {
  let count = 0;

  return {
    increment: () => ++count,
    decrement: () => --count,
    value: () => count
  };
}

const counter = createCounter();
console.log(counter.increment()); // 1
console.log(counter.increment()); // 2
console.log(counter.value()); // 2
```

클로저를 이용하면 private 변수를 만들 수 있다!