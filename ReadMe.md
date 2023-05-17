# CR

A simple Component Replacer script

The components are just html files, the name of the component is the name of the file that contains said component

## Args

No settings (yet)

First argument is the base file

Second argument is the destination file

Every other argument is a component file that will be used to replace the specific tag

## Feature to add

### Multiple component for a single file

I don't really think that this is of any use

### Arguments support for component

Something like
```html
<html>
	<head>
		...
	</head>
	<body>
		<Navbar color="BLUE"/>
	</body>
</html>
```

and the component would look like

```html
$args(color="default", ...)
<nav color=$color>
	
</nav>
```

but this would need file parsing and that is NOT fun
