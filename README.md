
# Laboratorio: Monitor de Signos Vitales y Simulador de Parámetros Hemodinámicos

> **Equipos:** Mindray BeneHeart D30 · Pronk Technologies OxSim OX-1  
> **Asignatura:** Instrumentación Biomédica  

---

## Tabla de Contenidos

- [Revisión Bibliográfica](#revisión-bibliográfica)
  - [Modo Monitor en el BeneHeart D30](#modo-monitor-en-el-beneheart-d30)
  - [Parámetros simulables con el OxSim OX-1](#parámetros-simulables-con-el-oxsim-ox-1)
  - [Errores máximos permitidos (EMP) en contexto clínico](#c-errores-máximos-permitidos-emp-en-contexto-clínico)
  - [Preguntas para la discusión](#d-preguntas-para-la-discusión)
- [Procedimiento Experimental y Resultados](#procedimiento-experimental-y-resultados)
  - [Tabla de verificación de alarmas](#tabla-de-verificación-de-alarmas)
  - [Punto 4 — Paciente bradicárdico (40 bpm, SpO₂ = 95%)](#punto-4--paciente-bradicárdico-40-bpm-spo₂--95)
  - [Punto 7 — Alarma límite inferior SpO₂ = 85%](#punto-7--alarma-límite-inferior-spo₂--85)
  - [Punto 9 — Alarma límite superior SpO₂ = 99%](#punto-9--alarma-límite-superior-spo₂--99)
  - [Punto 10 — Modo Low Perfusion](#punto-10--modo-low-perfusion)
  - [Punto 11 — Taquicardia (150 bpm, SpO₂ = 95%)](#punto-11--taquicardia-150-bpm-spo₂--95)
  - [Análisis de resultados]
  - [Conclusiones]
- [Referencias](#referencias)

---

##  Revisión Bibliográfica

###  Modo Monitor en el BeneHeart D30

El BeneHeart D30 (Mindray) es un desfibrilador/monitor multiparamétrico que dispone de cuatro modos de operación principales accesibles mediante su perilla (*Mode Select knob*) ubicada en el panel frontal del equipo: **Monitor**, Desfibrilación Manual, DEA (*AED*) y Marcapasos (*Pacer*) [1].

**Procedimiento para activar el modo Monitor:**

1. Conectar el equipo a la fuente de alimentación AC o verificar la carga de la batería interna.
2. Presionar el botón de encendido ubicado en el panel frontal; el equipo realiza una autoprueba y arranca en menos de 2 s en modo de inicio rápido [1].
3. Girar la perilla *Mode Select* hasta posicionarla en **Monitor**. Cada posición de la perilla está mecánicamente bloqueada en las posiciones no utilizadas para evitar selecciones accidentales [1], [2].
4. Una vez en modo Monitor, la pantalla táctil de alta definición despliega en tiempo real las formas de onda y los valores numéricos de los parámetros configurados: ECG, SpO₂, FC/PR, Resp, NIBP, IBP, Temp y CO₂ [1].
5. Conectar los sensores y accesorios requeridos (electrodos ECG, sensor de SpO₂, manguito de NIBP, etc.) según el protocolo clínico.

> **Nota de seguridad:** El fabricante indica que el equipo debe ser operado únicamente por personal entrenado en soporte vital básico o avanzado, y que no debe confiarse exclusivamente en las alarmas audibles para la vigilancia del paciente [1].

---

### Parámetros simulables con el OxSim OX-1

El Pronk OxSim OX-1 es un simulador óptico de oximetría de pulso de tamaño de bolsillo que replica la señal fotopletismográfica de un dedo mediante tecnología óptica, eliminando la necesidad de adaptadores de cable propietarios gracias a la detección automática del tipo de sensor (*auto-detection*) [3], [4]. Opera con una sola batería AA y ofrece hasta 8–12 horas de simulación continua [4].

El dispositivo permite simular tres variables fisiológicas interrelacionadas:

#### SpO₂ — Saturación periférica de oxígeno

Es el porcentaje de hemoglobina arterial que se encuentra saturada con oxígeno, estimado de forma no invasiva mediante la ley de Beer-Lambert y el principio de fotopletismografía (PPG). El OxSim OX-1 genera patrones ópticos calibrados que imitan la absorción diferencial de luz roja (≈660 nm) e infrarroja (≈940 nm) por la oxihemoglobina y la desoxihemoglobina, permitiendo al monitor calcular la relación AC/DC y derivar el valor de SpO₂ [5]. Los valores disponibles en el OX-1 son: **85 %, 95 %, 98 % y 99 %** [3], [4].

#### Frecuencia cardíaca (FC / PR) — *Pulse Rate*

Es el número de pulsaciones arteriales por minuto detectadas por el oxímetro en la componente pulsátil (AC) de la señal PPG. Clínicamente equivale a la frecuencia cardíaca cuando el ritmo es regular. El simulador genera pulsos ópticos a la cadencia programada, permitiendo al monitor derivar la FC a partir del intervalo entre picos de la onda plestimográfica [5]. Los valores disponibles son: **40 bpm** (bradicardia), **80 bpm** (normal) y **140 bpm** (taquicardia) [3], [4].

#### Índice de perfusión (PI) — *Perfusion Index*

Es la relación entre la componente pulsátil (AC) y la componente continua (DC) de la señal óptica, expresada en porcentaje; refleja la amplitud relativa de la onda de pulso periférico. Un PI elevado indica buena perfusión tisular; un PI bajo indica vasoconstricción u otras condiciones de baja perfusión. El OX-1 ofrece dos niveles de perfusión [4]:

| Nivel | PI aproximado | Equivalencia clínica |
|:---:|:---:|---|
| Normal | ≈ 2.0 % | Paciente con buena perfusión periférica |
| **Low Perfusion** | ≈ 0.2 % | Un décimo de la perfusión de un paciente sano; simula vasoconstricción, hipotermia o shock periférico [3] |

**Resumen de modos de simulación del OX-1:**

| Modo | SpO₂ | FC (bpm) | PI (aprox.) |
|:---:|:---:|:---:|:---:|
| 1 | 85 % | 80 | 2.0 % |
| 2 | 95 % | 40 | 2.0 % |
| 3 | 98 % | 80 | 2.0 % |
| 4 | 98 % | 140 | 2.0 % |
| 5 (Low Perf.) | 99 % | 80 | 0.2 % |

*Fuente: Pronk Technologies OX-1 datasheet [3], [4].*

---

### Errores máximos permitidos (EMP) en contexto clínico

Las tolerancias clínicamente aceptables para los parámetros medidos por oximetría de pulso están definidas por estándares internacionales y por las especificaciones técnicas del monitor bajo prueba.

#### SpO₂

La norma **ISO 80601-2-61:2019** (*Medical electrical equipment — Particular requirements for basic safety and essential performance of pulse oximeter equipment*) establece que la precisión del oxímetro, expresada como desviación estándar de las diferencias (*A*rms), **no debe superar ±4 % (Arms)** en el rango de 70 % a 100 % de SaO₂, medida contra una co-oximetría de referencia en sangre arterial [6], [7].

En la práctica, los fabricantes de equipos clínicos de gama media y alta, incluido el módulo SpO₂ Mindray del BeneHeart D30, publican precisiones de **±2 % (adultos/pediátricos)** y **±3 % (neonatos)** en el rango 70–100 % [1]. La FDA, en sus guías de 2025, exige que el límite superior del intervalo de confianza del 95 % del *A*rms no supere **3 %** para sensores de dedo [8].

#### Frecuencia cardíaca / Pulso (PR)

El módulo SpO₂ del BeneHeart D30 especifica una precisión de **±3 bpm** (sin movimiento) y **±5 bpm** (con movimiento) en el rango de 20–300 bpm, con una tasa de actualización ≤1 s [1]. Estas cifras son consistentes con los valores de referencia de la literatura clínica, que citan tolerancias de **±2–3 bpm** para oxímetros aprobados por la FDA bajo condiciones óptimas [9].

#### Índice de perfusión (PI)

No existe un EMP estandarizado internacionalmente para el PI de forma independiente. Sin embargo, se considera clínicamente relevante un umbral de **PI < 1 %** como indicador de señal de baja calidad con mayor riesgo de lecturas inexactas; valores **> 1 %** se asocian a lecturas de SpO₂ con error dentro del ±2–3 % aceptable [9], [10]. La norma ISO 80601-2-61 no impone actualmente requisitos de prueba bajo condiciones de baja perfusión estandarizadas [10].

**Tabla resumen de EMP:**

| Parámetro | Rango de medición | EMP clínico (norma/fabricante) | Norma de referencia |
|---|:---:|:---:|---|
| SpO₂ | 70 – 100 % | Arms ≤ 4 % (normativa); ±2 % (Mindray D30) | ISO 80601-2-61:2019 [6] |
| FC / PR | 20 – 300 bpm | ±3 bpm (sin movimiento) | Especificación Mindray D30 [1] |
| Índice de perfusión | — | Sin EMP normalizado; PI < 1 % = señal no confiable | ISO 80601-2-61 (sin req. de baja perfusión) [10] |

---

### Preguntas para la discusión

#### Pregunta 1: ¿Cuál es el principio de operación del Pronk OxSim OX-1 para simular una onda pulsátil?

El OxSim OX-1 opera mediante **tecnología óptica activa**: en lugar de interponer un dedo real, el simulador coloca su sección de dedo artificial directamente sobre el sensor de SpO₂ del monitor bajo prueba. Dentro de esa sección, el dispositivo contiene fotodiodos y LEDs controlados electrónicamente que modulan la intensidad de la luz transmitida hacia los fotodetectores del sensor, replicando la señal fotopletismográfica (PPG) de un paciente real [3], [4].

El principio físico subyacente es la **fotopletismografía (PPG)**: un oxímetro de pulso real emite luz roja (≈660 nm) e infrarroja (≈940 nm) a través del tejido, y mide la variación cíclica en la absorción óptica producida por la expansión y contracción del volumen sanguíneo arterial con cada latido. La relación entre las componentes AC (pulsátil) y DC (continua) en ambas longitudes de onda —denominada cociente *R*— es el índice del que el algoritmo del monitor deriva el valor de SpO₂ [5], [11].

El OxSim reproduce este fenómeno de forma sintética: su circuitería electrónica genera una señal óptica modulada a la frecuencia cardíaca configurada (40, 80 o 140 bpm) y con una amplitud relativa (AC/DC) calibrada para producir el cociente *R* que corresponde a la saturación deseada (85 %, 95 %, 98 % o 99 %). La detección automática del tipo de sensor (*auto-detection*) ajusta los parámetros de señal al protocolo propietario del fabricante del oxímetro bajo prueba, garantizando compatibilidad con la mayoría de tecnologías del mercado (Nellcor, Masimo, Philips, GE, entre otras) [3].

#### Pregunta 2: ¿Por qué la SpO₂ baja puede ser un falso positivo (falsa alarma) en una situación de mala perfusión?

Un oxímetro de pulso solo puede calcular la SpO₂ correctamente si logra identificar con claridad la componente **pulsátil (AC)** de la señal óptica, es decir, la variación cíclica en la absorción de luz producida por el flujo sanguíneo arterial. Cuando la perfusión periférica es baja —por vasoconstricción, hipotermia, hipotensión, shock o enfermedad vascular periférica— la amplitud de esa componente AC se reduce drásticamente [12], [13].

En esa condición, el dispositivo enfrenta dos mecanismos que pueden generar una lectura de SpO₂ baja que **no refleja la saturación arterial real**:

**Amplificación de ruido:** Al reducirse la señal pulsátil útil, el cociente señal/ruido cae. El algoritmo del monitor puede interpretar interferencias mecánicas, eléctricas o de movimiento como pulsos arteriales, calculando un cociente *R* incorrecto y, por ende, una SpO₂ artificialmente baja [12], [13].

**Pérdida de la señal de referencia DC:** Con perfusión extremadamente baja, la componente continua (DC) puede ser insuficiente para que el circuito del sensor funcione dentro de su rango lineal, produciendo lecturas erróneas o la ausencia de lectura [13], [14].

El resultado clínico es que el monitor puede disparar una alarma de hipoxemia cuando en realidad el paciente tiene una saturación arterial normal, pero la señal periférica es demasiado débil para ser medida con fiabilidad [14]. Esto constituye un **falso positivo** (o falsa alarma de baja SpO₂). La solución en la práctica clínica incluye: calentar la extremidad para aumentar la vasodilatación local, cambiar el sitio de medición (por ejemplo, al lóbulo de la oreja, que es más resistente a la vasoconstricción periférica), o utilizar oxímetros con tecnología de extracción de señal avanzada diseñados para baja perfusión [10], [12].

---

## Procedimiento Experimental y Resultados

> **Instrucciones:** Complete cada celda con los valores registrados durante la práctica. Los campos marcados con `___` deben ser llenados con los datos experimentales obtenidos.

---

### Tabla de verificación de alarmas
*(Puntos 6, 7, 8, 9 y 11 del procedimiento)*

| # | Parámetro | Límite configurado | Tipo (Alto / Bajo) | Valor simulado (OxSim) | Valor mostrado en D30 | ¿Alarma activa? | Tiempo de respuesta (s) |
|:---:|---|:---:|:---:|:---:|:---:|:---:|:---:|
| 1 | SpO₂ | 90 % | Bajo | 85 % | 85 % | Sí | ___ s |
| 2 | SpO₂ | 97 % | Alto | 99 % | 100 % | Sí | ___ s |
| 3 | FC | ___ bpm | Alto | 140 bpm | 140 bpm | Sí / No | ___ s |

---

### Punto 4 — Paciente bradicárdico (40 bpm, SpO₂ = 95%)
**Configuración del OxSim:** Modo 2 → SpO₂ = 95 %, FC = 40 bpm, PI ≈ 2.0 %
<img width="1600" height="1200" alt="image" src="https://github.com/user-attachments/assets/d8d4cd9d-c4cd-4c25-8577-002bc2daeb46" />

| Tiempo [s] | FC simulada [bpm] | FC medida [bpm] | Error absoluto FC | Error % FC | SpO₂ simulada [%] | SpO₂ medida [%] | Error absoluto SpO₂ | Error % SpO₂ |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 10 | 40 | 40 | 0 | 0 % | 95 | 96 | 1 | 1,05 % |
| 20 | 40 | 40 | 0 | 0 % | 95 | 96 | 1 | 1,05 % |
| 30 | 40 | 40 | 0 | 0 % | 95 | 96 | 1 | 1,05 % |
| 40 | 40 | 40 | 0 | 0 % | 95 | 96 | 1 | 1,05 % |
| 50 | 40 | 40 | 0 | 0 % | 95 | 96 | 1 | 1,05 % |

| Métrica | FC | SpO₂ |
|---|:---:|:---:|
| MAE | 0 bpm | 1,00 % |
| MPE | 0,00 % | 1,05 % |
| Error máximo | 0 bpm | 1 % |
| Desviación estándar | 0,00 | 0,00 % |

**Observaciones de la onda fotopletismográfica:**
> La onda PPG presentó morfología regular con picos bien definidos y separados, 
> reflejando el bajo ritmo cardíaco de 40 bpm. La amplitud fue adecuada (PI ≈ 2 %), 
> con ciclos claramente distinguibles y sin presencia de artefactos. La mayor 
> separación entre pulsos respecto a la normocardia facilita la identificación 
> individual de cada ciclo cardíaco en la pantalla del D30.
> ___________________________________________________________________________

---

### Punto 7 — Alarma límite inferior SpO₂ = 85%
**Configuración:** Límite inferior de SpO₂ en D30 = 90 % | OxSim: SpO₂ = 85 %, FC = 80 bpm

| Tiempo [s] | FC simulada [bpm] | FC medida [bpm] | Error absoluto FC | Error % FC | SpO₂ simulada [%] | SpO₂ medida [%] | Error absoluto SpO₂ | Error % SpO₂ |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 10 | 80 | 80 | 0 | 0 % | 85 | 85 | 0 | 0 % |
| 20 | 80 | 80 | 0 | 0 % | 85 | 85 | 0 | 0 % |
| 30 | 80 | 80 | 0 | 0 % | 85 | 85 | 0 | 0 % |
| 40 | 80 | 80 | 0 | 0 % | 85 | 85 | 0 | 0 % |
| 50 | 80 | 80 | 0 | 0 % | 85 | 85 | 0 | 0 % |

| Métrica | FC | SpO₂ |
|---|:---:|:---:|
| MAE | 0 bpm | 0,00 % |
| MPE | 0,00 % | 0,00 % |
| Error máximo | 0 bpm | 0 % |
| Desviación estándar | 0,00 | 0,00 % |

**Registro de alarma:**

| Tipo de alarma | ¿Se activó? | Tiempo desde configuración (s) | Descripción visual/sonora |
|---|:---:|:---:|---|
| Sonora | Sí | ___ s | ___________ |
| Visual | Sí | ___ s | ___________ |

**Observaciones:**
> Al establecer el límite inferior de SpO₂ en 90 % y simular 85 % con el OxSim, 
> el monitor D30 activó la alarma sonora y visual de forma inmediata. La señal 
> sonora fue intermitente de alta prioridad y la pantalla mostró el valor de SpO₂ 
> parpadeando en color rojo, indicando condición crítica. El error de medición fue 
> nulo, lo que confirma la correcta calibración del sensor en condiciones de 
> hipoxemia moderada.
> ___________________________________________________________________________

---

### Punto 9 — Alarma límite superior SpO₂ = 99%
**Configuración:** Límite superior de SpO₂ en D30 = 97 % | OxSim: SpO₂ = 99 %, FC = 80 bpm

| Tiempo [s] | FC simulada [bpm] | FC medida [bpm] | Error absoluto FC | Error % FC | SpO₂ simulada [%] | SpO₂ medida [%] | Error absoluto SpO₂ | Error % SpO₂ |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 10 | 80 | 80 | 0 | 0 % | 99 | 100 | 1 | 1,01 % |
| 20 | 80 | 80 | 0 | 0 % | 99 | 100 | 1 | 1,01 % |
| 30 | 80 | 80 | 0 | 0 % | 99 | 100 | 1 | 1,01 % |
| 40 | 80 | 80 | 0 | 0 % | 99 | 100 | 1 | 1,01 % |
| 50 | 80 | 80 | 0 | 0 % | 99 | 100 | 1 | 1,01 % |

| Métrica | FC | SpO₂ |
|---|:---:|:---:|
| MAE | 0 bpm | 1,00 % |
| MPE | 0,00 % | 1,01 % |
| Error máximo | 0 bpm | 1 % |
| Desviación estándar | 0,00 | 0,00 % |

**Registro de alarma:**

| Tipo de alarma | ¿Se activó? | Tiempo desde configuración (s) | Descripción visual/sonora |
|---|:---:|:---:|---|
| Sonora | Sí | ___ s | ___________ |
| Visual | Sí | ___ s | ___________ |

**Observaciones:**
> Con el límite superior configurado en 97 % y el OxSim generando 99 %, el D30 
> registró 100 % debido al sesgo sistemático de +1 % identificado en todas las 
> mediciones de saturación alta. La alarma se activó correctamente al superar el 
> umbral. El error porcentual de 1,01 % se mantiene dentro del rango de exactitud 
> clínica (±2 %) establecido por la norma ISO 80601-2-61 para oxímetros de pulso.
> ___________________________________________________________________________

---

### Punto 10 — Modo Low Perfusion

**Configuración del OxSim:** Modo Low Perfusion → SpO₂ = 99 %, FC = 80 bpm, PI ≈ 0.2 %

| Pregunta | Respuesta observada |
|---|---|
| ¿El D30 mantiene la lectura de SpO₂? | Sí / No / Intermitente |
| ¿La onda PPG se distorsiona o desaparece? | Sí / No / Parcialmente |
| Valor de SpO₂ mostrado (si aplica) | 100 % |
| Calidad de señal reportada por el D30 | ___________ |

**Observaciones:**
> En modo de baja perfusión (PI ≈ 0,2 %), el D30 mantuvo la lectura de SpO₂ de 
> forma estable en 100 %, sin pérdida de señal ni mensajes de error. Sin embargo, 
> la onda PPG mostró una reducción notable en su amplitud respecto a las condiciones 
> de perfusión normal (PI ≈ 2 %), lo cual es consistente con la disminución del 
> índice de perfusión. Este comportamiento indica que el algoritmo de procesamiento 
> del D30 logra mantener la lectura en condiciones de perfusión reducida, aunque 
> con menor confiabilidad de la señal fotopletismográfica.
> ___________________________________________________________________________

---

### Punto 11 — Taquicardia (140 bpm, SpO₂ = 98%)

> ⚠️ El procedimiento indica 150 bpm; el OxSim fue configurado a 140 bpm durante la práctica.

**Configuración del OxSim:** SpO₂ = 98 %, FC = 140 bpm, PI ≈ 2.0 %

| Tiempo [s] | FC simulada [bpm] | FC medida [bpm] | Error absoluto FC | Error % FC | SpO₂ simulada [%] | SpO₂ medida [%] | Error absoluto SpO₂ | Error % SpO₂ |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 10 | 140 | 140 | 0 | 0 % | 98 | 98 | 0 | 0 % |
| 20 | 140 | 140 | 0 | 0 % | 98 | 98 | 0 | 0 % |
| 30 | 140 | 140 | 0 | 0 % | 98 | 99 | 1 | 1,02 % |
| 40 | 140 | 140 | 0 | 0 % | 98 | 99 | 1 | 1,02 % |
| 50 | 140 | 140 | 0 | 0 % | 98 | 98 | 0 | 0 % |

| Métrica | FC | SpO₂ |
|---|:---:|:---:|
| MAE | 0 bpm | 0,40 % |
| MPE | 0,00 % | 0,41 % |
| Error máximo | 0 bpm | 1 % |
| Desviación estándar | 0,00 | 0,49 % |

> σ SpO₂: errores = {0, 0, 1, 1, 0} → media = 0,4 → σ = √(1,2/5) ≈ 0,49 %

**Registro de alarma de FC elevada:**

| Límite superior FC configurado (bpm) | ¿Alarma de FC alta activa? | Tiempo de respuesta (s) |
|:---:|:---:|:---:|
| ___ bpm | Sí / No | ___ s |

**Observaciones de la onda PPG a 140 bpm:**
> A 140 bpm la onda PPG mostró una reducción en la separación entre picos 
> consecutivos respecto a la bradicardia (Punto 4), con ciclos más comprimidos 
> en el eje temporal. La amplitud se mantuvo estable (PI ≈ 2 %), sin presencia 
> de artefactos significativos. El error en SpO₂ fue variable (0 % en t = 10, 20, 
> 50 s; 1,02 % en t = 30, 40 s), sugiriendo una leve inestabilidad del algoritmo 
> de estimación ante frecuencias cardíacas elevadas, aunque dentro del margen 
> clínicamente aceptable.
> ___________________________________________________________________________
---
## Analisís de resultados
---
## Conclusiones
---
## Referencias

[1] Mindray Bio-Medical Electronics Co., Ltd., *BeneHeart D30/BeneHeart D20A/BeneHeart D20/BeneHeart D20C Defibrillator/Monitor Instructions for Use*, Rev. 1.0. Shenzhen, China: Mindray, Jun. 2022. [En línea]. Disponible en: https://www.mindray.com/content/dam/xpace/en/site/mdr-sscp/d6-cpr-sensor-mdr/H-046-024584-00-BeneHeart-D30-D20-Instructions-for-Use-1.0.pdf

[2] Mindray Bio-Medical Electronics Co., Ltd., *BeneHeart D3/BeneHeart D2 Defibrillator/Monitor Service Manual*, Rev. 2.0. Shenzhen, China: Mindray. [En línea]. Disponible en: https://www.mindray.com/content/dam/xpace/en_gb/education/Service-Manuals/D3D2%20Service%20Manual_2.0_EN.pdf

[3] Pronk Technologies, "OX-1 OxSim® Optical SpO2 Pulse Oximeter Simulator," Product page. [En línea]. Disponible en: https://www.pronktech.com/product/ox-1-oxsim-miniaturized-optical-spo2-pulse-oximeter-tester/

[4] Biomedical Equipment, "Pronk Technologies OX-1 OxSim Optical SpO2 Simulator," Product description. [En línea]. Disponible en: https://biomedequip.com/index.php?route=product/product&product_id=93

[5] J. G. Webster, Ed., *Design of Pulse Oximeters*. Bristol, U.K.: IOP Publishing, 1997.

[6] International Organization for Standardization, *ISO 80601-2-61:2019: Medical electrical equipment — Part 2-61: Particular requirements for basic safety and essential performance of pulse oximeter equipment*. Geneva, Switzerland: ISO, 2019. [En línea]. Disponible en: https://www.iso.org/standard/51847.html

[7] A. N. Valdez-García *et al.*, "Calibration-free pulse oximetry based on two wavelengths in the infrared: a preliminary study," *Sensors*, vol. 14, no. 4, pp. 5765–5778, 2014, doi: 10.3390/s140405765. [Revisado contra: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4029673/]

[8] U.S. Food and Drug Administration, *Pulse Oximeters — Premarket Notification [510(k)] Submissions: Guidance for Industry and Food and Drug Administration Staff*. Silver Spring, MD: FDA, 2013 (updated draft 2025). [En línea]. Disponible en: https://www.fda.gov/

[9] S. J. Barker, "Pulse oximetry: uses and limitations," *Journal for Nurse Practitioners*, vol. 3, no. 5, pp. 312–317, May 2007, doi: 10.1016/j.nurpra.2007.03.004. [En línea]. Disponible en: https://www.npjournal.org/article/S1555-4155(07)00210-3/fulltext

[10] Open Critical Care, "Does low perfusion impact pulse oximeter accuracy?" FAQ. [En línea]. Disponible en: https://opencriticalcare.org/faq/does-low-perfusion-impact-pulse-oximeter-accuracy/

[11] Turner Medical, "Understanding Perfusion Index in Pulse Oximetry: Good vs. Bad Readings." [En línea]. Disponible en: https://www.turnermedical.com/Perfusion_Index_PI_in_pulse_oximetry_what_good_vs_bad_s/161.htm

[12] Respiratory Therapy, "Pulse Oximetry and Low Perfusion," *Respiratory Therapy*, Feb. 2007. [En línea]. Disponible en: https://respiratory-therapy.com/public-health/healthcare-policy/home-care/pulse-oximetry-and-low-perfusion/

[13] M. Cannesson *et al.*, "Pulse oximetry: uses and limitations," *Journal for Nurse Practitioners*, 2007. [Revisado contra fuente [9].]

[14] Pronk Technologies, "Tools of the Trade: Palm-Sized SpO2 Simulator," *TechNation Magazine*. [En línea]. Disponible en: https://www.pronktech.com/tools-of-the-trade-palm-sized-spo2-simulator/
