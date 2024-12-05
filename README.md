# sprint 4
## Ejecución de yaml de deployment
Al ejecutar el yaml, se generan los microservicios como se observa en la imagen en la que cada microservicio está conectado con su base de datos y a su vez está conectado a kong mediante el kong.yml.

![Captura de pantalla 2024-12-05 124728](https://github.com/user-attachments/assets/391d005b-d101-43d2-9ff4-976f31292152)


## Llenado de tablas para la realización de las pruebas:
Como se observa en las imágenes siguientes, se realiza un llenado de todas las tablas de la base de datos con el fin de que las pruebas que se realicen tengan sentido y se asemejan de alguna forma a un escenario de la vida real, contando con más de 100 mil recibos de pago generado para miles de estudiantes de las 15 instituciones.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd1Ad5_YEow25aLzuOrV_6TsDEZRHEtJOH99jbTdXjeHFDX457R9K893XzDXIrK4JB8xhbW7KO-_udLm2YRmKRJY_ETdvavPVafzqPjD0Qu1CukvCoBSBxm7XF3ULuQpkhnJk6RpQ?key=rb5JCnmizxIzpsgzwXQpIVLN)
Como se puede observar anteriormente, se genera un factory para cada uno de los microservicios en los cuales se procederá a llenar su base de datos de su información, en el caso de la imagen anterior, ya se llenaron las instituciones, ahora se procede a llenar la información con los estudiantes. Y así sucesivamente con la información de los cronogramas, recibos de pago y recibos de cobro.
![cqrs_instituciones_estudiantes](https://github.com/user-attachments/assets/f7186214-6fb4-4f55-a74a-4080bd5ba4a6)

A la izquierda es posible observar que a medida que se insertan los estudiantes como se observaba en la imagen donde se insertan, se envía a la cola de rabbitMQ, generando el patrón CQRS y llenando la información de la base de datos centralizada de reportes, donde se encuentra la información de las instituciones, estudiantes, cronogramas, recibos de pago y recibos de cobro.

Finalmente, a continuación se muestra la comparativa del número de documentos entre cada base de datos de cada microservicio, con la centralizada, como se puede observar se envió la misma cantidad de información, aplicando el patrón CQRS de Microservicios:
- Servicio de Facturación:
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf7af0kT9FHfbl2L6eCsPOKdaLpILPHnhmf-6_QRqn5xwaX7Go6tWmY-hY88rzMjMM93MsOMW1mETBoXdHwXv2eoa0VXpbnINC20Nvg-7RvKMElg-64-d6yr51NJILavAiE_eBSgA?key=rb5JCnmizxIzpsgzwXQpIVLN)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfgjEAjacfOcoFfiu2-EAWBMjgculnP5xfOy5OUp8T0oBS7bHrdI75yhZP0Gpy65HMm3IvchazUDVpD8guhIMgqbSn4PjwZylUbSvjWBbS0fp1V5hEbU5nnxFibKo1ROH1i9HM8FQ?key=rb5JCnmizxIzpsgzwXQpIVLN)
- Servicio de Cronogramas:
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXee1enVWM1S6Z_xJ0bGJwVSX2lUdMLAHVxRkDgyoUEd7Q6EiYsUYrR7pxd8kAXsVLs3s_3u9yKdAWnPKQduqk-PiwPOUrZThUWWswUj4OtEiguOO_VsdPe-kdKpf5SV3XahUZvDAQ?key=rb5JCnmizxIzpsgzwXQpIVLN)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdOyEFpm8uxkFA10ZKxkAl3_lfjwC1EKfcyX3uk8KxkJVgcN13iyr5GvajISY0jLmxnaJzai0Z-aEKEFJgiKxqf_VhaLdRsQkekg3Dk5_Nf-XgjVscT4KtU26thfcYJfrc90vI4fQ?key=rb5JCnmizxIzpsgzwXQpIVLN)
 
# Reporte a generar para el ASR de latencia.
  
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe06U_XTRXBjzpEmUNiRjp_bki5dfWvhZhfrZ1FX0GbUImzJ7iuKFjctGC--9vQVzWJNfCWK1dZFy6SoP6jvgZmwrR2kNNnkuS_1lu1kF4xG5l-F-QanuihHybBCmuxx5k50qgB9Q?key=rb5JCnmizxIzpsgzwXQpIVLN)
  
