Canal oficial de Angular en YouTube:
	https://www.youtube.com/playlist?list=PL1w1q3fL4pmj9k1FrJ3Pe91EPub2_h4jF
	Consiste de 8 videos.

Existe una versión interactiva que tiene más contenido y explicaciones adicionales: https://angular.dev/tutorials/first-app/01-hello-world




Directorio del curso:
	`/home/jrondon/Documents/Cursos/Angular_Tutorial`


Lo primero es instalar el ambiente, para lo que se usa [[NVM]] (Node Version Manager)

Luego se instala node:
	`nvm install v18.20.4`

Verificar la instalación:
	`node --version`
	`npm --version`

Para listar las versiones de node disponibles:
	`nvm list`

Para seleccionar una versión de node específica:
	`nvm use v18.20.4`\
\
Para instalar Angular de manera global:
	`npm install -g @angular/cli`

Verificar la instalación de Angular_CLI:
	`ng --version`

Listar paquetes instalados:
	`npm list`

Listar paquetes instalados globalmente:
	`npm list --global`



# Video 1. Introduction to Angular - Learning Angular (Part 1)
Introducción.
Se va a implementar una aplicación web para encontrar residencia (to find housing) usando angular.

# Video 2. Getting started with Angular - Learning Angular (Part 2)

Instalar angular CLI:
	`npm install -g @angular/cli`

Verificar la instalación:
```bash
jrondon@jrondon-ltp:angular-tutorial$ ng version

#     _                      _                 ____ _     ___
#    / \   _ __   __ _ _   _| | __ _ _ __     / ___| |   |_ _|
#   / △ \ | '_ \ / _` | | | | |/ _` | '__|   | |   | |    | |
#  / ___ \| | | | (_| | |_| | | (_| | |      | |___| |___ | |
# /_/   \_\_| |_|\__, |\__,_|_|\__,_|_|       \____|_____|___|
#                |___/   

Angular CLI: 18.2.6
Node: 18.20.4
Package Manager: npm 10.8.3
OS: linux x64

Angular: 
... 

Package                      Version
------------------------------------------------------
@angular-devkit/architect    0.1802.6 (cli-only)
@angular-devkit/core         18.2.6 (cli-only)
@angular-devkit/schematics   18.2.6 (cli-only)
@schematics/angular          18.2.6 (cli-only)
```

Descargar la aplicación desde goo.gle/homes-app-start que redirecciona a https://github.com/angular/codelabs/tree/homes-app-start. Es la aplicación base para hacer el tutorial.

Me descargué el código desde GitHub usando un zip y creé un repositorio de git allí.

Siguiendo las instrucciones del video:
	- Renombré el directorio que obtengo al descomprimir el zip a `homes-app`
	- `cd homes-app`
	- `npm install`

Para probar la aplicación:
	`ng serve`

Ir al navegador e ir a `http://localhost:4200/`
	`Hello World!`

Usaremos `vscode` con la extensión `Angular Language Service`.

Minuto `4:00` se habla de la estructura del código de la aplicación:
- El archivo `angular.json` permite configurar el proyecto. Permite indicar la configuración del build, internacionalización, entre otros.
- `package.json` contienen las dependencias del proyecto.
- `tsconfig.json` contiene las configuraciones de typescript.
- `/src/app/` contiene la aplicación. En este ejemplo, el archivo `app.component.ts` es el que contiene la lógica de la aplicación y más específicamente, contiene el template de lo que se muestra en pantalla al ejecutar la aplicación.


Se modifica `src/app/app.component.ts` para cambiar el mensaje de `Hello World!` a `Hello Universe!`



# Video 3. Components in Angular - Learning Angular (Part 3)
https://www.youtube.com/watch?v=R0nRX8jD2D0&list=PL1w1q3fL4pmj9k1FrJ3Pe91EPub2_h4jF&index=3

## Components in Angular
Los componentes en angular tienen tres partes:
- La clase del componente escrita en Typescript (Typescript Component Class): es el lugar donde se desarrolla la lógica de la aplicación. Es donde se realizan las llamadas a las API o donde se definen los manejadores de eventos (Event Handlers).
- Template HTML: el template es donde se define la interfaz de usuario para el componente. Si el template es muy complejo se puede incluir en su propio archivo HTML.
- CSS Styles: contiene los estilos del componente, con el alcance del componente. Se pueden escribir en SASS, LESS o CSS puro. Los estilos se pueden escribir en la clase del componente o se pueden incluir desde un archivo externo. En este curso se colocan los estilos en un archivo separado.


## Aplicando los componentes a la app
Aun cuando se puede hacer el header con un componente, se puede agregar template del componente de la aplicación y ese se muestra en todos lados.

#important Desde el minuto 1:13 hasta el 2:24 se habla acerca de la estructura de la aplicación a implementar.
- Paso 1: El Header en el que se tiene el logo y la palabra Homes, no se implementará como un componente pero se podría. Se deja en el template de la aplicación (y por lo que entiendo, aparece en todos lados de la aplicación).
- Paso 2: El cuadro de búsqueda y los resultados (todos) se colocarán en un componente llamado `home component`.
- Paso 3: Los resultados individuales se meten en un componente aparte. Este componente contiene la imagen, el nombre y la ubicación. Este componente se llamará `Housing location` y lo usaremos dentro del componente `home component`.
- Los componentes pueden ser anidados y/o utilizados unos dentro de otros.

Paso 1: para agregar el header se va a modificar el `template `HTML de la aplicación `app.component.ts`.
```typescript
import { Component } from '@angular/core';

@Component({
	standalone: true,
	selector: 'app-root',
	template: `
	<main>
		<header class="brand-name">
			<img src="/assets/logo.svg" class="brand-logo"
			alt="logo" aria-hidden="true">
		</header>
	</main>
	`,
	styleUrls: ['./app.component.css'],
})
export class AppComponent {
	title = 'homes';
}
```
#investigar `aria-hidden=true`

