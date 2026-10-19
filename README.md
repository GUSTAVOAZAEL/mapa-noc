# NOCout

Herramienta web para documentar la infraestructura de red de cada cliente y diagnosticar fallas más rápido.

**Abrir la herramienta:** https://gustavoazael.github.io/mapa-noc/

## Qué hace

- **Inventario global de equipos**: cada router, switch, OLT, firewall, radio o CPE se registra una sola vez, con IP, marca, modelo, acceso (SSH, Telnet, web) y sus puertos.
- **Carpetas por cliente**: Cliente › Sitio › Servicio. Cada carpeta tiene su propio diagrama.
- **Diagramas tipo Draw.io**: agrega equipos del inventario y textos, y conéctalos arrastrando el punto del borde de un equipo hacia otro. En cada conexión indicas el puerto de salida, el de llegada, el medio (fibra, cobre, radio, lógico) y una etiqueta (VLAN, ONT, circuito).
- **Análisis de impacto**: eliges un equipo o un puerto y te muestra todos los clientes y servicios que pasan por ahí, con resaltado en cada diagrama y una lista lista para copiar al ticket.
- **Búsqueda global** por equipo, IP, cliente o puerto.

## Vistas de tarjetas: Clientes y Equipos

Arriba a la izquierda cambias entre **Clientes** (vista principal al abrir), **Equipos** y **Diagramas**. Las tarjetas son otra forma de llegar a lo mismo; el árbol y los paneles siguen igual.

**Clientes**
- La estrella **☆** de cada tarjeta (o *Personalizar*) marca al cliente como **destacado / VIP**: aparece primero, con borde dorado y la etiqueta ★ VIP; el filtro **★ Destacados** muestra solo esos.
- **Aa Texto** ajusta el tamaño y color de los nombres de cliente, sitio y servicio (aplica a todos).
- Una tarjeta por cliente con su ícono o logo, color, número de sitios y servicios, y aviso si tiene incidencias activas.
- El filtro **Con incidencia activa** muestra solo los clientes afectados.
- El lápiz de cada tarjeta (o **Personalizar**) cambia nombre, color, ícono o imagen/logo.
- Al abrir un cliente ves sus sitios con los servicios de cada uno; **Abrir diagrama** (o **Empezar diagrama** si está vacío) te lleva directo al diagrama. Desde ahí agregas sitios y servicios, y con el lápiz renombras, mueves o eliminas cualquiera. Al crear un servicio te pregunta si quieres abrir su diagrama de inmediato.

**Equipos**
- Tarjetas agrupadas en **Red de voz**, **Red de transporte** y **Red de datos** (y *Sin red*), con filtro por red, buscador (nombre, IP o puerto) y **Solo con incidencia**.
- Al tocar una tarjeta se abre la **ficha del equipo**: datos, acceso, puertos/IPs, diagramas donde aparece, incidencias, ubicación física, color de la tarjeta, editar y ver impacto.

## Ubicación física (ciudad › edificio › sitio › piso › sala › gabinete › rack)

Las ubicaciones forman un catálogo único y ordenado: **Ciudad › Edificio › Sitio › Piso › Sala › Gabinete › Rack** (puedes saltarte niveles). Un rack está en un gabinete, un gabinete en una sala, una sala en un piso, un piso en un sitio, un sitio en un edificio y un edificio en una ciudad. En **Sitio** también aparecen como opción los sitios de tus clientes (*Cliente/Sitio*); al elegir uno queda ligado y sus equipos se agregan a ese sitio.

- **Sin encimarse**: al abrir un diagrama, al agregar un equipo o al soltar uno, los recuadros de ubicación se acomodan solos: los del mismo nivel quedan lado a lado, cada uno dentro del de arriba, y los equipos que no pertenecen a una ubicación se sacan de su recuadro. Un equipo nuevo que ya tiene ubicación aparece dentro de su grupo.

