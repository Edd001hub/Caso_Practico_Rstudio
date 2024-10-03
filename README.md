# Caso_Practico_Rstudio
En este repositorio se presenta las consultas realizadas en el software de R  de acuerdo al caso practicto agregado.


## Objetivo
Realizacion de un analisis de una base de datos del titanic de las  personas que sobrevivieron con ayuda del software Rstudio.

## Producto

El analisis realizado arroja datos curiosos de las personas abrodo del Titanic, como a continuación se ira desglosando.


### Crear una tabla nueva por Pclass 

type_class <- filter(titanic, Pclass %in% c("Lower Class", "Middle Class", "Upper Class"))


# Promedio de edades a bordo del Titanic

total_age <- sum(titanic$Age, na.rm = TRUE)
avg_age <- mean(titanic$Age, na.rm = TRUE)

El promedio de edades abordo es de 30 años

view(avg_age)

### Selecciona las los campos  Ticket, Name, Survived, Age
### filtrar las personas que sobrevivieran 
### filtrar las personas que son mayores de 18

titanic %>%
  select(Ticket, Name, Survived, Age) %>%
  filter(Survived == "Yes") %>%
  filter(Age > 18) %>%
  head(15)

### Selecciona Name, Sex, survived, Age, Embarked
### filtrar las personas que no sobrevivieran 
### Filtrar las edades que marquen NULL en la columna de Age

titanic %>%
  select(Name, Sex, Survived, Age, Embarked) %>%
  filter(Survived == "No") %>%
  filter(is.na(Age)) %>%
  head(15)

### Crear una grafica de barras de la cantidad de personas que tuvieron deceso en el Viaje  

titanic %>%
  ggplot(aes(x = Survived)) +
  geom_bar()

Como se muestra en la grafica mas del 50% de las personas que viajaron tuvieron deceso 

### Grafica los puntos de Embarcacion que tubo el barco

titanic %>%
  ggplot(aes(x = Embarked)) +
  geom_bar()

Se muestra que en Southampton fue el mayor donde se abordo el mayor numero de personas.
  
### Grafica donde se ubican las personas que sobrevivieron y el Tipo de clase que sobrevivio

titanic %>%
  ggplot(aes(x = Survived, y = Age, color = Pclass)) + 
  geom_point()

La grafica arroja en la visualiacion que las personas que lograron sobrevivieron son de Upper Class  de un promedio de personas mayores de 20 años

### Grafica donde se ubican las personas que sobrevivieron y donde embarcaron

 titanic %>%
  ggplot(aes(x = Survived, y = Age, color = Embarked)) + 
  geom_point()

  Como se puede observar en la grafica muestra que en la mayoria fallecieron las personas embarcadas en Southampton

