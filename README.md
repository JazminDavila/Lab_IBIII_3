# Amplificador de Instrumentación de Tres Op-Amps — Ganancia Diferencial y Rechazo de Modo Común

**Informe de Laboratorio N.º 3 — Instrumentación Biomédica III**  
*Escuela Profesional de Ingeniería Biomédica — Universidad Nacional Mayor de San Marcos (UNMSM)*

---

## 1. Resumen

En esta experiencia se implementó y caracterizó un amplificador de instrumentación discreto de tres amplificadores operacionales, basado en el circuito integrado **TL084N**. La primera etapa (A1 y A2) está formada por dos amplificadores no inversores con una resistencia de ganancia $R_g$ entre sus entradas inversoras, y la segunda etapa (A3) es un restador con resistencias apareadas previamente. La ganancia diferencial nominal de diseño es $A_d = 21\text{ V/V}$.

Con ambas entradas a tierra se midió una tensión continua de salida (offset) de **−8.3 mV**, sin saturación. Luego se evaluó el circuito con una señal sinusoidal de 60 Hz bajo excitación diferencial de baja amplitud ($V_1 = 5.20\text{ mV}_{pp}$) y bajo excitación de modo común de gran amplitud ($V_1 = V_2 = 4.80\text{ V}_{pp}$).

Con las resistencias medidas se obtuvo una ganancia diferencial teórica de **20.96 V/V**, una ganancia diferencial medida de **$A_d = 5.54\text{ V/V}$** y una ganancia de modo común de **$A_{cm} = 0.00542\text{ V/V}$**, lo que da un **CMRR de 60.19 dB**.

---

## 2. Objetivos

* **Amplificación de una señal pequeña:** medir la ganancia ante una señal diferencial de unos 10 mV$_{pp}$, del orden de un biopotencial.
* **Rechazo de modo común:** medir qué parte de una señal de 1 V$_{pp}$ a 60 Hz, aplicada por igual a ambas entradas (interferencia de red), llega a la salida.
* **Comparación:** verificar que el circuito amplifica la señal diferencial y atenúa la de modo común.

---

## 3. Diagrama de Bloques y Arquitectura del Sistema

El generador de funciones entrega una señal de 1 V$_{pp}$ y 60 Hz. En la Etapa B pasa por un divisor resistivo (RD1 = 10 kΩ, RD2 = 100 Ω) que la reduce a unos 10 mV$_{pp}$ en V1, con V2 a GND. En la Etapa C se retira el divisor y la señal se aplica a V1 y V2 unidos. La etapa de entrada (A1, A2) amplifica la diferencia con ganancia $1 + (R_{1a}+R_{1b})/R_g$, el restador (A3) entrega $V_{OUT}$ con ganancia $R_3/R_2 \approx 1$, y el osciloscopio mide V1 (CH1) y $V_{OUT}$ (CH2).

![Diagrama de Bloques](imagenes/fig1_diagrama_bloques.png)
*Figura 1. Diagrama de bloques del amplificador de instrumentación y de los equipos de medición. La línea naranja punteada indica la reconexión de la Etapa C (V1 = V2, sin divisor).*

---

## 4. Esquemático Eléctrico y Montaje Físico

El circuito usa un TL084N (cuatro op-amps): los op-amps 1, 2 y 3 cumplen las funciones de A1, A2 y A3, y el op-amp 4, sin uso, se configuró como seguidor con la entrada no inversora a GND. La alimentación es una fuente dual de $\pm 12\text{ V}$ con capacitores de desacople de 100 nF a GND en cada pin de alimentación.

La ganancia diferencial total es:

$$A_d = \left(1 + \frac{2R_1}{R_g}\right)\left(\frac{R_3}{R_2}\right)$$

Con $R_1 = R_2 = R_3 = 10\text{ k}\Omega$ y $R_g = 1\text{ k}\Omega$, la ganancia teórica nominal es 21.

![Circuito de referencia](imagenes/fig10_circuito_referencia.png)
*Figura 10. Circuito de referencia de la guía de laboratorio.*

