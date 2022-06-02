Firmware - Technical Test

El proyecto fue realizado bajo la documentaciòn encontrada en internet.

Los pasos para la ejecuciòn del proyecto estan descritas a continuaciòn:

-Navegar a la ruta demos\projects\ESPRESSIF\ESP32
-Ejecutar el IDF-CMD y ejecutar idf.py menuconfig
-Seleccionar  Azure IoT middleware for FreeRTOS Main Task Configuration
    para corroborar las configuraciones realizadas para la conexiòn con AZURE
    
    Despues de revisar salir del menuconfig
-Para compilar: Navegar a la ruta demos\projects\ESPRESSIF\ESP32 ejecutar en el IDF-CMD el comando
  
  idf.py --no-ccache -B "C:\espbuild" build
  
-Proceder a flashear la ESP32 con el comando

  idf.py --no-ccache -B "C:\espbuild" -p <Your-COM-port> flash
  
-Posterior ejecutar monitor para corroborar la conexiòn
  
  idf.py -B "C:\espbuild" -p <Your-COM-port> monitor
  
  Lo cual presentara los siguientes logs
  
  I (51057) MQTT: Packet received. ReceivedBytes=2.
  I (51057) MQTT: Ack packet deserialized with result: MQTTSuccess.
  I (51057) MQTT: State record updated. New state=MQTTPublishDone.
  I (51067) AZ IOT: Puback received for packet id: 0x00000008
  I (53067) AZ IOT: Keeping Connection Idle...
  

  Para realizar la visualizaciòn de AZURE
  
  Realice el siguiente procedimiento:
  
  En el siguiente enlace https://apps.azureiotcentral.com/home
  
  Cree una aplicaciòn llamada FIRMWARE TEST
  
  ![image](https://user-images.githubusercontent.com/63884945/171551408-8c29dfd8-0051-4dce-bb71-2aedbb702a46.png)

  Posterior a ello cree un dispositivo con las siguientes credenciales
  
  Ámbito de id. 0ne00629EE9
  Id. de dispositivo:  ESP32_2f4hkegfxcy
  Primary key: qr0QcctAcKkaNlvwjauw8hoOglCKqsZjgg4pvWlz8sI=
  
  
  Por ultimo y tener el dispositivo listo la ESP32 reportara sin problemas en AZURE con el JSON construido de la siguiente manera:
                     {\"temperature\":%0.2f,\"ZONE\":%d,\"Voltage_L1_N\":%0.2f,\"Voltage_L2_N\":%0.2f,\"Voltage_L3_N\":%0.2f,\"Current_L1\":%0.2f,\"Current_L2\":%0.2f,\"Current_L3\":%0.2f,\"Power_Factor_L1\":%0.2f,\"Power_Factor_L2\":%0.2f,\"Power_Factor_L3\":%0.2f,\"cumulativeEnergy\":%0.2f}", (double)13.4,zone,Voltage_L1_N, Voltage_L2_N,Voltage_L3_N,Current_L1,Current_L2,Current_L3,Power_Factor_L1,Power_Factor_L2,Power_Factor_L3, cumulativeEnergy);
  
  Donde se pueden observar las variables:
  
        "ZONE": 2,                   // ZONA QUE CAMBIA DEPENDIENDO DEL MEDIDOR
        "Voltage_L1_N": 305674515,   // VARIABLES RANDOM DE LOS MEDIDORES 
        "Voltage_L2_N": 1864893120,
        "Voltage_L3_N": 1546483181,
        "Current_L1": 3154851462,
        "Current_L2": 1587274491,
        "Current_L3": 1987591009,
        "Power_Factor_L1": 3703565860,
        "Power_Factor_L2": 3582724658,
        "Power_Factor_L3": 575824104,
        "cumulativeEnergy": 1269629183
        "_eventtype": "Telemetría",       //EVENTO DE TELEMETRIA PARA AZURE
        "_timestamp": "2022-06-02T00:02:37.671Z"    //TIEMPO DE REPORTE DEL EVENTO

  
  ![image](https://user-images.githubusercontent.com/63884945/171551982-3ace1ed8-3017-4615-896f-08d84f0908f6.png)
  ![image](https://user-images.githubusercontent.com/63884945/171552005-721bd5b2-35c4-44f6-8cd3-f4670832de78.png)


  
  Por ultimo las funciones principales sobre las cuales se trabajo fueron:
  ruta:
    \demos\sample_azure_iot_pnp
      * linea 93  funcion void PAC3200 (void)
                  Funcion para crear datos random en los medidores
      * linea 510 funcion uint32_t ulCreateTelemetry
                  Duncion para envio de datos a azure
  
  
  
  DIAGRAMA DE CONEXIÒN MODBUS/TCP
  
  ![conexion azure esp32](https://user-images.githubusercontent.com/63884945/171552998-d36a32b3-a905-4a39-8762-f8ed8ee5414e.png)

  
  
  Recurso tomado de: https://github.com/Azure-Samples/iot-middleware-freertos-samples
  

  Gracias por permitirme participar en su proceso de selecciòn.

  
  
  
  
  
  
  

  

