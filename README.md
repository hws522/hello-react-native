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

- react native는 웹사이트가 아니다. HTML이 아니기 때문에 div를 쓸 수 없고, View를 써야한다. (`import { StyleSheet, Text, View } from 'react-native'`)

- View는 container 다.

- react native 에 있는 모든 text 는 `<Text> component` 에 들어가야 한다.

- 웹의 react.js 에서 처럼 inline style 을 적용가능하다. (일부는 불가능)

- StyleSheet.create 는 styles object 를 생성하는 데 사용한다.

  - css 자동 완성 기능 제공

  - 따로 구분함으로 인해 style 이 거대해지는 걸 방지 (따라서 일반적으로 스타일을 StyleSheet 에 구분하고 component 를 위에 써줌)

<br>
