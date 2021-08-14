// Write your JavaScript code here!
window.addEventListener("load", function(){

   document.addEventListener("submit", function(event){
      event.preventDefault();
      const launchStatus = document.getElementById("launchStatus");

      const pName = document.querySelector("input[name=pilotName]");
      const cPName = document.querySelector("input[name=copilotName]")
      const fuel = document.querySelector("input[name=fuelLevel]")
      const mass = document.querySelector("input[name=cargoMass]")
      let inputOK = false;

      if (pName.value === ""){
         alert("All fields are required!");
         event.preventDefault();
      } else if (!isNaN(pName.value) || typeof pName.value !== "string"){
         alert("Make sure to enter valid information for each field!");
         event.preventDefault();
      } else if (cPName.value === ""){
         alert("All fields are required!");
         event.preventDefault();
      } else if (!isNaN(cPName.value) || typeof cPName.value !== "string"){
         alert("Make sure to enter valid information for each field!");
         event.preventDefault();
      } else if (fuel.value === ""){
         alert("All fields are required!");
         event.preventDefault();
      } else if (isNaN(fuel.value)){
         alert("Make sure to enter valid information for each field!");
         event.preventDefault();
      } else if (mass.value === ""){
         alert("All fields are required!");
         event.preventDefault();
      } else if (isNaN(mass.value)){
         alert("Make sure to enter valid information for each field!");
         event.preventDefault();
      } else {
         inputOK = true;
      }

      const faultyItems = document.getElementById("faultyItems");

      const pilotStatus = document.getElementById("pilotStatus")
      pilotStatus.innerHTML = `Pilot Ready (${pName.value})`;

      const copilotStatus = document.getElementById("copilotStatus")
      copilotStatus.innerHTML = `Co-pilot Ready (${cPName.value})`;

      const fuelStatus = document.getElementById("fuelStatus");
      const cargoStatus = document.getElementById("cargoStatus");
      let fuelOK = true;
      let cargoOK = true;

      if (fuel.value< 10000){
         fuelStatus.innerHTML = "Not enough fuel for launch";
         faultyItems.style.visibility = "visible";
         launchStatus.innerHTML = "Shuttle not ready for launch";
         launchStatus.style.color = "red";
         fuelOK = false;
      }

      if (mass.value > 10000){
         cargoStatus.innerHTML = "Too much mass for the shuttle to take off";
         faultyItems.style.visibility = "visible";
         launchStatus.innerHTML = "Shuttle not ready for launch";
         launchStatus.style.color = "red";
         cargoOK = false;
      }

      if(!inputOK){
         launchStatus.innerHTML = "Shuttle not ready for launch";
         launchStatus.style.color = "red";
      }

      if(cargoOK && fuelOK && inputOK) {
         launchStatus.innerHTML = "Shuttle is ready for launch";
         launchStatus.style.color = "green";
         faultyItems.style.visibility = "hidden";
      }
   })
})

/* This block of code shows how to format the HTML once you fetch some planetary JSON!*/
window.addEventListener("load", function(){
   fetch("https://handlers.education.launchcode.org/static/planets.json").then(function(response){
      response.json().then(function(json){
         let r = Math.floor(Math.random()*json.length);
         const mission = document.getElementById("missionTarget");
         mission.innerHTML=`
         <h2>Mission Destination</h2>
         <ol>
            <li>Name: ${json[r].name}</li>
            <li>Diameter: ${json[r].diameter}</li>
            <li>Star: ${json[r].star}</li>
            <li>Distance from Earth: ${json[r].distance}</li>
            <li>Number of Moons: ${json[r].moons}</li>
         </ol>
         <img src="${json[r].image}"></img>
         `
      })
   }
   )
})
