# Creación de maquinas virtuales

Esta sección contiene 2 partes:
- [Máquinas Virtuales](#aprendamos-un-poco-sobre-las-máquinas-virtuales)
- [Laboratorio 3](#laboratorio-3-creación-de-máquinas-virtuales)

## Aprendamos un poco sobre las máquinas virtuales 

Oracle Cloud Infrastructure permite aprovisionar y gestionar hosts de cómputo conocidos como instancias. Puedes crear instancias según sea necesario para satisfacer tus requisitos de cómputo y aplicaciones. Después de crear una instancia, puedes acceder a ella de forma segura desde tu computadora, reiniciarla, adjuntar y desvincular volúmenes y cerrarla cuando ya no la necesites. Esto proporciona flexibilidad y escalabilidad para satisfacer las necesidades de tu infraestructura de TI en la nube.

Para saber más, puedes consultar la documentación de OCI 🤓➡️ https://docs.oracle.com/en-us/iaas/Content/Compute/Concepts/computeoverview.htm

## Laboratorio 3: Creación de máquinas virtuales

En este laboratorio, aprenderás a crear 2 máquinas virtuales Linux.

_**Tiempo estimado para el laboratorio**_: 35 minutos

Objetivos:
- Crear un par de claves SSH en OCI Cloud Shell
- Crear 2 máquinas virtuales (VM) Linux
- Acceder a las instancias

**Cada máquina virtual debe estar en un AD diferente**. Para ellos seguiremos los siguientes pasos:
- [Paso 1: Crear un par de llaves SSH](#paso-1-crear-un-par-de-llaves-ssh)
- [Paso 2: Crear 2 máquinas virtuales Oracle Linux](#paso-2-crear-2-máquinas-virtuales-oracle-linux)
- [Paso 3: Acceder a la VM por el terminal](#paso-3-acceder-a-la-vm-por-el-terminal)

### Paso 1: Crear un par de llaves SSH

1. Acceda al escritorio remoto en su VCN haciendo click en **Launch Remote Desktop** o simplemente acceda a la pestaña <NoVNC> si ya está abierta. 

 ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-1.png)
 ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-2.png)
 
 Si la terminal no está abierta, puede abrirla nuevamente.
 ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-3.png)
 
 > **Nota:** Use el Portapapeles de NoVNC para facilitar la copia dentro y fuera de la Terminal. De ahora en adelante, siempre que necesites copiar/pegar algo a la Terminal, y también desde la Terminal hacia afuera, usa el Portapapeles.
 
 ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-4.png)

2. Para crear el par de llaves usamos el comando:

   ```
   ssh-keygen -t rsa
   ```
   - Mantenga el nombre original de la llave (id_rsa) aprentando enter
   - El campo "Key Passphrase" es opcional
   - Click "ENTER" nuevamente para finalizar la creación

   ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-5.png)

3. Para ver el contenido de la llave pública, ejecuta este comando:
   
   ```
   cat ~/.ssh/id_rsa.pub
   ```
  > **Nota:** Si no sabes la combinación de teclas para el símbolo "~" (virgulilla), busca el símbolo y copialo en el área de transferencia del Escritorio Remoto. Luego de ello, pégalo dentro del terminal usando _clic derecho + pegar_. Puedes hacer esto para facilitar el copiado/pegado de texto entre tu escritorio y el escritorio remoto.

   ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-6.png)

  * Seleccione el contenido en la terminal y utilice el botón derecho del mouse para copiarlo.
    ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-7.png)

  * Seleccione, copie y pegue el cnotenido de esta llave en el Portapapeles/Clipboard como se muestra en la imagen de abajo, y si es posible guárdelo en un bloc de notas, ya que lo usaremos para crear las máquinas virtuales Linux.
    ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-8.png)

    
  _Para la creación de la VM, usaremos una llave pública y para la conexión, usaremos la llave privada_
  
     
### Paso 2: Crear 2 máquinas virtuales Oracle Linux

