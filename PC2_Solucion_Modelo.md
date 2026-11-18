# PC2 – Diseño de Experimentos de ISW (1ASI0732) · Solución modelo

> Material de práctica. En el examen no se permite IA, y si dos alumnos entregan respuestas idénticas, ambos desaprueban. Úsalo para aprender la estructura y redacta tus propias preguntas y features.

## Cómo cumple cada criterio de la rúbrica

| Criterio | Qué exige para "Excelente" | Dónde se cumple en este documento |
|---|---|---|
| C01. Experiment Cards y Question Backlog (8 pts) | Usar XDPD, redacción clara y coherente, estructura establecida | P1: Raw Material → Supuestos/Question Backlog → Matriz de priorización → 8 Experiment Cards con la plantilla de clase (Question, Why, What, Hypothesis, Métricas, Metas) |
| C02. Null & Alternative Hypotheses (8 pts) | Hipótesis falseable, comprobable, medible, que describa un cambio, con el template; nula = reflejo de la hipótesis | P2: Fase de diseño (pasos 4 a 8), con 8 pares H1/H0, más Measures, Conditions, Scale y Method |
| C03. Pull (1 pt) | Descargar la imagen con comandos y mostrar evidencia | Caso 2, P3 |
| C04. Run (1 pt) | Usar `run` e instalar el programa dentro del contenedor, con evidencia | Caso 2, P4 |
| C05. Configuration (1 pt) | Terminar la configuración inicial y guardar los cambios en una imagen | Caso 2, P5 (`docker commit`) |
| C06. Push (1 pt) | Usar `push` y mostrar la imagen compartida | Caso 2, P6 |

---

# CASO 1 – Passarela (Experiment-Driven Product Development)

## 0. Filtro de restricciones

Antes de redactar, cada feature se revisó contra las restricciones del caso: usuario/login, perfil, mensajes, comunicación entre segmentos, correos, notificaciones, pagos, país/idioma, devoluciones, soporte, y modificación de features existentes (Categorías, Carrito, Bolsos, Tarjetas de regalo, Inicio de sesión, Buscador).

| # | Feature nuevo | ¿Existe en el As-Is? | ¿Choca con alguna restricción? |
|---|---|---|---|
| 1 | Recomendador de talla por marca | No | No. Se mide conversión; no toca devoluciones |
| 2 | "Completa tu look" (calzado + bolso/accesorio) | No | No |
| 3 | Packs Familia (varios pares en un pedido) | No | No. Es una oferta comercial, no un medio de pago |
| 4 | Disponibilidad en tienda física y reserva para recojo | No | No |
| 5 | Probador virtual con realidad aumentada | No | No |
| 6 | Comparador de modelos | No | No |
| 7 | Asistente "Encuentra tu calzado ideal" por ocasión de uso | No | No. Es una sección nueva; no modifica Categorías |
| 8 | Ofertas Flash por tiempo limitado | No | No. No usa notificaciones ni correos |

---

## PREGUNTA 1 – Experiment-Driven Product Development **Planning**

La fase de planificación de XDPD tiene tres pasos: **Raw Material → 1. Uncover Premises → 2. Prepare Questions → 3. Establish Motivation**. El resultado es un **Question Backlog** priorizado.

### 1.1 As-Is Software Platform (resumen)

Passarela es una cadena peruana de calzado multimarca: 14 marcas, más de 80 tiendas y rubros deportivo, casual, elegante y familia. Su e-commerce actual (versión solo para Perú) tiene estas opciones: Categorías de Productos (calzado), Carrito (envío gratis en Lima en 24 h laborales, delivery a todo el Perú), Bolsos, Tarjetas de regalo e Inicio de sesión. La empresa quiere crecer en Perú y expandirse a Sudamérica, pero la plataforma todavía no tiene features que ayuden al cliente a decidir su compra online.

### 1.2 Raw Material → Uncover Premises

| Tipo | Raw material | Premisa descubierta |
|---|---|---|
| Assumption | Las tallas cambian entre las 14 marcas | El cliente online duda de su talla y por eso no compra |
| Assumption | Quien compra calzado también compra bolsos y accesorios | Una sugerencia combinable aumenta el ticket |
| Assumption | El rubro "familia" compra para varios miembros a la vez | Un pack familiar aumenta los pares por pedido |
| Knowledge gap | No sabemos cuántos clientes prefieren ver el producto en tienda antes de comprar | Mostrar el stock por tienda convertiría a esos clientes |
| Idea | Probador virtual desde el celular | Ver el calzado puesto aumenta la intención de compra |
| Claim | "Tenemos toda la variedad de las grandes marcas" | Tanta variedad dificulta decidir entre modelos parecidos |
| Knowledge gap | No sabemos si el cliente elige por marca o por ocasión de uso | Guiar por ocasión ayudaría al cliente indeciso |
| Idea | Ofertas por tiempo limitado | Dan un motivo para volver a la web con frecuencia |

### 1.3 Supuestos y Question Backlog (plantilla de clase)

> **Supuestos:** lo que creemos firmemente y no vamos a someter a prueba; es el punto de partida.
> **Question Backlog:** preguntas de negocio que no podemos responder con certeza y sobre las que plantearemos la hipótesis.
> Ambas columnas se refieren a un negocio en marcha, están relacionadas entre sí y se parecen, pero no son iguales.

