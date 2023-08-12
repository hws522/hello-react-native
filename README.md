# hello-react-native

<br>

## 2.0 Snack

Snack 은 브라우저에서 React application 을 만들 수 있게 해주는 온라인 코드에디터다.

브라우저만 사용할 수 있을 때 쓰면 좋다.

폰에 `expo` 를 설치했다면 QR 로 화면을 띄울 수도 있다.

난 안쓸거니까 넘어간다.

https://snack.expo.dev

<br>

## 2.1 The Rules of Native

react native는 웹사이트가 아니다. HTML이 아니기 때문에 div를 쓸 수 없고, View를 써야한다. (`import { StyleSheet, Text, View } from 'react-native'`)

View는 container 다.

react native 에 있는 모든 text 는 `<Text> component` 에 들어가야 한다.

웹의 react.js 에서 처럼 inline style 을 적용가능하다. (일부는 불가능)

StyleSheet.create 는 styles object 를 생성하는 데 사용한다. 이에 대한 장점은 아래와 같다.

- css 자동 완성 기능 제공

- 따로 구분함으로 인해 style 이 거대해지는 걸 방지 (따라서 일반적으로 스타일을 StyleSheet 에 구분하고 component 를 위에 써줌)

<br>

## 2.2 React Native Packages

이전 RN 은 지금보다 훨씬 많은 APIs 와 components 들을 제공했다.

하지만 많은 버그들과 모든 components 를 지원하는게 어렵다는 것을 깨달았고,

현재는 가장 필수적인 것들만 놔두고 모두 사라졌다.

유지 관리와 업데이트를 위해 지원하는 범위를 줄였다.

<br>

## 2.3 Third Party Packages

`Expo` 에도 `StatusBar` 가 있고, `RN` 에도 `StatusBar` 가 있다.

그 이유는 커뮤니티에서 자체적으로 `Packages` 를 만드려는 노력이 있기 때문이다. 특히 `Expo` 가 그렇다.

`Expo` 는 우리가 사용할 수 있는 모든 API 와 Packages 를 만들고 지원한다.

`RN` 이 독자적으로 제공하지 않는 것들도 `Expo` 에서 지원한다.

대부분의 필수 패키지는 `Expo` 가 만들어서 사용할 수 있다.

커뮤니티에서 개발된 패키지들보다 훨씬 안정적이다.

React Native Doc
https://reactnative.dev/docs/0.60/components-and-apis

React Native Directory
https://reactnative.directory/

Expo Doc
https://docs.expo.dev/versions/latest/

<br>

## 2.4 Layout System

`RN` 에서 레이아웃을 만들려면 `Flexbox` 를 사용해야 한다.

`web` 에서와 거의 비슷한데 몇가지 차이가 있다.

`display: block, inline-block, grid` 항목 같은 것들이 없다.

기본적으로 `모든 View 는 Flex Container` 다.

그래서 `flexDirection: 'row'` 한줄이면 된다. `display: 'flex'` 를 안해도 된다.

그리고 `web` 에서는 `Flex Direction` 의 기본값은 `Row` 지만, `RN` 에서는 `Flex Direction` 의 기본값은 `Column` 이다.

RN app 을 만들 때, 스크린 사이즈는 매우 다양하기 때문에 반응형을 항상 고려해야한다.

그래서 대부분의 경우 width 나 height 를 사용하지 않는다.

`RN` 의 방식으로 레이아웃을 구성할텐데, `RN` 에서는 숫자만 생각하면 된다.

`flex: 1` 처럼 비율로 표현한다.

```js
export default function App() {
  return (
    <View style={{ flex: 1, flexDirection: 'row' }}>
      <View style={{ flex: 1, backgroundColor: 'tomato' }}></View>
      <View style={{ flex: 1, backgroundColor: 'teal' }}></View>
      <View style={{ flex: 1, backgroundColor: 'orange' }}></View>
    </View>
  );
}
```

위처럼 비율로 정해지기 때문에, 부모 컴포넌트의 Flex 가 매우 중요하다.

위 부모의 flex 가 1 이 아니라, 4 든 5 든 비율에 변동이 없다.

이유는, View 가 하나 있기 때문에 계산할 비율이 없다. 동일한 스크린의 4 배 5 배가 되기에 변화가 없다.

부모 View 옆에 다른 View 가 또 있다면 달라질 수 있다. 아래 자식 View 처럼.
<br>