Paso 2: Se va a generar un componente que contendrá al campo de búsqueda y la lista de resultados. Para crear el componente se ejecuta el siguiente comando desde la raíz del proyecto:
```bash
ng generate component Home --standalone --inline-template
```
Explicación:
	`ng generate component` Se usa para generar un componente. Se pueden generar servicios, interfaces (y otros?).
	`Home` Es el nombre del componente.
	#investigar `--standalone` Es el tipo de componente creado 
	#investigar `--inline-template` Creo que es para que el template del componente sea inline y no en un archivo aparte.

Salida:
```bash
jrondon@jrondon-ltp:homes-app$ ng generate component Home --standalone --inline-template
CREATE src/app/home/home.component.css (0 bytes)
CREATE src/app/home/home.component.spec.ts (540 bytes)
CREATE src/app/home/home.component.ts (303 bytes)
```

Luego, debemos modificar `app.component.ts` para hacer referencia al nuevo componente en el template. Es decir, debajo del header vamos a agregar una nueva sección en la que vamos a agregar el nuevo componente (`home component`).
```html
<section>
	<app-home></app-home>
</section>
```
El prefijo app en `app-home` le indica a Angular que home es un componente y que lo inserte aquí. El prefijo se puede configurar. Al igual que en Vue, se debe hacer el import del componente para poder usarlo en el template. Esto se hace en dos partes, primero se hace el import del componente recientemente creado `HomeComponent` al inicio, donde están los otros imports (file level import). Luego en la metadata del componente (`@Component` <- component decorator metadata) se agrega una propiedad llamada `imports` (plural), cuyo valor es un arreglo de los componentes a incluir en `AppComponent` (`app.component.ts`). En este punto solo se incluye en el imports a `HomeComponent`.

Las líneas que se agregan en `app.component.ts` son:
```typescript
import { HomeComponent } from './home/home.component';

@Component({
//  standalone: true,
//  selector: 'app-root',
//  template: `...`
//  styleUrls: ['./app.component.css'],
  imports: [HomeComponent]
})
```
Los comentarios son para resaltar los cambios.

En este punto, se creó un componente nuevo (`HomeComponent`) y se incorporó a la aplicación principal. El componente nuevo no hace nada todavía.


El siguiente paso es actualizar el template del componente nuevo para que contenga el cuadro de búsqueda y los resultados de la búsqueda. Eso se hace en el archivo del componente nuevo `src/app/home/home.component.ts`. 
En el template de `HomeComponent` se agregan dos secciones (html). Una que contiene un formulario que a su vez contiene el campo de búsqueda (input tipo texto) y el botón buscar y la otra sección para contener los resultados. Por el momento, la segunda sección no contiene nada y sólo se le asigna la clase "results".

El template del archivo `home.component.ts` queda de la siguiente manera:
```html
<section>
  <form>
	<input type="text" placeholder="Filter by city">
	<button class="primary" type="button">Search</button>
  </form>
</section>

<section class="results">
</section>
```


Paso 3: ahora se va a crear un componente que contenga los resultados individuales que se van a mostrar en la sección de resultados en el componente `HomeComponent`. Este componente va a mostrar un resultado particular recibiendo como parámetro el id de la ubicación a mostrar. Luego en el `HomeComponent` se hace un for para mostrar todos los resultados. 

Para generar el nuevo componente:
```bash
ng generate component HousingLocation --standalone --inline-template
```

Ahora este nuevo componente `HousingComponent` hay que importarlo dentro del componente que lo va a usar (`HomeComponent`). Dos include: uno a nivel de archivo y otro a nivel del decorator en el arreglo de `imports`. Este nuevo componente se va a incluir dentro de la sección de resultados en el `HomeComponent`.

El archivo de `HomeComponent` queda de la siguiente manera:
```typescript
import { Component } from '@angular/core';
import { CommonModule } from '@angular/common';
import { HousingLocationComponent } from '../housing-location/housing-location.component';

@Component({
  selector: 'app-home',
  standalone: true,
  imports: [CommonModule, HousingLocationComponent],
  template: `
    <section>
      <form>
        <input type="text" placeholder="Filter by city">
        <button class="primary" type="button">Search</button>
      </form>
    </section>
    <section class="results">
      <app-housing-location></app-housing-location>
    </section>
  `,
  styleUrls: ['./home.component.css']
})
export class HomeComponent {

}
```

En este punto se tiene una aplicación hecha en angular que tiene un componente y un template. El template se modifica para que contenga el logo y se el componente se llama `HomeComponent` y contiene dos secciones: una para el botón de búsqueda y el campo de entrada de la búsqueda, y la otra sección contiene un componente en este momento que representa los resultados de las búsquedas.

En el siguiente video se va a modificar el componente `HousingLocation` para aceptar parámetros y mostrar diferentes resultados y se va a modificar el `HomeComponent` para listar todos los resultados encontrados.



# Video 4. Customizing components and directives (Part 4)
https://www.youtube.com/watch?v=eM3zi_n7lNs&list=PL1w1q3fL4pmj9k1FrJ3Pe91EPub2_h4jF&index=4

En este video se va an a llevar a cabo los siguientes pasos:
- Paso 1: Construir la estructura del componente `HousingLocation`.
- Paso 2: Hacer que el componente de `HousingLocation` sea personalizable (que acepte parámetros).
- Paso 3: Mostrar dinámicamente las ubicaciones de los resultados (usando los parámetros).
- Paso 4: Agregar los estilos de la aplicación.


Paso 1: dentro del componente `HousingLocation` se va a actualizar el template. Se crea una sección con tres elementos: una imagen para mostrar la imagen de la casa, un título `h2` y un párrafo `<p>`.
Estos tres campos los va a tomar de un json que contiene todas las Housing Locations. En un principio este json es un arreglo estático en una variable, después se mueve a un servicio y después se mueve a un servidor desde el que se obtiene una respuesta (en el video 8). El componente `HousingLocation` tomará un parámetro (id) para tomar un elemento de un arreglo y llenar los tres campos que tiene en la sección que se creó.
```html
<section class="listing">
  <img class="listing-photo">
  <h2 class="listing-heading"></h2>
  <p class="listing-location"></p>
</section>
```

En angular se utilizan Input Properties para  pasar data a los componentes.

