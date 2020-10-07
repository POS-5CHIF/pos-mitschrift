# Lineare Regression

einziger Eingangsparameter ist Intercept falls dieser bekannt ist

$\widehat{y}$ ist geschätzter Wert

$\widehat{y}=a\cdot{}x+b$

$\sum_{i=1}^{n}(y_i-\widehat{y_i})^{2}$ (der Fehler) soll minimal werden

Gerade geht immer durch $(\overline{x}/\overline{y})$

Gradientenabstiegsverfahren (Gradient Descent) zur Fehlerminimierung

```python
from sklearn.linear_model import LinearRegression

model = LinearRegression()
model.fit(X,y) # trainiert Modell
print(model.coef_, model.intercept_) # Koeffizienten sind m1, m2 etc, Intercept ist b
predictions = model.predict(X_test)
model.score() # Testen des Modells
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

Bei gaußscher Glockekurve ist Distanz zwischen Scheitel der Kurve und Wendepunkte die Standardabweichung -> grafisch ablesbar!
