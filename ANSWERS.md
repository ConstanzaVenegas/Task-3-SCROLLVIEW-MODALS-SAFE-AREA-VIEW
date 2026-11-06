# Task 3 — Respuestas

## 1. ¿Qué hace la prop `visible` de `Modal` y por qué la controlamos con `useState`?

La prop `visible` decide si el modal se muestra (`true`) o se oculta (`false`). La controlamos con `useState` porque React solo actualiza la pantalla cuando cambia el estado. Si usara una variable normal, el modal no se abriría ni se cerraría al presionar el botón. En mi app, `setModalVisible(true)` lo abre y `closeModal` lo cierra.

## 2. ¿Para qué sirve `onRequestClose`? ¿Qué pasa en Android si no cierras el modal ahí?

`onRequestClose` es la función que se ejecuta cuando el usuario presiona el botón *atrás* de Android mientras el modal está abierto. Si no cerramos el modal dentro de ella, el botón atrás no hace nada y el modal sigue abierto, así que el usuario se siente atrapado. En el Paso 1 solo mostraba una alerta, y en el Paso 2 lo cambié a `onRequestClose={closeModal}` para que cierre bien.

## 3. ¿Qué efecto tiene `transparent={true}`? Nombra los tres valores de `animationType`.

Con `transparent={true}` el fondo del modal es transparente, así que se sigue viendo la app detrás. Esto me permite hacer un overlay oscuro semitransparente con una tarjeta blanca encima. Sin esa prop, el modal cubre toda la pantalla con fondo blanco. Los tres valores de `animationType` son `none`, `slide` y `fade`.

## 4. ¿Por qué existe `ScrollView`? ¿Qué pasa con un `View` largo sin él? ¿Cuándo elegirías `FlatList`?

`ScrollView` existe para que el usuario pueda desplazar contenido que es más grande que la pantalla. Un `View` largo sin él no hace scroll, así que lo que no cabe se corta y el usuario no puede verlo. Elegiría `FlatList` para listas largas (cientos de elementos o datos de una API), porque solo renderiza los elementos que se ven, mientras que `ScrollView` renderiza todos de una vez.

## 5. ¿Cuál es la diferencia entre las props `style` y `contentContainerStyle` de un `ScrollView`?

`style` se aplica al `ScrollView` en sí, el contenedor externo, para cosas como su tamaño, `flex`, `maxHeight` o color de fondo. `contentContainerStyle` se aplica al contenedor interno que guarda a los hijos, para cosas como padding, `gap` o alineación. En mi app, `styles.contactList` (con `maxHeight`) va en `style`, y `styles.projectsRow` (con `gap` y `paddingRight`) va en `contentContainerStyle`.

## 6. ¿Para qué sirve `SafeAreaView` y qué zonas del dispositivo protege? ¿Por qué usamos `react-native-safe-area-context`?

`SafeAreaView` agrega el padding necesario para que el contenido no quede debajo de las partes de la pantalla que tapa el dispositivo. Protege el notch o la cámara frontal, la barra de estado, el indicador de inicio o la barra de navegación de abajo, y las esquinas redondeadas. Usamos `react-native-safe-area-context` porque funciona tanto en iOS como en Android y es la librería recomendada por Expo, mientras que el `SafeAreaView` de React Native solo funciona en iOS. Además nos da el hook `useSafeAreaInsets` para leer los márgenes exactos.

## 7. Escribe con tus palabras las tres buenas prácticas del checklist del Paso 5 y da un ejemplo de cuándo un modal **no** es buena idea.

1. Usar un solo modal en la pantalla, y solo para una acción corta y concreta, como elegir contactos para compartir un perfil.
2. Mantener limitado el contenido dentro de un `ScrollView`. En mi app las únicas listas son `PROJECTS` (5 elementos) y `CONTACTS` (8 elementos), así que no pesan en la app.
3. Poner la pantalla dentro de un `SafeAreaView` para que el notch o las barras del sistema no tapen nada.

Un modal no es buena idea para contenido largo o complejo, por ejemplo un formulario de registro con muchos campos o un artículo largo, porque bloquea el resto de la app y es mejor como una pantalla normal. Tampoco conviene abrir modales encima de otros modales ni usarlos para un mensaje simple que se puede escribir directamente en la pantalla.