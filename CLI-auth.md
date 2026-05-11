# ServiceNow SDK Authentifizierung

## Übersicht
Die Authentifizierung für das ServiceNow SDK erfolgt über die CLI. Damit können verschiedene Instanzen und Benutzer verwaltet werden.

## Alle gespeicherten Zugangsdaten auflisten
```bash
npx @servicenow/sdk auth --list
```
Zeigt alle gespeicherten Aliase und deren Konfiguration an.

## Default Alias ändern
```bash
npx @servicenow/sdk auth --use <alias>
```
Setzt den angegebenen Alias als Standard für alle weiteren CLI-Befehle.

## Neuen Alias hinzufügen (Authentifizierung anlegen)
```bash
npx @servicenow/sdk auth --add <instance>
```
Führt einen Dialog durch, um eine neue Instanz mit Benutzername und Passwort zu hinterlegen.

## Alias entfernen
```bash
npx @servicenow/sdk auth --delete <alias>
```
Entfernt einen gespeicherten Alias aus der Konfiguration.

## Hinweise
- Die Zugangsdaten werden lokal gespeichert und können für verschiedene Instanzen genutzt werden.
- Nach dem Hinzufügen oder Ändern eines Alias empfiehlt sich ein Test der Verbindung, z.B. mit `npx @servicenow/sdk info --auth <alias>`.