# PRÁCTICA  PR0501: APLICACIÓN DE DIRECTIVAS
## CARACTERÍSTICAS:
- Dominio: aso.local
- Unidades organizativas
  - Usuarios: contiene los usuarios del dominio divididos en dos unidades organizativas:
    - management
    - development
  - Equipos: contiene los equipos de los empleados
### Creamos las unidades organizativas con powershell
![Creación unidades organizativas](image.png)
### Se podía haber realizado desde Usuarios y equipos de Active Directory. 
### Continuamos incorporando los usuarios a las unidades organizativas, de modo que Aperez pertenezca a la unidad development y Fgonzalez a la UO management. El cambio lo he realizado arrastrando los usuarios a su carpeta.
![Usuario Aperez](image-1.png)
![Usuario Fgonzalez](image-2.png)
### Directiva 1. No se puede cambiar el fondo de pantalla del escritorio. Se aplica a los usuarios del grupo management
#### Entramos en Herramientas>Administración de directivas de grupo>Objetos de directiva de grupo> Default Domain Controllers Policy>Configuración>En un espacio en blanco clicar con el botón derecho y seleccionar Editar para que se abra el Editor de directivas de grupo>Configuración de usuario>Directivas>Plantillas administrativas>Active Desktop>Active Desktop>Tapiz del escritorio. Clicando dos veces se abre una nueva ventana.

