---
layout: post
title:  "Mining Craigslist Missed Connections"
date:   2015-04-16 18:38:49
categories: jekyll update
---

Remember that time I saw you in the airport waiting in line to buy a Cinnabon? 
We made eye contact, but then I was too shy to scoot my [Rascal R6 300](http://www.scootaround.com/files/manuals/electricmobility/Electric%20Mobility%20Rascal%20R6%20300,%20R6%20300HD%20Scooter%20Owner%27s%20Manual.pdf "In Ferrari-red.") up to you to talk.
You were wearing tight leopard skin leggings, you were huge, you were beautiful. 
You know I wanted to fly a helicopter right up that a$$. 


We happened across hundreds of fine Craigslist missed connections...


We analyzed the popularity of missed connections posts by day, split by gender of the poster for large US cities. 
Curiously, the bulk of the distribution does not always fall on around the weekend.
<!-- Ugly D3 code from here on out. -->
<dd>
<meta charset="utf-8">
<style>
body {
  font: 10px sans-serif;
}

.axis path,
.axis line {
  fill: none;
  stroke: #000;
  shape-rendering: crispEdges;
}

.bar:hover {
  fill: orangered ;
}

.x.axis path {
  display: none;
}

.d3-tip {
  line-height: 1;
  font-weight: bold;
  padding: 12px;
  background: rgba(0, 0, 0, 0.8);
  color: #fff;
  border-radius: 2px;
}

/* Creates a small triangle extender for the tooltip */
.d3-tip:after {
  box-sizing: border-box;
  display: inline;
  font-size: 10px;
  width: 100%;
  line-height: 1;
  color: rgba(0, 0, 0, 0.8);
  content: "\25BC";
  position: absolute;
  text-align: center;
}

/* Style northward tooltips differently */
.d3-tip.n:after {
  margin: -1px 0 0 0;
  top: 100%;
  left: 0;
}
</style>

Select yo cities: <select id="select-city">
  <option value="">Total</option>
  <option value="atlanta">Atlanta</option>
  <option value="austin">Austin</option>
  <option value="boston">Boston</option>
  <option value="chicago">Windy Shitty (Chicago)</option>
  <option value="dallas">Dallas</option>
  <option value="denver">Denver</option>
  <option value="detroit">Detroit</option>
  <option value="houston">Houston</option>
  <option value="lasvegas">Las Vegas</option>
  <option value="losangeles">Los Angeles</option>
  <option value="miami">Miasma</option>
  <option value="minneapolis">Minneapolis</option>
  <option value="newyork">New York</option>
  <option value="orangecounty">Orange County</option>
  <option value="philadelphia">Philadelphia</option>
  <option value="phoenix">Phoenix</option>
  <option value="portland">Portland</option>
  <option value="raleigh">Raleigh</option>
  <option value="sacramento">Sacramento</option>
  <option value="sandiego">Sand Diego</option>
  <option value="seattle">Seattle</option>
  <option value="sfbay">Man Bay (Bay Area)</option>
  <option value="washingtondc"> Washington DC </option>
</select>
<select id="select-city1">
  <option value="">Total</option>
  <option value="atlanta">Atlanta</option>
  <option value="austin">Austin</option>
  <option value="boston">Boston</option>
  <option value="chicago">Windy Shitty (Chicago)</option>
  <option value="dallas">Dallas</option>
  <option value="denver">Denver</option>
  <option value="detroit">Detroit</option>
  <option value="houston">Houston</option>
  <option value="lasvegas">Las Vegas</option>
  <option value="losangeles">Los Angeles</option>
  <option value="miami">Miasma</option>
  <option value="minneapolis">Minneapolis</option>
  <option value="newyork">New York</option>
  <option value="orangecounty">Orange County</option>
  <option value="philadelphia">Philadelphia</option>
  <option value="phoenix">Phoenix</option>
  <option value="portland">Portland</option>
  <option value="raleigh">Raleigh</option>
  <option value="sacramento">Sacramento</option>
  <option value="sandiego">Sand Diego</option>
  <option value="seattle">Seattle</option>
  <option value="sfbay">Man Bay (Bay Area)</option>
  <option value="washingtondc"> Washington DC </option>
</select>
<div id="poopchute"></div>

<script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.3/jquery.min.js"></script>
<script src="http://d3js.org/d3.v3.min.js"></script>
<script src="http://labratrevenge.com/d3-tip/javascripts/d3.tip.v0.6.3.js"></script>
<script>
$("#select-city").change(city_dropdown);
$("#select-city1").change(city_dropdown);

var city1 = "all", city2 = "all";

var margin = {top: 40, right: 20, bottom: 30, left: 40},
    width = 560 - margin.left - margin.right,
    height = 300 - margin.top - margin.bottom;

var formatPercent = d3.format(".0%");

var x0 = d3.scale.ordinal()
    .rangeRoundBands([0, width], .3);

var x1 = d3.scale.ordinal();

var y = d3.scale.linear()
    .range([height, 0]);

var xAxis = d3.svg.axis()
    .scale(x0)
    .orient("bottom");

var yAxis = d3.svg.axis()
    .scale(y)
    .orient("left")
    .tickFormat(formatPercent);

var tip = d3.tip()
  .attr('class', 'd3-tip')
  .offset([-10, 0])
  .html(function(d) {
    return "<strong>Frequency:</strong> <span style='color:lightgray'>" + (d.value*100).toFixed(2) + "%</span>"+"<br/><strong>Count:</strong> <span style='color:lightgray'>" + d.count + "</span>";
  })
function city_dropdown() {
    if ($(this)[0].id === 'select-city') {
    if ($(this).val() != "") {
      city1 = $(this).val()
    }
  } else {
    if ($(this).val() != "") {
      city2 = $(this).val()
    }
  }
  $('div#poopchute').empty();
  barchart('/data/dookie_craigslist/male_days.csv', 'Derp', 'Male')
  barchart('/data/dookie_craigslist/female_days.csv', 'Derp', 'Female')
  barchart('/data/dookie_craigslist/transgender_days.csv', 'Derp', 'Transgender')
}


function barchart(filename, xlabel, title){
  var color = d3.scale.ordinal().range(['#67a9cf', '#ef8a62'])
  // var color_scale = d3.scale.ordinal().range(["#8aa236", "#7a296a", "#27576b", "#AA7539"]);
  var svg = d3.select("div#poopchute").append("svg")
      .attr("width", width + margin.left + margin.right)
      .attr("height", height + margin.top + margin.bottom)
    .append("g")
      .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

  svg.call(tip);
  var both_data = [];
  var max_count = 0;
  var max_freq = 0.0;
  d3.csv(filename, function(error, data) {
    if (data.length === 0 && data1.length === 0){
       svg.append("g")
          .attr("class", "x axis")
          .attr("transform", "translate(0," + height + ")")
          .call(xAxis);
    } else {    
      var cityNames = d3.keys(data[0]).filter(function(key) { return key !== "Day" && (key === city2 || key === city1); });

      data.forEach(function(d) {
        d.cities = cityNames.map(function(name) { return {name: name, value:+d[name], count:+d[name+'_count']};   });
      });
      console.log(data)

      x0.domain(data.map(function(d) { return d.Day; }));
      x1.domain(cityNames).rangeRoundBands([0, x0.rangeBand()]);
      y.domain([0, d3.max(data, function(d) { return d3.max(d.cities, function(d) { return d.value; }); })]);

      svg.append("g")
          .attr("class", "x axis")
          .attr("transform", "translate(0," + height + ")")
          .call(xAxis);
      svg.append("g")
          .attr("class", "y axis")
          .call(yAxis)
        .append("text")
          .attr("transform", "rotate(-90)")
          .attr("y", 6)
          .attr("dy", ".71em")
          .style("text-anchor", "end")
          .text("Population");
    
      svg.append('text')
        .attr('y', -15)
        .attr('x', width/2)
        .text(title)
        .style('text-anchor', 'middle')
        .style('font-size', 20)
        .style('font-weight', 'bold')

      var day = svg.selectAll(".day")
          .data(data)
        .enter().append("g")
          .attr("class", "g")
          .attr("transform", function(d) { return "translate(" + x0(d.Day) + ",0)"; });

      day.selectAll("rect")
          .data(function(d) { return d.cities; })
        .enter().append("rect")
          .attr("width", x1.rangeBand())
          .attr("x", function(d) { return x1(d.name); })
          .attr("y", function(d) { return y(d.value); })
          .attr("height", function(d) { return height - y(d.value); })
          .style("fill", function(d) { return color(d.name); })
          .on('mouseover', tip.show)
          .on('mouseout', tip.hide);

      var legend = svg.selectAll(".legend")
          .data(cityNames.slice().reverse())
        .enter().append("g")
          .attr("class", "legend")
          .attr("transform", function(d, i) { return "translate(0," + i * 20 + ")"; });

      legend.append("rect")
          .attr("x", width - 18)
          .attr("width", 18)
          .attr("height", 18)
          .style("fill", color);

      legend.append("text")
          .attr("x", width - 24)
          .attr("y", 9)
          .attr("dy", ".35em")
          .style("text-anchor", "end")
          .text(function(d) { return d; });
    }
  });
}

function type(d) {
  d.frequency = +d.frequency;
  return d;
}
</script>
</dd>