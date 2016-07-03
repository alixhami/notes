## HTML Notes

#### Document Skeleton
```html
<!DOCTYPE html>
<html>
	<head>
		<title>Page Title</title>
	</head>
	<body>
	</body>
</html>
```
#### Adding CSS
```html
<!-- in the head tag -->
<style>
	body {background-color:black;}
</style>

<!-- inside the tag itself -->
<h1 style="color:blue;">This is a Blue Heading</h1>

<!-- in the head tag -->
<link rel="stylesheet" type="text/css" href="styles.css">
```
#### Adding JavaScript
```html
<script>
	document.getElementById("demo").innerHTML = "Hello JavaScript!";
</script>

<!-- in case browser doesn't support -->
<noscript>Browser doesn't support JS!</noscript>

<!-- external script -->
<script type="text/javascript" src="script.js"></script>
```
#### Basics
```html
<h1>		<!-- Biggest header -->
<h6>		<!-- Smallest header -->
<p>			<!-- Paragraph -->
<br>		<!-- Line break -->
<ul>		<!-- Unordered list -->
<ol>		<!-- Ordered list -->
<li>		<!-- List item -->
<div>		<!-- Section -->
<span>		<!-- Inline section -->
<a href="">		<!-- Hyperlink -->
<img src="" alt="" width="">	<!-- Image (self closing) -->
```
#### Text Styling
```html
<strong>	<!-- Bold text -->
<em>		<!-- Emphasized text -->
<i>			<!-- Italic text -->
<del>		<!-- Strikethrough text -->
```
#### Table
```html
<table>
  <tr>
  	<th>col1</th>
  	<th>col2</th>
  	<th>col3</th>
  </tr>
  <tr>
  	<td>data1</td>
  	<td>data2</td>
  	<td>data3</td>
  </tr>
</table>
```
