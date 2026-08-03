# Process overview

A reading-guide to how the work came together --- a map to your process, not an
essay about it. Markers read this file and follow its citations; they don't
trawl the repo for evidence you didn't point at, so if a moment mattered, cite
it.

This file is the shape; the course site's
[assessment page](https://comp.anu.edu.au/courses/comp4020-agentic-coding-studio/topics/assessment/#what-you-submit)
is the requirement, and each brief adds its own word count and moment count.

## What I built

The modern web is very difficult to the web of in the 00s and especially the 90s. The web started off as a between universities and then mostly between people. Largely, now the web is between companies. As a result of this, the way the modern web is styled follows a paradigm that is instantly recognisable as being contemporary or modern. Some examples of this are the use of flex boxes to enable a div to be easily made responsive to a smaller viewport with the change of the flex-direction css property. My site aims to put these modernities to the side (at least as much as I can do in like less than 5 days), and celebrates things like absolute positioning and sites that were full of images, movement and colour. All whilst not sacrificing accessibility, by the way. As a result, what I've made is sort of surreal (not in the melting clocks salvador dali kinda way) in my own way. Hope you enjoy it.

## The moments that mattered

I didn't use an agent, I googled when I needed help and I asked the llm like two questions. So I'll focus on that.

I wanted to change the colour of a tiled noise background that I have on my homepage to be something other than the boring default grey that it usually is. Hence, I just asked the llm how to do it and showed my current boring noisy background css. Then the llm gave me 2 options i could copy and paste into my css to remedy the issue, with one being just changing the background colour the noise is overlayed upon and the other being changing the colours used in the svg that is used as the background-image in css to create a tiled noise background on the site. I copied and pasted in the latter -- rather I got the llm to give me a line i could copy and paste in cause the line it gave previously was not very useful -- then i checked in my browser pointing to the localhost port that `pnpm dev` had given me and saw beautiful colours in my websites background noise. This meant it worked, since this is exactly what i wanted. You can see this change in the styles.css file in this commit [`5d879bf`](https://github.com/comp4020-agentic-coding-studio/comp4020-crit1-NikhilaGurusinghe/commit/5d879bff0556843aac7fd61d1ed52fd63bb9d073)

#### llm convo
#### my prompt

> tell me how to change the colour of the noise here   
  .noise-background {                                  
    background-color: transparent;                     
    background-image: url("data:image/svg+xml,%3Csvg   
  xmlns='http://www.w3.org/2000/svg' viewBox='0 0 600  
  600'%3E%3Cfilter id='a'%3E%3CfeTurbulence            
  type='fractalNoise' baseFrequency='.65'              
  numOctaves='3'                                       
  stitchTiles='stitch'/%3E%3C/filter%3E%3Crect         
  width='100%25' height='100%25' filter='url(%23a)'    
  /%3E%3C/svg%3E");                                    
    background-repeat: repeat;                         
    background-size: 182px;                            
     }  

#### claude
>Two ways to tint that noise, since raw feTurbulence
>  output is grayscale:
>  
>  Option A — CSS blend mode (easiest, no SVG edit 
>  needed)
>
>  Set an actual color on background-color and blend it
>  with the noise:
>
>  .noise-background {
>    background-color: #ff6600;         /* your colour 
>  */
>    background-blend-mode: multiply;    /* or overlay, 
>  screen, soft-light */
>    background-image: url("data:image/svg+xml,...");
>    background-repeat: repeat;
>    background-size: 182px;
>  }
>
>  multiply darkens toward your color, screen lightens
>  toward it, overlay/soft-light give more
>  contrast-preserving tints. Try a few — it changes the
>  look a lot.
>
>  Option B — Colorize inside the SVG with feColorMatrix
>
>  Add a color matrix filter after the turbulence to map
>  gray values to a specific hue instead of relying on
>  blending:
>
>  %3Cfilter id='a'%3E
>    %3CfeTurbulence type='fractalNoise'
>  baseFrequency='.65' numOctaves='3'
>  stitchTiles='stitch'/%3E
>    %3CfeColorMatrix type='matrix' values='0 0 0 0 1  0
>  0 0 0 0.4  0 0 0 0 0  0 0 0 1 0'/%3E
>  %3C/filter%3E
>
>  That matrix example maps the grayscale noise to an
>  orange tint (R=1, G=0.4, B=0 per pixel, alpha
>  unchanged). Swap the three color rows (R, G, B) for
>  whatever 0–1 RGB you want.
>
>  For a quick single-color tint, Option A is simplest —
>  just change background-color and pick a blend mode.
>  Option B gives more control over how the noise grain
>  itself looks (contrast/brightness of the grain vs.
>  flat tint)

#### my prompt
> give me something i can copy and paste in that uses  
  155dff into this %3Cfilter id='a'%3E                 
      %3CfeTurbulence type='fractalNoise'              
    baseFrequency='.65' numOctaves='3'                 
    stitchTiles='stitch'/%3E                           
      %3CfeColorMatrix type='matrix' values='0 0 0 0 1 
   0                                                   
    0 0 0 0.4  0 0 0 0 0  0 0 0 1 0'/%3E               
    %3C/filter%3E      

#### claude
> Here's the filter with #155dff (R=0.082, G=0.365,
>  B=1) swapped in:
>
>  %3Cfilter id='a'%3E
>      %3CfeTurbulence type='fractalNoise'
>    baseFrequency='.65' numOctaves='3'
>    stitchTiles='stitch'/%3E
>      %3CfeColorMatrix type='matrix' values='0 0 0 0
>  0.082  0
>    0 0 0 0.365  0 0 0 0 1  0 0 0 1 0'/%3E
>    %3C/filter%3E
>
>  And the full background-image line, ready to paste:
>
>  .noise-background {
>    background-color: transparent;
>    background-image: url("data:image/svg+xml,%3Csvg 
>  xmlns='http://www.w3.org/2000/svg' viewBox='0 0 600 
>  600'%3E%3Cfilter id='a'%3E%3CfeTurbulence 
>  type='fractalNoise' baseFrequency='.65' 
>  numOctaves='3' 
>  stitchTiles='stitch'/%3E%3CfeColorMatrix 
>  type='matrix' values='0 0 0 0 0.082  0 0 0 0 0.365  0
>  0 0 0 1  0 0 0 1 0'/%3E%3C/filter%3E%3Crect 
>  width='100%25' height='100%25' filter='url(%23a)' 
>  /%3E%3C/svg%3E");
>    background-repeat: repeat;
>    background-size: 182px;
>  }
>
>  Each row maps output R/G/B to a fixed value (0.082 /
>  0.365 / 1) regardless of the noise's own RGB, while
>  the last row keeps alpha driven by the turbulence —
>  so the grain shows up as varying opacity of that blue
>  rather than varying color.

## Before you ship

`pnpm check:evidence` verifies your citations resolve to real commits, that the
current reflection entry is in `reflections/`, and that your `CLAUDE.md` is
there --- before a marker ever opens the file. It checks that your map is
traceable, not that it is good: the marker judges whether your small,
deliberately chosen set of moments shows real judgement and reflection. A green
check is not a substitute for that curation.

Images are deliberately not checked, because whether one renders is visible the
moment you look. Open this file on GitHub and look at it before you ship.
