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

​			El v-if no plasma el bloque html, mientras que el v-show, si lo hace pero agregandole un 			display none
