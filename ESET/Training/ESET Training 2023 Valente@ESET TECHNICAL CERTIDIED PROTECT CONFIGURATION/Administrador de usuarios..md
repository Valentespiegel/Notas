[[ESET]]

![[Pasted image 20230614142426.png]]

Los administradores del servidor ESET Protect y sus roles administrativos se pueden configurar en la pestaña Mas > Permisos de usuarios.
Los usuarios y los conjuntos se administran por separado.
![[Pasted image 20230614142629.png]]

La cuenta de usuario adminstrador se crea de forma predeterminada durante  la instalacion. Se pueden agregar nuevos usuarios manualmente al grupo de usuarios nativos oh usar los grupos de seguridad del dominio.

Cuando se crea un nuevo usuario, solo existen dos configuraciones obligatorias: el nombre de usuario y contraseña.
El administrador puede habilitar/deshabilitar la cuenta o hacer que un usuario cambie ña contraseña en el próximo inicio de sesión.
![[Pasted image 20230614143135.png]]
Se pueden asignar grupos de permisos múltiples a un usuario directamente durante la creación de su cuenta.
Los permisos de acceso finales asignados a un usuario son un resumen de todos los permisos en todos los grupos de permisos asignados a dicho usuario.
![[Pasted image 20230614143620.png]]

A continuación , la nueva cuenta de usuario se incluye en la lista junto con los demás usuarios creados o predefinidos.
Se pueden ver todas las configuraciones y la información sobre el usuario desde la ventana de permisos.
El administrador puedes usar los grupos de permisos predefinidos o crear uno nuevo mas especifico.
![[Pasted image 20230614143843.png]]
Por ejemplo si una empresa tiene una sucursal técnica y el administrador desea contra con un administrador local que tenga acceso restringido a ESET PROTECT, crea un grupo de permisos para un nuevo usuario que solo pueda realizar el grupo de acciones especificas. Este ejemplo, Sera un Grupo de permisos locales.
![[Pasted image 20230614144200.png]]
El campo funcionalidad le permite al administrador establecer específicamente lo que el usuario puede hacer y no.

==Permiso de lectura

Le permite al usuario ver el componente/la configuración, pero no interactuar.

==Permiso de escritura/ejecución

Otorga el control completo sobre el componente seleccionado.




