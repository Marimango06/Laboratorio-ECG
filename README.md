# Variabilidad de la frecuencia cardiaca 

Cuando estamos en momentos de estrés o actividad física, en nuestro cuerpo se activa el sistema nervioso simpático, el cual es el encargado de aumentar la frecuencia cardiaca y la fuerza de la contracción del miocardio, lo que produce un mayor gasto cardiaco, mejorando el flujo sanguíneo, el metabolismo celular, entre otras. Por el contrario, cuando nos encontramos más relajados, actúa el sistema nervioso parasimpático, el cual genera un efecto opuesto al anterior, donde disminuye la frecuencia cardiaca, disminución del gasto cardiaco. 

Es importante determinar la relación que tienen estos dos sistemas, ya que ayudan a mantener en equilibrio el cuerpo humano, sin embargo la constancia de activación de alguno de estos sistemas puede indicar algún signo de alarma. Por esta razón, se realiza una medición de la variabilidad de la frecuencia cardiaca, donde se toman las frecuencias altas y bajas, y si las frecuencias altas predominan, quiere decir que se mantiene más activo el sistema simpático, y si por el contrario, predominan las frecuencias bajas se mantendrá mayor mente el sistema parasimpático. De esta misma forma, se puede determinar si una persona se encuentra en niveles de estrés peligrosos para la salud. 

Teniendo en cuenta esta importancia de la variabilidad de la frecuencia,  se realizó un laboratorio donde, se capturó una señal ECG de un paciente joven para posteriormente procesarla. Con el fin de Analizar la variabilidad de la frecuencia cardíaca (HRV) utilizando la transformada wavelet y así identificar cambios en las frecuencias características y analizar la dinámica temporal de la señal cardíaca.

Comenzando con la adquisición de la señal ECG del paciente. Donde se instalaron los electrodos, dos en las clavículas (positivo, negativo) y otro en las costillas (tierra), de la siguiente forma: 

