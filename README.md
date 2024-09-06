# STM32_Matlab_Control_Motor_DC
Explora las capacidades avanzadas de STM32, destacando su velocidad de procesamiento, capacidad de control en tiempo real.
# Descripción del Proyecto
En este proyecto, exploramos y desarrollamos un sistema de control On/Off para un motor utilizando tarjetas STM32. Abordamos aspectos clave del diseño, implementación y análisis del controlador, destacando las características específicas de las tarjetas STM32 y su aplicación en el control de motores.
# Objetivos Principales
- Investigar y comprender los principios de funcionamiento de las tarjetas STM32 y su integración en sistemas de control.

- Diseñar e implementar un controlador On/Off eficiente para el motor, aprovechando las capacidades y características de las tarjetas STM32.

- Analizar el rendimiento del sistema de control en términos de precisión, eficiencia y estabilidad.

# Contenido del Repositorio
- Documentación detallada sobre el diseño y la implementación del controlador On/Off.

- Código fuente, incluyendo programas en lenguaje C específicamente desarrollados para tarjetas STM32.

- Diagramas, esquemas y recursos adicionales relacionados con el proyecto.

- Instrucciones de configuración y uso del sistema de control.

# Conexion STM32 y simulink
En este proyecto se ocupo el STM32F407G Discovery, para iniciar la conexión entre Matlab-Simulink y el microcontrolador STM32, es esencial contar con los controladores adecuados. Afortunadamente, estos controladores se pueden encontrar en la página oficial de Matlab. Descargar e instalar estos controladores es el primer paso crucial para establecer una comunicación efectiva entre nuestra aplicación en Matlab-Simulink y el STM32. Una vez que hayamos asegurado la instalación correcta de los controladores, estaremos listos para proceder con el desarrollo y la implementación de nuestro proyecto en el siguiente link podemos obtener los drivers para crear el vinculo entre STM32 y simulink https://www.mathworks.com/matlabcentral/fileexchange/43093-embedded-coder-support-package-for-stmicroelectronics-stm32-processors.

# Pruebas
Una de las primeras pruebas que se hicieron en proyecto 
# Contribuciones
¡Las contribuciones son bienvenidas! Si estás interesado en colaborar o tienes sugerencias para mejorar este proyecto, no dudes en abrir un problema o enviar una solicitud de extracción. Juntos, podemos hacer que este repositorio sea una valiosa fuente de información para la comunidad interesada en el control de motores con tarjetas STM32.

En esta prueba se fue obtener señales desde la STM32 en este caso lo que se hizo desde un boton.
![image](https://github.com/user-attachments/assets/50567cb5-d860-4f84-992f-fbc817f938c3)

La siguiente imagen muestra los diagramas de bloque se ocuparon la obtener la señal y el pequeño programa que se ocupo para obtener la señal en el diagrama de blquen FCN.

![image](https://github.com/user-attachments/assets/7ed1e08f-1096-4b6e-8e01-f7d846b330e7)
```
function y = fcn (u)
    x = u*100;
y= x;
 ```
Lo que obtendremos de nuestra señal se podra ver representada de la siguiente manera en la siguiente grafica, mientras no se pulse el boton la señal estara en el rango de 20 - 90 cuando sea pulsada la señal sera 0.
![image](https://github.com/user-attachments/assets/49b242c8-553a-43b2-a993-440d119886c6)
Con esto podemos crear un contador y obtener cuantas veces se a pulsado el boton.
```
fuction y= fcn(u)
  persistent contador;

  if isemty(contador)
    contador = 0;
end
if  u == 0 && u < 20 || u > 80
  contador = contador + 1;
end
y= contador;
end
```
![image](https://github.com/user-attachments/assets/1fca2c6b-52e2-45c3-b74e-7ff709355465)

La sieuguiente prueba ya fue con el motor en donde le manderemos la señal del motor para poder vizualizar las vueltas y posteriormente poder calcular la velocidad del motor la siguiente imagen es la de nuestro diagrama de bloques para el motor.
![image](https://github.com/user-attachments/assets/ca4f8884-533a-4ee1-a0cf-90d61e4dbc88)

```
function y = fcn(u)
 persistent contador ;

 if isempty ( contador )
   contador = 0;
 end

% L o g i c a para contar cuando se detecta un pulso del motor
 if u == 1
   contador = contador + 1;
 end

% Devolver el valor actual del contador
 y = contador ;
 end
```
![image](https://github.com/user-attachments/assets/c23e2d3e-f8b3-4ccc-98fa-6302d2397a3f)
Como finalizacion de proyecto lo que se logro hacer fue controlar la velocidad desde matlab, obtener la velocidad del motor en tiempo real y poder hacer el cambio de giro del motor, todo esto desde matlab, la siguiente imagen muestra como se logro crear todo esto con los diagramas de bloque.
![image](https://github.com/user-attachments/assets/7d687d52-29e6-44a6-be87-741094085325)
## Programa en donde podemos obtener la velocidad del motor
```
function y = fcn(u, tiempo)
  persistent contador;

  if isempty(contador)
    contador = 0;
  end

  % Lógica para contar cuando se detecta la pulsación del botón
  % Modifica esta lógica según cómo se detecta la pulsación en tu sistema
  if u == 1 % Suponiendo que 1 representa la pulsación del botón
    contador = contador + 1;
  end

  % Convertir el número de pulsaciones a radianes (2π radianes por pulsación)
  radianes = contador * 0.95 * 2 * pi;

  % Calcular la velocidad angular (radianes por segundo)
  velocidad_angular = radianes / tiempo;

  % Convertir la velocidad angular a revoluciones por segundo
  velocidad = velocidad_angular * 60 / (2 * pi);

  % Devolver la velocidad
  y = velocidad;
end
```
Para el giro del motor ocupamos estos diagramas de bloque.
![image](https://github.com/user-attachments/assets/0d2a7ec3-4ff4-4768-9ee7-8dca59778014)
