---
layout: post
title: Blogpost 1 - Andrew Yuan
description: Blogpost 1 - World Cup scored goals
tags: assignments
---

<meta charset="utf-8">
<style>
	body {
	  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
	  margin: auto;
	}
	
	text {
	  font: 10px sans-serif;
	}
	
	.axis path,
	.axis line {
	  fill: none;
	  stroke: #000;
	  shape-rendering: crispEdges;
	}
	
      #tooltip {
        position: absolute;
        width: 200px;
        height: auto;
        padding: 10px;
        background-color: white;
        -webkit-border-radius: 10px;
        -moz-border-radius: 10px;
        border-radius: 10px;
        -webkit-box-shadow: 4px 4px 10px rgba(0, 0, 0, 0.4);
        -moz-box-shadow: 4px 4px 10px rgba(0, 0, 0, 0.4);
        box-shadow: 4px 4px 10px rgba(0, 0, 0, 0.4);
        pointer-events: none;
      }

      #tooltip.hidden {
        display: none;
      }

      #tooltip p {
        margin: 0;
        font-family: sans-serif;
        font-size: 12px;
        line-height: 20px;
      }


</style>

<body>
**Team Members:** Andrew Yuan (agy2108)

<script src="http://d3js.org/d3.v3.min.js">
</script>
<p>
<p>
<br>
<svg></svg>
<div id="tooltip" class="hidden">
        <p><span id="value"></p>
</div>


<script>
/*modified from Mike Bostock at http://bl.ocks.org/3943967 */


