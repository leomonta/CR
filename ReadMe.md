# CR

A simple Component Replacer script

The components are just html files, the name of the component is the name of the file that contains said component

An example of a component is

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
And can be used like this

``` html
<html>
	<head>
		...
	</head>
	<body>
		<navbar/>
	</body>
</html>

```

Resulting in


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
		<div id="gh-projects" class="dropdown-options"></div>
	</div>
</nav>
	</body>
</html>

```
Be wary that the tool does not hve any regards for indentation (as shown)


## Args

First argument is the base file, the file that refers / uses components

Second argument is the destination file, the file that will be written with the component added

Every other argument is a component file that will be used to replace the specific tag

## Passing arguments to components

You can define a component that uses arguments by just adding the symbol in the compnents html delimited by tilde '~'

Something like
``` html
<a href="~url~">
	This leads to another part of the website
</a>
```
When the component is used the 'url' can be specified as if it was a prop

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

producing

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

Any prop that is not specified is not replaced, except if a default value is specified on the firsts line of the component

Valid

``` html
~url~ = "404.html"
<a href="~url~">
	This leads to another part of the website
</a>
```
Invalid

``` html
<p> 
	Lorem ipsum dolor sit amete
</p>
~url~ = "404.html"
<a href="~url~">
	This leads to another part of the website
</a>
```