![Esquemático en Proteus](imagenes/fig11_esquematico_proteus.png)
*Figura 11. Esquemático del circuito armado (Proteus), con numeración de pines del TL084N, alimentación de ±12 V y capacitores de desacople.*

![Montaje en Protoboard](imagenes/fig12_montaje_protoboard.jpg)
*Figura 12. Montaje sobre protoboard del TL084N, capacitores de desacople y resistencias apareadas del restador.*

---

## 5. Resultados

### Tabla de resistencias (valores nominales vs. medidos)

| Resistencia | Nominal | Medido |
| :---: | :---: | :---: |
| R1a | 10 kΩ | 9.89 kΩ |
| R1b | 10 kΩ | 9.85 kΩ |
| Rg | 1 kΩ | 0.981 kΩ |
| R2a | 10 kΩ | 9.82 kΩ |
| R2b | 10 kΩ | 9.82 kΩ |
| R3a | 10 kΩ | 9.73 kΩ |
| R3b | 10 kΩ | 9.76 kΩ |
| RD1 | 10 kΩ | 9.80 kΩ |
| RD2 | 100 Ω | 99.6 Ω |

| R1a | R1b | Rg |
| :---: | :---: | :---: |
| ![R1a](imagenes/fig2_medicion_R1a.jpg) | ![R1b](imagenes/fig3_medicion_R1b.jpg) | ![Rg](imagenes/fig4_medicion_Rg.jpg) |
| *Fig. 2* | *Fig. 3* | *Fig. 4* |

| R2a y R2b | R3a | R3b |
| :---: | :---: | :---: |
| ![R2](imagenes/fig5_medicion_R2a_R2b.jpg) | ![R3a](imagenes/fig6_medicion_R3a.jpg) | ![R3b](imagenes/fig7_medicion_R3b.jpg) |
| *Fig. 5* | *Fig. 6* | *Fig. 7* |

| RD1 | RD2 | Offset en $V_{OUT}$ |
| :---: | :---: | :---: |
| ![RD1](imagenes/fig8_medicion_RD1.jpg) | ![RD2](imagenes/fig9_medicion_RD2.jpg) | ![Offset](imagenes/fig13_offset_vout.jpg) |
| *Fig. 8* | *Fig. 9* | *Fig. 13* |

*Mediciones con el multímetro Fluke 179 (resistencias y tensión continua de offset).*

### Mediciones por etapa

| Etapa | Condición | Entrada | $V_{OUT}$ | Observación |
| :---: | :--- | :---: | :---: | :--- |
| A | V1 = V2 = GND | 0 V | **−8.3 mV (DC)** | Sin saturación |
| B | Señal diferencial, 60 Hz | 5.20 mV$_{pp}$ | **28.80 mV$_{pp}$** | En fase con V1 (≈ 0°) |
| C | Señal de modo común, 60 Hz | 4.80 V$_{pp}$ | **26 mV$_{pp}$** | Senoidal de 60 Hz sobre el piso de ruido |

![Respuesta diferencial](imagenes/fig14_respuesta_diferencial.jpg)
*Figura 14. Respuesta a una señal diferencial (Etapa B).*

![Respuesta de modo común](imagenes/fig15_respuesta_modo_comun.jpg)
*Figura 15. Respuesta a una señal de modo común (Etapa C).*

### Ganancias y CMRR

| Magnitud | Cálculo | Resultado |
| :--- | :--- | :---: |
| Ganancia diferencial teórica | $\left[1 + \frac{R_{1a}+R_{1b}}{R_g}\right] \times \frac{1}{2}\left(\frac{R_{3a}}{R_{2a}} + \frac{R_{3b}}{R_{2b}}\right)$ | **20.96 V/V** |
| Ganancia diferencial medida, $A_d$ | $V_{OUT}/V_1$ (Etapa B) | **5.54 V/V** |
| Ganancia de modo común, $A_{cm}$ | $V_{OUT}/V_1$ (Etapa C) | **0.00542 V/V** |
| CMRR | $20\log_{10}(A_d/A_{cm})$ | **60.19 dB** |

