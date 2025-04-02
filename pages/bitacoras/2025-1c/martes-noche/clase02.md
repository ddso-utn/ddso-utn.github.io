---
layout: page
title: Clase 2
description: Martes Noche, 2025, Primer Cuatrimestre
permalink: /bitacoras/2025-1c/martes-noche/clase-02/
---

# Resumen

En esta clase hablamos de:


## Cualidades de diseño
- Independientes de Tecnología  
- Dependientes de Tecnología  
- SOLID

## Git Avanzado

### Repaso
- Repositorio  
- Commit  
- Pull  
- Push  
- Merge  
- Conflictos

### Branching
- Puntero a un commit  
- Usadas para desarrollos divergentes  
  - Ejemplo: Feature Branches  
  - Ejemplo: Branches por ambiente

### Merge Strategies

#### Fast-Forward
- Branch destino sin cambios  
- Me pone los commits después  
- Sin Merge Commit

#### Recursive
- Branch destino con cambios  
- Me intercala los commits  
- Tiene Merge commit  
- Conflictos

##### Sin conflictos
- Merge commit vacío

##### Con conflictos
- Me pide resolver  
- Hace Merge commit con la resolución

### Alternativas al Merge

#### Rebase & Merge
- Coloca los commits de la branch fuente atrás de los de la branch destino  
- Cambia el ancestro común  
- Aplica sucesivamente cada commit y detiene en conflictos  
- Resultado: fast forward más prolijo

#### Squash & Merge
- Combina todos los cambios en un solo commit  
- Historial más conciso pero menos detallado  
- A lo sumo un solo conflicto

#### Cherry-pick
- Aplica de a un commit sobre una branch  
- Combinado con squash puede equivaler a un rebase más conciso

### Pull Requests (o request-pull)
- Herramienta de QA (mejora de proceso)  
- Revisión de pares  
- Consolida criterios  
- Abre debates  
- Permite supervisar  
- Varios ojos ven más que uno

---

## Plataformas

### Javascript
- Lenguajes compilados vs Interpretados:
- Node Interpreter  
- Concepto de VM/Runtime

### Armando mi primera app

#### Server Node pelado
- Es de muy bajo nivel
- Mejor usar un framework

##### Biblioteca vs Framework

###### Biblioteca
- La llamo yo  
- Menos decisiones pre-tomadas

###### Framework
- Me llama a mí  
- Da estructura  
- Metáfora del esqueleto/carne  
- Muchas decisiones pre-tomadas

#### Dependencias
- Manejadores:
  - Maven  
  - NPM  
  - Gradle  
  - Gemfiles
  - Etc.

##### NPM
- Metadata del proyecto:  
- Dependencias/DevDependencies

## Ejemplo práctico con Express
- Creamos un "Hola Mundo" que se puede acceder desde el navegador

--- 

# Material

* [Presentación](https://www.canva.com/design/DAGjWQ_nX6E/_vwL62qHc2FsEnwtYD7j-g/view?utm_content=DAGjWQ_nX6E&utm_campaign=designshare&utm_medium=link2&utm_source=uniquelinks&utlId=hf3334dcf89)
* [Cualidades de diseño](https://docs.google.com/document/d/14HdvHvS33WqYb6Ak0BGa0IeCTbzeCRSDKs-1Ot-qLDw/edit?tab=t.0)
* [Clean Architecture](https://github.com/GunterMueller/Books-3/blob/master/Clean%20Architecture%20A%20Craftsman%20Guide%20to%20Software%20Structure%20and%20Design.pdf)
* [Biblioteca vs Framework](https://docs.google.com/document/d/1D_MCoh4J8kL1MAKNlbDgAMu2nYxri-81nZBYOPFWnO0/edit?tab=t.0#heading=h.6ab0fffv8tld)
