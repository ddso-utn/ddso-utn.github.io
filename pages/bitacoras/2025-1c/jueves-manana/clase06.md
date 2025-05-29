---
layout: page
title: Clase 6
description: Jueves Mañana, 2025, Primer Cuatrimestre
permalink: /bitacoras/2025-1c/jueves-manana/clase-06/
---

# Temeario

 * Patrones de UI. Componentes. Conceptos
 * Client side vs Server Side.
 * MVC. MVVM.
 * Reactividad. Variantes. Generalizacion.

# Resumen clase

## Arquitectura de presentación

  * Repaso de la arquitectura **cliente pesado**, con **dibujado del lado del cliente**, **_single page_**:
    * El cliente descarga del servidor la mayoría de los recursos (código HTML, JS, CSS, Fuentes, etc)
    * El cliente renderiza el HTML _esquelético_ de la página principal
    * El cliente ejecuta el código JS que dibuja los componentes dinámicos y realiza más llamados al servidor, que ahora devuelve sólo datos en un formato estructurado, como JSON
    * El cliente termina de dibujar los componentes usando los datos
    * El cliente queda a la espera de nuevos eventos de le usuarie. Ante ellos, disparará:
      * la ejecución de lógica de dominio y presentación
      * la carga de nuevos datos o la modificación de los mismos en el servidor
      * el dibujado de nuevas pantallas y componentes
  * Formas de organizar el código y arquitectura de presentación:
    * MVC: Modelo, Vista y Controlador
    * MVVM: Modelo, Vista y Modelo de la Vista. Binding bidireccional
    * Reactividad

## React

  * Originado en FB
  * Cambio de paradigam de HTML (componentes, manipulacion directa DOM, etc, separacion HTML, JS, CSS)
  * Eventos
  * JSX, componentes, props y estado. Diferencia entre JS y JSX. 

## Ejemplo: Conversor de unidades

```jsx
import React, { useState } from 'react';

function Conversor() {
  const [millas, setMillas] = useState('0');
  const [kilometros, setKilometros] = useState('');

  const convertir = () => {
    const valorMillas = Number.parseFloat(millas);
    if (!Number.isNaN(valorMillas)) {
      const valorKilometros = valorMillas * 1.60934;
      setKilometros(valorKilometros.toFixed(2));
    } else {
      setKilometros('');
    }
  };

  return (
    <div style={{ maxWidth: '300px', margin: 'auto', padding: '1rem', fontFamily: 'sans-serif' }}>
      <h2>Conversor de Millas a Kilómetros</h2>
      <div style={{ marginBottom: '1rem' }}>
        <label for="millas">Millas:</label>
        <input
          type="number"
          name="millas"
          value={millas}
          onChange={(e) => setMillas(e.target.value)}
          style={{ width: '100%', padding: '0.5rem' }}
        />
      </div>
      <div style={{ marginBottom: '1rem' }}>
        <label for="kilometros">Kilómetros:</label>
        <input
          type="number"
          name="kilometros"
          value={kilometros}
          readOnly
          style={{ width: '100%', padding: '0.5rem', backgroundColor: '#f0f0f0' }}
        />
      </div>
      <button type='button' onClick={convertir} style={{ width: '100%', padding: '0.5rem' }}>
        Convertir
      </button>
    </div>
  );
}
```

> :Desafío: ¿se podría hacer que no necesitemos un botón convertir?


# Material


* https://es.react.dev/
* https://nextjs.org/
* https://reactstrap.github.io


# Tarea

_Sección en progreso_