1.  Se realizan pruebas de GET, sin Redis, sin seguridad, ni el job cron (todas las peticiones se hacen directamente a la base de datos CQRS donde se encuentra almacenada toda la información de forma centralizada de las Instituciones, Estudiantes, Cronogramas y Facturación).
    
  
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc6-wtSIg6MF6Rxth7FwVO6yB1tyE-v6z3zAsqBsFHsqmelj32tf573uB_hbGXme_6-CHHB7RKU2230lOGnBA3b0i6xoHGpVGjJyRJUbTH8q8LJ12LXQNnMpKN3VkzyQTRoqO7bfQ?key=rb5JCnmizxIzpsgzwXQpIVLN)
  
  
  
  
  
  
1.  Con 10 hilos y un periodo de subida de 5: 
    
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc3gU6zEg8AeWa7zDyDIxsnt0Kh52WrzMXD2VKUIvitiyRbCZer6ZJudWUl5KtkecQrvFlVmoJFNz1YvibOHkP9c5-UVEyJoeWlqFLpiqj7UfxsVBFgea4LQaKGANig9V2fwFXH?key=rb5JCnmizxIzpsgzwXQpIVLN)
2.  Con 15 hilos y un periodo de subida de 5: 
    
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfx9d3bdaUFPIwOkUbvYfU-tE22JNHF4nb-IybB2zpdpR3EigIH-SJ_aAYaU9WEt0o25M7qcL7JNMKru33fIqTp4LMDZrtNNhCED2-BP_ai_7KK9bEEdCcbX-XQVo337DCMu47nMg?key=rb5JCnmizxIzpsgzwXQpIVLN)
3.  Con 30 hilos y un periodo de subida de 5: 
    
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf6d50S3glFdnbut0AxeaQnsbXX5QwTa5VvXs66vtbNdmzxWbyIssAWRdeXz30lTFKR2XfWdhSrWL7mb9AJDv5sxK3lEu8j-acFGt0lYl9LBJjg7d4epj6qOx4zDXtUS2pMcyaBdA?key=rb5JCnmizxIzpsgzwXQpIVLN)
  
  
2.  Se realizan pruebas GET con Redis, job cron y sin seguridad.
    
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc6-wtSIg6MF6Rxth7FwVO6yB1tyE-v6z3zAsqBsFHsqmelj32tf573uB_hbGXme_6-CHHB7RKU2230lOGnBA3b0i6xoHGpVGjJyRJUbTH8q8LJ12LXQNnMpKN3VkzyQTRoqO7bfQ?key=rb5JCnmizxIzpsgzwXQpIVLN)
  
  
  
  
  
  
  
1.  Con 10 hilos y un periodo de subida de 5: 
    
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcRgzQFxdT2mP_vkwO8qPwiVE1jYkAXbL5eoaH4XTdx4doZvB7ahPElZ_fgrd-d5rpFQd9DowbCxc_jme8FijztnNhMNg8nCPj8IdgvQasIrX2Lw6usFoxt908TdMwxsoI57zStgg?key=rb5JCnmizxIzpsgzwXQpIVLN)
2.  Con 15 hilos y un periodo de subida de 5: 
    
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdgNnAmeSztf4IsTmJlFI-R2QLKg8pqIRONvSTXGUAVOVeMkCrOVykXISjk9v9tmzmcg2XAA0PyfXS5nwrYFeOMJveAi8KLO3os_N2HoyVbv3NCxOUPv1JmKsWZVq6_oN83tg3otA?key=rb5JCnmizxIzpsgzwXQpIVLN)
3.  Con 30 hilos y un periodo de subida de 5: 
    
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdzJ0LG9AQ4YP00BY2HsPU5AyfA_vgk6PYiNrxUw7GYUqL_XPQki_sjKzGoscm7uCyGn4zUnh2zGKSXTdsdENuYdO6HvR9QjRaMLGjPcLTACiAToL20EezFfoA6QizYQW0tnDY4qw?key=rb5JCnmizxIzpsgzwXQpIVLN)
3.  Se realizan pruebas GET, usando el navegador sin Redis, job cron y sin seguridad.
    
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeW8wEdn8OYcE9DOgTfZOzeqD4rSAP4iP5CFAsNDUcrefTc1zTlhP9d3ic03LjlJksYgsI521jmH7IXIJyZIS7S8bvtXdLDgsrFVMw8crvybYO6FFgtY5pT3JJ6uzlI5VCgcJm3Pw?key=rb5JCnmizxIzpsgzwXQpIVLN)
  
