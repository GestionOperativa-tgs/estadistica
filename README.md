# Estadística de Accidentes GPM

Tablero web (GitHub Pages) de la estadística mensual de accidentes que se informa a ENARSA para el O&M del GPM, con los contratos **tgs** y **Telcosur**.

## Archivos
- `index.html` – el tablero (un solo archivo, sin dependencias).
- `Code.gs` – Apps Script que expone el Google Sheets como JSON.
- `BASE_ACCIDENTES_GPM.xlsx` – base para crear el Google Sheets:
  - **DATOS**: una fila por contrato y mes (única pestaña de carga).
  - **CONTRATOS**: código y nombre de cada contrato (agregar uno nuevo acá y el tablero lo toma solo).
  - **Reporte tgs** / **Reporte Telcosur**: el formato enviado a ENARSA, calculado con fórmulas desde DATOS (cambiar contrato en C2 y año en E2).
  - **AYUDA**: descripción de cada columna.

## Puesta en marcha
1. Subir `BASE_ACCIDENTES_GPM.xlsx` a Drive y abrirlo como Google Sheets (Archivo > Guardar como Hojas de cálculo de Google).
2. En ese Sheets: Extensiones > Apps Script, pegar `Code.gs`, Implementar como aplicación web (Ejecutar como: Yo · Acceso: Cualquier usuario) y copiar la URL `/exec`.
3. En `index.html`, completar `const FUENTE = { appsScriptUrl: "https://script.google.com/macros/s/.../exec", sheetId: "" };`
4. Settings > Pages > Deploy from branch `main` / root.

## Carga mensual
Completar en DATOS la fila del mes de cada contrato. El tablero toma como corte el último mes con *Personal* cargado y calcula IP, DMB, IF, totales y acumulados.
Si la URL de datos falla, el tablero muestra la copia embebida y lo indica en el pie ("Fuente").

## Índices
- IP = días de baja / personal × 1.000
- DMB = días de baja / accidentes con días de baja (B)
- IF = accidentes con días de baja (B) / horas trabajadas × 1.000.000
- Total de accidentes = A + B + C + D. El IP acumulado usa la suma mensual de personal, igual que la fila Total de la planilla.
