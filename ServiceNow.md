# Gesammelte ServiceNow Erkenntnisse

## 📚 Weitere Dokumentation
Siehe auch die spezialisierten Guides in diesem Ordner:
- [CLI-Kommandos](CLI.md) - ServiceNow SDK Kommandozeilen-Befehle
- [UI-Entwicklungsansätze](UI_approach.md) - Empfehlungen für UI-Entwicklung
- [Arbeiten mit Tables](working-with-tables.md) - Tabellen im ServiceNow SDK erstellen
- [Arbeiten mit Records](working-with-records.md) - Datensätze im ServiceNow SDK verwalten



## Service Now Fluent language
https://www.servicenow.com/docs/r/application-development/servicenow-fluent.html

.now.ts files 
(=> TypeScript)


## Workflow
Neben einem lokalen `git pull` muss man sich auch Änderungen aus der Plattform holen
Irgendjemand ändert dort zB die Tabellen Struktur, dann muss ich syncen (siehe [CLI-Kommandos](CLI.md))
Man also zwei Source of truths... Low Coder coden dort in der UI und ändern Dinge und Devs coden hier in den Sourcen. Darüber muss man noch mal nachdenken

💡 **Siehe auch**: [UI-Entwicklungsansätze](UI_approach.md) für Empfehlungen zur UI-Entwicklung


## Folder structure

https://www.servicenow.com/docs/r/application-development/building-applications-source-code.html

## src
Directory containing the source code of your application. This directory includes the following subdirectories:

### client
Directory containing the client-side files for developing user interfaces.

### fluent
Directory containing ServiceNow Fluent code in .now.ts files. 

The generated subdirectory contains the application files converted to ServiceNow Fluent. *Do not make any changes here!* This is generated on every `npm run build`

📋 **Für Details siehe**: 
- [Arbeiten mit Tables](working-with-tables.md) - Tabellendefinitionen erstellen
- [Arbeiten mit Records](working-with-records.md) - Datensätze verwalten

### server
Directory containing JavaScript module code in .js or .ts files.
