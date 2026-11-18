# GUÍA PARA EL EXAMEN PC2 – Diseño de Experimentos de ISW (1ASI0732)

> **Cómo usar esta guía:** las 6 preguntas son siempre las mismas. **Solo cambia el caso de la Parte 1** (empresa, pantallas y restricciones). La **Parte 2 (Docker)** es idéntica: sigue los comandos al pie de la letra.
> El ejemplo completo resuelto con el caso Passarela está en [PC2_Solucion_Modelo.md](PC2_Solucion_Modelo.md).
> En el examen no se permite IA. Redacta con tus palabras; si dos entregas son idénticas, ambas desaprueban.

---

## 0. Antes del examen (jueves por la noche)

- [ ] Docker Desktop abierto y diciendo **Engine running**.
- [ ] El repo `clair-ui` ya **no** aparece en hub.docker.com/repositories/krxxg (lo borraste el 17/11).
- [ ] Probar la contraseña: `docker login -u krxxg` → `Login Succeeded`, y luego `docker logout`. Si falla, crea un Personal Access Token en app.docker.com/settings (Read & Write) y guárdalo en un lugar seguro.
- [ ] Verificar que existe el build de Clair:
  ```powershell
  dir "C:\Users\ASUS\Desktop\UPC\UPC-Ciclo Vlll\Diseño de Experimentos\clair-ui\dist\angular-project\browser\index.html"
  ```
  Si no existe: `cd` a `clair-ui`, luego `npm install --no-package-lock` y `npm run build`. Los avisos en rojo de *deprecated* y *budget* son solo advertencias.
- [ ] Tener a mano la plantilla Excel `Docs/1. Semana 20 - Plantilla Experiment Card - Copia.xlsx` y este archivo.
- [ ] Saber tomar capturas rápido: **Win + Shift + S** y pegar en el Word con **Ctrl + V**.

## 1. Plan de tiempo (110 min)

| Min | Qué hacer | Por qué |
|---|---|---|
| 0–5 | Renombrar el Word (`código_apellidos_nombre_1asi0732_pc2_Sección.docx`), leer el caso y **marcar las restricciones** | Sin esto todo lo demás puede salir mal |
| 5–25 | **Parte 2 (Docker) completa, P3 a P6.** Mientras corre `apt-get` o `npm`, lee el caso 1 | 4 puntos casi asegurados; además, si Docker falla, todavía tienes tiempo de arreglarlo |
| 25–60 | **Pregunta 1**: raw material, supuestos y backlog, matriz, 8 Experiment Cards | 8 puntos |
| 60–100 | **Pregunta 2**: 8 pares H1/H0, measures, conditions, scale, method | 8 puntos |
| 100–110 | Revisar restricciones, números coherentes, capturas en el Word. Guardar y enviar | |

---

# PARTE 1 – CASO 1 (Experiment-Driven Product Development)

## Paso A · Leer el caso y armar el filtro (5 min)

1. Lista las **pantallas y features que YA existen** (As-Is). **No puedes modificarlos.** Todo lo que propongas debe ser un feature nuevo.
2. Copia la lista de **restricciones** y tenla a la vista. En el ejemplo eran: login/usuario, perfil, mensajes, comunicación entre segmentos, correos, notificaciones, pagos, país/idioma, devoluciones, soporte y modificar features existentes.
3. **Trampas típicas**: features que *parecen* válidos pero chocan con una restricción.

| Feature tentador | Por qué puede chocar |
|---|---|
| Alerta de stock / avisos de precio | Notificaciones o correos |
| Chatbot, chat con asesor | Soporte o mensajes |
| Reseñas / comentarios entre clientes | Comunicación entre segmentos |
| Puntos de fidelidad, cuotas, billetera | Pagos |
| Cambio de moneda o región | País e idioma |
| "Mejorar el buscador / filtros / carrito" | Modificar un feature existente |
| Wishlist / favoritos | Necesita cuenta de usuario o perfil (riesgoso) |
| Política de cambio de talla | Devoluciones |

## Paso B · Banco de features "seguros" (adáptalos al rubro del caso)

