# Vibe Coding to Production

🇺🇸 [English](README.md) | 🇨🇳 [中文](README-zh.md) | 🇻🇳 [Tiếng Việt](README-vi.md) | 🇪🇸 [Español](README-es.md) | 🇩🇪 [Deutsch](README-de.md)

Eine vollständige Schritt-für-Schritt-Anleitung für **Nicht-Entwickler**, um eine Website von Grund auf zu erstellen und mit KI-gestütztem Programmieren (Vibe Coding) mithilfe von Claude Code in Produktion zu deployen.

Am Ende dieser Anleitung haben Sie:

- Eine vollständig funktionsfähige Next.js-Website
- Stripe-Zahlungsintegration
- Deployment auf einem Live-Server mit Dokploy
- Google Analytics-Tracking eingerichtet

Keine Programmiererfahrung erforderlich. Los geht's.

---

## Inhaltsverzeichnis

1. [GitHub-Konto & Repository erstellen](#1-github-konto--repository-erstellen)
2. [Git, Node.js & Claude Code installieren](#2-git-nodejs--claude-code-installieren)
3. [GitHub-Repository klonen](#3-github-repository-klonen)
4. [Claude Code einrichten](#4-claude-code-einrichten)
5. [Website mit Next.js erstellen](#5-website-mit-nextjs-erstellen)
6. [Stripe-Zahlungen einrichten](#6-stripe-zahlungen-einrichten)
7. [DigitalOcean-Server einrichten](#7-digitalocean-server-einrichten)
8. [Dokploy installieren & konfigurieren](#8-dokploy-installieren--konfigurieren)
9. [Website deployen](#9-website-deployen)
10. [Google Analytics einrichten](#10-google-analytics-einrichten)

---

## 1. GitHub-Konto & Repository erstellen

GitHub ist der Ort, an dem Ihr Website-Code gespeichert wird. Stellen Sie es sich als einen Cloud-Ordner für Ihr Projekt vor, der außerdem jede Änderung nachverfolgt, die Sie vornehmen.

### GitHub-Konto erstellen

1. Gehen Sie zu [github.com](https://github.com)
2. Klicken Sie auf **Sign up**
3. Geben Sie Ihre E-Mail-Adresse ein, erstellen Sie ein Passwort und wählen Sie einen Benutzernamen
4. Schließen Sie die Verifizierung ab und klicken Sie auf **Create account**
5. Überprüfen Sie Ihre E-Mail und bestätigen Sie Ihr Konto

### Neues Repository erstellen

Ein Repository (oder „Repo") ist wie ein Projektordner auf GitHub.

1. Klicken Sie nach dem Einloggen auf das **+**-Symbol in der oberen rechten Ecke
2. Klicken Sie auf **New repository**
3. Füllen Sie die Details aus:
   - **Repository name**: Wählen Sie einen Namen für Ihr Projekt (z. B. `my-website`)
   - **Description**: Optional, fügen Sie eine kurze Beschreibung hinzu
   - **Public** oder **Private**: Wählen Sie Private, wenn Sie nicht möchten, dass andere Ihren Code sehen
   - Aktivieren Sie **Add a README file**
4. Klicken Sie auf **Create repository**

<img width="100%" src="./images/github-create-repo.png" alt="GitHub-Repository erstellen" />

5. Sie haben nun ein Repository! Kopieren Sie die URL aus Ihrem Browser — sie sieht so aus: `https://github.com/your-username/my-website`

---

## 2. Git, Node.js & Claude Code installieren

Sie benötigen drei Tools auf Ihrem Computer: Git (zur Codeverwaltung), Node.js (zum lokalen Ausführen Ihrer Website) und Claude Code (Ihren KI-Programmierassistenten).

### Git installieren

Git ist das Tool, das Ihren Computer mit GitHub verbindet.

**Auf dem Mac:**

1. Öffnen Sie die App **Terminal** (suchen Sie mit Cmd + Space nach „Terminal" in Spotlight)
2. Geben Sie Folgendes ein und drücken Sie die Eingabetaste:
   ```bash
   git --version
   ```
3. Falls Git nicht installiert ist, erscheint ein Popup, das Sie auffordert, die Command Line Tools zu installieren — klicken Sie auf **Install**
4. Warten Sie, bis die Installation abgeschlossen ist

**Unter Windows:**

1. Gehen Sie zu [git-scm.com](https://git-scm.com)
2. Laden Sie das Installationsprogramm herunter und führen Sie es aus
3. Klicken Sie durch alle Standardoptionen mit **Next** und schließen Sie die Installation ab
4. Öffnen Sie **Git Bash** aus Ihrem Startmenü (verwenden Sie dies anstelle der normalen Eingabeaufforderung)

### Git konfigurieren

Teilen Sie Git nach der Installation mit, wer Sie sind. Öffnen Sie Ihr Terminal (Mac) oder Git Bash (Windows) und führen Sie Folgendes aus:

```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

Verwenden Sie dieselbe E-Mail-Adresse, die Sie für GitHub verwendet haben.

### Node.js installieren

Node.js ermöglicht es Ihnen, Ihre Website während der Entwicklung auf Ihrem Computer auszuführen.

1. Gehen Sie zu [nodejs.org](https://nodejs.org)
2. Laden Sie die **LTS**-Version herunter (die mit dem Hinweis „Recommended for most users")
3. Führen Sie das Installationsprogramm aus und folgen Sie den Standardoptionen
4. Überprüfen Sie die Installation, indem Sie Terminal öffnen und Folgendes ausführen:
   ```bash
   node --version
   npm --version
   ```
   Beide sollten eine Versionsnummer anzeigen.

### Claude Code installieren

Claude Code ist ein KI-Assistent, der in Ihrem Terminal läuft und Code für Sie schreibt.

1. Öffnen Sie Terminal und führen Sie Folgendes aus:
   ```bash
   npm install -g @anthropic-ai/claude-code
   ```
2. Überprüfen Sie die Installation:
   ```bash
   claude --version
   ```

---

## 3. GitHub-Repository klonen

„Klonen" bedeutet, Ihr GitHub-Repo auf Ihren Computer herunterzuladen, damit Sie lokal daran arbeiten können.

1. Öffnen Sie Terminal
2. Navigieren Sie zu dem Ort, an dem Ihr Projekt gespeichert werden soll. Um es beispielsweise in einem Ordner „Projects" abzulegen:
   ```bash
   mkdir -p ~/Projects
   cd ~/Projects
   ```
3. Klonen Sie Ihr Repo (ersetzen Sie dies durch Ihre tatsächliche URL aus Schritt 1):
   ```bash
   git clone https://github.com/your-username/my-website.git
   ```
4. Wechseln Sie in den Projektordner:
   ```bash
   cd my-website
   ```

Sie befinden sich jetzt in Ihrem Projektordner und sind bereit, mit dem Aufbau zu beginnen.

---

## 4. Claude Code einrichten

### Claude-Abonnement erwerben

Claude Code erfordert einen Anthropic API-Key oder ein Claude-Abonnement.

**Option A: Anthropic API-Key (Pay-as-you-go)**

1. Gehen Sie zu [console.anthropic.com](https://console.anthropic.com)
2. Registrieren Sie sich für ein Konto
3. Gehen Sie zu **Settings** > **API Keys**
4. Klicken Sie auf **Create Key** und kopieren Sie ihn
5. Fügen Sie Zahlungsinformationen unter **Settings** > **Billing** hinzu und laden Sie Guthaben auf (beginnen Sie mit $10–20)

**Option B: Claude Max-Abonnement (Unbegrenzte Nutzung)**

1. Gehen Sie zu [claude.ai](https://claude.ai)
2. Registrieren Sie sich und abonnieren Sie den **Max-Plan** ($100/Monat), der die Claude Code-Nutzung einschließt

### Claude Code mit Ihrem Konto verbinden

1. Öffnen Sie Terminal und navigieren Sie zu Ihrem Projektordner:
   ```bash
   cd ~/Projects/my-website
   ```
2. Starten Sie Claude Code:
   ```bash
   claude
   ```
3. Beim ersten Start werden Sie zur Authentifizierung aufgefordert:
   - Bei Verwendung eines **API-Keys**: Sie werden aufgefordert, Ihren Key einzugeben
   - Bei Verwendung eines **Claude-Abonnements**: Es öffnet sich ein Browserfenster zum Einloggen
4. Folgen Sie den Anweisungen auf dem Bildschirm, um die Authentifizierung abzuschließen

<img width="100%" src="./images/claude-code-first-launch.png" alt="Claude Code Erster Start" />

Sie sind jetzt bereit zum Vibe Coding! Claude Code liest Ihre Projektdateien und hilft Ihnen beim Aufbau Ihrer Website.

---

## 5. Website mit Next.js erstellen

Next.js ist ein beliebtes Framework zum Erstellen moderner Websites. Sie müssen es nicht verstehen — Claude Code richtet alles für Sie ein.

### Projekt initialisieren

Stellen Sie sicher, dass Sie sich in Ihrem Projektordner befinden, und starten Sie dann Claude Code:

```bash
cd ~/Projects/my-website
claude
```

Geben Sie folgenden Prompt ein:

```
Set up a new Next.js project in the current directory with TypeScript, Tailwind CSS,
and the App Router. Use the latest version of Next.js. Keep the default configuration
simple and clean.
```

Claude Code erstellt alle notwendigen Dateien. Wenn es fertig ist, können Sie Ihre Website lokal in der Vorschau ansehen:

```bash
npm run dev
```

Öffnen Sie Ihren Browser und gehen Sie zu `http://localhost:3000`, um Ihre Website zu sehen.

### Website-Layout gestalten

Teilen Sie Claude Code nun mit, wie Ihre Website aussehen soll. Hier sind einige Beispiel-Prompts, die Sie verwenden können:

**Für eine Landing Page:**

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

**Für eine mehrseitige Website:**

```
Create these pages for my website:
- Home page: landing page with hero, features, and testimonials
- About page: company story, team section with photos
- Pricing page: 3 pricing tiers (Basic, Pro, Enterprise) with feature comparison
- Contact page: a contact form with name, email, and message fields
Add a consistent navigation bar and footer across all pages.
```

**Für eine SaaS-Produktseite:**

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

**Um das Design zu verfeinern:**

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

### Tipps für Vibe Coding

- **Seien Sie konkret**: Je mehr Details Sie angeben, desto besser das Ergebnis
- **Iterieren Sie**: Wenn etwas nicht richtig aussieht, beschreiben Sie, was geändert werden soll
- **Verweisen Sie auf Websites, die Ihnen gefallen**: „Make it look like the Stripe homepage" gibt Claude Code einen Referenzpunkt
- **Bitten Sie um Korrekturen**: Wenn Sie einen Fehler sehen, beschreiben Sie ihn einfach — „The navigation menu is overlapping the hero section on mobile, please fix it"

---

## 6. Stripe-Zahlungen einrichten

Stripe ermöglicht es Ihnen, Zahlungen auf Ihrer Website zu akzeptieren. Sie richten ein Stripe-Konto ein und verwenden dann Claude Code, um Zahlungsfunktionen hinzuzufügen.

### Stripe-Konto erstellen

1. Gehen Sie zu [stripe.com](https://stripe.com)
2. Klicken Sie auf **Start now** und erstellen Sie ein Konto
3. Nach dem Einloggen befinden Sie sich standardmäßig im **Testmodus** (Sie sehen einen Umschalter im Dashboard) — das ist ideal zum Entwickeln; es wird kein echtes Geld belastet
4. Gehen Sie zu **Developers** > **API keys**
5. Sie sehen zwei Keys:
   - **Publishable key**: beginnt mit `pk_test_...`
   - **Secret key**: beginnt mit `sk_test_...` (zum Anzeigen klicken)

6. Lassen Sie diese Seite geöffnet — Sie benötigen beide Keys

### Produkte in Stripe erstellen

1. Gehen Sie im Stripe-Dashboard zu **Product catalog** > **Add product**
2. Erstellen Sie Ihre Preisstufen:
   - Name: "Basic Plan"
   - Preis: $9/Monat (oder was auch immer Sie möchten)
   - Klicken Sie auf **Save product**
3. Wiederholen Sie dies für andere Stufen (Pro, Enterprise usw.)
4. Kopieren Sie für jedes Produkt die **Price ID** (beginnt mit `price_...`) — diese werden Sie benötigen

### Stripe zu Ihrer Website hinzufügen

Starten Sie Claude Code in Ihrem Projektordner und verwenden Sie diese Prompts:

**Stripe-Integration einrichten:**

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

**Preisseite mit Checkout hinzufügen:**

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

**Ihre echten Stripe-Keys hinzufügen:**

```
Update the .env.local file with my real Stripe keys:
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_test_your_actual_key_here
STRIPE_SECRET_KEY=sk_test_your_actual_key_here
```

### Zahlungen testen

1. Führen Sie Ihre Website lokal mit `npm run dev` aus
2. Gehen Sie zur Preisseite und klicken Sie auf einen Kaufbutton
3. Verwenden Sie auf der Stripe-Checkout-Seite die Testkartennummer: `4242 4242 4242 4242`
   - Ablaufdatum: ein beliebiges zukünftiges Datum
   - CVC: beliebige 3 Ziffern
4. Schließen Sie den Kauf ab — Sie sollten zur Erfolgsseite weitergeleitet werden
5. Überprüfen Sie Ihr Stripe-Dashboard unter **Payments**, um die Testzahlung zu sehen

### Auf echte Zahlungen umstellen

Wenn Sie bereit für echte Zahlungen sind:

1. Schließen Sie die Einrichtung Ihres Stripe-Kontos ab (Geschäftsdaten, Bankkonto)
2. Wechseln Sie im Stripe-Dashboard vom **Testmodus** in den **Live-Modus**
3. Kopieren Sie Ihre Live-API-Keys (sie beginnen mit `pk_live_` und `sk_live_`)
4. Aktualisieren Sie Ihre `.env.local` mit den Live-Keys

---

## 7. DigitalOcean-Server einrichten

Sie benötigen einen Server, um Ihre Website zu hosten, damit jeder über das Internet darauf zugreifen kann.

### DigitalOcean-Konto erstellen

1. Gehen Sie zu [digitalocean.com](https://www.digitalocean.com)
2. Klicken Sie auf **Sign up** und erstellen Sie ein Konto
3. Fügen Sie eine Zahlungsmethode hinzu (Kreditkarte oder PayPal)
4. Als neuer Nutzer erhalten Sie möglicherweise $200 an kostenlosem Guthaben für 60 Tage

### Server erstellen (Droplet)

1. Klicken Sie nach dem Einloggen auf **Create** > **Droplets**
2. Wählen Sie folgende Einstellungen:
   - **Region**: Wählen Sie die Ihren Nutzern nächstgelegene (z. B. San Francisco, New York, London)
   - **Image**: Wählen Sie **Ubuntu 22.04 (LTS)** oder das neueste Ubuntu LTS
   - **Size**: Wählen Sie **Basic** > **Regular** > **$12/mo** (2 GB RAM / 1 CPU) — das reicht für den Anfang
   - **Authentication**: Wählen Sie **Password** und legen Sie ein starkes Root-Passwort fest (bewahren Sie es sicher auf!)
3. Klicken Sie auf **Create Droplet**
4. Warten Sie ca. 60 Sekunden, bis er hochgefahren ist
5. Kopieren Sie die angezeigte **IP-Adresse** (z. B. `164.90.xxx.xxx`) — diese werden Sie benötigen

---

## 8. Dokploy installieren & konfigurieren

Dokploy ist ein kostenloses Open-Source-Tool, das das Deployen Ihrer Website so einfach macht wie einen Knopfdruck. Es ist wie eine einfachere Version von Vercel oder Heroku, die auf Ihrem eigenen Server läuft.

### Dokploy auf Ihrem Server installieren

1. Öffnen Sie Terminal auf Ihrem Computer
2. Verbinden Sie sich über SSH mit Ihrem Server:
   ```bash
   ssh root@your-server-ip-address
   ```
3. Geben Sie `yes` ein, wenn Sie nach dem Fingerprint gefragt werden, und geben Sie dann Ihr Server-Passwort ein
4. Sobald Sie verbunden sind, führen Sie den Dokploy-Installationsbefehl aus:
   ```bash
   curl -sSL https://dokploy.com/install.sh | sh
   ```
5. Warten Sie, bis die Installation abgeschlossen ist (das dauert einige Minuten)
6. Wenn fertig, wird eine URL wie `http://your-server-ip:3000` angezeigt

### Dokploy einrichten

1. Öffnen Sie Ihren Browser und gehen Sie zu `http://your-server-ip:3000`
2. Sie sehen den Dokploy-Einrichtungsbildschirm
3. Erstellen Sie ein Administrator-Konto:
   - Geben Sie Ihre E-Mail-Adresse ein
   - Erstellen Sie ein Passwort
   - Klicken Sie auf **Register**
4. Sie befinden sich jetzt im Dokploy-Dashboard

### Dokploy mit GitHub verbinden

Damit kann Dokploy Ihren Code automatisch von GitHub abrufen.

1. Gehen Sie in Dokploy zu **Settings** (Zahnrad-Symbol) > **Git Providers**
2. Klicken Sie auf **Add GitHub**
3. Sie werden zu GitHub weitergeleitet — klicken Sie auf **Authorize**, um Dokploy Zugriff zu gewähren
4. Wählen Sie aus, auf welche Repositories Dokploy zugreifen kann:
   - Wählen Sie **Only select repositories** und wählen Sie Ihr Website-Repo
   - Klicken Sie auf **Install & Authorize**
5. Sie werden zurück zu Dokploy weitergeleitet — die Verbindung ist nun aktiv

---

## 9. Website deployen

### Code zu GitHub pushen

Bevor Sie deployen, müssen Sie Ihren Code zu GitHub pushen. Gehen Sie zurück zu Ihrem lokalen Terminal (nicht die Server-SSH-Sitzung) und führen Sie Folgendes aus:

1. Öffnen Sie Terminal und gehen Sie zu Ihrem Projektordner:
   ```bash
   cd ~/Projects/my-website
   ```
2. Fügen Sie alle Ihre Dateien zu Git hinzu:
   ```bash
   git add .
   ```
3. Erstellen Sie einen Commit (eine Momentaufnahme Ihres Codes):
   ```bash
   git commit -m "Initial website build"
   ```
4. Pushen Sie ihn zu GitHub:
   ```bash
   git push origin main
   ```

Falls dies Ihr erster Push ist, könnte Git Sie bitten, sich bei GitHub anzumelden. Folgen Sie den Anweisungen.

**Tipp:** Sie können dies auch über Claude Code tun:

```
Commit all changes with the message "Initial website build" and push to GitHub.
```

### Anwendung in Dokploy erstellen

1. Klicken Sie im Dokploy-Dashboard auf **Projects** in der Seitenleiste

<img width="100%" src="./images/dokploy-projects.png" alt="Dokploy Projekte" />

2. Klicken Sie auf **Create Project** und geben Sie ihm einen Namen (z. B. „My Website")
3. Klicken Sie innerhalb des Projekts auf **Create Service** > **Application**
4. Konfigurieren Sie die Anwendung:
   - **Name**: Geben Sie ihr einen Namen (z. B. „web")
   - **Source**: Wählen Sie **GitHub**
   - **Repository**: Wählen Sie Ihr Website-Repository
   - **Branch**: `main`
   - **Build Type**: Wählen Sie **Nixpacks** (erkennt Ihren Projekttyp automatisch)
5. Klicken Sie auf **Save**

### Umgebungsvariablen einrichten

Ihre Website benötigt die Stripe-Keys, um in der Produktion zu funktionieren.

1. Gehen Sie in Ihren Anwendungseinstellungen in Dokploy zum Tab **Environment**
2. Fügen Sie Ihre Umgebungsvariablen hinzu (eine pro Zeile):
   ```
   NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_live_your_key
   STRIPE_SECRET_KEY=sk_live_your_key
   ```
3. Klicken Sie auf **Save**

### Domain einrichten (Optional, aber empfohlen)

Falls Sie einen Domainnamen haben:

1. Gehen Sie in Dokploy zu Ihrer Anwendung > Tab **Domains**
2. Klicken Sie auf **Add Domain**
3. Geben Sie Ihre Domain ein (z. B. `www.mywebsite.com`)
4. Aktivieren Sie **HTTPS** (kostenloses SSL-Zertifikat über Let's Encrypt)
5. Klicken Sie auf **Save**
6. Fügen Sie bei Ihrem Domain-Registrar (wo Sie die Domain gekauft haben) einen DNS-Eintrag hinzu:
   - **Type**: A
   - **Name**: `@` (oder `www`)
   - **Value**: die IP-Adresse Ihres Servers
   - **TTL**: 3600

### Deployen

1. Gehen Sie in Dokploy zu Ihrer Anwendung und klicken Sie auf **Deploy**
2. Beobachten Sie die Build-Logs — Dokploy wird:
   - Ihren Code von GitHub abrufen
   - Abhängigkeiten installieren
   - Ihre Next.js-Website erstellen
   - Sie starten
3. Sobald der Build abgeschlossen ist, ist Ihre Website live!

### Auto-Deploy bei Push

Dokploy kann automatisch deployen, sobald Sie neuen Code zu GitHub pushen:

1. Gehen Sie in Ihren Anwendungseinstellungen zum Tab **General**
2. Aktivieren Sie **Auto Deploy**
3. Jedes Mal, wenn Sie Code zu GitHub pushen, erstellt und deployed Dokploy automatisch neu

### Der vollständige Arbeitsablauf: Änderungen vornehmen und deployen

Das ist Ihr täglicher Arbeitsablauf zum Aktualisieren Ihrer Website:

1. Öffnen Sie Terminal, navigieren Sie zu Ihrem Projekt und starten Sie Claude Code:
   ```bash
   cd ~/Projects/my-website
   claude
   ```
2. Teilen Sie Claude Code mit, was geändert werden soll:
   ```
   Change the hero headline to "Welcome to the Future" and update the
   background color to dark blue.
   ```
3. Vorschau lokal unter `http://localhost:3000` anzeigen (führen Sie `npm run dev` aus)
4. Wenn Sie mit den Änderungen zufrieden sind, committen und pushen Sie:
   ```bash
   git add .
   git commit -m "Update hero section"
   git push origin main
   ```
5. Dokploy deployed Ihre Änderungen automatisch. Fertig!

---

## 10. Google Analytics einrichten

Mit Google Analytics können Sie sehen, wie viele Personen Ihre Website besuchen, woher sie kommen und welche Seiten sie aufrufen.

### Google Analytics-Konto erstellen

1. Gehen Sie zu [analytics.google.com](https://analytics.google.com)
2. Klicken Sie auf **Start measuring**
3. Füllen Sie die Kontodetails aus:
   - **Account name**: Ihr Name oder Unternehmensname
   - Klicken Sie auf **Next**
4. Erstellen Sie eine Property:
   - **Property name**: Ihr Website-Name
   - Wählen Sie Ihre Zeitzone und Währung
   - Klicken Sie auf **Next**
5. Füllen Sie Ihre Geschäftsdaten aus und klicken Sie auf **Create**
6. Akzeptieren Sie die Nutzungsbedingungen

### Ihre Mess-ID erhalten

1. Gehen Sie in Google Analytics zu **Admin** (Zahnrad-Symbol) > **Data Streams**
2. Klicken Sie auf **Add stream** > **Web**
3. Geben Sie Ihre Website-URL und einen Stream-Namen ein
4. Klicken Sie auf **Create stream**
5. Kopieren Sie die **Measurement ID** — sie sieht so aus: `G-XXXXXXXXXX`

<img width="100%" src="./images/google-analytics-measurement-id.png" alt="Google Analytics Mess-ID" />

### Google Analytics zu Ihrer Website hinzufügen

Starten Sie Claude Code in Ihrem Projektordner und verwenden Sie diesen Prompt:

```
Add Google Analytics to my Next.js project.
My Google Analytics Measurement ID is G-XXXXXXXXXX (replace with your real ID).
Set it up using the recommended approach with the Next.js Script component.
Add it to the root layout so it tracks all pages. Use an environment variable
called NEXT_PUBLIC_GA_MEASUREMENT_ID for the ID.
```

Fügen Sie dann die Umgebungsvariable hinzu:

1. **Lokal**: Fügen Sie es zu Ihrer `.env.local`-Datei hinzu:
   ```
   NEXT_PUBLIC_GA_MEASUREMENT_ID=G-XXXXXXXXXX
   ```
2. **Auf Dokploy**: Fügen Sie dieselbe Variable im Tab **Environment** Ihrer Anwendung hinzu

### Überprüfen, ob es funktioniert

1. Pushen Sie Ihre Änderungen zu GitHub:
   ```bash
   git add .
   git commit -m "Add Google Analytics"
   git push origin main
   ```
2. Warten Sie, bis Dokploy deployed hat
3. Besuchen Sie Ihre Live-Website
4. Gehen Sie in Google Analytics zu **Reports** > **Realtime**
5. Sie sollten sich selbst als aktiven Nutzer sehen

---

## Kurzübersicht: Nützliche Befehle

| Was Sie tun möchten                   | Befehl                                          |
| ------------------------------------- | ----------------------------------------------- |
| Terminal öffnen                       | Cmd + Space, „Terminal" eingeben (Mac)          |
| In Ihren Projektordner navigieren     | `cd ~/Projects/my-website`                      |
| Claude Code starten                   | `claude`                                        |
| Website lokal ausführen               | `npm run dev`                                   |
| Lokalen Server stoppen                | `Ctrl + C` im Terminal drücken                  |
| Änderungen in Git speichern           | `git add .` dann `git commit -m "your message"` |
| Zu GitHub pushen                      | `git push origin main`                          |
| Neuesten Code abrufen                 | `git pull origin main`                          |
| Projektstatus prüfen                  | `git status`                                    |
| Mit Ihrem Server verbinden            | `ssh root@your-server-ip`                       |

## Fehlerbehebung

**„command not found: node"**
Node.js ist nicht korrekt installiert. Installieren Sie es erneut von [nodejs.org](https://nodejs.org).

**„command not found: claude"**
Führen Sie `npm install -g @anthropic-ai/claude-code` erneut aus.

**Git fragt jedes Mal nach Benutzername/Passwort**
Richten Sie SSH-Keys ein oder verwenden Sie die GitHub CLI (`gh auth login`).

**Website funktioniert lokal, aber nicht nach dem Deployment**
Überprüfen Sie, ob Ihre Umgebungsvariablen im Environment-Tab von Dokploy gesetzt sind.

**Stripe-Zahlungen funktionieren nicht in der Produktion**
Stellen Sie sicher, dass Sie Live-Keys (keine Test-Keys) verwenden und diese in den Umgebungsvariablen von Dokploy gesetzt sind.

**Build schlägt auf Dokploy fehl**
Überprüfen Sie die Build-Logs in Dokploy auf Fehlermeldungen. Kopieren Sie den Fehler und fügen Sie ihn in Claude Code ein:

```
I'm getting this error when deploying: [paste error here]. How do I fix it?
```

---

## Zusammenfassung

Das haben Sie erreicht:

1. **GitHub** — Ihr Code ist gespeichert und versioniert
2. **Git + Node.js + Claude Code** — Ihr lokales Entwicklungs-Toolkit
3. **Next.js** — ein modernes, schnelles Website-Framework
4. **Stripe** — Zahlungen von Kunden akzeptieren
5. **DigitalOcean + Dokploy** — Ihre Website ist live im Internet
6. **Google Analytics** — Sie können Besucher nachverfolgen und das Wachstum messen

Das Schöne an diesem Setup ist der Arbeitsablauf, der von nun an gilt: Claude Code öffnen, beschreiben, was Sie ändern möchten, committen, pushen, und schon ist es live. Viel Spaß beim Vibe Coding!
