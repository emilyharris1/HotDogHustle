Hot Dog Hustle is an interactive Processing game connected to an Arduino-based input system. Players physically squeeze ketchup and mustard bottles (each with pressure sensors) to match condiment orders on a moving hot dog. The project evolved significantly across four versions. Each iteration focused on improving usability, gameplay clarity, visual design, and sensor responsiveness.

Version 1 - Basic Functionality & Proof of Concept

Goals
* Read sensor values from Arduino.
* Move a hot dog across the screen.
* Map sensor input to ketchup and mustard levels.
* Generate random food orders.
* Score the player's accuracy.
  
Main Features
* Serial Input: First implementation of Serial.list()[2] and parsing ketchup, mustard.
* Hotdog Movement: Hotdog moves left to right using hotdogX += hotdogSpeed.
* Condiment Bars: Ketchup and mustard appear as horizontal colored bars.
* Basic Orders: Only ketchup, only mustard, or mixed.
* Simple Scoring: Based on total difference between target and actual levels.
* UI: Text-based start screen, minimal graphics.

Limitations
* Condiment bars did not visually match the hotdog.
* Bottles were not yet implemented.
* Gameplay lacked feedback (no animation).
* Orders felt inconsistent.
* Game speed was slow and visually plain.

What I Learned
I learned how to get the sensor readings working and established the core gameplay loop. It gave me a base to build upon before focusing on graphics and polish.

Version 2 - Visual Refinements & Bottle Animation

Goals
* Add actual ketchup and mustard bottle graphics.
* Move toward a more polished, engaging look.
* Better alignment of condiments with the hotdog.

Major Improvements
* Bottle Images: Added ketchup and mustard bottle images.
* Condiment Streams: Replaced bar-only visualization with vertical red/yellow lines under the bottles.
* Tabletop Background: Improved theme coherence with a background table.
* Updated Order & Score Bar: Black banner at the top to cleanly display game info.
* Fixed Hotdog Rotation: Made it consistently angle 25 degrees.
* Fonts + Branding: Introduced SportPulse + Lato fonts and a hotdog-themed start screen.

Gameplay Adjustments
* Threshold for squeezing set to >20 instead of >30.
* Condiments constrained to 120 max.
* Bottle positions defined by ketchupOffsetX, mustardOffsetX, and bottleOffsetY instead of hard coding.

Issues Still Present
* Condiment streams were still vertical lines, not following the hotdog.
* Hotdog moved slowly.
* No on-screen feedback when scoring.

What I Learned
This version focused on graphic identity and better visual mapping. I learned how to position rotated objects, use imageMode(CENTER), and synchronize multiple animated assets.

Version 3 - Scoring Feedback, Popups, and Smoother Flow

Goals
* Improve gameplay feel and responsiveness.
* Add animated point popups.
* Introduce equal mix order.
* Increase game speed and difficulty.

Major Improvements
* Popup Animation: Points float upward and fade out over 2 seconds.
* Game Speed: Increased base speed (+ speed increment per round).
* Scoring Logic:
    * Added support for orders like Equal mix, Light ketchup, Heavy mustard, etc.
    * Introduced equalMixOrder boolean for special evaluation.
* Threshold Changes: Squeezing now triggers when sensors exceed value 3, making the game goals more obtainable/possible.
* Cleaned-Up Bars: Thinner and cleaner condiment bars.

Visual Upgrades
* Bottle sizes enlarged for emphasis.
* Bottle drip distance increased.
* Hotdog image enlarged to 300×150 for better visibility.
* Popup system color-coded.

Structural Improvements
* Consolidated bottle drawing in drawBottles().

Remaining Issues
* Condiment is still drawn as bars/lines-not dots following the hotdog.
* Condiment still didn’t travel with the hotdog realistically.
* Game still lacked curve-shaped ketchup/mustard trails.

What I Learned
This version transformed the game from functional to playable and rewarding. I learned how to animate fading UI, implement conditional scoring, and tune difficulty pacing.

Version 4 - Dots, Wavy Trajectories, Accurate Placement, Better Orders

Goals
* Make the condiments look realistic and visually follow the hotdog.
* Use wavy lines of dots instead of bars.
* Add more specific orders (plain dog, equal mix, light/heavy variations).
* Improve scoring fairness.
* Improve visual polish.

Major Technical Enhancements
* Condiment Dots System:
    * Added dynamic ArrayLists (mustardDots, ketchupDots).
    * Each dot stores an x-offset and y-position.
* Wavy Path Animation:
    * Used sin() with independent phase, amplitude, and step values for ketchup and mustard.
    * Created visually appealing left/right wavy squiggles.
* Dot Maximum Distance: Added bounds (mustardMaxX, ketchupMaxX) to stop dots at the end of the dog.

Gameplay Refinements
* More specific order types:
    * Heavy ketchup
    * Heavy mustard
    * Light/heavy mixed combinations
    * Equal mix
    * Plain hot dog 
* Scoring logic refined to use tolerance windows (±25 = perfect, ±50 = ok).
* Penalty for being completely wrong (-2 points).
* More lenient scoring.

Visual Polish
* Better bottle offsets.
* Improved start and pause screens.
* Added more images.

Technical Improvements
* Cleaned reset logic in newOrder().
* Ensured all dots reset each round.
* Improved Arduino serial parsing to assign mustard/ketchup correctly.

What I Learned
This version taught me how to use lists of dynamic particles, animation timing, sine-wave motion, and more advanced visual alignment. It also completed the vision of the project: an interactive, polished game that visually reacts to real-world squeezes.

During the final stretch of the project, I ran into an unexpected wiring issue that caused the game to work only some of the time during the demo. Even after double-checking the circuit layout and reviewing my Arduino + Processing code, the problem kept showing up in new, inconsistent ways that were different from the issues I had already solved earlier in the process.

What I learned from this experience is that last-minute hardware problems are rarely about one obvious mistake. They often come from small things that add up: a loose jumper wire, a sensor not fully seated, or a connection that works until the board gets bumped. Going through this forced me to slow down, test each part individually, and think more systematically about debugging instead of assuming I knew where the problem was. It also reminded me that building anything with physical components needs extra buffer time for troubleshooting, because even well-designed circuits can behave unpredictably under pressure.

If I had more time, I would redesign the wiring to be more stable, most likely by switching from loose jumper wires on a breadboard to soldered connections or at least more secure connectors. I’d also label my wires better, build in more structured testing points, and run longer stress tests to make sure the system holds up when people interact with it. 

Overall, the inconsistent performance was frustrating, but it taught me a lot about reliability, preparation, and the importance of building hardware that can survive real-world use, not just ideal conditions.
