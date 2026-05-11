# Guide: ServiceNow UI Components mit TypeScript entwickeln

Diese Anleitung führt dich durch den kompletten Prozess, um eigene Web Components mit **TypeScript** für den ServiceNow UI Builder zu erstellen, lokal zu testen und auf deine Instanz zu deployen.

---

## 📋 1. Voraussetzungen

Bevor du startest, müssen folgende Tools auf deinem System installiert sein:

* **Node.js**: (LTS Version empfohlen).
* **ServiceNow CLI (SNC)**: Das offizielle Command Line Interface von ServiceNow.
* **Java Runtime Environment (JRE)**: Version 11 oder höher (wird für den Build-Prozess benötigt).
* **ServiceNow Instanz**: Eine aktive Instanz (z. B. eine Personal Developer Instance / PDI).

---

## 🛠️ 2. Setup & Konfiguration

### CLI Profil einrichten
Verbinde dein Terminal mit deiner Instanz, damit das CLI weiß, wohin der Code geliefert werden soll:

```bash
snc configure profile set
```

* Host: `https://deine-instanz.service-now.com`
* Login Method: `Username/Password` (oder OAuth)
* Output Format: `json`

### Projekt initialisieren
Erstelle einen neuen Ordner für dein Projekt und initialisiere die Komponente. Das Flag `--extension ts` ist entscheidend, um das TypeScript-Gerüst zu generieren:

```bash
# Ordner erstellen und hineinwechseln
mkdir my-custom-component
cd my-custom-component

# Projekt mit TypeScript-Support anlegen
snc ui-component project --name @my-scope/my-component --description "Meine TS Komponente" --extension ts
```

> **Wichtig:** Der Name muss zwingend ein Präfix mit `@` enthalten (z. B. `@firma/komponente`).

### Abhängigkeiten installieren

```bash
npm install
```

---

## 💻 3. Entwicklung

### Projektstruktur verstehen

* `src/`: Hier liegt dein TypeScript-Quellcode (z. B. `index.ts`).
* `now-ui.json`: Die wichtigste Konfigurationsdatei. Hier definierst du Properties (Eigenschaften) und Events, die später im UI Builder (rechtes Panel) sichtbar sein sollen.
* `package.json`: Enthält Metadaten und die Version deiner Komponente.

### Lokaler Development-Server
Du kannst deine Komponente live im Browser testen, ohne sie jedes Mal hochzuladen:

```bash
snc ui-component develop
```

Deine Komponente ist nun standardmäßig unter `http://localhost:8080` erreichbar.

---

## 🚀 4. Deployment

Sobald die Komponente fertig ist, musst du sie auf die Instanz übertragen.

### Build & Push
Der folgende Befehl kompiliert den TypeScript-Code automatisch in JavaScript und erstellt die notwendigen Datensätze in der Tabelle `sys_ux_lib_component`:

```bash
snc ui-component deploy
```

---

## 🎨 5. Nutzung im UI Builder

Nach dem erfolgreichen Deployment ist die Komponente auf der Instanz registriert und einsatzbereit:

1. Melde dich in deiner ServiceNow Instanz an.
2. Öffne den **UI Builder**.
3. Öffne eine bestehende Seite oder erstelle eine neue.
4. Klicke auf das **"+"** (Add Component) Icon im linken Menü.
5. Suche nach dem Namen deiner Komponente (z. B. `my-component`).
6. Ziehe die Komponente per Drag-and-drop auf die Canvas.
7. Konfiguriere die Properties im rechten Panel.

---

## 💡 Best Practices für TypeScript

* **Typisierung:** Nutze Interfaces für `state` und `properties` in deiner `index.ts`. Das gibt dir volle Autocomplete-Unterstützung in VS Code.
* **Properties abgleichen:** Achte darauf, dass die Namen der Properties in der `now-ui.json` exakt mit denen in deinem TypeScript-Interface übereinstimmen.
* **Versionsverwaltung:** Erhöhe bei größeren Updates die Version in der `package.json`, bevor du erneut `deploy` ausführst, um Konflikte zu vermeiden.

---

*Dokumentation erstellt für die Nutzung mit dem ServiceNow Next Experience UI Framework (Seismic).*
