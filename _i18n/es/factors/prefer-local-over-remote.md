En los últimos años, algunos equipos de desarrollo usan alternativas que requieren menos desarrollo, a expensas de la experiencia del usuario final al ubicar más lógica en un servidor back-end remoto siendo así la aplicación iOS una especie de cliente ligero que muestra los resultados obtenidos del servidor. Esta variante resulta en frustración para el usuario cuando la aplicación es usada con una conexión a internet "no tan perfecta" (como en el subterraneo, asensores o una conexión WiFi intermitente).

**Una aplicación debería hacer tanta lógica de negocio y cálculos en el dispositivo como sea posible** por múltiples razones:

- Privacidad: Evitar enviar información sensible a un servidor remoto.
- Velocidad: Enviar datos a un servidor y esperar por una respuesta requiere tiempo y está expuesto a fallos (ej. WiFi inestable).
- Gasto de datos: Los usuarios suelen tener un plan mensual de datos limitado.
- Escalamiento: Si la aplicación se hace viral, conlleva a la responsabilidad de escalar los servicios back-end.
- Batería: El uso de datos móbiles es costoso para la duración de la batería.
- Fiabilidad: Algunos paises aun tienen conexiones LTE/3G poco confiables.

La mayoría de aplicaciones iOS requieren algún tipo de back-end para ciertas tareas, como por ejemplo autenticación, operaciones muy complejas o almacenamiento de contenido.

**Limitar el número de tareas que corren en back-end al mínimo, para asegurar la experiencia del usuario final y proteger su privacidad.**

Todos los componentes de una aplicación que no necesariamente **necesitan** una conexión a internet (ej. login) deberían funcionar por completo aún sin estar conectados a la red:

- La pantalla de inicio de la aplicación ([que no debería existir en primer lugar](https://developer.apple.com/design/human-interface-guidelines/patterns/launching/)) jamás debe esperar por una primera respuesta exitosa del servidor web, ya que esto causa una mala experiencia de usuario cuando la conexión a internet es mala.
- Si la aplicación requiere una conexión a internet para todo (ej. red social o aplicación de navegación), debería funcionar de todas maneras (en modo de solo lectura) sin una conexión a internet para acceder a información histórica (ej. viajes recientes, mensajería privada).
- Toda característica de la aplicación que requiera una conexión a internet debería mostrar un mensaje de error claro sobre la incapacidad de conectarse al servidor.
- Ya que los puntos de acceso WiFi podrían solicitar inicio de sesión o confirmación de algún tipo (ej. hotel o aeropuerto), las solicitudes HTTPS se atascarán con frecuencia y se invalidarán por time-out después de un minuto aproximadamente. Hasta que Apple resuelva este inconveniente a nivel del sistema, nosotros como desarrolladores tenemos que asegurar un manejo adecuado de estas situaciones.
- Nunca se debe asumir que un usuario tiene conexión a internet al momento de lanzar la aplicación por primera vez. El usuario podría haber instalado la aplicación y no haberla abierto hasta ir en camino sin ninguna connectividad a internet. Se asume la responsabilidad de entregar una aplicación en un estado de funcionamiento por fuera de la caja con los recursos más actualizados en tiempo de despliegue. Ésto se relaciona directamente con el tren de releases semanal descrito en el factor [despliegue](/es/deployment).
