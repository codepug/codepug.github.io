---
layout: home
title: Say the Weather on a Mac
permalink: /wiki/say-the-weather-on-a-mac
tag: misc
---

## Say the Weather on a Mac

If you've ever found yourself trapped inside working for a lengthy period of time, and curious about the weather outside, then this is the page for you.  On OS X Yosemite or above, the following script entered into the command console will speak the current weather.  

<code>
say The weather is `curl -A "Mozilla/5.0 (X11; CrOS armv7l 2913.260.0) AppleWebKit/537.11 (KHTML, like Gecko) Chrome/23.0.1271.99 Safari/537.11" -s 'https://www.google.com/search?as_q=weather' | grep -oE 'id=.?wob_tm[^<>]*>[^<>]+' | cut -d'>' -f2` degrees. 
</code>

Additionally, you can add the weather command in your terminal by creating an alias.  Edit your ~/.profile file and add the following to enable this.
<code>
alias weather='say The weather is `curl -A "Mozilla/5.0 (X11; CrOS armv7l 2913.260.0) AppleWebKit/537.11 (KHTML, like Gecko) Chrome/23.0.1271.99 Safari/537.11" -s "https://www.google.com/search?as_q=weather" | grep -oE "id=.?wob_tm[^<>]*>[^<>]+" | cut -d">" -f2` degrees. '
</code>

On top of the weather, a similar script can be used to get the latest movies that are out in theaters.
<code>
alias movie='curl -A "Mozilla/5.0 (X11; CrOS armv7l 2913.260.0) AppleWebKit/537.11 (KHTML, like Gecko) Chrome/23.0.1271.99 Safari/537.11" -s https://www.yahoo.com/movies/showtimes | grep \"movieCardTitle | cut -d">" -f2 | cut -d"<" -f1 | sort | uniq'
</code>