var data = [
{"year":2010, "team":"Germany", "round1":5, "round2":4, "round3":7},
{"year":2010, "team":"Netherlands", "round1":5, "round2":2, "round3":5},
{"year":2010, "team":"Uruguay", "round1":4, "round2":2, "round3":5},
{"year":2010, "team":"Argentina", "round1":7, "round2":3, "round3":0},
{"year":2010, "team":"Brazil", "round1":5, "round2":3, "round3":1},
{"year":2010, "team":"Spain", "round1":4, "round2":1, "round3":3},
{"year":2010, "team":"Portugal", "round1":7, "round2":0, "round3":0},
{"year":2010, "team":"Korea Republic", "round1":5, "round2":1, "round3":0},
{"year":2010, "team":"Slovakia", "round1":4, "round2":1, "round3":0},
{"year":2010, "team":"Ghana", "round1":2, "round2":2, "round3":1},
{"year":2010, "team":"USA", "round1":4, "round2":1, "round3":0},
{"year":2010, "team":"Mexico", "round1":3, "round2":1, "round3":0},
{"year":2010, "team":"Cote d'Ivoire", "round1":4, "round2":0, "round3":0},
{"year":2010, "team":"Italy", "round1":4, "round2":0, "round3":0},
{"year":2010, "team":"Japan", "round1":4, "round2":0, "round3":0},
{"year":2010, "team":"South Africa", "round1":3, "round2":0, "round3":0},
{"year":2010, "team":"Chile", "round1":3, "round2":0, "round3":0},
{"year":2010, "team":"Australia", "round1":3, "round2":0, "round3":0},
{"year":2010, "team":"Denmark", "round1":3, "round2":0, "round3":0},
{"year":2010, "team":"Slovenia", "round1":3, "round2":0, "round3":0},
{"year":2010, "team":"England", "round1":2, "round2":1, "round3":0},
{"year":2010, "team":"Nigeria", "round1":3, "round2":0, "round3":0},
{"year":2010, "team":"Paraguay", "round1":3, "round2":0, "round3":0},
{"year":2010, "team":"Serbia", "round1":2, "round2":0, "round3":0},
{"year":2010, "team":"Greece", "round1":2, "round2":0, "round3":0},
{"year":2010, "team":"New Zealand", "round1":2, "round2":0, "round3":0},
{"year":2010, "team":"Cameroon", "round1":2, "round2":0, "round3":0},
{"year":2010, "team":"Korea DPR", "round1":1, "round2":0, "round3":0},
{"year":2010, "team":"France", "round1":1, "round2":0, "round3":0},
{"year":2010, "team":"Switzerland", "round1":1, "round2":0, "round3":0},
{"year":2010, "team":"Algeria", "round1":0, "round2":0, "round3":0},
{"year":2010, "team":"Honduras", "round1":0, "round2":0, "round3":0},
{"year":2006, "team":"Germany", "round1":8, "round2":2, "round3":4},
{"year":2006, "team":"Italy", "round1":5, "round2":1, "round3":6},
{"year":2006, "team":"Argentina", "round1":8, "round2":2, "round3":1},
{"year":2006, "team":"Brazil", "round1":7, "round2":3, "round3":0},
{"year":2006, "team":"Spain", "round1":8, "round2":1, "round3":0},
{"year":2006, "team":"France", "round1":3, "round2":3, "round3":3},
{"year":2006, "team":"Portugal", "round1":5, "round2":1, "round3":1},
{"year":2006, "team":"England", "round1":5, "round2":1, "round3":0},
{"year":2006, "team":"Mexico", "round1":4, "round2":1, "round3":0},
{"year":2006, "team":"Cote d'Ivoire", "round1":5, "round2":0, "round3":0},
{"year":2006, "team":"Australia", "round1":5, "round2":0, "round3":0},
{"year":2006, "team":"Ukraine", "round1":5, "round2":0, "round3":0},
{"year":2006, "team":"Ecuador", "round1":5, "round2":0, "round3":0},
{"year":2006, "team":"Switzerland", "round1":4, "round2":0, "round3":0},
{"year":2006, "team":"Ghana", "round1":4, "round2":0, "round3":0},
{"year":2006, "team":"Korea Republic", "round1":3, "round2":0, "round3":0},
{"year":2006, "team":"Czech Republic", "round1":3, "round2":0, "round3":0},
{"year":2006, "team":"Sweden", "round1":3, "round2":0, "round3":0},
{"year":2006, "team":"Costa Rica", "round1":3, "round2":0, "round3":0},
{"year":2006, "team":"Netherlands", "round1":3, "round2":0, "round3":0},
{"year":2006, "team":"Tunisia", "round1":3, "round2":0, "round3":0},
{"year":2006, "team":"Poland", "round1":2, "round2":0, "round3":0},
{"year":2006, "team":"Saudi Arabia", "round1":2, "round2":0, "round3":0},
{"year":2006, "team":"Paraguay", "round1":2, "round2":0, "round3":0},
{"year":2006, "team":"Serbia and Montenegro", "round1":2, "round2":0, "round3":0},
{"year":2006, "team":"Croatia", "round1":2, "round2":0, "round3":0},
{"year":2006, "team":"USA", "round1":2, "round2":0, "round3":0},
{"year":2006, "team":"Iran", "round1":2, "round2":0, "round3":0},
{"year":2006, "team":"Japan", "round1":2, "round2":0, "round3":0},
{"year":2006, "team":"Angola", "round1":1, "round2":0, "round3":0},
{"year":2006, "team":"Togo", "round1":1, "round2":0, "round3":0},
{"year":2006, "team":"Trinidad and Tobago", "round1":0, "round2":0, "round3":0},
{"year":2002, "team":"Brazil", "round1":11, "round2":2, "round3":5},
{"year":2002, "team":"Germany", "round1":11, "round2":1, "round3":2},
{"year":2002, "team":"Spain", "round1":9, "round2":1, "round3":0},
{"year":2002, "team":"Turkey", "round1":5, "round2":1, "round3":4},
{"year":2002, "team":"Korea Republic", "round1":4, "round2":2, "round3":2},
{"year":2002, "team":"Senegal", "round1":5, "round2":2, "round3":0},
{"year":2002, "team":"USA", "round1":5, "round2":2, "round3":0},
{"year":2002, "team":"England", "round1":2, "round2":3, "round3":1},
{"year":2002, "team":"Portugal", "round1":6, "round2":0, "round3":0},
{"year":2002, "team":"Belgium", "round1":6, "round2":0, "round3":0},
{"year":2002, "team":"Paraguay", "round1":6, "round2":0, "round3":0},
{"year":2002, "team":"Republic of Ireland", "round1":5, "round2":1, "round3":0},
{"year":2002, "team":"Costa Rica", "round1":5, "round2":0, "round3":0},
{"year":2002, "team":"Denmark", "round1":5, "round2":0, "round3":0},
{"year":2002, "team":"Sweden", "round1":4, "round2":1, "round3":0},
{"year":2002, "team":"Italy", "round1":4, "round2":1, "round3":0},
{"year":2002, "team":"Japan", "round1":5, "round2":0, "round3":0},
{"year":2002, "team":"South Africa", "round1":5, "round2":0, "round3":0},
{"year":2002, "team":"Uruguay", "round1":4, "round2":0, "round3":0},
{"year":2002, "team":"Russia", "round1":4, "round2":0, "round3":0},
{"year":2002, "team":"Mexico", "round1":4, "round2":0, "round3":0},
{"year":2002, "team":"Poland", "round1":3, "round2":0, "round3":0},
{"year":2002, "team":"Croatia", "round1":2, "round2":0, "round3":0},
{"year":2002, "team":"Ecuador", "round1":2, "round2":0, "round3":0},
{"year":2002, "team":"Cameroon", "round1":2, "round2":0, "round3":0},
{"year":2002, "team":"Slovenia", "round1":2, "round2":0, "round3":0},
{"year":2002, "team":"Argentina", "round1":2, "round2":0, "round3":0},
{"year":2002, "team":"Tunisia", "round1":1, "round2":0, "round3":0},
{"year":2002, "team":"Nigeria", "round1":1, "round2":0, "round3":0},
{"year":2002, "team":"France", "round1":0, "round2":0, "round3":0},
{"year":2002, "team":"China PR", "round1":0, "round2":0, "round3":0},
{"year":2002, "team":"Saudi Arabia", "round1":0, "round2":0, "round3":0},
{"year":1998, "team":"France", "round1":9, "round2":1, "round3":5},
{"year":1998, "team":"Brazil", "round1":6, "round2":4, "round3":4},
{"year":1998, "team":"Netherlands", "round1":7, "round2":2, "round3":4},
{"year":1998, "team":"Croatia", "round1":4, "round2":1, "round3":6},
{"year":1998, "team":"Argentina", "round1":7, "round2":2, "round3":1},
{"year":1998, "team":"Denmark", "round1":3, "round2":4, "round3":2},
{"year":1998, "team":"Mexico", "round1":7, "round2":1, "round3":0},
{"year":1998, "team":"Germany", "round1":6, "round2":2, "round3":0},
{"year":1998, "team":"Spain", "round1":8, "round2":0, "round3":0},
{"year":1998, "team":"Italy", "round1":7, "round2":1, "round3":0},
{"year":1998, "team":"England", "round1":5, "round2":2, "round3":0},
{"year":1998, "team":"Nigeria", "round1":5, "round2":1, "round3":0},
{"year":1998, "team":"Yugoslavia", "round1":4, "round2":1, "round3":0},
{"year":1998, "team":"Chile", "round1":4, "round2":1, "round3":0},
{"year":1998, "team":"Morocco", "round1":5, "round2":0, "round3":0},
{"year":1998, "team":"Norway", "round1":5, "round2":0, "round3":0},
{"year":1998, "team":"Romania", "round1":4, "round2":0, "round3":0},
{"year":1998, "team":"Belgium", "round1":3, "round2":0, "round3":0},
{"year":1998, "team":"South Africa", "round1":3, "round2":0, "round3":0},
{"year":1998, "team":"Paraguay", "round1":3, "round2":0, "round3":0},
{"year":1998, "team":"Austria", "round1":3, "round2":0, "round3":0},
{"year":1998, "team":"Jamaica", "round1":3, "round2":0, "round3":0},
{"year":1998, "team":"Iran", "round1":2, "round2":0, "round3":0},
{"year":1998, "team":"Saudi Arabia", "round1":2, "round2":0, "round3":0},
{"year":1998, "team":"Cameroon", "round1":2, "round2":0, "round3":0},
{"year":1998, "team":"Korea Republic", "round1":2, "round2":0, "round3":0},
{"year":1998, "team":"Scotland", "round1":2, "round2":0, "round3":0},
{"year":1998, "team":"USA", "round1":1, "round2":0, "round3":0},
{"year":1998, "team":"Bulgaria", "round1":1, "round2":0, "round3":0},
{"year":1998, "team":"Japan", "round1":1, "round2":0, "round3":0},
{"year":1998, "team":"Colombia", "round1":1, "round2":0, "round3":0},
{"year":1998, "team":"Tunisia", "round1":1, "round2":0, "round3":0},
{"year":1994, "team":"Sweden", "round1":6, "round2":3, "round3":6},
{"year":1994, "team":"Brazil", "round1":6, "round2":1, "round3":4},
{"year":1994, "team":"Romania", "round1":5, "round2":3, "round3":2},
{"year":1994, "team":"Spain", "round1":6, "round2":3, "round3":1},
{"year":1994, "team":"Bulgaria", "round1":6, "round2":1, "round3":3},
{"year":1994, "team":"Germany", "round1":5, "round2":3, "round3":1},
{"year":1994, "team":"Netherlands", "round1":4, "round2":2, "round3":2},
{"year":1994, "team":"Italy", "round1":2, "round2":2, "round3":4},
{"year":1994, "team":"Argentina", "round1":6, "round2":2, "round3":0},
{"year":1994, "team":"Nigeria", "round1":6, "round2":1, "round3":0},
{"year":1994, "team":"Russia", "round1":7, "round2":0, "round3":0},
{"year":1994, "team":"Saudi Arabia", "round1":4, "round2":1, "round3":0},
{"year":1994, "team":"Switzerland", "round1":5, "round2":0, "round3":0},
{"year":1994, "team":"Colombia", "round1":4, "round2":0, "round3":0},
{"year":1994, "team":"Belgium", "round1":2, "round2":2, "round3":0},
{"year":1994, "team":"Korea Republic", "round1":4, "round2":0, "round3":0},
{"year":1994, "team":"Mexico", "round1":3, "round2":1, "round3":0},
{"year":1994, "team":"USA", "round1":3, "round2":0, "round3":0},
{"year":1994, "team":"Cameroon", "round1":3, "round2":0, "round3":0},
{"year":1994, "team":"Morocco", "round1":2, "round2":0, "round3":0},
{"year":1994, "team":"Republic of Ireland", "round1":2, "round2":0, "round3":0},
{"year":1994, "team":"Bolivia", "round1":1, "round2":0, "round3":0},
{"year":1994, "team":"Norway", "round1":1, "round2":0, "round3":0},
{"year":1994, "team":"Greece", "round1":0, "round2":0, "round3":0},
{"year":1990, "team":"Germany FR", "round1":10, "round2":2, "round3":3},
{"year":1990, "team":"Czechoslovakia", "round1":6, "round2":4, "round3":0},
{"year":1990, "team":"Italy", "round1":4, "round2":2, "round3":4},
{"year":1990, "team":"England", "round1":2, "round2":1, "round3":5},
{"year":1990, "team":"Yugoslavia", "round1":6, "round2":2, "round3":0},
{"year":1990, "team":"Cameroon", "round1":3, "round2":2, "round3":2},
{"year":1990, "team":"Spain", "round1":5, "round2":1, "round3":0},
{"year":1990, "team":"Belgium", "round1":6, "round2":0, "round3":0},
{"year":1990, "team":"Argentina", "round1":3, "round2":1, "round3":1},
{"year":1990, "team":"Soviet Union", "round1":4, "round2":0, "round3":0},
{"year":1990, "team":"Costa Rica", "round1":3, "round2":1, "round3":0},
{"year":1990, "team":"Colombia", "round1":3, "round2":1, "round3":0},
{"year":1990, "team":"Brazil", "round1":4, "round2":0, "round3":0},
{"year":1990, "team":"Romania", "round1":4, "round2":0, "round3":0},
{"year":1990, "team":"Sweden", "round1":3, "round2":0, "round3":0},
{"year":1990, "team":"Netherlands", "round1":2, "round2":1, "round3":0},
{"year":1990, "team":"Uruguay", "round1":2, "round2":0, "round3":0},
{"year":1990, "team":"Austria", "round1":2, "round2":0, "round3":0},
{"year":1990, "team":"USA", "round1":2, "round2":0, "round3":0},
{"year":1990, "team":"Scotland", "round1":2, "round2":0, "round3":0},
{"year":1990, "team":"United Arab Emirates", "round1":2, "round2":0, "round3":0},
{"year":1990, "team":"Republic of Ireland", "round1":2, "round2":0, "round3":0},
{"year":1990, "team":"Korea Republic", "round1":1, "round2":0, "round3":0},
{"year":1990, "team":"Egypt", "round1":1, "round2":0, "round3":0},
{"year":1986, "team":"Argentina", "round1":6, "round2":1, "round3":7},
{"year":1986, "team":"Soviet Union", "round1":9, "round2":3, "round3":0},
{"year":1986, "team":"France", "round1":5, "round2":2, "round3":5},
{"year":1986, "team":"Belgium", "round1":5, "round2":4, "round3":3},
{"year":1986, "team":"Spain", "round1":5, "round2":5, "round3":1},
{"year":1986, "team":"Denmark", "round1":9, "round2":1, "round3":0},
{"year":1986, "team":"Brazil", "round1":5, "round2":4, "round3":1},
{"year":1986, "team":"Germany FR", "round1":3, "round2":1, "round3":4},
{"year":1986, "team":"England", "round1":3, "round2":3, "round3":1},
{"year":1986, "team":"Mexico", "round1":4, "round2":2, "round3":0},
{"year":1986, "team":"Italy", "round1":5, "round2":0, "round3":0},
{"year":1986, "team":"Paraguay", "round1":4, "round2":0, "round3":0},
{"year":1986, "team":"Korea Republic", "round1":4, "round2":0, "round3":0},
{"year":1986, "team":"Morocco", "round1":3, "round2":0, "round3":0},
{"year":1986, "team":"Portugal", "round1":2, "round2":0, "round3":0},
{"year":1986, "team":"Bulgaria", "round1":2, "round2":0, "round3":0},
{"year":1986, "team":"Hungary", "round1":2, "round2":0, "round3":0},
{"year":1986, "team":"Northern Ireland", "round1":2, "round2":0, "round3":0},
{"year":1986, "team":"Uruguay", "round1":2, "round2":0, "round3":0},
{"year":1986, "team":"Poland", "round1":1, "round2":0, "round3":0},
{"year":1986, "team":"Scotland", "round1":1, "round2":0, "round3":0},
{"year":1986, "team":"Algeria", "round1":1, "round2":0, "round3":0},
{"year":1986, "team":"Iraq", "round1":1, "round2":0, "round3":0},
{"year":1986, "team":"Canada", "round1":0, "round2":0, "round3":0},
{"year":1982, "team":"France", "round1":6, "round2":5, "round3":5},
{"year":1982, "team":"Brazil", "round1":10, "round2":5, "round3":0},
{"year":1982, "team":"Hungary", "round1":12, "round2":0, "round3":0},
{"year":1982, "team":"Italy", "round1":2, "round2":5, "round3":5},
{"year":1982, "team":"Germany FR", "round1":6, "round2":2, "round3":4},
{"year":1982, "team":"Poland", "round1":5, "round2":3, "round3":3},
{"year":1982, "team":"Scotland", "round1":8, "round2":0, "round3":0},
{"year":1982, "team":"Argentina", "round1":6, "round2":2, "round3":0},
{"year":1982, "team":"Soviet Union", "round1":6, "round2":1, "round3":0},
{"year":1982, "team":"England", "round1":6, "round2":0, "round3":0},
{"year":1982, "team":"Northern Ireland", "round1":2, "round2":3, "round3":0},
{"year":1982, "team":"Austria", "round1":3, "round2":2, "round3":0},
{"year":1982, "team":"Algeria", "round1":5, "round2":0, "round3":0},
{"year":1982, "team":"Spain", "round1":3, "round2":1, "round3":0},
{"year":1982, "team":"Chile", "round1":3, "round2":0, "round3":0},
{"year":1982, "team":"Belgium", "round1":3, "round2":0, "round3":0},
{"year":1982, "team":"Honduras", "round1":2, "round2":0, "round3":0},
{"year":1982, "team":"Czechoslovakia", "round1":2, "round2":0, "round3":0},
{"year":1982, "team":"Peru", "round1":2, "round2":0, "round3":0},
{"year":1982, "team":"Yugoslavia", "round1":2, "round2":0, "round3":0},
{"year":1982, "team":"New Zealand", "round1":2, "round2":0, "round3":0},
{"year":1982, "team":"Kuwait", "round1":2, "round2":0, "round3":0},
{"year":1982, "team":"El Salvador", "round1":1, "round2":0, "round3":0},
{"year":1982, "team":"Cameroon", "round1":1, "round2":0, "round3":0},
{"year":1978, "team":"Argentina", "round1":4, "round2":8, "round3":3},
{"year":1978, "team":"Netherlands", "round1":5, "round2":9, "round3":1},
{"year":1978, "team":"Germany FR", "round1":6, "round2":4, "round3":0},
{"year":1978, "team":"Brazil", "round1":2, "round2":6, "round3":2},
{"year":1978, "team":"Italy", "round1":6, "round2":2, "round3":1},
{"year":1978, "team":"Austria", "round1":3, "round2":4, "round3":0},
{"year":1978, "team":"Peru", "round1":7, "round2":0, "round3":0},
{"year":1978, "team":"Poland", "round1":4, "round2":2, "round3":0},
{"year":1978, "team":"Scotland", "round1":5, "round2":0, "round3":0},
{"year":1978, "team":"France", "round1":5, "round2":0, "round3":0},
{"year":1978, "team":"Hungary", "round1":3, "round2":0, "round3":0},
{"year":1978, "team":"Tunisia", "round1":3, "round2":0, "round3":0},
{"year":1978, "team":"Spain", "round1":2, "round2":0, "round3":0},
{"year":1978, "team":"Mexico", "round1":2, "round2":0, "round3":0},
{"year":1978, "team":"Iran", "round1":2, "round2":0, "round3":0},
{"year":1978, "team":"Sweden", "round1":1, "round2":0, "round3":0},
{"year":1974, "team":"Poland", "round1":12, "round2":3, "round3":1},
{"year":1974, "team":"Netherlands", "round1":6, "round2":8, "round3":1},
{"year":1974, "team":"Germany FR", "round1":4, "round2":7, "round3":2},
{"year":1974, "team":"Yugoslavia", "round1":10, "round2":2, "round3":0},
{"year":1974, "team":"Argentina", "round1":7, "round2":2, "round3":0},
{"year":1974, "team":"Sweden", "round1":3, "round2":4, "round3":0},
{"year":1974, "team":"Brazil", "round1":3, "round2":3, "round3":0},
{"year":1974, "team":"Italy", "round1":5, "round2":0, "round3":0},
{"year":1974, "team":"German DR", "round1":4, "round2":1, "round3":0},
{"year":1974, "team":"Scotland", "round1":3, "round2":0, "round3":0},
{"year":1974, "team":"Bulgaria", "round1":2, "round2":0, "round3":0},
{"year":1974, "team":"Haiti", "round1":2, "round2":0, "round3":0},
{"year":1974, "team":"Chile", "round1":1, "round2":0, "round3":0},
{"year":1974, "team":"Uruguay", "round1":1, "round2":0, "round3":0},
{"year":1974, "team":"Zaire", "round1":0, "round2":0, "round3":0},
{"year":1974, "team":"Australia", "round1":0, "round2":0, "round3":0},
{"year":1970, "team":"Brazil", "round1":8, "round2":0, "round3":11},
{"year":1970, "team":"Germany FR", "round1":10, "round2":0, "round3":7},
{"year":1970, "team":"Italy", "round1":1, "round2":0, "round3":9},
{"year":1970, "team":"Peru", "round1":7, "round2":0, "round3":2},
{"year":1970, "team":"Mexico", "round1":5, "round2":0, "round3":1},
{"year":1970, "team":"Soviet Union", "round1":6, "round2":0, "round3":0},
{"year":1970, "team":"Bulgaria", "round1":5, "round2":0, "round3":0},
{"year":1970, "team":"England", "round1":2, "round2":0, "round3":2},
{"year":1970, "team":"Romania", "round1":4, "round2":0, "round3":0},
{"year":1970, "team":"Uruguay", "round1":2, "round2":0, "round3":2},
{"year":1970, "team":"Belgium", "round1":4, "round2":0, "round3":0},
{"year":1970, "team":"Morocco", "round1":2, "round2":0, "round3":0},
{"year":1970, "team":"Sweden", "round1":2, "round2":0, "round3":0},
{"year":1970, "team":"Czechoslovakia", "round1":2, "round2":0, "round3":0},
{"year":1970, "team":"Israel", "round1":1, "round2":0, "round3":0},
{"year":1970, "team":"El Salvador", "round1":0, "round2":0, "round3":0},
{"year":1966, "team":"Portugal", "round1":9, "round2":0, "round3":8},
{"year":1966, "team":"Germany FR", "round1":7, "round2":0, "round3":8},
{"year":1966, "team":"England", "round1":4, "round2":0, "round3":7},
{"year":1966, "team":"Soviet Union", "round1":6, "round2":0, "round3":4},
{"year":1966, "team":"Hungary", "round1":7, "round2":0, "round3":1},
{"year":1966, "team":"Korea DPR", "round1":2, "round2":0, "round3":3},
{"year":1966, "team":"Argentina", "round1":4, "round2":0, "round3":0},
{"year":1966, "team":"Brazil", "round1":4, "round2":0, "round3":0},
{"year":1966, "team":"Spain", "round1":4, "round2":0, "round3":0},
{"year":1966, "team":"Chile", "round1":2, "round2":0, "round3":0},
{"year":1966, "team":"Uruguay", "round1":2, "round2":0, "round3":0},
{"year":1966, "team":"Italy", "round1":2, "round2":0, "round3":0},
{"year":1966, "team":"France", "round1":2, "round2":0, "round3":0},
{"year":1966, "team":"Switzerland", "round1":1, "round2":0, "round3":0},
{"year":1966, "team":"Bulgaria", "round1":1, "round2":0, "round3":0},
{"year":1966, "team":"Mexico", "round1":1, "round2":0, "round3":0},
{"year":1962, "team":"Brazil", "round1":4, "round2":0, "round3":10},
{"year":1962, "team":"Yugoslavia", "round1":8, "round2":0, "round3":2},
{"year":1962, "team":"Chile", "round1":5, "round2":0, "round3":5},
{"year":1962, "team":"Soviet Union", "round1":8, "round2":0, "round3":1},
{"year":1962, "team":"Hungary", "round1":8, "round2":0, "round3":0},
{"year":1962, "team":"Czechoslovakia", "round1":2, "round2":0, "round3":5},
{"year":1962, "team":"Colombia", "round1":5, "round2":0, "round3":0},
{"year":1962, "team":"England", "round1":4, "round2":0, "round3":1},
{"year":1962, "team":"Uruguay", "round1":4, "round2":0, "round3":0},
{"year":1962, "team":"Germany FR", "round1":4, "round2":0, "round3":0},
{"year":1962, "team":"Mexico", "round1":3, "round2":0, "round3":0},
{"year":1962, "team":"Italy", "round1":3, "round2":0, "round3":0},
{"year":1962, "team":"Switzerland", "round1":2, "round2":0, "round3":0},
{"year":1962, "team":"Argentina", "round1":2, "round2":0, "round3":0},
{"year":1962, "team":"Spain", "round1":2, "round2":0, "round3":0},
{"year":1962, "team":"Bulgaria", "round1":1, "round2":0, "round3":0},
{"year":1958, "team":"France", "round1":11, "round2":0, "round3":12},
{"year":1958, "team":"Brazil", "round1":5, "round2":0, "round3":11},
{"year":1958, "team":"Germany FR", "round1":7, "round2":0, "round3":5},
{"year":1958, "team":"Sweden", "round1":5, "round2":0, "round3":7},
{"year":1958, "team":"Paraguay", "round1":9, "round2":0, "round3":0},
{"year":1958, "team":"Czechoslovakia", "round1":9, "round2":0, "round3":0},
{"year":1958, "team":"Yugoslavia", "round1":7, "round2":0, "round3":0},
{"year":1958, "team":"Hungary", "round1":7, "round2":0, "round3":0},
{"year":1958, "team":"Northern Ireland", "round1":6, "round2":0, "round3":0},
{"year":1958, "team":"Argentina", "round1":5, "round2":0, "round3":0},
{"year":1958, "team":"Soviet Union", "round1":5, "round2":0, "round3":0},
{"year":1958, "team":"Wales", "round1":4, "round2":0, "round3":0},
{"year":1958, "team":"England", "round1":4, "round2":0, "round3":0},
{"year":1958, "team":"Scotland", "round1":4, "round2":0, "round3":0},
{"year":1958, "team":"Austria", "round1":2, "round2":0, "round3":0},
{"year":1958, "team":"Mexico", "round1":1, "round2":0, "round3":0},
{"year":1954, "team":"Hungary", "round1":17, "round2":0, "round3":10},
{"year":1954, "team":"Germany FR", "round1":14, "round2":0, "round3":11},
{"year":1954, "team":"Austria", "round1":6, "round2":0, "round3":11},
{"year":1954, "team":"Uruguay", "round1":9, "round2":0, "round3":7},
{"year":1954, "team":"Switzerland", "round1":6, "round2":0, "round3":5},
{"year":1954, "team":"Turkey", "round1":10, "round2":0, "round3":0},
{"year":1954, "team":"Brazil", "round1":6, "round2":0, "round3":2},
{"year":1954, "team":"England", "round1":6, "round2":0, "round3":2},
{"year":1954, "team":"Italy", "round1":6, "round2":0, "round3":0},
{"year":1954, "team":"Belgium", "round1":5, "round2":0, "round3":0},
{"year":1954, "team":"France", "round1":3, "round2":0, "round3":0},
{"year":1954, "team":"Mexico", "round1":2, "round2":0, "round3":0},
{"year":1954, "team":"Yugoslavia", "round1":2, "round2":0, "round3":0},
{"year":1954, "team":"Korea Republic", "round1":0, "round2":0, "round3":0},
{"year":1954, "team":"Scotland", "round1":0, "round2":0, "round3":0},
{"year":1954, "team":"Czechoslovakia", "round1":0, "round2":0, "round3":0},
{"year":1950, "team":"Brazil", "round1":8, "round2":0, "round3":14},
{"year":1950, "team":"Uruguay", "round1":8, "round2":0, "round3":7},
{"year":1950, "team":"Sweden", "round1":5, "round2":0, "round3":6},
{"year":1950, "team":"Spain", "round1":6, "round2":0, "round3":4},
{"year":1950, "team":"Yugoslavia", "round1":7, "round2":0, "round3":0},
{"year":1950, "team":"Chile", "round1":5, "round2":0, "round3":0},
{"year":1950, "team":"Switzerland", "round1":4, "round2":0, "round3":0},
{"year":1950, "team":"USA", "round1":4, "round2":0, "round3":0},
{"year":1950, "team":"Italy", "round1":4, "round2":0, "round3":0},
{"year":1950, "team":"England", "round1":2, "round2":0, "round3":0},
{"year":1950, "team":"Mexico", "round1":2, "round2":0, "round3":0},
{"year":1950, "team":"Paraguay", "round1":2, "round2":0, "round3":0},
{"year":1950, "team":"Bolivia", "round1":0, "round2":0, "round3":0},
{"year":1938, "team":"Brazil", "round1":6, "round2":0, "round3":8},
{"year":1938, "team":"Italy", "round1":2, "round2":0, "round3":9},
{"year":1938, "team":"Sweden", "round1":0, "round2":0, "round3":11},
{"year":1938, "team":"Hungary", "round1":0, "round2":0, "round3":9},
{"year":1938, "team":"Poland", "round1":5, "round2":0, "round3":0},
{"year":1938, "team":"Czechoslovakia", "round1":3, "round2":0, "round3":2},
{"year":1938, "team":"Cuba", "round1":5, "round2":0, "round3":0},
{"year":1938, "team":"Switzerland", "round1":5, "round2":0, "round3":0},
{"year":1938, "team":"Romania", "round1":4, "round2":0, "round3":0},
{"year":1938, "team":"France", "round1":3, "round2":0, "round3":1},
{"year":1938, "team":"Germany", "round1":3, "round2":0, "round3":0},
{"year":1938, "team":"Norway", "round1":1, "round2":0, "round3":0},
{"year":1938, "team":"Belgium", "round1":1, "round2":0, "round3":0},
{"year":1938, "team":"Netherlands", "round1":0, "round2":0, "round3":0},
{"year":1934, "team":"Italy", "round1":7, "round2":0, "round3":5},
{"year":1934, "team":"Germany", "round1":5, "round2":0, "round3":6},
{"year":1934, "team":"Czechoslovakia", "round1":2, "round2":0, "round3":7},
{"year":1934, "team":"Austria", "round1":3, "round2":0, "round3":4},
{"year":1934, "team":"Switzerland", "round1":3, "round2":0, "round3":2},
{"year":1934, "team":"Hungary", "round1":4, "round2":0, "round3":1},
{"year":1934, "team":"Sweden", "round1":3, "round2":0, "round3":1},
{"year":1934, "team":"Spain", "round1":3, "round2":0, "round3":1},
{"year":1934, "team":"France", "round1":2, "round2":0, "round3":0},
{"year":1934, "team":"Argentina", "round1":2, "round2":0, "round3":0},
{"year":1934, "team":"Egypt", "round1":2, "round2":0, "round3":0},
{"year":1934, "team":"Belgium", "round1":2, "round2":0, "round3":0},
{"year":1934, "team":"Netherlands", "round1":2, "round2":0, "round3":0},
{"year":1934, "team":"Romania", "round1":1, "round2":0, "round3":0},
{"year":1934, "team":"USA", "round1":1, "round2":0, "round3":0},
{"year":1934, "team":"Brazil", "round1":1, "round2":0, "round3":0},
{"year":1930, "team":"Argentina", "round1":7, "round2":0, "round3":11},
{"year":1930, "team":"Uruguay", "round1":5, "round2":0, "round3":10},
{"year":1930, "team":"Yugoslavia", "round1":6, "round2":0, "round3":1},
{"year":1930, "team":"USA", "round1":6, "round2":0, "round3":1},
{"year":1930, "team":"Brazil", "round1":5, "round2":0, "round3":0},
{"year":1930, "team":"Chile", "round1":4, "round2":0, "round3":1},
{"year":1930, "team":"France", "round1":4, "round2":0, "round3":0},
{"year":1930, "team":"Mexico", "round1":4, "round2":0, "round3":0},
{"year":1930, "team":"Romania", "round1":3, "round2":0, "round3":0},
{"year":1930, "team":"Paraguay", "round1":1, "round2":0, "round3":0},
{"year":1930, "team":"Peru", "round1":1, "round2":0, "round3":0},
{"year":1930, "team":"Bolivia", "round1":0, "round2":0, "round3":0},
{"year":1930, "team":"Belgium", "round1":0, "round2":0, "round3":0}
];

