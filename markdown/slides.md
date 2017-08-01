layout: true

---
class: middle, center, general
# React Native
## Desarrolla Aplicaciones Nativas usando JS
Una pequeña charla por [Carlos González](http://caal-15.github.io)

Síguela en [caal-15.github.io/react-native-talk](http://caal-15.github.io/react-native-talk)
.footnote[.alt-link[[Sitio de React Native](https://facebook.github.io/react-native/)]]

---
class: left, middle

# ¿Qué Es?

.big[Es un _Framework_, para construir aplicaciones nativas usando _React_ y
_JavaScript_.]

---
class: center, middle

# Diferencias con otros Frameworks

.big[
* Los Componentes Visuales renderizados son _nativos_ de cada Plataforma.
* No hay acceso a _HTML_ ni a _CSS_, sólo a un intérprete de _JavaScript_.
* No depende de un _Webview_.
]

---
class: left middle

# Ventajas

.big[
* __Performance:__  Al usar Componentes de UI _nativos_ de cada plataforma y no
un _Webview_ para renderizar, el desempeño de la aplicación mejora
considerablemente.

* __Redux:__ El _flujo de datos_ de la aplicación puede manejarse usando redux
haciéndo los estados de la aplicación más predecibles y fáciles de diseñar.

* __Modularidad:__ Como en _React_, los Componentes desarrollados pueden ser
altamente reutilizables.

* __Integración:__ Al sólo utilizar el intérprete de _JavaScript_ y componentes
de UI nativos, se facilita la utilización de _código nativo_
(Swift, Java, etc.).
]

.footnote[.alt-link[[Comparativa de desempeño con Swift](https://medium.com/the-react-native-log/comparing-the-performance-between-native-ios-swift-and-react-native-7b5490d363e2)]]

---
class: left, middle

# Arquitectura Híbrida

![React Native Architecture](img/arch-cordova.png)

---
class: left, middle

# Arquitectura RN

![React Native Architecture](img/arch.png)

---
class: center, middle

# ¿Cómo Funciona?

---
class: left, middle

# Componentes

.big[Tal y como los _tags HTML_ son los bloques base de React, React Native
provee _Componentes Nativos_ que cumplen esa misma función.]

```javascript
import React from 'react'
import { View, Text } from 'react-native'

export default function HelloComponent () {
  return (
    <View>
      <Text>Hello!</Text>
    </View>
  )
}
```

---
class: left, middle

# Estilos

.big[React Native provee una implementación de estilos similar a los
_inline styles_ de React, el layout se puede hacer utilizando flex:]

```javascript
export default function HelloComponent () {
  const contStyle = {
    flex: 1,
    backgroundColor: 'blue'
  }
  return (
    <View style={contStyle}>
      <Text>Hello!</Text>
    </View>
  )
}
```

---
class: left, middle

# State y Props

.big[El manejo de _State_ y _Props_ sigue siendo el mismo de React.]

```javascript
class AwesomeHello extends Component {
  constructor (props) {
    super(props)
    this.state = { iHaveState: true }
  }
  render () {
    const { iHaveProps } = this.props
    const { iHaveState } = this.state
    ...
  }
}
```

---
class: center, middle

# ¿Cómo Empezar?

---
class: left, middle

# Create React Native App

.big[Una colaboración entre _Expo_ y los desarrolladores de React Native, no
requiere una instalación de _Android Studio_ o _Xcode_, simplemente instala
_Expo Client_ en tu dispositivo iOS o Android, y en tu PC.]

```bash
npm install -g create-react-native-app
create-react-native-app myApp && cd myApp
npm start
```

.big[Escanea el código de barras que aparece en pantalla con _Expo Client_ y
estás listo para empezar!.]

---
class: center, middle

# Consideraciones Adicionales

---
class: left, middle

# Flujo de Datos (Redux)

.big[Si bien la aplicación se podría manejar a través de _State_ y _Props_,
React Native es completamente compatible con _Redux_ y _React Redux_, con
lo que los pasos para implementarlo son exactamente iguales.]

---
class: left, middle

# Los Reducers

```javascript
const initialState = {
  saidHello: false,
  phrase: 'Hello'
}
function reducer (state=initialState, action) {
  switch action.type {
    case 'SAID_HELLO':
      return Object.assign({}, state, {
        saidHello: true
      })
    ...
  }
}
```

---
class: left, middle

# La Store

```javascript
import { createStore } from 'redux'

export default store = createStore (
  reducer,
  undefined
  ...
)  
```

---
class: left, middle

# Junto a RN

.big[En el componente Raíz]

```javascript
import { Provider } from 'react-redux'
import store from './store'
import Hello from './Hello'

export default function HelloApp() {
  return (
    <Provider store={store}>
      <Hello />
    </Provider>
  )
}
```

---
class: left, middle

.big[En el componente Hello]

```javascript
import { connect } from 'react-redux'

class Hello extends Component {
  componentWillMount () {
    this.props.dispatch({ type: 'SAID_HELLO' })
  }
  ...
}

function mapStateToProps (state) {
  return { saidHello: state.saidHello }
}

export default connect(mapStateToProps)(Hello)
```

---
class: left, middle

# Navegación

.big[_React Navigation_ provee una manera sencilla de navegar entre pantallas,
un ejemplo:]

```javascript
import {StackNavigator} from 'react-navigation'
import Login from './Login'
import Home from './Home'

export default Navigator = StackNavigator ({
  Login: { screen: Login },
  Home: { screen: Home }
})
```

---
class: left, middle

# En el Componente Raíz

```javascript
import Navigator from './Navigator'

export default function App () {
  return (
    <Navigator />
  )
}
```
---
class: left, middle

# Despachando Navegación desde un componente

```javascript
class Login extends Component {
  ...
  componentDidUpdate () {
    const { user, navigation } = this.props
    if (user) {
      navigation.navigate('Home')
    }
  }
  ...
}
```

---
class: left, middle

# Otras Consideraciones

.big[

* ¿Dónde están mis requests?
  *  RN incluye la API _fetch_.

* No me gusta fetch >:(
  * Se puede usar la API _XMLHttpRequest_ y también librerías construidas sobre
  ella, como _superagent_.

* ¿Puedo usar otras librerías de _JavaScript_ en React Native?
  * Si, mientras no actúen sobre el DOM y no lo requieran para funcionar (es
    decir, mientras trabajen solo usando JS), un ejemplo de esto es _moment.js_.
]

---
class: center, middle

# Gracias por su atención!
