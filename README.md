<!-- Banner -->
<p align="center">
  <img width="3926" height="408" alt="TRANZIT banner" src="https://github.com/user-attachments/assets/84e77819-1950-47cb-bf75-3ec47b835990"/>
</p>

<!-- Lema -->
<p align="center">
  <b>Anticípate a las incidencias de tu transporte público. Antes de llegar a la estación.</b>
</p>

<!-- Badges de tecnologías -->
<p align="center">
  <img src="https://img.shields.io/badge/Kotlin-7F52FF?style=flat&logo=kotlin&logoColor=white" alt="Kotlin">
  <img src="https://img.shields.io/badge/Android-34A853?style=flat&logo=android&logoColor=white" alt="Android">
  <img src="https://img.shields.io/badge/Android_Studio-3DDC84?style=flat&logo=androidstudio&logoColor=white" alt="Android Studio">
  <img src="https://img.shields.io/badge/Jetpack_Compose-4285F4?style=flat&logo=jetpackcompose&logoColor=white" alt="Jetpack Compose">
  <img src="https://img.shields.io/badge/Gradle-02303A?style=flat&logo=gradle&logoColor=white" alt="Gradle">
  <img src="https://img.shields.io/badge/Firebase-FFCA28?style=flat&logo=firebase&logoColor=black" alt="Firebase">
  <img src="https://img.shields.io/badge/Vercel-000000?style=flat&logo=vercel&logoColor=white" alt="Vercel">
  <img src="https://img.shields.io/badge/Room-4285F4?style=flat&logo=sqlite&logoColor=white" alt="Room">
  <img src="https://img.shields.io/badge/NFC-000000?style=flat&logo=nfc&logoColor=white" alt="NFC">
</p>

<!-- Badges de estado -->
<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-Proprietary-007ACC?style=flat" alt="License"></a>
  <img src="https://img.shields.io/badge/Estado-En_proceso-yellow?style=flat" alt="En proceso">
  <a href="https://github.com/ag-hp/tranzit/actions/workflows/build.yml">
    <img src="https://github.com/ag-hp/tranzit/actions/workflows/build.yml/badge.svg?branch=main" alt="Build Status">
  </a>
  <a href="https://github.com/ag-hp/tranzit/stargazers"><img src="https://img.shields.io/github/stars/ag-hp/tranzit.svg?style=social&label=Star&maxAge=2592000&v=2" alt="GitHub stars"></a>
  <img src="https://api.visitorbadge.io/api/visitors?path=https%3A%2F%2Fgithub.com%2Fag-hp%2Ftranzit&label=visitors&countColor=%230c7ebe&style=flat&labelStyle=none" alt="Visitors">
</p>

<!-- Separador -->
<p align="center">
  <img width="1963" height="10" alt="separator" src="https://github.com/user-attachments/assets/8025f457-6a76-4166-918a-4411a2ee1318"/>
</p>

<!-- Índice -->
<p><img src="docs/assets/sec-indice.svg" alt="Índice" width="100%"></p>

<p align="center">
  <a href="#descripcion"><img src="docs/assets/idx-1.svg" alt="1. Descripción" width="300"></a>
  <a href="#caracteristicas"><img src="docs/assets/idx-2.svg" alt="2. Características" width="300"></a><br>
  <a href="#capturas"><img src="docs/assets/idx-3.svg" alt="3. Capturas de pantalla" width="300"></a>
  <a href="#arquitectura"><img src="docs/assets/idx-4.svg" alt="4. Arquitectura" width="300"></a><br>
  <a href="#base-de-datos"><img src="docs/assets/idx-5.svg" alt="5. Base de datos" width="300"></a>
  <a href="#tecnologias"><img src="docs/assets/idx-6.svg" alt="6. Tecnologías" width="300"></a><br>
  <a href="#instalacion"><img src="docs/assets/idx-7.svg" alt="7. Instalación y ejecución" width="300"></a>
  <a href="#estructura"><img src="docs/assets/idx-8.svg" alt="8. Estructura del proyecto" width="300"></a><br>
  <a href="#autor"><img src="docs/assets/idx-9.svg" alt="9. Autor" width="300"></a>
  <a href="#licencia"><img src="docs/assets/idx-10.svg" alt="10. Licencia" width="300"></a><br>
</p>

---

<!-- 1. Descripción -->
<p><a name="descripcion"></a><img src="docs/assets/sec-1-descripcion.svg" alt="1. Descripción" width="100%"></p>

**TRANZIT** es una aplicación móvil nativa para Android orientada a la **anticipación de incidencias** en redes de transporte público (**Metro, Cercanías y CRTM**).

Su objetivo es avisar al usuario **antes** de que llegue a la estación. Para ello combina un backend ligero de extracción de datos con notificaciones push segmentadas por líneas (*Firebase FCM Topics*). Además, integra lectura y escritura **NFC (NTAG215)** para consultar estados de forma física.