| Feature nuevo | Sirve para… | Métrica de negocio | Métrica financiera |
|---|---|---|---|
| Recomendador / guía inteligente (talla, plan, producto) | e-commerce, servicios | Conversión | +% ventas |
| "Completa tu compra" / productos complementarios | e-commerce | Attach rate | Ticket promedio |
| Packs / combos / bundles | e-commerce, comida, servicios | % de pedidos con pack | Ventas, ticket |
| Disponibilidad en local físico + reserva | Retail con tiendas | Uso + conversión | Ventas atribuidas |
| Probador / vista virtual (AR, 3D, simulador) | Moda, muebles, autos, inmuebles | Add-to-cart | Ventas móvil |
| Comparador lado a lado | Catálogos grandes | Conversión, tiempo de decisión | Ventas |
| Asistente / quiz "encuentra tu ideal" | Clientes indecisos | Conversión | Ventas |
| Ofertas flash / por tiempo limitado | Retail, delivery, viajes | Retorno a 7 días | Ventas |
| Calculadora o cotizador | Servicios, seguros, construcción | Leads o solicitudes | Ventas |
| Agenda o reserva de cita / visita | Salud, servicios, inmobiliaria | % de reservas | Ventas |
| Seguimiento visual del pedido (sin notificaciones) | Delivery, logística | Recompra | Ventas recurrentes |
| Contenido guía (lookbook, tutoriales, rutinas) | Moda, fitness, educación | Tiempo en sitio, conversión | Ventas |

## Paso C · Pregunta 1 – Planning (35 min)

**Orden y estructura exacta** (según tus clases: *Raw Material → Uncover Premises → Prepare Questions → Establish Motivation*):

### C1. As-Is (2–3 líneas)
> [Empresa] es [qué hace]. Su plataforma actual ofrece [features existentes]. Quiere [objetivo del caso: expansión, mejorar la experiencia…], pero no tiene features que [problema].

### C2. Raw Material → Premisas (tabla de 8 filas)
| Tipo (Assumption / Knowledge gap / Idea / Claim) | Raw material | Premisa descubierta |
|---|---|---|
| | | |

Usa **los 4 tipos** al menos una vez.

### C3. Supuestos y Question Backlog (plantilla Excel)
| # | Supuesto (lo que creo y NO pruebo) | Pregunta (lo que NO sé y voy a probar) |
|---|---|---|
| Q1 | | ¿…? |

Reglas de la plantilla:
- El negocio **ya existe**: lo que propongas incrementa o modifica algo de un negocio en marcha.
- El supuesto y la pregunta **están relacionados y se parecen, pero no son iguales**.
- La pregunta es **sobre el comportamiento del cliente** ("¿Los clientes X harían Y si Z?"), no sobre el feature en sí.

### C4. Question Prioritization Matrix
| Question | Confidence | Risk | Impact | Interest | Total Score |
|---|---|---|---|---|---|
| Q1 | 1–5 | 1–5 | 1–5 | 1–5 | suma |

Define la escala en una línea (Confidence = seguridad de poder responderla con un experimento; Risk = riesgo de no responderla; Impact = impacto en ventas; Interest = interés del negocio). Ordena de mayor a menor y presenta el **Question Backlog priorizado**.

### C5. Experiment Card ×8 (plantilla de clase, en una tabla por card)
| Campo | Contenido |
|---|---|
| **Question** | La pregunta del backlog, copiada igual |
| **Why** | ¿Por qué ganaría el negocio? → cómo genera dinero o qué problema resuelve |
| **What** | La forma más simple de validarlo: *"Agregar [feature] en [pantalla]… Test A/B sobre [N total] [usuarios/pedidos] (50/50) durante [2 semanas]."* |
| **Hypothesis** | *"Si [el X % de los usuarios usa el feature / la métrica de negocio pasa de A a B], entonces [métrica de negocio cambia de A a B] e incrementaremos [las ventas / el ticket] en al menos Y %."* |
| **Métricas** | Fórmulas: Conversión = compras / visitas; % de uso = sesiones que usan el feature / sesiones; Ventas (S/) |
| **Metas** | Uso ≥ X %; métrica ≥ B; **+Y % ventas** |