Punto importante: la data que se espera recibir que describe los resultados tiene la forma que se muestra a continuación.
```json
{
	id: 0,
	name: "Acme Fresh Start Housing",
	city: "Chicago",
	state: "IL",
	photo: "/asset/image.jpg",
	availableUnits: 4,
	wifi: true,
	laundry:true,
},
```
El anterior es un elemento de un arreglo de objetos que contiene la información de las diferentes ubicaciones listadas en la aplicación.

En la página de inicio de la aplicación se mostrará el nombre, la ciudad y el estado.

Se va a crear un tipo de datos para albergar las respuestas con ese formato en específico. El tipo de datos se implementa a través de una interfaz para acceder a los datos. "Una interfaz es un contrato entre nosotros y la data" minuto 3:00. 

Para crear la interfaz:
```bash
ng generate interface housingLocation
```
El comando anterior indica a Angular CLI que genere una interfaz llamada `housingLocation`.

#duda por qué se usa camel case en `housingLocation`. En el video hacen énfasis en 'capital L'.

Salida:
```bash
jrondon@jrondon-ltp:homes-app$ ng generate interface housingLocation
CREATE src/app/housing-location.ts (37 bytes)
```

Ahora se actualiza la interfaz creada para que contenga el tipo de datos que se desea. En el archivo `src/app/housing-location.ts` recién creado, se agrega lo siguiente:
```typescript
export interface HousingLocation {
    id: number,
    name: string,
    city: string,
    state: string,
    photo: string,
    availableUnits: number,
    wifi: boolean,
    laundry: boolean,
}
```

A continuación se van a pasar `input properties` para pasar data al componente `HousingLocation` y se usará la interfaz para que el componente sepa que tipo de datos esperar.

Se puede marcar una propiedad con el "decorador" `@Input()` y eso le dice a angular que la propiedad puede ser seteada en el template.

En el archivo `housing-location.component.ts` debo importar la interfaz que creé y debo importar 'Input' de `@angular/core`.
```typescript
   import { Component, Input } from '@angular/core';
// import { CommonModule } from '@angular/common';
   import { HousingLocation } from '../housing-location';
```

Ahora, en la clase del componente `HousingLocationComponent` (la clase es la tercera parte de un componente, junto con el template y el CSS), se agrega:
```typescript
@Input() housingLocation!:HousingLocation;
```
Aquí se crea una nueva propiedad llamada `housingLocation` de tipo `HousingLocation`. El tipo (con dos mayúsculas H...L...) es el que se importó de la interfaz. A la propiedad `housingLocation` se le coloca el prefijo `@Input()` para declarar que es una propiedad de tipo input.

El signo de exclamación es para indicar que esa propiedad me la van a pasar desde otro lado. En caso de que no me la pasen debo inicializar la variable. El signo de exclamación en typescript se llama 'non null assertion operator' y le dice al compilador de typescript que el valor de la propiedad no será nulo o no definido.

Los decoradores se escriben con arroba, luego el nombre del decorador y terminan con paréntesis, que pueden tener cosas dentro o no.

En este punto, el componente `HousingLocationComponent` tiene una propiedad (de tipo input y de tipo `HousingLocation`) con la que podemos trabajar.

Ahora necesitamos acceder a esa data en el template del componente. En el caso de la imagen, se actualiza la fuente de la imagen (`src` property) con el valor contenido en `housingLocation.photo`. para que el template tome el valor de la variable y no solo un string literal "`housingLocation.photo`" se debe encerrar entre corchetes la propiedad `src`. Esto se llama `property binding`.

Para el texto alternativo de la imagen se usa lo siguiente: `alt="Exterior photo of {{housingLocation.name}}"`. En este caso, las doble llaves se usan para la interpolación. Con la interpolación también se inyectan valores en el template, específicamente para mezclar valores de variables con strings en los templates. 

El componente `HousingLocationComponent` admite un input para personalizar el componente.
Ahora se va a crear la lista de objetos para luego pasarla desde el `HomeComponent` hacia el `HousingLocationComponent`.

En el componente `HomeComponent` importo la interfaz que se creó (`HousingLocation`) y creo una nueva propiedad en la clase del componente `HomeComponent` llamada `housingLocationList` y que es un arreglo de objetos `HousingLocation`.
```typescript
...
import { HousingLocation } from '../housing-location';
...
export class HomeComponent {
  housingLocationList: HousingLocation[] = [];
}
```

Se va a inicializar esa lista (`housingLocationList`) a mano por ahora, con la data que dan en le curso en goo.gle/homes-app-listings, que redirecciona a https://gist.github.com/MarkTechson/efe8a9d4727ef33949b78812e66db082

>[!info]- Listing data
> ```json
> {
>      id: 0,
>      name: 'Acme Fresh Start Housing',
>      city: 'Chicago',
>      state: 'IL',
>      photo: '/assets/bernard-hermant-CLKGGwIBTaY-unsplash.jpg',
>      availableUnits: 4,
>      wifi: true,
>      laundry: true
>    },
>    {
>      id: 1,
>      name: 'A113 Transitional Housing',
>      city: 'Santa Monica',
>      state: 'CA',
>      photo: '/assets/brandon-griggs-wR11KBaB86U-unsplash.jpg',
>      availableUnits: 0,
>      wifi: false,
>      laundry: true
>    },
>    {
>      id: 2,
>      name: 'Warm Beds Housing Support',
>      city: 'Juneau',
>      state: 'AK',
>      photo: '/assets/i-do-nothing-but-love-lAyXdl1-Wmc-unsplash.jpg',
>      availableUnits: 1,
>      wifi: false,
>      laundry: false
>    },
>    {
>      id: 3,
>      name: 'Homesteady Housing',
>      city: 'Chicago',
>      state: 'IL',
>      photo: '/assets/ian-macdonald-W8z6aiwfi1E-unsplash.jpg',
>      availableUnits: 1,
>      wifi: true,
>      laundry: false
>    },
>    {
>      id: 4,
>      name: 'Happy Homes Group',
>      city: 'Gary',
>      state: 'IN',
>      photo: '/assets/krzysztof-hepner-978RAXoXnH4-unsplash.jpg',
>      availableUnits: 1,
>      wifi: true,
>      laundry: false
>    },
>    {
>      id: 5,
>      name: 'Hopeful Apartment Group',
>      city: 'Oakland',
>      state: 'CA',
>      photo: '/assets/r-architecture-JvQ0Q5IkeMM-unsplash.jpg',
>      availableUnits: 2,
>      wifi: true,
>      laundry: true
>    },
>    {
>      id: 6,
>      name: 'Seriously Safe Towns',
>      city: 'Oakland',
>      state: 'CA',
>      photo: '/assets/phil-hearing-IYfp2Ixe9nM-unsplash.jpg',
>      availableUnits: 5,
>      wifi: true,
>      laundry: true
>    },
>    {
>      id: 7,
>      name: 'Hopeful Housing Solutions',
>      city: 'Oakland',
>      state: 'CA',
>      photo: '/assets/r-architecture-GGupkreKwxA-unsplash.jpg',
>      availableUnits: 2,
>      wifi: true,
>      laundry: true
>    },
>    {
>      id: 8,
>      name: 'Seriously Safe Towns',
>      city: 'Oakland',
>      state: 'CA',
>      photo: '/assets/saru-robert-9rP3mxf8qWI-unsplash.jpg',
>      availableUnits: 10,
>      wifi: false,
>      laundry: false
>    },
>    {
>      id: 9,
>      name: 'Capital Safe Towns',
>      city: 'Portland',
>      state: 'OR',
>      photo: '/assets/webaliser-_TPTXZd9mOo-unsplash.jpg',
>      availableUnits: 6,
>      wifi: true,
>      laundry: true
>    }
> ```
>

