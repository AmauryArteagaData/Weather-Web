# Guía de Desarrollo: Weather Web Application

## 1. Visión General del Proyecto
Este documento establece las directrices de arquitectura, diseño de interfaz, estándares de desarrollo y manejo de errores para el desarrollo de la aplicación web de clima.

---

## 2. Stack Tecnológico

### Front-End
* Framework: Astro Framework
* Estilado: Tailwind CSS

### Back-End
* Framework: Hono.js
* Base de Datos: MongoDB
* Integración: API Externa de Clima (e.g., OpenWeatherMap, WeatherAPI)

### Infraestructura & Despliegue
* Control de Versiones: GitHub
* Hosting / Serverless: Vercel

---

## 3. Arquitectura del Layout (UI Components)

La interfaz se divide en los siguientes componentes principales:

1. Current Forecast: Muestra el estado del tiempo actual (temperatura, ubicación, icono del clima).
2. Weather Detail Condition: Información detallada adicional (humedad, viento, presión, índice UV).
3. Forecast per Hour: Pronóstico por horas durante el día actual.
4. Temperature Average: Visualización del promedio o rango de temperatura esperada.
5. Prevision Week: Pronóstico de la semana (próximos 5 a 7 días).

---

## 4. Estándares de Clean Code

### Responsabilidad Única (SRP)
* Separación estricta entre capa de presentación (Astro), capa de lógica de negocio (Hono) y acceso a datos (MongoDB).
* Los componentes Astro deben centrarse únicamente en el renderizado y paso de propiedades.

### Nombres Claros y Semánticos
* Variables y funciones en inglés, descriptivas y contextuales.
* Nombres de componentes en UpperCamelCase (ej. `CurrentForecast.astro`).
* Utilizar verbos para funciones: `getWeatherData()`, `formatTemperature()`, `saveUserLocation()`.

### Modularidad y Reusabilidad
* Reutilizar utilidades de formato (fechas, conversiones de unidades) en una carpeta `/utils`.
* Clases de Tailwind agrupadas o abstraídas en componentes para evitar duplicación masiva en el HTML.

### Control de Tipos e Interfaces
* Definir esquemas o interfaces para la respuesta de la API externa y los modelos de MongoDB.
* Asegurar que el contrato de API entre Hono.js y el Front-End esté documentado y tipado.

---

## 5. Estrategia de Manejo de Errores

### Capa de Backend (Hono.js)
* Middleware Global de Errores: Capturar excepciones no controladas mediante `app.onError()`.
* Formato Unificado de Respuestas de Error:
  ```json
  {
    "success": false,
    "error": {
      "code": "WEATHER_API_UNAVAILABLE",
      "message": "No se pudo obtener la información del clima en este momento."
    }
  }