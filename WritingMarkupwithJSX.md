*Texto en cursiva*
_Texto en cursiva_
**Texto en negrita**
__Texto en negrita__
***Texto en cursiva y negrita***
___Texto en cursiva y negrita___

Título 1
=
Título 2
-





Writing Markup with JSX
=

JSX es una extensión de sintaxis para JavaScript que le permite escribir marcas similares a HTML dentro de un archivo JavaScript. Aunque hay otras formas de escribir componentes, la mayoría de los desarrolladores de React prefieren la concisión de JSX y la mayoría de las bases de código la usan.

JSX: poner marcado en JavaScript
=

La Web se ha construido sobre HTML, CSS y JavaScript. Durante muchos años, los desarrolladores web mantuvieron el contenido en HTML, el diseño en CSS y la lógica en JavaScript, ¡a menudo en archivos separados! El contenido se marcó dentro de HTML mientras que la lógica de la página vivía por separado en JavaScript:

                         
_HTML_

![Esta es una imagen de ejemplo](https://beta.reactjs.org/_next/image?url=%2Fimages%2Fdocs%2Fdiagrams%2Fwriting_jsx_html.png&w=384&q=75)

_JavaScript_

![Esta es una imagen de ejemplo](https://beta.reactjs.org/_next/image?url=%2Fimages%2Fdocs%2Fdiagrams%2Fwriting_jsx_js.png&w=384&q=75)


Pero a medida que la Web se volvió más interactiva, la lógica determinó cada vez más el contenido. ¡JavaScript estaba a cargo del HTML! Esta es la razón por la que en React, la lógica de representación y el marcado viven juntos en el mismo lugar: los componentes.

_Sidebar.js React component_

![Esta es una imagen de ejemplo](https://beta.reactjs.org/_next/image?url=%2Fimages%2Fdocs%2Fdiagrams%2Fwriting_jsx_sidebar.png&w=384&q=75)

_Form.js React component_

![Esta es una imagen de ejemplo](https://beta.reactjs.org/_next/image?url=%2Fimages%2Fdocs%2Fdiagrams%2Fwriting_jsx_form.png&w=384&q=75)

Mantener juntas la lógica de representación y el marcado de un botón garantiza que permanezcan sincronizados entre sí en cada edición. Por el contrario, los detalles que no están relacionados, como el marcado del botón y el marcado de una barra lateral, están aislados entre sí, lo que hace que sea más seguro cambiar cualquiera de ellos por su cuenta.

Cada componente de React es una función de JavaScript que puede contener algún marcado que React muestra en el navegador. Los componentes de React usan una extensión de sintaxis llamada JSX para representar ese marcado. JSX se parece mucho a HTML, pero es un poco más estricto y puede mostrar información dinámica. La mejor manera de entender esto es convertir algunas marcas HTML en marcas JSX.

Nota
=
__JSX y React son dos cosas separadas. A menudo se usan juntos, pero puede usarlos independientemente el uno del otro. JSX es una extensión de sintaxis, mientras que React es una biblioteca de JavaScript.__
=
Convirtiendo HTML a JSX
=


```html
<h1>Hedy Lamarr's Todos</h1>
<img 
  src="https://i.imgur.com/yXOvdOSs.jpg" 
  alt="Hedy Lamarr" 
  class="photo"
>
<ul>
    <li>Invent new traffic lights
    <li>Rehearse a movie scene
    <li>Improve the spectrum technology
</ul>
```
Queremos poner esto en un componente

```javascript
export default function TodoList() {
  return (
    // ???
  )
}
```
Si intentamos correr ese contenido en un componente de React vemos que 

App.js
```javascript
export default function TodoList() {
  return (
    // This doesn't quite work!
    <h1>Hedy Lamarr's Todos</h1>
    <img 
      src="https://i.imgur.com/yXOvdOSs.jpg" 
      alt="Hedy Lamarr" 
      class="photo"
    >
    <ul>
      <li>Invent new traffic lights
      <li>Rehearse a movie scene
      <li>Improve the spectrum technology
    </ul>
  );
}
```
Arroja éste error
```javascript
Error
/App.js: Adjacent JSX elements must be wrapped in an enclosing tag. Did you want a JSX fragment <>...</>? (5:4)

  3 |     // This doesn't quite work!
  4 |     <h1>Hedy Lamarr's Todos</h1>
> 5 |     <img 
    |     ^
  6 |       src="https://i.imgur.com/yXOvdOSs.jpg" 
  7 |       alt="Hedy Lamarr" 
  8 |       class="photo"
```

¡Esto se debe a que JSX es más estricto y tiene algunas reglas más que HTML! Si lee los mensajes de error anteriores, lo guiarán para corregir el marcado, o puede seguir la guía a continuación.

Nota
=
__La mayoría de las veces, los mensajes de error en pantalla de React lo ayudarán a encontrar dónde está el problema. ¡Dales una lectura si te quedas atascado!__
=

# Las reglas de JSX

1. Devolver un solo elemento raíz

_Para devolver varios elementos de un componente, envuélvalos con una sola etiqueta principal._
Por ejemplo podemos usar un "div"
```javascript
{
<div>
  <h1>Hedy Lamarr's Todos</h1>
  <img 
    src="https://i.imgur.com/yXOvdOSs.jpg" 
    alt="Hedy Lamarr" 
    class="photo"
  >
  <ul>
    ...
  </ul>
</div>
}
```
Si no querés agregar un div podés usar una etiqueta vacía llamada Fragment <></>

```javascript
<>
  <h1>Hedy Lamarr's Todos</h1>
  <img 
    src="https://i.imgur.com/yXOvdOSs.jpg" 
    alt="Hedy Lamarr" 
    class="photo"
  >
  <ul>
    ...
  </ul>
</>
```
Los fragmentos le permiten agrupar cosas sin dejar ningún rastro en el árbol HTML del navegador.

¿Por qué es necesario envolver varias etiquetas JSX?


JSX parece HTML, pero bajo el capó se transforma en objetos simples de JavaScript. No puede devolver dos objetos de una función sin envolverlos en una matriz. Esto explica por qué tampoco puede devolver dos etiquetas JSX sin envolverlas en otra etiqueta o Fragmento.
2. Cerrar todas las etiquetas

*JSX requiere que las etiquetas se cierren explícitamente*: las etiquetas de cierre automático como `<img>`deben convertirse en `<img />`, y las etiquetas envolventes como `<li>` "algo" deben escribirse como `<li>`"algo"`</li>`.
```javascript
<>
  <img 
    src="https://i.imgur.com/yXOvdOSs.jpg" 
    alt="Hedy Lamarr" 
    class="photo"
   />
  <ul>
    <li>Invent new traffic lights</li>
    <li>Rehearse a movie scene</li>
    <li>Improve the spectrum technology</li>
  </ul>
</>
```

3. camelCase en la mayoría de las cosas!

JSX se convierte en JavaScript y los atributos escritos en JSX se convierten en keys de objetos JavaScript. En sus propios componentes, a menudo querrá leer esos atributos en variables. Pero JavaScript tiene limitaciones en los nombres de variables. Por ejemplo, sus nombres no pueden contener guiones ni ser palabras reservadas como class.

Por eso, en React, muchos atributos HTML y SVG están escritos en camelCase. Por ejemplo, en lugar de `stroke-width`, usa `strokeWidth`. Dado que class es una palabra reservada, en React escribes className en su lugar, con el nombre de la propiedad DOM correspondiente:
```html
<img 
  src="https://i.imgur.com/yXOvdOSs.jpg" 
  alt="Hedy Lamarr" 
  className="photo"
/>
```
*Pro-Tip: Usar un convertidor de JSX

¡Convertir todos estos atributos en marcas existentes puede ser tedioso! Recomendamos usar un convertidor para traducir su HTML y SVG existente a JSX. Los convertidores son muy útiles en la práctica, pero aún así vale la pena entender lo que está pasando para que puedas escribir cómodamente JSX por tu cuenta.

Acá está el resultado final 

```javascript
export default function TodoList() {
  return (
    <>
      <h1>Hedy Lamarr's Todos</h1>
      <img 
        src="https://i.imgur.com/yXOvdOSs.jpg" 
        alt="Hedy Lamarr" 
        className="photo" 
      />
      <ul>
        <li>Invent new traffic lights</li>
        <li>Rehearse a movie scene</li>
        <li>Improve the spectrum technology</li>
      </ul>
    </>
  );
}
```
Ahora sabe por qué existe JSX y cómo usarlo en componentes:

 * Los componentes de React agrupan la lógica de representación junto con el marcado porque están relacionados.
 * JSX es similar a HTML, con algunas diferencias. Puedes usar un convertidor si lo necesitas.
 * Los mensajes de error a menudo lo guiarán en la dirección correcta para corregir su marcado.