La data anterior (Listing data) se debe pegar en la declaración de la propiedad `housingLocationListing`, es decir, en lugar de inicializarlo con un arreglo vacío, se inicializa con el conjunto de objetos de Listing data.

A continuación, en la sección de resultados del `HomeComponent`, se desea mostrar la lista completa de resultados (Listing data). Para lograr esto, se recorrerá el arreglo `housingLocationList` utilizando un bucle, que en Angular se implementa con `ngFor`. A medida que se itera sobre el arreglo, se irán creando componentes `HousingLocationComponent`, pasando cada elemento del arreglo como parámetro para personalizar el contenido de cada componente.

En la sección de resultados del `HomeComponent` se modifica el llamado al sub-componente `HousingLocation` con el `ngFor` de la siguiente manera:
```typescript
<section class="results">
  <app-housing-location *ngFor="let housingLocation of housingLocationList" [housingLocation]="housingLocation">
  </app-housing-location>
</section>
```
Explicación:
	`let i of housingLocationList`
		`housingLocationList` es un iterable y la variable `i` contendrá un elemento de la lista iterable en cada ciclo del loop.
	`[housingLocation]="i"` tomo el valor que tiene la variable `i` en cada loop y se la voy pasando como parámetro al componente `HousingLocation` para que lo tome y se construya cada vez con un elemento nuevo del iterable.


En este punto, falta el CSS para que se vea bien. Para actualizar los estilos ir a goo.gle/homes-app-styles que redirige a https://gist.github.com/MarkTechson/fa601fdc856d26b3bfa5030dae147f00.
En esos enlaces están los CSS y se indica en qué archivo deben ir.


# Video 5. How to route in Angular - Learning Angular (Part 5)
https://www.youtube.com/watch?v=r5DEBMuStPw&list=PL1w1q3fL4pmj9k1FrJ3Pe91EPub2_h4jF&index=5

Routing: Se va a crear un componente para albergar los detalles de un housing location y se va a agregar una ruta (enlace) para llegar desde el Home Component hasta la página de detalles.

Para habilitar las rutas, es necesario configurar la aplicación para aceptar routing. Esto se puede hacer desde la creación del proyecto o se puede incorporar más adelante (ahora). Tal como en Vue usando `vite` o `vue-cli`.

## Habilitar Routing
Para habilitar routing se debe ir al archivo `src/main.ts` e importar el router, y se deben modificar los parámetros de la función `bootstrapApplication` agregando como segundo parámetro un literal de javascript (objeto { } ) con una propiedad llamada `providers` que contiene un arreglo. Este arreglo contiene una llamada a la función `provideRouter([])` y se le pasa un arreglo vacío como parámetro de momento. Ese arreglo vacío contendrá las rutas.

Las rutas estarán contenidas en el archivo `src/app/routes.ts`. 
En este archivo:
- Importo `Routes` de `@angular/router` (`Routes` es un tipo de datos). Se importan desde el archivo de rutas sin usar '{}'.
- Creo un objeto llamado `routeConfig` de tipo `Routes` para almacenar allí las rutas. Lo inicializo como un arreglo vacío.
- Exporto el objeto para que pueda ser importado desde otros archivos (`main.ts`).

Para agregar las rutas a un componente:
- Importo el componente al que va dirigida la ruta.
- Creo la entrada en el objeto de rutas (`routeConfig`).


Para usar la ruta voy al componente en el que necesitaré la ruta y hago lo siguiente:
- Importo `RouterModule` desde `@angular/router`.
- Agrego `RouterModule` a la propiedad `imports` del decorador `@Component` del componente.
- Agrego la directiva `<router-outlet></router-outlet>` en el template del módulo para indicar el lugar en el que se insertará el componente de destino de la ruta.

El archivo `main.ts` queda de la siguiente manera:
```typescript
import { bootstrapApplication } from '@angular/platform-browser';
import { AppComponent } from './app/app.component';
import { provideRouter } from '@angular/router';
import routeConfig from './app/routes';

bootstrapApplication(AppComponent, {
  providers: [
    provideRouter(routeConfig)
  ]
}).catch(err => console.error(err));
```

El archivo de las rutas `routes.ts` queda de la siguiente manera al agregar la ruta por defecto (ruta vacía '')
```typescript
import { Routes } from '@angular/router';
import { HomeComponent } from './home/home.component';

const routeConfig: Routes = [
    {
        path: '',
        component: HomeComponent,
        title: 'Homes App'
    }
];

export default routeConfig;
```


