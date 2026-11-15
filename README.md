# AXIAS

Documentos de diseño y decisiones de la familia de software Axia (AEXIS Compliance Legal). Contiene modelos maestros genéricos y decisiones. **Nunca datos de clientes.**

## Estructura

| Carpeta | Contenido | Quién escribe |
|---|---|---|
| `base-comun/` | Contexto del sistema, arquitectura (niveles de captura y atributos de puesto) y convenciones de redacción compartidas por todos los productos Axia | Solo Cerebro (Axia RH). `arquitectura-y-convenciones.md` se genera del registro de Axia RH; no se edita a mano |
| `axia-rh/` | Registro de decisiones y mapa del PMV de Axia RH | Solo Cerebro (Axia RH) |
| `axia-noms/` | Registro, mapa y cortes de Axia NOMs | Solo el Cerebro de Axia NOMs |

## Reglas

1. **Una sola fuente.** Cada decisión vive en un solo archivo. La base común se deriva del registro de Axia RH; nadie la copia ni la reescribe en otro proyecto.
2. **Variables compartidas.** Toda variable de los niveles empresa, organigrama o alta, aunque la proponga otro producto, se decide en Axia RH. El otro proyecto la pide como encargo y Cerebro la registra.
3. **Cortes.** Las conversaciones de cada proyecto siguen guardando su «Corte - [documento]» en el conocimiento del proyecto de claude.ai. El Cerebro de cada producto los integra y actualiza aquí su registro y su mapa.
4. **Lectura.** Cada proyecto de claude.ai conecta este repositorio y selecciona sus carpetas: Axia RH, `base-comun/` y `axia-rh/`; Axia NOMs, `base-comun/` y `axia-noms/`. Después de cada cambio hay que sincronizar el proyecto.
5. **Historial.** Cada cambio es un commit con la fecha y el motivo; las versiones anteriores se consultan en el historial de GitHub.
