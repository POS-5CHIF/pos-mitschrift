# Lineare Regression

- Für Berechnung von kontinuierlichen Werten

einziger Eingangsparameter ist Intercept falls dieser bekannt ist

$\widehat{y}$ ist geschätzter Wert

$\widehat{y}=a\cdot{}x+b$

$\sum_{i=1}^{n}(y_i-\widehat{y_i})^{2}$ (der Fehler) soll minimal werden

Gerade geht immer durch $(\overline{x}/\overline{y})$

Gradientenabstiegsverfahren (Gradient Descent) zur Fehlerminimierung

```python
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(df[["Height"]], df[["Weight"]],
test_size=0.2, random_state=0)

model = LinearRegression()
model.fit(X_train,y_train) # trainiert Modell
print(model.coef_, model.intercept_) # Koeffizienten sind m1, m2 etc, Intercept ist b
predictions = model.predict(X_test)
model.score(X_test, y_test) # Testen des models
```

score (0-1) bei zB Klassifizierung einfacher zu verstehen als bei linearer Regression

$$
R^2 = 1 - \frac
{\sum_{i=1}^{n}(y_i-\widehat{y_i})^{2}}
{\sum_{i=1}^{n}(y_i-\overline{y})^{2}}
$$

$R^2$ ist also eine Verhältniszahl zum "schlechtesten Modell":

- $R^2 = 1$: perfektes Modell,
- $R^2 = 0$: gleich gut wie "schlechtestes Modell",
- $R^2 < 0$: schlechter als "schlechtestes Modell"

Korrelationskoeffizient $\rho$ (ergibt nur im Zweidimensionalen Sinn):

- $0.8 < |\rho| < 1$: Punkte liegen "gut auf der Linie"
- $|\rho| = 0$: kein "Zusammenhang" zwischen den Lagen der Punkte

Bei gaußscher Glockenkurve ist Distanz zwischen Scheitel der Kurve und Wendepunkte die Standardabweichung -> grafisch ablesbar!

# Logistische Regression

- binäre Klassifizierung
- zuerst lineare Regression, darauf dann Sigmoid
- `liblinear` für binäre Klassifizierung
- `newton-cg` für nicht-binäre Klassifizierung

```python
# ...
model = LogisticRegression(solver='liblinear')
# ...
```

# Confusion Matrix

```python
from sklearn.metrics import confusion_metrics
confusion_matrix(y_test, predictions)
```

# Grid Search

- Optimierung eines Modells durch Variation der Hyperparameter

# KNN

- sehr langsam
- leicht zu verstehen

## Eingangswerte skalieren

```python
from sklearn.preprocessing import StandardScaler
sc = StandardScaler()
sc.fit(transform(X_train))
sc.transform(X_test)
```

Berechnung erfolgt intern: $\frac{x-mean(x)}{std(x)}$

# Naive Bayes

- setzt voraus dass Features unabhängig ist, da er einfach Multiplikationssatz verwendet
- muss nicht skaliert werden, da er sowieso Mittelwert und std verwendet
