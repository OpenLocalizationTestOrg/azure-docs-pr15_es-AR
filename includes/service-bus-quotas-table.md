La tabla siguiente muestra información de cuota específica de Bus de servicios de mensajería. Límites de concentradores de eventos se incluyen en esta tabla, pero para obtener información específica acerca de los concentradores de eventos, vea [Eventos precios de concentradores](https://azure.microsoft.com/pricing/details/event-hubs/). Para obtener información sobre precios y otras cuotas para el Bus de servicio, vea la información general de [Tarifas de servicio de Bus](https://azure.microsoft.com/pricing/details/service-bus/) .

|Nombre de cuota|Ámbito de aplicación|Tipo|Comportamiento cuando supera|Valor|
|---|---|---|---|---|
| Número máximo de espacios de nombres por cada suscripción de Azure|Namespace|Estática|Se rechazarán las solicitudes posteriores para espacios de nombres adicionales por el portal.|100|
|Tamaño de cola/tema|Entidad|Definido durante la creación de la cola/tema.|Se rechazarán los mensajes entrantes y se recibirá una excepción en el código de llamada.|1, 2, 3, 4 o 5 GB.<br /><br />Si está habilitada la [partición](service-bus-partitioning.md) , el tamaño máximo de cola/tema es 80 GB.|
|Número de conexiones simultáneas en un espacio de nombres|Namespace|Estática|Se rechazarán las solicitudes posteriores para conexiones adicionales y se recibirá una excepción en el código de llamada. RESTO operaciones no se contabilizan para conexiones TCP simultáneas.|NetMessaging: 1.000<br /><br />AMQP: 5.000|
|Número de conexiones simultáneas en una entidad de cola/tema/suscripción|Entidad|Estática|Se rechazarán las solicitudes posteriores para conexiones adicionales y se recibirá una excepción en el código de llamada. RESTO operaciones no se contabilizan para conexiones TCP simultáneas.|Limitada por el límite de conexiones simultáneas por espacio de nombres.|
|Número concurrente de recepción de las solicitudes en una entidad de cola/tema/suscripción|Entidad|Estática|Recibir posteriores se rechazarán las solicitudes y se recibirá una excepción en el código de llamada. Este límite se aplica a la combinación número de concurrentes recibir las operaciones a través de todas las suscripciones en un tema.|5.000|
|Número de temas y colas por espacio de nombres del servicio|Todo el sistema|Estática|Se rechazarán las solicitudes posteriores para la creación de un nuevo tema o cola en el espacio de nombres del servicio. Como resultado, si se configura a través del [portal de Azure][], se generará un mensaje de error. Si llama desde la API de administración, se recibirá una excepción en el código de llamada.|10.000<br /><br />El número total de temas más colas en un espacio de nombres del servicio debe ser menor o igual a 10.000.<br/>Esto no es aplicable a Premium como se particionan todas las entidades.|
|Número de temas/colas divididas por espacio de nombres del servicio|Todo el sistema|Estática|Se rechazarán las solicitudes posteriores para la creación de un nuevo tema con particiones o una cola en el espacio de nombres del servicio. Como resultado, si se configura a través del [portal de Azure][], se generará un mensaje de error. Si llama desde la API de administración, se recibirá una excepción **QuotaExceededException** en el código de llamada.|Niveles básicos y estándares - 100<br />Premium - 1.000<br/><br />Cada cola con particiones o tema cuenta hacia la cuota de 10.000 entidades por espacio de nombres.|
|Tamaño máximo de cualquier ruta de acceso de entidad mensajería: cola o tema|Entidad|Estática|-|260 caracteres|
|Tamaño máximo de cualquier nombre de entidad mensajería: espacio de nombres, suscripción, regla de suscripción o concentrador de evento|Entidad|Estática|-|50 caracteres|
|Tamaño máximo de evento del evento concentradores|Todo el sistema|Estática|-|256 KB|
|Tamaño de mensaje para una entidad de cola/tema/suscripción|Todo el sistema|Estática|Se rechazarán los mensajes entrantes que superen estos contingentes y se recibirá una excepción en el código de llamada.|Tamaño máximo de mensaje: ([nivel Standard](../articles/service-bus/service-bus-premium-messaging.md)) de 256KB o 1 MB ([nivel Premium](../articles/service-bus/service-bus-premium-messaging.md)). <br /><br />**Nota** Debido a la sobrecarga del sistema, este límite suele ser ligeramente inferior.<br /><br />Tamaño máximo del encabezado: 64KB<br /><br />Número máximo de propiedades de encabezado en la bolsa de propiedades: **bytes/int. MaxValue**<br /><br />Tamaño máximo de la propiedad en la bolsa de propiedades: sin límite explícito. Limitado por el tamaño máximo del encabezado.|
|Tamaño de la propiedad de mensaje para una entidad de cola/tema/suscripción|Todo el sistema|Estática|Se genera una excepción **SerializationException** .|Tamaño máximo de los mensajes de la propiedad para cada propiedad es 32K. Tamaño acumulado de todas las propiedades no puede exceder de 64K. Esto se aplica al encabezado completo de [BrokeredMessage](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.aspx), que tiene dos propiedades de usuario, así como propiedades del sistema (por ejemplo, [SequenceNumber](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.sequencenumber.aspx), [etiqueta](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.label.aspx), [MessageId](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.brokeredmessage.messageid.aspx)y así sucesivamente).|
|Número de suscripciones por tema|Todo el sistema|Estática|Se rechazarán las solicitudes posteriores para crear suscripciones adicionales para el tema. Como resultado, si se configura a través del portal, se mostrará un mensaje de error. Si llama a la API de administración se recibirá una excepción en el código de llamada.|2.000|
|Número de filtros SQL por tema|Todo el sistema|Estática|Se rechazarán las solicitudes posteriores para la creación de filtros adicionales en el tema y se recibirá una excepción en el código de llamada.|2.000|
|Número de filtros de correlación por tema|Todo el sistema|Estática|Se rechazarán las solicitudes posteriores para la creación de filtros adicionales en el tema y se recibirá una excepción en el código de llamada.|100.000|
|Tamaño de filtros y acciones de SQL|Todo el sistema|Estática|Se rechazarán las solicitudes posteriores para la creación de filtros adicionales y se recibirá una excepción en el código de llamada.|Longitud máxima de cadena de la condición de filtro: 1024 (1K).<br /><br />Longitud máxima de cadena de la acción de regla: 1024 (1K).<br /><br />Número máximo de expresiones por la acción de regla: 32.|
|Número de reglas de [SharedAccessAuthorizationRule](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.sharedaccessauthorizationrule.aspx) por el espacio de nombres, cola o tema|Entidad, espacio de nombres|Estática|Se rechazarán las solicitudes posteriores para la creación de reglas adicionales y se recibirá una excepción en el código de llamada.|Número máximo de reglas: 12. <br /><br /> Reglas que se configuran en un espacio de nombres del Bus de servicio se aplican a todas las colas y los temas de ese espacio de nombres.

[Portal de Azure]: https://portal.azure.com