- **Grupos del diagrama**: al seleccionar un grupo eliges su **Tipo** y luego el lugar de la lista. Cada opción muestra su ruta (por ejemplo *Monterrey › DC Norte › Piso 2*) para distinguir una "Sala 5" de Monterrey de otra en Querétaro. Si no existe, escríbelo y créalo indicando **dentro de** qué lugar va.
- Al elegir un nivel bajo (por ejemplo un gabinete), la ruta completa se toma automáticamente y se muestra debajo como **Ruta de la ubicación**.
- **Los equipos guardan su ubicación**: al englobar un equipo en un grupo (o al moverlo dentro de uno) se le asigna el lugar más específico. Si ya tenía uno más detallado dentro de ese mismo lugar, se respeta.
- **Dos formas de registrar la ubicación de un equipo**: (1) a mano en **Editar equipo → Ubicación física** (escribes *Sala 5*, *GAB-07*… y eliges la opción con su ruta, o la creas); (2) desde un diagrama, metiéndolo en un grupo de ubicación.
- **La ubicación se refleja en todos los diagramas**: donde aparezca ese equipo se dibuja solo un recuadro punteado más tenue con su ciudad, edificio, piso, sala, gabinete o rack (sin repetir los que ya dibujaste a mano). Al arrastrar su título se mueven los equipos de esa ubicación; **Fijar como grupo editable** lo convierte en un grupo normal. El botón **📍 Ubicaciones** de la barra abre una lista para elegir qué niveles se ven (Ciudad, Edificio, Sitio, Piso, Sala, Gabinete, Rack), con **Todos** y **Ninguno**. Aplica a los diagramas (grupos automáticos y dibujados a mano) y al mapa general, y se recuerda. Si ocultas todos, no se acomoda nada ni cambia la ubicación al mover equipos.
- Si sacas un equipo de un grupo dibujado, pierde esa ubicación (queda en el nivel de arriba). Si sueltas un equipo **sin ubicación** dentro de un recuadro automático, toma esa ubicación.
- En el panel del equipo y en su ficha aparece **Ubicación física** con la ruta en orden; **Cambiar/Asignar** permite elegirla o crearla sin dibujar un grupo. **Ver ubicación física** del menú **+** te lleva a esa sección.
- **Equipos → Ubicaciones** muestra el catálogo completo con los equipos de cada lugar.
- El campo de texto libre del equipo ahora se llama *Referencia / nodo*.
- Tus grupos anteriores se convirtieron solos al catálogo la primera vez que abres esta versión.

## Equipos en tabla

En la vista **Equipos** cambia entre **▦ Tarjetas** y **☰ Tabla**. En la tabla editas directo en cada celda (nombre, IP, tipo, marca, modelo, referencia, acceso, puertos/IPs, notas); el cambio se guarda al salir de la celda (**Enter** baja a la fila siguiente, **Esc** deshace). Las redes **V / T / D** se activan con un clic. La ubicación va en columnas **Ciudad, Edificio, Sitio, Piso, Sala, Gabinete y Rack**: escribe o elige de la lista (solo muestra lo que existe dentro del nivel de arriba); si capturas directo un nivel bajo que ya existe, los de arriba se llenan solos, y si llenas un nivel intermedio que faltaba, queda insertado para todos los equipos de ese lugar. **📍** abre el catálogo, y clic en el título de una columna ordena. El acceso se escribe como `ssh, telnet:2323, web:8443`. **＋ Fila nueva** agrega un equipo en blanco. Los filtros de red, búsqueda y "solo con incidencia" también aplican a la tabla, y se recuerda la vista que elegiste.

En el panel de **Clientes** (y en la lista del mapa general) cada cliente va en un bloque sombreado con su color, para ver fácil dónde empieza y dónde termina. Clic en un **cliente** o **sitio** abre o cierra lo que contiene; solo los **servicios** abren su diagrama. Los botones **⊟** y **⊞** junto a *+ Cliente* compactan o despliegan todo el árbol.

