# Documentación del Contrato BoosterVeloLp

## Descripción General
El contrato **BoosterVeloLp** funciona como un intermediario entre los usuarios que depositan tokens LP y los contratos **Gauge** de Velodrome. Su objetivo es maximizar los rendimientos para los usuarios, pagando las recompensas en **ITP** en lugar de **VELO**.

---

## Características Principales

### Gestión de LPs y Gauges:
- Permite a los usuarios depositar tokens LP que son puestos en staking en los contratos Gauge asociados.
- Calcula y distribuye recompensas con un rendimiento adicional (*boost*) pagado en ITP.

### Boost de Recompensas:
- Utiliza un oráculo para convertir las recompensas originales en VELO a ITP.
- Aplica un porcentaje adicional específico para cada LP.

### Control Propietario:
- Permite al propietario del contrato gestionar los Gauges.
- Configura porcentajes de *boost*, comisiones y retira fondos acumulados.

---

## Variables Principales

### Tokens y Contratos Asociados:
- **itpToken**: Dirección del token ITP.
- **veloToken**: Dirección del token VELO.
- **router**: Contrato Velodrome Router.
- **oracle**: Contrato VeloOracle utilizado para tasas de conversión.

### Configuración y Control:
- **feePercentage**: Porcentaje de comisión para retiros.
- **boostPercentage**: Mapeo de LPs con el porcentaje de *boost* aplicado.
- **gauges**: Mapeo de LPs asociados con contratos Gauge.

### Balances y Recompensas:
- **balanceOf**: Mapeo del balance de LPs por usuario y token.
- **rewards**: Mapeo de recompensas pendientes por usuario y token.
- **lpFee**: Mapeo de comisiones acumuladas por token LP.

---

## Funciones del Contrato



## 1. Funciones Administrativas (*Solo Owner*)

### Gestión de Gauges
- **initializeGauges**: Asocia múltiples LPs con sus respectivos Gauges en una sola transacción.
- **addGauge**: Configura o actualiza un Gauge para un token LP.

### Gestión de Configuración
- **setRouter**: Actualiza la dirección del contrato Router.
- **setOracle**: Actualiza la dirección del contrato Oracle.
- **setFeePercentage**: Configura el porcentaje de comisión para retiros.
- **setBoostPercentage**: Configura el porcentaje de *boost* aplicado a las recompensas.

### Gestión de Fondos
- **claimVeloOwner**: Reclama recompensas acumuladas en VELO.
- **getLpFee**: Recupera las comisiones acumuladas para un LP.
- **withdrawITP**: Retira tokens ITP del contrato.

---

## 2. Funciones para Usuarios

### Depósito y Retiro
- **deposit**: Permite a los usuarios depositar LPs que son enviados al Gauge correspondiente.
- **withdraw**: Retira LPs junto con las recompensas generadas, aplicando una comisión sobre los retiros.

### Recompensas
- **earned**: Calcula las recompensas acumuladas para un usuario en un LP específico.
- **earnedItp**: Convierte las recompensas en VELO a ITP aplicando el *boost*.
- **balanceOfLp**: Retorna el balance de LPs de un usuario.
- **viewBoostPercentage**: Muestra el porcentaje de *boost* aplicado a un LP.

---

## 3. Funciones Internas

### Recompensas con Boost
- **rewardboost**: Calcula el valor de las recompensas en ITP utilizando el oráculo y aplica el *boost* definido para el LP.

### Actualización de Recompensas
- **_updateRewards**: Actualiza las recompensas acumuladas de un usuario antes de cualquier acción (depósito o retiro).

---


## Flujo del Contrato

### Depósito
1. Los usuarios depositan LPs.
2. Los LPs son enviados al Gauge correspondiente.
3. Se calculan las recompensas basadas en la actividad del Gauge.

### Recompensas
- Las recompensas en VELO generadas por el Gauge son convertidas a ITP con un *boost* adicional.

### Retiro
1. Los usuarios pueden retirar sus LPs y reclamar sus recompensas en ITP.
2. Se aplica una comisión sobre el retiro que se acumula para el propietario.

---

## Mejoras Futuras

- Soporte para más tokens y protocolos.
- Optimización del cálculo de *boost* para reducir costos de gas.
- Interfaz para seguimiento en tiempo real de las recompensas y balances.