| # | Supuesto | Pregunta (Question Backlog) |
|---|---|---|
| Q1 | Las tallas de calzado varían entre las marcas del portafolio de Passarela. | ¿Los clientes dejan de comprar calzado online porque no están seguros de qué talla elegir en cada marca? |
| Q2 | Los clientes que compran calzado también buscan bolsos y accesorios que combinen con él. | ¿Los clientes agregarían un bolso o accesorio a su pedido si se les sugiere uno que combine con el calzado elegido? |
| Q3 | Las familias compran calzado para varios de sus miembros en la misma temporada (escolar, fiestas). | ¿Las familias comprarían varios pares en un solo pedido si se les permite armar un pack familiar con descuento? |
| Q4 | Muchos clientes prefieren ver y probarse el calzado en una tienda física antes de comprarlo. | ¿Los clientes comprarían o reservarían online si supieran qué tienda cercana tiene su modelo y talla disponibles? |
| Q5 | Los clientes quieren saber cómo les queda el calzado puesto antes de decidir. | ¿Los clientes usarían un probador virtual desde su celular para decidir la compra de zapatillas? |
| Q6 | Los clientes dudan entre modelos parecidos de distintas marcas. | ¿Los clientes compran más rápido si pueden comparar lado a lado modelos similares? |
| Q7 | Una parte de los visitantes llega sin saber qué modelo quiere. | ¿Los clientes indecisos comprarían más si se les guía según la ocasión de uso (deporte, trabajo, fiesta, colegio)? |
| Q8 | Los clientes de calzado son sensibles a las ofertas por tiempo limitado. | ¿Una sección de ofertas por tiempo limitado hace que los clientes vuelvan a la web con más frecuencia? |

### 1.4 Question Prioritization Matrix

Escala del 1 al 5. **Confidence** mide qué tan seguros estamos de poder responder la pregunta con un experimento. **Risk** mide el riesgo para el negocio de no responderla. **Impact** mide el impacto esperado en ventas. **Interest** mide el interés del negocio y los stakeholders. **Total Score** es la suma de los cuatro.

| Question | Confidence | Risk | Impact | Interest | Total Score |
|---|---|---|---|---|---|
| Q1 Talla | 4 | 5 | 5 | 5 | **19** |
| Q2 Completa tu look | 4 | 3 | 5 | 5 | **17** |
| Q3 Packs Familia | 4 | 3 | 4 | 5 | **16** |
| Q4 Stock en tienda | 3 | 4 | 4 | 4 | **15** |
| Q5 Probador virtual | 3 | 4 | 4 | 3 | **14** |
| Q6 Comparador | 4 | 2 | 3 | 4 | **13** |
| Q7 Asistente por ocasión | 3 | 2 | 3 | 4 | **12** |
| Q8 Ofertas Flash | 4 | 2 | 3 | 2 | **11** |

### 1.5 Question Backlog priorizado

| Prioridad | Pregunta | Score |
|---|---|---|
| 1 | ¿Los clientes dejan de comprar calzado online porque no están seguros de qué talla elegir en cada marca? | 19 |
| 2 | ¿Los clientes agregarían un bolso o accesorio a su pedido si se les sugiere uno que combine con el calzado elegido? | 17 |
| 3 | ¿Las familias comprarían varios pares en un solo pedido si se les permite armar un pack familiar con descuento? | 16 |
| 4 | ¿Los clientes comprarían o reservarían online si supieran qué tienda cercana tiene su modelo y talla disponibles? | 15 |
| 5 | ¿Los clientes usarían un probador virtual desde su celular para decidir la compra de zapatillas? | 14 |
| 6 | ¿Los clientes compran más rápido si pueden comparar lado a lado modelos similares? | 13 |
| 7 | ¿Los clientes indecisos comprarían más si se les guía según la ocasión de uso? | 12 |
| 8 | ¿Una sección de ofertas por tiempo limitado hace que los clientes vuelvan a la web con más frecuencia? | 11 |

### 1.6 Experiment Cards

> Plantilla de clase. **Question:** ¿sobre qué pregunta de negocio se sustenta la hipótesis? **Why:** ¿por qué ganaría el negocio con esto? **What:** ¿cuál es la forma más simple de validarlo? **Hypothesis:** tiene la solución implícita, tiene métricas (una de negocio y una financiera), no habla de generalidades, no afirma y no somete a prueba la buena voluntad. **Métricas:** qué indicadores se miden. **Metas:** qué valor deben alcanzar.

#### Experiment Card 1 – Recomendador de talla

| Campo | Contenido |
|---|---|
| **Question** | ¿Los clientes dejan de comprar calzado online porque no están seguros de qué talla elegir en cada marca? |
| **Why** | Si resolvemos la duda de la talla, más visitantes de la ficha de calzado se convierten en compradores y crecen las ventas del canal online, que es la apuesta de expansión de Passarela. |
| **What** | Agregar en la ficha de calzado el botón "Encuentra tu talla": el cliente ingresa la medida de su pie en cm, o la talla que usa en otra marca, y el sistema le sugiere la talla correcta para esa marca. Test A/B sobre 42,164 visitantes de fichas de calzado (50 % control, 50 % con recomendador) durante 2 semanas. |
| **Hypothesis** | Si el 30 % de los visitantes de fichas de calzado usa el recomendador de talla, entonces la tasa de conversión de esas fichas pasará de 2.0 % a 2.4 % e incrementaremos las ventas online de calzado en al menos 5 %. |
| **Métricas** | Tasa de conversión = pedidos con calzado / visitas a fichas de calzado. % de uso del recomendador = sesiones que lo usan / sesiones en fichas. Ventas online de calzado (S/). |
| **Metas** | Uso ≥ 30 %; conversión ≥ 2.4 %; **+5 % en ventas** online de calzado. |

#### Experiment Card 2 – Completa tu look

