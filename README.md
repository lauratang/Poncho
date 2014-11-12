Poncho
======
<!Doctype html>
<html>
<head>
<meta charset=utf-8"/>
<title>Clothing Forecast</title>
</head>
<body>

<h1><center>Test</center></h1>

<p id = "temp0"></p>
<p id = "temp2"></p>
<p id = "temp1"></p>

<script language="javascript" type="text/javascript">

// VARIABLES
var temp = 60;
var lowtemp = 42;
var windmph = 3;
var wind; // super windy, windy, breezy, calm depending on mph
var windchill;
//WINDCHILL - FEELS LIKE?
var precip = "no precipitation";
// no precipitation, light rain, heavy rain, light snow, heavy snow
var precipTime = "none";
// none, allDay, morning, afternoon, evening
var variability;
var cloudcover = "partlycloudy";
// sunny, partlycloudy, cloudy
var hail = false;

if (temp-lowtemp>=12) {
	variability = "high";
} else if (temp-lowtemp>7 && temp-lowtemp<12) {
	variability = "medium";
} else variability = "low";

if (windmph>=27) {
	wind = "super windy";
} else if (windmph>=20 && windmph<27) {
	wind = "windy";
} else if (windmph>=15 && windmph<20) {
	wind = "breezy";
} else wind = "calm";

// VARIBLES FOR DATE IF NEEDED?
var today = new Date((new Date()).setHours(0,0,0,0));
var month = today.getMonth()+1;
var date = today.getDate();

// TEMPERATURE METHOD
function firstLayer(temp) {
	if (temp>=80) return 'tank top';
	else if (temp>=70 && temp <80) return 'tank top';
	else if (temp>=65 && temp <70) return 'short sleeve top';
	else if (temp>=60 && temp <65) return 'short sleeve top';
	else if (temp>=55 && temp <60) return 'short or long sleeve top';
	else if (temp>=50 && temp <55) return 'long sleeve top';
	else if (temp>=40 && temp <50) return 'long sleeve top';
	else if (temp>=30 && temp <40) return 'sweater';
	else if (temp>=20 && temp <40) return 'cozy sweater';
	else if (temp>=10 && temp <20) return 'cozy sweater';
	else return 'warmest sweater you own';
}
function secondLayer(temp) {
	if (temp>=80) return 'long-sleeve';
	else if (temp>=65 && temp <80) return 'sweater or cardigan';
	else if (temp>=60 && temp <65) return 'sweater or light jacket';
	else if (temp>=55 && temp <60) return 'jacket';
	else if (temp>=50 && temp <55) return 'thicker jacket';
	else if (temp>=40 && temp <50) return 'coat';
	else if (temp>=30 && temp <40) return 'winter coat or parka';
	else if (temp>=20 && temp <30) return 'winter coat';
	else if (temp>=10 && temp <20) return 'heavy winter coat';
	else if (temp>=0 && temp <10) return 'heavy winter coat. Grab a hat and gloves';
	else return 'heavy winter coat and a hat and gloves';
}

/*  
*
* PRINTOUT BELOW
*
*/

// MAIN MESSAGE (WEATHER)
document.getElementById("temp0").innerHTML = 
	"High of " + temp + " with " + precip + " and " +
	variability + " variability.";


/* SECONDARY MESSAGE (CLOTHING BY IMPORTANCE)
   MESSAGES LATER WILL OVERRIDE MESSAGES FURTHER
   IF CONDITIONS ARE MET */
// Messages that write into temp1 replace the original
// Messages that write into temp2 add a sentence.

// CLEAR, LOW VARIABILITY
if (!(temp<20)) {
	if (temp<75 && cloudcover==='sunny') {
		document.getElementById("temp1").innerHTML =
		"Wear a " + secondLayer(temp) +
		" on this clear day.";
	} else if ((temp<75 && cloudcover==='cloudy') || (temp<75 && cloudcover==='partlycloudy')) {
		document.getElementById("temp1").innerHTML =
		"Wear a " + secondLayer(temp) +
		" on this cloudy day.";
	} else if (temp>=75 && cloudcover==='sunny') {
		document.getElementById("temp1").innerHTML =
		"Short sleeves (or no sleeves!) with shorts and sandals. Don't forget your sunglasses B)";
	} else {
		document.getElementById("temp1").innerHTML =
		"Short sleeves (or no sleeves!) with shorts and sandals.";
	}
} else {
	document.getElementById("temp1").innerHTML = 
	"Keep warm with a " +secondLayer(temp)+ " today.";
}

