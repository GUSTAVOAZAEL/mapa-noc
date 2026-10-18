# Mapa NOC

Herramienta web para documentar la infraestructura de red de cada cliente y diagnosticar fallas más rápido.

**Abrir la herramienta:** https://gustavoazael.github.io/mapa-noc/

## Qué hace

- **Inventario global de equipos**: cada router, switch, OLT, firewall, radio o CPE se registra una sola vez, con IP, marca, modelo, acceso (SSH, Telnet, web) y sus puertos.
- **Carpetas por cliente**: Cliente › Sitio › Servicio. Cada carpeta tiene su propio diagrama.
- **Diagramas tipo Draw.io**: agrega equipos del inventario y textos, y conéctalos arrastrando el punto del borde de un equipo hacia otro. En cada conexión indicas el puerto de salida, el de llegada, el medio (fibra, cobre, radio, lógico) y una etiqueta (VLAN, ONT, circuito).
- **Análisis de impacto**: eliges un equipo o un puerto y te muestra todos los clientes y servicios que pasan por ahí, con resaltado en cada diagrama y una lista lista para copiar al ticket.
- **Búsqueda global** por equipo, IP, cliente o puerto.

## Vistas de tarjetas: Clientes y Equipos

Arriba a la izquierda puedes cambiar entre **Diagramas** (la vista de siempre), **Clientes** y **Equipos**. Las tarjetas son otra forma de llegar a lo mismo; el árbol y los paneles siguen igual.

**Clientes**
- Una tarjeta por cliente con su ícono o logo, color, número de sitios y servicios, y aviso si tiene incidencias activas.
- El filtro **Con incidencia activa** muestra solo los clientes afectados.
- El lápiz de cada tarjeta (o **Personalizar**) cambia nombre, color, ícono o imagen/logo.
- Al abrir un cliente ves sus sitios con los servicios de cada uno; **Abrir diagrama** (o **Empezar diagrama** si está vacío) te lleva directo al diagrama. Desde ahí agregas sitios y servicios, y con el lápiz renombras, mueves o eliminas cualquiera. Al crear un servicio te pregunta si quieres abrir su diagrama de inmediato.

**Equipos**
- Tarjetas agrupadas en **Red de voz**, **Red de transporte** y **Red de datos** (y *Sin red*), con filtro por red, buscador (nombre, IP o puerto) y **Solo con incidencia**.
- Al tocar una tarjeta se abre la **ficha del equipo**: datos, acceso, puertos/IPs, diagramas donde aparece, incidencias, ubicación física, color de la tarjeta, editar y ver impacto.

## Ubicación física

Desde el **+** de un equipo (**Ver ubicación física**), su panel derecho o **Equipos → Ubicaciones** ves en qué edificio, zona, piso, sala, gabinete o rack lo has englobado, juntando lo que capturaste en todos tus diagramas:

- Los grupos con el mismo tipo y nombre en distintos diagramas se consideran el mismo lugar y suman sus equipos.
- Si un gabinete estuvo dentro de un edificio en algún diagrama, o comparten equipos, el gabinete se muestra dentro del edificio.
- Ves qué otros equipos comparten ese lugar y en qué diagramas se capturó cada ubicación (con botón para abrirlos).
- Si el mismo equipo quedó en dos lugares distintos del mismo tipo (por ejemplo, dos gabinetes), te avisa para que lo revises.
- Sin equipo elegido muestra todas las ubicaciones, con buscador.

## Mapa general

El botón **Mapa general** (arriba) une en un solo diagrama todos los servicios que elijas, sin mezclar tus diagramas individuales:

- En el panel izquierdo marcas clientes, sitios o servicios. Puedes elegir varios a la vez; **Todos** y **Ninguno** ayudan a empezar.
- Cada equipo aparece una sola vez. Los que están en varios diagramas llevan un número con cuántos los usan y la lista **compartidos** te dice cuáles son. Si los elegidos no comparten nada, te lo indica.
- Cada línea toma el color de su diagrama (ver leyenda a la derecha). Las conexiones repetidas en varios diagramas se dibujan más gruesas.
- **Resaltar solo lo compartido** atenúa todo lo demás.
- **Mostrar ubicaciones** dibuja los edificios, salas, gabinetes y racks que capturaste en tus diagramas, unidos y anidados igual que en *Ubicación física*. Tocar el título de una ubicación abre su detalle. **Reacomodar automáticamente** agrupa a los equipos dentro de su ubicación.
- Al seleccionar un equipo ves en qué diagramas aparece y puedes abrirlos. Impacto e incidencias también se marcan en el mapa.
- Puedes arrastrar los equipos para acomodar el mapa; esa posición se guarda aparte y no cambia tus diagramas. **Reacomodar automáticamente** lo vuelve a ordenar.
- El mapa es de solo lectura: para agregar o cambiar conexiones, abre el diagrama del servicio.

## Mover clientes, sitios y servicios

En el árbol de la izquierda arrastra cualquier elemento y suéltalo sobre otro cliente, sitio o carpeta para moverlo ahí, con todo su contenido y diagramas. Para dejarlo en el nivel principal suéltalo en el recuadro que aparece al final del árbol. También puedes moverlo desde **⋯ → Ubicación (mover a)**, útil en celular.

## Edición rápida en el diagrama