| Campo | Contenido |
|---|---|
| **Question** | ¿Los clientes agregarían un bolso o accesorio a su pedido si se les sugiere uno que combine con el calzado elegido? |
| **Why** | Passarela vende calzado, bolsos y accesorios, pero hoy no los conecta entre sí. Si el cliente agrega un complemento, sube el ticket promedio sin necesidad de traer nuevos visitantes. |
| **What** | Mostrar en la ficha de calzado un bloque "Completa tu look" con 3 bolsos o accesorios que combinan en color y estilo, cada uno con su botón "Agregar". Test A/B sobre 2,110 pedidos que incluyen calzado durante 2 semanas. |
| **Hypothesis** | Si el porcentaje de pedidos con calzado que incluyen un bolso o accesorio pasa de 5 % a 8 %, entonces el ticket promedio subirá de S/ 180 a S/ 198 (+10 %) e incrementaremos las ventas online en al menos 4 %. |
| **Métricas** | Attach rate = pedidos con calzado + complemento / pedidos con calzado. Ticket promedio (S/). CTR del bloque "Completa tu look". Ventas online (S/). |
| **Metas** | Attach rate ≥ 8 %; ticket promedio ≥ S/ 198; **+4 % en ventas**. |

#### Experiment Card 3 – Packs Familia

| Campo | Contenido |
|---|---|
| **Question** | ¿Las familias comprarían varios pares en un solo pedido si se les permite armar un pack familiar con descuento? |
| **Why** | El rubro familia es uno de los cuatro de Passarela. Si la familia compra todos los pares en un solo pedido, crecen los pares por pedido y las ventas de temporada (escolar, fiestas). |
| **What** | Crear la sección "Packs Familia", donde el cliente arma un pack de 3 o más pares (adulto y niños) con 15 % de descuento sobre el pack. Test A/B sobre 3,718 pedidos durante la campaña escolar (3 semanas). |
| **Hypothesis** | Si los pedidos con 3 o más pares pasan de 4 % a 6 % gracias a los Packs Familia, entonces los pares por pedido aumentarán al menos 10 % e incrementaremos las ventas online del rubro familia en al menos 5 %. |
| **Métricas** | % de pedidos con 3 o más pares. Pares promedio por pedido. Ventas online del rubro familia (S/). |
| **Metas** | Pedidos con 3 o más pares ≥ 6 %; +10 % pares por pedido; **+5 % en ventas** del rubro familia. |

#### Experiment Card 4 – Disponibilidad en tienda física y reserva

| Campo | Contenido |
|---|---|
| **Question** | ¿Los clientes comprarían o reservarían online si supieran qué tienda cercana tiene su modelo y talla disponibles? |
| **Why** | Passarela tiene más de 80 tiendas. El cliente que quiere probarse el calzado hoy se va de la web sin saber si su talla está en la tienda. Mostrar el stock por tienda convierte esa visita en una venta, online o en la tienda. |
| **What** | Agregar en la ficha el botón "Ver disponibilidad en tienda", que muestra las tiendas de la ciudad del cliente con stock de esa talla y permite reservar el par por 24 horas para probárselo y comprarlo en la tienda. Test A/B sobre 27,582 visitantes de ciudades con tienda Passarela durante 2 semanas. |
| **Hypothesis** | Si el 15 % de los visitantes de fichas consulta la disponibilidad en tienda, entonces la conversión (compra online + reserva concretada en tienda) pasará de 2.0 % a 2.5 % e incrementaremos las ventas atribuidas a la web en al menos 5 %. |
| **Métricas** | % de uso de "Ver disponibilidad". Conversión = (pedidos online + reservas concretadas) / visitas a fichas. Ventas atribuidas a la web (S/). |
| **Metas** | Uso ≥ 15 %; conversión ≥ 2.5 %; **+5 % en ventas** atribuidas a la web. |

#### Experiment Card 5 – Probador virtual (realidad aumentada)

| Campo | Contenido |
|---|---|
| **Question** | ¿Los clientes usarían un probador virtual desde su celular para decidir la compra de zapatillas? |
| **Why** | Ver el calzado puesto reduce la incertidumbre de la compra online. Sería una ventaja competitiva en el canal móvil frente a otras tiendas multimarca. |
| **What** | Agregar en las fichas de zapatillas, solo en móvil, el botón "Pruébatelo": la cámara del celular superpone el modelo en el pie del cliente. Test A/B sobre 8,766 usuarios móviles en fichas de zapatillas durante 2 semanas. |
| **Hypothesis** | Si el 25 % de los usuarios móviles de fichas de zapatillas usa el probador virtual, entonces la tasa de "agregar al carrito" pasará de 6.0 % a 7.5 % e incrementaremos las ventas móviles de zapatillas en al menos 5 %. |
| **Métricas** | % de uso del probador. Add-to-cart rate = sesiones que agregan al carrito / sesiones en ficha. Ventas móviles de zapatillas (S/). |
| **Metas** | Uso ≥ 25 %; add-to-cart ≥ 7.5 %; **+5 % en ventas** móviles de zapatillas. |

#### Experiment Card 6 – Comparador de modelos

