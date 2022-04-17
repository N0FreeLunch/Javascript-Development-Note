## applySpec
- R.applySpec

## 표현
```
{k: ((a, b, …, m) → v)} → ((a, b, …, m) → {k: v})
```


## 설명



## 예제
```
const getMetrics = R.applySpec({
  sum: R.add,
  nested: { mul: R.multiply }
});
getMetrics(2, 4); // => { sum: 6, nested: { mul: 8 } }
```
