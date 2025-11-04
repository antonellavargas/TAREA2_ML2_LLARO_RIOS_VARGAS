# **TAREA 2 - MACHINE LEARNING 2**
### **Assignment 2: Principal Component Analysis, Neural Networks**

**Integrantes:**

* Llaro Castro, Diego Renato
* Rios Meza, Jennifer Saskia
* Vargas Flores, Johanna Antonella

---

Deadline: Tuesday, November 4th, 2025, 23:59

Environment: Python, numpy, pandas, matplotlib, scikit-learn, pytorch.

---

## Programming Exercises

### Part I: Eigenfaces for Face Recognition

1. **Load the Training and Test Sets**

   Se cargo los datos de training y test set respectivamente, al ser las imágenes de 50x50 y aplanar a un vector se contará con 2500 pixeles o atributos en este contexto.
   Se cargaron 540 imagenes para train y 100 para test

2. **Average Face**

   Se calculó el average por columna (feature) de la matriz de train, la cual produce una cara promedio >< del train set.

3. **Mean Subtraction**

   Se resto la cara promedio a todas las imágenes, con la finalidad de centrar los datos, esto fue realizado tanto para train como para test.

4. **Eigenfaces**

   Se realizó la descomposición para obtener los eigenfaces o rosotros básicos, estos rostros capturan los patrones más comunes en el set de datos, donde cada rostro del train puede ser expresado por estos eigenfaces.

5. **Eigenface Features**

   Se construyó una función donde cada imagen se representara por los r iegenfaces que se escogía, de esta manera se reduce drasticamente el tamaño que pueden ocupar. Además de saber que características tiene cada rostro y poder comparar rostros de manera mas simple.

6. **Face Recognition**

   Se realizó una regresión logistica para `r = 10`, se mapeo los datos de train y test a este `r` se entrenó el modelo y para la predicción se obtuvo un `accuracy de 76%`
   Se realizó el mismo procedimiento para `r = 1, 2, ..., 200` y se procedió a plotear la precisión respecto al número de iegenfaces tomadas, donde se observa que `apartir de r = 50, se tiene una precisión de mas de 90% la cual tiende a disminuir un poco por alrededor de r = 110`.
   **La mejor precisión fue de 93% en el r = 47**

7. **Low-Rank Reconstruction Loss**

   A partir de los eigenfeatures se pueden reconstruir las imágenes (aprox), demostrando que se preserva la información más importante. Además, se ploteo el error de reconstrucción respecto al número de eigenfaces para saber con cuantos eigenfaces son necesarios para reconstruir bien las imágenes, aunque no existe un número exacto ya que es un tradeoff de calidad vs tamaño.

### Part II: Neural Networks

   Se entrenó una Red Neuronal Convolucional (CNN) para clasificar dígitos escritos a mano (0-9).
   Se usó:
   - dos capas convolucionales (kernel de 3x3)
   - una de pooling (2x2) -> reduce dimensiones a la mitad
   - dos capas fully connected (128 y 10 neuronas respectivamente)
   - la función de activación `ReLU`

   Se obtuvieron los siguientes resultados con 5 epochs:

   | Época | Train Loss | Train Accuracy | Test Loss | Test Accuracy |
|:-----:|:----------:|:--------------:|:---------:|:-------------:|
| 1/5   | 0.1565     | 95.26%         | 0.0486    | 98.36%    |
| 2/5   | 0.0431     | 98.67%         | 0.0415    | 98.67%    |
| 3/5   | 0.0264     | 99.14%         | 0.0355    | 98.88%    |
| 4/5   | 0.0181     | 99.39%         | 0.0353    | 98.86%    |
| 5/5   | 0.0137     | 99.56%         | 0.0390    | 98.81%    |

   Como se observa el modelo aprende correctamente y tiene un rendimiento excelente en el test -> **98.81%**. En los plots se observa que para el error de train y test se desciende rápidamente a valores muy pequeños `<0.04`, y para el `accuracy` se llega por encima de 98% para ambos sets con un ligero `overfitting`.