## Unificar equipos duplicados

Si diste de alta el mismo equipo dos veces con nombres distintos (por ejemplo *ASR MTY 9010 1* y *mty-asr9010-1*): en **Equipos** marca la casilla de ambos (esquina de la tarjeta, o junto al nombre en la tabla) y presiona **⇄ Unificar**. Eliges cuál se queda y, cuando los datos no coinciden, qué nombre, IP, tipo, marca, modelo, ubicación, etc. conservar. Redes, accesos y puertos se suman; las notas se juntan y se anotan las IPs y nombres que no quedaron. El equipo que se va se reemplaza por el que se queda en todos los diagramas (sus líneas pasan al que se queda), incidencias y sitios. Se puede deshacer con Ctrl+Z.

## Mapa general

El mapa general se maneja desde el mismo árbol de clientes, sin cambiar el panel: **Mapa** (arriba del árbol) junta todo; el ícono de mapa en la fila de un **cliente** o **sitio** muestra solo sus diagramas; **☑ Comparar** abre el mapa vacío. Mientras estás en el mapa, cada fila del árbol tiene una casilla: marca o desmarca clientes, sitios o servicios (de clientes distintos si quieres) y el mapa se actualiza al momento. Arriba del árbol ves cuántos diagramas van, **Todos / Ninguno**, los equipos compartidos, y *Resaltar solo lo compartido*. Los equipos se quedan donde tú los acomodes. **↗** en un servicio abre su diagrama y **✕ Salir del mapa** regresa. El mapa une en un solo diagrama todos los servicios que elijas, sin mezclar tus diagramas individuales:

- En el panel izquierdo marcas clientes, sitios o servicios. Puedes elegir varios a la vez; **Todos** y **Ninguno** ayudan a empezar.
- Cada equipo aparece una sola vez. Los que están en varios diagramas llevan un número con cuántos los usan y la lista **compartidos** te dice cuáles son. Si los elegidos no comparten nada, te lo indica.
- Cada línea toma el color de su diagrama (ver leyenda a la derecha). Las conexiones repetidas en varios diagramas se dibujan más gruesas.
- **Resaltar solo lo compartido** atenúa todo lo demás.
- **Mostrar ubicaciones** dibuja los edificios, salas, gabinetes y racks que capturaste en tus diagramas, unidos y anidados igual que en *Ubicación física*. Tocar el título de una ubicación abre su detalle.
- Al seleccionar un equipo ves en qué diagramas aparece y puedes abrirlos. Impacto e incidencias también se marcan en el mapa.
- **Mover un grupo**: arrastra el título de un recuadro de ubicación (ciudad, edificio, sala…) y se mueve con todo lo que tiene dentro. Un clic sin arrastrar abre el detalle de esa ubicación.
- **🌎 Mapa de México y EUA de fondo** (opcional, en el recuadro del mapa): dibuja los estados de ambos países detrás de los equipos para que los acomodes en su zona aproximada; con **Tamaño** lo agrandas o achicas respecto a los equipos. Es solo visual.
- Los **elementos sin inventario** (LAN del cliente, caja de empalme, splitter, poste…) también aparecen en el mapa, con sus líneas. Cada uno es propio de su diagrama, así que no se cuentan como compartidos. La primera vez se colocan junto al equipo con el que se conectan (o cerca de los equipos de su diagrama) y después se quedan donde los acomodes. Al darles clic ves en qué diagrama están.
- Puedes arrastrar los equipos para acomodar el mapa; esa posición se guarda aparte y no cambia tus diagramas.
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

## Equipos sugeridos del mismo cliente

Mientras dibujas un diagrama, el panel derecho (sin nada seleccionado) y la ventana **+ Equipo** muestran los equipos que ya usaste en otros diagramas del mismo cliente y que aún no están en este, ordenados por **Transporte, Datos, Voz** y *Sin red*. Un clic los agrega.

