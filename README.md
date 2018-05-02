 **Trabajo practico Arquitectura Web**
 
* Nombre de grupo:PalermoSoft
* Integrantes: Guido Besozzi, Lopolito Gonzalo.
* Descripción: Vamos a modelar un sistema de venta de prendas por catalogo
 
Alcance: Se van a poder de cargar en el back-end prendas en un catálogo con nombre, imagen, descripción y precio.

   title: 'Catalogo Para Ventas'
   description: 'Aplicación para generar catálogos WEB para venta de indumentaria.'

#poner los gets con query. (query.string, etc, AVERIGUAR y cambiarlos)
# agregar formato dinamico /productos/:id o /productos/:nombre
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
	Param: no
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
	Param: no
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




/usuario/catalogos/catalogo/producto                                      -------listar productos -> cambiar producto por productos? por logica q traera todos los productos?



 get:
        summary: Se envia el listado completo de productos correspondientes al catalogo en el que me encuentro
    
    responses:
      '200': Ok. 
      description: Se envia el listado completo de productos
      Body:
        required: true
        content:application/json:
            {
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
                Catadogo_id:
                	type: integer
            }
          400:
            description: Error en en la respuesta.
        

/usuario/catalogos/productos/nombre
	
	     post usuario/catalogos/catalogo/producto
		 Param: no
         summary: ingreso de nombre de producto a modificar ##----------> cambiar por id?
         Body:
         content:application/json:
              {
					nombre:
					 type: integer
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
                        Catadogo_id:
                			type: integer
                
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
                Catadogo_id:
                	type: integer
                }
    responses:
                
            '201': producto Modificado.
            '400': El nombre de producto ingresado ya se ecuentra utilizado.


/usuario/catalogos/productos/NuevoProducto

    	post
    	Param:
        tags:
        - Crear Producto
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
                Catadogo_id:
                	type: integer
                }
    responses:
          201:
            description: producto Creado.
          400:
            description: ingreso Invalido, Objeto invalido.
          409:
            description: el Producto ya existe.

 




/usuario/catalogos/producto

      delete /usuario/catalogos/producto
        tags:
        - Eliminar producto por nombre.( que supuestamente va a ser unico y no vamos a usar id de producto¿?)
         Body:
            required: true
            content:application/json:
                    nombre:
                      type: string #cambiar por id del producto
              
  
                responses:
                '200': El producto fue eliminado
                '200': Ok. 
                
      

/catalogos

	GET usuario/catalogos
	Param: no
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
          <link rel="catalogos/catalogo" uri="catalogos/$catalogo"/>
    		
/catalogos/catalogo

		GET /catalogos/catalogo
        summary: Se envia el listado completo de productos correspondientes al catalogo en el que me encuentro
    	responses:
     	 '200': Ok. 
     	 description: Se envia el listado completo de productos
      Body:
        required: true
        content:application/json:
            {
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
                Catadogo_id:
                	type: integer
            }
          400:
            description: Error en en la respuesta.
        
/catalogos/producto/nombre
	
	     GET usuario/catalogos/catalogo/producto
		 Param: no
         summary: ingreso de nombre de producto a visualizar ##----------> cambiar por id?
         Body:
         content:application/json:
              {
					nombre:
					 type: integer
              }
              
    responses:
        '404': El producto ingresado no existe.
        
        '200': Ok. 
                 description: Se envian los datos del producto solicitado
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
                        Catadogo_id:
                			type: integer
                
                   	}


catalogos/producto/tipoproducto:
		
		GET usuario/catalogos/catalogo/tipoproducto
		 Param: no
         summary: ingreso el id de los tipo de productos a visualizar 
         Body:
         content:application/json:
              {
					nombre:
					 type: integer
              }
              
    responses:
        '404': El tipo de producto ingresado no existe.
        
        '200': Ok. 
                 description: Se envian los datos de los productos del tipo de producto solicitado
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
                        Catadogo_id:
                			type: integer
                
                   	}

  
#-----------------------------------------------------hasta aca modifique!!!!!!!!! 20/4 G.B

#--cambiar por get para traer productos y luego la sintaxis que se valla a hacer modificar =PUT(update)  eliminar =delete

  
  
}