Y el componente `app.component.ts` queda de la siguiente manera al usar la ruta por defecto para mostrar el contenido de la página de inicio:
```typescript
// import { Component } from '@angular/core';
// import { HomeComponent } from './home/home.component';
   import { RouterModule } from '@angular/router';

@Component({
//   standalone: true,
//   selector: 'app-root',
  template: `
    <main>
      <header class="brand-name">
        <img src="/assets/logo.svg" class="brand-logo"
        alt="logo" aria-hidden="true">
      </header>
      <section>
        <router-outlet></router-outlet>
      </section>
    </main>
  `,
//   styleUrls: ['./app.component.css'],
  imports: [HomeComponent, RouterModule]
})
...
```
Los comentarios son para resaltar los cambios.

En este punto se tiene la aplicación usando la ruta por defecto (string vacío) que redirige al componente `HomeComponent` y que le cambia el título a `Homes App`.

## Details Component

A continuación se va a crear la página de detalles de cada propiedad (housing location). Para ello se va a crear un componente nuevo que se llama templates con el siguiente comando:
```bash
ng g c details --standalone --inline-template
```

Que es equivalente a:
```bash
ng generate component details --standalone --inline-template
```

Salida:
```bash
jrondon@jrondon-ltp:homes-app$ ng generate component details --standalone --inline-template
CREATE src/app/details/details.component.css (0 bytes)
CREATE src/app/details/details.component.spec.ts (561 bytes)
CREATE src/app/details/details.component.ts (315 bytes)
```

Ahora se agregará una ruta para navegar hacia el componente. Para ello se necesita:
1. Se va a crear una nueva ruta en el archivo de rutas.
2. Se va a agregar un link hacia el componente details desde el componente `HousingLocationComponent`

Paso 1: agregar una ruta nueva hacia el componente details.

Recordar:
Para agregar las rutas a un componente:
- Importo el componente al que va dirigida la ruta.
- Creo la entrada en el objeto de rutas (`routeConfig`).

Las líneas importantes a agregar en `routes.ts` son:
```typescript
import { DetailsComponent } from './details/details.component';

const routeConfig: Routes = [
    {..},
    {
        path: 'details',
        component: DetailsComponent,
        title: 'Details Page'
    }
];
```

Ahora se debe agregar el enlace en el componente `HousingLocationComponent`. Se va a agregar un anchor element al final de la sección en la que se muestra la imagen, el nombre, la ciudad y el estado. El texto del anchor se coloca a 'Learn more'. En lugar de usar un `href` se utilizará una directiva de angular `routerLink` que es un enlace a un componente pero manejado por angular.

Recordar:
Para usar la ruta voy al componente en el que necesitaré la ruta y hago lo siguiente:
- Importo `RouterModule` desde `@angular/router`.
- Agrego `RouterModule` a la propiedad `imports` del decorador `@Component` del componente.
- Agrego la directiva `<router-outlet></router-outlet>` en el template del módulo para indicar el lugar en el que se insertará el componente de destino de la ruta.

En este caso se va a usar la directiva `routerLink` en lugar de la directiva `router-outlet`.

El cambio en el archivo `housing-location.component.ts` serían los siguientes:
```typescript
import { RouterModule } from '@angular/router';

@Component({

  imports: [CommonModule, RouterModule],
  template: `
    <section class="listing">
	...
	  <a routerLink="details">Learn More</a>
    </section>
  `,
...
})
```

En este punto se agregó un enlace al componente `HousingLocationComponent` que lleva al nuevo componente `details`. Sin embargo, el componente details está vacío.

Ahora, es necesario saber desde cuál componente el usuario le dio click al enlace `Learn More` para poder adaptar la página del componente `Details` con el contenido adecuado. En angular se puede resolver esto de varias formas: pasando directamente a la ruta la data y la información del estado usando features del router, o se puede pasar data que identifique el housing location usando el URL. En este tutorial se usa el camino del URL.

Para implementar esta solución se deben hacer tres cosas:
1. Modificar el anchor en `HousingLocationComponent` para pasar como parámetro en el URL el id de la ubicación sobre la que estamos haciendo click (`housingLocation.id`).
2. Modificar la ruta para aceptar el formato `/details/<number>`.
3. Modificar el componente `DetailsComponent` para tomar los parámetros que se le pasaron por el URL

Paso 1: el nuevo anchor queda de la siguiente manera:
```html
<a [routerLink]="['/details', housingLocation.id]">Learn More</a>
```
Esto hace que el enlace que se busca cuando se hace click sobre "Learn More" sea de la forma http://localhost:4200/details/numero siendo el número el correspondiente a `housingLocation.id`.

Paso 2: se debe modificar la ruta para pasar el número como un parámetro. Para ello se debe cambiar el archivo de rutas de la siguiente manera:
```json
{
	path: 'details/:id',
	component: DetailsComponent,
	title: 'Details Page'
}
```

Paso 3: se va a modificar el componente `DetailsComponent` para acceder al valor que se está pasando en el URL y usarlo para obtener el housing location adecuado.
Se debe importar `inject` desde `@angular/core` y se debe importar `ActivatedRoute` desde `@angular/router` y luego se actualiza la clase del componente Details.

El componente `DetailsComponent` queda de la siguiente manera:
```typescript
import { Component, inject } from '@angular/core';
import { ActivatedRoute } from '@angular/router';

@Component({

  template: `
    <p>
      details works! {{ housingLocationId }}
    </p>
  `,
})
export class DetailsComponent {
  route: ActivatedRoute = inject(ActivatedRoute);
  housingLocationId = 0;

  constructor() {
    this.housingLocationId = Number(this.route.snapshot.params['id']);
  }

}
```
Se omiten varias partes para resaltar los cambios.

`ActivatedRoute` (en `inject(ActivatedRoute)`) es una referencia a la ruta actual (con la que se llegó al componente actual) de la que se puede extraer la información contenida en el URL. Esa referencia se guarda en la variable `route` que es de tipo `ActivatedRoute`.

En el constructor, la parte del `id` debe corresponder con el nombre que se le da al parámetro en la declaración de la ruta (`details/:id`).

En este punto, al darle click al enlace `Learn More` de alguno de los componentes `HousingLocationComponent` el componente en cuestión arma el URL con el string `'/details/'` y con el id de `housingLocation.id` y queda por ejemplo así -> http://localhost4200/details/4. Se modificó la ruta para aceptar ese parámetro numérico y se modificó el componente `DetailsComponent` para leer el parámetro del URL y usarlo para mostrar el id por medio de interpolación.