---

<!-- 2. Características -->
<p><a name="caracteristicas"></a><img src="docs/assets/sec-2-caracteristicas.svg" alt="2. Características" width="100%"></p>

- 🔔 **Alertas push por línea**: suscripción a las líneas que usas mediante FCM Topics.
- 🚇 **Cobertura multi-red**: Metro, Cercanías y CRTM.
- 📲 **NFC (NTAG215)**: lectura y escritura de tags para consultar el estado de una línea o estación.
- 🗄️ **Persistencia local** con Room.
- ☁️ **Backend ligero** de extracción de datos desplegado en Vercel.

---

<!-- 3. Capturas -->
<p><a name="capturas"></a><img src="docs/assets/sec-3-capturas.svg" alt="3. Capturas de pantalla" width="100%"></p>

> _Próximamente._

<!--
<p align="center">
  <img src="docs/screenshots/home.png" width="240" alt="Pantalla principal">
  <img src="docs/screenshots/alerts.png" width="240" alt="Alertas">
  <img src="docs/screenshots/nfc.png" width="240" alt="NFC">
</p>
-->

---

<!-- 4. Arquitectura -->
<p><a name="arquitectura"></a><img src="docs/assets/sec-4-arquitectura.svg" alt="4. Arquitectura" width="100%"></p>

```mermaid
%%{init: {'theme':'base','themeVariables':{'lineColor':'#4700FD','fontFamily':'Inter, Segoe UI, Arial, sans-serif'}}}%%
flowchart LR
    A[Fuentes de datos<br/>Metro · Cercanías · CRTM] --> B[Backend de extracción<br/>Vercel]
    B --> C[Firebase Cloud Messaging<br/>Topics por línea]
    C --> D[App Android<br/>Kotlin + Compose]
    D <--> E[(Room)]
    D <--> F[Tag NFC<br/>NTAG215]

    classDef azul fill:#4700FD,stroke:#2F00A8,stroke-width:1.5px,color:#fff,rx:10,ry:10
    class A,B,C,D,E,F azul
```

> _Aquí puedes ampliar con detalles de capas, patrones y decisiones técnicas._

---

<!-- 5. Base de datos -->
<p><a name="base-de-datos"></a><img src="docs/assets/sec-5-base-de-datos.svg" alt="5. Base de datos" width="100%"></p>

La base de datos en la nube se apoya en **Firebase (Cloud Firestore)**, y la app guarda una copia local con **Room** para consultar datos sin conexión. La estructura sale directamente de las pantallas del diseño: registro, foro de comunidad, mapa, contacto y soporte, y perfil.

<!-- 5.1 Roles -->
<p><img src="docs/assets/sub-5-1.svg" alt="5.1 Perfiles de usuario" width="440"></p>

Cada cuenta tiene un campo `rol` que determina lo que puede hacer en la app.

| Rol | Descripción | Permisos |
|---|---|---|
| `usuario1` | _Por definir_ | Registro, consulta de incidencias, foro, mapa, perfil propio |
| `usuario2` | _Por definir_ | _Por definir_ |
| `admin` | Administrador de la app | Moderar incidencias y comentarios, gestionar usuarios, responder tickets de soporte, editar FAQ y líneas |

<!-- 5.2 Modelo ER -->
<p><img src="docs/assets/sub-5-2.svg" alt="5.2 Modelo entidad-relación" width="440"></p>

```mermaid
%%{init: {'theme':'base','themeVariables':{'primaryColor':'#EDF2FF','primaryTextColor':'#1E0A6B','primaryBorderColor':'#4700FD','secondaryColor':'#EDF2FF','tertiaryColor':'#EDF2FF','lineColor':'#4700FD','attributeBackgroundColorOdd':'#F6F8FF','attributeBackgroundColorEven':'#EDF2FF','fontFamily':'Inter, Segoe UI, Arial, sans-serif'}}}%%
erDiagram
    USUARIO ||--o{ INCIDENCIA : reporta
    USUARIO ||--o{ COMENTARIO : escribe
    INCIDENCIA ||--o{ COMENTARIO : recibe
    LINEA ||--o{ INCIDENCIA : afecta
    USUARIO ||--o{ SUSCRIPCION : tiene
    LINEA ||--o{ SUSCRIPCION : "es seguida en"
    USUARIO ||--o| TARJETA_NFC : enlaza
    USUARIO ||--o{ TICKET_SOPORTE : envia

    USUARIO {
        string uid PK
        string nombre
        string email
        string proveedor "email, google, x"
        string rol "usuario1, usuario2, admin"
        string fotoUrl
        string abonoTransporte
        timestamp creadoEn
    }
    LINEA {
        string id PK
        string red "Metro, Cercanias, CRTM"
        string nombre
        string topicFcm
    }
    INCIDENCIA {
        string id PK
        string titulo
        string descripcion
        string tipo "Emergencia, Informacion"
        string lineaId FK
        string estacion
        double lat
        double lng
        string autorId FK
        string estado
        timestamp fecha
    }
    COMENTARIO {
        string id PK
        string incidenciaId FK
        string autorId FK
        string texto
        timestamp fecha
    }
    SUSCRIPCION {
        string uid FK
        string lineaId FK
        boolean notificar
    }
    TARJETA_NFC {
        string uid FK
        string tagId "NTAG215"
        timestamp vinculadaEn
    }
    TICKET_SOPORTE {
        string id PK
        string uid FK
        string mensaje
        string estado
        timestamp fecha
    }
```

