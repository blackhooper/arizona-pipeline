# arizona-pipeline

Repo público solo con los flujos de GitHub Actions de la plataforma: en un repo público los minutos de Actions son gratis y sin límite (runners estándar), así que **toda acción nueva va aquí**, nunca en los repos privados. No contiene datos ni código del proyecto: clona los repos privados con un token, corre lo que haga falta y guarda los resultados allí.

| Flujo | Cuándo | Qué hace |
|---|---|---|
| `actualizar.yml` | día 5 de cada mes y a mano | Corre `pipeline/correr_pasos.py` (todos los pasos de datos y, después, los tiempos de viaje); guarda crudos en `arizona-datos` y publica lo procesado en la página. |
| `terreno.yml` | 1 de septiembre y a mano | Teselas de elevación del USGS 3DEP. |
| `verificar.yml` | cada 15 minutos y a mano | Corre `pipeline/verificar.py` sobre cada commit nuevo de los PR abiertos y de `main` de la página, y marca el resultado como estado «Verificar (repo público)» del commit. |

- Los registros son públicos: ningún flujo imprime la salida de los scripts. Solo se ve «paso NN/total: ok» o «commit abc1234: success»; los detalles quedan en el repo privado de datos (`fuentes/ultima_corrida_*.log`, `fuentes/verificacion/`).
- Secrets: `PUBLICAR_TOKEN` (fine-grained; Contents lectura y escritura sobre la página y `arizona-datos`, y **Commit statuses** lectura y escritura sobre la página; renovar antes de que venza) y `CENSUS_API_KEY`.
- No usar runners grandes (*larger runners*): esos sí se cobran aun en repos públicos.
- GitHub apaga los flujos programados de un repo público tras 60 días sin actividad: si pasa, reactivarlos en la pestaña Actions.
