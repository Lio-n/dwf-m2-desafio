# Desafío del módulo 2

### **Condiciones del desafio**

- Forkeá y cloná este repo: https://github.com/zapaiamarce/dwf-m2-desafio

- Creá un archivo JSON con películas. Con este formato:
  ```
  id: number;
  title: string;
  tags: string[];
  ```

1. ### **En models.ts:**
   - Tomá la estructura base y **completá la clase PelisCollection**. Además, agregale a esta clase los siguientes **métodos asincrónicos** (o sea que todos deben devolver una promesa que a su vez devuelva lo indicado en cada método):
     - **getAll()** devuelve un array del tipo Peli con todas las pelis que se encuentren guardadas en el archivo JSON de pelis.
     - **getById(id:number)** devuelve la peli que tenga el id que se le pase por parámetro.
     - **search(options:any)** recibe un objeto y, según cuales sean sus propiedades, hay dos opciones:
       - **si el objeto tiene la propiedad title**, el método tiene que devolver todas las películas que tengan ese string en su title. (Por ejemplo si search es "a" debe devolver todas las películas que tengan la letra "a" en su title.)
       - **si el objeto tiene la propiedad tag**, el método tiene que devolver todas las películas que tengan ese string en sus tags. (Por ejemplo si tags es "classic" debe devolver todas las películas que tengan el tag "classic".)
     - **add(peli:Peli)** recibe una Peli y la guarda en el archivo. Tiene que devolver un boolean que indique si se agregó correctamente la peli. No debe admitir agregar IDs repetidos. O sea que, si no pudo guardar el dato en el archivo por algún error de escritura o por que el id está duplicado, debe devolver false.

2. ### **En controller.ts:**
    - Instanciá el modelo PelisCollection y guardalo en una propiedad interna del controller.
   - Tomá la estructura base y completá la clase PelisController. Además, agregale a esta clase los siguientes métodos asincrónicos que tienen que usar los métodos del modelo para interactuar con la data:
     - get(options) recibe un objeto y, según cuales sean sus propiedades, hay dos opciones:
       - si el objeto tiene la propiedad id (ej: { id:1234 }), debe devolver la película con ese id.
       - si el objeto tiene la propiedad search (que es un objeto) y:
         - si el objeto search tiene la propiedad title, debe buscar las pelis que tengan ese string en el título. (ej: { search:{ title:"ju" } })
         - si el objeto search tiene la propiedad tag, debe buscar las pelis que tengan ese tag. (ej: { search:{ tag:"action" } })
puede recibir las dos opciones. (ej: { search:{ tag:"action", title:"x" } } busca pelis con el tag action y que tengan la letra x en su title)
       - si no recibe ningún parámetro, debe devolver todas las películas.

      - add(peli:Peli) recibe un objeto y crea una peli en base a él. (Ej.: { id:4421, title:"Una peli", tags:["classic","action"] })

3. ### **En index.ts:**

    - Parseá los argumentos de la terminal.
    - Usá la librería [minimist](https://www.npmjs.com/package/minimist). Los comandos que deberían funcionar son los siguientes:



        ````
        ts-node index.ts add --id=4411 --title="Título de la nueva peli" --tags=action --tags=classic
        ````
        ````
        ts-node index.ts get 4411
        ````
        ````
        ts-node index.ts search --title="a"
        ````
        ````
        ts-node index.ts search --tag="classic"
        ````
        ````
        ts-node index.ts search --title="x" --tag="action"
        ````
        ````
        ts-node index.ts (este último comando debe devolver todas las películas)
        ````
