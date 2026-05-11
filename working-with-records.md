# Working with Records in ServiceNow SDK

## Überblick

Records ermöglichen es, Dateneinträge für ServiceNow-Tabellen programmatisch zu definieren und zu erstellen. Sie werden mit dem ServiceNow SDK in TypeScript definiert und dann in die ServiceNow-Instanz übertragen.

## Record-Struktur

Ein Record wird mit der `Record()` Funktion aus `@servicenow/sdk/core` erstellt:

```typescript
import { Record } from '@servicenow/sdk/core'

export const recordName = Record({
    $id: Now.ID['unique-identifier'],
    table: 'table_name',
    data: {
        field1: 'value1',
        field2: 42,
        // weitere Felder...
    }
})
```

## Erforderliche Properties

### `$id`
- Eindeutige Identifizierung des Records
- Format: `Now.ID['identifier-name']`
- Beispiel: `Now.ID['incident-1']`

### `table`
- Name der Zieltabelle in ServiceNow
- Muss auf eine existierende Tabelle verweisen
- Beispiel: `'x_1961941_d_enab_0_tableone'`

### `data`
- Objekt mit den Feldwerten für den Record
- Feldnamen müssen mit der Tabellendefinition übereinstimmen
- Pflichtfelder müssen angegeben werden

## Praktische Beispiele

### Einfacher Record
```typescript
export const record1 = Record({
    $id: Now.ID['incident-1'],
    table: 'x_1961941_d_enab_0_tableone',
    data: {
        x_1961941_d_enab_0_string_field: 'true',
        x_1961941_d_enab_0_integer_field: 42,
    }
})
```

### Record mit DateTime-Feld
```typescript
export const record2 = Record({
    $id: Now.ID['incident-2'],
    table: 'x_1961941_d_enab_0_tableone',
    data: {
        x_1961941_d_enab_0_string_field: 'ServiceNow Enablement',
        x_1961941_d_enab_0_integer_field: 100,
        x_1961941_d_enab_0_datetime_field: '2026-04-02 10:30:00',
    }
})
```


## Deployment

Records werden zusammen mit Tabellendefinitionen über das ServiceNow SDK in die Instanz übertragen:

```bash
npx now-sdk transform --auth <alias>
```

## Zugriff auf Records (Server-seitig)

In Server-Scripts können die Records über `GlideRecord` abgerufen werden:

```typescript
const gr = new GlideRecord('x_1961941_d_enab_0_tableone');
gr.query();
while (gr.next()) {
    // Record verarbeiten
}
```