* **Relaciones del restador:** $R_{3a}/R_{2a} = 0.9908$ y $R_{3b}/R_{2b} = 0.9939$, con una diferencia de solo $0.0031$ (0.31 %) gracias al apareamiento previo.
* **Comparación de salidas:** la señal de modo común fue unas 923 veces mayor que la diferencial, pero las salidas fueron del mismo orden (26 mV$_{pp}$ vs. 28.80 mV$_{pp}$).
* **Diferencia entre $A_d$ teórica y medida:** se atribuye a posibles falsos contactos en $R_g$ y a la lectura de V1 con punta ×1 sobre el divisor, que pudo incorporar ruido de 60 Hz.
* **Peor caso sin aparear (±5 %):** $A_{cm} \approx 4t/(1+R_3/R_2) = 0.10\text{ V/V}$ (CMRR ≈ 20 dB), frente a 0.00542 V/V obtenido (mejora de unas 18.5 veces, +25.3 dB).
* **Referencia clínica:** las normas IEC 60601-2-27 e IEC 60601-2-25 exigen un CMRR mínimo de 80–89 dB, por lo que el montaje es adecuado para fines académicos pero queda por debajo del umbral clínico.

---

## 6. Componentes e Instrumental Utilizados

| Componente / equipo | Cantidad |
| :--- | :---: |
| TL084N | 1 |
| Resistencia 10 kΩ | 7 |
| Resistencia 1 kΩ | 1 |
| Resistencia 100 Ω | 1 |
| Capacitor cerámico 100 nF | 2 |
| Cable BNC–caimán | 1 |
| Protoboard | 1 |
| Cables jumper macho-macho | ≈ 20 |

* Fuente de banco dual de $\pm 12\text{ V}$
* Generador de funciones (señal senoidal de 1 V$_{pp}$, 60 Hz)
* Osciloscopio digital ATTEN ADS1062CML
* Multímetro Fluke 179 True RMS

---

## 7. Conclusiones

* Se armó y verificó un amplificador de instrumentación de tres op-amps con el TL084N y resistencias apareadas, con una tensión de salida en reposo de −8.3 mV, sin saturación.
* Ante una señal diferencial de 5.20 mV$_{pp}$ a 60 Hz, el circuito amplificó la señal manteniendo la fase respecto a V1, con $A_d = 5.54\text{ V/V}$ (frente a 20.96 V/V teóricos).
* Ante una señal de modo común de 4.80 V$_{pp}$ a 60 Hz, la salida se atenuó hasta 26 mV$_{pp}$ ($A_{cm} = 0.00542\text{ V/V}$), con un CMRR experimental de 60.19 dB, lo que muestra la capacidad de la topología para rechazar interferencias comunes en la adquisición de biopotenciales.

---

## 8. Referencias

* Analog Devices. (1998). *A practical review of common mode and instrumentation amplifiers.*
* Kugelstadt, T. (2005). *Getting the most out of your instrumentation amplifier design.* Texas Instruments.
* Texas Instruments. (s. f.). *TL08x JFET-input operational amplifiers* [Hoja de datos].
* Winter, B. B., & Webster, J. G. (1983). Driven-right-leg circuit design. *IEEE Transactions on Biomedical Engineering, BME-30*(1), 62–66.
* Horowitz, P., & Hill, W. (2015). *The art of electronics* (3.ª ed.). Cambridge University Press.
* Webster, J. G. (Ed.). (2010). *Medical instrumentation: Application and design* (4.ª ed.). Wiley.

---

## 9. Integrantes

* **Dávila Pucuhuayla, Jazmín Saraí** — *Código: 23190369*
* **More Quispe, Gregory Martin** — *Código: 23190125*
* **Leon Vasquez, Jimmy Fabricio** — *Código: 23190378*
* **Maldonado Villacorta, Paola Margot** — *Código: 23190124*

**Docente:** Dra. María Elisia Armas Alvarado  
**Curso:** Instrumentación Biomédica III — Universidad Nacional Mayor de San Marcos (UNMSM)  
**Grupo / horario:** 2:00 – 4:00 pm  
**Fecha:** 21/11/2026
