---
layout: page
permalink: /about/index.html
title: Jon Thomas Van Lew
tags: [jtvanlew, me]
chart: true
charttype: pie
comments: true
---

{% assign total_words = 0 %}
{% assign readtime = 0 %}
{% assign featuredcount = 0 %}
{% assign statuscount = 0 %}

{% for post in site.posts %}
    {% assign post_words = post.content | strip_html | number_of_words %}
    {% if site.wpm %}{% assign indi_readtime = post_words | append: '.0' | divided_by:site.wpm %}{% else %}{% assign indi_readtime = post_words | append: '.0' | divided_by:180 %}{% endif %}
    {% assign total_words = total_words | plus: post_words %}
    {% assign readtime = readtime | plus: indi_readtime %}
    {% if post.featured %}
    {% assign featuredcount = featuredcount | plus: 1 %}
    {% endif %}
{% endfor %}
{% for status in site.data.statuses %}{% assign statuscount = statuscount | plus:1 %}{% endfor %}

My name is ^^ and this is my website. 

This is Molly, the eponymous little black dog:

<figure>
	<img src="{{ site.url }}/images/page/about/molly-bw.jpg" alt="Molly">
	<figcaption>Molly, so serious</figcaption>
</figure>

This is the start of Molly's story, written by the rescue agency that found her:

2012年二月初，台灣動物緊急救援小組大隊長在執行例行性巡邏時，途經高雄市燕巢區一處養豬場旁，發現有兩隻剛出生不久的小幼犬穿梭在附近的草堆內，動物救援小組大隊長靠近仔細查看後發現兩隻小狗身上都患有嚴重的皮膚病，又不見母狗在身旁照顧，動物救援小組大隊長便將兩隻小幼犬送往動物醫院接受皮膚病治療，並會在狗兒療程結束恢復健康後，為牠們尋找溫暖新家。

If you really paid attention, you may have noticed something strange about that story: it's in Chinese and you can't read it. Ho ho, you clever dog! Molly and her sister were found outside a pig farm in Taiwan (explaining the language) with a skin disease and no mother around to take care of them. The particular rescue agency that took care of her then put her online for an abroad adoption -- which is how we came to find her. She was flown to LAX by a volunteer and picked up by us. Here's Molly a few days after she arrived in Los Angeles, 

<figure>
	<img src="{{ site.url }}/images/page/about/molly-young.jpg" alt="young Molly">
	<figcaption>Molly soon after arriving from Taiwan</figcaption>
</figure>

I love this dog a whole lot.

<hr>
## Website info
The blog-o-side of my site currently has a total of {{ site.posts | size }} posts in {{ site.categories | size }} categories which combined have only {{ total_words }} words. When you think about it, that will only take an average reader (going at {{ site.wpm }} WPM) approximately {% if readtime > 60 %}{% assign readtime_hours = readtime | divided_by: 60 %}{% assign readtime_minutes = readtime | modulo:60 %}{% if readtime_hours > 1 and readtime_hours < 2 %}1 hour{% else %}<span class="hour">{{ readtime_hours }}</span> hours{% endif %}{% if readtime_minutes < 1 %}{% elsif readtime_minutes > 1 and readtime_minutes < 1.5 %} and 1 minute {% elsif readtime_minutes > 1.5 %} and <span class="time">{{ readtime_minutes }}</span> minutes{% endif %}{% else %}{% if readtime < 1 %}less than 1 minute {% elsif readtime > 1 and readtime < 1.5 %}1 minute {% elsif readtime > 1.5 %}<span class="time">{{ readtime }}</span> minutes {% endif %}{% endif %} to read. So, heck, go through the entire site while you're here!

The page is maintained on GitHub where it's powered by [Jekyll](http://jekyllrb.com/). The last commit to the github repository was on {{ site.time | date: "%A, %d %b %Y" }} at {{ site.time | date: "%I:%M %p" }} [UTC](http://en.wikipedia.org/wiki/Coordinated_Universal_Time "Temps Universel Coordonné").

We all love data (don't we?), so here's a breakdown of what's going on here:

<div class="chart" id="chartdiv" style="width: 100%; height: 500px; margin-bottom: 20px;" ></div>

Well... that's me, I guess? Feel free to comment all over the site and complain about how reading this totally ruined your day.




<!-- amCharts javascript code -->
<script type="text/javascript">
	AmCharts.makeChart("chartdiv",
		{
			"type": "pie",
			"pathToImages": "http://cdn.amcharts.com/lib/3/images/",
			"balloonText": "Category: [[title]]<br><span style='font-size:14px'><b>[[value]] Posts</b> ([[percents]]%)</span>",
			"innerRadius": "40%",
			"minRadius": 100,
			"pullOutRadius": "15%",
			"startRadius": "30%",
			"colors": [
				"#69D2E7",
				"#A7DBD8",
				"#E0E4CC",
				"#F38630",
				"#FA6900",
				"#B0DE09",
				"#04D215",
				"#0D8ECF",
				"#0D52D1",
				"#2A0CD0",
				"#8A0CCF",
				"#CD0D74",
				"#754DEB",
				"#DDDDDD",
				"#999999",
				"#333333",
				"#000000",
				"#57032A",
				"#CA9726",
				"#990000",
				"#4B0C25"
			],
			"hoverAlpha": 0.74,
			"pullOutEffect": "elastic",
			"pullOutOnlyOne": true,
			"startEffect": "easeOutSine",
			"titleField": "category",
			"valueField": "number-of-posts",
			"allLabels": [],
			"balloon": {},
			"legend": {
				"align": "center",
				"markerType": "diamond",
				"switchable": false,
				"textClickEnabled": true,
				"useMarkerColorForLabels": true,
				"useMarkerColorForValues": true,
				"valueText": "[[value]] Posts"
			},
			"titles": [
				{
					"id": "Title-1",
					"text": "Number of Posts Breakdown"
				}
			],
      "dataProvider": [
{% assign tags_list = site.categories %}  
  {% if tags_list.first[0] == null %}
    {% for tag in tags_list %} 
        {
          "category": "{{ tag | capitalize }}",
          "number-of-posts": {{ site.tags[tag].size }}
        },
    {% endfor %}
  {% else %}
    {% for tag in tags_list %} 
        {
          "category": "{{ tag[0] | capitalize }}",
          "number-of-posts": {{ tag[1].size }}
        },
    {% endfor %}
  {% endif %}
{% assign tags_list = nil %}
      ]
    }
  );
</script>
