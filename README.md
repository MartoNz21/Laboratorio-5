# Laboratorio-5

Introducción 


En este laboratorio se realizó con el objetivo de analizar una señal de la actividad eléctrica del corazón y su frecuencia cardiaca afectada por el sistema simpático y parasimpático, analizando su variabilidad (HRV) a través de los intervalos R-R el cual nos indica el equilibrio o desequilibrio del sistema nervioso autónomo, donde se utilizaron herramientas para su procesamiento como un filtrado digital a la señal capturada por un tiempo de aproximadamente 5 minutos en estado de reposo, para eliminar frecuencias de interferencia para detectar el HVR , utilizamos también la transformada wavelet para observar cómo varían las bandas de baja y alta frecuencia a lo largo del tiempo. 



# 1. Fundamento teórico 
El sistema nervioso autónomo (SNA) comprende dos divisiones principales: el sistema simpático y el parasimpático. El simpático, también conocido como "lucha o huida", prepara el cuerpo para situaciones de estrés o emergencia, aumentando la frecuencia cardíaca y respiratoria, entre otras funciones. El parasimpático, por otro lado, promueve el estado de relajación y descanso, facilitando la digestión y disminuyendo la frecuencia cardíaca.
La Variabilidad de la Frecuencia Cardiaca (VFC) se refiere a las fluctuaciones en el intervalo R-R del electrocardiograma (ECG), que refleja la interacción entre el sistema nervioso autónomo y la frecuencia cardiaca. En este análisis, las frecuencias de interés son la baja frecuencia (LF, 0.04-0.15 Hz), la alta frecuencia (HF, 0.15-0.5 Hz) y la muy baja frecuencia (VLF, <0.04 Hz), cada una asociada a diferentes mecanismos fisiológicos. 
La transformada wavelet es una herramienta matemática utilizada para analizar señales no estacionarias, es decir, aquellas cuyos componentes frecuenciales cambian con el tiempo, como es el caso de muchas señales biológicas. A diferencia de la transformada de Fourier, que descompone una señal en senos y cosenos infinitamente largos, la transformada wavelet utiliza funciones oscilatorias de duración finita llamadas wavelets.
La transformada wavelet representa una señal en función del tiempo y la frecuencia a la vez, proporcionando una mejor resolución temporal para frecuencias altas y una mejor resolución frecuencial para frecuencias bajas. Existen dos formas:

Transformada Wavelet Continua (CWT): útil para análisis detallados y espectrogramas.

Transformada Wavelet Discreta (DWT): más eficiente para compresión y detección de eventos.

Usos en señales biológicas:
- Análisis de la variabilidad de la frecuencia cardíaca (HRV).

- Detección de picos R en ECG.

- Identificación de patrones en EEG, EMG y otras señales fisiológicas.

- Detección de eventos transitorios o anómalos en registros médicos.

Tipos comunes de wavelets en señales biológicas:
- Morlet (compleja): ideal para análisis de HRV en frecuencia, ya que tiene buena resolución en ambas dimensiones.

- Daubechies (db4, db6, etc.): excelente para detección de picos y compresión de señales.

- Coiflet y Symlet: similares a Daubechies, pero con mejor simetría, usadas en análisis ECG.

- Biorthogonal: útil en codificación y reconstrucción sin pérdida de señales fisiológicas.


![image](https://github.com/user-attachments/assets/0ea734e7-a24a-43ec-ba50-ab2b517a5df2)


# 2. Adquisición de la señal ECG
Para el proceso de adquisición de la señal principalmente se conecta un sensor a un microcontrolador el cual se ve alimentado por un computador, este sensor toma la señal a partir de un conversor análogo digital y envía la señal a través de un transmisor del puerto, el puerto recibe la información y esta finalmente es recibida en un código el cual toma la información captada del adc, guardando la información para que
# 3. Pre-procesamiento de la señal

En esta etapa iniciamos aplicando el filtro digital necesario para eliminar el ruido de la señal, debido a que tiene ruido de bajas y altas frecuencias, aplicamos un filtro pasa banda de 0.5 a 40 Hz, lo cual nos permite dejar la frecuencia que necesitamos limpia, siendo el QRS de la señal ECG 


![image](https://github.com/user-attachments/assets/e9326c06-ad65-46d5-8237-0791341efe79)


Diseñamos un filtro IIR basándonos en los parámetros de la señal, para el cual debemos hallar sus coeficientes b y a, de lo que se obtiene un filtro IIR de  orden 4, con frecuencias normalizadas entre 0.5 Hz y 40 Hz. El filtro Butterworth fue elegido por su respuesta suave sin ondulaciones en la banda pasante. 
Ya con el filtro IIR, a partir de sus coeficientes podemos obtener la ecuacion en diferencias que describe la señal


![image](https://github.com/user-attachments/assets/2a7698bd-b8f3-450f-8b9d-844b6d75a937)


![image](https://github.com/user-attachments/assets/3d244483-3a1f-489a-a2ab-1ddf18f0399d)


 Para calcular cada salida y[n] a partir de las entradas x[n-i] pasadas y salidas pasadas y[n-i].
Se implementa el filtro a la señal obtenida asumiendo parámetros iniciales en 0


![image](https://github.com/user-attachments/assets/246a0629-76ed-4237-a203-5bf165cc150c)


Aquí ya es implementado el filtro IIR en forma directa I desde cero, asumiendo que todos los valores pasados son cero.

Por ultimo en esta etapa se identifican los picos R, y se calculan los intervalos R-R para obtener nueva señal


![image](https://github.com/user-attachments/assets/15bac808-5014-4e17-9e00-61715c221431)


Gracias a la obtención del tiempo entre los intervalos R-R se puede dar paso al análisis de HRV en el dominio del tiempo y frecuencia.

# 4. Análisis de la HRV en el dominio del tiempo
Los parámetros básicos para el HVR en el dominio del tiempo, como la media de los intervalos R-R y su desviación estándar, los calculamos de esta forma:

![image](https://github.com/user-attachments/assets/79173763-9d05-4669-adb4-797c19a0ec64)

![image](https://github.com/user-attachments/assets/63c7339a-2af3-45cc-99e9-c00b0a2f0a6b)


Para el análisis de estos parámetros nos apoyamos con esta gráfica la cual nos permite la visualización temporal de los intervalos R-R, para observar la variación de los latidos a lo largo del tiempo.


![image](https://github.com/user-attachments/assets/0143e7ad-782e-46cd-91af-283e07b1b6f8)


![image](https://github.com/user-attachments/assets/aabfb28e-486a-4b16-b997-4a689462c659)

Con lo cual podemos observar si hay estabilidad o fluctuaciones significativas en los latidos.
La media nos dice cuánto tiempo pasa, en promedio, entre un latido del corazón y el siguiente. La desviación estándar (SDRR) nos muestra cuánto varía ese tiempo entre latidos. Si los intervalos R-R cambian mucho, la SDRR será alta, lo que normalmente es bueno porque indica que el cuerpo se adapta bien a diferentes situaciones (como al respirar o moverse). En cambio, si los intervalos cambian poco y están todos muy parecidos, la SDRR será baja, lo que puede ser señal de estrés o problemas en el control del ritmo cardíaco por parte del sistema nervioso.


![image](https://github.com/user-attachments/assets/709a9869-0d24-4bf2-81a5-586371811805)

 






