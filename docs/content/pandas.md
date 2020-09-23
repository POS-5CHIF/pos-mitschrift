# Pandas

## Arten von Daten

- nominale (=kategorische) verbale Daten, keine Rangordnung, zB Religionszugehörigkeit
- ordinale Daten, haben Rangordnung, lässt sich aber nicht vergleichen, zB Schulklassen, Noten
- metrische Daten, Merkmalsausprägungen, zB Alter, Einkommen

## Datenaufbereitung

### Alle Zeilen löschen, wo mindestens eine Spalte fehlt

eher nicht verwenden, da dadurch idR Anzahl der Datensätze stark reduziert wird

```python
data.dropna()
```

### Daten ergänzen mit Mittelwert

Nicht nur mit Mittelwert des ganzen DF, sondern Mittelwert innerhalb von Gruppierungen (mit groupBy)

### Nominale Daten in Ziffern umwandeln

Mit one hot encoding:

```python
pd.get_dummies(series)
```
