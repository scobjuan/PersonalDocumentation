# Documentacion VUEJS

<!-- Juan Andres Escobar -->

<!-- https://www.youtube.com/watch?v=Wd9dOIlTWCc -->

```vue
 <div id="app">
 </div>
```

Delimita el espacio de trabajo, todo lo que pongamos dentro de ese div, vuejs lo reconocera como una instancia de vue 



```vue
<script>
    const app = new Vue ({
        // Aqui estara toda la logica de vuejs
        el: "#app",
    })
</script>
```

Instanciamos vue y le pasamos el id (#) de nuestro espacio de trabajo (El div con el id "app")



```vue
<script> 
    data: {
		// Declaramos todas nuestras variables(datos)
    }
</script>
```

La data es el objeto utilizado para que vue interprete nuestros datos



```vue
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aprendiendo VUEJS</title>
</head>
<body>
    <div id="app">
        <h1>{{ message }}</h1>
        <ul>
            <li v-for="(show, posicionArray) in shows" v-bind:key="posicionArray">
                <strong>{{ show.name }}</strong> ({{ show.seasons }} Temporadas)
            </li>
        </ul>    
    </div>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.4.2/vue.js" integrity="sha512-njMD8/lt6qrl5S7BFajlL1KztlxeFyLYq/rkt395asAA8dz8uZaNU5VcAxL1DwZul9dmJk+or3HbjafV107ODA==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                message: 'Hola mundo de Vuejs',
                shows: [
                    {name: 'Game of thrones', seasons: 7},
                    {name: 'Breaking bad', seasons: 5},
                    {name: 'The walking dead', seasons: 12},
                    {name: 'The 100', seasons: 7}
                ]

            }
        })
    </script>
</body>
</html>
```

```vue
<h1>{{ message }}</h1>
```

En un h1, estamos mostrando la variable message



```vue
<ul>
    <li v-for="(show, posicionArray) in shows" v-bind:key="posicionArray">
        <strong>{{ show.name }}</strong> ({{ show.seasons }} Temporadas)
    </li>
</ul>
shows: [
    {name: 'Game of thrones', seasons: 7},
    {name: 'Breaking bad', seasons: 5},
    {name: 'The walking dead', seasons: 12},
    {name: 'The 100', seasons: 7}
]

```

En una lista desordenada estamos recorriendo el array shows con el metodo v-for y en el metodo :key, le pasamos el id por el que nos va ir listando y reconociendo cada registro dentro del array. Lo que hace que el front cargue mas rapido los datos de este objeto y se le haga todo mas facil. El listado de esta manera es mas eficiente





![Qué son las directivas de Vue? - Javascript en español](https://lenguajejs.com/vuejs/directivas-vue/que-son-directivas/directivas-vue.png)

**Nota: ** En si, lo que aqui estoy llamando metodos. Se llaman directivas: Las directivas son atributos especiales que se colocan en las etiquetas HTML, pero en si, son metodos. Ej. Cuando llamo a v-for y pongo entre comillas mi array (show in shows), le estoy pasando un parametro a ese metodo que podria ser asi: 

```javascript
// Donde actual seria show y arrayCompleto seria shows
v-for(actual, arrayCompleto) {
	foreach (actual in arrayCompleto){
		return actual;
	}
}
```



### Listado de directices 

**V-BIND y/o ":" : **Directrices de tipo atributo.Ej: v-bind:key o :key

**V-ON y/o "@": **Directices de tipo escuchador de eventos.Ej. v-on:click o @click

**v-for: **Recorre un array dentro de la etiqueta que estipulemos

```html
<ul>
	<li>Game of thrones</li>
	<li>The walking dead</li>
	<li>Breaking bad</li>
</ul>
// En este caso cada valor del array, representario un ul de la lista
```



**:key ** Le pasamos id para que haya un control al recorrer estos datos (Le da un orden y por tanto, es capaz de hacer esto, en menos tiempo)

**v-if: **Condicional, que decide si mostrar o no, la etiqueta en la que ponemos nuestra directriz

```vue
// Donde mostrar es una variable booleana
<h1 v-if="mostrar">Un titulo</h1>
```

Podemos utilizar de la misma manera el **v-else** siempre y cuando lo pongamos en la proxima etiqueta de la que pusimos **v-if**. Asi:

```vue
<h1 v-if="mostrar">Un titulo</h1>
<p v-else>No se encontro un titulo</p>
```



**v-show: **Esta directiva funciona igual que el v-if y se complementa con el **v-hide**

```vue
<h1 v-show="mostrar">Un titulo</h1>
<p v-hide="mostrar">No se encontro un titulo</p>
// A tener en cuenta, lo que estamos diciendo es lo siguiente: 
v-show = mostrar
v-hide = ocultar
	cuando mostrar sea true, me muestra un titulo y cuando mostrar sea true se oculta "No 	  se encontro un titulo" y cuando sea lo contrario, el dice: mostrar? (mostrar es igual 	a false), responde no. Ocultar (mostrar es igual a false), responde no. Por tanto no 	 se mostraria el titulo y se mostraria el "No se encontro un titulo"
```

​	**Nota: **La unica diferencia que podemos encontrar entre v-if/v-else y v-show/v-hide es:

​			El v-if no plasma el bloque html, mientras que el v-show, si lo hace pero agregandole 			un display none

### Componentes en vuejs

Los componentes son trozos de codigo reutilizables, para dividir el codigo y organizarlo mejor. De tal manera que nos podamos concentrar en cosas especificas, despreocupandonos de otras.

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aprendiendo VUEJS</title>
</head>
<body>
    <div id="app">
        <h1>{{ message }}</h1>
        <!-- Si mostrar == true, el ul se muestra, de lo contrario, no.  -->
        <button @click="changeVisibility">Mostrar/Ocultar</button>
        <ul v-if="mostrar">
            <!-- El v-for se pone aqui, para que se repita cada li(item) del ul(lista) -->
            <!-- <tvshow v-for="(show, key) in shows" :key="key" :name="show.name" :seasons="show.seasons"></tvshow> -->
            <tvshowlist></tvshowlist>
        </ul>
        <p v-else>No se encontraron datos</p>    
    </div>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.4.2/vue.js" integrity="sha512-njMD8/lt6qrl5S7BFajlL1KztlxeFyLYq/rkt395asAA8dz8uZaNU5VcAxL1DwZul9dmJk+or3HbjafV107ODA==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
    <script>
        Vue.component('tvshowlist', {
            data: function(){
                return {
                    shows: [
                        {name: 'Game of thrones', seasons: 7},
                        {name: 'Breaking bad', seasons: 5},
                        {name: 'The walking dead', seasons: 12},
                        {name: 'The 100', seasons: 7}
                    ]
                }
            },
            template: `
                <ul>
                    <tvshow v-for="(show, key) in shows" :key="key" :name="show.name" :seasons="show.seasons"></tvshow>
                </ul>
            `
        })

        Vue.component('tvshow', {
            //Los datos(data) en los componentes, son una funcion
            props: {
                name: String,
                seasons: Number,
            },
            //Codigo HTML
            template: `
                <li>
                    <strong>{{ name }}</strong> ({{ seasons }} Temporadas)
                </li>
            `
        })
        const app = new Vue({
            el: '#app',
            data: {
                message: 'Hola mundo de Vuejs',
                mostrar: false,
            },
            methods: {
                changeVisibility: function () {
                    this.mostrar = !this.mostrar
                }
            }
        })
    </script>
</body>
</html>
```

En este trozo de codigo estamos utilizando componentes, llamando el componente tvshows, dentro de tvshowlist. Pasandole datos, del componente padre, al hijo por medio de props. Asi:

```vue
Vue.component('tvshowlist', {
            data: function(){
                return {
                    shows: [
                        {name: 'Game of thrones', seasons: 7},
                        {name: 'Breaking bad', seasons: 5},
                        {name: 'The walking dead', seasons: 12},
                        {name: 'The 100', seasons: 7}
                    ]
                }
            },
            template: `
                <ul>
                    <tvshow v-for="(show, key) in shows" :key="key" 			  						:name="show.name" :seasons="show.seasons"></tvshow>
                </ul>
```

El componente padre tvshowlist, tiene un dato de tipo array llamado shows, este por medio de los props (variables que quiere y/o que necesita recibir para ejecutarse y que fueron definidas en el componente hijo, pues es el, el que sabe que tiene que recibir). Ejecuta un foreach y le pasa los show.name y show.seasons(donde show es la variable que va guardando cada recorrido del foreach)

A tener en cuenta: Los props los definimos aqui, asi:

​	***AQUI MOSTRAMOS COMO PASAR DATOS DE PADRE A HIJO(Props)***

```vue
Vue.component('tvshow', {
            //Los datos(data) en los componentes, son una funcion
            props: {
                name: String,
                seasons: Number,
            },
            //Codigo HTML
            template: `
                <li>
                    <strong>{{ name }}</strong> ({{ seasons }} Temporadas)
                </li>
            `
        })
```

​	***AQUI MOSTRAMOS COMO PASAR DATOS DE HIJO A PADRA(Emits)***

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Emits en vuejs</title>
</head>
<body>
    <div id="app">

    </div>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.4.2/vue.js" integrity="sha512-njMD8/lt6qrl5S7BFajlL1KztlxeFyLYq/rkt395asAA8dz8uZaNU5VcAxL1DwZul9dmJk+or3HbjafV107ODA==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
    <script>

        Vue.component('todolist', {
            props: {
                todos: Array
            },
            template: `
                <div>
                    <ul>
                        <todoitem v-for="(todo, key) in todos" :key="key" :todo="todo"></todoitem>
                    </ul>
                </div>
            `
        })

        Vue.component('todoitem', {
            props: {
                todo: Object
            },
            template: `
                <div>
                    <li>
                        <strong>{{ todo.title }}</strong>
                    </li>
                </div>
            `
        })

        Vue.component('todoadd', {
            data: function() {
                return {
                    title: null
                }
            },
            template: `
                <div>
                    <input type="text" placeholder="Ingrese el titulo de la tarea" v-model="title"></input>
                    <button @click="enviarApadre">Añadir tarea</button>    
                </div>
            `,
            methods: {
                enviarApadre: function(){
                    this.$emit('muestrame', {title: this.title})
                    this.title = null
                }
            }
        })

        const app = new Vue({
            el: '#app',
            data: {
                todos:[
                    { title: 'Tarea1', completed: false },
                    { title: 'Tarea2', completed: false },
                    { title: 'Tarea3', completed: false }
                ],
                title: null
            },
            //La instancia raiz de vue va a tener un template
            /* "muestrame" es un reemplazo de @click, dentro de la etiqueta de mi 			componente, y este componente lo llamamos donde lo necesitemos.Ej. 
          Cuando damos click en el boton "añadir tarea", ejecutamos en @click de 		   "todoadd", que fue reemplazado por "muestrame". "Muestrame", le dice 
          que metodo ejecutar en la instancia de vue, y a el viene amarrado el dato 		  que queremos pasar. Todo se hace a la vez, cuando damos click en el boton 		  de arriba, en realidad estamos ejecutando el metodo "verLoQueTrajo". Los 			 enventos son boleanos son un suitche que se activa cuando ejecutamos una 			accion dentro del dom */
            template: `
                <div>
                    <todolist :todos="todos"></todolist>
                    <todoadd @muestrame="verLoQueTrajo"></todoadd>
                </div>
            `,
            methods: {
                verLoQueTrajo: function(title){
                    this.todos.push(title)
                }
            }
        })
    </script>
</body>
</html>
```

"Muestrame" es un reemplazo de @click, dentro de la etiqueta de mi componente, y este componente lo llamamos donde lo necesitemos. Ej. Cuando damso click en el boton "añadir tarea", ejecutamos el @click de todoadd(componente hijo), que fue reemplazado por "muestrame". "Muestrame", le dice que metodo ejecutar en la instancia de vue(componente padre, que es donde esta la variable de tipo array, todos, para poder hacerle el push), y a el viene amarrado el dato que queremos pasar. Todo se hace a la vez, cuando damos click en el boton de arriba, en realidad estamos ejecutando el metodo "verLoQueTrajo". Los eventos son un sitche que se activa cuando ejecutamos una accion dentro del DOM 
