# 📘 README · Simulador ANSI/BICSI 002

## 🎯 Propósito del simulador

Este simulador educativo permite **visualizar y experimentar** el comportamiento de un centro de datos (Data Center) según los lineamientos de la norma **ANSI/BICSI 002**. Está diseñado para que operadores, estudiantes y profesionales comprendan:

- La relación entre **fallos técnicos** y **respuesta del operador**
- El impacto de **ignorar alertas** (mala práctica operativa)
- Los beneficios de **buenas prácticas** (escalar capacidad, restablecer sistema)
- La clasificación **Rating BICSI (F0–F4)** según disponibilidad del sistema

---

## 🖥️ Requisitos técnicos

| Requisito | Detalle |
|-----------|---------|
| **Navegador** | Moderno (Chrome, Edge, Firefox, Safari) |
| **JavaScript** | Activado (obligatorio) |
| **Conexión a internet** | Solo para cargar fuentes de Google Fonts (opcional, el diseño funciona sin ellas) |
| **Sistema operativo** | Cualquiera (Windows, macOS, Linux, móvil con orientación horizontal) |

No requiere instalación. Copia el código HTML en un archivo `.html` y ábrelo con el navegador.

---

## 🧩 Estructura de la interfaz

```
┌─────────────────────────────────────────────────────────────────┐
│  BARRA SUPERIOR · Estado del sistema + reloj                   │
├────────────────────────────────────┬────────────────────────────┤
│                                    │  📋 ALERTAS ACTIVAS        │
│  VISTA PRINCIPAL                   │  - Lista de eventos        │
│  - Temperatura (HVAC)              ├────────────────────────────┤
│  - CPU / Servidores                │  🎮 SIMULAR ESCENARIOS     │
│  - Tráfico de red / Latencia       │  - 6 botones de acción     │
│  - UPS / Red eléctrica             ├────────────────────────────┤
│  - Métricas: PUE, Uptime,          │  📘 CONTENIDO BICSI 002    │
│    Capacidad, Rating               │  - 5 bloques teóricos      │
│                                    ├────────────────────────────┤
│                                    │  📐 Nota de la norma       │
└────────────────────────────────────┴────────────────────────────┘
```

---

## 🎮 Guía de uso: Botones de simulación

### 1. 🌡 **Sobrecalentamiento (fallo HVAC)**
| Qué hace | Efecto visible |
|----------|----------------|
| Simula una falla en el sistema de climatización | Temperatura sube a 38°C (alerta amarilla → roja si se ignora) |

**¿Cuándo usarlo?** Para enseñar cómo el calor afecta al data center y la importancia del HVAC.

---

### 2. 📈 **Pico de tráfico (CPU/red alta)**
| Qué hace | Efecto visible |
|----------|----------------|
| Simula una demanda inesperada de procesamiento y red | CPU sube a 91%, ancho de banda a 8.5 Gb/s, latencia alta |

**¿Cuándo usarlo?** Para mostrar cómo la saturación de recursos degrada el rendimiento.

---

### 3. ⚡ **Fallo de red eléctrica**
| Qué hace | Efecto visible |
|----------|----------------|
| Corta el suministro eléctrico principal | UPS comienza a descargarse, generador arranca (simulado) |

**¿Cuándo usarlo?** Para explicar la función del UPS, generadores y la continuidad del servicio.

---

### 4. 📦 **Escalar capacidad (buena práctica)**
| Qué hace | Efecto visible |
|----------|----------------|
| Simula la instalación de nuevos racks y recursos | Capacidad usada baja ~8%, CPU objetivo sube ligeramente |

**¿Cuándo usarlo?** Para enseñar cómo **prevenir** la saturación mediante expansión planificada (Fase 3 de escalabilidad).

---

### 5. ⚠ **IGNORAR ALERTA ACTIVA** (¡Cuidado!)
| Condición | Qué hace |
|-----------|----------|
| **Si NO hay alerta activa** | Muestra mensaje: "No hay alertas activas para ignorar" |
| **Si hay alerta activa (1ª vez)** | Empeora el problema (temp→45°C, CPU→98%, o UPS baja 30%) |
| **Si hay alerta activa (2ª vez)** | **CRASH total del data center** (pantalla roja) |

**¿Cuándo usarlo?** **SOLO para demostrar las consecuencias de la negligencia operativa.** No debe usarse en un escenario real de aprendizaje como "buena práctica", sino como ejemplo de **qué NO hacer**.

---

### 6. ✅ **Restablecer sistema**
| Qué hace | Efecto visible |
|----------|----------------|
| Reinicia todas las métricas a valores normales | Temp 22°C, CPU 42%, UPS 98%, uptime 99.98%, elimina alertas |

**¿Cuándo usarlo?** Después de cualquier simulación para volver al estado inicial. También es el botón que aparece en la pantalla de crash para reiniciar.

---

## 📊 Interpretación de métricas en tiempo real

| Métrica | Rango normal | Alerta (warn) | Crítico (crit) | ¿Qué significa? |
|---------|--------------|---------------|----------------|-----------------|
| **Temperatura** | 18-27°C | 28-35°C | >35°C | Riesgo de fallo por calor |
| **CPU** | <70% | 70-85% | >85% | Servidores sobrecargados |
| **UPS** | >80% | 60-80% | <60% | Batería descargándose |
| **Uptime** | >99.9% | 99-99.9% | <99% | Disponibilidad baja |
| **PUE** | 1.2-1.5 | 1.5-1.8 | >1.8 | Ineficiencia energética |
| **Capacidad usada** | <70% | 70-85% | >85% | Necesidad de escalar |

---

## 🔄 Secuencias de aprendizaje recomendadas

