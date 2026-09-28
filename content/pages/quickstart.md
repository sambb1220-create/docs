<!DOCTYPE html>
<html>

<head>

<title>Storyteller RPG</title>

<link rel="stylesheet" href="style.css">

</head>


<body>


<div id="game">


<header>

<h1>🌎 Storyteller RPG</h1>

<p>
A limitless RPG where creativity shapes reality.
</p>

</header>



<section class="panel">

<h2>🎭 Game Mode</h2>

<select id="gameMode">

<option value="human">
Human GM
</option>

<option value="ai">
AI GM
</option>

</select>



<label>
Chaos Level
</label>

<input 
id="chaos"
type="range"
min="1"
max="100"
value="50"
>


</section>





<section class="panel">

<h2>🌍 World Creator</h2>


<input 
id="worldName"
placeholder="World Name"
>


<textarea
id="worldDescription"
placeholder="
Describe your world.

Example:
A fantasy world where magic is created from forgotten memories.
">
</textarea>



<textarea
id="worldConflict"
placeholder="
Main conflict.

Example:
An ancient empire is awakening.
">
</textarea>


</section>





<section class="panel">


<h2>🧙 Character Creator</h2>


<input
id="characterName"
placeholder="Character Name"
>


<textarea
id="characterDescription"
placeholder="
Who are you?

Example:
A monster creator who can summon living weapons.
">
</textarea>



<textarea
id="abilities"
placeholder="
Abilities and powers
">
</textarea>



<button id="startButton">
Begin Adventure
</button>



</section>







<section class="panel">


<h2>🎡 Fate Wheel</h2>


<div id="fateWheel">

🎡

</div>


<button id="spinButton">

Spin Fate

</button>



</section>







<section class="panel">


<h2>📖 Adventure</h2>



<div id="storyLog">

Your adventure awaits...

</div>



<textarea
id="playerAction"
placeholder="
What do you do?
">
</textarea>



<button id="actionButton">

Take Action

</button>



</section>








<section class="panel">


<h2>🗺️ World Database</h2>


<h3>Locations</h3>

<div id="locations">

No locations discovered.

</div>



<h3>🐉 Monsters</h3>


<div id="monsters">

No monsters discovered.

</div>



<h3>👥 NPCs</h3>


<div id="npcs">

No NPCs discovered.

</div>



</section>







<section class="panel">


<h2>💾 Save Files</h2>


<input
id="saveName"
placeholder="Save Slot Name"
>


<button id="saveButton">

Save

</button>



<div id="saveList">

</div>



</section>



</div>



<script src="game.js"></script>


</body>

</html>

/* Storyteller RPG Visual Style */

* {
    box-sizing: border-box;
}


body {

    margin: 0;
    min-height: 100vh;

    font-family:
    "Trebuchet MS",
    Arial,
    sans-serif;

    color: white;

    background:
    linear-gradient(
        135deg,
        #16102b,
        #050509
    );

}




#game {

    min-height: 100vh;

    padding: 25px;

    transition:
    background 1s ease;

}





header {

    text-align: center;

    margin-bottom: 25px;

}



header h1 {

    font-size: 42px;

    text-shadow:
    0 0 15px #8c6cff;

}



header p {

    opacity: .8;

}





.panel {

    max-width: 900px;

    margin:
    20px auto;

    padding: 20px;


    background:

    rgba(
    0,
    0,
    0,
    .55
    );


    border:

    1px solid

    rgba(
    255,
    255,
    255,
    .15
    );


    border-radius: 18px;


    box-shadow:

    0 0 20px
    rgba(
    0,
    0,
    0,
    .5
    );


    backdrop-filter:
    blur(8px);

}





h2 {

    margin-top: 0;

    color:
    #d8c8ff;

}





input,
textarea,
select,
button {


    width: 100%;


    padding: 13px;


    margin:
    8px 0;


    border-radius: 12px;


    border: none;


    font-size: 16px;


}




input,
textarea,
select {


    background:

    rgba(
    255,
    255,
    255,
    .1
    );


    color:white;


    outline:none;


}




