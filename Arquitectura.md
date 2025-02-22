Esta es su nueva *bóveda*.

Cree una nota de algo, [[cree un enlace]], o pruebe [el Importador](https://help.obsidian.md/Plugins/Importer)!
# Documento de Arquitectura del Sistema de Gestión de Órdenes y Entregas

## 1. Introducción  
Este documento describe la arquitectura inicial del sistema de gestión de órdenes y entregas, incluyendo requisitos funcionales, requisitos de calidad y restricciones clave que deben ser consideradas en el diseño del software.

**Equipo:** 10  
**Integrantes:** Angie Juliana Jaramillo
		  Juan Jose Osorio Sanchez
		  Sebastián Orozco
		  Mateo Zambrano
**Fecha:** 20/02/2025

---

## 2. Requisitos Funcionales  
Los requisitos funcionales se presentan en forma de **historias de usuario**, especificando los **criterios de aceptación**.

### **Historias de Usuario**
| **ID**    | **Historia de Usuario**                                                                                                           | **Criterios de Aceptación**                                                                                                                                                                                                                                                                                                                      |
| --------- | --------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **US-01** | Como cliente registrado, quiero iniciar sesión en la plataforma para acceder a mi historial de pedidos y realizar nuevas compras. | - El usuario debe ingresar un correo y contraseña válidos.<br>- Si las credenciales son correctas, el usuario es redirigido a su perfil.<br>- Si las credenciales son incorrectas, se muestra un mensaje de error sin revelar detalles específicos.<br>- El usuario puede solicitar un restablecimiento de contraseña.                           |
| **US-02** | Como cliente, quiero poder agregar mis productos elegidos al carrito y finalizar mi compra del producto.                          | -El usuario debe seleccionar el producto deseado.<br>-Luego el usuario deberá seccionar el icono del carrito para guardar el producto.<br>-El usuario al momento de ingresar al carrito podrá finalizar la compra de este.                                                                                                                       |
| **US-03** | Como usuario, quiero iniciar sesión con mi correo y contraseña, para acceder a mis funcionalidades según mi rol.                  | -El sistema debe permitir iniciar sesión con correo y contraseña válidos.<br>-Si el usuario ingresa credenciales incorrectas, se debe mostrar un mensaje de error.<br>-Los usuarios deben tener roles asignados (Cliente, Administrador, Repartidor).<br>-Dependiendo del rol, el usuario solo podrá acceder a las funciones que le correspondan |
| **US-04** | Como administrador, quiero agregar, editar y eliminar productos del inventario, para mantener actualizada la oferta de la tienda. | -El sistema debe permitir registrar nuevos productos con nombre, precio, stock y categoría.<br>-Solo los administradores pueden modificar o eliminar productos.<br>-Si se intenta eliminar un producto con stock disponible, se debe pedir confirmación.<br>-Se debe actualizar el stock automáticamente cuando un cliente realice una compra.   |

>  **Instrucciones:**  
> - Completar al menos **tres historias de usuario**.  
> - Asegurar que cada historia tenga criterios de aceptación claros y verificables.  

---

## 3. Requisitos de Calidad  
Los requisitos de calidad se presentan en forma de **historias de calidad**, siguiendo la estructura de Len Bass.

### **Historias de Calidad**
| **ID**    | **Fuente**                | **Estímulo**                                                                                                 | **Artefactos**                                                                | **Entorno**                                                            | **Respuesta**                                                                                       | **Medida de Respuesta**                                                                                            |
| --------- | ------------------------- | ------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------- | ---------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| **RQ-01** | Desarrollador             | Se solicita modificar la lógica de asignación de pedidos para incluir nuevos criterios de prioridad.         | Código y configuración de reglas de negocio.                                  | Tiempo de ejecución                                                    | Se debe modificar, probar y desplegar la nueva lógica de asignación.                                | El esfuerzo requerido no debe superar 2 horas de trabajo y no deben generarse más de 2 defectos nuevos.            |
| **RQ-02** | Cliente                   |Quiere que el sistema siempre esté disponible para hacer pedidos sin interrupciones | Infraestructura del sistema,  balanceador de carga. | Procesamiento de múltiples órdenes simultáneamente.                    | Uso normal con múltiples usuarios accediendo al sistema. | El tiempo de procesamiento de una orden no debe superar los 2 segundos con una carga de 1000 órdenes concurrentes. |
| **RQ-03** | Administrador del sistema | Se requiere que el sistema soporte un aumento del 50% en la cantidad de órdenes sin afectar el rendimiento.  | Infraestructura de servidores, balanceo de carga y base de datos.             | Crecimiento del número de usuarios y pedidos durante temporadas altas. | Implementar un sistema de balanceo de carga y escalabilidad horizontal en la infraestructura.       | El sistema debe soportar el crecimiento sin que el tiempo de respuesta supere los 3 segundos bajo carga máxima.    |
| RQ-04     | Equipo de seguridad       | Se requiere garantizar la integridad y confidencialidad de los datos de los pedidos y usuarios.              | Sistema de autenticación, logs de seguridad, cifrado de datos.                | Accesos desde dispositivos externos y APIs de terceros.                | Implementar autenticación con OAuth2 y cifrado AES-256 para almacenamiento de datos sensibles.      | El 99% de los intentos de acceso no autorizados deben ser bloqueados y registrados en logs de seguridad.           |

>  **Instrucciones:**  
> - Completar al menos **tres historias de calidad**, alineadas con atributos clave como **rendimiento, escalabilidad y seguridad**.  
> - Definir cómo se medirá la respuesta esperada ante la situación planteada.  

---

## 4. Restricciones del Sistema  
Las restricciones establecen **limitaciones** en la arquitectura del sistema, ya sean tecnológicas, de negocio, regulatorias o de infraestructura.

### **Lista de Restricciones**
| **Tipo de Restricción** | **Descripción**                                                                                                                                                                                                                                                      |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Tecnológica             | El sistema debe desarrollarse utilizando **Spring Boot y PostgreSQL**, debido a la infraestructura actual de la empresa y su compatibilidad con otros sistemas internos.                                                                                             |
| Tecnológica             | Hacer uso del GitHub para el control de versiones. Esto permitirá un seguimiento detallado de los cambios realizados en el código, facilitando la colaboración entre los miembros del equipo y asegurando la integridad del proyecto en cada etapa de su desarrollo. |
| Negocio                 | Para garantizar la seguridad y el control de acceso en el sistema, los usuarios deberán iniciar sesión utilizando su usuario y contraseña. Este proceso validara sus credenciales y les permitirá acceder a la plataforma según su rol asignado.                     |

>  **Tipos de restricciones:**  
> - **Tecnológicas:** Lenguajes, frameworks o herramientas que deben utilizarse.  
> - **De negocio:** Normativas o estándares de la empresa.  
> - **Regulatorias:** Cumplimiento de normativas legales o de seguridad.  
> - **De infraestructura:** Limitaciones en hardware, red o almacenamiento.  


---

## 5. Formato de Entrega  
- **Formato:** Markdown (`.md`) en el repositorio de Codelabs, El documento debe llamarse `Arquitectura.md`.  
- **Extensión máxima:** 3 páginas.  

---

## **Tiempo estimado para completar el ejercicio: 50 minutos**  
**15 min** → Definir **3 historias de usuario con criterios de aceptación**.  
**15 min** → Definir **3 historias de calidad alineadas con atributos clave**.  
**10 min** → Identificar **2 restricciones relevantes**.  
**10 min** → Revisión y ajustes finales del documento.