var editionsData = [
{"year":2010, "host":"South Africa", "1st":"Spain", "2nd":"Netherlands", "3rd":"Germany", "4th":"Uruguay", "Games":32, "GridStart":0, "GridEnd":31},
{"year":2006, "host":"Germany", "1st":"Italy", "2nd":"France", "3rd":"Germany", "4th":"Portugal", "Games":32, "GridStart":32, "GridEnd":63},
{"year":2002, "host":"South Korea/Japan", "1st":"Brazil", "2nd":"Germany", "3rd":"Turkey", "4th":"South Korea", "Games":32, "GridStart":64, "GridEnd":95},
{"year":1998, "host":"France", "1st":"France", "2nd":"Brazil", "3rd":"Croatia", "4th":"Netherlands", "Games":32, "GridStart":96, "GridEnd":127},
{"year":1994, "host":"United States", "1st":"Brazil", "2nd":"Italy", "3rd":"Sweden", "4th":"Bulgaria", "Games":24, "GridStart":128, "GridEnd":151},
{"year":1990, "host":"Italy", "1st":"West Germany", "2nd":"Argentina", "3rd":"Italy", "4th":"England", "Games":24, "GridStart":152, "GridEnd":175},
{"year":1986, "host":"Mexico", "1st":"Argentina", "2nd":"West Germany", "3rd":"France", "4th":"Belgium", "Games":24, "GridStart":176, "GridEnd":199},
{"year":1982, "host":"Spain", "1st":"Italy", "2nd":"West Germany", "3rd":"Poland", "4th":"France", "Games":24, "GridStart":200, "GridEnd":223},
{"year":1978, "host":"Argentina", "1st":"Argentina", "2nd":"Netherlands", "3rd":"Brazil", "4th":"Italy", "Games":16, "GridStart":224, "GridEnd":239},
{"year":1974, "host":"West Germany", "1st":"West Germany", "2nd":"Netherlands", "3rd":"Poland", "4th":"Brazil", "Games":16, "GridStart":240, "GridEnd":255},
{"year":1970, "host":"Mexico", "1st":"Brazil", "2nd":"Italy", "3rd":"West Germany", "4th":"Uruguay", "Games":16, "GridStart":256, "GridEnd":271},
{"year":1966, "host":"England", "1st":"England", "2nd":"West Germany", "3rd":"Portugal", "4th":"Soviet Union", "Games":16, "GridStart":272, "GridEnd":287},
{"year":1962, "host":"Chile", "1st":"Brazil", "2nd":"Czechoslovakia", "3rd":"Chile", "4th":"Yugoslavia", "Games":16, "GridStart":288, "GridEnd":303},
{"year":1958, "host":"Sweden", "1st":"Brazil", "2nd":"Sweden", "3rd":"France", "4th":"West Germany", "Games":16, "GridStart":304, "GridEnd":319},
{"year":1954, "host":"Switzerland", "1st":"West Germany", "2nd":"Hungary", "3rd":"Austria", "4th":"Uruguay", "Games":16, "GridStart":320, "GridEnd":335},
{"year":1950, "host":"Brazil", "1st":"Uruguay", "2nd":"Brazil", "3rd":"Sweden", "4th":"Spain", "Games":13, "GridStart":336, "GridEnd":348},
{"year":1938, "host":"France", "1st":"Italy", "2nd":"Hungary", "3rd":"Brazil", "4th":"Sweden", "Games":14, "GridStart":349, "GridEnd":362},
{"year":1934, "host":"Italy", "1st":"Italy", "2nd":"Czechoslovakia", "3rd":"Germany", "4th":"Austria", "Games":16, "GridStart":363, "GridEnd":378},
{"year":1930, "host":"Uruguay", "1st":"Uruguay", "2nd":"Argentina", "3rd":"United States", "4th":"Yugoslavia", "Games":13, "GridStart":379, "GridEnd":391}
];
 
