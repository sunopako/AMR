## AMR — Autistic Movie Ranker `(v1 — Amélie)`

A movie evaluation system designed to replace arbitrary gut-feeling scores with a little less arbitrary mathematically grounded 100-point rating.

### Principles

To adopt such a system, certain presumptions must be accepted:

 - Art is inherently quantifiable.
 - The author is dead, as are all the factors surrounding the film under evaluation: the studio’s ambitions, audience reception, box office performance, controversies involving the actors, etc.
 - A film is the sum of its technical, evaluative components, and nothing more. No soul, no adjustments for nostalgia or one's mood, no x-factor, etc.
 - Eleven Aspects listed below are exhaustive, and there is nothing in any film that does not fall under one of these Aspects or that cannot be described by a combination of several of these Aspects.

An evaluator, of course, is an imperfectly calibrated measuring device and is therefore prone to error. It is precisely within this margin of imperfection that the subjective final evaluation lies.

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

 1. Bad
 2. Below Average
 3. OK
 4. Above Average
 5. Very Good

The only exception is ***Pacing***, which is rated on a scale of 1 to 3:

 1. Rushed or dragged 🥁
 2. OK
 3. Didn't notice time flew by

### Weighing System

All Aspects can be excluded from the calculation (i.e. corresponding weight set to `0`), and can also sometimes be adjusted in terms of their importance. Almost all of them have a low weight of `0.5`, a standard weight of `1.0`, and a high weight of `2.0`. The exceptions are ***Pacing***, with weights of `1.0`, `2.0`, and `4.0`, respectively, and *Sound*, with weights of `0.25`, `0.5`, and `2.0`, respectively.

#### Why change weights

 - Direction & Cinematography play a lesser role in found footage films (e.g. [Paranormal Activity](https://boxd.it/1yIM) or [The Last Broadcast](https://boxd.it/1e3Y)).
 - ***Pacing*** plays a more important role in very long films (e.g. [The Godfather](https://boxd.it/2aNK) or [2001: A Space Odyssey](https://boxd.it/2bf0)).
 - Casting & Acting play a more important role in chamber dramas or films with a limited acting ensemble (e.g. [Carnage](https://boxd.it/2peU) or [Marriage Story](https://boxd.it/hJAw)).
 - Choreography ∨ Stunts play a more important role in dance musicals or martial arts films (e.g. [Singin’ in the Rain](https://boxd.it/29oY) or [Hero](https://boxd.it/2bcq)), and a less important role in dialogue-driven films (e.g. [Before Sunrise](https://boxd.it/2bcU) or [The Sunset Limited](https://boxd.it/o8M)).
 - Production & Art Designs play a more important role in fantasy, science fiction, or historical films (e.g. [Alien](https://boxd.it/2awY) or [The Witch](https://boxd.it/9X0m)), and a less important role in films set in contemporary everyday life (e.g. [Clerks](https://boxd.it/2706) or [Youth](https://boxd.it/9Y7S)).
 - CGI ∨ Animation play a more important role in blockbusters with a strong emphasis on generated visuals or in cartoons (e.g. [Interstellar](https://boxd.it/4VZ8) or [Puss in Boots: The Last Wish](https://boxd.it/aaie)), and a less important role when these elements are used but are almost irrelevant to the film as a whole (e.g. [Pulp Fiction](https://boxd.it/29Pq) or [Challengers](https://boxd.it/zld0)).
 - Score plays a more important role if it’s a musical or simply a film about music (e.g. [Into the Woods](https://boxd.it/1zje) or [Linda Linda Linda](https://boxd.it/1s1C)).
 - *Sound* plays a more important role if it’s a cartoon or a horror film (e.g. [Aladdin](https://boxd.it/29yE) or [The Exorcist](https://boxd.it/1Yoo)), and a lesser role when it’s a dialogue-driven film where sound design is limited almost exclusively to recording the actors’ voices (e.g. [12 Angry Men](https://boxd.it/2auI) or [My Dinner with Andre](https://boxd.it/1vLe)).

None of the examples given cover all possible reasons for lowering or raising weights, but at this point I don’t believe there are any grounds, for example, to raise the weight for Direction & Cinematography or lower the weight for Score—only to turn them off if a particular Aspect is completely absent.

### Math

Since the weights may vary or be zero, the minimum and maximum possible scores are unique for different ratings. Therefore, the following three variables are calculated first:

$`\Huge C = \sum_{i=1}^{11}(S_i \cdot W_i)`$

$`\Huge m = \sum_{i=1}^{11}W_i`$

$`\Huge M = (5 \cdot m) - (2 \cdot W_3)`$

where $`C`$ is the raw rating, $`S`$ is the score for a specific Aspect, $`W`$ is the weight of a specific Aspect, $`m`$ is the minimum possible raw rating, and $`M`$ is the maximum possible raw rating.

After that, the final rating ($`R`$) is simply scaled to a 100-point rating system:

$`\Huge R =  \left\lfloor 1+ \left( \frac{C - m}{M - m} \right) \cdot 99 \right\rceil`$

### Conversion for [Letterboxd](https://boxd.it/gHhZL)

In conclusion, the rating is linearly mapped to a 10-point star scale:

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
