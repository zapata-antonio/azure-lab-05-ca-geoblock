# Lab 05 — Protección Geográfica con Acceso Condicional (Conditional Access) | Microsoft Entra ID

## Contexto (por qué lo hice)
El acceso desde países donde la organización no opera es un riesgo típico (credenciales filtradas, accesos sospechosos).  
En este lab implemento un **bloqueo geográfico** con **Conditional Access** de forma segura: primero en **Solo informe (Report-only)** para validar impacto sin cortar servicio, y después en **On**, confirmando el bloqueo real en **Sign-in logs**.

## Objetivo
Bloquear inicios de sesión desde regiones no autorizadas mediante CA, validando:
- Impacto en **Solo informe**
- Resultado real en **Sign-in logs** cuando la directiva está **On**

---

## Tareas realizadas
1. Creación de una **ubicación con nombre (Named location)** para países bloqueados: `Paises_Bloqueados`.
2. Creación de directiva de **Conditional Access**:
   - **Usuarios:** Todos (excluyendo cuenta **break-glass**)
   - **Recursos:** **Todos los recursos**
   - **Condición:** **Ubicación** → include `Paises_Bloqueados`
   - **Conceder:** **Bloquear acceso**
3. Validación en **Solo informe** con **What If**.
4. Activación de la directiva (**On**).
5. Verificación en **Sign-in logs** (bloqueo real por CA).

---

## Evidencias

### 01 - Named locations (Paises_Bloqueados)
[<img src="images/01-named-locations.png" width="800">](images/01-named-locations.png)

### 02 - CA Policy (Solo informe / Report-only)
[<img src="images/02-ca-report-only.png" width="800">](images/02-ca-report-only.png)

### 02B - CA Location (Include Paises_Bloqueados)
[<img src="images/02b-location-include-paises_bloqueados.png" width="800">](images/02b-location-include-paises_bloqueados.png)

### 02C - CA Grant (Block Access)
[<img src="images/02c-grant-block-access.png" width="800">](images/02c-grant-block-access.png)

### 03 - What If (bloqueo evaluado)
[<img src="images/03-what-if-block.png" width="800">](images/03-what-if-block.png)

### 04 - CA Policy (On)
[<img src="images/04-ca-on.png" width="800">](images/04-ca-on.png)

### 05 - Sign-in logs (bloqueo real por CA)
[<img src="images/06-signin-logs-blocked-ca.png" width="800">](images/06-signin-logs-blocked-ca.png)

---

## Checklist de verificación
- [x] `Paises_Bloqueados` creado (Named locations)
- [x] Directiva CA creada (All users, excluye break-glass)
- [x] Recursos: **Todos los recursos**
- [x] Ubicaciones: **Include** `Paises_Bloqueados`
- [x] Conceder: **Bloquear acceso**
- [x] Validación con **What If** (Solo informe)
- [x] Directiva activada (**On**)
- [x] Bloqueo real confirmado en **Sign-in logs**

---

## Qué explicaría en una entrevista / a un cliente
“Primero despliego el bloqueo geográfico en **Solo informe** para validar impacto sin cortar servicio. Compruebo con **What If** que la directiva bloquearía el acceso desde los países definidos y, una vez validado, la paso a **On** excluyendo una cuenta **break-glass**. Finalmente confirmo el comportamiento en **Sign-in logs**, donde queda registrada la trazabilidad del bloqueo por Acceso Condicional.”
