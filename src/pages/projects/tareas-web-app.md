---
layout: "../../layouts/ProjectLayout.astro"
order: 1
title: "Tareas | Web App"
description: "Una aplicación donde podes administrar tus tareas pendientes, consultar las completadas y organizarlas con un sistema de etiquetas."
link: "https://tareas.cdl.com.ar/"
github: "https://github.com/CristianLeyton/app-tareas"
image: "/assets/images/tareas.webp"
tags: [LARAVEL, LIVEWIRE, TAILWIND]
---

Esta hecha en Laravel usando Livewire, con una base de datos MySQL, traté de hacer más que una simple TO DO APP agregando las siguientes funcionalidades:

- Se pueden crear tareas sin iniciar sesion, pero solo eso, para las demas funciones hay que loguearse.
- Historial de tareas completadas.
- Descripcion y fecha de creacion de cada tarea.
- Organizar tareas por un sistema etiquetas.
- Ordenar tareas.
- Repetición de tareas. (Puede marcar una tarea, como "diaria" por ejemplo, y aunque se complete en el dia, aparece al proximo. Lo malo es que necesito un server pago para hacer funcionar el CRON JOB de laravel)

![image](https://github.com/user-attachments/assets/21d41794-325b-476d-8f2a-5e9a6a675d06)

![image](https://github.com/user-attachments/assets/4d1d906a-df22-496e-8689-9a0539fe4eb1)

Acceder al sitio:
<https://tareas.cdl.com.ar/>

> Usuario: <test@mail.com>
>
> Contraseña: test1234

Otra vez me limita un poco el no poder pagar un host. Espero poder alojarlo en un mejor host pronto.