textarea {

    min-height:110px;

    resize:vertical;

}




button {


    background:

    linear-gradient(
    135deg,
    #815cff,
    #4b2cff
    );


    color:white;


    cursor:pointer;


    font-weight:bold;


    transition:

    transform .2s,

    box-shadow .2s;


}




button:hover {


    transform:
    translateY(-2px);


    box-shadow:

    0 0 15px

    #815cff;


}





#fateWheel {


    height:150px;


    display:flex;


    justify-content:center;


    align-items:center;


    font-size:70px;


    transition:
    transform .8s;


}




.spin {


    animation:

    spinWheel 1s;


}



@keyframes spinWheel {


    from {

        transform:
        rotate(0deg);

    }


    to {

        transform:
        rotate(720deg);

    }


}







#storyLog {


    min-height:250px;


    padding:15px;


    border-radius:12px;


    background:

    rgba(
    0,
    0,
    0,
    .35
    );


    white-space:pre-wrap;


    line-height:1.5;


}





#locations,
#monsters,
#npcs,
#saveList {


    padding:15px;


    background:

    rgba(
    255,
    255,
    255,
    .05
    );


    border-radius:12px;


    min-height:50px;


}





.card {


    padding:12px;


    margin:10px 0;


    border-radius:12px;


    background:

    rgba(
    255,
    255,
    255,
    .08
    );


}





.success {

    color:
    #8cff9a;

}



.failure {

    color:
    #ff7777;

}



.legendary {

    color:
    #ffd86b;

}





@media(max-width:600px){


    #game {

        padding:10px;

    }


    header h1 {

        font-size:32px;

    }


    .panel {

        padding:15px;

    }


}

"use strict";


// ==========================
// Storyteller RPG Core Engine
// ==========================


let game = null;

let fateResult = null;

let isPlaying = false;



// HTML References

const gameMode =
document.getElementById("gameMode");

const chaos =
document.getElementById("chaos");


const worldName =
document.getElementById("worldName");

const worldDescription =
document.getElementById("worldDescription");

const worldConflict =
document.getElementById("worldConflict");


const characterName =
document.getElementById("characterName");

const characterDescription =
document.getElementById("characterDescription");

const abilities =
document.getElementById("abilities");


const storyLog =
document.getElementById("storyLog");


const playerAction =
document.getElementById("playerAction");


const fateWheel =
document.getElementById("fateWheel");


const locationsBox =
document.getElementById("locations");


const monstersBox =
document.getElementById("monsters");


const npcsBox =
document.getElementById("npcs");





// ==========================
// Start Game
// ==========================


document
.getElementById("startButton")
.onclick = () => {


game = {

    worldName:
    worldName.value ||
    "Unnamed World",


    description:
    worldDescription.value ||
    "A mysterious realm",


    conflict:
    worldConflict.value ||
    "Unknown danger",


    character:
    characterName.value ||
    "Traveler",


    characterDescription:
    characterDescription.value,


    abilities:
    abilities.value,


    history: [],


    locations: [],


    monsters: [],


    npcs: [],


    quests: []


};



isPlaying = true;


storyLog.innerText =

`
Welcome to ${game.worldName}.


${game.description}


Main Conflict:

${game.conflict}


${game.character} begins their adventure...
`;



changeBackground();

};






// ==========================
// Background Generator
// ==========================


function changeBackground(){


let text =
game.description.toLowerCase();



let background;



if(text.includes("space") ||
text.includes("galaxy")){


background =
"linear-gradient(#101040,#020208)";

}



else if(text.includes("ocean") ||
text.includes("sea")){


background =
"linear-gradient(#0077aa,#001522)";


}



else if(text.includes("forest") ||
text.includes("nature")){


background =
"linear-gradient(#075c22,#001000)";


}



else if(text.includes("dark") ||
text.includes("horror")){


background =
"linear-gradient(#400000,#050000)";


}



else{


background =
"linear-gradient(#604020,#090909)";


}



document
.getElementById("game")
.style.background =
background;


}






