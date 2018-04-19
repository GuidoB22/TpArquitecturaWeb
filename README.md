 **Trabajo practico Arquitectura Web**
 
* Nombre de grupo:PalermoSoft
* Integrantes: Guido Besozzi
* Integrantes: Guido Besozzi, Lopolito Gonzalo.
* Descripción: Vamos a modelar un sistema de venta de prendas por catalogo
 
Alcance: Se van a poder de cargar en el back-end prendas en un catálogo con nombre, imagen, descripción y precio.

   title: 'Catalogo Para Ventas'
   description: 'Aplicación para generar catálogos WEB para venta de indumentaria.'


paths: {


  /login: #todos mis endpoints que tengan: la accion, el path , parametros de entrada, el body (si llego a tener y para esto el response), codigo de error / cambiar LOS MODIFICAR Y BORRAR! SACAR LAS ACCIONES Y PONER SOLO RECURSOS!

    post /login
      summary: Envío de usuario y contraseña a validar.
      Param:no 					#preguntarle si esto significa parametros desde el body?(body?)

      Body:
        content:
          application/json: 
            {
              
                usuario:          # <--- campo form para Nombre
                  type: string
                pass:    # <--- campo form para Pass
                  type: string
              
             }
    responses:
      '200':
          description: Se ingreso al sistema con usuario Administrador.
          <link rel="/usuario/catalogos" uri="/$usuario/catalogos"/>  #se  usa asi "uri"? $relaciono al usuario ingresado y catalogos no hace falta con relacion $
      
      '404':
          description: No se pudo encontrar el usuario enviado.
          
 /usuario/catalogos

	post usuario/catalogos
	Param:
        summary: Elegir el catalogo a modificar
        Body
        content:
              application/json:
              {
					Id:
					 type: integer
              }
    responses:
    	'200':
    	description: Se ingreso al sistema con usuario Administrador.
          <link rel="/usuario/catalogos/catalogo" uri="/$usuario/catalogos/$catalogo"/>
    		

/usuario/catalogos/nuevocatalogo
	
	post usuario/catalogos
	Param:
        summary: Crear un nuevo catalogo.
        Body
        content:
              application/json:
              {
					Id:
					 type: integer
					Descripcion:
					 type: String
              }
    responses:
    	'200':
    	description: Se crea un nuevo catalogo y te accede al mismo.
          <link rel="/usuario/catalogos/catalogo" uri="/$usuario/catalogos/$catalogo"/>
        '400?'




/usuario/catalogos/catalogo/producto

#listar productos

 get:
        summary: Solicitud de productos a modificar
    
    responses:
      '200': Ok. 
      description: Se envia el listado completo de productos
      requestBodies:
        required: true
        content:
          application/json:
            
              type: object
              properties:
                nombre:          
                  type: string
                descripcion:    
                  type: string
                foto:
                  content: image/*: 
                precio:
                  type: double
                tipoProducto: 
                  type: string #es string o object debido a que es otra entidad?
          400:
            description: Error en en la respuesta.
	
	post usuario/catalogos/catalogo/producto
	Param:
        summary: ingreso de nombre de producto a modificar
        Body
        content:
              application/json:
              {
					nombre:
					 type: integer
              }
    responses:
    	'200':
    	description: 
          <link rel="/usuario/catalogos/catalogo/producto/nombre" uri="/$usuario/catalogos/catalogo/$nombre"/> ##.-----------------??


/usuario/catalogos/productos/nombre
	
	      post:
          description: solicitud de datos POR NOMBRE del producto ingresado.
          	Body:
            required: true
            content:
              application/json:
                {
                    nombre:
                      type: string #cambiar por id del producto
                }
              
    responses:
        '404': El nombre ingresado no existe.
        

        '200': Ok. 
                 description: Se envia el producto con los campos para ser modificados
                  Body:
                  required: true
                   content:application/json: 
                   {
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
                
      			put:
        		description: Modificacion producto
        		Body:
          		required: true
          		content:application/json: 
          		{
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



    responses:
                
            '201': producto Modificado.
            '400': El nombre de producto ingresado ya se ecuentra utilizado.
#-----------------------------------------------------hasta aca modifique!!!!!!!!! 19/4 G.B

	
    post
    Param:
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

/Ingreso/abm/modificar/modpornombre:


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
      

 /productos

        

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