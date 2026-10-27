# Museo del Espacio en Realidad Virtual

**Museo interactivo en realidad virtual sobre el Sistema Solar y los fenómenos del espacio.**

Es el proyecto final de la asignatura de Dispositivos Hardware. El usuario empieza en un hangar, sube a una nave espacial y elige a qué zona del museo quiere viajar: el **Sistema Solar**, los **fenómenos cósmicos extremos** (agujeros negros, supernovas…) o los **asteroides, la Luna y la posible vida en otros planetas**. Tras un breve vuelo por el cosmos, puede explorar libremente cada zona e interactuar con sus elementos.

[![Vídeo de demostración](https://img.youtube.com/vi/pFssI0sH7Qw/hqdefault.jpg)](https://youtu.be/pFssI0sH7Qw)

## Enlaces

- 🎥 **Vídeo de demostración:** [youtu.be/pFssI0sH7Qw](https://youtu.be/pFssI0sH7Qw)
- 📄 **Memoria del proyecto:** [DIHA_memoria_museo_Olaia.pdf](DIHA_memoria_museo_Olaia.pdf)
- 📦 **Build para Android/VR:** [pruebaMuseo.apk](pruebaMuseo.apk)
- 💻 **Proyecto de Unity:** [`DIHA_codigo_museo_Olaia`](DIHA_codigo_museo_Olaia)

## Mi aportación

Fue un proyecto en grupo en el que cada integrante se encargó de una escena principal. Yo desarrollé dos:

### Sistema Solar (`OlaiaScene`)

El usuario aparece en una plataforma flotante con el Sol suspendido en el centro y los planetas girando a su alrededor.

- Desde una **pantalla interactiva** (con flechas y un botón *Aceptar*) elige el planeta sobre el que quiere aprender.
- El planeta elegido **se acerca suavemente** a la plataforma, empieza a rotar sobre su eje y los demás desaparecen mientras suena un **audio explicativo**.
- Cuando el audio termina, o si el usuario pulsa *Detener*, el planeta vuelve a su órbita y los demás reaparecen.
- Para reforzar la sensación de presencia, la música ambiental y las explicaciones suenan desde **altavoces físicos dentro de la escena** (no como voz en off), y se añadió un sonido de respiración.

### Viaje entre escenas (`FlyingScene`)

Es la transición en la que la nave vuela hacia el destino elegido. Un cilindro con estrellas se desplaza alrededor de la nave para crear un **efecto túnel** que da sensación de alta velocidad.

## Aspectos técnicos destacados

**Scripting (C#)**

- `SeleccionarPlaneta`: lógica de la interfaz (anterior, siguiente y aceptar), conectada mediante `UnityEvent`.
- `AcercarPlaneta`: movimiento de ida y vuelta del planeta con `Vector3.Lerp` y `Time.deltaTime`, sincronizado con el audio y la animación.
- `RotacionPlanetas`: órbita de los planetas alrededor del Sol.
- `MoverTunel`: movimiento del túnel en la escena de vuelo.
- Buenas prácticas: variables privadas con `[SerializeField]` para mantener el encapsulamiento, y comprobaciones de nulos (*null checks*) para evitar errores en tiempo de ejecución.

**Shaders (Shader Graph)**

- **Cielo estrellado con parpadeo:** ruido de gradiente animado y combinado con una copia invertida para lograr un parpadeo continuo. Se usa en el skybox de todas las escenas y en el túnel de vuelo.
- **Atmósfera de los planetas:** efecto Fresnel que solo se ilumina en la cara expuesta a la luz (producto escalar entre la dirección de la luz y la normal). Un mismo shader genera un material distinto para cada planeta.
- **Atmósfera del Sol:** variante del Fresnel que no depende de la iluminación, porque el Sol es la propia fuente de luz.

**Iluminación y rendimiento en VR**

- Iluminación ambiental anaranjada y una luz puntual dentro del Sol, validada con pruebas en las gafas para no penalizar el rendimiento.
- Iluminación precalculada (*baked lighting*) en los objetos estáticos.
- Postprocesado en la cámara del XR Origin para mejorar la imagen y reducir el mareo.

**Animación**

- Rotación de los planetas sobre su eje con un único Animation Clip reutilizado en nueve Animator Controllers.

## Tecnologías

- **Unity 6** (6000.2) con Universal Render Pipeline
- **XR Interaction Toolkit**, **OpenXR** y **Oculus XR Plugin**
- **C#**, **Shader Graph** y el nuevo **Input System**
- **Git y GitHub** (con Git LFS) para el trabajo en equipo
- Recursos: Unity Asset Store (nave, planetas, altavoces y tablet), imágenes 2D de los planetas generadas con Gemini y audios generados con Luvvoice


## Equipo

| Integrante | Estancia |
|---|---|
| Manuel Alejandro Villalba | Fenómenos cósmicos extremos y Hangar |
| **Olaia Picabea** | **Sistema solar y Viaje entre escenas** |
| Álvaro Quintanilla Carrasco  | Asteroides, la luna y posible vida en otros planetas |
