# Prueba Técnica JavaScript + Node.js

Escribe las soluciones en el archivo `solutions/index.js` manteniendo el nombre de las funciones y sus `export`. Usa `ESModules` en tu proyecto de Node.js

1 - Arregla esta función para que el código posterior funcione como se espera:

```javascript
import net from 'node:net'

export const ping = (ip) => {
  const startTime = process.hrtime()

  const client = net.connect({ port: 80, host: ip }, () => {
    client.end()
    return { time: process.hrtime(startTime), ip }
  })
  
  client.on('error', (err) => {
    throw err
    client.end()
  })
}

ping('amazon.com', (err, info) => {
  if (err) console.error(err)
  console.log(info)
})
```

2 - Explica qué hace la funcion. Identifica y corrige los errores en el siguiente código. Si ves algo innecesario, elimínalo. Luego mejoralo para que siga funcionando con callback y luego haz lo que consideres para mejorar su legibilidad.

```javascript
export function procesarArchivo() {
  fs.readFile('input.txt', 'utf8', (error, contenido) => {
    if (error) {
      console.error('Error leyendo archivo:', error.message);
      return false;
    }

    setTimeout(() => {
      const textoProcesado = contenido.toUpperCase();

      fs.writeFile('output.txt', textoProcesado, error => {
        if (error) {
          console.error('Error guardando archivo:', error.message);
          return false;
        }

        console.log('Archivo procesado y guardado con éxito');
        return true
      });

    }, 1000);
  });
}
```
3. Vamos a crear nuestra propia utilidad `dotenv` en el archivo `dotenv.js`.

- La utilidad debe devolver un método `config` que lee el archivo `.env` y añade las variables de entorno que haya en el archivo al objeto `process.env`.
- Por ejemplo si tu archivo `.env` contiene:

```sh
PORT=8080
TOKEN="123abc"
```

Entonces podríamos hacer esto:

```javascript
const dotenv = require("./dotenv.js");
dotenv.config()

console.log(process.env.PORT) // "8008"
console.log(process.env.TOKEN) // "123abc"
```

También se le puede pasar el path del archivo `.env` como parámetro:

```javascript
const dotenv = require("./dotenv.js");
dotenv.config("./config/.env.local")
```

Cosas a tener en cuenta:

- Sólo se permite usar el módulo `fs` para leer el archivo.
- Si el archivo no existe, no debe dar error, simplemente no hace nada.
- Si el archivo existe, pero no tiene ninguna variable de entorno, no debe hacer nada.
- Sólo debe soportar el archivo `.env` o el que se le pasa como parametro, no hace falta que soporte `.env.local`, `.env.development` y similares de forma automática.
- Las variables de entorno siempre son strings, por lo que si en el archivo `.env` hay un número, por ejemplo `PORT=8080`, al leerlo con `fs` y añadirlo a `process.env` debe ser un string, no un número.
- `process.env` es un objeto y, por lo tanto, es mutable. Esto significa que podemos añadir propiedades nuevas sin problemas.

4 - Diseña una API REST utilizando Express que permite a los usuarios crear, leer, modificar, actualizar y eliminar elementos de una lista.

La lista tendrá objetos que tienen la siguiente forma:

```javascript
{
  id: 1,
  content: 'Item 1'
}
```

Haz la solución en el archivo `solutions/server.js` y exporta el `app` y `server` creado.
Instala Express con `npm install express`. No te preocupes por CORS.
