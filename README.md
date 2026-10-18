# Mapa NOC

Herramienta web para documentar la infraestructura de red de cada cliente y diagnosticar fallas más rápido.

**Abrir la herramienta:** https://gustavoazael.github.io/mapa-noc/

## Qué hace

- **Inventario global de equipos**: cada router, switch, OLT, firewall, radio o CPE se registra una sola vez, con IP, marca, modelo, acceso (SSH, Telnet, web) y sus puertos.
- **Carpetas por cliente**: Cliente › Sitio › Servicio. Cada carpeta tiene su propio diagrama.
- **Diagramas tipo Draw.io**: agrega equipos del inventario y textos, y conéctalos arrastrando el punto del borde de un equipo hacia otro. En cada conexión indicas el puerto de salida, el de llegada, el medio (fibra, cobre, radio, lógico) y una etiqueta (VLAN, ONT, circuito).
- **Análisis de impacto**: eliges un equipo o un puerto y te muestra todos los clientes y servicios que pasan por ahí, con resaltado en cada diagrama y una lista lista para copiar al ticket.
- **Búsqueda global** por equipo, IP, cliente o puerto.

## Dónde se guardan los datos

Los datos **no se suben a GitHub ni a ningún servidor**. Se guardan en el navegador de cada persona (`localStorage`).

- Usa **Exportar JSON** con frecuencia como respaldo.
- Si borras los datos del navegador o cambias de computadora, recupera todo con **Importar → Archivo JSON**.

## Compartir información con el equipo

Cada compañero tiene sus propios datos. Para intercambiar:

1. Exporta tu JSON y compártelo.
2. Tu compañero lo importa y elige **Combinar con lo mío**: los equipos se empatan por IP o nombre, y se agregan las carpetas, diagramas y conexiones que no tenga. No se borra nada de lo suyo.

## Importar inventario desde Excel

Guarda la hoja como CSV con estos encabezados (en español o inglés):

```
nombre,ip,tipo,marca,modelo,acceso,puerto acceso,ubicacion,puertos,notas
AGG-GPE-02,10.0.1.2,Switch,Huawei,S6730,ssh telnet,,Nodo GPE,XGE0/0/1|XGE0/0/2,
```

- **tipo**: Router, Switch, OLT, Firewall, Servidor, Radio, CPE u Otro.
- **acceso**: ssh, telnet y/o web.
- **puertos**: separados con `|`.
- Si la IP o el nombre ya existe, el equipo se actualiza en lugar de duplicarse. Acepta separador `,` o `;`.

## Atajos

- Rueda del mouse: zoom. Arrastrar el fondo: mover la vista.
- `Supr`: quita del diagrama lo seleccionado.
- Doble clic en un equipo: editarlo.
- `Esc`: cerrar ventanas o quitar la selección.
