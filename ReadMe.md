# CR

A simple Component Replacer script

The components are just html files, the name of the component is the name of the file that contains said component.

An example of a component is:

`file: navbar.html`
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

`file: index.html`
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


`file: result.html`
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

1. `base` file; the file that refers to / uses components.
2. `result` file; the file that will be produced as a result with the component expanded.
3. `component`s files; the files of all the component that might be present in the base file.

### Passing arguments to components

You can define a component that uses arguments by just adding the symbol in the components body delimited by the tilde `~` character.

Something like:
`file: link.html`
``` html
<a href=~url~>
	This leads to another part of the website
</a>
```
When the component is used the 'url' can be specified as if it was a prop.

`file: link.html`
``` html
<html>
	<head>
		...
	</head>
	<body>
		<link url="/projects/CR.html">
	</body>
</html>
```

Producing:

`file: result.html`
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

Any prop that is not specified is not replaced, except if a `default` is specified on the top, and only the top, lines of the component.
> The line must start with `~` else it will be treated as the content of the component and the rest of it will be skipped

Valid

``` html
~url~ = "404.html"
<a href=~url~>
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
<a href=~url~>
	This leads to another part of the website
</a>
```

Accidentally, defining an empty prop as default:

```html
~~ = "404.html"
<a href=~~>
	This leads to another part of the website
</a>
```
will work both with defaults and with props definition `<comp_name =value />`.
Make of this what you want.
