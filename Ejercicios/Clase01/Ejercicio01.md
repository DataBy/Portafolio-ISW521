Actividad 01
¿Es correcto lo que dijo el Rector?

Puede ser ambiguo, el rector dijo: “póngalo en internet” pero eso puede significar varias cosas. Internet es una red global de comunicación, basada en protocolos. Pero, www o web, es un servicio que funciona sobre internet y usa tecnologías específicas.

Si usan HTTP sobre Internet pero solo para usuarios internos de la UTN, ¿usan Internet, WWW o ambos?

Usan ambos, pero no como sitio público. Usan Internet como infraestructura de comunicación y usan tecnologías Web/WWW para acceder al sistema, pero el sistema no necesariamente es público.

¿Qué organismo define los estándares más relevantes: W3C o IETF?

IETF es clave para la comunicación, seguridad y protocolos de red.
W3C es clave para la estructura y presentación de la aplicación web.
Por tal, desde mi perspectiva, quién define los estándares más relevantes es IETF según a capa desde dónde se analice.

Actividad 02
Topología para cada necesidad

A) Sitio de información con trámites para vecinos: Debe estar disponible para cualquier ciudadano desde fuera de la municipalidad.

B) Sistema interno de gestión de planillas para RRHH: Intranet.
Debe ser usado solo por personal autorizado dentro de la municipalidad.

C) Portal para empresas constructoras que revisan permisos activos: Extranet.
No es público para todos, pero sí debe permitir acceso a usuarios externos autorizados.

¿Cuál requiere más inversión en seguridad?

El sistema B: requiere más seguridad porque contiene información más accesible; datos, salarios, problemas legales, entre otros.
En orden lo dejaría: Primero máxima seguridad la B, luego la C y por último la A.

¿Un mismo servidor físico podría alojar los tres sistemas de forma segura?

Sí, pero no mezclándolos directamente.
Se podría lograr usando máquinas virtuales o contenedores separados para cada sistema, con bases de datos independientes, usuarios distintos y permisos separados.

Actividad 03
Parte A: Disección de la URL

https://api.github.com:443/repos/bryancs/isw521/issues?state=open&labels=semana1#comentarios

Componentes principales identificados: 6

Protocolo: https
Dominio: api.github.com
Puerto: 443
Ruta: /repos/bryancs/isw521/issues
Query String: ?state=open&labels=semana1
Fragmento: #comentarios

Parámetros de la query:

?state=open&labels=semana1

Trae dos parámetros:

state = con valor open
labels = con valor semana1

Segmentos de la ruta

/repos/bryancs/isw521/issues

Se podría dividir en:

Repos = repositorios
Bryancs = usuario
Isw521 = nombre del repo
Issues = recurso solicitado
Parte B
Página de un curso: ISW-521, cuatrimestre 2026-II, sede San Carlos

https://utn.ac.cr/sedes/san-carlos/cursos/isw-521/2026-ii

Perfil de un estudiante con carné 2022-0001

https://utn.ac.cr/estudiantes

Lista de materiales de la semana 3 del curso ISW-521

https://utn.ac.cr/cursos/isw-521/semanas/3/materiales

Actividad 04
Partes de cada URL

URL: campus.utn.ac.cr

TLD: .cr
Tipo: ccTLD
Dominio Principal: utn.ac.cr
Subdominio: campus

URL: www.netflix.com

TLD: .com
Tipo: gTLD
Dominio Principal: netflix.com
Subdominio: www

URL: api.github.io

TLD: .io
Tipo: ccTLD
Dominio Principal: github.io
Subdominio: api

URL: app.maravilla.co.cr

TLD: .cr
Tipo: ccTLD
Dominio Principal: maravilla.co.cr
Subdominio: app
¿Quién administra .cr y .com?

.cr lo administra NIC Costa Rica / Academia Nacional de Ciencias
.com lo administra VeriSign, bajo el sistema ICANN

¿UTN debe pagar para crear egresados.utn.ac.cr?

No, con solo tener utn.ac.cr ya basta para crear otros submonios.

Registro A vs CNAME

Registro A: apunta un dominio a una IP.

campus.utn.ac.cr → 192.0.2.10
www.netflix.com → netflix.com