**Checklist de la Hypothesis (está en el Excel del profe):**
- [ ] Tiene **implícita la solución** (nombra el feature).
- [ ] Tiene **métricas**: siempre **una de negocio y una financiera**.
- [ ] No habla de generalidades ("mejorar la experiencia" ❌).
- [ ] **No afirma**: es condicional ("Si… entonces…").
- [ ] No somete a prueba la buena voluntad ("los clientes estarán contentos" ❌).
- [ ] Números sensatos: aumentos de +3 % a +10 % en ventas, y metas de conversión cercanas a la línea base.

## Paso D · Pregunta 2 – Design (40 min)

Pasos de la fase de diseño, que debes nombrar como subtítulos: **4. Formulate Hypothesis → 5. Decide Measures → 6. Determine Conditions → 7. Calculate Scale → 8. Decide Method.** Escribe una línea indicando que las preguntas son *belief-led*.

### D1. Null & Alternative Hypotheses ×8 (formato fijo)
- **Question:** (copiada del backlog)
- **Belief:** creencia previa en una línea.
- **Hypothesis (H1):** *Creemos que [construir FEATURE] para [SEGMENTO] logrará que [MÉTRICA] pase de [A] a [B] [y que las ventas suban Y %]. La evidencia se reflejará en [MEDIDAS], bajo las circunstancias de [A/B test 50/50 con N por grupo durante 2 semanas].*
- **Null hypothesis (H0):** *[FEATURE] no producirá un cambio significativo en [LA MISMA MÉTRICA] (se mantiene en [A]); cualquier diferencia se deberá al azar.*
- **Notación:** H0: p_B = p_A | H1: p_B > p_A (meta [B]).

**Checklist de la rúbrica para cada par:**
- [ ] **Falseable**: H0 puede resultar cierta.
- [ ] **Comprobable**: un A/B en 2–3 semanas.
- [ ] **Medible**: métrica y valor explícitos.
- [ ] **Describe un cambio**: "de A a B".
- [ ] **Sigue el template**: Creemos que… para… logrará… La evidencia… bajo las circunstancias…
- [ ] **H0 es el reflejo**: misma métrica, mismo segmento, sin cambio.

### D2. Measures (tabla)
| Exp. | Medida principal (decide H0/H1) | Medidas secundarias |

Las medidas deben ser **representativas, calculables y proporcionales**.

### D3. Conditions (tabla)
| Exp. | Participantes | Control (A) = As-Is, actúa como si H0 fuera cierta | Experimental (B) = con el feature |

Asignación aleatoria 50/50 por usuario; cada usuario ve siempre la misma versión.

### D4. Scale – tamaño de muestra
```
n por grupo = (Zα/2 + Zβ)² · [p1(1 − p1) + p2(1 − p2)] / (p2 − p1)²
α = 0.05 → Zα/2 = 1.96   |   potencia 80 % → Zβ = 0.84   |   (1.96 + 0.84)² = 7.84
```
Redondea siempre **hacia arriba**. Duración mínima de 2 semanas (ciclo semanal completo).

**Tabla rápida ya calculada** (elige pares de aquí y no tendrás que hacer cuentas):

| p1 (control) | p2 (meta) | Mejora | p1q1 + p2q2 | (p2 − p1)² | n por grupo | Total |
|---|---|---|---|---|---|---|
| 2 % | 2.4 % | +20 % | 0.043024 | 0.000016 | 21,082 | 42,164 |
| 2 % | 2.5 % | +25 % | 0.043975 | 0.000025 | 13,791 | 27,582 |
| 3 % | 3.6 % | +20 % | 0.063804 | 0.000036 | 13,896 | 27,792 |
| 3 % | 4 % | +33 % | 0.067500 | 0.000100 | 5,292 | 10,584 |
| 5 % | 6 % | +20 % | 0.103900 | 0.000100 | 8,146 | 16,292 |
| 5 % | 8 % | +60 % | 0.121100 | 0.000900 | 1,055 | 2,110 |
| 10 % | 12 % | +20 % | 0.195600 | 0.000400 | 3,834 | 7,668 |
| 10 % | 13 % | +30 % | 0.203100 | 0.000900 | 1,770 | 3,540 |
| 15 % | 18 % | +20 % | 0.275100 | 0.000900 | 2,397 | 4,794 |
| 20 % | 24 % | +20 % | 0.342400 | 0.001600 | 1,678 | 3,356 |
| 20 % | 25 % | +25 % | 0.347500 | 0.002500 | 1,090 | 2,180 |
| 30 % | 35 % | +17 % | 0.437500 | 0.002500 | 1,373 | 2,746 |
| 40 % | 46 % | +15 % | 0.488400 | 0.003600 | 1,064 | 2,128 |
| 50 % | 56 % | +12 % | 0.496400 | 0.003600 | 1,082 | 2,164 |