En el siguiente video se va a completar el componente `Details`.



# Video 6. Services in Angular - Learning Angular (Part 6)
https://www.youtube.com/watch?v=-jRxG84AzCI&list=PL1w1q3fL4pmj9k1FrJ3Pe91EPub2_h4jF&index=6

| Time          | Description                                                           |
| ------------- | --------------------------------------------------------------------- |
| 0:00 - 1:00   | El problema y cómo se va a resolver (servicios)                       |
| 1:00 - 4:15   | Crea el servicio. Se migra la data al servicio. Se crean los métodos. |
| 4:15 - 5:40   | Actualiza `HomeComponent` para usar el servicio.                      |
| 5:55 - 6:58   | Dependency injection. Explicación.                                    |
| 7:00 - 9:16   | Actualiza Details page para usar el servicio.                         |
| 9:20 - 12:44  | Crea el template de `DetailsComponent`.                               |
| 12:44 - 13:00 | Aplicar estilos.                                                      |
| 13:15         | Recap                                                                 |
| 13:30         | Outro                                                                 |
## El Problema
El problema que se presenta en este punto es la accesibilidad de la data desde los diferentes componentes. Para solucionarlo se utiliza el concepto de Servicios y dependency injection. En este proyecto, el servicio es usado para garantizar la disponibilidad de los datos para los componentes de la aplicación. El servicio se encarga de interactuar con la fuente de datos para leer y/o persistir los datos.

## Servicio
Para crear el servicio se ejecuta lo siguiente:
```bash
ng generate service housing
```

Salida:
```bash
jrondon@jrondon-ltp:homes-app$ ng generate service housing
CREATE src/app/housing.service.spec.ts (362 bytes)
CREATE src/app/housing.service.ts (136 bytes)
```

Un servicio es una clase de typescript en Angular. El decorador `@Injectable` indica esta clase se puede usar en el sistema de inyección de dependencias, lo que significa que otras partes de la aplicación pueden solicitar una instancia del servicio. La propiedad `providedIn` indica en qué partes de la aplicación se puede inyectar el servicio (root implica que se puede usar en toda la aplicación).

A continuación se va a migrar la housing list al servicio. La lista de locations está actualmente en una constante llamada `housingLocationList` en la clase del `HomeComponent`. También se van a crear los métodos para acceder a todas las locations y el método para acceder a una location por id.

Paso 1: migrar la data.
En el servicio se debe importar la interfaz `HousingLocation` para tener acceso al tipo de datos `HousingLocation`. Con esto creamos una propiedad (protected) de la clase `HousingService` que se llame `housingLocationList` que es un arreglo de `HousingLocation`. Por ahora se le asigna un arreglo vacío a `housingLocationList`. Este es el arreglo que vamos a llenar con la data que antes estaba en el `HomeComponent`.

Paso 2: crear los métodos.
```typescript
getAllHousingLocations() : HousingLocation[] {
	return this.housingLocationList;
}

getHousingLocationById(id: Number) : HousingLocation | undefined {
	return this.housingLocationList.find(housingLocation => housingLocation.id === id);
}
```
El método `getHousingLocationById` puede devolver un objeto de tipo `HousingLocation` o devuelve el valor `undefined`.

El archivo final es `housing.service.ts`.


## Home Component
A continuación se actualiza el home component para utilizar el servicio.

En el archivo `home.component.ts` se debe importar `inject` de `@angular/core` y también el servicio `HousingService`.
Para inyectar el servicio se debe crear una propiedad dentro de la clase del componente donde se inicializa con la llamada al método `inject`.
```typescript
export class HomeComponent {
	housingLocationList: HousingLocation[] = [];
	housingService: HousingService = inject(HousingService);
}
```

El arreglo `housingLocationList` quedó vacío al mover la data al servicio. Para poblarlo debemos invocar la función `getAllHousingLocations()` del servicio y asignar el resultado a `housingLocationList`. Esto se hace en el constructor de la clase.
```typescript
constructor() {
	this.housingLocationList = this.housingService.getAllHousingLocations();
}
```


## Details Component
Se va a modificar `details.component.ts` para que utilice el servicio. Para esto se debe:
- Paso 1: Importar `inject` de `@angular/core`. Ya está porque se uso `ActivatedRoute`.
- Paso 2: Importar la interfaz `HousingLocation`.
- Paso 3: Inyectar el servicio.
- Paso 4: Consultar el valor del housing location a mostrar en la página de `Details`.
- Paso 5: Hacer disponible el valor del housing location a mostrar.
- Paso 6: Hacer el template que use el housing location.


Antes se usaba la variable (class property para ser exactos) `housingLocationId` para tomar el valor del parámetro `id` que se estaba pasando por medio de la ruta que lleva al componente de `Details` y con ese valor mostrar algo en la página que nos dijera que estaba funcionando. Eso era para pruebas y ahora se necesita usar ese valor (`id`) para buscar el housing location adecuado para dibujarlo en la página.

El housing location lo voy a guardar en una propiedad de la clase del componente que la llamo `housingLocation` y que puede ser del tipo `HousingLocation` o `undefined`. Esto último debido a que al buscar el housing location por `id` puede que no encuentre nada y por eso el `undefined`.

En el constructor cambio la variable `housingLocationId`, que antes era una propiedad de la clase, por una variable local dentro del constructor. Esa variable solo la uso para buscar el housing location usando el servicio (más específicamente el método del servicio `getHousingLocationById`).

Las propiedades de la clase, las puedo acceder desde el template.

Para acceder a las propiedades del objeto `housingLocation`, como por ejemplo el `id`, es necesario usar el operador `?` de la siguiente manera:
	`housingLocation?.id`

El operador `?` ayuda a prevenir el llamado de la propiedad `id` cuando el valor devuelto por `getHousingLocationById` es `undefined` porque no encontró nada.

#investigar  `?` es el operador optional chaining de typescript.

Paso 6: En este punto estamos listos para comenzar el paso 6, que es hacer el template de lo que se quiere mostrar, usando el contenido que está disponible en el objeto `housingLocation`.