var n = 4, // number of layers
    m = data.length, // number of samples per layer
    stack = d3.layout.stack();

/*console.log(d3.range(n).map(function(d) { 
                var a = [];
      			for (var i = 0; i < m; ++i) {
        			a[i] = {x: i, y: data[i]['pop' + (d+1)]};
      			}
      			//console.log('hello');
  				//console.log(a);
  				return a;
             }));
*/    
var labels = data.map(function(d) {return d.team;});

console.log(labels);
    
    //go through each layer (pop1, pop2 etc, that's the range(n) part)
    //then go through each object in data and pull out that objects's population data
    //and put it into an array where x is the index and y is the number

var gapSize = 0.5;
var layers = stack(d3.range(n).map(function(d) { 
				console.log(d);
                var a = [];
      			for (var i = 0; i < m; ++i) {
      				if (d == 0) {
      					a[i] = {x: i, 
        					y: gapSize,
        					year: data[i]['year'],
        					team: data[i]['team'],
        					round: (d),
        					goals: (data[i]['round1'] + data[i]['round2'] + data[i]['round3'])
        					};
      				}
      				else {
      					a[i] = {x: i, 
        					y: data[i]['round' + (d)],
        					year: data[i]['year'],
        					team: data[i]['team'],
        					round: (d),
        					goals: (data[i]['round1'] + data[i]['round2'] + data[i]['round3'])
        					};	
      				}
      			}
      			//console.log('hello');
  				//console.log(a);
  				return a;
             }));
    //console.log('layers');
    //console.log(layers);
	//the largest single layer
