# Cub3D ~

### ~ a 42 School graphics project. Grade : 110/100.
<img align="center" src="wad/screenshot.png" alt="Screenshot of the graphics generated by this game engine"/>
Here it is, with textures sourced from Doom WADs, credit to id Software for these beauties.

## Goal	
#### Taking at stab at a raycasting engine.
Because a far fetched notion of what it takes to be a "proper" engineer apparently involves agonizing over some maths... or at least be able to get them to work for your problems.

## Usage
- Switch to macOS-evaluated or linux-dev branch accordingly to your OS.
  - On linux-dev branch, update the libft submodule.
- Compile using make
- ./cub3D [map path]

There are some map files inside the /maps folder, you can modify those using a text editor.

Some xpm textures are stored inside the /wad folder. You can replace or modify those as well.

## Constraints ~
No OpenGL, no SDL... just a spartan homebrewed graphics lib from 42 school with rudimentary window and events management... and the ability to print a single pixel to a screen or a buffer.

## Interest ~
Injecting some trigonometry to what was once a great applied IT cursus to meet governmental requirements for engineering degrees... and probably the subsidies they entitle.

As a former student of the history of technology, I was more enthusiastic about the potential for this project as an historical experiment. Putting ourselves in the shoes of Carmack and Romero, and as the former, using the state of the art in scholarly mathematics to display 3D graphics with 2D calculations.

A lesson in craftiness, sobriety and optimisation... also Doom was my first video game so it was exciting to get a peek under its hood !

## Technique ~
Vectorial 2D DDA raycasting, as featured in lodev's ubiquital reference on the subject (https://lodev.org/cgtutor/raycasting.html).

As I have a mental block on mathematics and lack culture on the matter as well, I felt the elemental logic of vectors much more concrete and approachable than the lingo laden angle calculations of some other methods (https://www.youtube.com/watch?v=eOCQfxRQ2pY).

## Implementation ~
Parsing of the map is done in a 1D array, thanks to some homespun data structures, and my own implementation of a vector data structure in C. Thus, a single malloc is needed for the whole map to be parsed, smoothing up memory management, and allowing us to greatly benefit from the processor cache.

The different map tiles are coded by an enum, including the space outside the map.

Access to the map tiles is solely done through a dedicated function which returns an OUTS enum identifier if we get out of bounds, strictly preventing illegal memory accesses.

I never did object oriented programming before, but I'm starting to see its appeal through the many structures I had to devise during this project. A homespun bottom up, "proto-class" is even found in the array of function pointers used to parse the configuration ".cub" file. This array is made from a structure comprising the function pointer necessary to parse some parameter next to a void* ready to hold its retrieved data.

## Bonuses ~
#### Collisions
Easily implemented thanks to the design choices explained above. Also seemed the easiest way to avoid segmentation faults from the get go.

#### Minimap
A breeze thanks to the scaling calculations used earlier in the "so_long" project (a 2D, top down maze game) and a nifty design choice : I chose to round the actual position of the camera (a 2D float vector) to a 2D int vector thanks to some casts.

The position of the player is then reduced to the map tile he is currently in, but it saved me from additional calculations. It is certainly rudimentary, but plenty functional to navigate this "game". Moreover it turns out to be useful for debugging collisions, and super cute as well!
