
FHIR is not a markup language. 
    It is a specification for how you might organize data using a markup language.
- JSON
- XML
It is not a database.
    It is a health data exchange format, and it may influence database design.
It is not a programming language.
    Many programming languages have libraries available to interact specifically with FHIR-formatted data, or at least to interact with the relevant markups such as XML or JSON. 
It is not software.
    Software can leverage the FHIR format to exchange healthcare information back and forth in a standardized, anticipatable way.
It is a specification / recommendation, and a standard for interoperability.

HIMSS (Healthcare Information and Management Systems Society) identifies 4 levels of interoperability:
1. Foundational (Level 1)
	   Foundational interoperability is the very basic level of connectedness between systems. It requires only that systems be able to exchange information, but not that that information be understandable in any way to each other.
		   Establishes the inter-connectivity requirements needed for one system or application to securely communicate data to and receive data from another.
		   Does not require the receiving system to be able to be able to interpret the data.
		   *Ex)* The transfer of a lab sample from one location to another. Or, electronically: transferring a PDF document that cannot be directly parsed on the receiving end.
2. Structural (Level 2)
	Defines the syntax of the data exchange. It ensures that data exchanges between information technology systems can be interpreted at the data field level.
	Does not imply an understanding at a meaningful level for interpretation or further use and relevant modification of the data between the two systems.
	*Ex)* An HTTP Request expecting a JSON response may receive JSON that does not contain the expected attributes. It can parse it, but it cannot understand it.
3. Semantic (Level 3)
	Provides for common underlying models and codification of the data including the use of data elements with standardized definitions from publicly available value sets and coding vocabularies, providing shared understanding and meaning to the user.
	Builds on Syntactic Interoperability by adding an additional layer of understanding of meaning behind the data structure.
	*Ex)* if the JSON from a minute ago is FHIR-formatted Patient data, then JavaScript expecting to see attributes like 'name' or 'id' won't be disappointed.
4. Organizational (New - Level 4)
	Includes governance, policy, social, legal and organizational considerations to facilitate the secure, seamless and timely communication and use of data both within and between organizations, entities and individuals. These components enable shared consent, trust and integrated end-user processes and workflows.
	- Similar policies regarding how to handle certain information. This could be policies regarding how to interpret data, respond to crises, etc.
    - Ability to either use similar standards and formats, or translate effectively in order to bridge gaps between different practices.
    - *ex)* The Police and Fire Department may respond to a fire differently, but should be aware of each other's protocol to work together efficiently.

FHIR-formatted data is made up of:
- Resources
- Fields with Values
- Identifiers
- Extensions
- Resource Bundles
- Compositions

Resources are the data packages used to send or receive data from a FHIR repository.

Examples: Medications, Diagnoses, Patients, Providers, Symptoms, and other discrete entities that define aspects of healthcare that have relationships within the larger structure of a healthcare data set.

