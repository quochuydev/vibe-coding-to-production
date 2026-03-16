# Vibe Coding to Production

🇺🇸 [English](README.md) | 🇨🇳 [中文](README-zh.md) | 🇻🇳 [Tiếng Việt](README-vi.md) | 🇪🇸 [Español](README-es.md) | 🇩🇪 [Deutsch](README-de.md)

Una guía completa paso a paso para **personas sin experiencia en programación** que quieren construir un sitio web desde cero y desplegarlo en producción usando programación asistida por IA (vibe coding) con Claude Code.

Al terminar esta guía, tendrás:

- Un sitio web Next.js completamente funcional
- Integración de pagos con Stripe
- Desplegado en un servidor en vivo con Dokploy
- Seguimiento de Google Analytics configurado

No se requiere experiencia previa en programación. Empecemos.

---

## Tabla de Contenidos

1. [Crear una Cuenta y Repositorio en GitHub](#1-crear-una-cuenta-y-repositorio-en-github)
2. [Instalar Git, Node.js y Claude Code](#2-instalar-git-nodejs-y-claude-code)
3. [Clonar tu Repositorio de GitHub](#3-clonar-tu-repositorio-de-github)
4. [Configurar Claude Code](#4-configurar-claude-code)
5. [Construir tu Sitio Web con Next.js](#5-construir-tu-sitio-web-con-nextjs)
6. [Configurar Pagos con Stripe](#6-configurar-pagos-con-stripe)
7. [Configurar un Servidor en DigitalOcean](#7-configurar-un-servidor-en-digitalocean)
8. [Instalar y Configurar Dokploy](#8-instalar-y-configurar-dokploy)
9. [Desplegar tu Sitio Web](#9-desplegar-tu-sitio-web)
10. [Configurar Google Analytics](#10-configurar-google-analytics)

---

## 1. Crear una Cuenta y Repositorio en GitHub

GitHub es donde vivirá el código de tu sitio web. Piénsalo como una carpeta en la nube para tu proyecto que también registra cada cambio que realizas.

### Crear una Cuenta en GitHub

1. Ve a [github.com](https://github.com)
2. Haz clic en **Sign up**
3. Ingresa tu correo electrónico, crea una contraseña y elige un nombre de usuario
4. Completa la verificación y haz clic en **Create account**
5. Revisa tu correo electrónico y verifica tu cuenta

### Crear un Nuevo Repositorio

Un repositorio (o "repo") es como una carpeta de proyecto en GitHub.

1. Después de iniciar sesión, haz clic en el ícono **+** en la esquina superior derecha
2. Haz clic en **New repository**
3. Completa los detalles:
   - **Repository name**: elige un nombre para tu proyecto (p. ej., `my-website`)
   - **Description**: opcional, agrega una descripción breve
   - **Public** o **Private**: elige Private si no quieres que otros vean tu código
   - Marca **Add a README file**
4. Haz clic en **Create repository**

<img width="100%" src="./images/github-create-repo.png" alt="Crear Repositorio en GitHub" />

5. ¡Ya tienes un repositorio! Copia la URL de tu navegador — se ve así: `https://github.com/your-username/my-website`

---

## 2. Instalar Git, Node.js y Claude Code

Necesitas tres herramientas en tu computadora: Git (para gestionar el código), Node.js (para ejecutar tu sitio web localmente) y Claude Code (tu asistente de programación con IA).

### Instalar Git

Git es la herramienta que conecta tu computadora con GitHub.

**En Mac:**

1. Abre la app **Terminal** (búscala con "Terminal" en Spotlight con Cmd + Space)
2. Escribe lo siguiente y presiona Enter:
   ```bash
   git --version
   ```
3. Si Git no está instalado, aparecerá un cuadro de diálogo pidiéndote que instales las Command Line Tools — haz clic en **Install**
4. Espera a que termine la instalación

**En Windows:**

1. Ve a [git-scm.com](https://git-scm.com)
2. Descarga el instalador y ejecútalo
3. Haz clic en **Next** en todas las opciones predeterminadas y termina la instalación
4. Abre **Git Bash** desde tu menú de Inicio (úsalo en lugar del símbolo del sistema normal)

### Configurar Git

Después de instalar, dile a Git quién eres. Abre tu Terminal (Mac) o Git Bash (Windows) y ejecuta:

```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

Usa el mismo correo electrónico que usaste para GitHub.

### Instalar Node.js

Node.js te permite ejecutar tu sitio web en tu computadora durante el desarrollo.

1. Ve a [nodejs.org](https://nodejs.org)
2. Descarga la versión **LTS** (la que dice "Recommended for most users")
3. Ejecuta el instalador y sigue las opciones predeterminadas
4. Verifica que esté instalado abriendo Terminal y ejecutando:
   ```bash
   node --version
   npm --version
   ```
   Ambos deben mostrar un número de versión.

### Instalar Claude Code

Claude Code es un asistente de IA que se ejecuta en tu terminal y escribe código por ti.

1. Abre Terminal y ejecuta:
   ```bash
   npm install -g @anthropic-ai/claude-code
   ```
2. Verifica que esté instalado:
   ```bash
   claude --version
   ```

---

## 3. Clonar tu Repositorio de GitHub

"Clonar" significa descargar tu repositorio de GitHub a tu computadora para poder trabajar en él localmente.

1. Abre Terminal
2. Navega hasta donde quieres que viva tu proyecto. Por ejemplo, para ponerlo en una carpeta "Projects":
   ```bash
   mkdir -p ~/Projects
   cd ~/Projects
   ```
3. Clona tu repositorio (reemplaza con tu URL real del Paso 1):
   ```bash
   git clone https://github.com/your-username/my-website.git
   ```
4. Entra a la carpeta del proyecto:
   ```bash
   cd my-website
   ```

Ahora estás dentro de la carpeta de tu proyecto y listo para empezar a construir.

---

## 4. Configurar Claude Code

### Comprar una Suscripción a Claude

Claude Code requiere una clave API de Anthropic o una suscripción a Claude.

**Opción A: Clave API de Anthropic (Pago por uso)**

1. Ve a [console.anthropic.com](https://console.anthropic.com)
2. Regístrate para obtener una cuenta
3. Ve a **Settings** > **API Keys**
4. Haz clic en **Create Key** y cópiala
5. Agrega información de facturación en **Settings** > **Billing** y añade créditos (empieza con $10–20)

**Opción B: Suscripción Claude Max (Uso ilimitado)**

1. Ve a [claude.ai](https://claude.ai)
2. Regístrate y suscríbete al plan **Max** ($100/mes) que incluye el uso de Claude Code

### Conectar Claude Code a tu Cuenta

1. Abre Terminal y navega a la carpeta de tu proyecto:
   ```bash
   cd ~/Projects/my-website
   ```
2. Inicia Claude Code:
   ```bash
   claude
   ```
3. En el primer inicio, te pedirá que te autentiques:
   - Si usas una **API Key**: te pedirá que ingreses tu clave
   - Si usas una **suscripción a Claude**: abrirá una ventana del navegador para iniciar sesión
4. Sigue las instrucciones en pantalla para completar la autenticación

<img width="100%" src="./images/claude-code-first-launch.png" alt="Primer Inicio de Claude Code" />

¡Ya estás listo para hacer vibe coding! Claude Code leerá los archivos de tu proyecto y te ayudará a construir tu sitio web.

---

## 5. Construir tu Sitio Web con Next.js

Next.js es un framework popular para construir sitios web modernos. No necesitas entenderlo — Claude Code configurará todo por ti.

### Inicializar el Proyecto

Asegúrate de estar en la carpeta de tu proyecto y luego inicia Claude Code:

```bash
cd ~/Projects/my-website
claude
```

Escribe el siguiente prompt:

```
Set up a new Next.js project in the current directory with TypeScript, Tailwind CSS,
and the App Router. Use the latest version of Next.js. Keep the default configuration
simple and clean.
```

Claude Code creará todos los archivos necesarios. Cuando termine, puedes previsualizar tu sitio localmente:

```bash
npm run dev
```

Abre tu navegador y ve a `http://localhost:3000` para ver tu sitio web.

### Diseñar el Layout de tu Sitio Web

Ahora dile a Claude Code cómo quieres que se vea tu sitio web. Aquí hay algunos prompts de ejemplo que puedes usar:

**Para una página de aterrizaje (landing page):**

```
Create a modern landing page with:
- A navigation bar with the logo "MyBrand" on the left and links to
  Home, Features, Pricing, and Contact on the right
- A hero section with a big headline "Build Something Amazing",
  a subtitle, and a call-to-action button
- A features section with 3 cards showing icons, titles, and descriptions
- A footer with copyright info and social media links
Make it look professional and modern with a clean design.
```

**Para un sitio web de varias páginas:**

```
Create these pages for my website:
- Home page: landing page with hero, features, and testimonials
- About page: company story, team section with photos
- Pricing page: 3 pricing tiers (Basic, Pro, Enterprise) with feature comparison
- Contact page: a contact form with name, email, and message fields
Add a consistent navigation bar and footer across all pages.
```

**Para una página de producto SaaS:**

```
Build a SaaS landing page for a project management tool called "TaskFlow":
- Hero section with a product screenshot mockup
- Problem/solution section
- Feature showcase with 6 features in a grid
- Social proof section with customer logos
- Pricing section with monthly/yearly toggle
- FAQ section with expandable answers
- CTA section at the bottom
Use a blue and white color scheme.
```

**Para refinar el diseño:**

```
Make the hero section taller, change the background to a gradient from blue to purple,
and make the headline text larger and bolder.
```

```
Add smooth scroll animations so elements fade in as the user scrolls down the page.
```

```
Make the website fully responsive so it looks great on mobile phones and tablets.
```

### Consejos para el Vibe Coding

- **Sé específico**: cuanto más detalle des, mejor será el resultado
- **Itera**: si algo no se ve bien, describe qué cambiar
- **Referencia sitios que te gusten**: "Make it look like the Stripe homepage" le da a Claude Code un punto de referencia
- **Pide correcciones**: si ves un error, simplemente descríbelo — "The navigation menu is overlapping the hero section on mobile, please fix it"

---

## 6. Configurar Pagos con Stripe

Stripe te permite aceptar pagos en tu sitio web. Crearás una cuenta de Stripe y luego usarás Claude Code para agregar la funcionalidad de pagos.

### Crear una Cuenta en Stripe

1. Ve a [stripe.com](https://stripe.com)
2. Haz clic en **Start now** y crea una cuenta
3. Después de iniciar sesión, estarás en el **modo de prueba** (Test mode) de forma predeterminada (puedes ver un interruptor en el panel) — esto es perfecto para construir; no se cobra dinero real
4. Ve a **Developers** > **API keys**
5. Verás dos claves:
   - **Publishable key**: comienza con `pk_test_...`
   - **Secret key**: comienza con `sk_test_...` (haz clic para revelarla)

6. Mantén esta página abierta — necesitarás ambas claves

### Crear Productos en Stripe

1. En el Panel de Stripe, ve a **Product catalog** > **Add product**
2. Crea tus niveles de precios:
   - Nombre: "Basic Plan"
   - Precio: $9/mes (o lo que quieras)
   - Haz clic en **Save product**
3. Repite para otros niveles (Pro, Enterprise, etc.)
4. Para cada producto, copia el **Price ID** (comienza con `price_...`) — los necesitarás

### Agregar Stripe a tu Sitio Web

Inicia Claude Code en la carpeta de tu proyecto y usa estos prompts:

**Configurar la integración con Stripe:**

```
Add Stripe payment integration to my Next.js project:
1. Install the Stripe packages (stripe and @stripe/stripe-js)
2. Create a .env.local file for my Stripe API keys with these placeholders:
   NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_test_xxx
   STRIPE_SECRET_KEY=sk_test_xxx
3. Create an API route at /api/checkout that creates a Stripe checkout session
4. The checkout should redirect to a /success page after payment
   and a /cancel page if they cancel
```

**Agregar una página de precios con checkout:**

```
Create a pricing page with 3 tiers:
- Basic: $9/month - 5 projects, basic support
- Pro: $29/month - unlimited projects, priority support
- Enterprise: $99/month - everything in Pro plus dedicated account manager

Each tier should have a "Get Started" button that redirects to Stripe Checkout.
Use these Stripe Price IDs:
- Basic: price_xxxxx (replace with your real price ID)
- Pro: price_xxxxx
- Enterprise: price_xxxxx
```

**Agregar tus claves reales de Stripe:**

```
Update the .env.local file with my real Stripe keys:
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_test_your_actual_key_here
STRIPE_SECRET_KEY=sk_test_your_actual_key_here
```

### Probar los Pagos

1. Ejecuta tu sitio web localmente con `npm run dev`
2. Ve a la página de precios y haz clic en un botón de compra
3. En la página de checkout de Stripe, usa el número de tarjeta de prueba: `4242 4242 4242 4242`
   - Vencimiento: cualquier fecha futura
   - CVC: cualquier 3 dígitos
4. Completa la compra — deberías ser redirigido a la página de éxito
5. Revisa tu Panel de Stripe en **Payments** para ver el pago de prueba

### Activar Pagos Reales

Cuando estés listo para recibir pagos reales:

1. Completa la configuración de tu cuenta de Stripe (datos del negocio, cuenta bancaria)
2. Cambia de **Test mode** a **Live mode** en el Panel de Stripe
3. Copia tus claves API en vivo (comienzan con `pk_live_` y `sk_live_`)
4. Actualiza tu `.env.local` con las claves en vivo

---

## 7. Configurar un Servidor en DigitalOcean

Necesitas un servidor para alojar tu sitio web para que cualquiera pueda acceder a él en internet.

### Crear una Cuenta en DigitalOcean

1. Ve a [digitalocean.com](https://www.digitalocean.com)
2. Haz clic en **Sign up** y crea una cuenta
3. Agrega un método de pago (tarjeta de crédito o PayPal)
4. Es posible que recibas $200 en créditos gratuitos por 60 días como nuevo usuario

### Crear un Servidor (Droplet)

1. Después de iniciar sesión, haz clic en **Create** > **Droplets**
2. Elige las siguientes configuraciones:
   - **Region**: elige la más cercana a tus usuarios (p. ej., San Francisco, New York, London)
   - **Image**: selecciona **Ubuntu 22.04 (LTS)** o la última Ubuntu LTS
   - **Size**: selecciona **Basic** > **Regular** > **$12/mo** (2 GB RAM / 1 CPU) — esto es suficiente para empezar
   - **Authentication**: elige **Password** y establece una contraseña root segura (¡guárdala en un lugar seguro!)
3. Haz clic en **Create Droplet**
4. Espera unos 60 segundos para que se cree
5. Copia la **dirección IP** que se muestra (p. ej., `164.90.xxx.xxx`) — la necesitarás

---

## 8. Instalar y Configurar Dokploy

Dokploy es una herramienta gratuita y de código abierto que hace que desplegar tu sitio web sea tan fácil como hacer clic en un botón. Es como una versión más simple de Vercel o Heroku que se ejecuta en tu propio servidor.

### Instalar Dokploy en tu Servidor

1. Abre Terminal en tu computadora
2. Conéctate a tu servidor mediante SSH:
   ```bash
   ssh root@your-server-ip-address
   ```
3. Escribe `yes` cuando te pregunten sobre la huella digital (fingerprint), luego ingresa la contraseña de tu servidor
4. Una vez conectado, ejecuta el comando de instalación de Dokploy:
   ```bash
   curl -sSL https://dokploy.com/install.sh | sh
   ```
5. Espera a que la instalación se complete (esto tarda unos minutos)
6. Cuando termine, mostrará una URL como `http://your-server-ip:3000`

### Configurar Dokploy

1. Abre tu navegador y ve a `http://your-server-ip:3000`
2. Verás la pantalla de configuración de Dokploy
3. Crea una cuenta de administrador:
   - Ingresa tu correo electrónico
   - Crea una contraseña
   - Haz clic en **Register**
4. Ahora estás en el panel de Dokploy

### Conectar Dokploy a GitHub

Esto permite que Dokploy obtenga tu código de GitHub automáticamente.

1. En Dokploy, ve a **Settings** (ícono de engranaje) > **Git Providers**
2. Haz clic en **Add GitHub**
3. Serás redirigido a GitHub — haz clic en **Authorize** para dar acceso a Dokploy
4. Selecciona a qué repositorios puede acceder Dokploy:
   - Elige **Only select repositories** y selecciona el repositorio de tu sitio web
   - Haz clic en **Install & Authorize**
5. Serás redirigido de vuelta a Dokploy — la conexión ya está activa

---

## 9. Desplegar tu Sitio Web

### Subir tu Código a GitHub

Antes de desplegar, necesitas subir tu código a GitHub. Vuelve a tu Terminal local (no la sesión SSH del servidor) y haz lo siguiente:

1. Abre Terminal y ve a la carpeta de tu proyecto:
   ```bash
   cd ~/Projects/my-website
   ```
2. Agrega todos tus archivos a Git:
   ```bash
   git add .
   ```
3. Crea un commit (una instantánea de tu código):
   ```bash
   git commit -m "Initial website build"
   ```
4. Súbelo a GitHub:
   ```bash
   git push origin main
   ```

Si es tu primer push, Git puede pedirte que inicies sesión en GitHub. Sigue las instrucciones.

**Consejo:** También puedes hacer esto a través de Claude Code:

```
Commit all changes with the message "Initial website build" and push to GitHub.
```

### Crear una Aplicación en Dokploy

1. En el panel de Dokploy, haz clic en **Projects** en la barra lateral

<img width="100%" src="./images/dokploy-projects.png" alt="Proyectos en Dokploy" />

2. Haz clic en **Create Project** y ponle un nombre (p. ej., "My Website")
3. Dentro del proyecto, haz clic en **Create Service** > **Application**
4. Configura la aplicación:
   - **Name**: ponle un nombre (p. ej., "web")
   - **Source**: selecciona **GitHub**
   - **Repository**: selecciona el repositorio de tu sitio web
   - **Branch**: `main`
   - **Build Type**: selecciona **Nixpacks** (detecta automáticamente el tipo de proyecto)
5. Haz clic en **Save**

### Configurar Variables de Entorno

Tu sitio web necesita las claves de Stripe para funcionar en producción.

1. En la configuración de tu aplicación en Dokploy, ve a la pestaña **Environment**
2. Agrega tus variables de entorno (una por línea):
   ```
   NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_live_your_key
   STRIPE_SECRET_KEY=sk_live_your_key
   ```
3. Haz clic en **Save**

### Configurar un Dominio (Opcional pero Recomendado)

Si tienes un nombre de dominio:

1. En Dokploy, ve a tu aplicación > pestaña **Domains**
2. Haz clic en **Add Domain**
3. Ingresa tu dominio (p. ej., `www.mywebsite.com`)
4. Activa **HTTPS** (certificado SSL gratuito mediante Let's Encrypt)
5. Haz clic en **Save**
6. En tu registrador de dominio (donde compraste el dominio), agrega un registro DNS:
   - **Type**: A
   - **Name**: `@` (o `www`)
   - **Value**: la dirección IP de tu servidor
   - **TTL**: 3600

### Desplegar

1. En Dokploy, ve a tu aplicación y haz clic en **Deploy**
2. Observa los registros de construcción (build logs) — Dokploy:
   - Descargará tu código de GitHub
   - Instalará las dependencias
   - Construirá tu sitio web Next.js
   - Lo pondrá en marcha
3. Una vez que la construcción esté completa, ¡tu sitio web está en vivo!

### Despliegue Automático al Hacer Push

Dokploy puede desplegar automáticamente cada vez que subes código nuevo a GitHub:

1. En la configuración de tu aplicación, ve a la pestaña **General**
2. Activa **Auto Deploy**
3. Ahora, cada vez que hagas push a GitHub, Dokploy reconstruye y despliega automáticamente

### El Flujo de Trabajo Completo: Hacer Cambios y Desplegar

Este es tu flujo de trabajo diario para actualizar tu sitio web:

1. Abre Terminal, navega a tu proyecto e inicia Claude Code:
   ```bash
   cd ~/Projects/my-website
   claude
   ```
2. Dile a Claude Code qué cambiar:
   ```
   Change the hero headline to "Welcome to the Future" and update the
   background color to dark blue.
   ```
3. Previsualiza localmente en `http://localhost:3000` (ejecuta `npm run dev`)
4. Cuando estés contento con los cambios, haz commit y push:
   ```bash
   git add .
   git commit -m "Update hero section"
   git push origin main
   ```
5. Dokploy despliega tus cambios automáticamente. ¡Listo!

---

## 10. Configurar Google Analytics

Google Analytics te permite ver cuántas personas visitan tu sitio web, de dónde vienen y qué páginas ven.

### Crear una Cuenta en Google Analytics

1. Ve a [analytics.google.com](https://analytics.google.com)
2. Haz clic en **Start measuring**
3. Completa los detalles de la cuenta:
   - **Account name**: tu nombre o el nombre de tu negocio
   - Haz clic en **Next**
4. Crea una propiedad:
   - **Property name**: el nombre de tu sitio web
   - Selecciona tu zona horaria y moneda
   - Haz clic en **Next**
5. Completa los detalles de tu negocio y haz clic en **Create**
6. Acepta los términos de servicio

### Obtener tu ID de Medición

1. En Google Analytics, ve a **Admin** (ícono de engranaje) > **Data Streams**
2. Haz clic en **Add stream** > **Web**
3. Ingresa la URL de tu sitio web y un nombre para el stream
4. Haz clic en **Create stream**
5. Copia el **Measurement ID** — se ve así: `G-XXXXXXXXXX`

<img width="100%" src="./images/google-analytics-measurement-id.png" alt="ID de Medición de Google Analytics" />

### Agregar Google Analytics a tu Sitio Web

Inicia Claude Code en la carpeta de tu proyecto y usa este prompt:

```
Add Google Analytics to my Next.js project.
My Google Analytics Measurement ID is G-XXXXXXXXXX (replace with your real ID).
Set it up using the recommended approach with the Next.js Script component.
Add it to the root layout so it tracks all pages. Use an environment variable
called NEXT_PUBLIC_GA_MEASUREMENT_ID for the ID.
```

Luego agrega la variable de entorno:

1. **Localmente**: agrégala a tu archivo `.env.local`:
   ```
   NEXT_PUBLIC_GA_MEASUREMENT_ID=G-XXXXXXXXXX
   ```
2. **En Dokploy**: agrega la misma variable en la pestaña **Environment** de tu aplicación

### Verificar que Funciona

1. Sube tus cambios a GitHub:
   ```bash
   git add .
   git commit -m "Add Google Analytics"
   git push origin main
   ```
2. Espera a que Dokploy despliegue
3. Visita tu sitio web en vivo
4. Ve a Google Analytics > **Reports** > **Realtime**
5. Deberías verte a ti mismo como un usuario activo

---

## Referencia Rápida: Comandos Útiles

| Lo que quieres hacer                  | Comando                                         |
| ------------------------------------- | ----------------------------------------------- |
| Abrir Terminal                        | Cmd + Space, escribe "Terminal" (Mac)           |
| Ir a la carpeta de tu proyecto        | `cd ~/Projects/my-website`                      |
| Iniciar Claude Code                   | `claude`                                        |
| Ejecutar tu sitio web localmente      | `npm run dev`                                   |
| Detener el servidor local             | Presiona `Ctrl + C` en Terminal                 |
| Guardar tus cambios en Git            | `git add .` luego `git commit -m "your message"` |
| Subir a GitHub                        | `git push origin main`                          |
| Descargar el código más reciente      | `git pull origin main`                          |
| Ver el estado del proyecto            | `git status`                                    |
| Conectarse a tu servidor              | `ssh root@your-server-ip`                       |

## Solución de Problemas

**"command not found: node"**
Node.js no está instalado correctamente. Vuelve a instalarlo desde [nodejs.org](https://nodejs.org).

**"command not found: claude"**
Ejecuta `npm install -g @anthropic-ai/claude-code` nuevamente.

**Git pide nombre de usuario/contraseña cada vez**
Configura claves SSH o usa GitHub CLI (`gh auth login`).

**El sitio web funciona localmente pero no después del despliegue**
Verifica que tus variables de entorno estén configuradas en la pestaña Environment de Dokploy.

**Los pagos de Stripe no funcionan en producción**
Asegúrate de estar usando claves en vivo (no las de prueba) y que estén configuradas en las variables de entorno de Dokploy.

**La construcción falla en Dokploy**
Revisa los registros de construcción (build logs) en Dokploy para ver los mensajes de error. Copia el error y pégalo en Claude Code:

```
I'm getting this error when deploying: [paste error here]. How do I fix it?
```

---

## Resumen

Esto es lo que has logrado:

1. **GitHub** — tu código está almacenado y con control de versiones
2. **Git + Node.js + Claude Code** — tu kit de desarrollo local
3. **Next.js** — un framework de sitios web moderno y rápido
4. **Stripe** — acepta pagos de clientes
5. **DigitalOcean + Dokploy** — tu sitio web está en vivo en internet
6. **Google Analytics** — puedes rastrear visitantes y medir el crecimiento

La belleza de esta configuración está en el flujo de trabajo que tienes por delante: abre Claude Code, describe lo que quieres cambiar, haz commit, push, y ya está en vivo. ¡Feliz vibe coding!