El template queda como se muestra a continuación:
```html
<article>
  <img class="listing-photo" [src]="housingLocation?.photo">
  <section class="listing-description">
	<h2 class="listing-heading">{{housingLocation?.name}}</h2>
	<p class="listing-location">{{housingLocation?.city}}, {{housingLocation?.state}}</p>
  </section>
  <section class="listing-features">
	<h2 class="section-heading">About this housing location</h2>
	<ul>
	  <li>Units available: {{housingLocation?.availableUnits}}</li>
	  <li>Does this location have wifi: {{housingLocation?.wifi}}</li>
	  <li>Does this location have laundry: {{housingLocation?.laundry}}</li>
	</ul>
  </section>
  <section class="listing-apply">
	<h2 class="section-heading">Apply now</h2>
	<button class="primary" type="button">Apply now</button>
  </section>
</article>
```
La última sección se va a utilizar en el video siguiente.

Los estilos a aplicar se descargan desde goo.gle/homes-app-styles que redirige a https://gist.github.com/MarkTechson/fa601fdc856d26b3bfa5030dae147f00


## Dependency Injection - Explicación
Volver al minuto 5:55






# Video 7. Forms in Angular - Learning Angular (Part 7)
https://www.youtube.com/watch?v=kWbk-dOJaNQ&list=PL1w1q3fL4pmj9k1FrJ3Pe91EPub2_h4jF&index=7


| Time        | Description                                                              |
| ----------- | ------------------------------------------------------------------------ |
| 0:00 - 0:40 | Recap del Botón `Apply now` e Intro de lo que se hará.                   |
| 0:40 - 1:19 | Definiciones: Angular Forms. Modelo de datos. Input validation.          |
| 1:19 - 3:35 | Prepara el componente para usar forms. Construcción del modelo de datos. |
| 3:35 - 5:40 | Actualiza el template.                                                   |
| 5:40 - 7:40 | Acción del botón `Apply Now`. Event binding.                             |
| 7:40 - 8:36 | Función Submit del servicio.                                             |
| 8:36 - Ende | Recap                                                                    |

## Intro
En la sección anterior se dejó un botón para postularse a la residencia que se mostraba en details, pero el botón no hace nada. En esta sesión se va a crear un pequeño formulario para cumplir con la función de `Apply now`.
## Angular forms
Los formularios se usan para introducir data en una aplicación web. 
En angular se pueden crear modelos de datos que representan los controles del formulario y de esa forma tener acceso a esos valores fácilmente. En los formularios se puede hacer validación de los valores que se ingresan.

Comenzaremos por el modelo (form model) que representa la data que se quiere recolectar. En este caso, se desea recolectar el nombre, apellido y el email. 

En el componente `DetailsComponent` que es donde se va a colocar el formulario se deben realizar varios cambios.
- Preparar el componente para que se puedan usar formularios.
- Construir el modelo de datos.

Para preparar el componente se deben importar algunas clases: `FormControl`, `FormGroup` y `ReactiveFormModule` desde `@angular/forms`. El módulo `ReactiveFormModule` provee algunas características que pueden ser usadas en el template y para usarlas es necesario importarla en el decorador del componente `@Component({ imports: [..., ReactiveFormsModule] })`.

A continuación se define el modelo de datos del formulario. Para esto se usa la directiva `FormGroup` y `FormControl`. Un `FormGroup` es una colección de `FormControl`, una agrupación lógica. El modelo se crea dentro de la clase del componente.
```typescript
applyForm = new FormGroup({
	firstName: new FormControl(''),
	lastName: new FormControl(''),
	email: new FormControl(''),
});
```
Al crear un `FormControl` se le puede pasar un valor por defecto entre los paréntesis. En este caso el valor por defecto es un string vacío. 

Lo siguiente es utilizar el modelo de datos (`applyForm`) en el template por medio de binding para tener acceso a los valores que ingresa el usuario en los campos del formulario.

El template queda de la siguiente manera:
```html
<article>
  <img class="listing-photo" [src]="housingLocation?.photo">
  <section class="listing-description">
	<h2 class="listing-heading">{{housingLocation?.name}}</h2>
	<p class="listing-location">{{housingLocation?.city}}, {{housingLocation?.state}}</p>
  </section>
  <section class="listing-features">
	<h2 class="section-heading">About this housing location</h2>
	<ul>
	  <li>Units available: {{housingLocation?.availableUnits}}</li>
	  <li>Does this location have wifi: {{housingLocation?.wifi}}</li>
	  <li>Does this location have laundry: {{housingLocation?.laundry}}</li>
	</ul>
  </section>
  <section class="listing-apply">
	<h2 class="section-heading">Apply now</h2>
	<form [formGroup]="applyForm">
	  <label for="first-name">First Name</label>
	  <input id="first-name" type="text" formControlName="firstName">
	  
	  <label for="last-name">Last Name</label>
	  <input id="last-name" type="text" formControlName="lastName">

	  <label for="email">email</label>
	  <input id="email" type="text" formControlName="email">
	  <button type="submit" class="primary">Apply now</button>
	</form>
  </section>
</article>
```

En este punto se tiene un template hecho con un formulario que está atado (bound) con el modelo de datos creado para el formulario.



## Botón Apply now
Se va a agregar una función que maneje el evento submit dentro del formulario.  En la declaración del formulario en el template se le agrega `(submit)="submitApplication()"`.
```html
<form [formGroup]="applyForm" (submit)="submitApplication()">
```
Lo que se coloca entre paréntesis "(submit)" es para hacer un binding de eventos (event binding). En el caso anterior, significa que al ocurrir el evento submit, invocar la ejecución de la función `submitApplication()`. Esta función se crea en la clase del componente details.

En este caso, esta función hace un llamado a una función del servicio `housingService` y es esa función del servicio la que maneja la respuesta al evento.
```typescript
submitApplication() {
	this.housingService.submitApplication(
		this.applyForm.value.firstName ?? '',
		this.applyForm.value.lastName ?? '',
		this.applyForm.value.email ?? ''
	);
}
```
El operador `??` lo que hace es que en caso de que el valor de la izquierda sea `null` o `undefined`, se utiliza el valor del lado derecho. En este caso un string vacío ('').
#investigar knowledge coalescent operator (`??`)