4.  Se realizan pruebas GET, usando el navegador con Redis, job cron y sin seguridad.
    
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfJIIABRFCQEfOZgzw20VX1TzhvT0jIo5XgzkJpdQC0-4UFeH-rtScIbp7hjX9kvMojrytkWMl-o5AuMKuS8C2ubsF7BvaRC1LtbTjOPL-uox8F7xMI20nrmocBKeev8jEpp0YH?key=rb5JCnmizxIzpsgzwXQpIVLN)

Como se puede observar en estas últimas pruebas, se requiere de autenticación, lo cual genera que haya mas delay y más demora en la generación de las cuentas por cobrar. Cabe resaltar que la implementación fue similar a la entrega pasada (Sprint 3) en la cual si un auxiliar contable quiere ver la información de otra institución, no puede porque se hace la validación con el microservicio de usuarios el cual tiene una BD de MongoDB.
  

----
# Comandos importantes:
##Para correr Django y FastAPI
```
- cd /labs/*/ofipensiones
- python3 manage.py runserver 0.0.0.0:8080
- python3 manage.py shell
- tail -f subscriber.log
- uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```
##Para revisar el shell de Mongo y de PostgreSQL y hacer consultas de las tablas
```
- docker exec -it 855347ef4687 mongosh -u microservicios_user -p password 
- docker exec -it 6b2aeaa561ee psql -U microservicios_user -d facturacion_service
- \dt
- SELECT COUNT(*) FROM "public.facturacionService_recibocobro" ;
- DELETE FROM "public"."facturacionService_recibopago";
- limit 10; 
- use db
- db.coleccion.countDocuments()
```
## Para poblar todas las bases de datos de cada microservicio, usando la shell de Django


```
- from institucionesService.factory import crear_instituciones_con_cursos
- crear_instituciones_con_cursos()

- from estudiantesService.factory import asignar_estudiantes_a_cursos
- asignar_estudiantes_a_cursos()

- from cronogramasService.factory import crear_cronogramas_bases, generar_detalles_cobro_para_instituciones
- crear_cronogramas_bases(), generar_detalles_cobro_para_instituciones()

- from facturacionService.factory import generar_recibos_cobro_hasta_actualidad, generar_recibos_pago
- generar_recibos_cobro_hasta_actualidad(), generar_recibos_pago()

- from usuariosService.factory import create_users
- create_users()
```


##Redis

```
-     sudo apt update
-     sudo apt install redis-server
-     sudo systemctl enable redis-server.service
-     sudo systemctl start redis-server.service
-     sudo nano /etc/redis/redis.conf
-     bind 0.0.0.0 ::1
-     protected-mode no
-     sudo systemctl restart redis-server
-     systemctl status redis-server
```
---
#Autenticación
Harloe_Elementary:
34.41.64.237:8000/reportes/reporte/Harloe_Elementary/Junio/
padre-familia-ernesto-1@padre-familia-ofipensiones.com
aux-jose-1@aux-contable-ofipensiones.com

Quincy_Middle_School 34.41.64.237:8000/reportes/reporte/Quincy_Middle_School/Junio/
padre-familia-valentina-1@padre-familia-ofipensiones.com
aux-camila-1@aux-contable-ofipensiones.com

----
#CQRS de RabbitMQ
A continuación los exchange y topics que se envían a la RabbitMQ para poder realizar el CQRS (falta para actualizar y eliminar alguna entidad):

```
exchange='recibos_pago', routing_key='recibo.pago.created'
exchange='recibos_cobro',routing_key='recibo.cobro.created'
exchange='cronogramas',routing_key='cronograma.created'
exchange='estudiantes',routing_key='estudiante.created'
exchange='instituciones',routing_key='institucion.created'
```

