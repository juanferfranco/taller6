Semana 8
===========

Trayecto de acciones, tiempos y formas de trabajo
---------------------------------------------------

Fase 6 (RETO)
^^^^^^^^^^^^^^^^^^^^^
* Fecha: agosto 24 y agosto 26 de 2020 - 2 p.m. 
* Descripción: procede con la solución del reto.
* Recursos: para abordar el reto de programación te recomiendo que tengas a la mano el siguiente material

  * Ingresa al grupo de `Teams <https://teams.microsoft.com/l/team/19%3a919658982cb4457e85d706bad345b5dc%40thread.tacv2/conversations?groupId=16c098de-d737-4b8a-839d-8faf7400b06e&tenantId=618bab0f-20a4-4de3-a10c-e20cee96bb35>`__.
    para resolver dudas en tiempo real con el docente.
  * Continua trabajando en el RETO en tus horas de trabajo autónomas.

* Duración de la actividad: 
  
  * Dos sesiones de 1 hora 40 minutos cada una para solución de dudas en tiempo real.
  * 5 horas de trabajo autónomo: 3 horas entre agosto 24 y 26 y 2 horas más luego de agosto 26.

* Forma de trabajo: individual.



..
    Hasta este punto del curso, la aplicación interactiva que se
    comunica con el sensor/actuador la hemos simulando con
    una terminal ascii (monitor de arduino) o una terminal binaria
    (Coolterm); sin embargo, ha llegado el momento de abordar los
    problemas de integración que se deben enfrentar a la hora de
    escribir aplicaciones interactivas que interactúan en tiempo real
    con el contenido digital y con información proveniente de sensores.

    En este punto aparece un mundo de posibilidades relacionadas con
    el origen del sensor, es decir, el sensor puede estar conectado
    a la misma plataforma de cómputo en la cual corre la aplicación
    interactiva o puede estar en otra plataforma de cómputo
    independiente. Adicionalmente, las plataformas de cómputo pueden
    estar conectadas por medios alambrados o inalámbricos; pueden estar
    en el mismo espacio o incluso en cualquier lugar del planeta.

    En sensores 1 nos concentraremos en la comunicación entre la
    aplicación interactiva y el sensor conectados a través de un puerto
    serial. En sensores 2 abordaremos las otras posibilidades mencionadas.

    Para comenzar esta exploración debemos introducir algunos conceptos
    traídos de los sistemas operativos: procesos, hilos, espacios de memoria
    virtual, máquinas virtuales. Además, usaremos como plataforma de
    experimentación Unity y por tanto C#.

    Sesión 1
    ----------

    Vamos a presentar el concepto de hilo y la relación entre otros
    conceptos estudiados en la carrera relativos a la programación orientada
    a objetos. Para ello vamos a revisar partes de `este <http://www.albahari.com/threading/>`__
    sitio y `esta <https://drive.google.com/file/d/1kYL85ThVU5xJmCiCPDVskS-UI4Y5jDde/view?usp=sharing>`__
    presentación de Samy Zafrany tomada de `este <https://samyzaf.com/braude/OS/index.html>`__
    sitio.

    Vamos a complementar con el material de estos sitios:

    * `¿Qué es el .NET? <https://dotnettutorials.net/lesson/dotnet-framework/>`__
    * `¿Qué es el CLR? <https://dotnettutorials.net/lesson/common-language-runtime-dotnet/>`__
    * `¿Cómo se ejecuta un programa .NET? <https://dotnettutorials.net/lesson/dotnet-program-execution-process/>`__

    Y de estos otros, que muestran la relación con Unity:

    * `IL2CPP <https://docs.unity3d.com/Manual/IL2CPP.html>`__
    * `¿Cómo funciona IL2CPP <https://docs.unity3d.com/Manual/IL2CPP.html>`__

    Sesión 2
    ----------
    En esta sesión comenzamos a analizar el material relacionado con la programación multihilada que está
    `aquí <http://www.albahari.com/threading/>`__

