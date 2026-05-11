# Working with Tables in ServiceNow SDK

## Überblick

Tables ermöglichen es, neue Datenbanktabellen in ServiceNow programmatisch zu definieren und zu erstellen. Sie werden mit dem ServiceNow SDK in TypeScript definiert und dann in die ServiceNow-Instanz übertragen. Jede Tabelle definiert ein Schema mit verschiedenen Spaltentypen.

## Table-Struktur

Eine Table wird mit der `Table()` Funktion aus `@servicenow/sdk/core` erstellt:

```typescript
import { Table, StringColumn, IntegerColumn } from '@servicenow/sdk/core'

export const table_name = Table({
    name: 'table_name',
    label: 'Human readable label',
    schema: {
        field1: StringColumn({ label: 'Field 1' }),
        field2: IntegerColumn({ label: 'Field 2' }),
        // weitere Felder...
    }
})
```

## Erforderliche Properties

### `name`
- Technischer Name der Tabelle in ServiceNow
- Wird automatisch mit dem Scope-Prefix versehen
- Beispiel: `'x_1961941_d_enab_0_tableone'`

### `label` (optional)
- Benutzerfreundlicher Anzeigename
- Beispiel: `'Example Table'`

### `schema`
- Objekt mit den Spaltendefinitionen
- Jede Spalte hat einen Namen und einen Spaltentyp
- Spaltenname wird als Schlüssel verwendet

## Verfügbare Spaltentypen

### StringColumn
```typescript
StringColumn({ 
    label: 'Text Field',
    mandatory: true,         // optional: Pflichtfeld
    maxLength: 255,          // optional: Maximale Länge
})
```

### ChoiceColumn (String mit Auswahloptionen)
```typescript
ChoiceColumn({
    label: 'Status',
    choices: {
        active: { label: 'Active' },
        inactive: { label: 'Inactive' },
    },
    dropdown: 'dropdown_without_none',  // optional
    default: 'active',                 // optional
})
```

### IntegerColumn
```typescript
IntegerColumn({ 
    label: 'Number Field',
    mandatory: true         // optional: Pflichtfeld
})
```

### DateTimeColumn
```typescript
DateTimeColumn({ 
    label: 'Date Time Field'
})
```

## Praktische Beispiele

### Einfache Tabelle
```typescript
export const x_1961941_d_enab_0_tableone = Table({
    name: 'x_1961941_d_enab_0_tableone',
    label: 'Example Table',
    schema: {
        x_1961941_d_enab_0_string_field: StringColumn({ label: 'String Field', mandatory: true }),
        x_1961941_d_enab_0_integer_field: IntegerColumn({ label: 'Integer Field', mandatory: true }),
        x_1961941_d_enab_0_datetime_field: DateTimeColumn({ label: 'Date Time Field' }),
    },
})
```

### Erweiterte Tabelle mit ChoiceColumn
```typescript
export const x_1961941_d_enab_0_christians_super_table = Table({
    name: 'x_1961941_d_enab_0_christians_super_table',
    label: 'Christians Super Tabelle',
    schema: {
        x_1961941_d_enab_0_string_field: StringColumn({ label: 'String Field', mandatory: true }),
        x_1961941_d_enab_0_integer_field: IntegerColumn({ label: 'Integer Field', mandatory: true }),
        x_1961941_d_enab_0_datetime_field: DateTimeColumn({ label: 'Date Time Field' }),
        x_1961941_d_enab_0_firstname_field: StringColumn({ label: 'First Name Field' }),
        nachname: ChoiceColumn({
            default: 'Greschus',
            choices: {
                Greschus: { label: 'Greschus' },
                Darsow: { label: 'Darsow' },
            },
            dropdown: 'dropdown_without_none',
            label: 'Nachname',
            maxLength: 55,
        }),
    },
})
```


## Datei-Organisation

Tables werden in `*.now.ts` Dateien im `src/fluent/` Ordner definiert:

- `src/fluent/index.now.ts` - Hauptdatei für Table-Definitionen
- Weitere `*.now.ts` Dateien können für bessere Organisation erstellt werden

## Deployment

Tables werden über das ServiceNow SDK in die Instanz übertragen:

```bash
npx now-sdk transform --auth <alias>
```

## Server-seitiger Zugriff

In Server-Scripts können die Tables über `GlideRecord` verwendet werden:

```typescript
const gr = new GlideRecord('x_1961941_d_enab_0_tableone');
gr.query();
while (gr.next()) {
    // Table-Daten verarbeiten
}
```