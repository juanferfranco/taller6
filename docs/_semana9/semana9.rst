Semana 9
===========

Trayecto de acciones, tiempos y formas de trabajo
---------------------------------------------------

Fase 6 (RETO-continuación)
^^^^^^^^^^^^^^^^^^^^^^^^^^^
* Fecha: agosto 31 de 2020 - 2 p.m. 
* Descripción: procede con la solución del reto.
* Recursos: para abordar el reto de programación te recomiendo que tengas a la mano el siguiente material

  * Ingresa al grupo de `Teams <https://teams.microsoft.com/l/team/19%3a919658982cb4457e85d706bad345b5dc%40thread.tacv2/conversations?groupId=16c098de-d737-4b8a-839d-8faf7400b06e&tenantId=618bab0f-20a4-4de3-a10c-e20cee96bb35>`__.
    para resolver dudas en tiempo real con el docente.
  * Continua trabajando en el RETO en tus horas de trabajo autónomas.

* Duración de la actividad: 
  
  * 1 hora 40 minutos con solución de dudas en tiempo real.
  * 3 horas de trabajo autónomo

* Forma de trabajo: individual.


Fase 7 (sustentación):
^^^^^^^^^^^^^^^^^^^^^^^^^
* Fecha: septiembre 1 de 2020
* Descripción: realiza el video de sustentación.
* Recursos: para realizar el video de sustentación te recomiendo los siguientes recursos
  
  * Software para capturar `OBS Studio <https://obsproject.com/>`__.
  * Ver `este <https://www.youtube.com/watch?time_continue=3&v=1tuJjI7dhw0>`__
    tutorial para el manejo de OBS Studio.

* Duración de la actividad: 2 horas de trabajo autónomo
* Forma de trabajo: individual

Fase 8 (retroalimentación): 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
* Fecha: septiembre 2 de 2020 - 2 p.m.
* Descripción: encuentro sincrónico para compartir y discutir los resultados del RETO. 
* Recursos: ingresa al grupo de `Teams <https://teams.microsoft.com/l/team/19%3a919658982cb4457e85d706bad345b5dc%40thread.tacv2/conversations?groupId=16c098de-d737-4b8a-839d-8faf7400b06e&tenantId=618bab0f-20a4-4de3-a10c-e20cee96bb35>`__
* Duración de la actividad: 
  
  * 50 minutos de discusión.
  * 50 minutos para que hagas las acciones de mejora sobre tu trabajo.

* Forma de trabajo: colaborativo con solución de dudas en tiempo real y trabajo individual en la acción de mejora.

Criterios de evaluación
------------------------
1. Criterio: integro dispositivos de entrada-salida con sistemas de cómputo para la
   creación de sistemas intermediados por el entretenimiento digital (Materialización).

2. Criterio: aplico los conceptos necesarios para el correcto diseño, implementación,
   funcionamiento y 
   diagnóstico del software en la producción de sistemas de entretenimiento digital utilizando los procedimientos y herramientas adecuadas según el contexto (Ingeniería de software).

Esta actividad tendrá un porcentaje sumativo del 20% en la nota final.