var x = d3.max(layers, function(layer) {
    		 
    		return d3.max(layer, function(d) { 
    									return d.y; 
    										}); 
    									}),
    //the largest stack
    yStackMax = d3.max(layers, function(layer) { return d3.max(layer, function(d) { return d.y0 + d.y; }); });

var margin = {top: 15, right: 10, bottom: 5, left: 100},
    width = 1000 - margin.left - margin.right,
    height = 1200 - margin.top - margin.bottom;
//    height = 533 - margin.top - margin.bottom;


var yScale = d3.scale.ordinal()
    .domain(d3.range(m))
    .rangeRoundBands([0, height], .3);

var xScale = d3.scale.linear()
    .domain([0, yStackMax])
    .range([0, width]);

//var color = d3.scale.linear()
//    .domain([0, n - 1])
//    .range(["#BDAEE5", "#A15D76"]);
//    .range(["#5F5572", "#CB6C69"]);
//    .range(["#aad", "#556"]);
//var color = ["#465971", "#728DB3", "#A3C6FA"];
//var color = ["#6982A5", "#B67FAA", "#FD897B"];
//var color = ["#46475F", "#757297", "#C7B7F1"];
//var color = ["black", "#969AC9", "#D6AA4B", "#C76A77"];
//var color = ["black", "#614DC4", "#659FE0", "#54EBB6"];
var color = ["#ddd", "#4C374C", "#967AA4", "#CCAFE8"];

