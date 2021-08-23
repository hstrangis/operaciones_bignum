# Operaciones aritméticas entre Bignums 

Se desarrollan algunas operaciónes aritmeticas básicas para operar con números extremadamente grandes, de precisión arbitraria. Se basan en una clase bignum, en la que cada dígito es almacenado en la posición correspondiente de un vector.

La implementacion recursiva del algoritmo de Karatsuba y Ofman, es una multiplicacion que permite reducir la complejidad de la multiplicacion clasica desde O(n^2) a O(n^1.58), gracias a la cancelacion de terminos.
