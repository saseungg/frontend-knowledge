# Type과 Interface 차이점

### 1. 확장 방식

```js
interface PeopleInterface {
  name: string;
  age: number;
}

interface StudentInterface extends PeopleInterface {
  school: string;
}
```

```ts
type PeopleType = {
  name: string,
  age: number,
};

type StudentType = PeopleType & {
  school: string,
};
```

### 선언적 확장
type은 새로운 속성을 추가하기 위해서 다시 같은 이름으로 선언할 수 없지만, interface는 항상 선언적 확장이 가능하다.

```ts
interface Window {
  title: string
}

interface Window {
  ts: TypeScriptAPI
}

// 같은 interface 명으로 Window를 다시 만든다면, 자동으로 확장이 된다.

const src = 'const a = "Hello World"'
window.ts.transpileModule(src, {})
```

```ts
type Window = {
  title: string
}

type Window = {
  ts: TypeScriptAPI
}

// Error: Duplicate identifier 'Window'.
// 타입은 안된다.
```

### interface는 객체에서만 사용 가능
```ts
interface FooInterface {
  value: string
}

type FooType = {
  value: string
}

type FooOnlyString = string
type FooTypeNumber = number

// 불가능
interface X extends string {}
```
### computed value의 사용
- type은 가능하지만 interface는 불가능하다.
- computed property name은 표현식(expression)을 이용해 객체의 key 값을 정의하는 문법
- mdn 설명: 상속과정에서 부모가 자식에게 물려주는 값

```ts
type names = 'firstName' | 'lastName'

type NameTypes = {
  [key in names]: string
}

const yc: NameTypes = { firstName: 'hi', lastName: 'yc' }

interface NameInterface {
  [key in names]: string // error
}
```

## 이후 고민해볼 주제
- 타입과 인터페이스는 언제 어떻게 사용하는 것이 좋을까?
- 이 주제는 취향차이이긴한데 필자마다 다 권장하는 방식이 다름. 내가 여러 자료를 보고 판단해보면서 고르는게 맞는 것 같음
- https://careerly.co.kr/qnas/2599

## 참고

- [타입스크립트 type과 interface의 공통점과 차이점](https://yceffort.kr/2021/03/typescript-interface-vs-type)
- [나 보려고 정리하는 TypeScript 핸드북](https://velog.io/@1998yuki0331/%EB%82%98-%EB%B3%B4%EB%A0%A4%EA%B3%A0-%EC%A0%95%EB%A6%AC%ED%95%98%EB%8A%94-TypeScript-%ED%95%B8%EB%93%9C%EB%B6%81)
- [TypeScript: type과 interface는 어떻게 다를까](https://medium.com/hcleedev/typescript-type%EA%B3%BC-interface%EB%8A%94-%EC%96%B4%EB%96%BB%EA%B2%8C-%EB%8B%A4%EB%A5%BC%EA%B9%8C-c4ca65a0257)