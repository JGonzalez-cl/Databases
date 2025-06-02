# REDIS

## STRINGS

- **Guarda un valor asociado a una clave**

        SET saludo "Hola"

- **Recupera el valor de una clave**

        GET saludo

- **Incrementa un valor numerico**

        SET visitas 1

        INCR visitas

- **Añade texto al final del valor**

        APPEND saludo ", soy Juan"

- **Guarda un valor con tiempo de expiracion**
  
        SETEX codigo 30 "12345"

- **Establce un tiempo de expiración en segundos para una clave**

        EXPIRE codigo 30

- **Elimina el tiempo de expiración de una clave**

        PERSIST codigo

## LISTS

- **Inserta elementos al inicio o al final de una lista**

        LPUSH tareas "leer"
        RPUSH tareas "estudiar"

- **Elimina y devuelve el primer/último elemento**
  
        LPOP tareas
        RPOP tareas

- **Muestra los elementos entre dos posiciones**
  
        LRANGE tareas 0 -1 (lista completa)

- **Longitud de la lista**

        LLEN tareas (devuelve numero)

## SETS

- **Añade un elemento (sin duplicados)**

        SADD frutas "manzana"
        SADD frutas "pera"
        SADD frutas "manzana" (no se repite)

- **Devuelve todos los miembros**

        SMEMBERS frutas

- **Comprueba si un valor existe**

        SISMEMBER frutas "pera"

- **Elimina un elemento**

        SREM frutas "pera"

- **Devuelve la diferencia entre dos conjuntos**

        SADD set1 "a" "b" "c"
        SADD set2 "b" "c" "d"
        SDIFF set1 set2 (resultado: "a")
        SDIFF set2 set1 (resultado: "d")

- **Devuelve la intersección de dos conjuntos**

        SADD set1 "a" "b" "c"
        SADD set2 "b" "c" "d"
        SINTER set1 set2 (resultado: "b", "c")

## ZSETS

- **Añade un valor con puntuación**

        ZADD ranking 100 "Ana"
        ZADD ranking 150 "Luis"

- **Devuelve elementos ordenados por su puntuación (menor a mayor)**

        ZRANGE ranking 0 -1 WITHSCORES

- **Orden inverso**

        ZREVRANGE ranking 0 -1 WITHSCORES

- **Incrementa puntuación**

        ZINCRBY ranking 52 "Ana" (se suma a la cantidad)

## HASHES

- **Añade un campo y valor a un hash**

        HSET user:1 nombre "Lucia"
        HSET user:1 edad 30

- **Recupera un campo específico**

        HGET user:1 nombre (resultado: "Lucia")

- **Todos los camps y valores**

        HGETALL user:1

- **Elimina un campo**

        HDEL user:1 edad

- **Devuelve el número de campos**

        HLEN user:1

- **Incrementa un campo numérico**

        HINCRBY user:1 edad 9

## BITMAPS

- **Modifica y consulta bits individuales**

        SETBIT flags 2 1
        GETBIT flags 2

- **Cuenta bits en 1**

        BITCOUNT flags 

## HYPERLOG

- **Estimación de elementos únicos**

        PFADD usuarios "juan" "ana" "luis"
        PFCOUNT usuarios

## GEO

- **Añade ubicación geográfica**

        GEOADD ciudades 13.361389 38.115556 "Palermo"
        GEOADD ciudades 15.087269 37.502669 "Catania"

- **Distancia entre puntos**

        GEODIST ciudades "Palermo" "Catania" km

- **Busca lugares a 200km de la coordenada 15 37**

        GEORADIUS ciudades 15 37 200 km

- **Devuelve la coordenada de una o más localizaciones**

        GEOPOS ciudades "Palermo" "Catania"

- **Obtener hash geoespacial**

        GEOHASH ciudades "Palermo"

## STREAMS

- **Añade un evento al stream**

        XADD mediciones * temperatura 22 (* = se generará un id automáticamente)

- **Elimina un mensaje por ID**
  
        XDEL mediciones 1689999999999-0

- **Muestra todos los registros**

        XRANGE mediciones - +
        XRANGE mediciones - + COUNT 10 (maximo 10 resultados)

- **Lee eventos del stream**

        XREAD COUNT 1 STREAMS mediciones <id>

        XREAD STREAMS mediciones 0

## TRABAJO CON CLAVES

- **Elimina una clave**

        DEL saludo

- **Tiempo de vida en segundos**

        EXPIRE codigo 30

- **Ver cuántos segundos le quedan**

        TTL codigo

- **Cambia el nombre de la clave**
  
        RENAME saludo saludo_nuevo

- **Lista todas las claves que coincidan**

        KEYS user:* (muestra todas las claves que coincidan con "user:")

## TRANSACCIONES

- **Agrupa comandos que se ejecutan juntos**

        MULTI
        SET producto "camisa"
        INCR stock
        EXEC

## PUB/SUB

- **Sistema de mensajería en tiempo real**

        SUBSCRIBE canal
        PUBLISH canal "¡Nuevo mensaje!"
