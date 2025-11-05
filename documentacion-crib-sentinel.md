## Integración de cribl-sentinel
--- 
En este apartado se muestran las configuraciones para la creación de una integración entre cribl y sentinel, esto con el fin de que los dispositivos que tienen la capacidad de
enviar logs a travez de una ip de ingesta hacia un recolector de logs en este caso cribl, que sirve de puente para la conexión con sentinel


## Creación del grupo de recursos
---
Lo primero es tener una cuenta de azure

1. Inicia sesión en el portal
Ve a https://portal.azure.com e inicia sesión con tu cuenta de Azure.

2. Accede a "Grupos de recursos"
En el menú lateral izquierdo, haz clic en "Grupos de recursos".

<img width="300" height="400" alt="image" src="https://github.com/user-attachments/assets/3f8c9ab7-47cd-468f-b3c5-3e03a808c3a2" />

Luego selecciona "Crear" en la parte superior.

<img width="373" height="172" alt="image" src="https://github.com/user-attachments/assets/61298376-4d87-4dcb-ab1b-c3d01386b618" />

3. Configura el grupo
Completa los siguientes campos:

      Suscripción: Elige la suscripción de Azure donde se creará el grupo.

      Nombre del grupo de recursos: Asigna un nombre único y descriptivo.

      Región: Selecciona la ubicación geográfica donde se almacenarán los metadatos del grupo (esto no afecta la ubicación de los recursos dentro del grupo).

4. Revisión y creación
Haz clic en "Revisar y crear".

     Verifica que toda la información esté correcta.

     Haz clic en "Crear" para finalizar.

## Creación de Log Analytics Wokspace (LAW)
---

1. Inicia sesión en el portal
      Accede a Azure Portal con tu cuenta.

2. Busca el servicio
      En la barra de búsqueda superior escribe “Log Analytics workspaces”.

      Selecciona la opción que aparece en los resultados.

3. Crear un nuevo workspace
      Haz clic en “Crear”.

      Se abrirá el asistente de configuración.

4. Configuración básica
      En la pestaña Básico completa:

      Suscripción: Selecciona la suscripción de Azure activa.

      Grupo de recursos: Elige el grupo de recursos que ya tienes creado.

      Nombre del área de trabajo: Define un nombre único (ejemplo: law-monitoring-prod).

      Región: Selecciona la misma región donde están tus recursos principales (para optimizar costos y latencia).

5. Revisar y crear
      Haz clic en Revisar y crear.

      Valida que la configuración sea correcta.

      Pulsa Crear para desplegar el workspace.

6. Validación
      Una vez completado, verás el recurso en tu grupo de recursos.

      Desde allí podrás conectarlo a Azure Monitor, VMs, Azure Security Center, Defender for Cloud, o incluso a fuentes externas.

## Configuración de Puntos de Conexión de Recopilación de Datos (DCE)
---
1. Inicia sesión en el portal
      Accede a Azure Portal con tu cuenta.

2. Buscar el servicio
      En la barra superior, escribe “Puntos de conexión de recopilación de datos” o “Data Collection Endpoints”.

      Selecciona la opción que aparece en los resultados.

3. Crear un nuevo DCE
      Haz clic en “Crear”.

      En la pestaña Básico completa:

      Suscripción: Selecciona la suscripción de Azure donde se desplegará.

      Grupo de recursos: Elige el grupo de recursos que ya tienes creado.

      Nombre: Define un nombre único y descriptivo (ejemplo: dce-monitoring-prod).

      Región: Selecciona la misma región donde estarán tus recursos y tu Log Analytics Workspace.

4. Configuración adicional
      Puedes dejar las opciones predeterminadas en la pestaña de Etiquetas si no necesitas clasificar el recurso.

      Haz clic en Revisar y crear.

      Valida la configuración y selecciona Crear.

6. Validación
      Una vez creado, verás el DCE en tu grupo de recursos.

      Desde allí podrás asociarlo a una Regla de recopilación de datos (DCR), que define qué datos se recopilan y a dónde se envían (por ejemplo, a un Log Analytics Workspace).