var svg = d3.select("svg")
    .attr("width", width + margin.left + margin.right)
    .attr("height", height + margin.top + margin.bottom)
  .append("g")
    .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

var layer = svg.selectAll(".layer")
    .data(layers)
  .enter().append("g")
    .attr("class", "layer")
    .style("fill", function(d, i) { return color[i]; });

layer.selectAll("rect")
    .data(function(d) { return d; })
  	.enter().append("rect")
    .attr("y", function(d) { return yScale(d.x); })
	.attr("x", 0)
    .attr("height", 0)
    .attr("width", 0)
    .on("mouseover", function(d){
               //highlight text
               //d3.select(this).classed("cell-hover",true);
               //d3.selectAll(".rowLabel").classed("text-highlight",function(r,ri){ return ri==(d.row-1);});
               //d3.selectAll(".colLabel").classed("text-highlight",function(c,ci){ return ci==(d.col-1);});
        
               //Update the tooltip position and value
               console.log(this);
               d3.select(this).attr("fill", "red");

               if(d.round != 0) {
               		tooltip = d.year + " - " + d.team + " - " + d.goals + " goals (" + d.y + " in round)";
               	}
               else {
               		tooltip = d.year + " - " + d.team + " - " + d.goals + " goals";
               	}

               d3.select("#tooltip")
//                 .style("left", (d3.event.pageX+10) + "px")
                 .style("left", xScale(0) + "px")
                 .style("top", (d3.event.pageY-10) + "px")
                 .select("#value")
                 .text(tooltip);  
  //                 .text(d.team + " - " + d.goals + " goals (" + d.y + " in round)");  
                 //.text("team:"+rowLabel[d.row-1]+","+colLabel[d.col-1]+"\ndata:"+d.value+"\nrow-col-idx:"+d.col+","+d.row+"\ncell-xy "+this.x.baseVal.value+", "+this.y.baseVal.value);  
               //Show the tooltip
               d3.select("#tooltip").classed("hidden", false);
       })
    .on("mouseout", function(d){
//               d3.select(this).classed("cell-hover",false);
//               d3.selectAll(".rowLabel").classed("text-highlight",false);
//               d3.selectAll(".colLabel").classed("text-highlight",false);
               d3.select(this).attr("fill", color[d.round]);
               d3.select("#tooltip").classed("hidden", true);
        })
	.transition()
	.delay(function(d) { return (d.x * 10);})
	.duration(750)
    .attr("y", function(d) { return yScale(d.x); })
	.attr("x", function(d) { return xScale(d.y0-gapSize); })
    .attr("height", yScale.rangeBand())
    .attr("width", function(d) { return xScale(d.y); })
     ;

