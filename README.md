# Fundamentos de Seguridad y Auditoría:
En el mundo real, los incidentes de seguridad no esperan a que terminemos nuestro café ni nos dan semanas de plazo para investigar. Por esta razón, solo dispondré de 2 horas de la clase de hoy para investigar, ejecutar, documentar y hacer el push a GitHub de esta Bitácora.

## 1. El Escenario: "La Defensa en Profundidad y el rastro digital":
### La defensa en profundidad:
Es una estrategia que aprovecha múltiples medidas de seguridad para proteger los activos de una organización. El pensamiento es que si una línea de defensa se ve comprometida, existen capas adicionales como respaldo para garantizar que las amenazas se detengan en el camino. La defensa en profundidad aborda las vulnerabilidades de seguridad inherentes no solo con el hardware y el software, sino también con las personas, ya que la negligencia o el error humano suelen ser la causa de una violación de seguridad. https://www.fortinet.com/lat/resources/cyberglossary/defense-in-depth 

### AWS, GC y Microsoft Azure, ¿Qué infraestructura Cloud es mejor para mi proyecto?:
Como conclusión te diremos que AWS, GC y Microsoft Azure son utilizados para los mismos propósitos y, aunque con matices, proveen casi los mismos servicios y casi las mismas funcionalidades por lo que todo va a depender de tus necesidades, cargas de trabajo, o las del proyecto que tu empresa quiera llevar a cabo. https://www.clarcat.com/comparativa-aws-vs-microsoft-azure-vs-google-cloud-platform/ 

### Hardening:
Es un conjunto de medidas y prácticas que ayudan a proteger las redes y a reducir la superficie de ataque y que esta tiene diferentes tipos. https://www.unir.net/revista/ingenieria/hardening-que-es/ 

### Uso de: sistema operativo (SO) basado en Unix
Se debería plantear usar un sistema operativo basado en Unix por su potente interfaz de línea de comandos, su amplia gama de software de código abierto y sus sólidas funciones de seguridad. Tanto si eres programador, administrador de sistemas o usuario avanzado, el entorno Unix te resultará muy propicio para crear flujos de trabajo eficientes y personalizables. 
https://www.lenovo.com/es/es/glossary/unix-like/?orgRef=https%253A%252F%252Fwww.google.com%252F&srsltid=AfmBOopVGbNquAf8fJy5pTpfDNbqCyI_935NAebnnCMGsfc1SMZlKmlj 


## 2. Fase de Investigación: Comprendiendo el corazón del sistema
### Reto de investigación 1:
#### ¿Qué es un servidor Syslog?
Como su nombre lo indica, se utiliza para que dispositivos como routers, switches, firewalls, puntos de acceso Wi-Fi y servidores Linux generen sus propios registros. Los servidores de Windows usan registros de eventos, pero pueden utilizarse junto con los servidores Syslog. Su función es almacenar eventos o mensajes de registro localmente dentro del dispositivo elegido y enviar esta información a un servidor Syslog para obtener, ordenar y filtrar todos los registros y datos que contiene. https://blog.invgate.com/es/que-es-syslog 

#### Cómo interactúan la gravedad y las instalaciones:
La mensajería Syslog resulta más eficaz cuando los niveles de gravedad y los códigos de instalación se combinan para crear un sistema de prioridades estructurado. Esta combinación ayuda a categorizar los registros para su filtrado, enrutamiento y respuesta automatizados. 
https://logcentral.io/en/blog/syslog-priority-grid-severity-facility 

#### ¿Por qué es una negligencia grave que el archivo /var/log/auth.log tenga permisos de lectura para usuarios no privilegiados? ¿Qué información específica (como PIDs, nombres de usuario o direcciones IP) diferencia un intento fallido de conexión remota SSH de un simple fallo de contraseña de un usuario local frente a la pantalla?
Permitir que usuarios no privilegiados lean /var/log/auth.log es una negligencia crítica porque este archivo suele contener contraseñas expuestas por error (cuando un usuario las teclea en el campo de "login") y permite la enumeración de cuentas válidas, facilitando ataques dirigidos. Además, un atacante local podría estudiar los patrones de uso de los administradores y detectar qué servicios tienen vulnerabilidades sin dejar rastro, comprometiendo la confidencialidad total del sistema.
Para diferenciar los ataques, la clave está en el origen y el proceso: un fallo SSH remoto siempre mostrará el proceso sshd, incluirá la dirección IP externa y el puerto de origen. Por el contrario, un fallo de usuario local mostrará el proceso login o un gestor gráfico, y en lugar de una IP, registrará el identificador del terminal físico o virtual utilizado (como tty1), indicando que el atacante tiene acceso físico al equipo.
https://man7.org/linux/man-pages/man3/syslog.3.html#DESCRIPTION 

### Reto de investigación 2:
#### Cumplimiento y Log Management:
Centralizar los logs en un servidor externo es vital por dos razones: integridad ante ataques y cumplimiento legal (RGPD). Si un atacante compromete una máquina, su primer paso será borrar los logs locales para ocultar sus huellas; sin embargo, si estos se envían en tiempo real a un servidor externo, las evidencias quedan a salvo para realizar un análisis forense. Esto garantiza la "trazabilidad", permitiendo demostrar quién hizo qué y cuándo, algo imprescindible para defenderse legalmente.
Desde el punto de vista del RGPD, la gestión centralizada permite cumplir con la obligación de notificar brechas de seguridad y garantiza que los registros de acceso a datos personales no sean manipulables. En lugar de tener datos dispersos y vulnerables, una empresa puede aplicar cifrado y políticas de retención uniformes en un solo lugar seguro, demostrando así la "diligencia debida" ante una auditoría o inspección de la AEPD. https://dialnet.unirioja.es/servlet/articulo?codigo=7400589
