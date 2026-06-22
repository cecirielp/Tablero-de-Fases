📊 Tablero de Control de Fases Operativas y Cuellos de Botella (Qlik Sense)

Este repositorio contiene la documentación y estructura analítica de un cuadro de mando interactivo en Qlik Sense, diseñado para centralizar la operación logística de múltiples centros de distribución, medir los tiempos de estadía, auditar el cumplimiento de objetivos (SLA), controlar las mermas por restos y auditar viajes a nivel transaccional.

🖥️ Vista del Tablero: Detalle General

<img width="674" height="314" alt="1" src="https://github.com/user-attachments/assets/9ef6c452-b8a0-4ff2-b83d-4f4480f84447" />

<img width="520" height="325" alt="2" src="https://github.com/user-attachments/assets/e6607dc7-17bd-40a1-b2ad-cef8a78f232d" />

<img width="677" height="315" alt="3" src="https://github.com/user-attachments/assets/7b10645d-cf2a-4980-8d6d-de867fff192b" />

<img width="672" height="325" alt="4" src="https://github.com/user-attachments/assets/cc2f8af5-88f7-412f-9758-bf11946107d8" />





1. Estadía Promedio por Almacén

Permite monitorear la evolución diaria del tiempo de permanencia (Lead Time) de las unidades, agrupado e individualizado por Centro de Distribución (Burzaco, Tortuguitas, Vicente López, Paraná y Garín). Es clave para identificar picos de demoras e irregularidades operativas.

2. % Cumplimiento de Estadía (Auditoría de SLA)

Gráfico de barras apiladas que muestra la relación mensual entre los viajes que cumplen con la ventana horaria estipulada y los que no.

Umbrales de SLA parametrizados dinámicamente: Paraná/Vicente López/Burzaco $\le$ 1:00 Hs | Garín/Garín Non Food $\le$ 1:15 Hs.

3. Volumetría y Tipos de Viaje

Un análisis de distribución que cuantifica el volumen diario de actividad desglosado por la naturaleza de la carga (Ruta Seco, Normal con/sin Refri, Congelado, Refrigerado, FYV). Permite cruzar el impacto de la demanda contra los tiempos de respuesta de la operación.

4. Apertura Logística Inicial (Fase 1)

Análisis de líneas enfocado en aislar el comportamiento del paso inicial del proceso a nivel micro para detectar si el cuello de botella general se origina desde la primera etapa de recepción.

📦 Módulo Especializado: Control de Restos y Remontes

Esta sección del dashboard está diseñada específicamente para auditar las ineficiencias en el proceso de consolidación de carga, analizando el impacto de los "restos" (mercadería que no logra ser consolidada en el viaje principal) sobre los tiempos de estadía y la frecuencia de remontes.

1. Distribución de Restos vs. Hojas de Carga (HDC)

Un análisis que cuantifica cuántas hojas de carga sufren la incidencia de restos dejados, permitiendo medir la severidad de la problemática por volumen de eventos.

2. Tendencia Semanal de Restos Dejados y Viajes Afectados

Monitoreo dinámico por año y semana que cruza la cantidad neta de unidades que quedan en el suelo contra el porcentaje total de viajes despachados que requirieron un proceso secundario de remonte.

3. Impacto de Restos en la Estadía Real

Gráfico combinado de doble eje que correlaciona de forma directa la cantidad de restos/remontes diarios con el tiempo de Estadía Real en el centro de distribución, demostrando visualmente cómo las fallas de consolidación incrementan los costos de permanencia.

4. Análisis de Restos por Hora de Carga

Un histograma de distribución horaria (0 a 23 hs) que identifica los picos críticos de generación de restos durante la jornada operativa. Es fundamental para determinar si las desviaciones se concentran en turnos específicos o en ventanas de alta saturación de los muelles de salida.

🕒 Módulo Avanzado: Análisis de Estadía por Horas, Turnos y Fases de Expedición

Este panel analítico permite cruzar variables temporales críticas para identificar el rendimiento operativo y de personal a lo largo de la jornada. Al correlacionar el volumen de viajes con la estadía real por franja horaria y turno de trabajo, el negocio puede ajustar las capacidades de los muelles y optimizar las dotaciones en los pases de turno.

1. Estadía Dinámica por Hora y Turnos Operativos

Análisis Horario (0 a 17+ Hs): Gráfico combinado que expone las horas pico de congestión en los muelles y cómo impacta la saturación de la demanda en el Lead Time real dentro del centro logístico.

Métrica por Turno de Trabajo (1-N/N al 6-T/N): Vista consolidada para evaluar el desempeño e identificar desvíos analizando las dinámicas de equipos específicas y los pases de turno.

2. Apertura Micro-Secuencial (Auditoría de las 4 Fases de Expedición)

El núcleo del seguimiento del transporte se divide en un análisis modular que desglosa el Lead Time de las unidades a través de sus cuatro etapas consecutivas de expedición. Esta lógica permite cruzar datos transaccionales del camión con la lectura de bultos del sistema para aislar quirúrgicamente dónde se genera cada cuello de botella:

Fase 1 (Check-in a Asignación): Mide el tiempo transcurrido desde la llegada física del interno al Centro de Distribución hasta que se le asigna efectivamente su muelle y hoja de carga (HDC). Permite detectar demoras en la planificación de ingresos.

Fase 2 (Proceso de Carga - Picking/Estiba): Controla la ventana operativa de carga neta, cronometrando de forma exacta desde la lectura del primer formato hasta el último bulto consolidado arriba del camión.

Fase 3 (Cierre de Carga a Documentación): Registra el tiempo muerto que transcurre desde que el operario lee el último formato hasta que el equipo administrativo emite e imprime la documentación de tránsito obligatoria.

Fase 4 (Salida de CD): Monitorea el tramo final del ciclo, midiendo el tiempo que le toma al transportista retirar los papeles, preparar la unidad y cruzar la barrera de salida definitiva del predio.

🔍 Módulo de Auditoría Transaccional: Detalle de Viajes y Matriz de Alertas

Para dar soporte técnico a la operación diaria, el dashboard cuenta con una vista granular de máximo detalle (Drill-down). Esta matriz permite realizar auditorías exhaustivas sobre despachos individuales cruzando identificadores únicos como el Centro Logístico (Almacén), el número de transporte (Interno) y la Hoja de Carga.

Características Clave de la Herramienta:

Mapa de Calor Cromático (Semaforización): Implementación de formato condicional visual (Verde/Amarillo/Rojo) basado en las desviaciones de tiempo respecto al SLA objetivo. Permite aislar al instante la subfase crítica que penalizó la Estadía Real de un viaje específico.

Apertura de Subfases de Control: El reporte desglosa de manera minuciosa micro-etapas (como las subfases de carga intermedio 4.1 y 4.2), otorgando trazabilidad total sobre los tiempos administrativos y logísticos.

⚙️ Lógica Backend: Data Load Script (Qlik Script Automatizado)

