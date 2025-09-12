---
layout: "../../layouts/ProjectLayout.astro"
order: 5
title: "FakeEcommerce | Web Site"
description: "Un sitio donde se puede armar una 'Lista de compras', y luego enviarla a la empresa para finalizar la compra. Usé Astro para el frontend y Strapi para el backend."
link: "https://ecommerce-fake-cdl.vercel.app/"
github: "https://github.com/CristianLeyton/fake-ecommerce"
image: "/assets/images/fake-ecommerce.webp"
tags: [STRAPI , ASTRO, TAILWIND]
hidden: false
---

Le puse como titulo "Fake-Ecommerce" porque para que sea un Ecommerce deberia tener una pasarela de pago. Este sitio solo te genera una **"Lista de Deseos"**. Es como que armar un presupuesto que al final lo envias por WhatsApp o Correo para confirmar el pedido a la empresa.

Consta de tres secciones principales.

### El inicio

![image](https://github.com/user-attachments/assets/f3d37db3-5cd8-4684-9a82-ca15c79e3cd8)

Una landing page con una cuenta regresiva para las fiestas, y una presentación rapida de las categorias de los productos y la empresa.

### Los productos

![image](https://github.com/user-attachments/assets/f2210761-9998-4c50-98c9-73d07377c304)

La sección "Productos" donde se puede agregar lo que quieras a la lista de deseos, dandole click al corazon naranja.

### La lista de deseos

![image](https://github.com/user-attachments/assets/6307a2b6-b59e-4478-8ad7-70365f3020ac)

Por último la propia lista de deseos, donde se puede editar y enviar la misma.

De nuevo, quizá entres y demore en cargar, es porque alojé el backend en un host gratuito que se apaga por inactividad. Espero pronto poder cambiar de host.
Por cierto, para el backend use Strapi, pero estoy pensando en usar AstroDB ya que solo son dos tablas. Deberia de poder hacerlo.

Acceder al sitio:
<https://ecommerce-fake-cdl.vercel.app/>

Acceder al backend:
<https://backend-ecommerce-c8cn.onrender.com/admin>

> *Usuario*: <test@mail.com>
>
> *Contraseña*: Test1234