## Elementos sin inventario

Para cosas que deben verse en el diagrama pero no se gestionan (caja de empalme, splitter, ODF, poste, registro, un proveedor externo…) usa **+ Elemento** (panel derecho) o **Elemento conectado** en el menú **+** de un equipo.

**Tipos de elemento propios:** en la ventana de **+ Elemento** (o *Elemento conectado* del menú +) presiona **＋ Nuevo tipo**, ponle nombre, ícono, forma y color, y se queda guardado como opción del menú para todos tus diagramas (viaja en tu JSON). La ✕ en la esquina lo quita del menú sin borrar los elementos ya dibujados.

- No se agregan al inventario ni cuentan en el análisis de impacto o el mapa general.
- Puedes poner **varios en el mismo diagrama** (botón **Duplicar**), con nombre, texto debajo (hilos, poste…), forma, ícono, color y notas.
- Se conectan con líneas como cualquier equipo; en sus extremos puedes escribir libremente (por ejemplo *Hilos 1-6*).

## Líneas privadas entre sitios

- Al editar un servicio (lápiz o ⋯), en **Línea privada: también llega a** marca los otros sitios del cliente por los que pasa. El servicio aparece en la página del cliente bajo cada sitio con la marca **↔ Línea privada con…**, y en el árbol con **↔**.
- En la página del cliente, el mismo servicio en dos sitios se marca con la etiqueta **L2L**, fondo amarillo y una **línea amarilla con dos puntos** que une ambos sitios, rodeando las tarjetas por debajo, por los espacios entre ellas.
- En las líneas del diagrama hay un medio nuevo, **Línea privada (L2L)**, que se dibuja con trazo de raya y punto.

## Equipos en cada sitio

En la página de un cliente (vista **Clientes**), cada sitio tiene **Equipos en este sitio**: agrégalos con **+ Equipo** (también aparecen solos los equipos cuyo campo *Ubicación* coincide con el nombre del sitio). **Toca un equipo para copiar su IP.**

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
2. En el panel derecho elige el tipo (Ciudad, Edificio, Piso, Sala, Gabinete, Rack, Sitio o Zona) y presiona **Crear grupo**. También puedes usar **+ Grupo** en la barra.
3. Ponle nombre, color y notas (dirección, acceso, contacto).

**Grupo tipo Sitio:** escribe parte del nombre (por ejemplo *Est…*) y aparecen los sitios de tus clientes como `Cliente/Sitio` (*Estafeta/CEDIS Guadalupe*, *Estafeta/Planta Apodaca*…). Puedes escribir varias palabras (`est apo`). Al elegir uno, los equipos dentro del grupo se agregan a los equipos de ese sitio (se ven en su tarjeta de cliente). Si no existe, puedes usar el texto como nombre libre.

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
- Doble clic sobre el recuadro de un equipo (en su nombre o IP, no en el punto de conexión ni en el +): copia su IP. También está el botón **Copiar IP** junto a la IP en el panel derecho. Para editarlo usa el botón **Editar equipo** del panel derecho.
- **Deshacer / Rehacer**: botones **↶ ↷** en la barra del diagrama, o **Ctrl+Z** y **Ctrl+Y** (también Ctrl+Shift+Z). Guarda hasta 60 pasos de la sesión: borrar equipos, líneas o grupos, moverlos, cambios en el panel, en la tabla de equipos, etc.
- Doble clic en una **parte vacía** del diagrama: aparece un menú para agregar **Equipo, Elemento, Texto o Grupo** justo en ese punto.
- Doble clic sobre un **texto** del diagrama: lo editas ahí mismo (Enter hace un salto de línea; **Ctrl+Enter** o clic fuera guarda; **Esc** cancela). En un **elemento** (caja de empalme, etc.) el doble clic edita su nombre (Enter guarda).
- `Esc`: cerrar ventanas o quitar la selección.
