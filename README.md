Autor: Sergio Gabriel Chaves Mosquera

Asignación: Taller de Parcial 1

Descripción: En este repositorio se encuentra el taller preparativo para el primer parcial del curso. Este se encuentra en el archivo "Taller de Parcial 1 - Sergio Chaves.pdf" el cual contiene el taller brindado por el profesor anteriormente con los enunciados originales y con las respuestas de cada ejercicio anexadas justo a continuación del mismo. Se empleó la fuente "Ancizar Sans", las respuestas se diferencian de los enunciados mediante el uso del color rojo y subtitulos del mismo color. 

Tambien en la parte posterior de este readme se encuentran anexadas todas las respuestas en formato de texto con la enumeración correspondiente a cada uno de los puntos del taller

----------------------------------------------------------------------------------

Parte A. Conceptos y lectura de Código


1. Respuesta: Las opciones A, B y D son correctas.

      Opción A: Es correcta porque el atributo x es publico

      Opción B: Es correcta porque el atributo _y esta protegido, pero esto no restringe su acceso

      Opción C: No es correcta porque el atributo __z es privado y provocaría un AtributeError

      Opción D: Es correcta porque, aunque el atributo __z es privado, con el name mangling se puede acceder sin problemas.

2. Respuesta: Imprime False True, porque en la primera pregunta, no contiene ‘__secret’ porque ya se establece anteriormente que a=A(), entonces el atributo queda ‘_A__secret’ lo que hace que en la segunda pregunta, la respuesta sea True

3.   
      a) El prefijo _impide el acceso desde fuera de la clase. 
  
      Respuesta:  Falso, porque él _ lo único que hace es la convención de público a protegido, pero esto no hace ninguna restricción, es una convención para la organización del programador 

      b) El prefijo __hace imposible acceder al atributo.
  
      Respuesta:  Falso. Aunque “dificulta” el acceso a como lo seria si el atributo tuviera _ o solamente no tuviera ningún prefijo, aun se puede acceder mediante la estructura _clase__atributo
  
      c) El name mangling depende del nombre de la clase.
  
      Respuesta:  Verdadero. El name mangling lo que permite es acceder a atributos añadiendo como prefijo el nombre de la clase, manteniendo esta estructura: _nombredelaclase__nombredelatributo



4. Respuesta:  “abc”. No hay error de acceso debido a la herencia, porque class Sub(Base): tiene herencia con la clase Base, entonces hereda tambien el metodo self._token = “abc”

5. Respuesta:  “2 1”.  Sub sobreescribe los datos de la clase Base con su metodo show(), debido a la herecia, al cual le da el valor de 2 al atributo __v, y luego con super() se crea el nuevo atributo  __v =1

6. Respuesta:  Genera un error, porque el atributo “y” no esta declarado ni en el metodo __slots__ ni se esta llamando de manera correcta desde c

7. Respuesta:  self._nombredeunatributo=99
Cualquier nombre que comience con _

8. Respuesta:  Imprime “True False True”
Porque si existe el metodo step() en M y es protegido, False pq esta llamando al metodo __tick como si fuera de la misma clase m, y no se puede, porque es privado, por lo que la ultima es True, pq aqui si lo llama de manera correcta.

9. Respuesta:   print(s._S__data)

10. Respuesta:   _D__a 
Porque pues __a no se puede porque estamos llamando antes d=D() entonces toca hacer el name mangling para poder acceder a este atributo privado y a no se puede porque es privado, entonces si o si, tiene que tener la nomenclatura antes de prefijo __
La unica que cumple con la condicion seria _D__a

--------------------------------------------------------------------------------------------------------------

Parte B. Encapsulación con @property y validación

11. 

        class Cuenta:
        		def __init__(self, saldo): 
        		self._saldo = 0 
        		self.saldo = saldo
        
        	@property
        		def saldo(self): 
        		return self._saldo
        
        	@saldo.setter
        		def saldo(self, value): 
        		# Validar no-negativo 
        		if value < 0:
        			 raise ValueError(“El saldo no puede ser negativo”)
        		else:
        			self._saldo = value

12.
  
       class Termometro:
         def __init__(self, temperatura_c): 
           self._c = float(temperatura_c)
              
              	# Define aquí la propiedad temperatura_f: F = C * 9/5 + 32
              	Escribe la propiedad.
              
              	@property
              	def temperatura_f(self):
              		return (self._c*9/5+32)

13. 

        class Usuario:
		      def __init__(self, nombre): 
		        self.nombre = nombre

        	# Implementa property para nombre
        	@property
            	def nombre(self):
                		return self._nombre
        
        	@nombre.setter
            	def nombre(self, value):
        		if not isinstance(value, str):
        			raise TypeError("El nombre debe ser tipo string")
        		self._nombre = value

14.

        class Registro:
		      def __init__(self): 
		        self.__items = []

		      def add(self, x): 
		        self.__items.append(x)

          # Crea una propiedad 'items' que retorne una tupla inmutable con el contenido
        	@property
            def items(self):
                return tuple(self._items)

--------------------------------------------------------------------------------------------------------------

Parte C. Diseño y refactor

15. 

        class Motor:
        	def __init__(self, velocidad):
        		self.velocidad = velocidad # refactor aquí
        
        
        Escribe la versión con @property.
            @property
            def velocidad(self):
                return self._velocidad
        
            @velocidad.setter
            def velocidad(self, value):
                if not (0 <= value <= 200):
                    raise ValueError("La velocidad debe estar entre 0 y 200")
                self._velocidad = value

16. Respuesta: Las convenciones _atributo, las usaria para todo lo que tenga que estar relacionado entre clases, como por ejemplo en objetos como Estudiante, en las que tambien esten relacionadas las clases Pregrado y Posgrado, las usaria para los atributos que tengan en comun se relacionen entre ellas, sin ser publicos con todas las demas clases, como _matricula, _avance, etc. Las convenciones __atributo, las usaria para todo lo que sea especifico de la clase y por privacidad o simplemente comodidad, no deba ser compartido con otras clases, como por ejemplo en la clase Estudiante, atributos como __documentoid, __pbm, entre otras.

17. Respuesta: El problema es que el método get_data() devuelve directa la lista interna _data. No devuelve una copia, sino la lista original.

        class Buffer:
            def __init__(self, data):
                self._data = list(data)
        
            def get_data(self):
                # Devolvemos una tupla, que es una copia inmutable.
                return tuple(self._data)

18. Respuesta: Este codigo fallara en la ultima linea porque “return self.__x” esta escrito de manera incorrecta, ya que para mencionar un atributo privado, aunque se tenga herencia, se debe hacer name mangling con el prefijo _nombredelaclase.
            
            return self._A__x

19.

        class _Repositorio:
        		def __init__(self): 
        		self._datos = {}
        		def guardar(self, k, v): 
        		self._datos[k] = v
        	def _dump(self):
        		return dict(self._datos)
        
        
        class Servicio:
        	def __init__(self):
        		self._repo = _Repositorio()
        
        
        # Expón un método 'guardar' que delegue en el repositorio, # pero NO expongas _dump ni _repo.
        
        	#Aqui iria el codigo brindado anteriormente, class _Repositorio, class Servicio…
        	def guardar(self, k, v):
        		self._repo.guardar(k, v)

20.

        class ContadorSeguro:
            def __init__(self):
                self._n = 0
            def __log(self):
                print("tick")    
            def inc(self):
                self._n += 1
                self.__log()        
            @property
            def n(self):
                return self._n
        contador = ContadorSeguro()
        contador.inc()
        contador.inc()
        print(contador.n)

