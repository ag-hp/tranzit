# PROYECTO INTERMODULAR - TRANZIT: Llega antes de que ocurra 

TRANSPORT + CITY

##  Eslogans:
  - Fuerza y gancho comercial para tu app Tranzit: Get there before it happens
  - Versión ultra corta y directa para un banner o pantalla de inicio: Arrive before it happens.

<p align="center">
  <p align="center">
  <img src="https://raw.githubusercontent.com/JetBrains/kotlin-web-site/master/docs/topics/images/kotlin-logo-social-preview.png" alt="Kotlin Banner" width="100%"/>
</p>

<h1 align="center">TRANZIT - APLICACIÓN MÓVIL DE TRANSPORTE PÚBLICO EN TIEMPO REAL</h1>

<p align="center">
  
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Kotlin-Native-7F52FF?style=for-the-badge&logo=kotlin&logoColor=white" alt="Kotlin">
  <img src="https://img.shields.io/badge/Android%20Studio-Hedgehog-3DDC84?style=for-the-badge&logo=android-studio&logoColor=white" alt="Android Studio">
  <img src="https://img.shields.io/badge/Firebase-FCM%20Topics-FFCA28?style=for-the-badge&logo=firebase&logoColor=black" alt="Firebase">
  <img src="https://img.shields.io/badge/Database-Room%20SQLite-4285F4?style=for-the-badge&logo=sqlite&logoColor=white" alt="Room DB">
  <img src="https://img.shields.io/badge/Hardware-NFC%20NTAG215-000000?style=for-the-badge&logo=nfc&logoColor=white" alt="NFC">
  <img src="https://img.shields.io/badge/Coste-0%20%E2%82%AC%20Free%20Tier-00C853?style=for-the-badge" alt="Coste 0">
  <img src="https://img.shields.io/badge/Estado-Completado-brightgreen?style=for-the-badge" alt="Estado">
</p>

---

## 📌 Proyecto → Movilidad Urbana → Notificaciones Predictivas & NFC

---

### 1. Descripción General del Proyecto

**TRANZIT** es una aplicación móvil nativa desarrollada para Android orientada a la anticipación de incidencias en redes de transporte público (Metro, Cercanías, CRTM). Su objetivo es alertar al usuario **antes** de que llegue a la estación mediante un backend ligero de extracción de datos y un sistema de notificaciones push segmentadas por líneas (*Firebase FCM Topics*). Además, integra lectura y escritura **NFC (NTAG215)** para consulta física de estados.

---

### 2. Visión y Pilares Fundamentales

1. **Anticipación Predictiva:** Filtrado automático de avisos y tweets oficiales de transporte para disparar alertas inmediatas.
2. **Suscripción por Líneas (Sin Spam):** El usuario solo recibe notificaciones de las líneas que utiliza (ej. `C-5`, `L10`).
3. **Acceso Físico NFC:** Escaneo directo de tarjetas para la comprobación rápida del estado de las líneas habituales.
4. **Infraestructura de Coste 0 €:** Diseñado 100% sobre capas gratuitas (Firebase Free Tier, SQLite local con Room y servidores serverless en Render/Fly.io).

---

### 3. Stack Tecnológico y Arquitectura
