[[GIT]]

1. `git init`: Este comando se usa para inicializar un nuevo repositorio de Git en un directorio vacío o existente. Crea una estructura interna de Git en el directorio, lo que permite que Git comience a rastrear los cambios en los archivos en ese directorio.
    
2. `git status`: Muestra el estado actual del repositorio de Git. Te proporciona información sobre qué archivos han sido modificados, agregados o eliminados, y si estos cambios han sido o no confirmados (commited) en el repositorio.
    
3. `git add .`: Este comando agrega todos los archivos modificados en el directorio de trabajo al área de preparación (staging area) de Git. Los archivos en el área de preparación están listos para ser confirmados en el repositorio en el siguiente paso.
    
4. `git commit -m "mensaje"`: Crea un commit (confirmación) con los cambios que se encuentran en el área de preparación. Los cambios confirmados se almacenan en el historial del repositorio junto con un mensaje descriptivo proporcionado después de la opción `-m`. El mensaje debe ser informativo y describir brevemente los cambios realizados en esta confirmación.
    
5. `git remote add origin https://github.com/Valentespiegel/Notas.git`: Este comando establece una conexión remota entre tu repositorio local y un repositorio remoto en GitHub (u otra plataforma similar). "Origin" es el nombre que se le da a esta conexión remota, y la URL especificada es la ubicación del repositorio remoto en GitHub.
    
6. `git push origin master`: Finalmente, este comando envía tus confirmaciones locales al repositorio remoto (en este caso, llamado "origin") en la rama "master". Esto significa que tus cambios locales se reflejarán en el repositorio remoto y estarán disponibles para otros colaboradores o personas que accedan al repositorio remoto. La rama "master" es la rama principal por defecto en muchos repositorios, aunque este nombre puede variar según la configuración del proyecto.