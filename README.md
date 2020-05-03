# Pasatiempos resueltos en Python

## Calcular el area de dos cuadrados o cubos superpuestos

Determinar el área común de dos lineas, rectángulos/cuadrados o cubos superpestos (cualquier dimensión) dado los centroides de las dos figuras  y el largo de las figura (el cual pueden ser distintos o no).

### Explicación

Independientemente de la dimensión en la que se trabaje, sabemos que la proyección de ambos vectores de ambas figuras estará comprendido en una recta, por lo que para calcular el area total de los rectángulos superpuestos (sin importar la dimensión), calcularemos las diferencias de los vectores en cada dimensión y multiplicaremos esas diferencias obteniendo así el área del rectángulo superpuesto.

```python

class Fig():

    def __init__(self, square_A, lenght_A, square_B, lenght_B):

        self.A, self.L_A = square_A, lenght_A
        self.B, self.L_B = square_B, lenght_B
    
    def minmax_1D(self, a, b):

        return a - self.L_A/2, a + self.L_A/2, b - self.L_B/2, b + self.L_B/2        
    
    def in_range(self, value, min_r, max_r):

        return value > min_r and value < max_r

    def figs_colision(self):

        colision = 1

        for i in range(len(self.A)):

            minA, maxA, minB, maxB = self.minmax_1D(self.A[i], self.B[i])
            
            A_in = self.in_range(minA, minB, maxB) or self.in_range(maxA, minB, maxB)
            B_in = self.in_range(minB, minA, maxA) or self.in_range(maxB, minA, maxA)

            colision = colision * (A_in or B_in)

        return colision

    def diff_1D(self, a, b):

        if a == b:

            return min(self.L_A, self.L_B)

        else:

            minA, maxA, minB, maxB = self.minmax_1D(a, b)

            return min(maxA, maxB) - max(minA, minB)
    
    def area(self):

        if self.figs_colision():

            total_area = 1

            for i in range(len(self.A)):
                total_area = total_area * self.diff_1D(self.A[i], self.B[i])
            
            return total_area
        
        else:
            return 0
        
```

Ejemplos de llamadas y salida

En 1D

Gráfico:

![](https://github.com/Guillermo-C-A/pasatiempos-resueltos-en-python/blob/master/img_Readme/1D.png)

Llamada:

```python

print(f"Total area in common: {Fig([1.5],3,[3.5],4).area()}")

```

Salida:

```
Total area in common: 1.5
```

En 2D

Gráfico:

![](https://github.com/Guillermo-C-A/pasatiempos-resueltos-en-python/blob/master/img_Readme/2D.png)

Llamada:

```python

print(f"Total area in common: {Fig([0,3],4,[1.5,1.5],3).area()}")

```

Salida:

```
Total area in common: 4.0
```

En 3D

Gráfico:

![](https://github.com/Guillermo-C-A/pasatiempos-resueltos-en-python/blob/master/img_Readme/3D.png)

Llamada:

```python

print(f"Total area in common: {Fig([2,2,2],4,[1,1,1],2).area()}")

```

Salida:

```
Total area in common: 8.0
```

En el caso de que las figuras no se superpongan, el area sera 0

En 1D

Gráfico:

![](https://github.com/Guillermo-C-A/pasatiempos-resueltos-en-python/blob/master/img_Readme/1D_1.png)

Llamada:

```python

print(f"Total area in common: {Fig([1],2,[4],2).area()}")

```

Salida:

```
Total area in common: 0
```

En 2D

Gráfico:

![](https://github.com/Guillermo-C-A/pasatiempos-resueltos-en-python/blob/master/img_Readme/2D_1.png)

Llamada:

```python

print(f"Total area in common: {Fig([1,1],2,[4,2],2).area()}")

```

Salida:

```
Total area in common: 0
```

En 3D

Gráfico:

![](https://github.com/Guillermo-C-A/pasatiempos-resueltos-en-python/blob/master/img_Readme/3D_1.png)

Llamada:

```python

print(f"Total area in common: {Fig([2,1,1],2,[-2,1,1],2).area()}")

```

Salida:

```
Total area in common: 0

## Combinaciones de a x b = c

Obtener todas las combinaciones de números enteros de forma que a x b = c

```python

def combinaciones(c):

    combinaciones = []

    for i in range(1,int(c/2)):

        if c%i == 0 and i < c/i:
            combinaciones.append([i, int(c/i)])
    
    return combinaciones

```

Ejemplo:

Obtener las combinaciones de a x b = 2000

Llamada:

```python

combinaciones(2000)

```

Salida:

```

[[1, 2000], [2, 1000], [4, 500], [5, 400], [8, 250], [10, 200], [16, 125], [20, 100], [25, 80], [40, 50]]

```