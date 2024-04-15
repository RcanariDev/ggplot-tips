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

## 4. Grafico de barra agrupado simple

<br />

```r
DataEmp11 %>% 
  ggplot(
    data = .
  ) +
  geom_bar(
    mapping = aes(x = NombreCompania, y = TotalCasos, fill = FechaMesOrdenAjustado)
    , stat = "identity"
    , position = "dodge"
  )
```

<br />
<br />

## 5. Agregar un área de sombras entre dos lines

<br />

Se emplea la función *annotate()*

<br />

```r
DataSem12 %>% 
  ggplot(
    data = .
  ) +
  geom_line(
    mapping = aes(x = DiaSemana, y = TotalCasos, group = Anio, color = Anio)
  ) +
  geom_point(
    mapping = aes(x = DiaSemana, y = TotalCasos, group = Anio, color = Anio)
  )+
  scale_color_manual(
    values = c("red", "blue")
  ) +
  annotate('rect', xmin=3.5, xmax=6.5, ymin=-Inf, ymax=Inf, alpha=.4, fill='grey') +
  theme_bw()

```

<br />
<br />

## 6. Agregar detalle a un tema predeterminado

<br />

- Se aumenta *theme()* al tema predeterminado *theme_bw()*

<br />

```r
DataSem12 %>% 
  ggplot(
    data = .
  ) +
  theme_bw() +
  theme(axis.text.x = element_text(angle = 45, vjust = 1, hjust=1)
  )
```


<br />
<br />

# 7. Cambiar nombre a los ejes y la leyenda

<br />

- Se utiliza los parámetros: *x*, *y* y *fill*
  
<br />

````r
DataSem12 %>% 
  ggplot(
    data = .
  ) +
    labs(
        x = "Nombre Compañia"
        , y = "Total Casos"
        , fill = "Fecha (Viernes)"
      ) 
```


<br />
<br />




