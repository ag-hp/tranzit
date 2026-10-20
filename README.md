<p align="center">
  <img width="3926" height="408" alt="TRANZIT banner" src="https://github.com/user-attachments/assets/84e77819-1950-47cb-bf75-3ec47b835990"/>
</p>

<p align="center">
  <b>Anticípate a las incidencias de tu transporte público. Antes de llegar a la estación.</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Kotlin-7F52FF?style=flat&logo=kotlin&logoColor=white" alt="Kotlin">
  <img src="https://img.shields.io/badge/Android_Studio-3DDC84?style=flat&logo=androidstudio&logoColor=white" alt="Android Studio">
  <img src="https://img.shields.io/badge/Jetpack_Compose-4285F4?style=flat&logo=jetpackcompose&logoColor=white" alt="Jetpack Compose">
  <img src="https://img.shields.io/badge/Gradle-02303A?style=flat&logo=gradle&logoColor=white" alt="Gradle">
  <img src="https://img.shields.io/badge/Firebase-FFCA28?style=flat&logo=firebase&logoColor=black" alt="Firebase">
  <img src="https://img.shields.io/badge/Vercel-000000?style=flat&logo=vercel&logoColor=white" alt="Vercel">
  <img src="https://img.shields.io/badge/Room-4285F4?style=flat&logo=sqlite&logoColor=white" alt="Room">
  <img src="https://img.shields.io/badge/NFC-000000?style=flat&logo=nfc&logoColor=white" alt="NFC">
</p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-Proprietary-007ACC?style=flat" alt="License"></a>
  <img src="https://img.shields.io/badge/Cost-Free%20Tier-00C853?style=flat" alt="Cost">
  <img src="https://img.shields.io/badge/Estado-En_proceso-yellow?style=flat" alt="En proceso">
  <a href="https://github.com/ag-hp/tranzit/actions/workflows/build.yml">
    <img src="https://github.com/ag-hp/tranzit/actions/workflows/build.yml/badge.svg?branch=main" alt="Build Status">
  </a>
</p>

<p align="center">
  <img width="1963" height="10" alt="separator" src="https://github.com/user-attachments/assets/8025f457-6a76-4166-918a-4411a2ee1318"/>
</p>

## Índice

1. [Descripción](#1-descripción)
2. [Características](#2-características)
3. [Capturas de pantalla](#3-capturas-de-pantalla)
4. [Arquitectura](#4-arquitectura)
5. [Base de datos](#5-base-de-datos)
6. [Tecnologías](#6-tecnologías)
7. [Instalación y ejecución](#7-instalación-y-ejecución)
8. [Estructura del proyecto](#8-estructura-del-proyecto)
9. [Autor](#9-autor)
10. [Licencia](#10-licencia)

---

## 1. Descripción

**TRANZIT** es una aplicación móvil nativa para Android orientada a la **anticipación de incidencias** en redes de transporte público (**Metro, Cercanías y CRTM**).

Su objetivo es avisar al usuario **antes** de que llegue a la estación. Para ello combina un backend ligero de extracción de datos con notificaciones push segmentadas por líneas (*Firebase FCM Topics*). Además, integra lectura y escritura **NFC (NTAG215)** para consultar estados de forma física.

---

## 2. Características

- 🔔 **Alertas push por línea**: suscripción a las líneas que usas mediante FCM Topics.
- 🚇 **Cobertura multi-red**: Metro, Cercanías y CRTM.
- 📲 **NFC (NTAG215)**: lectura y escritura de tags para consultar el estado de una línea o estación.
- 🗄️ **Persistencia local** con Room.
- ☁️ **Backend ligero** de extracción de datos desplegado en Vercel.
- <!-- Añade aquí nuevas características -->

---

## 3. Capturas de pantalla

> _Próximamente._

<!--
<p align="center">
  <img src="docs/screenshots/home.png" width="240" alt="Pantalla principal">
  <img src="docs/screenshots/alerts.png" width="240" alt="Alertas">
  <img src="docs/screenshots/nfc.png" width="240" alt="NFC">
</p>
-->

---

## 4. Arquitectura

```mermaid
flowchart LR
    A[Fuentes de datos<br/>Metro · Cercanías · CRTM] --> B[Backend de extracción<br/>Vercel]
    B --> C[Firebase Cloud Messaging<br/>Topics por línea]
    C --> D[App Android<br/>Kotlin + Compose]
    D <--> E[(Room)]
    D <--> F[Tag NFC<br/>NTAG215]
```

> _Aquí puedes ampliar con detalles de capas, patrones y decisiones técnicas._

---

## 5. Base de datos

La base de datos en la nube se apoya en **Firebase (Cloud Firestore)**, y la app guarda una copia local con **Room** para consultar datos sin conexión. La estructura sale directamente de las pantallas del diseño: registro, foro de comunidad, mapa, contacto y soporte, y perfil.

### 5.1 Perfiles de usuario

Cada cuenta tiene un campo `rol` que determina lo que puede hacer en la app.

| Rol | Descripción | Permisos |
|---|---|---|
| `usuario1` | _Por definir_ | Registro, consulta de incidencias, foro, mapa, perfil propio |
| `usuario2` | _Por definir_ | _Por definir_ |
| `admin` | Administrador de la app | Moderar incidencias y comentarios, gestionar usuarios, responder tickets de soporte, editar FAQ y líneas |

### 5.2 Modelo entidad-relación

```mermaid
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

### 5.3 Colecciones y pantallas

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

## 6. Tecnologías

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

## 7. Instalación y ejecución

### Requisitos previos

- Android Studio (versión reciente)
- JDK compatible con el proyecto
- Dispositivo Android con NFC (para probar esa función)
- Proyecto de Firebase configurado

### Pasos

```bash
# 1. Clonar el repositorio
git clone https://github.com/ag-hp/tranzit.git
cd tranzit

# 2. Abrir en Android Studio y sincronizar Gradle

# 3. Compilar
./gradlew assembleDebug
```

### Configuración de Firebase

1. Crea un proyecto en la [consola de Firebase](https://console.firebase.google.com/).
2. Registra la app Android y descarga `google-services.json`.
3. Colócalo en `app/google-services.json`.

> _Añade aquí variables de entorno, claves o configuración del backend si son necesarias._

---

## 8. Estructura del proyecto

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

📑 **Presentación del proyecto:** [`docs/presentacion/`](docs/presentacion/)
<!-- Cuando subas el archivo, enlázalo directo: [Ver presentación](docs/presentacion/tranzit.pdf) -->

---

## 9. Autor

Desarrollado por **[ag-hp](https://github.com/ag-hp)** y .

---

## 10. Licencia

Este proyecto es **software propietario**. Consulta el archivo [LICENSE](LICENSE) para conocer los términos de uso, modificación y distribución.

<p align="center">
  <img width="1963" height="100" alt="footer" src="https://github.com/user-attachments/assets/8025f457-6a76-4166-918a-4411a2ee1318"/>
</p>