### Secuencia 1: Respuesta correcta a una alerta
1. Presiona **"Sobrecalentamiento"** → temperatura sube a 38°C
2. Presiona **"Restablecer sistema"** → todo vuelve a la normalidad
3. **Conclusión:** El operador responde a tiempo y evita el crash.

### Secuencia 2: Consecuencia de ignorar alertas (¡NO hacer!)
1. Presiona **"Sobrecalentamiento"** → temperatura sube
2. Presiona **"Ignorar alerta activa" (1ª vez)** → temperatura sube a 45°C
3. Presiona **"Ignorar alerta activa" (2ª vez)** → **CRASH**
4. Presiona **"Reiniciar simulación"** en pantalla roja
5. **Conclusión:** Ignorar alertas mata el data center.

### Secuencia 3: Escalar capacidad como prevención
1. Presiona **"Pico de tráfico"** → CPU 91%, capacidad 63%
2. Presiona **"Escalar capacidad"** → capacidad baja a ~55%, CPU sube ligeramente
3. **Conclusión:** Expandir recursos evita la saturación.

### Secuencia 4: Fallo eléctrico + recuperación
1. Presiona **"Fallo de red eléctrica"** → red cortada, UPS empieza a bajar
2. Espera 3 segundos → generador "arranca"
3. Presiona **"Restablecer sistema"** → todo normal
4. **Conclusión:** Redundancia eléctrica (UPS + generador) garantiza continuidad.

---

## 🏆 El Rating BICSI (disponibilidad)

El simulador calcula automáticamente el **Rating** según el uptime actual:

| Uptime | Rating | Significado |
|--------|--------|-------------|
| <99.0% | Nivel 0 (F0) | Básico, sin redundancia |
| 99.0% - 99.9% | Nivel 1-2 (F1-F2) | Redundancia mínima o de componentes |
| 99.9% - 99.99% | Nivel 3 (F3) | Redundancia de sistemas (mantenimiento concurrente) |
| >99.99% | Nivel 4 (F4) | Tolerante a fallos (2N, sin puntos únicos de falla) |

---

## ❓ Preguntas frecuentes (FAQ)

### ¿Por qué "Ignorar alerta activa" no hace nada si no hay alertas?
Porque es **lógico**: no se puede ignorar algo que no existe. El simulador te lo indica con un mensaje informativo. Esto es **intencional** para enseñar que la negligencia solo es peligrosa cuando hay un problema real.

### ¿Cuánto tarda el generador en arrancar tras un fallo eléctrico?
En la simulación, **3 segundos**. En un data center real son entre 10 y 30 segundos, pero se comprime para que sea didáctico.

### ¿Qué pasa si el UPS llega a 0%?
El sistema colapsa con pantalla de crash porque no hay energía para los servidores.

### ¿Puedo volver atrás después de un crash?
Sí, presiona **"Reiniciar simulación"** en la pantalla roja. También puedes presionar "Restablecer sistema" en cualquier momento (excepto durante el crash).

### ¿Las alertas se acumulan? ¿Puedo tener dos problemas a la vez?
Técnicamente sí. Si activas "Sobrecalentamiento" y luego "Pico de tráfico", la última alerta reemplaza a la anterior en el estado `activeAlert`, pero los efectos combinados (temp alta + CPU alta) sí persisten.

---

## 🧑‍🏫 Para el profesor / presentación oral

Si vas a exponer este simulador, sigue esta estructura:

| Minuto | Qué hacer | Qué decir |
|--------|-----------|-----------|
| 0:00 - 0:30 | Mostrar panel lateral (5 bloques) | "Esto es lo que cubre ANSI/BICSI 002: desde clasificación hasta buenas prácticas" |
| 0:30 - 1:30 | Activar "Sobrecalentamiento" + Restablecer | "Un operador atento resuelve el problema de inmediato" |
| 1:30 - 2:30 | Activar "Sobrecalentamiento" + Ignorar (2 veces) | "Si ignora las alertas, el data center colapsa. La norma lo exige: responder es obligatorio" |
| 2:30 - 3:00 | Mostrar Rating BICSI cambiando | "El nivel de disponibilidad sube o baja según el uptime. Un banco necesita nivel 3 o 4" |

---

## 🐛 Solución de problemas

| Problema | Posible solución |
|----------|------------------|
| Los botones no responden | Recarga la página (F5). Asegúrate de que JavaScript esté activado. |
| Pantalla de crash sin motivo | Alguien pudo haber ignorado alertas antes. Presiona "Restablecer". |
| Las métricas no se actualizan | Espera 1-2 segundos (el tick es cada 1 segundo). Si no, recarga. |
| El generador no arranca | En "Fallo eléctrico", espera 3-4 segundos. Aparece un mensaje de confirmación. |

---

## 📁 Cómo obtener el código

1. Copia el código completo del simulador (el que te proporcioné en el mensaje anterior)
2. Pégalo en un bloc de notas o editor de texto (VS Code, Notepad++, Sublime Text)
3. Guarda el archivo con extensión `.html` (ejemplo: `simulador_bicsi.html`)
4. Abre el archivo con tu navegador web

---

## ✅ Resumen: Lo que el simulador te enseña

| Concepto | Cómo se enseña |
|----------|----------------|
| HVAC y temperatura | Escenario de "Sobrecalentamiento" |
| Saturación de CPU/red | Escenario de "Pico de tráfico" |
| Redundancia eléctrica | Escenario de "Fallo de red eléctrica" |
| Escalabilidad preventiva | Botón "Escalar capacidad" |
| Consecuencia de ignorar alertas | Botón "Ignorar alerta activa" (solo si hay alerta) |
| Recuperación | Botón "Restablecer sistema" |
| Rating BICSI (disponibilidad) | Se calcula automáticamente según uptime |