| Campo | Contenido |
|---|---|
| **Question** | ¿Los clientes compran más rápido si pueden comparar lado a lado modelos similares? |
| **Why** | Con 14 marcas hay muchos modelos parecidos. Si el cliente compara precio, material y tallas en una sola vista, decide antes y abandona menos la compra. |
| **What** | Agregar la opción "Comparar" en las fichas (hasta 3 modelos) con una tabla lado a lado. Test A/B sobre 33,540 visitantes que ven 3 o más fichas en una sesión, durante 2 semanas. |
| **Hypothesis** | Si el 15 % de los visitantes que revisan 3 o más fichas usa el comparador, entonces su conversión pasará de 2.5 % a 3.0 %, el tiempo hasta la compra se reducirá 20 % y las ventas online subirán al menos 3 %. |
| **Métricas** | % de uso del comparador. Conversión de visitantes con 3 o más fichas vistas. Tiempo promedio hasta la compra (min). Ventas online (S/). |
| **Metas** | Uso ≥ 15 %; conversión ≥ 3.0 %; −20 % en tiempo hasta la compra; **+3 % en ventas**. |

#### Experiment Card 7 – Asistente "Encuentra tu calzado ideal"

| Campo | Contenido |
|---|---|
| **Question** | ¿Los clientes indecisos comprarían más si se les guía según la ocasión de uso (deporte, trabajo, fiesta, colegio)? |
| **Why** | El visitante que no sabe qué modelo quiere navega sin rumbo y se va. Un asistente que lo guía hacia pocos modelos adecuados convierte esa visita en una venta. |
| **What** | Crear el asistente "Encuentra tu calzado ideal": 3 preguntas (ocasión, estilo, rango de precio) y, al final, 6 modelos recomendados. Test A/B sobre 27,792 visitantes que entran al home sin buscar un producto específico, durante 2 semanas. |
| **Hypothesis** | Si el 20 % de los visitantes indecisos completa el asistente, entonces su conversión pasará de 3.0 % a 3.6 % e incrementaremos las ventas online en al menos 3 %. |
| **Métricas** | % de visitantes que completan el asistente. Conversión de visitantes indecisos. Ventas online (S/). |
| **Metas** | Completan ≥ 20 %; conversión ≥ 3.6 %; **+3 % en ventas**. |

#### Experiment Card 8 – Ofertas Flash

| Campo | Contenido |
|---|---|
| **Question** | ¿Una sección de ofertas por tiempo limitado hace que los clientes vuelvan a la web con más frecuencia? |
| **Why** | Hoy no hay un motivo para volver a la web. Si el cliente vuelve más seguido, tiene más oportunidades de comprar y crecen las ventas recurrentes. |
| **What** | Crear la sección "Ofertas Flash": 5 modelos con descuento que cambian cada 24 horas, con un contador visible. Test A/B sobre 4,794 visitantes nuevos durante 3 semanas, con seguimiento de su regreso a los 7 días. |
| **Hypothesis** | Si el 20 % de los visitantes entra a Ofertas Flash, entonces la tasa de retorno a 7 días pasará de 15 % a 18 % e incrementaremos las ventas online en al menos 3 %. |
| **Métricas** | % de visitantes que entran a Ofertas Flash. Tasa de retorno a 7 días. Conversión en la sección. Ventas online (S/). |
| **Metas** | Entrada ≥ 20 %; retorno a 7 días ≥ 18 %; **+3 % en ventas**. |

---

## PREGUNTA 2 – Experiment-Driven Product Development **Design**

La fase de diseño de XDPD tiene estos pasos: **Belief-led Questions → 4. Formulate Hypothesis → 5. Decide Measures → 6. Determine Conditions → 7. Calculate Scale → 8. Decide Method**.
Las 8 preguntas del backlog son *belief-led*: tenemos una creencia previa que queremos contrastar con la evidencia.

### 2.1 Formulate Hypothesis – Null & Alternative Hypotheses Statements

**Template usado (hypothesis statement de clase + feature hypothesis):**
> **H1:** *Creemos que* [construir este feature] *para* [estos usuarios] *logrará* [este cambio medible]. *La evidencia se reflejará en* [medidas], *bajo las circunstancias de* [condiciones].
> **H0 (reflejo):** [Este feature] *no producirá* un cambio significativo en [la misma medida]; cualquier diferencia observada se deberá al azar.

Las hipótesis son **falseables** (H0 puede resultar cierta), **comprobables** (A/B test en 2–3 semanas), **medibles** (métrica y valor objetivo explícitos) y **describen un cambio** (de X a Y).

#### H-1 · Recomendador de talla
- **Question:** ¿Los clientes dejan de comprar calzado online porque no están seguros de qué talla elegir en cada marca?
- **Belief:** La duda sobre la talla es la principal barrera de la compra online de calzado, porque las tallas varían entre marcas.
- **Hypothesis (H1):** Creemos que agregar un recomendador de talla en la ficha de calzado, para los clientes que compran calzado online, logrará que la tasa de conversión de esas fichas pase de 2.0 % a 2.4 % y que las ventas online de calzado suban al menos 5 %. La evidencia se reflejará en la tasa de conversión, el % de uso del recomendador y las ventas, bajo las circunstancias de un A/B test 50/50 con 21,082 visitantes por grupo durante 2 semanas.
- **Null hypothesis (H0):** Agregar el recomendador de talla no producirá un cambio significativo en la conversión de las fichas de calzado (se mantiene en 2.0 %) ni en las ventas; cualquier diferencia entre grupos se deberá al azar.
- **Notación:** H0: p_B = p_A  |  H1: p_B > p_A (meta p_B = 2.4 %).

