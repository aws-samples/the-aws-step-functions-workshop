---
title: 'Resumen de la arquitectura'
weight: 93
---

Este módulo contiene los siguientes recursos:

- Tres funciones AWS Lambda
- Un endpoint de API Gateway
- Un rol de AWS IAM utilizado para integrar la API Gateway con Step Function

En este módulo, crearás un flujo de trabajo Express que reciba una matriz de enteros como entrada y, en paralelo, calcule la suma, la media, y los valores máximo y mínimo. La máquina de estado devuelve un objeto JSON con las respuestas de cada una de las tareas en paralelo.

A continuación, configurarás una integración asíncrona de API Gateway con tu máquina de estado. Ejecutarás la máquina de estado enviando una solicitud a API Gateway. Luego, modificarás la integración para que la respuesta de Step Function sea síncrona.
![Visual Workflow](/static/img/module-7/visual-workflow.png)



