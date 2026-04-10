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
# Meting Overview 


1. Go through my first presentation: [Presentation_1](https://thygeminator.github.io/research-notebook/Presentation_1.html) (~40 minutes)
   - Ground work presentation, on SHM, OSP, My research topic, and Theory/Methodology.
   - Strong slide: [Summary of Method in factor graph with plates](https://thygeminator.github.io/research-notebook/Presentation_1.html#/summary)

2. Second Presentation: [Presentation_2](https://thygeminator.github.io/research-notebook/Presentation_2.html) (~40 minutes)
   - Simple case study, Present FEM model, Assumptions, Results.

3. Whats Next (~10 minutes)
   - Discuss what I should focus on til next meeting. 

Note: We will discuss the context of the presentations along the way. So the presentation is meant to be an aid in or discussing more than a formal presentation.


---  
## Abbreviations 

- Structural Health Monitoring (SHM)
- Optimal Sensor Placement (OSP)





<!-- ## Meeting Plan / Work Done Last Time

- Reading papers on how to set up the link between the likelihood function and the uncertainty in observing the features for a damage state with a given sensor configuration.
   - Hard to find papers that use the likelihood function for optimal sensor placement; most of the papers I have found have been using Bayesian risk to optimize the decision process.
   - Most papers assume an arbitrary multivariate normal distribution for the noise feature function. 
   - **Value of information from vibration-based structural health monitoring extracted via Bayesian model updating**
- Investigate and implement [pyOMA2](https://github.com/dagghe/pyOMA2) for OMA
- Set up a model and investigate the noise function for 2 sensor configurations
   - Assume that it is okay to only introduce noise as changes in the stiffness of the elements, and that the noise is normally distributed and independent.
   - Generate samples for the undamaged model with stiffness changes


## Questions + Notes -->




<!-- --- 

- Problem of defining Damage states and sensor states, they explode combinatorially if no assumptions are made.
  - Note: Sensor states is okay because that is what we optimize for. 
  - Damage states: the problem whit the damage states are that they are need in the sum over all senarios in the bayesian risk, and they explode combinatorially quickly if no assumptions are made.
    - Assume Example: only analyze states whit one damaged element.
  - Number of states both for sensors and damage states, $e$ and $\theta$ respectively
    - (Binomial coefficient) $ \text{Number of scenarios}=\binom{n}{k} =\frac{n!}{k!(n-k)!}$, where $n$ is the total number of elements or sensor locations, and $k$ is the number of elements or sensor locations that are in a particular state. 
    - Total combinations: $\text{Total combinations} = \sum \binom{n}{k} = \sum \frac{n!}{k!(n-k)!} =  2^n$

--- 

- how to define Priors and how shot they be understood???  -->