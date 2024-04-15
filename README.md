# ggplot-tips

<br />
<br />

## 1. Poner coma de miles 

<br />

```r
ggplot( .... ) +
scale_y_continuous(
    labels = scales::comma
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



