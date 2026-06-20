<div align="center">

# 🚌 RBE — Rutas Baja Express

**Sistema de Gestión de Transporte · Baja California, MX**

Plataforma integral de taquilla web y app móvil para la gestión de transporte terrestre en Baja California.

`Django 4.2` `Flutter` `MySQL` `REST API` `IA Elipse` `Groq LLM` `Python 3` `BCrypt` `PDF Gen` `Firebase`

</div>

<br/>

<div align="center">

| 🟦 Backend Django | 🟦 Flutter Mobile | 🟪 IA Elipse integrada | 🟩 REST API completa | 🟨 Panel administrativo |
|---|---|---|---|---|

</div>

---

## 📋 Tabla de contenidos

- [¿Qué es RBE?](#-qué-es-rbe)
- [Elipse — IA integrada](#-elipse--inteligencia-artificial-integrada)
- [Funcionalidades clave](#-funcionalidades-clave)
- [Arquitectura del sistema](#-arquitectura-del-sistema)
- [Stack tecnológico](#-stack-tecnológico)
- [Esquema de base de datos](#-esquema-mysql)
- [Instalación y ejecución](#-instalación-y-ejecución)
- [El equipo](#-el-equipo)
- [Licencia / Créditos](#-créditos)

---

## 🧭 ¿Qué es RBE?

RBE es una plataforma de taquilla y administración de autobuses diseñada para **Rutas Baja Express**, cubriendo desde la venta de boletos en ventanilla hasta la app móvil para pasajeros, todo conectado a una sola base de datos centralizada.

<table>
<tr>
<td width="50%" valign="top">

### 🌐 Panel Web Administrativo
Dashboard con KPIs en tiempo real, gestión de viajes, rutas, autobuses, conductores, terminales y taquilleros. CRUD completo vía API interna.

</td>
<td width="50%" valign="top">

### 📱 App Móvil Flutter
Aplicación nativa para Android con roles diferenciados: pasajero, taquillero e invitado. Compra de boletos, historial, selección de asientos y generación de PDF.

</td>
</tr>
<tr>
<td width="50%" valign="top">

### 🤖 IA Elipse
Asistente de inteligencia artificial propio, integrado en el panel web, capaz de consultar la base de datos en lenguaje natural y ejecutar SQL directo sobre el sistema.

</td>
<td width="50%" valign="top">

### 🎫 Venta y Gestión de Boletos
Flujo completo de compra: selección de viaje, asiento interactivo, datos de pasajero, pago, generación de PDF y envío por correo electrónico.

</td>
</tr>
<tr>
<td width="50%" valign="top">

### 🔐 Autenticación Segura
Contraseñas encriptadas con BCrypt. Login por correo/contraseña y Google (Firebase). Roles separados para taquilleros, administradores y pasajeros.

</td>
<td width="50%" valign="top">

### 📊 Dashboard & Reportes
Reportes de ventas por periodo, ingresos, ocupación de unidades, ranking de taquilleros y análisis de rutas. Todo exportable con datos reales.

</td>
</tr>
</table>

---

## 🤖 Elipse — Inteligencia Artificial integrada

> 👑 Creada y propiedad de **Misael Urquidez Arredondo**

**Elipse** es la IA propietaria del sistema RBE. Creada desde cero como módulo interno, permite a los administradores consultar la base de datos completa usando lenguaje natural en español — sin escribir una sola línea de SQL — o ejecutar consultas directas si lo prefieren.

Elipse usa modelos de lenguaje de última generación vía **Groq API** (Llama 3.3 70B, Llama 3.1 8B, Gemma 2 9B) y está protegida contra operaciones destructivas. Solo puede *consultar*, nunca modificar datos.

### Capacidades

| | Capacidad | Ejemplo |
|---|---|---|
| 📅 | **Consultas por fecha** | "Viajes programados para mañana", "boletos vendidos el 1 de marzo" |
| 🏆 | **Rankings automáticos** | "Top 5 conductores con más viajes", "taquillero con más ventas" |
| 💰 | **Análisis financiero** | "Ingresos del año 2025", "cuánto se recaudó hoy" |
| 🚌 | **Estado de flota** | "Autobuses sin asignar", "camiones disponibles esta semana" |
| 👤 | **Detalle por viaje** | "Pasajeros del viaje #40", "conductor del viaje 15" |
| 💻 | **SQL directo** | Escribe cualquier `SELECT ...` y Elipse lo ejecuta al instante |
| 🔒 | **Seguridad activa** | Detecta y bloquea automáticamente intenciones de `DELETE`, `DROP`, `INSERT` o `UPDATE` |

---

## ⚙️ Funcionalidades clave

RBE cubre el ciclo completo de operación de una empresa de autobuses — desde la terminal hasta el teléfono del pasajero.

| # | Funcionalidad | Descripción |
|---|---|---|
| 01 | **CRUD Dinámico Universal** | API genérica que permite insertar, leer, actualizar y eliminar registros en cualquier tabla desde el panel, sin endpoints hardcodeados por tabla. |
| 02 | **Selección visual de asientos** | Mapa interactivo de asientos por autobús con estados en tiempo real (disponible / ocupado), tanto en web como en la app móvil. |
| 03 | **Generación y envío de PDF** | Cada boleto genera un PDF con código de folio, datos del viaje y pasajero, enviable automáticamente al correo del cliente. |
| 04 | **Múltiples roles de usuario** | Taquillero, Administrador, Pasajero registrado e Invitado — cada uno con vistas y permisos diferenciados tanto en web como en móvil. |
| 05 | **KPIs y dashboard en vivo** | Métricas generales y específicas: viajes activos, ingresos del periodo, tasa de ocupación, boletos vendidos por taquillero y más. |
| 06 | **Gestión de salidas** | Vista de salidas en tiempo real con estado del viaje (programado, en curso, cancelado, completado), filtros y asignación de conductor y unidad. |
| 07 | **Login Google + Firebase** | Los pasajeros pueden registrarse con cuenta Google desde la app móvil vía Firebase Authentication, con vinculación automática al sistema. |
| 08 | **Hotspot LAN para móvil** | El servidor Django puede exponerse en la red local para conectar la app física sin internet, ideal para demos y entornos sin conexión externa. |
| 09 | **Encriptación de contraseñas** | Script dedicado `migrar_contrasenas.py` que encripta todas las contraseñas existentes en la BD con BCrypt de forma segura y no destructiva. |

---

## 🏗️ Arquitectura del sistema

Arquitectura cliente-servidor con backend centralizado Django, API REST consumida tanto por el panel web como por la app Flutter.

```
📱 App Flutter  ── REST / JSON ──▶  ⚙️ Django Backend  ── ORM / SQL ──▶  🗄️ MySQL DB
   Android · Dart                    Python 3 · DRF                      XAMPP · Local
```

<table>
<tr>
<td width="50%" valign="top">

**// Web (Templates Django)**
```
├─ login.html             — auth taquillero/admin
├─ panel_principal.html   — taquilla
├─ dash.html              — dashboard KPIs
├─ salidas.html           — gestión viajes
├─ panel_admin.html       — CRUD general
└─ elipse.html            — chat con IA
```

</td>
<td width="50%" valign="top">

**// Móvil (Flutter Screens)**
```
├─ auth/        — login · signup
├─ taquillero/  — home · historial · perfil
├─ cliente/     — home · historial · perfil
├─ invitado/    — home · perfil
└─ shared/      — buscar · asientos · pago · PDF
```

</td>
</tr>
</table>

---

## 🧰 Stack tecnológico

<table>
<tr>
<td width="33%" valign="top">

**Backend**
- Django 4.2
- Django REST Framework
- Python 3
- Gunicorn / ASGI
- python-dotenv
- WhiteNoise

</td>
<td width="33%" valign="top">

**Base de Datos**
- MySQL (XAMPP)
- mysqlclient ORM
- Raw SQL (Elipse)
- Migraciones Django

</td>
<td width="33%" valign="top">

**Seguridad**
- BCrypt (hashing)
- Firebase Auth
- Google OAuth
- Sesiones Django
- `.env` secrets

</td>
</tr>
<tr>
<td width="33%" valign="top">

**IA · Elipse**
- Groq API
- Llama 3.3 70B
- Llama 3.1 8B
- Gemma 2 9B
- NLP → SQL propio

</td>
<td width="33%" valign="top">

**Móvil**
- Flutter / Dart
- Firebase SDK
- PDF generation
- REST HTTP client
- scrcpy (mirror)

</td>
<td width="33%" valign="top">

**DevOps · Local**
- XAMPP (MySQL)
- venv Python
- nmcli hotspot LAN
- Procfile (Heroku)

</td>
</tr>
</table>

---

## 🗄️ Esquema MySQL

14 tablas relacionadas que modelan la operación completa de la empresa: flota, rutas, personal, pasajeros y transacciones.

<details>
<summary><strong>📦 viaje</strong></summary>

| Campo | Tipo |
|---|---|
| `numero` | 🔑 PK |
| `fecHoraSalida` | — |
| `fecHoraEntrada` | — |
| `ruta` | 🔗 FK |
| `estado` | 🔗 FK |
| `autobus` | 🔗 FK |
| `conductor` | 🔗 FK |

</details>

<details>
<summary><strong>🎫 ticket</strong></summary>

| Campo | Tipo |
|---|---|
| `codigo` | 🔑 PK |
| `precio` | — |
| `fechaEmision` | — |
| `asiento` | 🔗 FK |
| `viaje` | 🔗 FK |
| `pasajero` | 🔗 FK |
| `pago` | 🔗 FK |

</details>

<details>
<summary><strong>🛣️ ruta</strong></summary>

| Campo | Tipo |
|---|---|
| `codigo` | 🔑 PK |
| `duracion` | — |
| `origen` | 🔗 FK |
| `destino` | 🔗 FK |
| `precio` | — |

</details>

<details>
<summary><strong>🚌 autobus</strong></summary>

| Campo | Tipo |
|---|---|
| `numero` | 🔑 PK |
| `placas` | — |
| `serieVIN` | — |
| `modelo` | 🔗 FK |

</details>

<details>
<summary><strong>💺 asiento</strong></summary>

| Campo | Tipo |
|---|---|
| `numero` | 🔑 PK |
| `tipo` | 🔗 FK |
| `autobus` | 🔗 FK |

</details>

<details>
<summary><strong>🙋 pasajero</strong></summary>

| Campo | Tipo |
|---|---|
| `num` | 🔑 PK |
| `paNombre` | — |
| `paPrimerApell` | — |
| `fechaNacimiento` | — |

</details>

<details>
<summary><strong>🧑‍✈️ conductor</strong></summary>

| Campo | Tipo |
|---|---|
| `registro` | 🔑 PK |
| `conNombre` | — |
| `licNumero` | — |
| `licVencimiento` | — |

</details>

<details>
<summary><strong>🪪 taquillero</strong></summary>

| Campo | Tipo |
|---|---|
| `registro` | 🔑 PK |
| `usuario` | — |
| `contrasena` | — |
| `terminal` | 🔗 FK |

</details>

<details>
<summary><strong>🏢 terminal</strong></summary>

| Campo | Tipo |
|---|---|
| `numero` | 🔑 PK |
| `nombre` | — |
| `ciudad` | 🔗 FK |
| `telefono` | — |

</details>

<details>
<summary><strong>💳 pago</strong></summary>

| Campo | Tipo |
|---|---|
| `numero` | 🔑 PK |
| `monto` | — |
| `fechaPago` | — |
| `tipo` | 🔗 FK |

</details>

<details>
<summary><strong>🚐 modelo</strong></summary>

| Campo | Tipo |
|---|---|
| `numero` | 🔑 PK |
| `nombre` | — |
| `numAsientos` | — |
| `marca` | 🔗 FK |

</details>

<details>
<summary><strong>👤 cuenta_pasajero</strong></summary>

| Campo | Tipo |
|---|---|
| `pasajero_num` | 🔑 PK / 🔗 FK |
| `correo` | — |
| `firebase_uid` | — |
| `proveedor` | — |

</details>

> 🔑 PK — Clave primaria · 🔗 FK — Clave foránea

---

## 🚀 Instalación y ejecución

> Requisitos previos: **Python 3**, **MySQL via XAMPP** y **Flutter SDK**. Sigue estos pasos en orden.

### 00 · Prerrequisito — Importar la base de datos

> ⚠️ Antes de cualquier cosa, abre XAMPP, inicia MySQL y Apache, e importa el archivo `.sql` del proyecto en phpMyAdmin.

### 01 · Crear entorno virtual

```bash
# Linux / macOS
python3 -m venv venv

# Windows
python -m venv venv
```

### 02 · Activar el entorno virtual

```bash
# Ubuntu / macOS
source venv/bin/activate

# Windows
venv\Scripts\activate
```

### 03 · Instalar dependencias

```bash
pip install -r requirements.txt
```

### 04 · Ejecutar migraciones de Django

```bash
python manage.py migrate
```

### 05 · Encriptar contraseñas existentes

```bash
python Salvador/migrar_contrasenas.py
```

> 🔒 Este script migra todas las contraseñas en texto plano a hashes BCrypt seguros. Ejecútalo solo una vez.

### 06 · Iniciar el servidor

```bash
# Servidor web local
python manage.py runserver

# Accesible desde dispositivos móviles en la misma red
python manage.py runserver 0.0.0.0:8000
```

> 🌐 Accede a **http://localhost:8000** en tu navegador.

### 07 · Conexión LAN para app móvil (opcional)

```bash
# Crear hotspot WiFi en Linux
nmcli device wifi hotspot ifname wlp0s20f3 ssid "RBE-local" password "12345678"
```

```bash
# Espejo de pantalla Android (scrcpy)
cd Salvador
chmod +x auto_scrcpy.sh
./auto_scrcpy.sh
```

### 08 · Configurar IA Elipse (API Key Groq)

```bash
# Archivo .env en la raíz del proyecto
GROQ_API_KEY=gsk_tu_api_key_aqui
```

> 🔑 Si la API de Elipse está caída, genera una clave gratuita en **console.groq.com** → API Keys → Create API Key.

---

## 👥 El equipo

Cuatro desarrolladores, cada uno dominando su área. Un sistema cohesivo y completo como resultado.

### 👑 Misael Urquidez Arredondo
**Principal Architect & Full Stack Lead** · *Creador & Propietario de Elipse*

Arquitecto principal del sistema. Diseñó e implementó el backend Django completo, la REST API, la app móvil Flutter, los módulos de seguridad BCrypt y Firebase, los dashboards web, y es creador y propietario de la IA Elipse y el proyecto rbe.

---

### 📝 Anwar Fernando Estrada Santos
**Technical Documentation Engineer**

Responsable de la documentación técnica integral del proyecto: diagramas, manuales de usuario, flujos de datos y especificaciones del sistema. Pieza clave para la mantenibilidad y transferencia del conocimiento.

---

### 🗄️ Salvador Garcia Bojorquez
**Database Architect & Analyst**

Analista y diseñador del esquema de base de datos MySQL. Definió las entidades, relaciones, claves foráneas y normalización del modelo de datos sobre el que opera todo el sistema.

---

### 📱 Hemilton Raul Orduño Santiago
**Mobile Developer & Documentation**

Colaboró en el desarrollo de la app móvil Flutter y apoyó con la documentación técnica del sistema. Contribuyó en las pantallas de experiencia de usuario y flujos de la aplicación cliente.

---

## 🏁 Créditos

<div align="center">

### RBE

Rutas Baja Express · Sistema de gestión desarrollado en Baja California, México

---

IA **Elipse** — Propiedad intelectual de **Misael Urquidez Arredondo** · Todos los derechos reservados

</div>