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

## 2.1 Poner etiquetas SIMPLE a gráfico de barrats

<br />

- Agregar el parámetro **label**
- Manejar el espacio vertical con **vjust**

<br />

```r
DataPreg11 %>% 
  ggplot(
    data = .
  ) +
  geom_bar(
    mapping = aes(x = FechaMesOrdenAjustado, y = TotalCasos)
    , stat = "identity"
    , fill = "#087830"
  ) +
  geom_text(
    mapping = aes(x = FechaMesOrdenAjustado, y = TotalCasos, label = LabTotalCasos)
    , vjust = -1.6
    , color = "black"
    , size = 4
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

## 4.1 Poner etiquetas SIMPLE a grafico de barras agrupadas

<br />

- Se tiene que cambiar *fill* por **group**
- Agregar el parámetro **label**
- Se tiene poner **position** y **vjust**

<br />

```r
DataCanal11 %>% 
  ggplot(
    data = .
  ) + 
  geom_bar(
    mapping = aes(x = CanalVenta, y = TotalCasos, fill = FechaAjustada)
    , stat = "identity"
    , position = "dodge"
  ) +
  geom_text(
    mapping = aes(x = CanalVenta, y = TotalCasos, group = FechaAjustada, label = DifTotalLab)
    , position = position_dodge2(width = 0.9, preserve = "single")
    , vjust = -.5
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

## 7. Cambiar nombre a los ejes y la leyenda

<br />

- Se utiliza los parámetros: *x*, *y* y *fill*
  
<br />

```r
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


## 8. Unir ggplots

<br />

```r
library(ggpubr)

DataUnida11 <- ggarrange(
  PlotEmp11, PlotEmp12
  , ncol = 2
  , nrow = 1
  , common.legend = TRUE
  , legend = "top"
)
DataUnida11
```

<br />
<br />

# 8.1 Agregar spacio entre ggpubr

<br />

- Se tiene que agregar **NULL**
- Se tiene que agregar el parámetro **widths**

<br />

```r
library(ggpubr)
ImCanalUnida11 <- ggarrange(
  ImgCanal11, NULL, ImgCanal12
  , ncol = 3
  , nrow = 1
  # , common.legend = TRUE
  , legend = "top"
  , widths = c(1, .2, 1)
)
ImCanalUnida11
```

<br />
<br />


## 9. Guardar ggplot como imagen png o jpg

<br />

```r
ggsave("C:/Users/.../img/Img15.png", plot = DataUnida11, width=18, height=8, dpi=700)
```

<br />
<br />


## 10. Uso de grepl() para patrones

<br />

- Si contiene: **!grepl("-01", FechaMesOrdenAjustado)**
- No contiene: **grepl("-01", FechaMesOrdenAjustado)**
- Contiene varios valores (ó) (|): **grepl("-01|-02", FechaMesOrdenAjustado)**

<br />

```r
Data11 %>% 
  mutate(Mes = case_when(
    grepl("-01", FechaMesOrdenAjustado) ~ "Enero",
    grepl("-02", FechaMesOrdenAjustado) ~ "Febrero",
    grepl("-03", FechaMesOrdenAjustado) ~ "Marzo",
    grepl("-04", FechaMesOrdenAjustado) ~ "Abril"
  ), .before = FechaMesOrdenAjustado)

```

<br />
<br />





