# Mapa NOC

Herramienta web para documentar la infraestructura de red de cada cliente y diagnosticar fallas más rápido.

**Abrir la herramienta:** https://gustavoazael.github.io/mapa-noc/

## Qué hace

- **Inventario global de equipos**: cada router, switch, OLT, firewall, radio o CPE se registra una sola vez, con IP, marca, modelo, acceso (SSH, Telnet, web) y sus puertos.
- **Carpetas por cliente**: Cliente › Sitio › Servicio. Cada carpeta tiene su propio diagrama.
- **Diagramas tipo Draw.io**: agrega equipos del inventario y textos, y conéctalos arrastrando el punto del borde de un equipo hacia otro. En cada conexión indicas el puerto de salida, el de llegada, el medio (fibra, cobre, radio, lógico) y una etiqueta (VLAN, ONT, circuito).
- **Análisis de impacto**: eliges un equipo o un puerto y te muestra todos los clientes y servicios que pasan por ahí, con resaltado en cada diagrama y una lista lista para copiar al ticket.
- **Búsqueda global** por equipo, IP, cliente o puerto.

## Redes: voz, transporte y datos

Cada equipo puede pertenecer a una o varias redes (**Voz**, **Transporte**, **Datos**). Se marca al editar el equipo o con la columna `red` del CSV.

- En **Equipos** filtras el inventario por red (o ves los que no tienen red asignada).
- En el diagrama cada equipo muestra etiquetas **V / T / D**, y el selector **Todas las redes** de la barra resalta una red y atenúa lo demás.

## Punto de demarcación

Selecciona una conexión y activa **Punto de demarcación**. Se dibuja una barra transversal sobre la línea, con el texto que quieras (por ejemplo "Demarcación" o "Entrega Telmex") y el nombre de cada lado (*Proveedor ⟷ Cliente*). La posición sobre la línea se ajusta con el control deslizante.

## Grupos: edificio, piso, sala, gabinete, rack

Para englobar equipos que están en el mismo lugar físico:

1. Selecciona varios equipos con **Shift+clic**, o con **Shift+arrastrar** sobre el fondo para hacer un recuadro.
2. En el panel derecho elige el tipo (Edificio, Piso, Sala, Gabinete, Rack o Zona) y presiona **Crear grupo**. También puedes usar **+ Grupo** en la barra.
3. Ponle nombre, color y notas (dirección, acceso, contacto).

Los grupos se pueden anidar (un rack dentro de una sala dentro de un edificio). Arrastra la franja del título para mover el grupo con todo lo que contiene y usa la esquina inferior derecha para cambiar su tamaño. Si un equipo dentro del grupo tiene una incidencia, el contorno del grupo se marca en rojo.

## Incidencias

En la pestaña **Incidencias** registras cada evento: título, ticket de red, ticket del proveedor, severidad, causa, inicio, fin y notas. En **Equipos y puertos afectados** eliges qué equipo (y opcionalmente qué puerto) falló; la herramienta calcula sola qué servicios y clientes quedan afectados.

- Una incidencia sin hora de fin está **activa**. Con **Cerrar ahora** se registra el fin.
- Los equipos y conexiones afectados se marcan en **rojo** en todos los diagramas, y al abrir el diagrama de un cliente afectado aparece un aviso de **evento activo**.
- En el árbol de clientes, un punto rojo indica que hay una incidencia activa dentro.
- **Copiar resumen** genera un texto con la afectación lista para pegar en el ticket o en un correo.
- También puedes registrar una incidencia desde el panel de un equipo o desde el análisis de impacto.

**Capa de incidencias** (selector en la barra del diagrama):

- **Activas**: resalta solo los eventos en curso.
- **Historial**: resalta todo lo que ha fallado en el periodo elegido y muestra en cada equipo cuántas incidencias ha tenido. Sirve para ver en qué parte del camino de un cliente se concentran las fallas.
- **Ocultas**: diagrama limpio.

Al final de la pestaña Incidencias está el ranking de **equipos y clientes más afectados** por periodo (30 días, 90 días, 12 meses o todo).

## Tipos de equipo

En **Equipos → Tipos** (o en el engrane ⚙) puedes crear y editar tipos como *CIENA*, *Switch Huawei*, *Firewall Fortinet* o *CPE Cliente*. Cada tipo tiene:

- Un ícono de la galería (30 opciones: router, switch, OLT, óptico, ODF, splitter, mufla, torre, satélite, energía, rack, firewall, VPN, servidor, base de datos, cámara IP, teléfono IP, CPE, edificio, internet, nube…) con el color que elijas, **o**
- Una imagen propia (PNG, JPG o SVG). Se reduce automáticamente a 96×96 px y viaja dentro del JSON exportado, así que tus compañeros también la ven al importar.

Si renombras un tipo, sus equipos se actualizan. Si lo eliminas, eliges a qué tipo pasan sus equipos. En el CSV, un tipo que no existe se crea solo con un ícono sugerido.

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