Specification: [https://www.hl7.org/fhir/resourcelist.html](https://www.hl7.org/fhir/resourcelist.html)

Fields are discrete pieces of information about a resource. 

Examples: Name, Birthdate, Address, Medication Name, Dosage, Diagnosis.

Fields can have pre-defined allowable value sets (select one or more from a fixed list) or be free-text fields like address or name.

Fields can be references to specific entity identifiers, like Patient ID or Medication ID.

When this happens, we begin to see the relational nature of certain aspects of FHIR markup.

Identifiers are unique references to other resources in the data. They add relational capabilities to FHIR resources by allowing their attribute values to reference other resources.
- Unique, persistent references to other Resources in the data.
- Identifier values in a field assign the Identified Resource as the value
- Relational Database Equivalent: Foreign Keys

A very important characteristic of FHIR is that it is Extensible. What this means is that, in addition to the standard fields and types, developers can specify new fields and types to track new types of data, as long as they properly document and register these resources so that systems that access them know where to find human- and/or machine-readable information about how to use and interpret them.
Developers and Organizations can define their own properties and allowable values, and then use these properties as resource attributes.
- Define it
- Register it
- Use it

Define an Extension:
Requires detailed markup conforming to specifications that are laid out in the documentation.
Ex) [https://www.hl7.org/fhir/extension-patient-nationality.json.html](https://www.hl7.org/fhir/extension-patient-nationality.json.html)

Types of Resource Bundles
List
Dynamic: Items added and removed over time.
Example:
A patient's current medications
Group
Possibly editable, but less dynamically so.
Examples:
Patients in a clinical trial
Animals with certain characteristics
Medicines of a certain type
Composition
Logical Document
General basis for a FHIR Document

We can use SMART on FHIR's JavaScript tools to interact with a FHIR API directly:
[http://docs.smarthealthit.org/client-js/](http://docs.smarthealthit.org/client-js/)

Here is the URL for the FHIR Client CDN (Content Delivery Network). You would include this URL as the 'src' in a script tag to make the tools available:
https://cdn.jsdelivr.net/npm/fhirclient/build/fhir-client.js

SMART Health IT provides a demo API that doesn't require a real key:
[https://r3.smarthealthit.org](https://r3.smarthealthit.org)

```
/*

NOTE: Certain operations like Update and Create seem so take a little while to "kick in" on the server.

They may be performing basic validation to prevent abuse/obscenity.

When you add or edit something, don't be thrown off be errors when searching for those names again for a few minutes.

Usually it will resolve within a few minutes.

*/

  

const client = FHIR.client("https://r3.smarthealthit.org");


//// CREATE:

  

function addPatient() {

//// Let's prompt the user for the pieces of info that we want to store about our new patient:

var firstname = prompt("First name?");

var lastname = prompt("Last name?");

//// Let's create a minimal object structured the way a FHIR Patient resource would be structured:

var patient = {

"resourceType": "Patient",

"name": {

"given": [firstname],

"family": lastname

},

}

client.create(patient).then(function(x) {

addPatientRow(x);

});

//// Or even this works:

//client.create(patient).then(addPatientRow);

}

  
  

//// 'patient' Starts at data.entry[d].resource level in the data that client.request returns

function addPatientRow(patient) {

//// Get a reference to patientResults tbody

var patientResults = document.querySelector("#patientResults");

//// Build a new table row (tr):

var tr = document.createElement("tr");

//// Create a table data cell (td)

var td = document.createElement("td");

//// Fill it with our first piece of info, which is our patient's first given name (first element in the 'given' array under the 'name' property's first entry)

td.innerHTML = patient.id;

tr.appendChild(td);

//// Create a table data cell (td)

var td = document.createElement("td");

//// Fill it with our first piece of info, which is our patient's first given name (first element in the 'given' array under the 'name' property's first entry)

td.innerHTML = patient.name[0].given[0];

tr.appendChild(td);

var td = document.createElement("td");

td.innerHTML = patient.name[0].family;

tr.appendChild(td);

var td = document.createElement("td");

var btn = document.createElement("button");

btn.innerHTML = "[X]";

//// You can use <function>.bind({object}) to bind values to a function when attaching it to a listener like this. That way you make sure to maintain proper references.

//// We want to make sure that LATER, when we CALL the function by clicking the button (when we're not in this loop anymore), that it still knows what the right patient/data/etc is:

btn.onclick = deletePatient

.bind({patient_id:patient.id, row:tr});

//// Compare to this, where the ID will repeat incorrectly:

//btn.onclick = function() {

// deletePatient(data.entry[d].resource.id);

//}

td.appendChild(btn);

var btn = document.createElement("button");

btn.innerHTML = "[Edit]";

btn.onclick = updatePatient.bind({patient:patient, row:tr});

td.appendChild(btn);

tr.appendChild(td);

//// Append that table row (tr) to my patientResults tbody

patientResults.appendChild(tr);

}

  
  
  
  

//// READ

  

function showPatients() {

//// Basically doing this:

//// https://r3.smarthealthit.org/Patient?name=...

//// Keep in mind when displaying patients that this service seems to be caching requests and only refreshing every once in a while. Your changes me not immediately be apparent.

var n = prompt("Name to search:");

//if (confirm("Are you sure you want to pop up that name?")) {

// alert(lastname);

//}

client.request("Patient?name="+n)

.then(handlePatients)

.catch(console.error)

;

}

  

function handlePatients(data) {

//// Creating a reference to our tbody in our HTML so I can do things to change the content:

var patientResults = document.querySelector("#patientResults");

//// Clear the content by clearing out the innerHTML of our tbody

patientResults.innerHTML = "";

console.log(data);

//return;

//// Check to make sure 'entry' even exists as a property in our data, because that's where our array of patient results will be:

if (data.entry) {

//// Then loop through it using a for-loop:

for (var d=0; d<data.entry.length; d++) {

//// Sometimes the API takes a bit to process everything. Let's just have a try/catch around this to avoid complications:

//try {

//// Here I'm calling another function that I will write to VISUALLY insert a row into my table. I'm doing this as a separate function so that I don't have to write all of the lines of code everywhere else that I want to use them.

addPatientRow(data.entry[d].resource);

//} catch(error) {

// console.log("Skipped a patient row due to incomplete data.");

//}

}

}

}

  
  
  
  
  
  

//// UPDATE

function updatePatient() {

var firstname = prompt("First name?", this.patient.name[0].given[0]);

if (!firstname) { return; }

var lastname = prompt("Last name?", this.patient.name[0].family);

if (!lastname) { return; }

client.patch("Patient/"+this.patient.id, [

{ op: "replace", path: "/name/0/given/0", value: firstname }

,

{ op: "replace", path: "/name/0/family", value: lastname }

]).then(function(updatedPatient) {

addPatientRow(updatedPatient);

});

this.row.parentNode.removeChild(this.row);

}

  
  
  

//// DELETE

//function deletePatient(patient_id) {

// console.log(patient_id);

//}

function deletePatient() {

//// Because of our binding in addPatientRow below, we now know that we will have a 'patient_id' property and a 'row' property. 'row' will refer to the TR (table row) in the DOM that contains this particular patient record

if (confirm("Are you sure you want to delete this patient?")) {

//// Whenever you 'bind' things to a function and run it, those variables are available as properties of the 'this' object

client.delete("Patient/"+this.patient_id);

//// Have the parent of the row we passed in remove the row from itself:

this.row.parentNode.removeChild(this.row);

//// Alternatively, we COULD have just re-read the entire set of results, but then we'd have to pass in the proper name search again, etc.

}

}
```

### **Purpose of `.bind()`**
![[Pasted image 20251212101326.png]]

```
  

// Layer group to manage markers

const markerLayer = L.layerGroup().addTo(map);

  

// Event: filter change

typeSelect.addEventListener("change", loadLocations);

  

// Initial load

loadLocations();

  

/**

* Load locations from FHIR server

*/

function loadLocations() {

markerLayer.clearLayers();

  

const typeCode = typeSelect.value;

  

let query = "Location";

  

// Optional filtering by type

if (typeCode) {

query += `?type=${typeCode}`;

}

  

client.request(query)

.then(renderLocations)

.catch(console.error);

}

  

/**

* Render location markers

*/

function renderLocations(data) {

if (!data.entry) return;

  

data.entry.forEach(entry => {

const location = entry.resource;

  

// Ensure lat/lng exists

if (!location.position) return;

  

const lat = location.position.latitude;

const lng = location.position.longitude;

  

if (lat == null || lng == null) return;

  

// Tooltip (hover)

const tooltipText =

location.name || "Unnamed Location";

  

// Popup (click)

const popupHTML = `

<strong>${location.name || "Unnamed Location"}</strong><br>

${formatAddress(location.address)}<br>

<em>${location.type?.[0]?.coding?.[0]?.display || ""}</em>

`;

  

const marker = L.marker([lat, lng])

.bindTooltip(tooltipText)

.bindPopup(popupHTML);

  

markerLayer.addLayer(marker);

});

}

  

// Format address safely

function formatAddress(address) {

if (!address) return "No address available";

  

const lines = [];

  

if (address.line) lines.push(address.line.join(", "));

if (address.city) lines.push(address.city);

if (address.state) lines.push(address.state);

if (address.postalCode) lines.push(address.postalCode);

  

return lines.join(", ");

}
```


```
/*

* - Query FHIR Location resources from the SMART demo server

* - Display them as markers on a Leaflet map

* - Show a tooltip on hover

* - Show a detailed popup on click

*/

  

// Create FHIR client. Connect to the SMART Health IT demo FHIR server.

const client = FHIR.client("https://r3.smarthealthit.org");

  

// DOM

const typeSelect = document.querySelector("#typeSelect");

  

// Initialize Leaflet map

const map = L.map("map").setView(

[39.5, -98.35], // US-centered view

4 //Zoom level

);

  

// Map OpenStreetMap tiles as the base layer

L.tileLayer("https://tile.openstreetmap.org/{z}/{x}/{y}.png", {

maxZoom: 18,

attribution: "&copy; OpenStreetMap contributors"

}).addTo(map);

  

// Store markers so we can remove them later

let markers = [];

  

// Store all locations once

let allLocations = [];

  

// Load/fetch location data from FHIR API

/* client.request("Location")

.then(displayLocations)

.catch(console.error); */

// above renders the locations immediately. below stores it first.

client.request("Location")

.then(bundle => {

if (!bundle.entry) return;

  

allLocations = bundle.entry.map(e => e.resource);

  

populateTypeFilter(allLocations);

displayLocations(allLocations);

})

.catch(console.error);

  
  

function displayLocations(bundle) {

// FHIR search responses return a Bundle

// Actual resources are in bundle.entry[]

if (!bundle.entry) {

console.warn("No Location data returned");

return;

}

  

bundle.entry.forEach(entry => {

const location = entry.resource; // Each entry.resource is a location

  

// Only plot locations that have coordinates

if (!location.position) return;

  

const lat = location.position.latitude;

const lng = location.position.longitude;

  

// Create a Leaflet marker, converts FHIT geographic data to map markers.

const marker = L.marker([lat, lng]).addTo(map);

  

// Tooltip: shown when hovering over marker

marker.bindTooltip(

location.name || "Unnamed Location",

{ direction: "top" }

);

  

// Popup: shown when marker is clicked

marker.bindPopup(popupContent(location));

  

// UX: zoom and center when clicked

marker.on("click", function () {

map.setView(this.getLatLng(), 8);

});

});

}

  

// Build popup content

  

function popupContent(location) {

// Safely extract optional fields

const name = location.name || "Unnamed Location";

  

const address = location.address

? `

${location.address.line?.join(", ") || ""}<br/>

${location.address.city || ""},

${location.address.state || ""}

`

: "Address not available";

  

const type = location.type?.[0]?.coding?.[0]?.display

|| "Unknown type";

  

// Return HTML string for popup

return `

<strong>${name}</strong><br/>

<em>${type}</em><br/><br/>

${address}

`;

}
```