# Research Notebook (MSc Thesis)

Hi Evangelos and Luigi 👋

This repository is used to share my ongoing thesis progress ahead of our meetings.  You may optionally review it prior to the meeting to support discussion and feedback.  

➡ **Rendered notes (GitHub Pages):**
https://thygeminator.github.io/research-notebook/

The website contains the readable HTML version of my Quarto/Jupyter notebook

The repository itself only exists to generate the website — the page above is the intended way to read the material.

All content is preliminary and written as working notes rather than a structured report.
Some spelling or grammar errors may be present, as the notes are not proofread and mainly serve as a live record of ideas, code development, and ongoing work.

Thank you!

--- 
# Week now - Overview 



## Questions + Notes

--- 

- Problem of defining Damage states and sensor states, they explode combinatorially if no assumptions are made.
  - Note: Sensor states is okay because that is what we optimize for. 
  - Damage states: the problem whit the damage states are that they are need in the sum over all senarios in the bayesian risk, and they explode combinatorially quickly if no assumptions are made.
    - Assume Example: only analyze states whit one damaged element.
  - Number of states both for sensors and damage states, $e$ and $\theta$ respectively
    - (Binomial coefficient) $ \text{Number of scenarios}=\binom{n}{k} =\frac{n!}{k!(n-k)!}$, where $n$ is the total number of elements or sensor locations, and $k$ is the number of elements or sensor locations that are in a particular state. 
    - Total combinations: $\text{Total combinations} = \sum \binom{n}{k} = \sum \frac{n!}{k!(n-k)!} =  2^n$

--- 

- how to define Priors and how shot they be understood??? 