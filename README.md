![Java](https://img.shields.io/badge/Lenguaje-Java-blue?logo=java)
![NetBeans](https://img.shields.io/badge/IDE-NetBeans-blue?logo=apachenetbeanside)
[![License: GPL v2](https://img.shields.io/badge/License-GPL%20v2-blue.svg)](https://www.gnu.org/licenses/old-licenses/gpl-2.0.html)
[![Concurrencia](https://img.shields.io/badge/Tema-Concurrencia-important)](https://docs.oracle.com/javase/tutorial/essential/concurrency/)

# Problema del Productor-Consumidor en Java

Implementación clásica del problema de sincronización entre procesos usando **hilos en Java**, con solución utilizando:
- `wait()`/`notify()`
- Semáforos

## 📚 Explicación del problema

El problema del productor-consumidor (también conocido como *bounded-buffer problem*) es un ejemplo clásico de **sincronización entre procesos múltiples** donde:

- **Productor(es)**: Generan datos y los colocan en un buffer.
- **Consumidor(es)**: Toman datos del buffer para procesarlos.
- **Buffer compartido**: Zona de almacenamiento con capacidad limitada.

<p align="center">
  <img src="https://www.netmentor.es/imagen/effab1d1-f759-4ecd-a4aa-e8f2f4ca09c6.jpg" width="500" alt="Diagrama Productor-Consumidor">
</p>
Fuente de la imagen del diagrama [NetMentor](https://www.netmentor.es/entrada/patron-productor-consumidor)

## 🛠️ Solución implementada

### 1. Wait/Notify
```java
public synchronized void put(int value) 
{
    while (contenedorlleno) 
    {
        try 
        {
            wait();
        } 
        catch (InterruptedException e) 
        {
            System.err.println("Contenedor: Error en put -> " + e.getMessage());
        }
    }
    contenido = value;
    contenedorlleno = Boolean.TRUE;
    notify();
}
