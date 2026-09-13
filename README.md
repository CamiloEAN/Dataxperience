# Predicción de Temperatura de un Motor DC a partir de su Corriente

Proyecto Final de Dataxperience, aplicado a Ingeniería Mecatrónica. 
¿Se puede saber qué tan caliente está un motor solo midiendo cuánta corriente
consume?** Si esto se puede, entonces ¿es posible armar un sistema que prenda un ventilador *antes* de que el motor
se sobrecaliente, usando solo un sensor de corriente?

## Los datos

No se tiene un motor real conectado a sensores, así que **se inventaron los datos** con una
regla simple: más corriente = más calor, con algo de variación al azar. También se agrego a
propósito 10 casos de "motor recién prendido" (columna `evento` = `arranque`), para poder
estudiarlos aparte de los datos normales. Todo el proceso está documentado en
`scripts/generar_datos.py`.

## Resumen del proyecto

**Etapa 1 — Preparar los datos:** dataset simulado, documentado con transparencia; sin
datos faltantes ni repetidos (verificado); 190 registros de funcionamiento normal y 10 de
arranque, separados desde el inicio.

**Etapa 2 — Explorar los datos:** la corriente y la temperatura están muy relacionadas
(0.95 en general, 0.99 si se quitan los casos de arranque). El gráfico de dispersión
(Corriente vs. Temperatura) deja ver claramente los casos de arranque; el diagrama de caja
de solo la corriente no los detecta osea hay que mirar las dos variables juntas.

**Etapa 3 — El modelo:**

| Fórmula encontrada | `Temperatura ≈ 2.66 × Corriente + 15.38` |
| Qué tan bien explica los datos (R²) | 0.97 |
| Margen de error típico | ≈ 2.5 °C |

Por cada Amperio extra que consume el motor, la temperatura sube casi 2.7°C. El modelo se
entrenó solo con los datos de funcionamiento normal, dejando aparte los de arranque.

**Para qué sirve:** un sensor de corriente + un microcontrolador pueden calcular la
temperatura esperada del motor y prender un ventilador de forma preventiva, sin necesitar un
sensor de temperatura físico sobre una pieza en movimiento. Detalle completo en el Proyecto.

## Autor

Proyecto Final — Dataxperience · Ingeniería Mecatrónica · JUAN CAMILO VARGAS ESCOBAR