A continuación se detalla el núcleo del script de extracción, transformación y carga (ETL) desarrollado en el editor de datos. El código consolida bases relacionales complejas y soluciona desafíos críticos de modelado:

Arquitectura Multi-Almacén: Implementación de un bucle dinámico (FOR EACH) que recorre los servidores de producción de los centros logísticos (509, 501, 503, 514, 504) e inyecta la información en un modelo unificado mediante sentencias CONCATENATE.

Algoritmo de Proximidad Temporal (Best Match Key): Creación de una lógica de validación cruzada (Almacen_Distancia_Validada) que calcula la diferencia absoluta (Fabs) entre las marcas de tiempo de las planificaciones (HDC_C) y los ingresos reales por portería (TsLlegada), purgando desvíos mayores a ventanas críticas de tolerancia.

Segmentación de Negocio Avanzada: Clasificación automatizada de tipos de viaje en base al mix de pallets validados por radiofrecuencia (Seco, FYV, Congelado, Refrigerado, Restos) y cálculo dinámico de fases mediante manipulación de intervalos temporales (Interval).

Prevención de Claves Sintéticas (Clean Data Model): Técnicas avanzadas de renombrado de campos en tablas satélites (como el módulo de choferes y la planilla de control de Drive) y el uso estratégico de MAPPING LOAD para inyectar datos evitando la redundancia y garantizando un modelo en estrella óptimo.

// =========================================================
// CONFIGURACIÓN GLOBAL
// =========================================================
SET TimestampFormat='DD/MM/YYYY hh:mm:ss';
SET DateFormat='DD/MM/YYYY';
SET TimeFormat='hh:mm:ss';

LET vFechaDesde = Year(Today()-240)*10000 + Month(Today()-240)*100 + Day(Today()-240);
LET vToleranciaHoras = ; 
LET vMargenAnticipada = 3/24; 

// =========================================================
// 1. EXTRACCIÓN SIAL (JORNADAS + MAESTROS DE IDENTIDAD)
// =========================================================
LIB CONNECT TO 'SIAL';

[chofer_maestro]:
SQL SELECT 
    ChoferHChoferId AS CHOFER_ID, 
    ChoferHNombre, 
    ChoferHApellido, 
    ChoferHDNI 
FROM sial.choferhistorico;

[chofer_asociar]:
LOAD 
    CHOFER_ID, 
    ChoferHNombre & ' ' & ChoferHApellido AS [Chofer del Viaje],
    ChoferHDNI AS [DNI Chofer]
RESIDENT [chofer_maestro];
DROP TABLE [chofer_maestro];

TempCitacion:
SQL SELECT 
    CitacionHFecha, 
    CitacionHFechaCreacion, 
    CitacionHAlmacenId, 
    CitacionHEmpresaId, 
    CitacionHNumero,
    CitacionId, 
    CitacionHId, 
    CitacionHTransporteId, 
    CitacionHObservaciones, 
    CitacionHSituacionId, 
    CitacionHTipoCamionId 
FROM sial.citacionhistorico 
WHERE CitacionHFecha >= DATE_SUB(CURDATE(), INTERVAL 240 DAY);

citacionhistorico:
LOAD 
    *, 
    Date(CitacionHFecha) as [FECHA CITA],
    Timestamp#(Date(Floor(CitacionHFechaCreacion - (3/24)), 'DD/MM/YY') & ' ' & Time(CitacionHFechaCreacion - (3/24), 'hh:mm:ss'), 'DD/MM/YYYY hh:mm:ss') AS ActualizadoTS 
RESIDENT TempCitacion;
DROP TABLE TempCitacion;

transporte: 
LOAD 
    TransporteId, 
    INTERNO_SIAL, 
    Patente_Temp AS [Patente SIAL],
    TransporteModifFecha, 
    CHOFER_ID;
SQL SELECT 
    TransporteId, 
    Trim(TransporteNumeroInterno) AS INTERNO_SIAL, 
    TransportePatente AS Patente_Temp, 
    TransporteModifFecha,
    TransporteChoferId AS CHOFER_ID 
FROM sial.transporte;

LEFT JOIN (citacionhistorico) 
LOAD 
    TransporteId AS CitacionHTransporteId, 
    INTERNO_SIAL, 
    TransporteModifFecha,
    [Patente SIAL],
    CHOFER_ID 
RESIDENT transporte; 
DROP TABLE transporte;

LEFT JOIN (citacionhistorico)
LOAD * RESIDENT [chofer_asociar];
DROP TABLE [chofer_asociar];

almacen: 
SQL SELECT AlmacenId, AlmacenNombre FROM sial.almacen;

LEFT JOIN (citacionhistorico) 
LOAD 
    AlmacenId AS CitacionHAlmacenId, 
    AlmacenNombre as Almacen_SIAL 
RESIDENT almacen; 
DROP TABLE almacen;

Historico_Seguro:
NOCONCATENATE LOAD
    [DNI Chofer],
    INTERNO_SIAL as [Interno_Historico],
    TransporteModifFecha as [Fecha_Desde]
RESIDENT citacionhistorico;

Llegadas_Temp: 
LOAD 
    CitacionId, 
    Min(If(CitacionHObservaciones='En almacén', ActualizadoTS)) AS TsLlegada 
RESIDENT citacionhistorico 
GROUP BY CitacionId;

LEFT JOIN (citacionhistorico) LOAD CitacionId, TsLlegada RESIDENT Llegadas_Temp; 
DROP TABLE Llegadas_Temp;

Salidas_Temp: 
LOAD 
    CitacionId, 
    Min(If(CitacionHObservaciones='En tránsito' AND ActualizadoTS > TsLlegada, ActualizadoTS)) AS TsSalida 
RESIDENT citacionhistorico 
WHERE IsNum(TsLlegada) 
GROUP BY CitacionId;

LEFT JOIN (citacionhistorico) LOAD CitacionId, TsSalida RESIDENT Salidas_Temp; 
DROP TABLE Salidas_Temp;

Jornadas_Final: 
LOAD DISTINCT 
    CitacionId, 
    INTERNO_SIAL as INTERNO, 
    [Patente SIAL],
    [Chofer del Viaje],
    [DNI Chofer],
    TransporteModifFecha,
    TsLlegada, 
    TsSalida as TsSalida_Real, 
    [FECHA CITA],
    CitacionHNumero,
    Upper(Trim(Almacen_SIAL)) as AlmacenKey
RESIDENT citacionhistorico;

DROP TABLE citacionhistorico;

