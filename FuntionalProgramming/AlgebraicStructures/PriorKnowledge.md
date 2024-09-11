# 사전지식

## [General](https://github.com/fantasyland/fantasy-land?tab=readme-ov-file#general)
> An algebra is a set of values, a set of operators that it is closed under and some laws it must obey.
- 대수란 값들의 집합을 의미한다. 연산자들의 집합은 닫혀있고, 따라야 할 몇 가지 법칙이 있다.

> Each Fantasy Land algebra is a separate specification. An algebra may have dependencies on other algebras which must be implemented.
- 각각의 판타지 렌드의 대수는 서로 다른 개념의 사양이다. 어떤 대수가 다른 대수에 종속성을 갖는다면 (종속성을 갖는 대상은) 구현되어야 한다.

## [terminology](https://github.com/fantasyland/fantasy-land?tab=readme-ov-file#terminology)
> 1. "value" is any JavaScript value, including any which have the structures defined below.
- 값("value")라는 개념은 자바스크립트의 값의 모든 형태를 가리킨다. 아래와 같이 정의되는 어떠한 구조도 포함된다.
> 2. "equivalent" is an appropriate definition of equivalence for the given value. The definition should ensure that the two values can be safely swapped out in a program that respects abstractions. For example:
- 동등성("equivalent")이란 개념은 주어진 값에 대해 '같다'(equivalence)의 적절한 정의이다. 이 정의는 대수적 양상의 프로그램 안에서는 두 값을 서로 완전히 교체할 수 있다는 의미이다. 예를 들어
> - Two lists are equivalent if they are equivalent at all indices.
- 두 리스트는 모든 인덱스에서 동일하면 동일하다.
> - Two plain old JavaScript objects, interpreted as dictionaries, are equivalent when they are equivalent for all keys.
- 딕셔너리로 해석이 되는 두 자바스크립트의 플레인 오브젝트(구 개념의)는 모든 키들에 대해 동일하면 동일하다.
> - Two promises are equivalent when they yield equivalent values.
- 두 프로미스는 값들이 동일 값을 산출(yield)하면 동일하다.
> - Two functions are equivalent if they yield equivalent outputs for equivalent inputs.
- 두 함수는 동일한 인풋에 대하여 동일한 아웃풋을 산출(yield)하면 동등하다.