#### H-2 · Completa tu look
- **Question:** ¿Los clientes agregarían un bolso o accesorio a su pedido si se les sugiere uno que combine con el calzado elegido?
- **Belief:** Los clientes de calzado también quieren complementos, pero no los buscan por su cuenta.
- **Hypothesis (H1):** Creemos que mostrar el bloque "Completa tu look" a los clientes que agregan calzado logrará que los pedidos con complemento pasen de 5 % a 8 % y que el ticket promedio suba de S/ 180 a S/ 198 (+10 %). La evidencia se reflejará en el attach rate y el ticket promedio, bajo las circunstancias de un A/B test con 1,055 pedidos por grupo durante 2 semanas.
- **Null hypothesis (H0):** Mostrar "Completa tu look" no producirá un cambio significativo en el attach rate (se mantiene en 5 %) ni en el ticket promedio; cualquier diferencia se deberá al azar.
- **Notación:** H0: p_B = p_A  |  H1: p_B > p_A (meta 8 %).

#### H-3 · Packs Familia
- **Question:** ¿Las familias comprarían varios pares en un solo pedido si se les permite armar un pack familiar con descuento?
- **Belief:** Las familias compran calzado para varios miembros en la misma temporada, pero hoy lo hacen en pedidos separados o en otra tienda.
- **Hypothesis (H1):** Creemos que ofrecer Packs Familia de 3 o más pares a los clientes del rubro familia logrará que los pedidos con 3 o más pares pasen de 4 % a 6 % y que las ventas del rubro familia suban al menos 5 %. La evidencia se reflejará en el % de pedidos con 3 o más pares y en los pares por pedido, bajo las circunstancias de un A/B test con 1,859 pedidos por grupo durante la campaña escolar (3 semanas).
- **Null hypothesis (H0):** Ofrecer Packs Familia no producirá un cambio significativo en el % de pedidos con 3 o más pares (se mantiene en 4 %) ni en las ventas del rubro familia; cualquier diferencia se deberá al azar.
- **Notación:** H0: p_B = p_A  |  H1: p_B > p_A (meta 6 %).

#### H-4 · Disponibilidad en tienda y reserva
- **Question:** ¿Los clientes comprarían o reservarían online si supieran qué tienda cercana tiene su modelo y talla disponibles?
- **Belief:** Una parte importante de los visitantes prefiere probarse el calzado y abandona la web porque no sabe si su talla está en una tienda cercana.
- **Hypothesis (H1):** Creemos que mostrar la disponibilidad por tienda y permitir la reserva, para los visitantes de ciudades con tienda Passarela, logrará que la conversión (compra online + reserva concretada) pase de 2.0 % a 2.5 % y que las ventas atribuidas a la web suban al menos 5 %. La evidencia se reflejará en el uso de "Ver disponibilidad", la conversión y las reservas concretadas, bajo las circunstancias de un A/B test con 13,791 visitantes por grupo durante 2 semanas.
- **Null hypothesis (H0):** Mostrar la disponibilidad en tienda no producirá un cambio significativo en la conversión (se mantiene en 2.0 %); cualquier diferencia se deberá al azar.
- **Notación:** H0: p_B = p_A  |  H1: p_B > p_A (meta 2.5 %).

#### H-5 · Probador virtual
- **Question:** ¿Los clientes usarían un probador virtual desde su celular para decidir la compra de zapatillas?
- **Belief:** Ver cómo le quedan las zapatillas puestas aumenta la intención de compra del cliente móvil.
- **Hypothesis (H1):** Creemos que ofrecer un probador virtual con realidad aumentada a los usuarios móviles en fichas de zapatillas logrará que la tasa de "agregar al carrito" pase de 6.0 % a 7.5 % y que las ventas móviles de zapatillas suban al menos 5 %. La evidencia se reflejará en el add-to-cart rate y el uso del probador, bajo las circunstancias de un A/B test con 4,383 usuarios móviles por grupo durante 2 semanas.
- **Null hypothesis (H0):** Ofrecer el probador virtual no producirá un cambio significativo en el add-to-cart rate (se mantiene en 6.0 %); cualquier diferencia se deberá al azar.
- **Notación:** H0: p_B = p_A  |  H1: p_B > p_A (meta 7.5 %).

#### H-6 · Comparador
- **Question:** ¿Los clientes compran más rápido si pueden comparar lado a lado modelos similares?
- **Belief:** Los clientes que revisan varias fichas están indecisos entre modelos parecidos y abandonan por la dificultad de compararlos.
- **Hypothesis (H1):** Creemos que ofrecer un comparador de hasta 3 modelos a los visitantes que revisan 3 o más fichas logrará que su conversión pase de 2.5 % a 3.0 % y que su tiempo hasta la compra se reduzca 20 %. La evidencia se reflejará en la conversión y el tiempo hasta la compra, bajo las circunstancias de un A/B test con 16,770 visitantes por grupo durante 2 semanas.
- **Null hypothesis (H0):** Ofrecer el comparador no producirá un cambio significativo en la conversión (se mantiene en 2.5 %) ni en el tiempo hasta la compra; cualquier diferencia se deberá al azar.
- **Notación:** H0: p_B = p_A  |  H1: p_B > p_A (meta 3.0 %).

#### H-7 · Asistente por ocasión de uso
- **Question:** ¿Los clientes indecisos comprarían más si se les guía según la ocasión de uso?
- **Belief:** Muchos clientes eligen calzado según para qué lo usarán, no por marca, y no encuentran esa forma de búsqueda en la web.
- **Hypothesis (H1):** Creemos que ofrecer el asistente "Encuentra tu calzado ideal" a los visitantes que llegan sin buscar un producto específico logrará que su conversión pase de 3.0 % a 3.6 % y que las ventas online suban al menos 3 %. La evidencia se reflejará en el % que completa el asistente y en la conversión, bajo las circunstancias de un A/B test con 13,896 visitantes por grupo durante 2 semanas.
- **Null hypothesis (H0):** Ofrecer el asistente no producirá un cambio significativo en la conversión de los visitantes indecisos (se mantiene en 3.0 %); cualquier diferencia se deberá al azar.
- **Notación:** H0: p_B = p_A  |  H1: p_B > p_A (meta 3.6 %).

