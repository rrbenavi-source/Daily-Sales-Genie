# Cómo calcula el Gap vs AP el Power BI — para usuario final

Ejemplo concreto: **Marca XX Lager, Canal OFF TRADE, Mayo 2026, corte al día 15**.

---

## Paso 1 — ¿Cuánto vendiste este año hasta hoy?

```
MTD Actual Year = HL vendidos del 1 al 15 de mayo 2026

Ejemplo: 500 HL
```

Esto es simplemente lo que llevas vendido en el mes hasta el día de corte.

---

## Paso 2 — ¿Cuánto vendiste el año pasado en el mismo período?

```
MTD Last Year = HL vendidos del 1 al 15 de mayo 2025

Ejemplo: 480 HL
```

Mismo corte, mismo canal, misma marca — pero del año anterior. Es tu **referencia histórica del mismo momento del mes**.

---

## Paso 3 — ¿Cuánto estás creciendo vs el año pasado? (Delta MTD)

```
Delta MTD vs LY = (500 − 480) / 480 = +4.2%
```

Esto responde: *"¿Estoy vendiendo más o menos que hace un año en este mismo punto del mes?"*

- **+4.2%** → vendes más que el año pasado al mismo corte
- **−3.0%** → vendes menos que el año pasado al mismo corte

---

## Paso 4 — ¿Cuánto vendiste el año pasado en TODO el mes?

```
LY FM ITM = HL vendidos en TODO mayo 2025 (mes completo)

Ejemplo: 1,000 HL
```

Aquí ya no es el corte al día 15 — es el **mes entero del año pasado**. Este dato es fijo y conocido.

---

## Paso 5 — ¿Cuánto dice el plan que debes vender este mes?

```
AP FM ITM = HL Plan de mayo 2026 (mes completo)

Ejemplo: 1,100 HL
```

Este es el objetivo mensual que se fijó en la planeación anual.

---

## Paso 6 — ¿Cuánto crecimiento exige el plan vs el año pasado? (Delta AP)

```
Delta AP vs LY = (1,100 − 1,000) / 1,000 = +10.0%
```

Esto responde: *"¿Qué tan ambicioso es el plan comparado con lo que se vendió el año pasado?"*

El plan pide crecer **10%** vs el mes completo del año pasado.

---

## Paso 7 — ¿Qué tan alineado estás con ese ritmo de crecimiento? (Gap)

```
Gap vs AP = Delta MTD vs LY − Delta AP vs LY
          = +4.2% − +10.0%
          = −5.8 pp
```

Esto responde: *"¿Estoy creciendo al ritmo que el plan exige, o por encima/debajo?"*

| Gap | Significado |
|---|---|
| **0 pp** | Vas exactamente al ritmo del plan |
| **+3 pp** | Estás creciendo 3 puntos más rápido de lo que el plan pedía |
| **−5.8 pp** | Estás creciendo 5.8 puntos más lento de lo que el plan pedía |

---

## ¿Por qué no comparar HL Real vs HL Plan directamente?

Porque el día 15 solo llevas la mitad del mes. Si comparas **500 HL reales vs 1,100 HL del plan**, siempre vas a parecer muy abajo — no porque vayas mal, sino porque el mes no ha terminado.

En cambio, este método compara **velocidades de crecimiento**:

```
¿A qué ritmo creces vs el año pasado?      → +4.2%
¿A qué ritmo el plan esperaba que crezcas? → +10.0%
¿Hay diferencia entre esos ritmos?         → −5.8 pp  ← el Gap real
```

Así, el corte al día 15 y el mes completo son comparables porque cada uno se mide contra su propio año anterior del mismo período.

---

## El caso DISCOUNTERS — por qué siempre muestra 0

El plan anual **no tiene segmento DISCOUNTERS** — ese canal se construye en Power BI reagrupando cadenas específicas (como OXXO, 7-Eleven, etc.) que en el plan original están dentro de otros canales. Como el plan no tiene ese desglose, no es posible calcular un Gap válido para DISCOUNTERS, y se muestra 0 para evitar engañar al usuario.

---

## Resumen visual

Imagina dos corredores en una carrera:

- **Corredor Real**: lleva 15 km de 31 km recorridos, corriendo a +4.2% más rápido que su propio récord personal en el mismo tramo.
- **Plan**: esperaba que corrieras a +10.0% más rápido que tu récord en la carrera completa.

El **Gap de −5.8 pp** dice: *"Estás corriendo más lento de lo que el plan preveía, aunque todavía llevas la mitad de la carrera."*

---

## Fórmulas DAX de referencia

```dax
Delta MTD ITM vs LY =
    IFERROR(
        CALCULATE(DIVIDE(([MTD Actual Year] - [MTD Last Year]), ABS([MTD Last Year]))),
        "-"
    )

Delta AP FM ITM vs LY =
    IFERROR(
        CALCULATE(DIVIDE(([AP FM ITM] - [LY FM ITM]), ABS([LY FM ITM]))),
        "-"
    )

Gap vs AP ITM =
VAR IsDiscounter = SELECTEDVALUE(Sales[canal_estrategico_desc]) = "DISCOUNTERS"
VAR TotalLY      = Sales[Delta MTD ITM vs LY]
VAR TotalAP      = Sales[Delta AP FM ITM vs LY]
RETURN
    IF(
        HASONEVALUE(Sales[canal_estrategico_desc]) && IsDiscounter,
        0,
        IF(ISERROR(TotalLY - TotalAP), "-", TotalLY - TotalAP)
    )
```