// =========================================================
// 2. BUCLE DE ALMACENES (ARWH)
// =========================================================
FASE_Final_Acumulada:
LOAD * Inline [HOJA DE CARGA, INTERNO, Almacen, Chofer del Viaje, DNI Chofer, Patente SIAL, Tipo Viaje, TIME_HDC_ORIGINAL, TIMESTAMP_IMPRESION, HORA_IMPRESION_FMT, MIN_CARGA2, MAX_CARGA_TS, Y_ULT_ETQ, ETIQ_SECO_VAL, ETIQ_SECO_TOT, ETIQ_FYV_VAL, ETIQ_FYV_TOT, ETIQ_REFRI_VAL, ETIQ_REFRI_TOT, ETIQ_CONG_VAL, ETIQ_CONG_TOT, ETIQ_REMONTE_TOT, ETIQ_RESTO_TOT, ETIQ_RESTO_ANTES_HDC, ETIQ_RESTO_POST_HDC, CALLES_INVOLUCRADAS, Calle];

[Detalle_Etiquetas_Resto]:
LOAD * Inline [HOJA DE CARGA, N° Etiqueta Resto, Calle Resto, Timestamp Lectura Resto, Hora Lectura Resto, Momento de Lectura];

FOR EACH vAlm IN '509','501','503','514','504'
    LET vAlmNombre = Pick(Match('$(vAlm)','509','501','503','514','504'), 'PARANA', 'VICENTELOPEZ', 'BURZACO', 'GARIN', 'TORTUGUITASNONFOOD');
    LIB CONNECT TO 'ARWH$(vAlm)';
    
    TempDatos: 
    SQL SELECT DISTINCT TRIM(AMPDCC.CCTRS) AS "INTERNO", AMPDCC.CCHJC AS "HOJA DE CARGA", 
        AMPDCC.CCAHC, AMPDCC.CCMHC, AMPDCC.CCDHC, AMPDCC.CCHHC, AMPDCC.CCNHC, 
        AMETCC.ETACC, AMETCC.ETMCC, AMETCC.ETDCC, AMETCC.ETHCC, AMETCC.ETNCC, 
        AMPDCC.CCAAR, AMPDCC.CCMMR, AMPDCC.CCDDR, AMPDCC.CCHHR, AMPDCC.CCNNR, 
        AMPDCC.CCCLL, AMETCC.ETARS, AMPDCC.CCAAH, 
        AMETCC.ETEST, 
        COUNT(*) AS "QTY_ETIQ"
    FROM ALMA.AMPDCC AMPDCC JOIN ALMA.AMETCC AMETCC ON AMPDCC.CCPED = AMETCC.ETPED 
    WHERE LEFT(AMPDCC.CCPED, 1) = 'P' AND AMPDCC.CCTRS <> 0 
    AND (AMPDCC.CCAHC * 10000 + AMPDCC.CCMHC * 100 + AMPDCC.CCDHC) >= $(vFechaDesde) 
    GROUP BY TRIM(AMPDCC.CCTRS), AMPDCC.CCHJC, AMPDCC.CCAHC, AMPDCC.CCMHC, AMPDCC.CCDHC, AMPDCC.CCHHC, AMPDCC.CCNHC, AMETCC.ETACC, AMETCC.ETMCC, AMETCC.ETDCC, AMETCC.ETHCC, AMETCC.ETNCC, AMPDCC.CCAAR, AMPDCC.CCMMR, AMPDCC.CCDDR, AMPDCC.CCHHR, AMPDCC.CCNNR, AMPDCC.CCCLL, AMETCC.ETARS, AMPDCC.CCAAH, AMETCC.ETEST;

    CONCATENATE ([Detalle_Etiquetas_Resto])
    LOAD 
        [HOJA DE CARGA],
        AutoNumber([HOJA DE CARGA] & '-' & CCCLL & '-' & ETACC & '-' & ETNCC) as [N° Etiqueta Resto], 
        CCCLL as [Calle Resto],
        Timestamp#(ETACC & '-' & Right('0' & ETMCC,2) & '-' & Right('0' & ETDCC,2) & ' ' & Right('0' & ETHCC,2) & ':' & Right('0' & ETNCC,2), 'YYYY-MM-DD hh:mm') as [Timestamp Lectura Resto],
        Time(Frac(Timestamp#(ETACC & '-' & Right('0' & ETMCC,2) & '-' & Right('0' & ETDCC,2) & ' ' & Right('0' & ETHCC,2) & ':' & Right('0' & ETNCC,2), 'YYYY-MM-DD hh:mm')), 'hh:mm:ss') as [Hora Lectura Resto],
        If(Timestamp#(ETACC & '-' & Right('0' & ETMCC,2) & '-' & Right('0' & ETDCC,2) & ' ' & Right('0' & ETHCC,2) & ':' & Right('0' & ETNCC,2), 'YYYY-MM-DD hh:mm') <= Timestamp#(CCAHC & '-' & Right('0' & CCMHC,2) & '-' & Right('0' & CCDHC,2) & ' ' & Right('0' & CCHHC,2) & ':' & Right('0' & CCNHC,2), 'YYYY-MM-DD hh:mm'), 'Resto Anticipado a HDC', 'Resto Posterior a HDC') as [Momento de Lectura]
    RESIDENT TempDatos
    WHERE ETEST = '6';

    Almacen_Agrupado:
    LOAD 
        [HOJA DE CARGA], INTERNO,
        Timestamp#(CCAHC & '-' & Right('0' & CCMHC,2) & '-' & Right('0' & CCDHC,2) & ' ' & Right('0' & CCHHC,2) & ':' & Right('0' & CCNHC,2), 'YYYY-MM-DD hh:mm') AS TIME_HDC_ORIGINAL,
        If(CCAAR>0, Timestamp#(CCAAR & '-' & Right('0' & CCMMR,2) & '-' & Right('0' & CCDDR,2) & ' ' & Right('0' & CCHHR,2) & ':' & Right('0' & CCNNR,2), 'YYYY-MM-DD hh:mm')) AS TIMESTAMP_IMPRESION,
        If(CCAAR>0, Time#(Right('0' & CCHHR,2) & ':' & Right('0' & CCNNR,2), 'hh:mm:ss')) AS HORA_IMPRESION_FMT,

        Min(If(Timestamp#(ETACC & '-' & Right('0' & ETMCC,2) & '-' & Right('0' & ETDCC,2) & ' ' & Right('0' & ETHCC,2) & ':' & Right('0' & ETNCC,2), 'YYYY-MM-DD hh:mm') >= 
               Timestamp#(CCAHC & '-' & Right('0' & CCMHC,2) & '-' & Right('0' & CCDHC,2) & ' ' & Right('0' & CCHHC,2) & ':' & Right('0' & CCNHC,2), 'YYYY-MM-DD hh:mm'),
               Timestamp#(ETACC & '-' & Right('0' & ETMCC,2) & '-' & Right('0' & ETDCC,2) & ' ' & Right('0' & ETHCC,2) & ':' & Right('0' & ETNCC,2), 'YYYY-MM-DD hh:mm')
        )) AS MIN_CARGA2,

        Max(Timestamp#(ETACC & '-' & Right('0' & ETMCC,2) & '-' & Right('0' & ETDCC,2) & ' ' & Right('0' & ETHCC,2) & ':' & Right('0' & ETNCC,2), 'YYYY-MM-DD hh:mm')) AS MAX_CARGA_TS,
        Max(CCAAH) as Y_ULT_ETQ,

        Sum(If(NOT Match(ETEST, '4', '6') AND (($(vAlm)='504' AND Match(ETARS, '14', '07')) OR ($(vAlm)='514' AND Match(ETARS, '01', '14', '03', '13', '07', '91', '')) OR (Match($(vAlm), '501', '503', '509') AND Match(ETARS, '01', '14', '03', '13', ''))), If(ETACC > 0, QTY_ETIQ, 0), 0)) as ETIQ_SECO_VAL,
        Sum(If(NOT Match(ETEST, '4', '6') AND (($(vAlm)='504' AND Match(ETARS, '14', '07')) OR ($(vAlm)='514' AND Match(ETARS, '01', '14', '03', '13', '07', '91', '')) OR (Match($(vAlm), '501', '503', '509') AND Match(ETARS, '01', '14', '03', '13', ''))), QTY_ETIQ, 0)) as ETIQ_SECO_TOT,
        Sum(If(NOT Match(ETEST, '4', '6') AND (($(vAlm)='503' AND ETARS = '07') OR (Match($(vAlm), '501', '509') AND ETARS = '04')), If(ETACC > 0, QTY_ETIQ, 0), 0)) as ETIQ_FYV_VAL,
        Sum(If(NOT Match(ETEST, '4', '6') AND (($(vAlm)='503' AND ETARS = '07') OR (Match($(vAlm), '501', '509') AND ETARS = '04')), QTY_ETIQ, 0)) as ETIQ_FYV_TOT,
        Sum(If(NOT Match(ETEST, '4', '6') AND ETARS = '02' AND ETACC > 0, QTY_ETIQ, 0)) as ETIQ_REFRI_VAL,
        Sum(If(NOT Match(ETEST, '4', '6') AND ETARS = '02', QTY_ETIQ, 0)) as ETIQ_REFRI_TOT,
        Sum(If(NOT Match(ETEST, '4', '6') AND ETARS = '06' AND ETACC > 0, QTY_ETIQ, 0)) as ETIQ_CONG_VAL,
        Sum(If(NOT Match(ETEST, '4', '6') AND ETARS = '06', QTY_ETIQ, 0)) as ETIQ_CONG_TOT,
        Sum(If(ETEST = '4', QTY_ETIQ, 0)) as ETIQ_REMONTE_TOT,
        Sum(If(ETEST = '6', QTY_ETIQ, 0)) as ETIQ_RESTO_TOT,

        Sum(If(ETEST = '6' AND Timestamp#(ETACC & '-' & Right('0' & ETMCC,2) & '-' & Right('0' & ETDCC,2) & ' ' & Right('0' & ETHCC,2) & ':' & Right('0' & ETNCC,2), 'YYYY-MM-DD hh:mm') <= Timestamp#(CCAHC & '-' & Right('0' & CCMHC,2) & '-' & Right('0' & CCDHC,2) & ' ' & Right('0' & CCHHC,2) & ':' & Right('0' & CCNHC,2), 'YYYY-MM-DD hh:mm'), QTY_ETIQ, 0)) as ETIQ_RESTO_ANTES_HDC,
        Sum(If(ETEST = '6' AND Timestamp#(ETACC & '-' & Right('0' & ETMCC,2) & '-' & Right('0' & ETDCC,2) & ' ' & Right('0' & ETHCC,2) & ':' & Right('0' & ETNCC,2), 'YYYY-MM-DD hh:mm') > Timestamp#(CCAHC & '-' & Right('0' & CCMHC,2) & '-' & Right('0' & CCDHC,2) & ' ' & Right('0' & CCHHC,2) & ':' & Right('0' & CCNHC,2), 'YYYY-MM-DD hh:mm'), QTY_ETIQ, 0)) as ETIQ_RESTO_POST_HDC,

        Concat(DISTINCT CCCLL, ', ') AS CALLES_INVOLUCRADAS,
        Min(Num(KeepChar(CCCLL, '0123456789'))) AS Calle,
        '$(vAlmNombre)' AS Almacen
    RESIDENT TempDatos GROUP BY [HOJA DE CARGA], INTERNO, CCAHC, CCMHC, CCDHC, CCHHC, CCNHC, CCAAR, CCMMR, CCDDR, CCHHR, CCNNR;
    DROP TABLE TempDatos;

    Almacen_PreMatch:
    NOCONCATENATE LOAD *,
        If(IsNull(TIMESTAMP_IMPRESION), 'No', 'Si') AS Flag_Impreso,
        If(Fabs(TIMESTAMP_IMPRESION - TIME_HDC_ORIGINAL) > 0.5, 
            If(TIMESTAMP_IMPRESION < TIME_HDC_ORIGINAL, TIME_HDC_ORIGINAL - 1, TIME_HDC_ORIGINAL + 1), TIME_HDC_ORIGINAL) AS [HDC_C],
        If(ETIQ_RESTO_TOT > 0 AND ETIQ_SECO_TOT = 0 AND ETIQ_FYV_TOT = 0 AND ETIQ_REFRI_TOT = 0 AND ETIQ_CONG_TOT = 0 AND ETIQ_REMONTE_TOT = 0, 'Ruta Restos',
        If(ETIQ_FYV_TOT > 0 AND ETIQ_SECO_TOT = 0 AND ETIQ_REFRI_TOT = 0 AND ETIQ_CONG_TOT = 0, 'Ruta FYV',
        If(ETIQ_CONG_TOT > 0 AND ETIQ_SECO_TOT = 0 AND ETIQ_FYV_TOT = 0 AND ETIQ_REFRI_TOT = 0, 'Ruta Congelado',
        If(ETIQ_REFRI_TOT > 0 AND ETIQ_SECO_TOT = 0 AND ETIQ_FYV_TOT = 0 AND ETIQ_CONG_TOT = 0, 'Ruta Refrigerado',
        If(ETIQ_SECO_TOT > 0 AND ETIQ_FYV_TOT = 0 AND ETIQ_REFRI_TOT = 0 AND ETIQ_CONG_TOT = 0, 'Ruta Seco', 
        If(ETIQ_REFRI_TOT > 0, 'Normal con Refri', 'Normal sin Refri')))))) AS [Tipo Viaje]
    RESIDENT Almacen_Agrupado;
    DROP TABLE Almacen_Agrupado;

    Almacen_Distancia_Full:
    NOCONCATENATE LOAD * RESIDENT Almacen_PreMatch;
    LEFT JOIN (Almacen_Distancia_Full) LOAD * RESIDENT Jornadas_Final WHERE AlmacenKey = '$(vAlmNombre)';

    Almacen_Distancia_Validada:
    NOCONCATENATE LOAD *, 
        If(IsNum(TsLlegada), 
            If(TsLlegada > [HDC_C] AND (TsLlegada - [HDC_C]) > $(vMargenAnticipada), 99, 
                If(Fabs([HDC_C] - TsLlegada) > (3/24), 99, Fabs([HDC_C] - TsLlegada))
            )
        , 99) as Dif_Num 
    RESIDENT Almacen_Distancia_Full; DROP TABLE Almacen_Distancia_Full;

    Mejor_Match_Key:
    NOCONCATENATE LOAD [HOJA DE CARGA], Min(Dif_Num) as Min_Dif RESIDENT Almacen_Distancia_Validada GROUP BY [HOJA DE CARGA];

    Almacen_Final_Loop:
    NOCONCATENATE LOAD * RESIDENT Almacen_PreMatch;
    LEFT JOIN (Almacen_Final_Loop) LOAD * RESIDENT Almacen_Distancia_Validada;
    INNER JOIN (Almacen_Final_Loop) LOAD [HOJA DE CARGA], Min_Dif as Dif_Num RESIDENT Mejor_Match_Key;

    Final_Loop_Limpio:
    NOCONCATENATE LOAD *,
        If(Dif_Num = 99, Null(), TsLlegada) as TsLlegada_OK,
        If(Dif_Num = 99, Null(), TsSalida_Real) as TsSalida_OK,
        If(Dif_Num = 99, Null(), CitacionId) as CitacionId_OK,
        If(Dif_Num = 99, Null(), CitacionHNumero) as CitacionHNumero_OK
    RESIDENT Almacen_Final_Loop;

CONCATENATE (FASE_Final_Acumulada) 
    LOAD 
        [HOJA DE CARGA], INTERNO, Almacen, 
        [Chofer del Viaje], [DNI Chofer], [Patente SIAL],TransporteModifFecha,
        TIME_HDC_ORIGINAL, TIMESTAMP_IMPRESION, HORA_IMPRESION_FMT,
        MIN_CARGA2, MAX_CARGA_TS, Y_ULT_ETQ, CALLES_INVOLUCRADAS, Calle,
        ETIQ_SECO_VAL, ETIQ_SECO_TOT, ETIQ_FYV_VAL, ETIQ_FYV_TOT, 
        ETIQ_REFRI_VAL, ETIQ_REFRI_TOT, ETIQ_CONG_VAL, ETIQ_CONG_TOT,
        ETIQ_REMONTE_TOT, ETIQ_RESTO_TOT, ETIQ_RESTO_ANTES_HDC, ETIQ_RESTO_POST_HDC,
        Flag_Impreso, [HDC_C], Dif_Num, CitacionHNumero,
        TsLlegada_OK as TsLlegada, TsSalida_OK as TsSalida_Real, CitacionId_OK as CitacionId,
        [Tipo Viaje]
    RESIDENT Final_Loop_Limpio;
    
    DROP TABLES Almacen_Distancia_Validada, Mejor_Match_Key, Almacen_Final_Loop, Final_Loop_Limpio, Almacen_PreMatch;
NEXT
DROP TABLE Jornadas_Final;

// =========================================================
// 3. BLOQUE FINAL: CONSOLIDACIÓN Y LIMPIEZA DE DATOS
// =========================================================

FASE_Unificada:
NOCONCATENATE LOAD 
    *,
    If(IsNull(TsLlegada) OR Len(Trim(TsLlegada)) = 0 OR Dif_Num >= 99, Null(), CitacionHNumero) as CitacionHNumero_Limpia
RESIDENT FASE_Final_Acumulada 
WHERE INTERNO <> '1333' AND (ETIQ_SECO_TOT + ETIQ_REFRI_TOT + ETIQ_CONG_TOT + ETIQ_FYV_TOT + ETIQ_REMONTE_TOT + ETIQ_RESTO_TOT) > 0; 

DROP TABLE FASE_Final_Acumulada;

FASE_Limpieza_Dups:
NOCONCATENATE LOAD DISTINCT
    [HOJA DE CARGA], INTERNO, Almacen, [Chofer del Viaje], TransporteModifFecha, [DNI Chofer], [Patente SIAL],
    TsSalida_Real, TsLlegada, TIMESTAMP_IMPRESION, TIME_HDC_ORIGINAL, Flag_Impreso,
    MIN_CARGA2, MAX_CARGA_TS, Y_ULT_ETQ, [HDC_C], Dif_Num, HORA_IMPRESION_FMT, CALLES_INVOLUCRADAS, Calle, 
    CitacionHNumero_Limpia as CitacionHNumero,
    ETIQ_SECO_VAL, ETIQ_SECO_TOT, ETIQ_FYV_VAL, ETIQ_FYV_TOT, ETIQ_REFRI_VAL, ETIQ_REFRI_TOT, ETIQ_CONG_VAL, ETIQ_CONG_TOT,
    ETIQ_REMONTE_TOT, ETIQ_RESTO_TOT, ETIQ_RESTO_ANTES_HDC, ETIQ_RESTO_POST_HDC, [Tipo Viaje]
RESIDENT FASE_Limpieza_Dups;

DROP TABLE FASE_Limpieza_Dups;

FASE_Pre_Ranking:
NOCONCATENATE LOAD * RESIDENT FASE_Limpieza_Dups ORDER BY INTERNO ASC, [HDC_C] ASC;
DROP TABLE FASE_Limpieza_Dups;

FASE_Ranking:
NOCONCATENATE LOAD
    *,
    If(INTERNO = Peek(INTERNO) AND [HOJA DE CARGA] <> Peek([HOJA DE CARGA]) AND ( [HDC_C] - Peek([HDC_C]) ) <= (1/24), 
        RangeSum(Peek('Rank_Cita'), 1), 1) as Rank_Cita
RESIDENT FASE_Ranking;

DROP TABLE FASE_Pre_Ranking;

FASE_Final_Pre_Controles:
NOCONCATENATE LOAD
    *,
    If(Rank_Cita > 1, 'Múltiple HDC', If(IsNull(CitacionHNumero), 'Sin citación', If(TsLlegada > [HDC_C], 'HDC Anticipada', 'OK'))) AS [Control entrada],
    If(IsNum(TsSalida_Real), If((TsSalida_Real - [HDC_C]) > (12/24) OR (TsSalida_Real < TIMESTAMP_IMPRESION), 'Salida Cancelada', 'Despachado'), If((Now() - [HDC_C]) >= 0.5, 'Sin salida Sial', 'No Despachado')) AS [Control Salida],
    If(ETIQ_REMONTE_TOT > 0, 'Si', 'No') as [Tiene Remonte],
    If(ETIQ_RESTO_TOT > 0, 'Si', 'No') as [Tiene Restos],
    If(IsNum(TIMESTAMP_IMPRESION) and IsNum(TIME_HDC_ORIGINAL), If(Fabs(TIMESTAMP_IMPRESION - TIME_HDC_ORIGINAL) > 1, 'Si', 'No'), 'Sin Datos') AS [Error as400]
RESIDENT FASE_Ranking;

DROP TABLE FASE_Ranking;

FASE_Final_Motor:
NOCONCATENATE LOAD
    *, 
    CitacionHNumero AS [Número Citación],
    Hour([HDC_C]) AS [Hora], 
    If(IsNum(MIN_CARGA2) AND IsNum([HDC_C]), If(MIN_CARGA2 < [HDC_C], Time(0, 'hh:mm:ss'), Interval(MIN_CARGA2 - [HDC_C], 'hh:mm:ss')), Time(0, 'hh:mm:ss')) AS [Fase 2_Calculada],
    If([Control Salida] = 'No Despachado', If([Control entrada] = 'HDC Anticipada', (Now() - [HDC_C]), (Now() - TsLlegada)), If([Control Salida] = 'Despachado', If([Control entrada] = 'HDC Anticipada', (TsSalida_Real - [HDC_C]), (TsSalida_Real - TsLlegada)), 0)) AS [_Estadia_Calculo],
    If(Hour([HDC_C]) >= 6 AND Hour([HDC_C]) < 14, 'Mañana', If(Hour([HDC_C]) >= 14 AND Hour([HDC_C]) < 22, 'Tarde', 'Noche')) AS [Turno HDC],
    If(Match([Control Salida], 'No Despachado', 'Sin salida Sial'), If(Hour(Now()) >= 6 AND Hour(Now()) < 14, 'Mañana', If(Hour(Now()) >= 14 AND Hour(Now()) < 22, 'Tarde', 'Noche')), If(Hour(TsSalida_Real) >= 6 AND Hour(TsSalida_Real) < 14, 'Mañana', If(Hour(TsSalida_Real) >= 14 AND Hour(TsSalida_Real) < 22, 'Tarde', 'Noche'))) AS [Turno Egreso]
RESIDENT FASE_Final_Pre_Controles;

DROP TABLE FASE_Final_Pre_Controles; 

Tablero_Logistico:
NOCONCATENATE LOAD
    [HOJA DE CARGA], INTERNO, Almacen, [Chofer del Viaje], [DNI Chofer], TransporteModifFecha, [Patente SIAL],
    TsSalida_Real, TsLlegada, TIMESTAMP_IMPRESION, TIME_HDC_ORIGINAL, Flag_Impreso, 
    MIN_CARGA2, MAX_CARGA_TS, Y_ULT_ETQ, [HDC_C], Dif_Num, HORA_IMPRESION_FMT,
    CALLES_INVOLUCRADAS, Calle, CitacionHNumero, [Número Citación], [Control entrada], [Control Salida],
    [Turno HDC], [Turno Egreso], [Hora], [Fase 2_Calculada], [Tipo Viaje],

    If([Turno HDC] <> [Turno Egreso], 'Si', 'No') AS [Pase de Turno],
    If([Turno HDC] <> [Turno Egreso] AND [_Estadia_Calculo] > (1.5 / 24), 'Si', 'No') AS [Demora en Pase de Turno],
    Pick(Match(Left([Turno HDC], 1) & '/' & Left([Turno Egreso], 1), 'N/N', 'N/M', 'M/M', 'M/T', 'T/T', 'T/N'), '1-N/N', '2-N/M', '3-M/M', '4-M/T', '5-T/T', '6-T/N') AS [Turnos],

    Date(Floor([HDC_C] + (2/24)), 'DD/MM/YYYY') AS [Fecha], 
    Date(Floor([HDC_C] + (2/24)), 'DD/MM/YYYY') AS [Fecha Operativa], 
    Year(Floor([HDC_C] + (2/24))) AS [Año], 
    Month(Floor([HDC_C] + (2/24))) AS [Mes], 
    Week(Floor([HDC_C] + (2/24))) AS [Semana],
    Year(Floor([HDC_C] + (2/24))) & Num(Week(Floor([HDC_C] + (2/24))), '00') AS [SemAño],
    Year([HDC_C])&Num(Month([HDC_C]),'00') AS [MesAño],
    
    If(Match([Control entrada], 'Sin citación', 'Excluir', 'Múltiple HDC'), Null(), Time(TsLlegada, 'hh:mm:ss')) AS [Hora En almacen],
    If(Match([Control entrada], 'Sin citación', 'Excluir', 'Múltiple HDC'), Null(), Time(TsSalida_Real, 'hh:mm:ss')) AS [Egreso Sial],
    If(Match([Control entrada], 'Sin citación', 'Excluir', 'Múltiple HDC'), Null(), Timestamp(TsSalida_Real, 'DD/MM/YYYY hh:mm:ss')) AS [Egreso],
    If(IsNum(TsSalida_Real) AND TsSalida_Real >= TsLlegada, Interval(TsSalida_Real - TsLlegada, 'hh:mm:ss'), 'Sin salida') AS [Estadia Sial],
    Time(TsLlegada, 'hh:mm:ss') AS [Ingreso Sial],
    If(Hour([HDC_C]) >= 6 AND Hour([HDC_C]) < 14, 'Mañana', If(Hour([HDC_C]) >= 14 AND Hour([HDC_C]) < 22, 'Tarde', 'Noche')) AS [Turno],
    
    Time(TIME_HDC_ORIGINAL, 'hh:mm:ss') AS [Hora entrega HDC],
    Time([HDC_C], 'hh:mm:ss') AS [Entrega Hoja de Carga],
    If(IsNum(TIMESTAMP_IMPRESION) AND IsNum(TIME_HDC_ORIGINAL), Interval(TIMESTAMP_IMPRESION - TIME_HDC_ORIGINAL, 'hh:mm:ss'), 'Sin datos') AS [Desde Entrega de Hoja de Carga hasta Hoja de Reparto],
    Interval([_Estadia_Calculo], 'hh:mm:ss') AS [Estadia Real],
    Timestamp([HDC_C], 'DD/MM/YYYY hh:mm:ss') AS [TIME_HDC],
    Time(MIN_CARGA2, 'hh:mm:ss') AS [Confirmación de 1ra Etiqueta],
    Time(MAX_CARGA_TS, 'hh:mm:ss') AS [Finalización de Carga],
    Time(Alt(HORA_IMPRESION_FMT, Frac(TIMESTAMP_IMPRESION)), 'hh:mm:ss') AS [Hoja de Ruta],

    Hour(TIME_HDC_ORIGINAL) AS [Hora HDC],
    Hour(MIN_CARGA2) AS [Hora Confirmación 1ra etiqueta],
    Hour(MAX_CARGA_TS) AS [Hora Finalización de Carga],
    Hour(Alt(HORA_IMPRESION_FMT, Frac(TIMESTAMP_IMPRESION))) AS [Hora Impresión Hoja de Ruta],

    Timestamp(MIN_CARGA2, 'DD/MM/YYYY hh:mm:ss') as [Dato Mínimo Confirmación Etiqueta],
    Timestamp(MAX_CARGA_TS, 'DD/MM/YYYY hh:mm:ss') as [Dato Máximo Confirmación Última Etiqueta],

    Interval(fabs([HDC_C] - TsLlegada), 'hh:mm:ss') AS [Fase 1.2],
    If(IsNum(TsLlegada), If(TsLlegada > [HDC_C] AND (TsLlegada - [HDC_C]) <= (15/1440), Interval(0, 'hh:mm:ss'), Interval([HDC_C] - TsLlegada, 'hh:mm:ss')), Null()) AS [Fase 1],
    If(IsNum(MIN_CARGA2) AND IsNum([HDC_C]), Interval(MIN_CARGA2 - [HDC_C], 'hh:mm:ss'), Time(0, 'hh:mm:ss')) AS [Fase 2], 
    Interval(MAX_CARGA_TS - MIN_CARGA2, 'hh:mm:ss') AS [Fase 3],
    If(Flag_Impreso = 'Si', Interval( (If(Y_ULT_ETQ <> 0, If(Fabs(TIMESTAMP_IMPRESION - MAX_CARGA_TS) > 0.4, 0, If(TIMESTAMP_IMPRESION < MAX_CARGA_TS, (TIMESTAMP_IMPRESION + 1) - MAX_CARGA_TS, TIMESTAMP_IMPRESION - MAX_CARGA_TS)), 0)) + (If(IsNum(TsSalida_Real), If(TsSalida_Real < TIMESTAMP_IMPRESION, (TsSalida_Real + 1) - TIMESTAMP_IMPRESION, TsSalida_Real - TIMESTAMP_IMPRESION), 0)), 'hh:mm:ss'), Interval('00:00:00', 'hh:mm:ss')) AS [Fase 4],
    If(IsNum(TIMESTAMP_IMPRESION) AND IsNum(MAX_CARGA_TS), Interval(TIMESTAMP_IMPRESION - MAX_CARGA_TS, 'hh:mm:ss'), Time(0, 'hh:mm:ss')) AS [Fase 4.1],
    If(IsNum(TsSalida_Real) AND Flag_Impreso = 'Si', Interval(TsSalida_Real - TIMESTAMP_IMPRESION, 'hh:mm:ss'), Interval('00:00:00', 'hh:mm:ss')) AS [Fase 4.2],

    If(TIME_HDC_ORIGINAL > TIMESTAMP_IMPRESION, 'Error: HDC post Impresión', If((MIN_CARGA2 - [HDC_C]) < 0, 'Error: Carga anterior a HDC', If(Fabs(MIN_CARGA2 - [HDC_C]) > 0.4, 'Error: Salto Horario Irreal', If(IsNull(MIN_CARGA2) AND (ETIQ_SECO_TOT + ETIQ_FYV_TOT + ETIQ_CONG_TOT) > 0, 'Error: Sin marcas de RF', 'OK') ) ) ) AS [Estado Datos HDC],
    
    If((ETIQ_SECO_TOT + ETIQ_REFRI_TOT + ETIQ_CONG_TOT + ETIQ_FYV_TOT + ETIQ_REMONTE_TOT + ETIQ_RESTO_TOT) = 0, 'No ok',
        If((([Control entrada] = 'OK') OR ([Control entrada] = 'HDC Anticipada' AND (TsLlegada - [HDC_C]) <= (15/1440))) AND [Control Salida] = 'Despachado' AND (TIME_HDC_ORIGINAL <= TIMESTAMP_IMPRESION) AND (MIN_CARGA2 >= [HDC_C]) AND IsNum(MIN_CARGA2), 'OK', 'No ok')
    ) AS Muestras,
    
    If([_Estadia_Calculo] > (2.5/24) AND [_Estadia_Calculo] <= (3/24), 'Si', 'No') AS [Estadia 2:30-3:00 hs],
    If([_Estadia_Calculo] > (3/24), 'Si', 'No') AS [Estadia > 3 hs],
   
    ETIQ_SECO_VAL  & '/' & ETIQ_SECO_TOT  as [SECO], 
    ETIQ_FYV_VAL   & '/' & ETIQ_FYV_TOT   as [FYV], 
    ETIQ_REFRI_VAL & '/' & ETIQ_REFRI_TOT as [REFRIGERADO],
    ETIQ_CONG_VAL  & '/' & ETIQ_CONG_TOT  as [CONGELADO],
    
    ETIQ_REMONTE_TOT as [Cant Remonte],
    ETIQ_RESTO_TOT   as [Restos dejados],
    
    ETIQ_RESTO_ANTES_HDC as [Restos Antes de HDC],
    ETIQ_RESTO_POST_HDC as [Restos Después de HDC],
    
    If(ETIQ_RESTO_TOT = 0, 'Sin Restos',
        If(ETIQ_RESTO_POST_HDC > 0 AND ETIQ_RESTO_ANTES_HDC > 0, 'Resto Mixto',
        If(ETIQ_RESTO_POST_HDC > 0, 'Resto Posterior a HDC', 'Resto Anticipado a HDC'))
    ) AS [Control Resto Viaje],
    
    If(ETIQ_REMONTE_TOT > 0, 'SI', 'NO') as [Dejo Remonte],
    If(ETIQ_RESTO_TOT > 0, 'SI', 'NO')   as [Tiene Resto],
    If(ETIQ_REMONTE_TOT > 0, 1, 0) as [Qty Remonte],
    If(ETIQ_RESTO_TOT > 0, 1, 0)   as [Qty Resto],
    
    (ETIQ_SECO_TOT + ETIQ_REFRI_TOT + ETIQ_CONG_TOT + ETIQ_FYV_TOT + ETIQ_REMONTE_TOT + ETIQ_RESTO_TOT) as [Cant Total etiquetas],   
    ETIQ_SECO_TOT + ETIQ_REFRI_TOT + ETIQ_CONG_TOT + ETIQ_FYV_TOT + ETIQ_REMONTE_TOT + ETIQ_RESTO_TOT as [Cant Total]
RESIDENT FASE_Final_Motor;

DROP TABLE FASE_Final_Motor;

// =========================================================
// 5. ANÁLISIS DE PRODUCTIVIDAD POR CHOFER (Campos renombrados para evitar SYN 2)
// =========================================================
Analisis_Choferes:
NOCONCATENATE LOAD
    [Fecha Operativa] as [Bodega_Fecha_Operativa], 
    [Chofer del Viaje] as [Bodega_Chofer], 
    [DNI Chofer] as [Bodega_DNI_Chofer],
    Count(DISTINCT INTERNO) as [Cant Internos x Día],
    Sum([Cant Total etiquetas]) as [Total Etiquetas x Día],
    Concat(DISTINCT INTERNO, ' / ') as [Internos Operados]
RESIDENT Tablero_Logistico
GROUP BY [Fecha Operativa], [Chofer del Viaje], [DNI Chofer];

TRACE ▶ Análisis de choferes cargado correctamente sin generar claves sintéticas.;

LIB CONNECT TO 'GOOGLE_DRIVE_CONECTOR';

// =========================================================
// 6. CARGA DE INFORMACIÓN: INTERNOS - BODEGA (GOOGLE DRIVE)
// =========================================================
Internos_Bodega_Sico:
NOCONCATENATE LOAD 
    Date(Date#(FECHA, 'DD/MM/YYYY'), 'DD/MM/YYYY') as [Bodega_FECHA], 
    INTERNOS as [Bodega_INTERNOS], 
    [SURTIDO 1] as [Bodega_SURTIDO_1], 
    [PLAN DE CARGA N° CONFIRMACION 1] as [Bodega_PLAN_DE_CARGA_1], 
    [SURTIDO 2] as [Bodega_SURTIDO_2], 
    [PLAN DE CARGA N° CONFIRMACION 2] as [Bodega_PLAN_DE_CARGA_2], 
    CD as [Bodega_CD];
SELECT 
    FECHA, INTERNOS, [SURTIDO 1], [PLAN DE CARGA N° CONFIRMACION 1], [SURTIDO 2], [PLAN DE CARGA N° CONFIRMACION 2], CD
FROM GetSheetValues
WITH PROPERTIES (
    spreadsheetKey='121OuVKZyfJDL9mh1rEPQtGiSIgDrfjErWRQfyAAJeHU',
    range='BODEGA',
    valueRenderOption='FORMATTED_VALUE',
    dateTimeRenderOption='FORMATTED_STRING',
    generatedNumberedColumns='false',
    skipRows=''
);

TRACE ▶ Bloque 6 finalizado con éxito: Datos de Drive leídos en memoria.;

// =========================================================
// 7. TABLA SATÉLITE - VINCULACIÓN DE ESTADÍA DESDE SIAL (PLAN 2)
// =========================================================

LET vEstadiaSIALCol = '';

FOR i = 1 TO NoOfFields('Tablero_Logistico')
    LET vNomCol = FieldName($(i), 'Tablero_Logistico');
    IF WildMatch(Lower('$(vNomCol)'), '*estad*') THEN
        LET vEstadiaSIALCol = vNomCol;
    END IF;
NEXT i;

IF Len('$(vEstadiaSIALCol)') > 0 THEN
    TRACE ▶ COLUMNA ENCONTRADA EN SIAL: [$(vEstadiaSIALCol)];
    
    Mapa_Estadia_SIAL:
    MAPPING LOAD
        [HOJA DE CARGA],
        [$(vEstadiaSIALCol)]
    RESIDENT Tablero_Logistico
    WHERE Len([HOJA DE CARGA]) > 0;
ELSE
    TRACE ▶ ADVERTENCIA: No se encontró campo de Estadía en Tablero_Logistico.;
END IF;

Control_Bodega_Sico:
NOCONCATENATE LOAD
    [Bodega_PLAN_DE_CARGA_2] as [HOJA DE CARGA], 
    [Bodega_INTERNOS]        as [Interno bodega],
    [Bodega_PLAN_DE_CARGA_1] as [Plan_De_Carga_1],
    [Bodega_PLAN_DE_CARGA_2] as [Plan_De_Carga_2],
    [Bodega_FECHA]           as [Fecha_De_Bodega_Final],
    [Bodega_CD]              as [CD_Bodega_Final],
    [Bodega_SURTIDO_1]       as [Surtido_Plan_1],
    [Bodega_SURTIDO_2]       as [Surtido_Plan_2],
    'SI'                     as [Bodega],
    'SI'                     as [Control_Bodega_Filtro]
RESIDENT Internos_Bodega_Sico 
WHERE Len([Bodega_PLAN_DE_CARGA_2]) > 0;

DROP TABLE Internos_Bodega_Sico;
SET vEstadiaSIALCol = ;
SET vNomCol = ;

TRACE ▶ Bloque 7 finalizado con éxito: Todo el modelo integrado limpio y optimizado.;


📌 Introducción y Contexto del Negocio

En operaciones logísticas y de gestión de procesos complejas, los datos crudos de los sistemas transaccionales (como AS400 o ERPs tradicionales) suelen mostrar registros planos con marcas de tiempo. Esto dificulta que los coordinadores identifiquen de forma inmediata en qué etapa o fase del ciclo operativo se encuentran retenidos los pedidos, lotes o tareas.

Desarrollé esta herramienta con el objetivo de consolidar, secuenciar y medir el tiempo de permanencia de los flujos de trabajo de punta a punta, optimizando la toma de decisiones basada en datos y reduciendo los tiempos muertos en la cadena de suministro.

🛠️ Desafío Técnico y Modelo de Datos

El principal reto analítico radicaba en que los datos de origen no contaban con una estructura linealizada por fases. Para resolverlo, trabajé en las siguientes etapas dentro de Qlik Sense:

Modelado de Datos Asociativo: Diseñé un modelo de datos en estrella vinculando tablas de movimientos históricos, maestros de almacenes y estados actuales, evitando la creación de claves sintéticas (synthetic keys) mediante el uso de llaves compuestas e índices optimizados.

Lógica de Tiempos de Ciclo (Lead Time): Implementé funciones en el Data Load Script para calcular la diferencia de tiempo exacta (días/horas/minutos) entre el ingreso y egreso de cada fase de forma individualizada mediante tablas residentes y optimización de campos tipo Timestamp.

Anonimización y Seguridad: El dataset visible ha sido protegido mediante el enmascaramiento de datos confidenciales (indicadores de centros logísticos y fechas simuladas) para resguardar la privacidad de la operación real de la compañía.

🚀 Expresiones Avanzadas Utilizadas (Set Analysis)

Para lograr que los indicadores no se rompieran al aplicar filtros dinámicos y permitieran comparar el estado actual contra el histórico, desarrollé expresiones avanzadas utilizando Set Analysis.

Ejemplo de cálculo dinámico para medir órdenes atrasadas en una fase específica ignorando selecciones de tiempo secundarias:

// Cuenta las órdenes cuya fecha de fase superó el tiempo límite estimado (SLA) para el mes en curso
Count({<[Estado Fase]={'Demorado'}, [Año Actual]={'$(=Max(Año))'}>} DISTINCT ID_Orden)


📈 Impacto y Resultados Operativos

Visibilidad de Extremo a Extremo: Se sustituyeron los reportes planos de texto por un embudo de fases interactivo, reduciendo drásticamente el tiempo de detección de anomalías en el flujo operacional.

Detección de Cuellos de Botella: La combinación asociativa de Qlik permitió descubrir qué fases y franjas horarias retenían la mayor parte del tiempo total del ciclo logístico.

Automatización del Reporte: Se eliminó la necesidad de procesar archivos manuales de forma diaria gracias a la carga programada y estructurada del modelo analítico.
