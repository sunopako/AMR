## AMR — Autistic Movie Ranker `(v1)`

I love scales and sliders, so I developed a movie rating system for myself that uses scales and sliders.

### Eleven Aspects

 1. Direction & Cinematography
 2. Editing
 3. ***Pacing***
 4. Casting & Acting
 5. Сhoreography ∨ Stunts
 6. Production & Art Designs
 7. CGI ∨ Animation
 8. Script
 9. Lines
 10. Score
 11. *Sound*

Almost all of them are rated on a scale of 1 to 5, which roughly corresponds to:

 1. Poor
 2. Below Average
 3. OK
 4. Above Average
 5. Very Good

The only exception is ***Pacing***, which is rated on a scale of 1 to 3:

 1. Bored even once
 2. OK
 3. So interesting that time flew by

### Weighing System

All Aspects can be excluded from the calculation, and can also sometimes be increased or decreased. Almost all of them have a low weight of `0.5`, a standard weight of `1.0`, and a high weight of `2.0`. The exceptions are ***Pacing***, with weights of `1.0`, `2.0`, and `4.0`, respectively, and *Sound*, with weights of `0.25`, `0.5`, and `2.0`, respectively.

#### Why change weights

 - Direction & Cinematography play a lesser role in found footage films (e.g. <a href="https://boxd.it/1yIM">Paranormal Activity</a> or <a href="https://boxd.it/1e3Y">The Last Broadcast</a>).
 - ***Pacing*** plays a more important role in very long films (e.g. <a href="https://boxd.it/2aNK">The Godfather</a> or <a href="https://boxd.it/2bf0">2001: A Space Odyssey</a>).
 - Casting & Acting play a more important role in chamber dramas or films with a limited acting ensemble (e.g. <a href="https://boxd.it/2peU">Carnage</a> or <a href="https://boxd.it/hJAw">Marriage Story</a>).
 - Choreography ∨ Stunts play a more important role in dance musicals or martial arts films (e.g. <a href="https://boxd.it/29oY">Singin’ in the Rain</a> or <a href="https://boxd.it/2bcq">Hero</a>), and a less important role in dialogue-driven films (e.g. <a href="https://boxd.it/2bcU">Before Sunrise</a> or <a href="https://boxd.it/o8M">The Sunset Limited</a>).
 - Production & Art Designs play a more important role in fantasy, science fiction, or historical films (e.g. <a href="https://boxd.it/2awY">Alien</a> or <a href="https://boxd.it/9X0m">The Witch</a>), and a less important role in low- or mid-budget films set in contemporary everyday life (e.g. <a href="https://boxd.it/2706">Clerks</a> or <a href="https://boxd.it/9Y7S">Youth</a>).
 - CGI ∨ Animation play a more important role in blockbusters with a strong emphasis on visuals or in cartoons (e.g. <a href="https://boxd.it/4VZ8">Interstellar</a> or <a href="https://boxd.it/aaie">Puss in Boots: The Last Wish</a>), and a less important role when these elements are used but are almost irrelevant to the film as a whole (e.g. <a href="https://boxd.it/29Pq">Pulp Fiction</a> or <a href="https://boxd.it/zld0">Challengers</a>).
 - Score plays a more important role if it’s a musical or simply a film about music (e.g. <a href="Into the Woods">Into the Woods</a> or <a href="https://boxd.it/1s1C">Linda Linda Linda</a>).
 - *Sound* plays a more important role if it’s a cartoon or a horror film (e.g. <a href="https://boxd.it/29yE">Aladdin</a> or <a href="https://boxd.it/1Yoo">The Exorcist</a>), and a lesser role when it’s a dialogue-driven film where sound design is limited to recording the actors’ voices (e.g. <a href="https://boxd.it/2auI">12 Angry Men</a> or <a href="https://boxd.it/1vLe">My Dinner with Andre</a>).

None of the examples given cover all possible reasons for lowering or raising weights, but at this point I don’t believe there are any reasons, for example, to raise the weight for Direction & Cinematography or lower the weight for Score—only to turn them off if a particular Aspect is completely absent.

### Math

Since the weights may vary or be zero, the minimum and maximum possible scores are unique for different ratings. Therefore, the following three variables are calculated first:

$`C = \sum_{i=1}^{11}(S_i \cdot W_i)`$

$`m = \sum_{i=1}^{11}W_i`$

$`M = (5 \cdot m) - (2 \cdot W_3)`$

where $`C`$ is the unadjusted rating, $`S`$ is the score for a specific Aspect, $`W`$ is the weight of a specific Aspect, $`m`$ is the minimum possible unadjusted rating, and $`M`$ is the maximum possible unadjusted rating.

After that, the final rating ($`R`$) is simply scaled to a 100-point rating system:

$`R =  \left\lfloor 1+ \left( \frac{C - m}{M - m} \right) \cdot 99 \right\rceil`$

### Conversion for [Letterboxd](https://boxd.it/gHhZL)

 - `1–10` → ½
 - `11–20` → ★
 - `21–30` → ★½
 - `31–40` → ★★
 - `41–50` → ★★½
 - `51–60` → ★★★
 - `61–70` → ★★★½
 - `71–80` → ★★★★
 - `81–90` → ★★★★½
 - `91–100` → ★★★★★
