# 📊 Tablero de Control de Fases Operativas y Cuellos de Botella (Qlik Sense)

## 📌 Introducción y Contexto del Negocio
En operaciones logísticas y de gestión de procesos complejas, los datos crudos de los sistemas transaccionales (como AS400 o ERPs tradicionales) suelen mostrar registros planos con marcas de tiempo. Esto dificulta que los coordinadores identifiquen de forma inmediata en qué etapa o fase del ciclo operativo se encuentran retenidos los pedidos, lotes o tareas.

Este proyecto consiste en el diseño e implementación de un **Tablero de Control de Fases** en Qlik Sense, desarrollado con el objetivo de consolidar, secuenciar y medir el tiempo de permanencia de los flujos de trabajo de punta a punta. La herramienta permite identificar cuellos de botella en tiempo real y optimizar la toma de decisiones operativas.

---

## 🛠️ Desafío Técnico y Modelo de Datos
El principal reto analítico radicaba en que los datos de origen no contaban con una estructura linealizada por fases. Para resolverlo, trabajé en las siguientes etapas dentro de Qlik Sense:

* **Modelado de Datos Asociativo:** Diseñé un modelo de datos en estrella vinculando tablas de movimientos históricos y estados actuales, evitando la creación de claves sintéticas (*synthetic keys*) mediante el uso de llaves compuestas e índices optimizados.
* **Lógica de Tiempos de Ciclo (Lead Time):** Implementé funciones en el *Data Load Script* para calcular la diferencia de tiempo exacta (días/horas/minutos) entre el ingreso y egreso de cada fase de forma individualizada.
* **Anonimización y Seguridad:** El dataset fue enmascarado en su totalidad mediante funciones de aleatorización en el script de carga para proteger la confidencialidad de la operación.

---

## 💡 KPIs Clave Implementados
El tablero se estructuró dividiendo las métricas principales en la parte superior del panel para una lectura rápida:

1. **Lead Time Total Promedio:** Tiempo medio que le toma a un elemento recorrer todas las fases desde el inicio hasta el cierre operativo.
2. **Volumen por Fase Activa:** Cantidad de órdenes o tareas retenidas actualmente en cada etapa para medir la carga de trabajo de los equipos individuales.
3. **Tasa de Desvío (SLA):** Porcentaje de procesos que excedieron el tiempo límite parametrizado para cada fase específica.

---

## 🚀 Expresiones Avanzadas Utilizadas (Set Analysis)
Para lograr que los indicadores no se rompieran al aplicar filtros dinámicos y permitieran comparar el estado actual contra el histórico, desarrollé expresiones avanzadas utilizando **Set Analysis**.

*Ejemplo de cálculo dinámico para medir órdenes atrasadas en una fase específica ignorando selecciones de tiempo secundarias:*
```qlik
// Cuenta las órdenes cuya fecha de fase superó el tiempo límite estimado (SLA) para el mes en curso
Count({<[Estado Fase]={'Demorado'}, [Año Actual]={'$(=Max(Año))'}>} DISTINCT ID_Orden)
