# ServiceNow SDK CLI Kommandos

## Überblick
Das ServiceNow SDK wird über die Kommandozeilenschnittstelle bedient:
```bash
npx @servicenow/sdk
```

## Build-Prozess

### Applikation aus dem lokalen Code bauen
```bash
npx @servicenow/sdk build
```
Die Build-Ergebnisse werden im Verzeichnis „dist/app" ausgegeben, einschließlich der Metadaten als XML-Dateien im Verzeichnis „dist/app/update".


## Synchronisation mit der ServiceNow-Plattform
Die Information, mit welcher App die Synchronisation durchgeführt wird, steht in der Datei `now.config.json`.

### ServiceNow → lokaler Code (Transform)
```bash
npx @servicenow/sdk transform --auth <alias>
```
oder alternativ:
```bash
npm run transform
```

### Lokaler Code → ServiceNow (Install)
Erst bauen, dann installieren:
```bash
npx @servicenow/sdk build
npx @servicenow/sdk install --auth <alias>
```

## Typical Workflow
1. Lokale Änderungen durchführen
2. `npx @servicenow/sdk build` - Code bauen
3. `npx @servicenow/sdk install --auth <alias>` - Auf ServiceNow-Plattform deployieren
4. Bei Änderungen auf der Plattform: `npx @servicenow/sdk transform --auth <alias>` - Änderungen zurückholen