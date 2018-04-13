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
          
          
          
  /Ingreso/abm/crear: 
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
/Ingreso/abm/listar:
      get:
        summary: Solicitud de productos a modificar
    
    responses:
      '200': Ok. 
      description: Se envia el listado completo de productos
      requestBodies:
        required: true
        content:
          application/x-www-form-urlencoded:
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
                  type: string #es string o object debido a que es otra entidad?
/Ingreso/abm/modificar/modpornombre:

      get:
        tags:
        - solicitud por nombre de producto a modificar
        summary: 
        operationId: idmod
        description: solicitud de datos POR NOMBRE del producto ingresado.
          requestBodies:
            required: true
            content:
              application/json:
                schema:
                  type: object
                  properties:
                    nombre:
                      type: string #cambiar por id del producto
              
  
                responses:
                '404': El nombre ingresado no existe.
                '200': Ok. 
                 description: Se envia el producto con los campos para ser modificados
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
                
                
      put:
      tags:
        - Modificacion del producto
        summary: Modifica el producto
        operationId: ModProd
        description: Modificacion producto
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
                
                '201': producto Modificado.
                '400': El nombre de producto ingresado ya se ecuentra utilizado.

/Ingreso/abm/modificar/eliminarpornombre:

      delete: # o post?
        tags:
        - Eliminar producto por nombre.
        summary: 
        operationId: idmod
        description: eliminacion de producto por nombre
          requestBodies:
            required: true
            content:
              application/json:
                schema:
                  type: object
                  properties:
                    nombre:
                      type: string #cambiar por id del producto
              
  
                responses:
                '200': El producto fue eliminado
                '200': Ok. 
                
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