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
<!-- BOOTSTRAP, JQUERY, D3 -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.3/jquery.min.js"></script>
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.4/js/bootstrap.min.js"></script>
<script src="http://d3js.org/d3.v3.min.js"></script>
<script src="http://labratrevenge.com/d3-tip/javascripts/d3.tip.v0.6.3.js"></script>

<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.4/css/bootstrap.min.css">
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
<div class = "container-fluid" id="top-padded">
  Select yo cities: <select id="select-city">
  <option value="">Select a city.</option>
  <option value="Total">Total</option>
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
  <option value="">Select a city.</option>
  <option value="Total">Total</option>
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
<div id="poopchute">
  <div class="row" id="funk_row">
    <div class="col-sm-12">
      <div id="chute_female" class="panel panel-default">
      </div>
    </div>
  </div>
  <div class="row" id="funk_row">
    <div class="col-sm-12">
      <div id="chute_male" class="panel panel-default">
      </div>
    </div>
  </div>
  <div class="row" id="funk_row">
    <div class="col-sm-12">
      <div id="chute_trans" class="panel panel-default">
      </div>
    </div>
  </div>
</div>
<div id="dickchute">
  <div class="row" id="funk_row">
    <div class="col-sm-6">
      <div id="pbod1" class="panel panel-default">
        <div class="panel-body1">
        </div>
      </div>
    </div>
    <div class="col-sm-6">
      <div id="pbod2" class="panel panel-default">
        <div class="panel-body2">
        </div>
      </div>
    </div>
  </div>
</div>
<h4>Marky markov generated sentences!!1</h4>
<button type="button" id="regensentence">Regenerate</button>
<div id="markov-city1">
</div>
<div id="markov-city2">
</div>
</div>
<!-- Button trigger modal -->

<!-- Modal -->
<div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
        <h4 class="modal-title" id="myModalLabel">Dickz</h4>
      </div>
      <div class="modal-body">
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
      </div>
    </div>
  </div>
</div>
<script>
var something_drawn = false;
var city1_sentences = [];
var city2_sentences = [];

$( window ).resize(function() {
  if (something_drawn) {
    $('div#chute_male').empty();
    $('div#chute_female').empty();
    $('div#chute_trans').empty();
    barchart('/data/dookie_craigslist/male_days.csv', '#chute_male', 'Male')
    barchart('/data/dookie_craigslist/female_days.csv', '#chute_female', 'Female')
    barchart('/data/dookie_craigslist/transgender_days.csv', '#chute_trans', 'Transgender')
  }
});

$("#select-city").change(city_dropdown);
$("#select-city1").change(city_dropdown);
// hide that ug shi
d3.select('#pbod1').style('display', 'none').style('cursor', 'pointer').on('click', click_dick)
d3.select('#pbod2').style('display', 'none').style('cursor', 'pointer').on('click', click_dick)
d3.select('#chute_male').style('display', 'none')
d3.select('#chute_female').style('display', 'none')
d3.select('#chute_trans').style('display', 'none')
var city1 = "", city2 = "";

var margin = {top: 40, right: 20, bottom: 30, left: 40},
    width = 560 - margin.left - margin.right,
    height = 300 - margin.top - margin.bottom;

var formatPercent = d3.format(".0%");

var tip = d3.tip()
  .attr('class', 'd3-tip')
  .offset([-10, 0])
  .html(function(d) {
    return "<strong>Frequency:</strong> <span style='color:lightgray'>" + (d.value*100).toFixed(2) + "%</span>"+"<br/><strong>Count:</strong> <span style='color:lightgray'>" + d.count + "</span>";
  })

function click_dick(){
  // Modal
  $('#myModal').modal('show')
  var temp_city = ""
  if (this.id === 'pbod1') {
    temp_city = city1;
  } else {
    temp_city = city2;
  }
  d3.select('#dickforce').remove()
  d3.select("div.modal-body").append("img")
    .attr('src', '/images/craigslist/'+temp_city+'-trigram.png')
    .attr('id', 'dickforce')
}

function new_sentences() {
  var lineNumber = Math.floor(Math.random() * 10000);
  var randomLine = city1_sentences[lineNumber];
  d3.select('#markov-city1').append("p")
    .text(randomLine);

  var lineNumber = Math.floor(Math.random() * 10000);
  var randomLine = city2_sentences[lineNumber];
  d3.select('#markov-city2').append("p")
    .text(randomLine);
}

$(function(){
  $('#regensentence').click(function() {
    new_sentences();
  });
});

