---
layout: post
title: "React Hooks 실무에서 유용한 팁들"
date: 2025-09-15 14:30:00 +0900
categories: [react, frontend]
description: "React Hooks를 더 효율적으로 사용하는 방법들을 실제 예시와 함께 정리했습니다."
---

## React Hooks 최적화 팁

React Hooks를 사용하면서 성능과 코드 품질을 개선할 수 있는 실무 팁들을 정리해보았습니다.

### 1. useCallback으로 불필요한 리렌더링 방지

```javascript
// ❌ 매번 새로운 함수가 생성됨
const handleClick = () => {
  setCount(count + 1);
};

// ✅ 의존성 배열로 최적화
const handleClick = useCallback(() => {
  setCount(prev => prev + 1);
}, []);
```

### 2. useMemo로 무거운 계산 최적화

```javascript
const ExpensiveComponent = ({ items }) => {
  const expensiveValue = useMemo(() => {
    return items.reduce((acc, item) => acc + item.value, 0);
  }, [items]);

  return <div>총합: {expensiveValue}</div>;
};
```

### 3. 커스텀 Hook으로 로직 분리

```javascript
// useLocalStorage 커스텀 Hook
function useLocalStorage(key, initialValue) {
  const [storedValue, setStoredValue] = useState(() => {
    try {
      const item = window.localStorage.getItem(key);
      return item ? JSON.parse(item) : initialValue;
    } catch (error) {
      return initialValue;
    }
  });

  const setValue = (value) => {
    try {
      setStoredValue(value);
      window.localStorage.setItem(key, JSON.stringify(value));
    } catch (error) {
      console.error(error);
    }
  };

  return [storedValue, setValue];
}
```

### 4. useReducer로 복잡한 상태 관리

```javascript
const initialState = { count: 0, step: 1 };

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { ...state, count: state.count + state.step };
    case 'decrement':
      return { ...state, count: state.count - state.step };
    case 'setStep':
      return { ...state, step: action.step };
    default:
      return state;
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      Count: {state.count}
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
    </div>
  );
}
```

### 마무리

이런 최적화 기법들을 적절히 사용하면 더 나은 React 애플리케이션을 만들 수 있습니다. 하지만 과도한 최적화는 오히려 코드를 복잡하게 만들 수 있으니, 필요한 곳에만 적용하는 것이 중요합니다.