---
layout: post
title:  "Welcome to Jekyll!"
date:   2015-04-16 18:38:49
categories: jekyll update
---

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
Select the cities: <select id="select-city">
  <option value="all">Total</option>
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
  <option value="washingtondc"> Washington DC </options>
</select>
<select id="select-city1">
  <option value="all">Total</option>
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
  <option value="washingtondc"> Washington DC </options>
</select>
<div id="poopchute"></div>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.3/jquery.min.js"></script>
<script src="http://d3js.org/d3.v3.min.js"></script>
<script src="http://labratrevenge.com/d3-tip/javascripts/d3.tip.v0.6.3.js"></script>
<script>

$("#select-city").change(city_dropdown);
$("#select-city1").change(city_dropdown);

console.log('Running 1')
var city1 = "all", city2 = "all";

var margin = {top: 40, right: 20, bottom: 30, left: 40},
    width = 560 - margin.left - margin.right,
    height = 300 - margin.top - margin.bottom;

var formatPercent = d3.format(".0%");

var x = d3.scale.ordinal()
    .rangeRoundBands([0, width], .1);

var y = d3.scale.linear()
    .range([height, 0]);

var xAxis = d3.svg.axis()
    .scale(x)
    .orient("bottom");

var yAxis = d3.svg.axis()
    .scale(y)
    .orient("left")
    .tickFormat(formatPercent);

var tip = d3.tip()
  .attr('class', 'd3-tip')
  .offset([-10, 0])
  .html(function(d) {
    return "<strong>Frequency:</strong> <span style='color:red'>" + (d.frequency*100).toFixed(2) + "%</span>"+"<br/><strong>Count:</strong> <span style='color:orange'>" + d.count + "</span>";
  })


function city_dropdown() {
  console.log('Running 2')
  if ($(this)[0].id === 'select-city') {
    if ($(this).val() === 'all') {
      city1 = ""
    } else {
      city1 = $(this).val()+"_";
    }
  } else {
    if ($(this).val() === 'all') {
      city2 = ""
    } else {
      city2 = $(this).val()+"_";
    }
  }
  $('div#poopchute').empty();
  barchart("dookie_craigslist/"+city1+"male_time.tsv", "dookie_craigslist/"+city2+"male_time.tsv", "Time of Day", "#CFD369");
  barchart("dookie_craigslist/"+city1+"male_days.tsv","dookie_craigslist/"+city2+"male_days.tsv", "Day of the Week", "#CFD369");
  barchart("dookie_craigslist/"+city1+"female_time.tsv","dookie_craigslist/"+city2+"female_time.tsv", "Time of Day", "#C36279");
  barchart("dookie_craigslist/"+city1+"female_days.tsv","dookie_craigslist/"+city2+"female_days.tsv", "Day of the Week", "#C36279");
  barchart("dookie_craigslist/"+city1+"trans_time.tsv","dookie_craigslist/"+city2+"trans_time.tsv", "Time of Day", "#447884");
  barchart("dookie_craigslist/"+city1+"trans_days.tsv","dookie_craigslist/"+city2+"trans_days.tsv", "Day of the Week", "#447884");
}


function barchart(filename1, filename2, xlabel, color){
  console.log('Running 3')
  var svg = d3.select("div#poopchute").append("svg")
      .attr("width", width + margin.left + margin.right)
      .attr("height", height + margin.top + margin.bottom)
    .append("g")
      .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

  svg.call(tip);
  
  d3.csv("web_data/data.csv", function(error, data) {  
    console.log(data);
  });

  both_data = []
  d3.tsv(filename1, type, function(error, data) {
    d3.tsv(filename2, type, function(error1, data1) {
      
      // both_data.push(data)
      // both_data.push(data1)
      console.log(both_data)
      // x.domain(both_data.map(function(d) { return d.time; }));
      // y.domain([0, d3.max(both_data, function(d) { return d.frequency; })]);

  // d3.csv("data.csv", function(error, data) {
    var ageNames = [atlanta, boston]

    data.forEach(function(d) {
      d.ages = ageNames.map(function(name) { return {name: name, value: +d[name]}; });
    });

    // x0.domain(data.map(function(d) { return d.State; }));
    // x1.domain(ageNames).rangeRoundBands([0, x0.rangeBand()]);
    x0.domain([city1, city2]);
    x1.domain([])
    y.domain([0, d3.max(data, function(d) { return d3.max(d.ages, function(d) { return d.value; }); })]);

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

    var state = svg.selectAll(".state")
        .data(data)
      .enter().append("g")
        .attr("class", "g")
        .attr("transform", function(d) { return "translate(" + x0(d.State) + ",0)"; });

    state.selectAll("rect")
        .data(function(d) { return d.ages; })
      .enter().append("rect")
        .attr("width", x1.rangeBand())
        .attr("x", function(d) { return x1(d.name); })
        .attr("y", function(d) { return y(d.value); })
        .attr("height", function(d) { return height - y(d.value); })
        .style("fill", function(d) { return color(d.name); })
        .on('mouseover', tip.show)
        .on('mouseout', tip.hide);

    var legend = svg.selectAll(".legend")
        .data(ageNames.slice().reverse())
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
    });
  });
}

function type(d) {
  d.frequency = +d.frequency;
  return d;
}
</script>
</div>
</dd>