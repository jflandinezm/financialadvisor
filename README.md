Este código de Python es una herramienta financiera que analiza datos de Yahoo Finance para tomar una decisión de apertura en el mercado. Por ahora es una herramienta netamente académica, su uso no está sometido completamente a prueba. Teniendo en cuenta que se trata de un ejercicio predictivo y especulativo, aun no se recomienda usar en un ejercicio de inversión real. Está diseñado especialmente para Forex, sin embargo es adaptable para cualquier activo incluido en Yahoo Finance.

El algoritmo importa los datos de precios de cierre del activo del último año y modela, bajo el método numérico de mínimos cuadrados, una función. Con esa función intenta predecir el valor con el que el activo DEBERÍA cerrar al siguiente día. Se pueden presentar dos escenarios:

a. Se quiere abrir una posición: En este caso, con el histórico de cierres del último año se calcula la desviación estandar del activo con respecto al valor que debería presentar en la función, si el valor de la función más la desviación estandar es menor que el precio de cierre, se recomienda abrir la posición en venta. (Para el caso de Forex, en acciones no sería posible abrir una posición). En caso que el valor de la función menos la desviación estandar sea mayor que la función, se recomienda abrir la posición en venta. (Tanto para Forex como para acciones).

b. Se quiere cerrar una posición: Si la posición que se tiene abierta es de venta, cuando el activo esté un 1% por encima de su valor esperado por medio de la función, el algoritmo recomienda cerrar la posición. Si la posición es de compra, cuando el activo esté un 1% por debajo del valor esperado por medio de la posición se recomienda cerrar la posición.

El algoritmo calcula la cantidad de activos que se soliciten y van aconsejando uno por uno.