1. Volviendo a la consola de OCI, en el menú principal, haga click en: Compute > Instances , a continuación **Create Instance**
   > **Nota:** Verificar que su compartimiento esté seleccionado antes de crear la instancia

   ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-9.png)
   
   ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-10.png)

   > **Nota:** Antes de crear las instancias, verifique en que AD se creo su máquina NoVNC y luego use los otros 2 AD para crear las máquinas virtuales
   
   > **Ejemplo:** en la imagen a continuación, puede ver que la máquina NoVNC se creó en AD-2, esto significa que aún puede usar los AD-1 y AD-3 para crear cada una de las máquinas. Este diagraa solo se aplica al entorno sandbox del taller LiveLabs. En entornos reales, puede crear recursos en cualquier AD, siempre que se cumplan los límites y políticas necesarias.

   ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-11.png)

    Estos serán los datos de tu instancia:
    * Nombre de tu instancia: VM-OracleLinux-1
    * Availability Domain (AD): Elija uno que no esté siendo utilizado por la VM NoVNC
    * Sistema Operativo: Oracle Linux 8
    * Tipo de Instancia: Virtual Machine
    * Instance Shape: AMD VM.Standard.E5.Flex
    * Elija llave SSH: Insertar archivo de clave pública SSH (.pub)
    * Virtual Cloud Network Copartment: "Su Compartimento"
    * Virtual Cloud Network: "Tu VCN"
    * Subnet Compartment: "Tu Compartimento" (Creado por defecto en el ambiente)
    * Subnet: Subred Pública

     Llena los datos según lo indicado. **Recuerda que ya tienes un compartment creado por defecto. Debes elegir ese** 🤓☝️
   
   ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-12.png)

2. Después de expandir las opciones de Shapes and Network, ingrese los datos necesarios para concluir el proceso de creación
   ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-13.png)

   ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-14.png)

   ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-15.png)

   ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-16.png)

   ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-17.png)


3. Al ingresar la información de Networking, recuerda elegir tu VCN (Lab2), tu Subnet pública (Lab2) y la opción **Automatically assign public IPv4 address**
   ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-18.png)
  

4. Copie desde el Portapapeles/Clipboard y pegue la llave pública SSH creada por usted en la Tarea 1 de este laboratorio como se muestra en la imagen a continuación y haga click en **Create**
   ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-19.png)

   ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-20.png)

   ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-21.png)

   ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-22.png)

   ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-23.png)

   Su instancia se creará correctamente en unos minutos. Una vez finalizado el proceso de creación, la pantalla principal se verá asi:
   ![imagen](../Lab3-MaquinasVirtuales/imagenes/vm-running.png)

     

6. Realizamos los mismos pasos para crear la VM2. La crearemos en el AD que queda disponible.
   Estos serán los datos de su instancia:
    * Nombre de tu instancia: VM-OracleLinux-2
    * Availability Domain (AD): Seleccione AD que falta, es decir, que no esté siendo utilizado por la VM NoVNC o por VM-OracleLinux-1
    * Sistema Operativo: Oracle Linux 8
    * Tipo de Instancia: Virtual Machine
    * Instance Shape: AMD VM.Standard.E5.Flex
    * Elija llave SSH: Insertar archivo de clave pública SSH (.pub)
    * Virtual Cloud Network Copartment: "Su Compartimento"
    * Virtual Cloud Network: "Tu VCN"
    * Subnet Compartment: "Tu Compartimento" (Creado por defecto en el ambiente)
    * Subnet: Subred Pública
      
   > **Nota:** Utilice la misma llave pública para ambas VMs
   

  ### Paso 3: Acceder a la VM por el terminal

  1. Navegue por medio del menu a Compute > Instances y copie la IP privada de la instancia
     
     ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-9.png)

     ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-25.png)

     

  2. En la terminal de la VM NoVNC, conectese a la máquina creada (VM-OracleLinux1) usando el siguiente comando:

     ```
     ssh opc@<ip privada VM>
     la llave ya se encuentra registrada a nivel de SO
     en caso de que de algún problema probar lo siguiente:
     ssh -i <llave privada ssh> opc@<ip privada VM> // ejemplo: ssh -i id_rsa opc@10.0.0.94
     ```

     * El usuario por defecto de las instancias Linux es **opc**
     * Pruebe también el acceso a la VM-OracleLinux-2 posteriormente

     ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-26.png)

     > **Nota:** Para desconectarse de la VM en el terminal NoVNC utilice el comando **logout**
  
  
  3. Al completar esta tarea, verá que ahora tenemos 2 instancias de computo creadas junto con la instancia NoVNC, cada una en su propio dominio de disponibilidad (AD)

     ![imagen](../Lab3-MaquinasVirtuales/imagenes/compute-27.png)

     

     **Super! Continuemos con el siguiente laboratorio 🤩👉 [Laboratorio 4 - Block Volume](https://github.com/mcrsoci/OCI-Fast-Track-v2/tree/main/Lab4-BlockVolume)**
   
   
