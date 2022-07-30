# Práctica 22 - Comunicación por medio de IoT Hub

## Innovaccion Virtual (VII Edición) #IAWizards

### Semana 3 - Sesión 9

En esta práctica se realizó un muestreo de la temperatura y humedad con un Raspberry Pi comunicandolo con el servicio de IoT Hub de Azure.

-----------------------------------------------------------

#### Requerimientos 
- Cuenta de Azure con suscripción.
- Raspberry Pi modelo 3 en adelante.
- Sensor BME280 o similar.
**NOTA:** Si no se cuenta con los recursos físicos necesarios como la Raspberry Pi y el sensor de humedad, puede realizar la práctica a través de un simulador en este [link](https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted).
Si cuenta con los materiales requeridos, puede ver la conexión y como configurar la Raspberry Pi en este [link](https://docs.microsoft.com/es-mx/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).

------------------------------------------------------------

#### Pasos a seguir

1. Accedemos al portal de Azure y buscamos “IoT Hub” y le damos en ‘Centro de IoT’. Le damos en ‘Crear’ y llenamos los datos que nos pide para su creación.

![P22I1](Images\Sesión 9 - P22 01.PNG)

2. Una vez creado, le damos en ‘Ir al recurso’ y nos vamos al apartado de ‘Dispositivos’ y le damos en ‘Agregar dispositivo’. En ‘Id del dispositivo’ podemos poner “SensorTemperatura” mientras que los demás campos los dejamos como están y le damos en ‘Guardar’. Una vez creado, le damos en el dispositivo y veremos un apartado que dice ‘Cadena de conexión principal’. En este apartado copiamos todo el texto que aparece ahí.

![P22I2](Images\Sesión 9 - P22 02.PNG)

![P22I3](Images\Sesión 9 - P22 03.PNG)

![P22I4](Images\Sesión 9 - P22 04.PNG)

3. Accedemos al siguiente sitio web: [https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted](https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted) y nos centramos en la línea número 15 del código de programación, para después remplazar lo que está escrito entre corchetes por el texto que acabamos de copiar. Podremos ver que una vez se halla remplazado el texto por el que copiamos y le damos en ‘Run’, el LED de la pantalla comenzará a parpadear.

![P22I5](Images\Sesión 9 - P22 05.PNG)

4. Abrimos el explorador de archivos y nos ubicamos en alguna carpeta en donde queramos guardar el proyecto clonado que se realizará. Una vez ubicado la carpeta, abrimos el cmd desde ahí y en el navegador accedemos al siguiente link: [https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization](https://github.com/Azure-Samples/web-apps-node-iot-hub-data-visualization) y ubicamos el botón que dice ‘Code’ para después irnos al apartado de ‘Local’ y copiar el texto de SSH.

![P22I6](Images\Sesión 9 - P22 06.PNG)

![P22I7](Images\Sesión 9 - P22 07.PNG)

5. Regresamos al cmd y escribimos “git clone” y seguido pegamos el texto SSH que acabamos de copiar de GitHub y damos enter.

![P22I8](Images\Sesión 9 - P22 08.PNG)

6. Abrimos Visual Studio Code, vamos a ‘File’ y ‘Open Folder’ para después ubicar la carpeta que acabamos de clonar.

![P22I9](Images\Sesión 9 - P22 09.PNG)

7. Vamos al navegador, en la pestaña del portal de Azure y abrimos la terminal. En la terminal escribimos lo siguiente: `az iot hub connection-string show --hub-name ‘nombre’ --policy-name service` donde en ‘nombre’ pondremos el nombre del dispositivo IoT que creamos. Una vez escrito todo eso, damos enter. Si en pantalla muestra una pregunta, colocamos “y” y damos enter. En pantalla, después de un rato mostrará un “connectionString” el cual deberemos guardar para usarlo más adelante.

![P22I10](Images\Sesión 9 - P22 10.PNG)

![P22I11](Images\Sesión 9 - P22 11.PNG)

8. Regresamos a la ventada de cmd y escribimos: `az iot hub consumer-group créate --hub-name ‘nombre’ --name ‘nombregrupo’` donde ‘nombregrupo’ podrá ser cualquier nombre que queramos ponerle al grupo. Al finalizar damos enter. El name que arroje (que será el name que nosotros creamos) lo guardamos, puesto que también se ocupará.

![P22I12](Images\Sesión 9 - P22 12.PNG)

9. Volvemos al VSC e ingresamos al apartado de ‘Terminal’ para escribir `npm install`. Una vez creado, vamos al cmd y hacemos una copia del texto guardado en el paso 6 y pegamos en el cmd, modificándolo un poco, anteponiendo en un principio la palabra “set” luego espacio, y seguido escribimos “IotHubConnectionString=” pegado al texto que teníamos copiado en un principio.

![P22I13](Images\Sesión 9 - P22 13.PNG)

![P22I14](Images\Sesión 9 - P22 14.PNG)

10. Después de haber escrito lo anterior, escribimos “set EventHubConsumerGroup=” y seguido de esto pegamos lo que habíamos guardado en el paso 7.

![P22I15](Images\Sesión 9 - P22 15.PNG)

11. Posteriormente, escribimos el siguiente comando: `cd web-apps-node-iot-hub-data-visualization` y damos enter. Después de esto, escribimos `npm start`.

![P22I16](Images\Sesión 9 - P22 16.PNG)

12. Al finalizar el paso 10, veremos que en el cmd aparece ‘Listening on’ y un número, este número lo copiamos y en el navegador, en una nueva pestaña, escribimos ‘localhost’ y seguido pegamos el número copiado previamente. Con esto, mostrará el trackeo en forma de gráfica de la humedad y temperatura.

![P22I17](Images\Sesión 9 - P22 17.PNG)

13. Para mostrarlo en Azure, tenemos que crear un App Service desde el portal de Azure (también se puede desde la terminal de Azure). Abrimos el servicio y vamos al apartado de ‘Configuración de TLS/SSL’ y en la opción de ‘Solo HTTPS:’ le damos en ‘Activado’.

![P22I18](Images\Sesión 9 - P22 18.PNG)

![P22I19](Images\Sesión 9 - P22 19.PNG)

14. Ahora vamos al apartado de ‘Centro de Implementación’ y a ‘Credenciales GIT o FTPS locales’ y en el apartado de ‘Nombre de usuario’ colocamos el nombre que queramos, y para ‘Contraseña’ colocamos una y le damos en ‘Guardar’. Vamos ahora al apartado de configuración y copiamos el URL de Git Clone.

![P22I20](Images\Sesión 9 - P22 20.PNG)

15. Regresamos a VSC y escribimos en la terminal: “git remote add webapp” y pegamos el link previamente copiado del paso 13. Posteriormente, ponemos: “git push webapp master:master” y colocamos las credenciales que creamos en el paso 13.

16. Volvemos al navegador, al apartado del portal de Azure y vamos al apartado de ‘Configuración’ para agregar una ‘Nueva configuración de la aplicación’. En nombre ponemos: ‘IotHubConnectionScript’ y en valor copiamos y pegamos lo que está después del = del paso 8. Después, ponemos otra configuración de aplicación con los datos de Nombre= EventHubConsumerGroup y Valor= nombre del grupo (paso 7) y le damos en guardar.

17. En el portal de Azure vamos al apartado de Introducción y accedemos al link (URL). Después de un rato mostrará los resultados de la gráfica.