#### H-8 · Ofertas Flash
- **Question:** ¿Una sección de ofertas por tiempo limitado hace que los clientes vuelvan a la web con más frecuencia?
- **Belief:** Una oferta que cambia cada día crea un hábito de visita y más oportunidades de compra.
- **Hypothesis (H1):** Creemos que crear la sección Ofertas Flash para los visitantes nuevos logrará que su tasa de retorno a 7 días pase de 15 % a 18 % y que las ventas online suban al menos 3 %. La evidencia se reflejará en la tasa de retorno a 7 días y en la conversión de la sección, bajo las circunstancias de un A/B test con 2,397 visitantes nuevos por grupo durante 3 semanas.
- **Null hypothesis (H0):** Crear Ofertas Flash no producirá un cambio significativo en la tasa de retorno a 7 días (se mantiene en 15 %); cualquier diferencia se deberá al azar.
- **Notación:** H0: p_B = p_A  |  H1: p_B > p_A (meta 18 %).

### 2.2 Decide Measures

Las medidas deben ser representativas, calculables y proporcionales.

| Exp. | Medida principal (decide H0/H1) | Medidas secundarias |
|---|---|---|
| H-1 | Tasa de conversión de fichas de calzado | % de uso del recomendador, ventas de calzado (S/) |
| H-2 | Attach rate (pedidos con complemento) | Ticket promedio, CTR del bloque, ventas (S/) |
| H-3 | % de pedidos con 3 o más pares | Pares por pedido, ventas del rubro familia (S/) |
| H-4 | Conversión (online + reserva concretada) | % de uso de "Ver disponibilidad", ventas atribuidas a la web |
| H-5 | Add-to-cart rate en móvil | % de uso del probador, ventas móviles de zapatillas |
| H-6 | Conversión de visitantes con 3 o más fichas vistas | Tiempo hasta la compra, % de uso del comparador |
| H-7 | Conversión de visitantes indecisos | % que completa el asistente, ventas (S/) |
| H-8 | Tasa de retorno a 7 días | Conversión en Ofertas Flash, ventas (S/) |

### 2.3 Determine Conditions

La **control condition** (A) actúa como si H0 fuera cierta: se usa la plataforma As-Is. La **experimental condition** (B) busca evidencia para rechazar H0: se usa la plataforma con el feature nuevo. La asignación es aleatoria 50/50 por usuario y cada usuario ve siempre la misma versión.

| Exp. | Participantes | Control (A) | Experimental (B) |
|---|---|---|---|
| H-1 | Visitantes de fichas de calzado | Ficha sin recomendador | Ficha + "Encuentra tu talla" |
| H-2 | Clientes que agregan calzado | Ficha sin sugerencias | Ficha + "Completa tu look" |
| H-3 | Visitantes del rubro familia | Web sin Packs Familia | Web + sección Packs Familia |
| H-4 | Visitantes de ciudades con tienda | Ficha sin disponibilidad | Ficha + "Ver disponibilidad en tienda" |
| H-5 | Usuarios móviles en fichas de zapatillas | Ficha sin probador | Ficha + "Pruébatelo" (AR) |
| H-6 | Visitantes con 3 o más fichas vistas | Sin comparador | Con comparador |
| H-7 | Visitantes que entran sin buscar un producto | Home sin asistente | Home + asistente por ocasión |
| H-8 | Visitantes nuevos | Web sin Ofertas Flash | Web + sección Ofertas Flash |

### 2.4 Calculate Scale

Tamaño de muestra por grupo para comparar dos proporciones, con nivel de confianza del 95 % (α = 0.05, Z = 1.96) y potencia del 80 % (β = 0.20, Z = 0.84):

```
n = (Z_α/2 + Z_β)² · [p1(1 − p1) + p2(1 − p2)] / (p2 − p1)²
(Z_α/2 + Z_β)² = (1.96 + 0.84)² = 7.84
```

| Exp. | p1 (control) | p2 (meta) | p1q1 + p2q2 | (p2 − p1)² | n por grupo | Total |
|---|---|---|---|---|---|---|
| H-1 | 2.0 % | 2.4 % | 0.043024 | 0.000016 | **21,082** | 42,164 visitantes |
| H-2 | 5.0 % | 8.0 % | 0.121100 | 0.000900 | **1,055** | 2,110 pedidos |
| H-3 | 4.0 % | 6.0 % | 0.094800 | 0.000400 | **1,859** | 3,718 pedidos |
| H-4 | 2.0 % | 2.5 % | 0.043975 | 0.000025 | **13,791** | 27,582 visitantes |
| H-5 | 6.0 % | 7.5 % | 0.125775 | 0.000225 | **4,383** | 8,766 usuarios |
| H-6 | 2.5 % | 3.0 % | 0.053475 | 0.000025 | **16,770** | 33,540 visitantes |
| H-7 | 3.0 % | 3.6 % | 0.063804 | 0.000036 | **13,896** | 27,792 visitantes |
| H-8 | 15 % | 18 % | 0.275100 | 0.000900 | **2,397** | 4,794 visitantes |

Ejemplo del cálculo de H-1: n = 7.84 × 0.043024 / 0.000016 = 21,081.8, que se redondea hacia arriba a **21,082 por grupo**.
Duración: mínimo 2 semanas, para cubrir un ciclo semanal completo (días laborables y fin de semana), o hasta alcanzar n. Para H-3 y H-8 son 3 semanas.