function city_dropdown() {
    if ($(this)[0].id === 'select-city') {
    if ($(this).val() != "") {
      city1 = $(this).val()
      $('div#markov-city1').empty();

      $.get('/data/dookie_craigslist/marky/'+city1+'.txt.sentences', function(text) {
          city1_sentences = text.split("\n");
          var lineNumber = Math.floor(Math.random() * 10000);
          var randomLine = city1_sentences[lineNumber];
          d3.select('#markov-city1').append("p")
            .style('font-weight', 'bold')
            .text(format_me[city1]);
          d3.select('#markov-city1').append("p")
            .text(randomLine);
      });

      d3.select('#dickforce1').remove()
      d3.select('#pbod1').style('display', '')
      d3.select(".panel-body1").append("img")
        .attr('src', '/images/craigslist/'+city1+'-trigram.png')
        .attr('id', 'dickforce1')
        // .style('width', '150px')
        // .style('height', '150px')

    }
  } else {
    if ($(this).val() != "") {
      city2 = $(this).val()
      d3.select('#dickforce2').remove()
      d3.select('#pbod2').style('display', '')
      d3.select(".panel-body2").append("img")
        .attr('src', '/images/craigslist/'+city2+'-trigram.png')
        .attr('id', 'dickforce2')
        // .style('width', '150px')
        // .style('height', '150px')

  $('div#markov-city2').empty();
  $.get('/data/dookie_craigslist/marky/'+city2+'.txt.sentences', function(text) {
    city2_sentences = text.split("\n");
    var lineNumber = Math.floor(Math.random() * 10000);
    var randomLine = city2_sentences[lineNumber];
    d3.select('#markov-city2').append("p")
      .style('font-weight', 'bold')
      .text(format_me[city2]);
    d3.select('#markov-city2').append("p")
      .text(randomLine);
  });
    }
  }
  if (city1 == city2) {
    d3.select('#dickforce1').remove()
    d3.select('#dickforce2').remove()
    d3.select('#pbod1').style('display', '')
    d3.select('#pbod2').style('display', 'none')
    d3.select(".panel-body1").append("img")
      .attr('src', '/images/craigslist/'+city1+'-trigram.png')
      .attr('id', 'dickforce1')
  }
  something_drawn = true;
  // Take out anything if its there
  $('div#chute_male').empty();
  $('div#chute_female').empty();
  $('div#chute_trans').empty();
  // display that shit with borders (which were hidden)
  d3.select('#chute_male').style('display', '')
  d3.select('#chute_female').style('display', '')
  d3.select('#chute_trans').style('display', '')
  // Pop with new shit
  barchart('/data/dookie_craigslist/male_days.csv', '#chute_male', 'Male')
  barchart('/data/dookie_craigslist/female_days.csv', '#chute_female', 'Female')
  barchart('/data/dookie_craigslist/transgender_days.csv', '#chute_trans', 'Transgender')

}

format_me = {"Total":"Total","atlanta":"Atlanta","austin":"Austin","boston":"Boston","chicago":"Chicago","dallas":"Dallas","denver":"Denver","detroit":"Detroit","houston":"Houston","lasvegas":"Las Vegas","losangeles":"Los Angeles","miami":"Miasma","minneapolis":"Minneapolis","newyork":"New York","orangecounty":"Orange County","philadelphia":"Philadelphia","phoenix":"Phoenix","portland":"Portland","raleigh":"Raleigh","sacramento":"Sacramento","sandiego":"Sand Diego","seattle":"Seattle","sfbay":"Bay Area","washingtondc":"Washington DC" }

function get_pop_str(data, city){
  ret_str = " "
  var ind = (city === city1) ? 0 : 1;
  if (city1 === "") { ind = 0; }
  var city_pop = d3.sum( data.map(function(d){ console.log(d.cities); return d.cities[ind].count; } ));
  return ": " + city_pop;
}

function barchart(filename, divname, title){

  width = $(divname).width() - margin.left - margin.right,
  height = 300 - margin.top - margin.bottom;

  // Must do once pages is drawn
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


  var color = d3.scale.ordinal().range(['#67a9cf', '#ef8a62'])
  // var color_scale = d3.scale.ordinal().range(["#8aa236", "#7a296a", "#27576b", "#AA7539"]);
  var svg = d3.select(divname).append("svg")
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
          .attr("transform", function(d, i) { return "translate(0," + (i * 20)  + ")"; });

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
          .text(function(d) { return format_me[d] + get_pop_str(data, d); });
    }
  });
}

function type(d) {
  d.frequency = +d.frequency;
  return d;
}
</script>
</dd>