Muestra **un cálculo completo** como ejemplo: *n = 7.84 × 0.043024 / 0.000016 = 21,081.8 → 21,082 por grupo*. El **What** de la Experiment Card debe usar el mismo N total.

### D5. Method
> A/B test (experimento controlado aleatorizado). Prueba Z de diferencia de proporciones (prueba t si la métrica es un promedio, como el ticket o el tiempo). **Regla:** si p-value < 0.05 y se alcanza la meta, se rechaza H0, se acepta H1 y el feature se lanza a todos; si no, no se rechaza H0, el feature no se lanza y se registra lo aprendido.

## Paso E · Revisión final de la Parte 1 (en los últimos 10 min)
- [ ] Son 8 preguntas, 8 cards y 8 pares H1/H0, con la **misma numeración** en todas las secciones.
- [ ] Ningún feature toca una restricción ni modifica algo existente.
- [ ] Los números coinciden en todas partes: el A→B de la card es el mismo de la H1, de la tabla de scale y del N del What.
- [ ] Cada H1 tiene una métrica de negocio **y** una financiera.

---

# PARTE 2 – CASO 2 (Docker) · Proyecto **Clair** (`clair-ui`)

> Usa **2 terminales de PowerShell**. Usuario de Docker Hub: **krxxg**. Puerto 8081 (el 8080 lo usa el backend de Clair).
> Escenario que debes explicar: *"El frontend de mi proyecto Clair (Angular) se despliega en un contenedor Ubuntu 22.04 con Nginx, se guarda como imagen y se comparte en Docker Hub."*

## Pregunta 3 · Descarga (PULL) — Terminal 1
```powershell
docker --version
docker login -u krxxg
docker pull ubuntu:22.04
docker images ubuntu
```
- Si `docker login -u krxxg` da `unauthorized`, usa `docker login` sin `-u` (abre el navegador) o pega tu token como contraseña.
- **Explica:** `pull` descarga de Docker Hub la imagen base Ubuntu 22.04, donde se instalará el servidor web de Clair.

📸 Versión · `Login Succeeded` · `Downloaded newer image for ubuntu:22.04` · `docker images ubuntu`

## Pregunta 4 · Instalación (RUN) — Terminal 1
```powershell
docker run -dit --name clair-ui-app -p 8081:80 ubuntu:22.04
docker ps
docker exec -it clair-ui-app bash
```
Dentro del contenedor (`root@...:/#`):
```bash
apt-get update
DEBIAN_FRONTEND=noninteractive apt-get install -y nginx curl
nginx -v
```
- **Explica:** `-d` = segundo plano, `-it` = terminal interactiva, `--name` = nombre del contenedor, `-p 8081:80` = puerto del host → puerto del contenedor. `exec -it bash` abre una consola dentro del contenedor, y Nginx se instala **dentro** de él.
- ⚠️ **No cierres esta terminal.**

📸 `docker ps` (Up, `0.0.0.0:8081->80/tcp`) · final de la instalación (`Setting up nginx`) · `nginx -v` con el prompt `root@`

## Pregunta 5 · Configuración + guardar en imagen

**Terminal 2:**
```powershell
cd "C:\Users\ASUS\Desktop\UPC\UPC-Ciclo Vlll\Diseño de Experimentos\clair-ui"
docker cp "dist/angular-project/browser/." clair-ui-app:/var/www/html/
```
**Terminal 1** (dentro del contenedor):
```bash
rm -f /var/www/html/index.nginx-debian.html
ls /var/www/html
```
Pega este bloque **completo, de una vez**:
```bash
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
```
```bash
nginx -t
service nginx start
curl -I http://localhost
```
➡️ Abre **http://localhost:8081** en el navegador: debe cargar Clair.

```bash
exit
```
**Terminal 1** (ya en PowerShell):
```powershell
docker commit --change "CMD nginx -g 'daemon off;'" --change "EXPOSE 80" clair-ui-app krxxg/clair-ui:1.0
docker images krxxg/clair-ui
docker run -d --name clair-ui-verif -p 8082:80 krxxg/clair-ui:1.0
docker ps
```
➡️ Abre **http://localhost:8082**: Clair desde la imagen nueva.