Solo falta crear la función `submitApplication` en el servicio `housingService`.
```typescript
submitApplication(firstName: string, lastName: string, email: string) {
	console.log(firstName, lastName, email);
}
```
En este punto, solo se imprime un mensaje en la consola, pero se puede extender el código desde acá.



# Video 8. HTTP in Angular - Learning Angular (Part 8)
https://www.youtube.com/watch?v=5K10oYJ5Y-E&list=PL1w1q3fL4pmj9k1FrJ3Pe91EPub2_h4jF&index=8


| Time         | Description                                                            |
| ------------ | ---------------------------------------------------------------------- |
| 0:00 - 0:46  | Qué se va a hacer. Modificar el servicio para buscar la data por HTTP. |
| 0:46 - 2:19  | Servidor de JSON                                                       |
| 2:19 -       | Modificar el servicio `HousingService`                                 |
| 2:19 - 4:50  | Actualiza el método `getAllHousingLocations`                           |
| 4:50 - 5:49  | Actualiza el método `getHousingLocationById`                           |
| 5:49 - 7:43  | Actualiza los llamados a los métodos.                                  |
| 7:43 - 11:21 | Filtro con la barra de búsqueda. Template variables.                   |
| 11:35 -      | Recap                                                                  |

## Qué se hará
Se va a modificar el servicio `HousingService` para que tome la data de las housing locations desde un servidor externo. Este servidor la devuelve en el mismo formato que el que estamos usando en este momento.

Para servir el json se va a utilizar un paquete llamado `json-server`.

Para instalar el servidor json globalmente:
```bash
npm install -g json-server
```
Para instalarlo localmente para este proyecto:
```bash
npm install json-server
```

Se debe crear el json que va a servir y para ello usamos la data que está cableada en el servicio. Hay una pequeña modificación de la data allí.
El archivo a servir es `db.json` en el directorio `homes-app`.
```json
{
	"locations": [ <pegar la data de housingLocationList aquí> ]
}
```

Tuve que modificar el json porque le faltaban las comillas dobles del lado izquierdo y las comillas simples también tuve que cambiarlas por comillas dobles.

Se va a modificar el servicio para solicitar la data al json server. #investigar Para esto se utiliza la API fetch del navegador. En este caso, se modifican los métodos del servicio.

Se modifica el método `getAllHousingLocation()` de manera que utilice la API fetch del navegador. El método queda de la siguiente manera:
```typescript
async getAllHousingLocations() : Promise<HousingLocation[]> {
    const data = await fetch(this.locationsUrl);
    return await data.json() ?? [];
}
```

Para casos más complejos para la conexión a APIs externas, Angular provee el cliente HTTP (HTTP client service class). Más información: https://v17.angular.io/guide/understanding-communicating-with-http

Se hace lo mismo con la función `getHousingLocationById`:
```typescript
async getHousingLocationById(id: Number) : Promise<HousingLocation | undefined> {
    const data = await fetch(`${this.locationsUrl}/${id}`);
    return await data.json() ?? {};
}
```
En este caso se devuelve un objeto literal `{}` debido a que el tipo del valor de retorno es `HousingLocation` y no un arreglo de `HousingLocation`.

Ahora se debe actualizar los llamados a los métodos del servicio en toda la aplicación.

Primero en `home.component.ts` se modifica el llamado a `getAllHousingLocation` que se hace en el constructor:
```typescript
constructor() {
  this.housingService.getAllHousingLocations().then((housingLocationList: HousingLocation[]) => {
    this.housingLocationList = housingLocationList;
  });
}
```

Cosas por #investigar arrow functions, then function, await - fetch, promise, promised based functions.

En `details.component.ts` también se debe modificar el llamado a la función `getHousingLocationById` que se hace en el constructor:
```typescript
constructor() {
  const housingLocationId = Number(this.route.snapshot.params['id']);
  this.housingService.getHousingLocationById(housingLocationId).then(housingLocation => {
    this.housingLocation = housingLocation;
  });
}
```

En este punto se tiene la aplicación obteniendo la data de los housing locations por medio de una consulta HTTP a un servidor externo (json-server).




## Filtro usando el campo Search
Esto se puede hacer utilizando forms pero aquí hará con una variable del template (template variable).

Se necesita obtener la información del filtro que reside en el template y esto se hará con una variable del template.

La variable del template se agrega anteponiendo `#` al nombre de la variable. En este caso la variable se llama `filter`. La variable se agrega al campo input que es el campo de búsqueda del `HomeComponent`.
```html
<input type="text" placeholder="Filter by city" #filter>
```

En el botón de búsqueda es necesario agregar un manejador para el evento `click`.
```html
<button class="primary" type="button" (click)="filterResults(filter.value)">Search</button>
```
Aquí se indica que el evento `click` sobre el botón de búsqueda se está manejando con la función `filterResults` que toma como parámetro el valor de la variable de template `filter`. Para acceder al valor de la variable es necesario usar `filter.value` porque la variable de template es una variable HTML y `value` es una de las propiedades del elemento input.

Es necesario modificar la forma en la que se dibujan los componentes `HousingLocationComponent` para que tome en cuenta el filtro.
```html
<app-housing-location *ngFor="let housingLocation of filteredLocationList" [housingLocation]="housingLocation">
```

En el constructor se debe inicializar la lista filtrada:
```typescript
constructor() {
  this.housingService.getAllHousingLocations().then((housingLocationList: HousingLocation[]) => {
    this.housingLocationList = housingLocationList;
    this.filteredLocationList = housingLocationList;
  });
}
```

Por último, la función que maneja el evento `click` en el botón buscar quedaría de la siguiente manera:
```typescript
filterResults(text: string) {
  if (!text) this.filteredLocationList = this.housingLocationList;

  this.filteredLocationList = this.housingLocationList.filter(
    housingLocation => housingLocation?.city.toLowerCase().includes(text.toLowerCase())
  );
}
```

En este punto, se tiene la aplicación filtrando los resultados tomando en cuenta el valor del string que se introduce en el campo de búsqueda.

Para buscar cuando se le da enter al escribir, revisar: https://www.digitalocean.com/community/tutorials/angular-binding-keyup-keydown-events






