var yAxis = d3.svg.axis()
    .scale(yScale)
    .tickSize(1)
    .tickPadding(1)
	.tickValues("")
    .orient("left");

var xAxis = d3.svg.axis()
    .scale(xScale)
    .tickSize(1)
    .tickPadding(1)
	.tickValues([0, 5, 10, 15, 20, 25])
    .orient("top");


svg.append("g")
    .attr("class", "y axis")
    .call(yAxis);

svg.append("g")
    .attr("class", "x axis")
    .call(xAxis);

//vertical lines
svg.selectAll(".vline").data([0, 5, 10, 15, 20, 25]).enter()
    .append("line")
    .attr("x1", function (d) {
	    return xScale(d);
	})
    .attr("x2", function (d) {
    	return xScale(d);
	})
    .attr("y1", 0)
    .attr("y2", height)
	.style("stroke", "#eee");

//horizontal lines
svg.selectAll(".hline").data([32, 64, 96, 128, 152, 176, 200, 224, 240, 256, 272, 288, 304, 320, 336, 349, 363, 379, 392]).enter()
    .append("line")
    .attr("y1", function (d) {
	    return yScale(d);
	})
    .attr("y2", function (d) {
    	return yScale(d);
	})
    .attr("x1", -100)
    .attr("x2", width)
	.style("stroke", "#ccc");

