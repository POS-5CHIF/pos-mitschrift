# Jupyter

`?` nach Funktion etc liefert Hilfe

# Pandas

## Arten von Daten

- nominale (=kategorische) "verbale" Daten, keine Rangordnung, zB Religionszugehörigkeit
- ordinale Daten, haben Rangordnung, lässt sich aber nicht vergleichen, zB Schulklassen, Noten
- metrische Daten, Merkmalsausprägungen, zB Alter, Einkommen
  - mit Verhältnis, zB 30 Jahre alt ist doppelt so alt wie 15 Jahre

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
col = pd.get_dummies(df['Spalte'], drop_first=True)
df = pd.concat([df, col], axis=1)
df.drop("Spalte", axis=1, inplace=True)
```

### Conditional Selection

Alle Spalten mit 'Dr':

```python
df[df['Name'].str.contains('Dr')]
```

Mehrere Conditions mit `&` verknüpfen

### Wie oft trifft Condition zu?

```python
df.isnull().sum()
```

isnull liefert array mit 0 und 1 -> aufsummiert also, wie oft isnull zutrifft

### Beispiel: Fehlende Daten löschen

Spalte löschen (`inplace=True` macht es direkt am df):

```python
df.drop(['Spalte'], axis=1, inplace=True)
```

Zeilen mit NaN löschen

```python
df.drop(df[df['Spalte'].isnull()].index, inplace=True)
```

NaN durch Medianwerte ersetzen:

```python
df.groupby('Spalte')['Age'].median()
df['Age'] = df.groupby('Spalte')['Age'].apply(lambda x: x.fillna(x.median()))
```

# Seaborn und pyplot

```python
sns.countplot(x='Spaltenname' df=mydataframe)
```

```python
plt.scatter(x, y)
```

```python
sns.regplot(x=x, y=y, data=data) # scatterplot mit Gerader, gut für lineare Regression
```

```python
sns.regplot(x=x, y=y, data=data) # wie regplot, aber data ist pd.DataFrame
```