<!-- 5.3 Colecciones -->
<p><img src="docs/assets/sub-5-3.svg" alt="5.3 Colecciones y pantallas" width="440"></p>

| Colección | Pantalla que la usa |
|---|---|
| `usuarios` | Registro, Perfil |
| `lineas` | Foro, Mapa, Notificaciones |
| `incidencias` | Foro (Comunidad), Mapa, Historial de reportes |
| `comentarios` | Foro |
| `suscripciones` | Perfil (Notificaciones), alertas push (FCM Topics) |
| `tarjetas_nfc` | Perfil (Enlazar tarjeta NFC) |
| `tickets_soporte` | Contacto y Soporte |
| `faq` | Contacto y Soporte (Preguntas frecuentes) |

> _Aquí puedes ampliar con reglas de seguridad de Firestore e índices._

---

<!-- 6. Tecnologías -->
<p><a name="tecnologias"></a><img src="docs/assets/sec-6-tecnologias.svg" alt="6. Tecnologías" width="100%"></p>

| Área | Tecnología |
|---|---|
| Lenguaje | Kotlin |
| UI | Jetpack Compose |
| IDE / Build | Android Studio · Gradle |
| Notificaciones | Firebase Cloud Messaging (Topics) |
| Persistencia local | Room |
| Backend | Vercel |
| Hardware | NFC · NTAG215 |
| CI | GitHub Actions |

---

<!-- 7. Instalación -->
<p><a name="instalacion"></a><img src="docs/assets/sec-7-instalacion.svg" alt="7. Instalación y ejecución" width="100%"></p>

<p><img src="docs/assets/sub-7-req.svg" alt="Requisitos previos" width="440"></p>

- Android Studio (versión reciente)
- JDK compatible con el proyecto
- Dispositivo Android con NFC (para probar esa función)
- Proyecto de Firebase configurado

<p><img src="docs/assets/sub-7-pasos.svg" alt="Pasos" width="440"></p>

```bash
# 1. Clonar el repositorio
git clone https://github.com/ag-hp/tranzit.git
cd tranzit

# 2. Abrir en Android Studio y sincronizar Gradle

# 3. Compilar
./gradlew assembleDebug
```

<p><img src="docs/assets/sub-7-firebase.svg" alt="Configuración de Firebase" width="440"></p>

1. Crea un proyecto en la [consola de Firebase](https://console.firebase.google.com/).
2. Registra la app Android y descarga `google-services.json`.
3. Colócalo en `app/google-services.json`.

> _Añade aquí variables de entorno, claves o configuración del backend si son necesarias._

---

<!-- 8. Estructura -->
<p><a name="estructura"></a><img src="docs/assets/sec-8-estructura.svg" alt="8. Estructura del proyecto" width="100%"></p>

```text
tranzit/
├── app/            # Aplicación Android
├── backend/        # Backend de extracción de datos (si aplica)
├── docs/
│   ├── presentacion/   # Presentación del proyecto (PDF / PPTX)
│   └── screenshots/    # Capturas de pantalla de la app
├── LICENSE
└── README.md
```

> _Ajusta el árbol a la estructura real del repositorio._

<!-- Enlace a la presentación -->
📑 **Presentación del proyecto:** [`docs/presentacion/`](docs/presentacion/)

---

<!-- 9. Autor -->
<p><a name="autor"></a><img src="docs/assets/sec-9-autor.svg" alt="9. Autor" width="100%"></p>

Desarrollado por **[ag-hp](https://github.com/ag-hp)** y **[]()**.

[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat&logo=github&logoColor=white)](https://github.com/ag-hp)

---

<!-- 10. Licencia -->
<p><a name="licencia"></a><img src="docs/assets/sec-10-licencia.svg" alt="10. Licencia" width="100%"></p>

Este proyecto es **software propietario**. Consulta el archivo [LICENSE](LICENSE) para conocer los términos de uso, modificación y distribución.

<!-- Banner final -->
<p align="center">
  <img width="1963" height="100" alt="footer" src="https://github.com/user-attachments/assets/8025f457-6a76-4166-918a-4411a2ee1318"/>
</p>
