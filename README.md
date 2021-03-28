[![GitHub license](https://img.shields.io/github/license/ethanny2/threejs-webpack-boiler-staticsite)](https://github.com/ethanny2/threejs-webpack-boiler-staticsite)[![GitHub stars](https://img.shields.io/github/stars/ethanny2/threejs-webpack-boiler-staticsite)](https://github.com/ethanny2/threejs-webpack-boiler-staticsite/stargazers)[![GitHub forks](https://img.shields.io/github/forks/ethanny2/threejs-webpack-boiler-staticsite)](https://github.com/ethanny2/threejs-webpack-boiler-staticsite/network)[![Twitter Badge](https://img.shields.io/badge/chat-twitter-blue.svg)](https://twitter.com/ArrayLikeObj)

# Retro Fansite Scrape Backend

## [https://unofficial-playboicarti.netlify.app/](https://unofficial-playboicarti.netlify.app/)

<p align="center">
  <img src="https://media1.giphy.com/media/5HkeQBxSf4jC1iq7h8/giphy.gif" alt="Demo gif">
</p>


## Background
This is a simple PHP backend made to scrape the most recent photo or video from a specified Instagram account that is public and send it back a JSON to a front-end. Because you cannot scrape photos directly from Instagram I chose to instead scrape another site, ( [Gramho](https://gramho.com/) ) that already scrapes Instagram and makes the links publicly available/viewable without logging in. 

The content is pulled from the offical [Artist's account](https://www.instagram.com/playboicarti/).

## Technology used
- PHP
- Scraping Web content with PHP + String Manipulation (no libraries)
- encoding JSON data
  
## Concepts

### Web Scraping with PHP

As long as a server-side language has the ability to parse a URL as the returned HTML you can use that language to scrape the web for data. In the case of PHP this done with **file_get_contents()**
```
$output = file_get_contents($url);

/* 
  Afterwards you study the HTML pattern and determine where to split the string
  and get the <img> or <video> tag
*/

//If there is a <div class="single-photo"> inside is a video</div>
//If there is a <div class="item"> inside is an img</div>
$videoStart='<div class="single-photo">';
$videoEnd = '</div>';
$isVideo = fetchdata($page,$videoStart,$videoEnd);
if(empty($isVideo)){
  $photoStart='<div class="item">';
	$photoEnd = '</div>';
	$photo = fetchdata($page,$photoStart,$photoEnd);
	echo json_encode(array('pic'=>$photo));
	}else {
	  echo json_encode(array('vid'=>$isVideo));
	}
}

```