- **Botón + junto a cada elemento**: al pasar el mouse o seleccionar un equipo aparece un **+** al lado del punto de conexión. Desde ahí agregas un **equipo conectado** (se coloca a la derecha y queda unido con una línea), un **texto** debajo o un **grupo** alrededor.
- **Cambiar a qué elemento llega una línea**: selecciona la línea y arrastra el círculo de cualquiera de sus extremos hacia otro equipo, o elige el elemento en el panel derecho. Si la punta pasa a otro equipo, su puerto se limpia para que lo captures de nuevo.
- **Agregar equipos desde la búsqueda**: en *+ Equipo* escribe el nombre; si no existe, aparece **Crear equipo «nombre»** (o presiona Enter) y se abre el alta con ese nombre ya escrito. Al guardar se agrega al diagrama.
- **Colores**: selecciona una línea o un texto y elige su color en el panel derecho (hay paleta y selector libre). A los textos también les cambias tamaño y negritas.
- **Puertos o IPs en los enlaces**: al seleccionar una línea, debajo de cada extremo aparecen los puertos/IPs ya registrados en ese equipo; toca uno y queda puesto en el enlace. También puedes escribir uno nuevo y se guarda en el equipo.
- **Panel de Puertos / IPs**: al seleccionar un equipo, el recuadro *Puertos / IPs* muestra todos los registrados (resaltados los que se usan en el diagrama), permite agregar nuevos y abrir el impacto de cada uno. Útil para equipos de voz con varias IPs públicas.
- **Líneas sin flecha por default**: las conexiones nuevas se crean sin flecha; en el panel puedes elegir un sentido o ambos.
- El menú del **+** también tiene **Ver impacto** y **Registrar incidencia**. El resumen del impacto aparece en una tarjeta junto al equipo, con **Ver lista** y **Ocultar impacto**.
- **Nombres únicos**: no se puede guardar un equipo con un nombre que ya existe (sin importar mayúsculas). Mientras escribes te avisa y te ofrece **Agregar el existente**. Si la IP ya la tiene otro equipo, te avisa y te pide confirmar.

## Formas de los equipos

Cada tipo de equipo tiene una forma en el diagrama, que eliges en **Equipos → Tipos → Editar**:

| Forma | Uso sugerido |
|---|---|
| Rectángulo | Switches, OLT, firewalls, equipos en general |
| Caja chica | Mufla / caja de empalme, splitter, ODF |
| Vertical 3:4 | Servidores, racks |
| Círculo | Routers |
| Nube | ISP, internet, proveedor externo, nube |
| Anillo | Anillo o malla de red (metro, MPLS, backbone) |
| Hexágono | Núcleos o elementos lógicos |
| Solo ícono | Usuarios, teléfonos, cámaras, torres |

Si en un diagrama quieres otra forma para un equipo en particular, selecciónalo y cámbiala en **Forma en este diagrama**.

## Redes: voz, transporte y datos

Cada equipo puede pertenecer a una o varias redes (**Voz**, **Transporte**, **Datos**). Se marca al editar el equipo o con la columna `red` del CSV.

- En **Equipos** filtras el inventario por red (o ves los que no tienen red asignada).
- En el diagrama cada equipo muestra etiquetas **V / T / D** (el botón **V·T·D** de la barra las muestra u oculta), y el selector **Todas las redes** de la barra resalta una red y atenúa lo demás.

## Punto de demarcación

Selecciona una conexión y activa **Punto de demarcación**. Se dibuja una barra transversal sobre la línea, con el texto que quieras (por ejemplo "Demarcación" o "Entrega Telmex") y el nombre de cada lado (*Proveedor ⟷ Cliente*). La posición sobre la línea se ajusta con el control deslizante.

## Grupos: edificio, piso, sala, gabinete, rack

Para englobar equipos que están en el mismo lugar físico:

1. Selecciona varios equipos con **Shift+clic**, o con **Shift+arrastrar** sobre el fondo para hacer un recuadro.
2. En el panel derecho elige el tipo (Edificio, Piso, Sala, Gabinete, Rack o Zona) y presiona **Crear grupo**. También puedes usar **+ Grupo** en la barra.
3. Ponle nombre, color y notas (dirección, acceso, contacto).

Los grupos se pueden anidar (un rack dentro de una sala dentro de un edificio). Arrastra la franja del título para mover el grupo con todo lo que contiene y usa la esquina inferior derecha para cambiar su tamaño. Si un equipo dentro del grupo tiene una incidencia, el contorno del grupo se marca en rojo.

## Incidencias

En la pestaña **Incidencias** registras cada evento: título (opcional; si lo dejas vacío se arma con la causa, el equipo y el ticket), ticket de red, ticket del proveedor, severidad, causa, inicio, fin y notas. En **Equipos y puertos afectados** eliges qué equipo (y opcionalmente qué puerto) falló; la herramienta calcula sola qué servicios y clientes quedan afectados.

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

## Paneles laterales

- Los botones de panel en los extremos de la barra del diagrama ocultan o muestran el panel de clientes (izquierda) y el de detalle (derecha), para dejar más espacio al diagrama.
- Arrastra la línea entre un panel y el diagrama para hacerlo más angosto o más ancho. Doble clic sobre esa línea lo regresa a su ancho original.
- Se recuerda tu elección la próxima vez que abras la página.

## Atajos

- Los botones **+ Equipo**, **+ Texto** y **+ Grupo** están arriba del panel derecho (en celular, en la barra del diagrama).

- Rueda del mouse: zoom. Arrastrar el fondo: mover la vista.
- `Supr`: quita del diagrama lo seleccionado.
- Doble clic en un equipo: copia su IP (para pegarla en tu cliente SSH/Telnet o en el navegador). Para editarlo usa el botón **Editar equipo** del panel derecho.
- `Esc`: cerrar ventanas o quitar la selección.
