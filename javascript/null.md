## Object 객체

거의 대부분의 자바스크립트 객체는 자바스크립트의 [Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) 객체를 주형으로 하고, 이를 프로토타입으로 두는 구조를 갖고 있다.

프로토타입 체이닝에 의해서 프로토타입이 Object 객체가 아니라면, 프로토타입의 프로토타입을 타고 체이닝의 최종점으로 가면 대부분의 자바스크립트 객체는 Object 객체를 프로토타입으로 둔다.

`Object` 객체를 프로토타입으로 두지 않는 경우는 `null`을 프로토타입으로 두고 새로운 객체를 생성했을 경우이다. 자바스크립트에서 `typeof null`이라고 하면, 오브젝트임을 알 수 있는데, 자바스크립트에서 `null`은 오브젝트에 해당한다.

자바스크립트의 일반 객체의 프로토타입의 최종 도착점인 `Object` 객체의 프로토타입 객체는 `null`이다. 이러한 사실을 통해서 알 수 있는 것은 자바스크립트에서 `null`은 더 이상 프로토타입이 없는 객체라는 것이다.

하지만 null은 자바스크립트 타입 정의상 객체로 분류되어 있지만, null을 프로토타입으로 한 오브젝트 생성 문법은 제한적이다. 일반적으로 new 키워드에 오브젝트를 붙여 주면, 주어진 오브젝트를 프로토타입으로 하는 새로운 객체가 생성된다. `new null`을 하면 `Uncaught TypeError: null is not a constructor`라는 에러가 반환된다.

자바스크립트에서 `new` 키워드로 객체를 생성하기 위해서는 주형이 되는 객체에 `constructor`라는 메소드가 정의되어 있어야 하는데, 만약 이 메소드가 없다면 `new` 키워드로 객체를 생성할 수 없다. null은 객체이지만, 아무런 멤버가 존재하지 않기 때문에 `new` 키워드로는 `null`을 주형으로 한 오브젝트를 생성할 수 없다.

하지만 [Object.create](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/create)라는 함수를 사용하면, 프로토타입이 null인 객체를 생성할 수 있으며, 이 객체도 `constructor`는 없기 때문에 이 객체를 프로토타입으로 하는 객체에 `constructor` 메소드를 정의하지 않으면 `new` 키워드로 객체를 생성할 수 없다.
