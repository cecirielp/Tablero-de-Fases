# 📊 Tablero de Control de Fases Operativas y Cuellos de Botella (Qlik Sense)

Este repositorio contiene la documentación y estructura analítica de un cuadro de mando interactivo en Qlik Sense, diseñado para centralizar la operación logística de múltiples centros de distribución, medir los tiempos de estadía, auditar el cumplimiento de objetivos (SLA) y controlar las mermas por restos y remontes.

---

## 🖥️ Vista del Tablero: Detalle General

### 1. Estadía Promedio por Almacén
Permite monitorear la evolución diaria del tiempo de permanencia (Lead Time) de las unidades, agrupado e individualizado por Centro de Distribución (Burzaco, Tortuguitas, Vicente López, Paraná y Garín). Es clave para identificar picos de demoras e irregularidades operativas.

### 2. % Cumplimiento de Estadía (Auditoría de SLA)
Gráfico de barras apiladas que muestra la relación mensual entre los viajes que cumplen con la ventana horaria estipulada y los que no. 
* **Umbrales de SLA parametrizados dinámicamente:** Paraná/Vicente López/Burzaco $\le$ 1:00 Hs | Garín/Garín Non Food $\le$ 1:15 Hs.

### 3. Volumetría y Tipos de Viaje
Un análisis de distribución que cuantifica el volumen diario de actividad desglosado por la naturaleza de la carga (Ruta Seco, Normal con/sin Refri, Congelado, Refrigerado, FYV). Permite cruzar el impacto de la demanda contra los tiempos de respuesta de la operación.

### 4. Apertura y Seguimiento Secuencial (Fases)
Análisis de líneas enfocado en la **Fase 1** del flujo operativo, permitiendo aislar el comportamiento del paso inicial del proceso a nivel micro para detectar si el cuello de botella se origina en la recepción o en las primeras etapas de preparación.

---

## 📦 Módulo Especializado: Control de Restos y Remontes

Esta sección del dashboard está diseñada específicamente para auditar las ineficiencias en el proceso de consolidación de carga, analizando el impacto de los "restos" (mercadería que no logra ser consolidada en el viaje principal) sobre los tiempos de estadía y la frecuencia de remontes.

### 1. Distribución de Restos vs. Hojas de Carga (HDC)
Un análisis que cuantifica cuántas hojas de carga sufren la incidencia de restos dejados, permitiendo medir la severidad de la problemática por volumen de eventos.

### 2. Tendencia Semanal de Restos Dejados y Viajes Afectados
Monitoreo dinámico por año y semana que cruza la cantidad neta de unidades que quedan en el suelo contra el porcentaje total de viajes despachados que requirieron un proceso secundario de remonte.

### 3. Impacto de Restos en la Estadía Real
Gráfico combinado de doble eje que correlaciona de forma directa la cantidad de restos/remontes diarios con el tiempo de **Estadía Real** en el centro de distribución, demostrando visualmente cómo las fallas de consolidación incrementan los costos de permanencia.

### 4. Análisis de Restos por Hora de Carga
Un histograma de distribución horaria (0 a 23 hs) que identifica los picos críticos de generación de restos durante la jornada operativa. Es fundamental para determinar si las desviaciones se concentran en turnos específicos o en ventanas de alta saturación de los muelles de salida.

<img width="1346" height="524" alt="Restos" src="https://github.com/user-attachments/assets/b8ea1be8-317d-46a6-bfae-6831ae5222e5" />

---

## 📌 Introducción y Contexto del Negocio
En operaciones logísticas y de gestión de procesos complejas, los datos crudos de los sistemas transaccionales (como AS400 o ERPs tradicionales) suelen mostrar registros planos con marcas de tiempo. Esto dificulta que los coordinadores identifiquen de forma inmediata en qué etapa o fase del ciclo operativo se encuentran retenidos los pedidos, lotes o tareas.

Desarrollé esta herramienta con el objetivo de consolidar, secuenciar y medir el tiempo de permanencia de los flujos de trabajo de punta a punta, optimizando la toma de decisiones basada en datos y reduciendo los tiempos muertos en la cadena de suministro.

---

## 🛠️ Desafío Técnico y Modelo de Datos
El principal reto analítico radicaba en que los datos de origen no contaban con una estructura linealizada por fases. Para resolverlo, trabajé en las siguientes etapas dentro de Qlik Sense:

* **Modelado de Datos Asociativo:** Diseñé un modelo de datos en estrella vinculando tablas de movimientos históricos y estados actuales, evitando la creación de claves sintéticas (*synthetic keys*) mediante el uso de llaves compuestas e índices optimizados.
* **Lógica de Tiempos de Ciclo (Lead Time):** Implementé funciones en el *Data Load Script* para calcular la diferencia de tiempo exacta (días/horas/minutos) entre el ingreso y egreso de cada fase de forma individualizada.
* **Anonimización y Seguridad:** El dataset visible ha sido protegido mediante el enmascaramiento de datos confidenciales (indicadores de centros logísticos y fechas simuladas) para resguardar la privacidad de la operación real de la compañía.

---

## 🚀 Expresiones Avanzadas Utilizadas (Set Analysis)
Para lograr que los indicadores no se rompieran al aplicar filtros dinámicos y permitieran comparar el estado actual contra el histórico, desarrollé expresiones avanzadas utilizando **Set Analysis**.

*Ejemplo de cálculo dinámico para medir órdenes atrasadas en una fase específica ignorando selecciones de tiempo secundarias:*
```qlik
// Cuenta las órdenes cuya fecha de fase superó el tiempo límite estimado (SLA) para el mes en curso
Count({<[Estado Fase]={'Demorado'}, [Año Actual]={'$(=Max(Año))'}>} DISTINCT ID_Orden)
```

## 📈 Impacto y Resultados Operativos
Visibilidad de Extremo a Extremo: Se sustituyeron los reportes planos de texto por un embudo de fases interactivo, reduciendo el tiempo de detección de anomalías en el flujo operacional.

Detección de Cuellos de Botella: La combinación asociativa de Qlik permitió descubrir qué fases retenían la mayor parte del tiempo total del ciclo logístico.

Automatización del Reporte: Se eliminó la necesidad de procesar archivos manuales de forma diaria gracias a la carga programada y estructurada del modelo analítico.


