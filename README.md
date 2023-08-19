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

## 2.5 Styles

`inline` 으로 `css` 를 계속 작성해도 되지만, 컴포넌트가 커지다 보면 가독성이 떨어진다.

이때 아래처럼 `StyleSheet` 를 분리해서 작업하면 좋다.

```js
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: 'teal',
  },
  city: {
    flex: 1.2,
    justifyContent: 'center',
    alignItems: 'center',
  },
  cityName: {
    fontSize: 68,
    fontWeight: '500',
  },
  weather: {
    flex: 3,
  },
  day: {
    flex: 1,
    alignItems: 'center',
  },
  temp: {
    marginTop: 50,
    fontSize: 178,
  },
  description: {
    marginTop: -30,
    fontSize: 60,
  },
});
```

<br>

## 2.6 Styles part Two

화면상에 View 가 많아지게 되면 자연스럽게 스크롤이 작동될거라 생각하지만 그렇지 않다.

브라우저가 아니기 때문이다.

RN 은 모든 것이 컴포넌트이기 때문에, 이러한 상황에서도 컴포넌트를 사용해야한다.

`ScrollView` 는 내부에 컴포넌트와 뷰들을 자식으로 담을 수 있는, 화면의 스크롤을 사용할 때 쓰는 컴포넌트다.

스크롤 방향은 `horizontal` 을 통해 가로 또는 세로로 변경할 수 있다.

style 을 적용할 때도 `style` 대신 `contentContainerStyle` 을 사용해야 한다.

`scrollView` 는 화면보다 더 넘어가야하기 때문에 더 커야 한다. 그래서 당연히 `flex` 가 필요없다.

스크롤의 자유도를 떨어뜨려서 자연스럽게 다음장으로 넘어가도록 하기위해, `pagingEnabled` 를 사용한다.

```js
<ScrollView pagingEnabled horizontal showsHorizontalScrollIndicator={false} contentContainerStyle={styles.weather}>
  ...
</ScrollView>
```

<br>

## 2.7 Location

현재 내 위치를 가져오기 위해 `Expo Location` 을 이용한다.

이용하기 위해서는 설치를 해야한다.

가이드를 따라 터미널에서 설치해준다.

```shell
npx expo install expo-location
```

그 후 아래의 예제처럼 권한을 얻고, 권한을 얻었을 때 진행되는 로직을 구성하면 된다.

```js
import * as Location from 'expo-location';

export default function App() {
  const [location, setLocation] = useState(null);
  const [errorMsg, setErrorMsg] = useState(null);

  useEffect(() => {
    (async () => {
      let { status } = await Location.requestForegroundPermissionsAsync();
      if (status !== 'granted') {
        setErrorMsg('Permission to access location was denied');
        return;
      }

      let location = await Location.getCurrentPositionAsync({});
      setLocation(location);
    })();
  }, []);

  let text = 'Waiting..';
  if (errorMsg) {
    text = errorMsg;
  } else if (location) {
    text = JSON.stringify(location);
  }

  return (
    <View style={styles.container}>
      <Text style={styles.paragraph}>{text}</Text>
    </View>
  );
}
```

<br>

## 2.8 Weather

OpenWeather 사이트에서 무료버전으로 날씨 관련 API 를 이용하여 데이터를 가져올 수 있다.

`https://openweathermap.org/api` 에서 가입하고 API KEY 를 발급받는다.

발급받은 API KEY 를 코드에 그대로 넣는 행위는 하면 안되지만, 여기서는 넘어간다.

(js 에서 제공하는 fetch 를 이용해서 받아올 땐 아래와 같은 방식이다.)

```js
...
const getWeather = async () => {
  const { granted } = await Location.requestForegroundPermissionsAsync();
  if (!granted) {
    setOk(false);
  }
  const {
    coords: { latitude, longitude },
  } = await Location.getCurrentPositionAsync({ accuracy: 5 });
  const location = await Location.reverseGeocodeAsync({ latitude, longitude }, { useGoogleMaps: false });
  setCity(location[0].city);

  const response = await fetch(`https://api.openweathermap.org/data/2.5/onecall?lat=${latitude}&lon=${longitude}&exclude=alerts&appid=${API_KEY}&units=metric`);
  const json = await response.json();
  setDays(json.daily);
};

useEffect(() => {
  getWeather();
}, []);
...
```

`ActivityIndicator` 를 이용해서 간단하게 `Loading` 을 구현할 수 있다.

```js
...
return (
    <View style={styles.container}>
     ...
        {days.length === 0 ? (
          <View style={styles.day}>
            <ActivityIndicator color='white' style={{ marginTop: 10 }} size='large' />
          </View>
        ) : (
          days.map((day, index) => (
            <View key={index} style={styles.day}>
              <Text style={styles.temp}>{parseFloat(day.temp.day).toFixed(1)}</Text>
              <Text style={styles.description}>{day.weather[0].main}</Text>
              <Text style={styles.tinyText}>{day.weather[0].description}</Text>
            </View>
          ))
        )}
    </View>
  );
```

<br>

## 2.9 Recap

지금까지의 간단한 작업들에서 `React` 가 아닌 `React Native` 인 것은 `Location` 의 내부 값들과, `<View>`, `<Text>`, `ActivityIndicator` 뿐이다.

그 중 `Location` 의 `reverseGeocodeAsync` 는 위도와 경도를 주소로 변환해주고, `GeocodeAsync` 는 주소를 위도, 경도 숫자로 변환해준다.

여기선 days 의 초깃값이 빈배열이지만, `response.json();` 의 결괏값이 undefined 일 때 조건 처리가 되어있지않아 api 호출이 실패했을 때 에러가 발생할 수 있을 것 같다.

Location 을 사용했을 땐 위치정보를 허용해도 샌프란시스코로 나오는 상태이기때문에, 제대로 사용하려면 다른 걸 쓰거나 좀 더 찾아봐야 할 것 같다.

<br>

## 2.10 Icons

`expo init` 명령어로 어플리케이션을 만들었다면, 이미 아이콘 패키지가 설치되어 있다.

`expo/vector-icons` 를 사용하면 아이콘 라이브러리에 접근할 수 있다.

사용법은 간단하다.

아이콘 컴포넌트와 사용할 아이콘에 대한 `props` 만 지정해주면 끝이다.

아이콘들에 대한 정보는 https://icons.expo.fyi/Index 에서 확인 가능하다.

날씨의 아이콘을 지정하려면, api 에서 제공하는 날씨에 관한 이름 정보가 모두 있어야 매칭시킬 수 있기 때문에 정리가 필요하다.

아래처럼 api 에서 제공하는 날씨의 이름을 아이콘 이름과 맞춰놓으면 날씨에 따라 아이콘이 변경되어 출력되는 것을 확인할 수 있다.

```js
const icons = {
  Clouds: 'cloudy',
  Clear: 'day-sunny',
  Atmosphere: 'cloudy-gusts',
  Snow: 'snow',
  Rain: 'rains',
  Drizzle: 'rain',
  Thunderstorm: 'lightning',
};
```

```js
...
days.map((day, index) => (
  <View key={index} style={styles.day}>
    <View
      style={{
        flexDirection: 'row',
        alignItems: 'center',
        width: '100%',
        justifyContent: 'space-between',
      }}
    >
      <Text style={styles.temp}>{parseFloat(day.temp.day).toFixed(1)}</Text>
      <Fontisto name={icons[day.weather[0].main]} size={68} color='white' />
    </View>

    <Text style={styles.description}>{day.weather[0].main}</Text>
    <Text style={styles.tinyText}>{day.weather[0].description}</Text>
  </View>
))
...
```

<br>
