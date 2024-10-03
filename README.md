# Caso_Practico_Rstudio
En este repositorio se presenta las consultas realizadas en el software de R  de acuerdo al caso practicto agregado.


## Objetivo

Realizacion de un analisis de una base de datos del titanic de las  personas que sobrevivieron con ayuda del software Rstudio.

## Producto

El análisis realizado arroja datos curiosos de las personas a bordo del Titanic, como se desglosa a continuación.


Se usaron las siguientes librarias 

```
library(readxl)
library(tidyverse)
library(ggplot2)
library(dplyr)
library(tidyr)
```

Crear una tabla nueva por Pclass 

```
type_class <- filter(titanic, Pclass %in% c("Lower Class", "Middle Class", "Upper Class"))
```

> Promedio de edades a bordo del Titanic

```
total_age <- sum(titanic$Age, na.rm = TRUE)
```

```
avg_age <- mean(titanic$Age, na.rm = TRUE)
```


> El promedio de edades abordo es de 30 años


```
view(avg_age)
```

Selecciona las los campos  Ticket, Name, Survived, Age
Filtrar las personas que sobrevivieran 
Filtrar las personas que son mayores de 18

```
titanic %>%
  select(Ticket, Name, Survived, Age) %>%
  filter(Survived == "Yes") %>%
  filter(Age > 18) %>%
  head(15)
```


  ![yes](https://github.com/user-attachments/assets/0b9888e6-06b7-4332-a660-74b97b3dda47)


Selecciona Name, Sex, survived, Age, Embarked
Filtrar las personas que no sobrevivieran 
Filtrar las edades que marquen NULL en la columna de Age

```
titanic %>%
  select(Name, Sex, Survived, Age, Embarked) %>%
  filter(Survived == "No") %>%
  filter(is.na(Age)) %>%
  head(15)
```


![age](https://github.com/user-attachments/assets/729ed50f-eb5f-44d6-90fc-84ae31ffcf3e)


Crear una gráfica de barras de la cantidad de personas que tuvieron deceso en el Viaje:  

```
titanic %>%
  ggplot(aes(x = Survived)) +
  geom_bar()
  ```


![survived](https://github.com/user-attachments/assets/d623b754-2b93-4b4f-95a2-c282672176d0)


> Como se muestra en la grafica mas del 50% de las personas que viajaron tuvieron fallecieron. 

Gráfica los puntos de Embarcacion que tubo el barco:


`titanic %>%
  ggplot(aes(x = Embarked)) +
  geom_bar()`

![embarked](https://github.com/user-attachments/assets/0ea4174f-1f71-4e74-a40f-dd472cfcedf5)
  

> Se muestra que en Southampton fue el mayor donde se abordo el mayor numero de personas.
  

 Gráfica donde se ubican las personas que sobrevivieron y el Tipo de clase que sobrevivio:


```
titanic %>%
  ggplot(aes(x = Survived, y = Age, color = Pclass)) + 
  geom_point()
  ```



![Pclass](https://github.com/user-attachments/assets/2780a18e-cc26-42ba-b90b-8492cd09f0a9)


> La grafica arroja en la visualiacion que las personas que lograron sobrevivieron son de Upper Class  de un promedio de personas mayores de 20 años




 Gráfica donde se ubican las personas que sobrevivieron y donde embarcaron:


```
titanic %>%
  ggplot(aes(x = Survived, y = Age, color = Embarked)) + 
  geom_point()
  ```


![edad, embarked](https://github.com/user-attachments/assets/f629d114-4694-482f-bb22-ac5ed6772a24)


  > Como se puede observar en la grafica muestra que en la mayoria fallecieron las personas embarcadas en Southampton