// Add label

svg.selectAll(".labeltext")
      .data(editionsData)
      .enter().append("text")
      .text(function(d) { return d.year; })
      .attr("x", xScale(0)-margin.left)
      .attr("y", function(d, i) { 
      	console.log((d.GridStart));
      	console.log(yScale(d.GridStart + 5));
      	return yScale(Math.round((d.GridStart + d.GridEnd)/2)); })
      .style("font-size", "16px")
      .style("font-weight", "bold")
      .attr("text-anchor", "left");

svg.selectAll(".labeltext2")
      .data(editionsData)
      .enter().append("text")
      .text(function(d) { return d.host; })
      .attr("x", xScale(20))
      .attr("y", function(d, i) { 
      	console.log((d.GridStart));
      	console.log(yScale(d.GridEnd));
      	return yScale(d.GridEnd); })
      .style("font-size", "25px")
      .style("font-style", "italic")
      .style("font-weight", "bold")
      .style("fill", "#ddd")
      .attr("text-anchor", "left");


var legend = svg.selectAll(".legend")
    .data(["1st Round", "2nd Round", "Finals"])
  	.enter().append("g")
    .attr("class", "legend");
//    .style("fill", function(d, i) { return color[i+1]; });

legend.selectAll("rect")
    .data(["1st Round", "2nd Round", "Finals", "border"])
  	.enter().append("rect")
    .attr("y", function(d, i) {
    	if (d!="border"){
    		return yScale(2);
    	}    	
    	else {
    		return yScale(0);
    	}})
	.attr("x", function(d, i) { 
		if (d!="border"){
			return xScale(20.1+(i*3));
		}
		else {
			return xScale(20);
		}})
    .attr("height", function(d, i){
    	if (d!="border"){
    		return 10;
    	}
    	else {
			return 21;
    	}})
    .attr("width", function(d, i) {
    	if (d!="border"){
    		return 10;
    	}
    	else {
			return 250;
    	}})
    .style("fill", function(d, i) { 
    	if (d!="border"){
    		return color[i+1]; 
    	}
    	else {
    		return "none";
    	}})
	.style("stroke", "#555")
	  .style("stroke-width", "0.3px")
;
    	
console.log(legend);


legend.selectAll("text")
    .data(["1st Round", "2nd Round", "Finals"])
  	.enter().append("text")
  	.text(function(d) { return d; })
    .attr("y", function(d, i) { return yScale(5); })
	.attr("x", function(d, i) { 
		console.log(d);
		return xScale(20.5+(i*3)); })
    .style("font-size", "9px");

</script>

</body>

