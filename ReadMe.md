# CR

A simple Component Replacer script

The components are just html files, the name of the component is the name of the file that contains said component.

An example of a component is:

``` html
<nav class="navbar">
	<div id="nav-home">
		<a href="/index.html">Home</a>
	</div>
	<div class="dropdown">
		My projects
		<div id="gh-projects" class="dropdown-options"></div>
	</div>
</nav>

```
And can be used like this:

``` html
<html>
	<head>
		...
	</head>
	<body>
		<navbar prop=value/>
	</body>
</html>

```

Resulting in:


``` html
<html>
	<head>
		...
	</head>
	<body>
		
<nav class="navbar">
	<div id="nav-home">
		<a href="/index.html">Home</a>
	</div>
	<div class="dropdown">
		My projects
		<div id="gh-projects" class="dropdown-options">
			~prop~
		</div>
	</div>
</nav>
	</body>
</html>

```
> Be wary that the tool does not have any regards for indentation (as shown).

---

## Usage

### Args

The first argument is the base file, the file that refers to / uses components.

The second argument is the output file, the file that will be written with the component added.

Every other argument after will be considered as a component file that will be used to replace the specific tag.

### Passing arguments to components

You can define a component that uses arguments by just adding the symbol in the compnents html delimited by the tilde `~` character.

Something like:
``` html
<a href="~url~">
	This leads to another part of the website
</a>
```
When the component is used the 'url' can be specified as if it was a prop.

``` html
<html>
	<head>
		...
	</head>
	<body>
		<navbar url="/projects/CR.html">
	</body>
</html>
```

Producing:

``` html
<html>
	<head>
		...
	</head>
	<body>
		<a href="/projects/CR.html">
	This leads to another part of the website
</a>
	</body>
</html>
```

Any prop that is not specified is not replaced, except if a `default` is specified on the top, and only the top, line of the component.
> The line must start with `~` else it will be treated as the content of the component and the rest of it will be skipped

Valid

``` html
~url~ = "404.html"
<a href="~url~">
	This leads to another part of the website
</a>
```
Invalid
> (Will not throw an error but will not treat it as a defult definition)

``` html
<p> 
	Lorem ipsum dolor sit amete
</p>
~url~ = "404.html"
<a href="~url~">
	This leads to another part of the website
</a>
```

Accidentally, defining an empty prop as default:

```html
~~ = "404.html"
<a href="~~">
	This leads to another part of the website
</a>
```
will work both with defaults and with props definition `<comp_name =value />`.
Make of this what you want.