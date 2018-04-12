swagger: '2.0'
info:
  version: "1.4"
  title: 'Tienda Online'
  description: 'Tienda Tp Arquitectura WEB'
paths: {
  /Ingreso:
  #tengo que tener un get antes, que me traigar el form que solicite usuario y contraseña? o se le pasa un post con el usuario y contraseña y que ingrese?#
    get:
      summary: Solicitud de campos para ingreso a usuario administrador.
    
    responses:
      '200': Ok. 
      description: Se envian los campos usuario y pass para completar.
      requestBodies:
        required: true
        content:
          application/x-www-form-urlencoded:
            schema:
              type: object
              properties:
                usuario:
                  type: string
                contraseña:
    
    post:
      summary: Envío de usuario y contraseña a validar.
      requestBody:
        required: true
        content:
          application/x-www-form-urlencoded: # es la forma que usa swagger para devolver forms
            schema:
              type: object
              properties:
                usuario:          # <--- campo form para Nombre
                  type: string
                pass:    # <--- campo form para Pass
                  type: integer
              required:
                - name
                - pass
    
    responses:
      '200':
          description: Se ingreso al sistema con usuario Administrador.
      
      '404':
          description: No se pudo encontrar el usuario enviado.
          
          
          
  /Ingreso/abm:
    post:
        tags:
        - Crear Productos
        summary: Crea un nuevo producto para mostrar en el catalogo.
        operationId: crearProducto
        description: Crea un producto.
        requestBody:
          required: true
          content:application/x-www-form-urlencoded: # es la forma que usa swagger para devolver forms
            schema:
              type: object
              properties:
                nombre:          
                  type: string
                descripcion:    
                  type: string
                foto:
                  content: image/*: ##chequear si es type como los otros o content como dice carga de archivos en swagger tut
                precio:
                  type: double
                tipoProducto: 
                  type: string # es string o es object? debido a que es otra entidad ? 
                
              required:
                - name
                - descripcion
                - foto
                - precio
                - tipoProducto


    responses:
          201:
            description: producto Creado.
          400:
            description: ingreso Invalido, Objeto invalido.
          409:
            description: el Producto ya existe.
# cambiar por get para traer productos y luego la sintaxis que se valla a hacer modificar =PUT(update)  eliminar =delete
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
      
      
      
 ## ----------------------------------------------------------------
 # A PARTIR DE ACA !poner las validaciones en body con el "requestBody" antes utilizado
      

      /productos:
      get:
        tags:
        - Productos
        summary: mostrar catalogo completo.
        operationId: searchInventory
        description: Muestra la totalidad de los productos disponibles en el catalogo.
        produces:
        - application/json
        responses:
          200:
            description: Obtener la lista completa de productos.
            schema:
              type: array
              items:
                $ref: '#/' # es a donde estan los archivos en ruta por ej si se guardan los produictos en prodcutos/prod.txt
          400:
            description: Error en en la respuesta.

        

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
  
  
  
  
  
  
  
  
}
# Added by API Auto Mocking Plugin
host: virtserver.swaggerhub.com
basePath: /GuidoB22/TiendaUP/1.0
schemes:
 - https
  
  
  
  
}
# Added by API Auto Mocking Plugin
host: virtserver.swaggerhub.com
basePath: /GuidoB22/TiendaUP/1.0
schemes:
 - https