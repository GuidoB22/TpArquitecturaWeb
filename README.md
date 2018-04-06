**Trabajo practico Arquitectura Web**

* Nombre de grupo:PalermoSoft
* Integrantes: Guido Besozzi, Lopolito Gonzalo.
* Descripción: Vamos a modelar un sistema de venta de prendas por catalogo

Alcance: Se van a poder de cargar en el back-end prendas en un catálogo con nombre, imagen, descripción y precio.
A estas predas vamos a poder agregar, modificar y quitar del Catálogo.


-Ver como se ingresa el body en swagger para el POST de ingreso de usuario
-Terminar de sacar catalogo del sistema 


swagger: '2.0'
info:
  version: '0.1'
  title: 'Catalogo Para Ventas'
  description: 'Aplicación para generar catálogos WEB para venta de indumentaria.'
paths: 
 /ingreso:-----------------------------------
    post:
      tags:
      - Ingreso
      summary: Ingreso de usuario y contraseña.
      operationId: usuario,pass
      description: |
        Validación de usuario.
      produces:
      - application/json
      parameters:
      - name: usuario
        in: query
        description: El nombre del usuario.
        required: true
        type: string
      - name: password
        in: query
        description: La contraseña en texto plano.
        required: true
        type: integer
      responses:
        200:
          description: Ir a productos.
          schema:
            type: boolean
        400:
          description: Usuario o contraseña incorrecto.

  /productos:
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
      - name: nombre
        in: query
        description: El nombre del producto.
        required: true
        type: string

      - name: descripcion
        in: query
        description: La descripcion del producto.
        required: true
        type: string

        - name: foto
        in: query
        description: La imagen del producto.
        required: true
        type: image/png ------------------------------------------------------------------------

      - name: precio
        in: query
        description: El valor del producto.
        required: true
        type: double 

      - name: tipoProducto
        in: query
        description: El tipo de producto.
        required: true
        type: string
      responses:
        201:
          description: producto Creado.
        400:
          description: ingreso Invalido, Objeto invalido.
        409:
          description: el Producto ya existe.

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

  /productos/:nombre:        
    get:
      tags:
      - Buscar producto por nombre
      summary: mostrar el producto del "nombre".
      operationId: setNombre --------------------------------------------------------------
      description: | 
        id del producto.
      produces:
      - application/json
            parameters:
      - name: nombre
        in: query
        description: El nombre del producto.
        required: true
        type: string
      responses:
        200:
          description: Obtener el producto.
          schema:
            type: array
            items:
              $ref: '#/'
        400:
          description: Error en en la respuesta.

  /productos/:tipoproducto:        
    get:
      tags:
      - Buscar producto por tipo
      summary: mostrar productos por tipo.
      operationId: setNombre --------------------------------------------------------------
      description: | 
        id del producto.
      produces:
      - application/json
            parameters:
      - name: tipoproducto
        in: query
        description: el tipo de producto.
        required: true
        type: string
      responses:
        200:
          description: Obtener los productos por tipo.
          schema:
            type: array
            items:
              $ref: '#/'
        400:
          description: Error en en la respuesta.