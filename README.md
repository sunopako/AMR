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

### Math

Since the weights may vary or be zero, the minimum and maximum possible scores are unique for different ratings. Therefore, the following three variables are calculated first:

 - $`C = (S_1 \cdot W_1) + (S_2 \cdot W_2) + (S_3 \cdot W_3) + (S_4 \cdot W_4) + (S_5 \cdot W_5) + (S_6 \cdot W_6)+ (S_7 \cdot W_7) + (S_8 \cdot W_8) + (S_9 \cdot W_9) + (S_{10} \cdot W_{10}) + (S_{11} \cdot W_{11})`$
 - $`m = W_1 + W_2 + W_3 + W_4 + W_5 + W_6 + W_7 + W_8 + W_9 + W_{10} + W_{11}`$
 - $`M = (5 \cdot W_1) + (5 \cdot W_2) + (\textbf{3} \cdot W_3) + (5 \cdot W_4) + (5 \cdot W_5) + (5 \cdot W_6)+ (5 \cdot W_7) + (5 \cdot W_8) + (5 \cdot W_9) + (5 \cdot W_{10}) + (5 \cdot W_{11})`$

where $`C`$ is the unadjusted rating, $`S`$ is the score for a specific Aspect, $`W`$ is the weight of a specific Aspect, $`m`$ is the minimum possible unadjusted rating, and $`M`$ is the maximum possible unadjusted rating.

After that, the final rating ($`R`$) is simply scaled to a 100-point rating system:

$`R =  \left\lfloor 1+ \left( \frac{C - m}{M - m} \right) \cdot 99 \right\rceil`$

### Conversion for Letterboxd

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
