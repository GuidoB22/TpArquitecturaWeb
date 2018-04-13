swagger: '2.0'
info:
  version: "1.6real"
  title: 'Tienda Online'
  description: 'Tienda Tp Arquitectura WEB'
paths: {
  /login: #todos mis endpoints que tengan la accion, el path , parametros de entrada, el body (si llego a tener y para esto el response), codigo de error / cambiar LOS MODIFICAR Y BORRAR! SACAR LAS ACCIONES Y PONER SOLO RECURSOS!

    post:
      summary: Envío de usuario y contraseña a validar.
      Body:
        content:
          application/json: # es la forma que usa swagger para devolver forms
            {
              
                usuario:          # <--- campo form para Nombre
                  type: string
                pass:    # <--- campo form para Pass
                  type: string
              
             }
    responses:
      '200':
          description: Se ingreso al sistema con usuario Administrador.
      
      '404':
          description: No se pudo encontrar el usuario enviado.
          
          
          
  /productos: 
    post:
        tags:
        - Crear Productos
        summary: Crea un nuevo producto para mostrar en el catalogo.
  
        Body:{
          required: true
          content:application/json: # es la forma que usa swagger para devolver forms
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
                }
              # hasta aca modifique en la clase!


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
          400:
            description: Error en en la respuesta.

        

    /productos/:nombre:        
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

    /productos/:tipoproducto:        
      get:
        tags:
        - solicitud pe productos por TIPO DE PRODUCTO
        summary: 
        operationId: idconsulta
        description: solicitud de PRODUCTOS POR TIPO DE PRODUCTO
          requestBodies:
            required: true
            content:
              application/json:
                schema:
                  type: object
                  properties:
                    tipoproducto:
                      type: string #es string o object debido a que es otra entidad?
              
  
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
                  '404': El tipo de producto ingresado no fue encontrado
                    description: Error en en la respuesta.
  
  
  
  
  
  
  
}
# Added by API Auto Mocking Plugin
host: virtserver.swaggerhub.com
basePath: /GuidoB22/TiendaUP/1.0
schemes:
 - https