// VARIABILITY
if (variability==='high' && (temp>40) && (temp<70)) {
	document.getElementById("temp1").innerHTML =
	"Make sure to layer with a "
	+ secondLayer(temp) + ". You'll be facing a cooler morning but it'll heat up later.";
}
if (variability==='medium' && (temp>30) && (temp<75)) {
	document.getElementById("temp1").innerHTML =
	"Make sure to layer with a "
	+ secondLayer(temp) + " because it'll get a bit warmer throughout the day.";
}

// WIND
if ((wind==='super windy') && (temp<75)) {
	document.getElementById("temp1").innerHTML =
	"Don't get blown away!! Wear a windbreaker or otherwise wind-proof your outfit.";
}
if ((wind==='windy') && (temp<65)) {
	document.getElementById("temp1").innerHTML =
	"Be sure to wear a windbreaker or otherwise wind-proof your outfit.";
}
if (wind==='breezy' && (temp<80)) {
	document.getElementById("temp1").innerHTML =
	"Prepare for a breeze with a " + secondLayer(temp) + " and jeans.";
}

// PRECIPITATION
if (precip==='light rain') {
	if (precipTime==='morning' || precipTime==='afternoon' || precipTime==='evening') {
		document.getElementById("temp2").innerHTML =
		"Bring an umbrella if you'll be outside in the " + precipTime + ".";
		if (temp>=75) {
		document.getElementById("temp1").innerHTML =
		"Short sleeves (or no sleeves!) today with shorts and shoes that you don't mind getting wet.";
		}
		if (temp<75) {
		document.getElementById("temp1").innerHTML =
		"Wear a " + secondLayer(temp) + " and shoes that you don't mind getting wet.";
		}
	}
	if ((precipTime==='allDay' && !(wind==='windy')) || (precipTime==='allDay' && !(wind==='super windy'))) {
		document.getElementById("temp1").innerHTML =
		"Rain jacket recommended on this drizzly day. Wear over a " + firstLayer(temp) +
		" and pair with rain boots or water-proof shoes.";
	}
	if ((precipTime==='allDay' && wind==='windy') || (precipTime==='allDay' && wind==='super windy')) {
		document.getElementById("temp1").innerHTML =
		"Drizzly and windy. Wear a wind-proof rain jacket over a " + firstLayer(temp) +
		" and pair with rain boots or water-proof shoes.";
	}

}
if (precip==='heavy rain' && temp<70) {
	document.getElementById("temp1").innerHTML =
	"Heavy rain expected: raincoats, rain boots and umbrellas are essential today.";
	if (precipTime==='morning' || precipTime==='afternoon' || precipTime==='evening') {
		document.getElementById("temp1").innerHTML =
		"Heavy rain expected in the " + precipTime + ": rain jackets, rain boots and umbrellas are essential today.";
	}
}
if (precip==='heavy rain' && temp>70) {
		document.getElementById("temp2").innerHTML =
		"Heavy rain expected in the " + precipTime + ": bring an umbrella if you'll be out then.";
	}

if (precip==='light snow') {
	document.getElementById("temp1").innerHTML =
	"You'll want a winter jacket and a hat for today.";
	if (wind==='windy' || wind==='super windy') {
	document.getElementById("temp1").innerHTML =
	"Today's going to be windy and snowy! You'll want a winter jacket, a hat and a scarf.";
	}
}
if (precip==='heavy snow') {
	document.getElementById("temp1").innerHTML =
	"Let it snow! If you're going out today, be sure " + 
	"to wear your winter coat, sturdy boots, hat, and gloves to keep warm.";
	if (wind==='windy' || wind==='super windy') {
	document.getElementById("temp1").innerHTML =
	"With gusty winds and heavy snow, you'll definitely want a thick winter coat and " + firstLayer(temp) + " today. Bring out all your winter flair: hat, gloves, scarf, snow boots.";
	}
}
if (temp<0) {
	document.getElementById("temp1").innerHTML =
	"Today's going to be SO cold that you might as well just wear your sleeping bag to work.";
}
if (temp>95) {
	document.getElementById("temp1").innerHTML =
	"Wear as little clothing as possible.";
}
if (hail===true) {
	document.getElementById("temp2").innerHTML =
	"Take cover, ice cubes are falling from the sky today.";
}
//ADD HALLOWEEN: WEAR COSTUME, NEW YEARS: WEAR PARTY HAT AND BRING NOISEMAKERS, CHRISTMAS: HOLIDAY SWEATER AND SANTA HAT, ST PATTY'S DAY: GREEN

</script>


<body>
</body>
</html>