// ==========================
// Fate Wheel
// ==========================


document
.getElementById("spinButton")
.onclick = spinFate;



function spinFate(){


let roll =
Math.floor(Math.random()*100)+1;



if(roll <= 15){


fateResult =
"💀 Disaster";


}


else if(roll <=40){


fateResult =
"⚠ Failure";


}


else if(roll <=75){


fateResult =
"✨ Success";


}


else if(roll <=95){


fateResult =
"🌟 Great Success";


}


else{


fateResult =
"🔥 Legendary Success";


}



fateWheel.classList.add("spin");


setTimeout(()=>{


fateWheel.classList.remove("spin");


},1000);



fateWheel.innerText =
fateResult;


}






// ==========================
// Player Action
// ==========================


document
.getElementById("actionButton")
.onclick =
async()=>{


if(!isPlaying){

alert(
"Start a game first!"
);

return;

}



let action =
playerAction.value.trim();



if(!action)
return;



if(!fateResult){

spinFate();

}



game.history.push({

type:"player",

action:action,

result:fateResult

});




storyLog.innerText +=


`

\n\n${game.character}:

${action}


Fate:

${fateResult}

`;





// AI GM hook

if(gameMode.value==="ai"){


await askAI(action);


}


else{


storyLog.innerText +=


`

\nHuman GM mode:
The GM decides the outcome.

`;

}


playerAction.value="";


};







// ==========================
// AI Connection
// ==========================


async function askAI(action){


storyLog.innerText +=


`

\n\nAI GM:

Thinking...

`;



try{


let response =
await fetch(
"http://localhost:3000/story",
{


method:"POST",


headers:{

"Content-Type":
"application/json"

},


body:JSON.stringify({

worldName:
game.worldName,


world:
game.description,


problem:
game.conflict,


character:
game.character,


abilities:
game.abilities,


history:
game.history,


action:action,


fate:fateResult,


chaos:chaos.value


})


});




let data =
await response.json();




storyLog.innerText +=


`

${data.story}

`;



if(data.memory){

updateWorld(data.memory);

}



}

catch(error){


storyLog.innerText +=


`

AI GM ERROR:

Could not connect to server.

`;

console.error(error);


}



}








// ==========================
// World Memory Display
// ==========================


function updateWorld(memory){



if(memory.locations){


locationsBox.innerHTML="";


memory.locations.forEach(place=>{


locationsBox.innerHTML +=

`

<div class="card">

<h3>${place.name}</h3>

<p>
${place.type || ""}
</p>

</div>

`;

});


}





if(memory.monsters){


monstersBox.innerHTML="";


memory.monsters.forEach(monster=>{


monstersBox.innerHTML +=

`

<div class="card">

<h3>${monster.name}</h3>

<p>
${monster.type || ""}
</p>

</div>

`;

});


}





if(memory.npcs){


npcsBox.innerHTML="";


memory.npcs.forEach(npc=>{


npcsBox.innerHTML +=


`

<div class="card">

<h3>${npc.name}</h3>

<p>
${npc.personality || ""}
</p>

</div>

`;

});


}


}






// ==========================
// Save System
// ==========================


document
.getElementById("saveButton")
.onclick =
()=>{


if(!game)
return;



let name =
document
.getElementById("saveName")
.value
||
"Adventure";



localStorage.setItem(

"storyteller_"+
name,

JSON.stringify(game)

);



loadSaveList();


};






function loadSaveList(){


let list =
document.getElementById("saveList");


list.innerHTML="";



for(let i=0;i<localStorage.length;i++){


let key =
localStorage.key(i);



if(key.startsWith("storyteller_")){


let name =
key.replace(
"storyteller_",
""
);



list.innerHTML +=


`

<button onclick="loadGame('${name}')">

Load ${name}

</button>

`;



}


}


}




window.loadGame =
function(name){


let saved =
localStorage.getItem(
"storyteller_"+name
);



if(saved){


game =
JSON.parse(saved);



storyLog.innerText =

"Loaded "+game.worldName;


}


};




loadSaveList();