![image](https://github.com/user-attachments/assets/e70e0020-e37c-41dd-bc0e-da89dbc78482)



Esta medición se realizó por medio de un sensor AD8232 y un microcontrolador STM32. Por un intervalo de tiempo de estudio de cinco minutos, donde el paciente debía estar en reposo para reducir el ruido artefacto, con esto, la señal cuenta con una frecuencia de muestreo de 100Hz y un tiempo de muestreo de 1ms.
 
Después de cargar la señal en archivo txt y graficarla en Python se obtuvo lo siguiente:

![image](https://github.com/user-attachments/assets/b88ce50f-aa57-4724-b52f-46862f67ff9f)

Posteriormente se realizó un preprocesamiento de la señal, la cual consiste en filtrar la señal con un filtro butterworth pasa banda de orden 4, con un ancho de banda de 6,2Hz teniendo referente las frecuencias medias del corazón.
Se utilizó este tipo de filtro debido a su respuesta en magnitud plana en la banda de paso, lo que significa que no introduce ondulaciones indeseadas en las frecuencias que se desean conservar. Esto es crucial para mantener la integridad de las características del ECG, como los complejos QRS y las ondas P y T.Adicionalmente se tomaron los parámetros de diseño los cuales son: frecuencia baja de corte: 0,8 Hz; en la frecuencia alta de corte tenemos 8Hz. Con esto se calculo el orden del filtro con la siguiente fórmula:

![image](https://github.com/user-attachments/assets/af70d853-8b09-4cf1-8fd0-4e40d9430936)

Teniendo como resultado: 

![image](https://github.com/user-attachments/assets/2417218c-785b-4efc-8add-f3731f2aeae3)

Es importante conocer que las diferentes ondas que componen el complejo cardíaco reflejan la activación eléctrica del miocardio auricular y ventricular, así como la repolarización ventricular. Teniendo en cuenta la imagen a continuación, sabemos que el complejo QRS hace referencia a la despolarización del nodo auriculoventricular, donde tiene un tiempo de 0.08-0.12s, adicionalmente, con el pico R se puede determinar la frecuencia cardiaca, calculando el tiempo entre los intervalos R-R. sabiendo que la frecuencia cardíaca normal oscila entre 60-100lpm.

![image](https://github.com/user-attachments/assets/c10eea23-28fa-4d96-af78-f87965fa26e1)


Con esto, la variabilidad de frecuencia cardíaca (HRV) refleja la adaptabilidad del corazón a diferentes situaciones y aporta una visión de nuestros niveles de estrés, así como de nuestro estado general de bienestar y salud. Y para calcular esto, se identifican los picos R de cada pulsación cardiaca, y posteriormente calcular el tiempo del intervalo entre cada pico R, y generar un análisis estadístico de estas.

![image](https://github.com/user-attachments/assets/242c72e7-591f-4fd0-8d08-5d4aaaff335f)

Esto con el fin de determinar que tanto varía la frecuencia cardiaca respecto al tiempo, y para ello se encontró la media y la desviación estándar de estos intervalos. Dando como resultado:  
-Media:0,6519
-Desviación estándar: 0,2689

Con el valor de la media de los intervalos R-R se puede determinar la frecuencia cardiaca del paciente siguiendo la siguiente fórmula:

![image](https://github.com/user-attachments/assets/bd00755a-f9d0-4c7f-84c8-82c75a500fbc)

Reemplazando el valor obtenido de la media, tenemos que la frecuencia cardiaca del paciente a estudiar (en latidos por minuto) es de: 92 lpm
   
Por otro lado, la desviación estándar representa la variación de los valores de los intervalos RR. Con un valor elevado de desviación estándar se puede decir que se cuenta con una buena salud cardiaca, ya que es la respuesta activa del sistema autónomo el cual cumple con la capacidad de adaptarse a cambios externos (actividad física, estrés, meditación) con mayor facilidad.  


Por último se realizó un espectrograma de la variabilidad de la frecuencia cardiaca HRV usando la transformada wavelet tipo Morlet. 
Las wavelet son funciones matemáticas que permiten analizar señales en el dominio del tiempo y la frecuencia. A diferencia de las transformadas tradicionales como la de Fourier, que utilizan funciones sinusoidales extendidas en el tiempo, las wavelets son ondas de corta duración y energía finita que se concentran en intervalos específicos de tiempo.
En esta práctica, se utilizó la wavelet tipo morlet, porque combina propiedades de una onda senosoidal con una envolvente gaussiana, lo que le permite concentrar su energía en un rango específico de frecuencias y tiempos. Esto es crucial para el análisis de señales biológicas, donde los fenómenos pueden variar rápidamente y donde se requiere una resolución temporal alta para detectar cambios sutiles en las señales.Esta wavelet tiene la siguiente forma y ecuación.

![image](https://github.com/user-attachments/assets/1a2c2733-ec45-4b4c-b8bb-d3b49688e14f)

![image](https://github.com/user-attachments/assets/d9761368-93f2-4fc1-a7c9-f90781e225ec)

Con esta transformada se obtiene un espectrograma, el cual es una representación visual que muestra cómo varía la energía de las diferentes frecuencias de una señal a lo largo del tiempo. En este ejercicio el resultado de este fue:

(imagen espectrograma)


Con este, se puede analizar la dinámica temporal de la señal cardiaca. Teniendo presente que el eje horizontal representa el tiempo en s, el eje vertical la frecuencia y los colores la potencia o energía de la señal, donde los más brillantes como rojos, reflejan una alta potencia y los tonos azules reflejan la baja potencia. 
Con esta información, se analizaron las frecuencias altas y bajas de esta gráfica:
En las frecuencias bajas 0,04- 0,15:  las frecuencias bajas pueden mostrar cambios que reflejan la variación en la frecuencia cardíaca. Por ejemplo, un aumento en la actividad física puede llevar a un incremento en la frecuencia cardíaca, visible como un aumento en la energía en esta banda. La potencia se mantiene estable, pero puede cambiar significativamente durante el ejercicio o situaciones de estrés, estimulado por el sistema simpático.

En las frecuencias altas 0,15-0,4 tenemos que: pueden mostrar picos transitorios que indican eventos agudos, como extrasístoles o arritmias. Estos picos son importantes para detectar irregularidades en el ritmo cardíaco.Además la potencia espectral en esta banda puede verse afectada por interferencias externas (como ruido eléctrico) y por condiciones fisiológicas como arritmias. 



