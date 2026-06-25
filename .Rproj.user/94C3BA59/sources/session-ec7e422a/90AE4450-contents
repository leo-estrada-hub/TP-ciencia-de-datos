library(tidyverse)

base <- readRDS("02_input/tabla_rca.rds")

#EMPIEZA LIMPIEZA

base <- base %>%
  rename(empleo = empleo_registrado,
         sector = sector_agregado)


#Cuantos valores tengo valor = 0?

sum(base$vab == 0, na.rm = TRUE) #1791 valores con vab igual a 0
mean(base$vab == 0, na.rm = TRUE)#lo que representa un 10% aprox de la columna vab
sum(base$empleo == 0, na.rm = TRUE) #3503 valores con empleo igual a 0
mean(base$empleo == 0, na.rm = TRUE)#lo que representa un 20% de la columna empleo

#Como me queda la base cuando saco estos valores?

base_limpia <- base %>%
  filter(
    !is.na(vab),
    !is.na(empleo),
    vab > 0,
    empleo > 0
  )   
nrow(base_limpia)

#sacando los sectores con valor 0 en empleo y vab queda base de 17092
# 13887/17640= aprox 79% lo que implica depuracion del 21% de la base
# dado que el objetivo es realizar una regresión y ver ventajas comparativas
# valores iguales a 0 no son relevantes, ademas de que la muestra sigue siendo grande

#Y si extraemos los servicios?

sectores_no_transables <- c(
  "Construcción",
  "Infraestructura",
  "Enseñanza",
  "Servicios sociales y de salud",
  "Transporte",
  "Comercio mayorista, minorista y reparaciones",
  "Comunicaciones",
  "Servicios financieros",
  "Edición e impresión; reproducción de grabaciones",
  "Servicios de hoteleria y restaurantes"
  )

base_limpia <- base_limpia %>%
  filter(!sector %in% sectores_no_transables)
nrow(base_limpia)

# 8847/13887= aprox 64%, es decir se depura un 36% de la base
# 8847/17640 = aprox 50%, es decir se depura en TOTAL un 50% de la base
# Sin embargo en esta depuracion se eliminan los servicios que ensucian el 
#analisis al desconcentrar el HHI y aumentar empleo de manera 
#artificial, y por ende en la regresion dar siempre un resultado positivo
#apesar de la gran depuracion, queda una base grande, lo que genera una
#estadistica mas certera


unique(base_limpia$sector) #para ver cuantos sectores nos quedaron (de 35 a 25)
saveRDS(base_limpia, "02_input/base_filtrada.rds")
