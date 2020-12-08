# financialadvisor
import pandas as pd
import fix_yahoo_finance as yf
from datetime import datetime 
from datetime import timedelta
import numpy as np
import sympy as sym 
import matplotlib.pyplot as plt
import math


def text_prompt(msg):
  try:
    return raw_input(msg)
  except NameError:
    return input(msg)

def upRange(start, stop, step):
  while start <= stop:
    yield start
    start += abs(step)

def downRange(start, stop, step):
  while start >= stop:
    yield start
    start -= abs(step)


n = float(text_prompt('Ingrese la cantidad de activos que quiere evaluar'))
for i in (1 <= float(n)) and upRange(1, float(n), 1) or downRange(1, float(n), 1):

  today = datetime.now()
  firstday = today - timedelta(days=360)
  a = text_prompt("Ingrese nombre de activo. Asegurese de escribirlo con el código asignado en Yahoo Finance.")
  activo = yf.download(a, start= firstday ,end= today)
  cierres = []
  activo.shape
  d = activo.shape[0]
  for j in (1 <= float(d-1)) and upRange(1, float(d-1), 1) or downRange(1, float(d-1), 1):
    e =activo.iloc[j,4]
    f = float (e)
    cierres.append(f)
  g = len(cierres)
  sumax = 0
  for j in (1 <= g) and upRange(1, g, 1) or downRange(1, g, 1):
    sumax = sumax +j
  sumay = 0
  for j in (1 <= g) and upRange(1, g, 1) or downRange(1, g, 1):
    sumay = sumay + cierres[j-1]
  sumaxy = 0
  for j in (1 <= g) and upRange(1, g, 1) or downRange(1, g, 1):
    sumaxy = sumaxy +(j*cierres[j-1])
  xsqr=0
  for j in (1 <= g) and upRange(1, g, 1) or downRange(1, g, 1):
    xsqr = xsqr + (j*j)
  m = (sumaxy - ((sumax * sumay)/g))/(xsqr - (pow(sumax,2))/g)
  b = (sumay/g)-(m*(sumax/g))
  futuro = m*(g+1) + b
  sumadev = 0
  for j in (1 <= g) and upRange(1, g, 1) or downRange(1, g, 1):
    sumadev = sumadev + pow(abs((sumay/g)-cierres[j-1]),2)
  de = math.sqrt(sumadev/g)
  ac = text_prompt("¿Qué tipo de operación desea hacer? Si es apertura escriba (a) si es cierre escriba (c)")
  if (ac=="a"):
    z = 0
    if (futuro + de <= cierres[g-1] and cierres[g-1]>futuro):
      print ("El activo ",a," está en zona de venta" )
      z = 1
    if (futuro-de >= cierres[g-1] and cierres[g-1]<futuro):
      print ("El activo ",a," está en zona de compra" )
      z = 1
    if (z==0):
      print ("El activo ",a," está en zona de espera, se recomienda no operar" )  
  if (ac=="c"):
    cv = text_prompt("¿Su activo es de compra o venta? Si es compra escriba (c), si es venta escriba (v).")
    if (cv=="v"):
      if (futuro+futuro*0.01 > cierres[g-1]):
        print ("Se recomienda cerrar posición del activo ",a)
        print (futuro,cierres[g-1])
      else:
        print ("Se recomienda mantener posición del activo ",a)
    if (cv=="c"):
      if (futuro- futuro*0.01 < cierres[g-1]):
        print ("Se recomienda cerrar posición del activo ",a)
      else:
        print ("Se recomienda mantener posición del activo ",a)
  column = activo["Adj Close"]
  column.plot(grid=True)
  plt.show()
