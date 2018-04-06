**Trabajo practico Arquitectura Web**

* Nombre de grupo:PalermoSoft
* Integrantes: Guido Besozzi, Lopolito Gonzalo.
* Descripción: Vamos a modelar un sistema de venta de prendas por catalogo

Alcance: Se van a poder de cargar en el back-end prendas en un catálogo con nombre, imagen, descripción y precio.
A estas predas vamos a poder agregar, modificar y quitar del Catálogo.


swagger: '2.0'
info:
  version: '0.1'
  title: 'Catalogo Para Ventas'
  description: 'Aplicación para generar catálogos WEB para venta de indumentaria.'
paths: 
 /catalogo/ingreso/:usuario,pass:
    get:
      tags:
      - Ingreso
      summary: Ingreso de usuario y contraseña.
      operationId: usuario,pass
      description: |
        Validación de usuario.
      produces:
      - application/json
      responses:
        200:
          description: Ir a productos.
          schema:
            type: boolean
            items:
              $ref: '../catalogo/productos/'
        400:
          description: Error en en la respuesta.

  /catalogo/productos:
    get:
      tags:
      - Productos
      summary: mostrar catalogo completo.
      operationId: searchInventory
      description: |
        Muestra la totalidad de los productos disponibles en el catalogo.
      produces:
      - application/json
      responses:
        200:
          description: Obtener la lista completa de productos.
          schema:
            type: array
            items:
              $ref: '#/'
        400:
          description: Error en en la respuesta.
    post:
      tags:
      - Crear Productos
      summary: Crea un nuevo producto para mostrar en el catalogo.
      operationId: crearProducto
      description: Crea un producto.
      consumes:
      - application/json
      produces:
      - application/json
      parameters:
      - in: body
        name: nombre,descripcion,foto,precio
        description: parametros de nuevo producto. 
        schema:
          $ref: '#/'
      responses:
        201:
          description: producto Creado.
        400:
          description: ingreso Invalido, Objeto invalido.
        409:
          description: el Producto ya existe.
  /catalogo/productos/:id:        
    get:
      tags:
      - Buscar producto
      summary: mostrar catalogo completo.
      operationId: id
      description: | 
        id del producto.
      produces:
      - application/json
      responses:
        200:
          description: Obtener el producto.
          schema:
            type: array
            items:
              $ref: '#/'
        400:
          description: Error en en la respuesta.
    put:
      tags:
      - Modificar Producto
      summary: mostrar catalogo completo.
      operationId: idmod
      description: | 
        id del producto a modificar.
      produces:
      - application/json
      responses:
        201:
          description: producto Modificado.
        400:
          description: Modificación invalida, Objeto invalido.
    delete:
      tags:
      - Borrar Producto
      summary: mostrar catalogo completo.
      operationId: idEliminar
      description: | 
        id del producto a modificar.
      produces:
      - application/json
      responses:
        201:
          description: producto eliminado.
        400:
          description: Eliminación invalida, Objeto invalido.     