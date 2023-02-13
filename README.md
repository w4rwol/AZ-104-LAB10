# Laboratorio 10 - Copia de seguridad de máquinas virtuales

## Escenario de laboratorio
Se le asignó la tarea de evaluar el uso de Azure Recovery Services para realizar copias de seguridad y restaurar archivos alojados en máquinas virtuales de Azure y equipos locales. Además, desea identificar métodos para proteger los datos almacenados en el almacén de Recovery Services contra pérdidas de datos accidentales o maliciosas.

Nota: Hay disponible una simulación de laboratorio interactiva que le permite hacer clic en este laboratorio a su propio ritmo. Es posible que encuentre ligeras diferencias entre la simulación interactiva y el laboratorio alojado, pero los conceptos e ideas centrales que se demuestran son los mismos.

## Objetivos
En este laboratorio, usted:

- Tarea 1: Aprovisionar el entorno de laboratorio
- Tarea 2: crear un almacén de servicios de recuperación
- Tarea 3: implementar una copia de seguridad a nivel de máquina virtual de Azure
- Tarea 4: Implementar la copia de seguridad de archivos y carpetas
- Tarea 5: realizar la recuperación de archivos mediante el agente de Azure Recovery Services
- Tarea 6: realizar la recuperación de archivos mediante instantáneas de máquinas virtuales de Azure (opcional)
- Tarea 7: revisar la funcionalidad de eliminación temporal de Azure Recovery Services (opcional)

## Tiempo estimado: 50 minutos
## Diagrama de arquitectura

## Instrucciones
### Ejercicio 1
### Tarea 1: Aprovisionar el entorno de laboratorio
En esta tarea, implementará dos máquinas virtuales que se utilizarán para probar diferentes escenarios de copia de seguridad.

Inicie sesión en el portal de Azure .

En Azure Portal, abra Azure Cloud Shell haciendo clic en el icono en la parte superior derecha de Azure Portal.

Si se le solicita que seleccione Bash o PowerShell , seleccione PowerShell .

Nota : si es la primera vez que inicia Cloud Shell y aparece el mensaje No tiene almacenamiento montado , seleccione la suscripción que está usando en este laboratorio y haga clic en Crear almacenamiento .

En la barra de herramientas del panel de Cloud Shell, haga clic en el ícono Cargar/Descargar archivos , en el menú desplegable, haga clic en Cargar y cargue los archivos \Allfiles\Labs\10\az104-10-vms-edge-template.json y \ Allfiles\Labs\10\az104-10-vms-edge-parameters.json en el directorio principal de Cloud Shell.

Edite el archivo de parámetros que acaba de cargar y cambie la contraseña. Si necesita ayuda para editar el archivo en el Shell, solicite ayuda a su instructor. Como práctica recomendada, los secretos, como las contraseñas, deben almacenarse de forma más segura en Key Vault.

Desde el panel de Cloud Shell, ejecute lo siguiente para crear el grupo de recursos que hospedará las máquinas virtuales (reemplace el [Azure_region]marcador de posición con el nombre de una región de Azure donde pretende implementar máquinas virtuales de Azure). Escriba cada línea de comando por separado y ejecútelas por separado:

```
$location = '[Azure_region]'
```
```
$rgName = 'az104-10-rg0'
```
```
New-AzResourceGroup -Name $rgName -Location $location
```
Desde el panel de Cloud Shell, ejecute lo siguiente para crear la primera red virtual e implementar una máquina virtual en ella usando la plantilla y los archivos de parámetros que cargó:

```
New-AzResourceGroupDeployment `
   -ResourceGroupName $rgName `
   -TemplateFile $HOME/az104-10-vms-edge-template.json `
   -TemplateParameterFile $HOME/az104-10-vms-edge-parameters.json `
   -AsJob
```
Minimice Cloud Shell (pero no lo cierre).

**Nota :** no espere a que se complete la implementación, sino que continúe con la siguiente tarea. La implementación debería tardar unos 5 minutos.