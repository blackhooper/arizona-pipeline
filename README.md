# arizona-pipeline

Repo público solo con el flujo de GitHub Actions que actualiza los datos de la plataforma (así los minutos de Actions son gratis). No contiene datos ni código del proyecto: clona dos repos privados con un token, corre `pipeline/correr_pasos.py` y guarda los resultados allí.

- `actualizar.yml`: día 5 de cada mes y a mano («Run workflow»).
- Los registros de la corrida son públicos y solo muestran «paso NN/total: ok»; los detalles quedan en el repo privado de datos.
- Secrets: `PUBLICAR_TOKEN` (renovar antes de que venza) y `CENSUS_API_KEY`.
- GitHub apaga los flujos programados de un repo público tras 60 días sin actividad: si pasa, reactivarlo en la pestaña Actions.
