# Offene Fragen und Punkte – ServiceNow Projekt

## 1. Testing

### Frontend-Testing

- Wie können wir **Frontend-Testing** in ServiceNow durchführen?
  - Gibt es spezifische Tools oder Frameworks, die für ServiceNow geeignet sind?

### API-Tests

- Wie können wir **API-Tests** für ServiceNow durchführen?
  - Welche Tools oder Frameworks (z. B. Postman, RestAssured, Cypress) sind geeignet?
  - Wie können wir die API-Endpunkte testen, die von Low-Code-Komponenten genutzt werden?

### Unit- und Implementation-Tests

- Wie können wir **Unit-Tests** und **Implementation-Tests** in ServiceNow durchführen?
  - Gibt es Möglichkeiten, Tests direkt in ServiceNow zu schreiben (z. B. mit Scripted REST APIs oder ServiceNow-Test-Frameworks)?

---

## 2. Lokale Entwicklungsumgebung

### Lokale Datenbank/Cache

- Könnte man **lokal eine Datenbank im Cache** nutzen, sodass die im lokalen Repository definierten Tabellen auch zu lokalen Tabellen generiert werden?

### Lokales funktionales Backend


  - Gibt es Möglichkeiten, ein laufendes Backend mit Node.js zu simulieren?

---

## 3. Entwicklungsflow: Low-Code vs. Pro-Code

- Wie könnte der **Entwicklungsflow** im Zusammenspiel von Low-Code und Pro-Code aussehen?
  - Welche Teile des Projekts sollten in Low-Code (z. B. UI Builder) und welche in Pro-Code (z. B. JavaScript, Python) entwickelt werden?
  - Gibt es Best Practices für die Zusammenarbeit zwischen Low-Code- und Pro-Code-Entwicklern?
  - Wie vermeiden wir Konflikte bei der gleichzeitigen Arbeit an derselben Komponente?

---

## 4. Client Scripting

- Soll **Client Scripting** komplett nur im UI Builder stattfinden?
  - Wie kann eine **parallele Entwicklung** ermöglicht werden, wenn zwei Entwickler an derselben Truth of Source arbeiten?
  - Gibt es Möglichkeiten, Feature-Branches oder andere Git-Strategien in ServiceNow zu nutzen?
  - Wie können wir Merge-Konflikte vermeiden?

---

## 5. ServiceNow-Instanzen

- Gibt es eine **Staging-Instanz** von ServiceNow?
  - Wie können wir eine **Entwickler-Instanz** einrichten?
  - Welche Möglichkeiten gibt es, Änderungen zwischen Instanzen (z. B. Dev → Staging → Prod) zu synchronisieren?

---

## 6. Bug Reports und Feature Requests

- Wie sollen **Bug Reports** und **Feature Requests** von Nutzern gehandhabt werden?
  - Soll eine **Service-Hotline** eingerichtet werden?
  - Wie können wir die Kommunikation zwischen Entwicklern und Nutzern organisieren?

---

## 7. Sonstiges

- Wie können wir die Dokumentation und das Wissensmanagement für das Projekt sicherstellen?