### 2.5 Decide Method

| Exp. | Método | Prueba estadística | Regla de decisión |
|---|---|---|---|
| H-1 a H-8 | A/B test (experimento controlado aleatorizado) | Prueba Z de diferencia de proporciones (H-2 también usa la prueba t para el ticket promedio, y H-6 para el tiempo hasta la compra) | Si p-value < 0.05 **y** la medida alcanza la meta, se rechaza H0, se acepta H1 y el feature se lanza a todos. En otro caso no se rechaza H0: el feature no se lanza y se registra lo aprendido para el siguiente experimento. |

---

# CASO 2 – Tecnología de contenerización (con tu proyecto **Clair**)

**Escenario:** el frontend de tu proyecto (`clair-ui`, Angular 21) se despliega en un contenedor **Ubuntu 22.04 + Nginx**. Se descarga la imagen base (pull), se crea el contenedor y se instala Nginx dentro (run), se configura Nginx para servir la app Angular y se guarda en una imagen (commit), y se comparte en Docker Hub (push).

> Todos los comandos son para **PowerShell en Windows**. `krxxg` es tu usuario de Docker Hub. Nunca pongas un texto de ejemplo como "tuusuario".
> Se usa el puerto **8081** del host para no chocar con el backend de Clair, que usa el 8080.

## 0. Preparación (hazla el día anterior, no cuenta en el examen)

**a) Limpiar la práctica anterior** (si da error porque no existe, ignóralo):
```powershell
docker rm -f passarela-app clair-ui-app clair-ui-verif
docker rmi tuusuario/passarela-app:1.0
```

**b) Compilar el frontend Angular** (genera la carpeta que luego se copia al contenedor):
```powershell
cd "C:\Users\ASUS\Desktop\UPC\UPC-Ciclo Vlll\Diseño de Experimentos\clair-ui"
npm install --no-package-lock
npm run build
dir dist\angular-project\browser      # debe existir index.html aquí
```
> ✅ Verificado el 17/11: `npm install` tarda ~1 min, `npm run build` ~12 s y genera `dist\angular-project\browser\index.html` (1.5 MB en total).
> ⚠️ PowerShell 5.1 muestra en **rojo** (`NativeCommandError`) los avisos `npm warn deprecated @angular/animations` y `bundle initial exceeded maximum budget`. **Son advertencias, no errores.** El build terminó bien si ves `Application bundle generation complete` y `Output location: ...`.
>
> Si `npm run build` falla y no hay tiempo de arreglarlo, crea un `index.html` simple con el nombre "Clair" y úsalo en lugar de la carpeta `browser`. Igual cumples la rúbrica, aunque es mejor usar el build real.

## Pregunta 3 – Descarga de la aplicación (PULL) · C03

```powershell
docker --version
docker login            # login web: tu cuenta entra con GitHub, así que NO tiene contraseña de Docker
docker pull ubuntu:22.04
docker images ubuntu
```

**Qué explicar:** `docker pull` descarga desde Docker Hub la imagen base Ubuntu 22.04 sobre la que se instalará el servidor web del proyecto Clair. `docker images` confirma que ya está en local.

**📸 Evidencias P3:**
1. `docker --version` y `Login Succeeded`.
2. Salida de `docker pull ubuntu:22.04` con `Status: Downloaded newer image` (o `Image is up to date`).
3. Salida de `docker images ubuntu` mostrando `ubuntu:22.04`.

## Pregunta 4 – Instalación de la aplicación (RUN) · C04

**Terminal 1:**
```powershell
docker run -dit --name clair-ui-app -p 8081:80 ubuntu:22.04
docker ps
docker exec -it clair-ui-app bash
```
**Dentro del contenedor** (el prompt cambia a `root@<id>:/#`):
```bash
apt-get update
DEBIAN_FRONTEND=noninteractive apt-get install -y nginx curl
nginx -v
```

**Qué explicar:**
- `-d` lo ejecuta en segundo plano, `-i -t` dejan una terminal interactiva disponible, `--name` le da nombre al contenedor y `-p 8081:80` publica el puerto 80 del contenedor en el 8081 de Windows.
- `docker exec -it ... bash` abre una consola dentro del contenedor.
- `apt-get install` instala Nginx **dentro del contenedor**, no en Windows.

**📸 Evidencias P4:**
1. Salida de `docker run` (el ID largo) y de `docker ps` con `clair-ui-app` en estado **Up** y `0.0.0.0:8081->80/tcp`.
2. Final de `apt-get install -y nginx` (líneas `Setting up nginx ...`).
3. `nginx -v` → `nginx version: nginx/1.18.0 (Ubuntu)`, con el prompt `root@...` visible para que se note que estás dentro del contenedor.

## Pregunta 5 – Configuración de la aplicación + guardar en imagen · C05

**Terminal 2** (Windows, en la carpeta de `clair-ui`): copiar el build de Clair al contenedor.
```powershell
cd "C:\Users\ASUS\Desktop\UPC\UPC-Ciclo Vlll\Diseño de Experimentos\clair-ui"
docker cp "dist/angular-project/browser/." clair-ui-app:/var/www/html/
```

**Terminal 1** (dentro del contenedor): configurar Nginx para la aplicación Angular.
```bash
rm -f /var/www/html/index.nginx-debian.html
ls /var/www/html

cat > /etc/nginx/sites-available/default <<'EOF'
server {
    listen 80;
    server_name localhost;
    root /var/www/html;
    index index.html;
    location / {
        try_files $uri $uri/ /index.html;
    }
}
EOF

nginx -t
service nginx start
curl -I http://localhost
exit
```
Abre **http://localhost:8081** en el navegador. Debe cargar la interfaz de Clair. Las llamadas a `/api` fallarán porque el backend no está levantado, y eso es normal en este ejercicio.