..
  Sesión 1
  ----------
  Continuareamos analizando el material sobre hilos `aquí <http://www.albahari.com/threading/>`__

  Sesión 2
  ----------
  Vamos a realizar los siguientes ejercicios para introducir la necesidad de contar con hilos
  al utilizar entrada salida.

  Ejercicio 1
  ^^^^^^^^^^^^

  Un ejercicio extra para comenzar a calentar, sin hilos aún.
  La idea del ejercicio es comunicar a través del puerto serial
  el computador con un arduino, en este caso, un ESP32. Si desea
  trabajar en visual studio solo se requiere crear una aplicación
  .NET framework tipo consola. En caso de utilizar .netcore se pueden
  seguir los siguientes pasos en la terminal:

  * mkdir dotNetTest
  * cd dotNetTest
  * dotnet new console
  * En la siguiente línea, antes de versión tenemos doble guión. Ojo se ve como
    un solo guión, pero son dos.
  * dotnet add package System.IO.Ports --version 4.7
  * code .
  * copiar el código
  * dotnet build
  * dotnet run

  Este es el código para programar en el arduino:

  .. code-block:: cpp
    :lineno-start: 1

      void setup() {
        Serial.begin(115200);
      }

      void loop() {

        if(Serial.available()){
          if(Serial.read() == '1'){
            Serial.print("Hello from ESP32");
          }
        }
      }


  Este es el código para programar en el computador:

  .. code-block:: csharp
    :lineno-start: 1

      using System;
      using System.IO.Ports;

      namespace hello_serialport{
          class Program{
              static void Main(string[] args)
              {
                  SerialPort _serialPort = new SerialPort();
                  // Allow the user to set the appropriate properties.
                  _serialPort.PortName = "/dev/ttyUSB0";
                  _serialPort.BaudRate = 115200;
                  _serialPort.DtrEnable = true;
                  _serialPort.Open();
                  byte[] data = {0x31};
                  _serialPort.Write(data,0,1);
                  byte[] buffer = new byte[20];

                  while(true){
                      if(_serialPort.BytesToRead > 0){
                          _serialPort.Read(buffer,0,20);
                          Console.WriteLine(System.Text.Encoding.ASCII.GetString(buffer));
                          Console.ReadKey();
                          _serialPort.Write(data,0,1);
                      }
                  }
              }
          }
      }

  Ejercicio 2
  ^^^^^^^^^^^^
  Este es el código para programar en el arduino:

  .. code-block:: cpp
    :lineno-start: 1

      void setup() {
        Serial.begin(115200);
      }

      void loop() {

        if(Serial.available()){
          if(Serial.read() == '1'){
            delay(1000);
            Serial.print("Hello from ESP32\n");
          }
        }
      }

  Este es el código para programar el computador

  .. code-block:: cpp
    :lineno-start: 1

      using System;
      using System.IO.Ports;
      using System.Threading;

      namespace serialTestBlock
      {
      class Program{
              static void Main(string[] args)
              {
                  SerialPort _serialPort = new SerialPort();
                  _serialPort.PortName = "/dev/ttyUSB0";
                  _serialPort.BaudRate = 115200;
                  _serialPort.DtrEnable = true;
                  _serialPort.Open();

                  byte[] data = {0x31};
                  byte[] buffer = new byte[20];
                  int counter = 0;

                  while(true){
                      if(Console.KeyAvailable == true){
                          Console.ReadKey(true);
                          _serialPort.Write(data,0,1);
                          string message = _serialPort.ReadLine();
                          Console.WriteLine(message);
                      }
                      Console.WriteLine(counter);
                      counter = (counter + 1) % 100;
                      Thread.Sleep(100);
                  } 
              }   
          }
      }

  * Conecte el arduino.
  * Modifique el código del computador asignando el puerto
    serial correcto.
  * Corra el código del computador.
  * Al presionar cualquier tecla qué pasa?

  Ejercicio 3: Reto
  ^^^^^^^^^^^^^^^^^^
  Con lo que hemos discutido hoy cómo podríamos solucionar el
  problema anterior, considerando que no es posible (por el
  ejercicio académico) modificar el código de Arduino?

  .. warning::
    Alerta de spoiler

    El siguiente código muestra una posible solución al reto

  .. code-block:: csharp
    :lineno-start: 1

      using System;
      using System.IO.Ports;
      using System.Threading;

      namespace SerialTest
      {
          class Program
          {
              static void Main(string[] args)
              {

                  int counter = 0;

                  Thread t = new Thread(readKeyboard);
                  t.Start();

                  while (true)
                  {
                      Console.WriteLine(counter);
                      counter = (counter + 1) % 100;
                      Thread.Sleep(100);
                  }
              }

              static void readKeyboard()
              {

                  SerialPort _serialPort = new SerialPort(); ;
                  _serialPort.PortName = "COM4";
                  _serialPort.BaudRate = 115200;
                  _serialPort.DtrEnable = true;
                  _serialPort.Open();

                  byte[] data = { 0x31 };

                  while (true) {     
                      if (Console.KeyAvailable == true)
                      {
                          Console.ReadKey(true);
                          _serialPort.Write(data, 0, 1);
                          string message = _serialPort.ReadLine();
                          Console.WriteLine(message);
                      }
                  }
              }
          }
      }

  Ejercicio 4: Reto
  ^^^^^^^^^^^^^^^^^^^^
  Este ejercicio lo podemos comenzar en la sesión 2 y la idea
  es terminarlo en las horas de trabajo autónomas:

  Asuma que un arduino tiene conectados varios sensores y actuadores así:

  * Dos sensores digitales
  * Dos sensores analógicos: valores de 0 a 1023
  * Dos actuadores digitales.
  * Dos actuadores analógicos.

  A su vez el arduino se conecta a un computador a través del puerto USB y se comunica 
  utilizando la interfaz Serial. Realice un programa, en el arduino, que realice las siguientes tareas 
  concurrentes:

  * Recibir comandos a través de la interfaz Serial
  * Enciende y apaga un LED a una frecuencia de 10 Hz
  * Enciende y apaga un LED a una frecuencia de 5 Hz.

  Los comandos recibidos por el puerto serial serán los siguientes:

  * read D1. Este comando hace que se envie al PC el valor del sensor digital 1. 
    El arduino devuelve la cadena:  D1 estado. Donde estado puede ser 1 o 0.

  * read D2: enviar al PC el valor del sensor digital 2.  
    El arduino devuelve la cadena: D2 estado. Donde estado puede ser 1 o 0.

  * read A1: enviar el PC el valor del sensor analógico 1.  
    El arduino devuelve la cadena A1 valor. Donde valor está entre 0 y 1023.

  * read A2: enviar el PC el valor del sensor analógico 2. 
    El arduino devuelve la cadena A2 valor. Donde valor está entre 0 y 1023.

  * write O1 estado: donde estado puede ser 1 o 0. 
    Activa o desactiva la salida digital 1 

  * write O2 estado: donde estado puede ser 1 o 0. 
    Activa o desactiva la salida digital 2 

  * write P1 valor: donde valor puede ser de 0 a 255. 
    Escribir un valor de PWM igual a valor en el actuador analógico 1. 

  * write P2 valor: donde valor puede ser de 0 a 255. 
    Escribir un valor de PWM igual a valor en el actuador analógico 2.

  La aplicación del computador es tipo consola en C# y debe tener:

  * Dos hilos.
  * Un hilo debe imprimir cada 100 ms el valor de un contador.
  * Otro hilo pendiente de los eventos del teclado.
  * Asigne una tecla a cada comando que será enviado al arduino.
  * Indicar si el arduino entendió o no entendió el comando, es decir,
    mostrar el NACK o el ACK.

  NOTAS:

  Para cualquier de los comandos write el arduino debe devolver ACK si reconoce el comando y 
  NACK si no lo reconoce. Usted debe decidir, dados los requisitos de la aplicación, 
  si requiere introducir caracteres de nueva línea y/o retorno de carro. 
  TENGA PRESENTE que LOS LEDs deben funcionar SIEMPRE a 5 Hz y 10 HZ como se declaró previamente, 
  ese decir, su funcionamiento no puede ser interrumpido por las operaciones del puerto serial


