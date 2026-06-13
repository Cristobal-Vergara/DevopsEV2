# DevopsEV2
# Proyecto de Modernización y Despliegue Automatizado: Innovatech Chile

1. Contexto del Proyecto
Este proyecto forma parte de la Etapa 2 de modernización tecnológica de Innovatech Chile.
El objetivo principal es migrar una arquitectura de microservicios (Frontend y Backend) desde un modelo tradicional hacia un entorno contenerizado y altamente automatizado en la nube de Amazon Web Services (AWS)

2. Arquitectura de Contenedores
La solución utiliza Docker para garantizar la portabilidad y consistencia entre entornos.

Dockerfiles (Estrategia de Construcción)
Cada microservicio cuenta con un Dockerfile diseñado bajo los siguientes estándares de la industria:

Multi-stage Build: Se utiliza para separar el entorno de compilación del de ejecución, reduciendo drásticamente el tamaño de la imagen final y mejorando la seguridad al no incluir herramientas de desarrollo en producción.

Usuario No Root: Por seguridad, los procesos dentro del contenedor se ejecutan con un usuario de mínimo privilegio.

Limpieza de Capas: Se aplican técnicas de optimización para mantener imágenes livianas y eficientes.

Orquestación con Docker Compose
Se incluye un archivo docker-compose.yml que permite levantar el stack completo (servicios, redes y volúmenes) de forma individual o conjunta.
- Redes Internas: Se definen redes para aislar el tráfico entre el Backend y la base de datos.
- Dependencias: Configuración de depends_on para asegurar el orden correcto de inicio de los servicios.

3. Persistencia de Datos
Tipo de Volumen: Named Volume

Justificación Técnica: Se eligió este tipo de volumen para garantizar que la información crítica del Backend o la base de datos sea persistente ante reinicios o fallos de los contenedores.

4.Infraestructura en AWS y Conectividad
El despliegue se realiza sobre instancias EC2 configuradas previamente:

-Frontend: Accesible públicamente mediante su IP pública o dominio en el puerto configurado.
-Backend: Ejecución estable con conectividad restringida, respondiendo únicamente a peticiones del Frontend bajo las políticas de los Security Groups.
-Seguridad de Red: Se garantiza que solo el Frontend sea accesible desde Internet, manteniendo el Backend protegido.

6. Principios DevOps Aplicados
Este proyecto implementa prácticas de DevOps reales para favorecer la escalabilidad y mantenibilidad:

-Trazabilidad: Control de versiones con un historial de commits explicativos.
-Automatización: Eliminación de procesos manuales mediante CI/CD
-Consistencia: Gestión de entornos mediante contenedores para evitar el "funciona en mi máquina"