**Guardar la configuración en una imagen** (Terminal 1, ya en Windows):
```powershell
docker commit --change "CMD nginx -g 'daemon off;'" --change "EXPOSE 80" clair-ui-app krxxg/clair-ui:1.0
docker images krxxg/clair-ui
```

**Comprobar que la imagen guardó la configuración** (contenedor nuevo, creado desde tu imagen):
```powershell
docker run -d --name clair-ui-verif -p 8082:80 krxxg/clair-ui:1.0
docker ps
```
Abre **http://localhost:8082**: debe verse Clair sin haber configurado nada en este contenedor nuevo.

**Qué explicar:**
- `docker cp` copia los archivos compilados del proyecto al contenedor.
- `try_files ... /index.html` es la configuración que necesita una SPA de Angular para que las rutas internas no den 404.
- `nginx -t` valida la configuración.
- `docker commit` guarda el estado del contenedor (Nginx instalado, configuración y archivos de Clair) como la imagen `krxxg/clair-ui:1.0`.
- `--change "CMD ..."` hace que Nginx arranque solo cada vez que se cree un contenedor con esa imagen.

**📸 Evidencias P5:**
1. `docker cp` sin errores y `ls /var/www/html` mostrando `index.html` y los archivos `.js/.css` de Clair.
2. `nginx -t` → `syntax is ok` / `test is successful`, y `service nginx start` → `[ OK ]`.
3. **Navegador en http://localhost:8081 mostrando la app Clair** (la evidencia más importante de "cómo funciona").
4. Salida de `docker commit` (sha256) y `docker images krxxg/clair-ui` mostrando la etiqueta `1.0`. Sin esta captura solo obtienes 0.5 en este criterio.
5. (Extra) Navegador en http://localhost:8082 con el contenedor creado desde la imagen.

## Pregunta 6 – Compartir la aplicación (PUSH) · C06

```powershell
docker push krxxg/clair-ui:1.0
```
Comprobación de que cualquiera puede descargarla:
```powershell
docker rm -f clair-ui-verif
docker rmi krxxg/clair-ui:1.0
docker pull krxxg/clair-ui:1.0
```

**Qué explicar:** `docker push` sube la imagen a Docker Hub, en el repositorio `krxxg/clair-ui`. Desde ahí cualquier persona o servidor puede hacer `docker pull krxxg/clair-ui:1.0` y ejecutar la app con la misma configuración.

**📸 Evidencias P6:**
1. Salida de `docker push` terminando en `1.0: digest: sha256:... size: ...`.
2. **Navegador en hub.docker.com/repositories/krxxg** mostrando el repo `clair-ui` (Last pushed: *a few seconds ago*).
3. Pestaña **Tags** del repo mostrando la etiqueta `1.0`.
4. (Extra) `docker pull krxxg/clair-ui:1.0` descargándola de vuelta.

## Checklist final de capturas (pégalas en el Word en este orden)

| # | Pregunta | Captura |
|---|---|---|
| 1 | P3 | `docker --version` + `docker login` → Login Succeeded |
| 2 | P3 | `docker pull ubuntu:22.04` |
| 3 | P3 | `docker images ubuntu` |
| 4 | P4 | `docker run -dit ...` + `docker ps` (Up, 8081->80) |
| 5 | P4 | `apt-get install -y nginx` terminado |
| 6 | P4 | `nginx -v` dentro del contenedor (`root@...`) |
| 7 | P5 | `docker cp` + `ls /var/www/html` |
| 8 | P5 | `nginx -t` + `service nginx start [ OK ]` |
| 9 | P5 | Navegador http://localhost:8081 con Clair |
| 10 | P5 | `docker commit` + `docker images krxxg/clair-ui` |
| 11 | P5 | (extra) http://localhost:8082 desde la imagen nueva |
| 12 | P6 | `docker push krxxg/clair-ui:1.0` con digest |
| 13 | P6 | Docker Hub: repo `krxxg/clair-ui` |
| 14 | P6 | Docker Hub: Tags → `1.0` |

## Errores frecuentes (los que ya te pasaron y otros)

| Error | Causa | Solución |
|---|---|---|
| `push access denied ... insufficient_scope` | La imagen no lleva tu usuario (`tuusuario/...`) | `docker tag <imagen> krxxg/<nombre>:1.0` y vuelve a hacer push |
| `GetFileAttributesEx ... cannot find the file` en `docker cp` | Ejecutaste el comando fuera de la carpeta del proyecto o no hiciste el build | `cd` a `clair-ui` y `npm run build` primero |
| Los archivos copiados no aparecen en la imagen | Hiciste `docker cp` **después** del `commit` | El orden es cp → configurar → commit |
| La página no carga tras reiniciar el contenedor | Nginx no arranca solo | Usa el `--change "CMD nginx -g 'daemon off;'"` en el commit |
| `unauthorized: incorrect username or password` en `docker login -u krxxg` | Tu cuenta de Docker entra con GitHub y no tiene contraseña propia | Usa `docker login` sin `-u` (abre el navegador), o crea un Personal Access Token en app.docker.com/settings y pégalo como contraseña |
| `port is already allocated` | Otro contenedor usa ese puerto | Usa otro puerto: `-p 8083:80` |
| `Conflict. The container name "/clair-ui-app" is already in use` | Ya existe un contenedor con ese nombre | `docker rm -f clair-ui-app` |
