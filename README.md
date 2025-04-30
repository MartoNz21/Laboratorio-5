# Laboratorio-5

Introducción 


En este laboratorio se realizó con el objetivo de analizar una señal de la actividad eléctrica del corazón y su frecuencia cardiaca afectada por el sistema simpático y parasimpático, analizando su variabilidad (HRV) a través de los intervalos R-R el cual nos indica el equilibrio o desequilibrio del sistema nervioso autónomo, donde se utilizaron herramientas para su procesamiento como un filtrado digital a la señal capturada por un tiempo de aproximadamente 5 minutos en estado de reposo, para eliminar frecuencias de interferencia para detectar el HVR , utilizamos también la transformada wavelet para observar cómo varían las bandas de baja y alta frecuencia a lo largo del tiempo. 



# 1. Fundamento teórico 
# 2. Adquisición de la señal ECG
# 3. Pre-procesamiento de la señal

En esta etapa iniciamos aplicando el filtro digital necesario para eliminar el ruido de la señal, debido a que tiene ruido de bajas y altas frecuencias, aplicamos un filtro pasa banda de 0.5 a 40 Hz, lo cual nos permite dejar la frecuencia que necesitamos limpia, siendo el QRS de la señal ECG 
![image](https://github.com/user-attachments/assets/e9326c06-ad65-46d5-8237-0791341efe79)


Diseñamos un filtro IIR basándonos en los parámetros de la señal, para el cual debemos hallar sus coeficientes b y a, de lo que se obtiene un filtro IIR de  orden 4, con frecuencias normalizadas entre 0.5 Hz y 40 Hz. El filtro Butterworth fue elegido por su respuesta suave sin ondulaciones en la banda pasante. ¡¡¡¡¡¡¡
Ya con el filtro IIR, a partir de sus coeficientes podemos obtener la ecuacion en diferencias que describe la señal¡¡¡¡¡¡¡¡

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

Para el análisis de estos parámetros nos apoyamos con esta gráfica la cual nos permite la visualización temporal de los intervalos R-R, para observar la variación de los latidos a lo largo del tiempo.
![image](https://github.com/user-attachments/assets/0143e7ad-782e-46cd-91af-283e07b1b6f8)
![image](https://github.com/user-attachments/assets/aabfb28e-486a-4b16-b997-4a689462c659)

Con lo cual podemos observar si hay estabilidad o fluctuaciones significativas en los latidos.
 La media indica el intervalo promedio entre latidos, la desviación estándar mide cuánto varían esos intervalos respecto a la media, indicandonos la variabilidad cardíaca. En la gráfica de los intervalos R-R a lo largo del tiempo, una mayor dispersión de los puntos respecto a la media refleja una mayor SDRR, lo que suele asociarse con una mejor regulación autonómica y mayor adaptabilidad fisiológica. Por el contrario, una baja SDRR, evidenciada por intervalos poco variables y agrupados, puede sugerir estrés o disfunción del sistema nervioso autónomo.

 






