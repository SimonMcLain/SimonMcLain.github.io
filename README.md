<!DOCTYPE html>
<html lang="en">
<head>
	<title>Rivers</title>
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<link rel="stylesheet" href="index.css">
	<link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Raleway">
	<script src="https://d3js.org/d3.v5.min.js"></script>
	<script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
	<style>
	/*Change bar colour to grey when hovering over them */
	rect:hover {fill: #778899;}
	* {
	  box-sizing: border-box;
	}
	/*Put padding around each div*/
	div {
	  padding-top: 5px;
	  padding-right: 5px;
	  padding-bottom: 5px;
	  padding-left: 15px;
	}
	/*Set the font type*/
	body,h1 {font-family: "Raleway", sans-serif}
	body, html {height: 100%}
	/* Style the header */
	header {
	  background-color: #005d87;
	  padding: 30px;
	  text-align: center;
	  font-size: 35px;
	  color: white;
	}
	/* Container for flexboxes */
	section {
	  display: -webkit-flex;
	  display: flex;
	}
	/* Style the navigation menu */
	nav {
	  -webkit-flex: 1;
	  -ms-flex: 1;
	  flex: 1;
	  background: #b8cadb;
	  padding: 20px;
	}
	/* Style the article content */
	article {
	  -webkit-flex: 3;
	  -ms-flex: 3;
	  flex: 3;
	  background-color: #FFFFFF;
	  padding: 10px;
	}
	/* Style the footer */
	footer {
	  background-color: #005781;
	  padding: 10px;
	  text-align: center;
	  color: white;
	}
	/* Responsive layout - makes the menu and the content (inside the section) sit on top of each other instead of next to each other */
	@media (max-width: 600px) {
	  section {
		-webkit-flex-direction: column;
		flex-direction: column;
	  }
	}
	</style>
</head>

<body>
	<div>
		<h1>Ocean Plastic Sources</h1>
		<h2>Where does ocean plastic come from?</h2>
	</div>
<header>
	<a href = "waste.html">
		<img onmouseover="bigImg(this)" alt="Test" onmouseout="normalImg(this)" src="images/waste.jpg" height="200" width="250" hspace="25px"></a>
	<a href = "production.html">
		<img onmouseover="bigImg(this)" onmouseout="normalImg(this)"  src="images/factory.jpg" height="200" width="250" hspace="25px"></a>
		<a href = "recycle.html">
		<img onmouseover="bigImg(this)" onmouseout="normalImg(this)" src="images/recycling.jpg" height="200" width="250" hspace="25px"></a>
	<a href = "https://ourworldindata.org/">
		<img onmouseover="bigImg(this)" onmouseout="normalImg(this)" src="images/world.jpg" height="200" width="250" hspace="25px"></a> 
</header>
	<section>
		<nav>
			<h3>Chart Formater</h3>
			<h4>Select delay:</h4>
		<select id="chartDelay">
			<br><option value="1000">1 Seconds</option></br>
			<br><option value="2000">2 Seconds</option></br>
			<br><option value="3000">3 Seconds</option></br>
		</select>
			<br></br>
			<br><button onclick="drawChart()">Draw Chart</button></br>
			<br></br>
			<p> Rivers are a major source of plastic waste into oceans</p>
			<p>It is estimated that between 1.15 and 2.41 million metric tonnes of plastic currenty enters the ocean every year via rivers, with 86% of this global input coming from Asia.</p>
			<p>Click on the polluted beach and recycling icons to discover more facts about which countries consume the most plastic per person and some sample recycling statistics</p>	
		</nav> 
		<article>
			<h2>River sources of ocean plastics</h2>
			<div id="myDiv"></div>
		</article>
	</section>
<footer>
	  <p>Created by G00364775 with assistance from GMIT, W3schools.com, googleapis.com and ourworldindata.org</p>
</footer>
</body>
</html>
<script>
function drawChart(){
// Plastic mass output Data in an array
var myData = [
	{
	 region: 'Africa',
	 tonnes: 109200,
	 },
	 {
	 region: 'South America',
	 tonnes: 67400,
	 },
	 {
	 region: 'India',
	 tonnes: 115000,
	 },
	 {
	 region: 'China',
	 tonnes: 493300,
	 },
	 {
	 region: 'Europe',
	 tonnes: 3900,
	 },
	 {
	 region: 'Indonesia',
	 tonnes: 101300,
	 },
	 {
	 region: 'North America',
	 tonnes: 13400,
	 },
 ];
// Values for Bar Chart
var height = 500;
var width = 800;
var dataCount = myData.length;
var anime = document.getElementById("chartDelay").value;
// Create a scale for Y
var yScale = d3.scaleLinear()
	.domain([0, d3.max(myData, function(d){return d.tonnes})])
	.range([height, 0]);
// Create y Axis
var yAxis = d3.axisLeft()
	.scale(yScale);
// Create a scale for X
var xScale = d3.scaleBand()
	.domain(myData.map(function(d){return d.region;}))
	.range([0, width]);
// Creat a x axis
var xAxis = d3.axisBottom()
	.scale(xScale)
//Delete previous charts when changing chart size
d3.select("#myDiv").selectAll("*").remove();
// Create an svg container
var svgContainer = d3.select("#myDiv").append("svg")
	.attr("width", 1000)
	.attr("height", 1200);
// Create a rectange
var myRectangle = svgContainer.selectAll("rect")
	.data(myData);
// Add attributes to the rectangle
myRectangle.enter()
	.append("rect")
		// Start of transtion
		.attr("fill", "#556B2F")
		.attr("x", function(d, i){return 80 + (i*(width/dataCount));})
		.attr("y", 500)
		.attr("width", 50)
		.transition()
		.duration(3000)
		.delay(anime)
		// Finish of transition	
		.attr("x", function(d, i){return 80 + (i*(width/dataCount));})
		.attr("y", function(d){return yScale(d.tonnes);})
		.attr("width", 50)
		.attr("height", function(d){return height - yScale(d.tonnes);})
		.attr("fill", function(d){
			{return "#F08080";}
			
			
});
// Append chart axis
svgContainer.append("g")
	.attr("transform", "translate(50, 0)")
	.call(yAxis);
svgContainer.append("g")
	.attr("transform", "translate(50, " + height + ")")
	.call(xAxis)
	.selectAll("text")
		.attr("transform", "rotate(50)")
		.attr("text-anchor", "start")
		.attr("x", 9)
		.attr("y", 3)
		.style("font-size", "15px");
}
// function to increase picture sizes on hover
function bigImg(x) {
  x.style.height = "215px";
  x.style.width = "265px";
}
function normalImg(x) {
  x.style.height = "200px";
  x.style.width = "250px";
}
</script>
