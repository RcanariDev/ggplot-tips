# ggplot-tips

<br />
<br />

## 1. Poner coma de miles y establecer limites del eje Y

<br />

```r
ggplot( .... ) +
scale_y_continuous(
    labels = scales::comma
    , limits = c(0, 300)
  )
```


<br />
<br />

## 2. Grafico de barra simple

<br />

```r
Data %>%  
  ggplot(
    data = .
  ) +
  geom_bar(
    mapping = aes(x = VarCat, y = VarNumerica)
    , stat = "identity"
  )
```

<br />
<br />

## 3. Cambiar nombre de los ejes x e y

<br />

```r
ggplot( ... ) +
  labs(
    x = "Año - Mes",
    y = "Total de Casos"
  )
```

<br />
<br />