- **Explica:** `docker cp` copia el build de Clair al contenedor. `try_files` es la configuración que necesita una SPA de Angular. `nginx -t` valida la configuración. `docker commit` guarda en la imagen `krxxg/clair-ui:1.0` el contenedor con Nginx instalado, configurado y con la app. `--change CMD` hace que Nginx arranque solo.

📸 `Successfully copied` · `ls /var/www/html` · `syntax is ok` + `[ OK ]` + `HTTP/1.1 200 OK` · **navegador 8081 con Clair** · `docker commit` (sha256) + `docker images krxxg/clair-ui` · navegador 8082

## Pregunta 6 · Compartir (PUSH) — Terminal 1
```powershell
docker push krxxg/clair-ui:1.0
```
➡️ Navegador: **hub.docker.com/repositories/krxxg** → repo `clair-ui` → pestaña **Tags** → `1.0`.

Extra (demuestra que cualquiera la descarga):
```powershell
docker rm -f clair-ui-verif
docker rmi krxxg/clair-ui:1.0
docker pull krxxg/clair-ui:1.0
```
- **Explica:** `push` sube la imagen al repositorio `krxxg/clair-ui` de Docker Hub. Desde ahí cualquiera puede hacer `docker pull` y ejecutar la app con la misma configuración.

📸 `Pushed` + `1.0: digest: sha256:...` · Docker Hub con el repo `clair-ui` · pestaña Tags con `1.0` · (extra) el pull de vuelta

## Checklist de capturas para el Word (14)
| # | Preg. | Captura |
|---|---|---|
| 1 | P3 | `docker --version` + `Login Succeeded` |
| 2 | P3 | `docker pull ubuntu:22.04` |
| 3 | P3 | `docker images ubuntu` |
| 4 | P4 | `docker run` + `docker ps` (Up, 8081->80) |
| 5 | P4 | `apt-get install` terminado |
| 6 | P4 | `nginx -v` dentro del contenedor |
| 7 | P5 | `docker cp` + `ls /var/www/html` |
| 8 | P5 | `nginx -t` + `[ OK ]` + `200 OK` |
| 9 | P5 | **Navegador localhost:8081 con Clair** |
| 10 | P5 | `docker commit` + `docker images krxxg/clair-ui` |
| 11 | P5 | Navegador localhost:8082 |
| 12 | P6 | `docker push` con digest |
| 13 | P6 | Docker Hub: repo `clair-ui` |
| 14 | P6 | Docker Hub: Tags → `1.0` |

## Si algo falla
| Error | Solución |
|---|---|
| `unauthorized: incorrect username or password` | `docker login` sin `-u`, o usa un Personal Access Token como contraseña |
| `push access denied ... insufficient_scope` | La imagen no lleva `krxxg/`. Ejecuta `docker tag <imagen> krxxg/clair-ui:1.0` y vuelve a hacer push |
| `GetFileAttributesEx ... cannot find the file` en `docker cp` | No estás en la carpeta `clair-ui` o falta el build (`npm run build`) |
| Los archivos no aparecen en la imagen | Hiciste el `docker cp` después del commit. El orden es cp → configurar → commit |
| `Conflict. The container name ... is already in use` | `docker rm -f clair-ui-app` (o `clair-ui-verif`) |
| `port is already allocated` | Cambia el puerto: `-p 8083:80` |
| La página no carga en 8081 | Dentro del contenedor ejecuta `service nginx start` y `curl -I http://localhost` |
| La página no carga en 8082 | Faltó el `--change "CMD nginx -g 'daemon off;'"` en el commit. Repite el commit |
| `docker: error during connect` / `pipe ... not found` | Docker Desktop está cerrado: ábrelo y espera a que diga **Engine running** |
| Texto en rojo de `npm` (*deprecated*, *budget*) | Son advertencias. Si dice `Application bundle generation complete`, el build está bien |

## Limpieza después del examen (opcional)
```powershell
docker rm -f clair-ui-app clair-ui-verif
docker rmi krxxg/clair-ui:1.0 ubuntu:22.04
docker logout
```
