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
# Meeting Overview 

This week’s meeting focuses on the new stochastic model that I presented to Luigi last week, along with the implementation of new decision algorithms for estimating the risk associated with different sensor configurations.

I have also implemented importance sampling to reduce the variance of the risk estimation, thereby lowering the number of samples required to obtain reliable results. 

Additionally, I have included confusion matrices for the different decision algorithms. These provide insight into how each algorithm performs across the various sensor configurations.

[Presentation](https://thygeminator.github.io/research-notebook/P_new.html) overview:


- [New Stochastic model](https://thygeminator.github.io/research-notebook/P_new.html#/new-stochastic-model) (~20 min)
    - Mathimatical formulation, code example and implications
- [Set up case study](https://thygeminator.github.io/research-notebook/P_new.html#/case-study-overview) (~5 min)
    - FEM model, damage states, sensor states, cost function and priors.
    - Covariance matrix for the noise function.
- [Analysis of the rsik](https://thygeminator.github.io/research-notebook/P_new.html#/analysis-1) (~30 min)
    - A1: explicit liklihood function, MCS, no use of features 
    - A1.1: explicit liklihood function, MCS importance sampling, no use of features
    - A2: use of features, MCS whit importance sampling, 
         - logistic regression
- [Questions](https://thygeminator.github.io/research-notebook/P_new.html#/questions) (~10 min)
- [Whats next?](https://thygeminator.github.io/research-notebook/P_new.html#/whats-next) (~10 min)



<!-- This week's meeting focuses on the new stochastic model, where the stochasticity is introduced on the modal properties and not directly on the features. There is also a focus on the implications of this choice and what options it opens up for the model of the Bayesian risk.

- [Presentation](https://thygeminator.github.io/research-notebook/P_new.html) - New stochastic model, and its implications.
   - Section for this meting: 
      - [New Stochastic model](https://thygeminator.github.io/research-notebook/P_new.html#/new-stochastic-model)
      - [Code example - Stochastic model](https://thygeminator.github.io/research-notebook/P_new.html#/code-example---stochastic-model)
      - [Questions](https://thygeminator.github.io/research-notebook/P_new.html#/questions)

Note: The other parts of the presentation are for next meeting. -->



---  
## Abbreviations 

- Structural Health Monitoring (SHM)
- Optimal Sensor Placement (OSP)
- Operational Modal Analysis (OMA)
- Monte Carlo Simulation (MCS)
- Machine learning (ML)
- Bayesian Risk (BR)
- Maximum likelihood estimation (MLE)



--- 
## Old presentations

Week 16:

- [Presentation_1](https://thygeminator.github.io/research-notebook/week_16/Presentation_1.html) - Over all model and method overview.
- [Presentation_2](https://thygeminator.github.io/research-notebook/week_16/Presentation_2.html) - Case study of cantilever beam, Present FEM model, Assumptions, Results.

Week 17: (Thyge and Luigi)

- [Presentation_1](https://thygeminator.github.io/research-notebook/week_17/P_new.html) - New stochatic model, and its implications. 

Week 18: 

- [Presentation_1](https://thygeminator.github.io/research-notebook/week_18/P_new.html) - New stochatic model and ML and confusion matrices.


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