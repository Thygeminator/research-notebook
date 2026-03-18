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

Hey Evangelos and Luigi,

I have been working on several aspects of the project. I started by setting up a cantilever beam model and computing the vibration periods for all possible combinations of stiffness reductions. I then compared the resulting feature lists of periods using metrics such as measured error and cosine similarity. The differences between cases turned out to be quite small, making it difficult to distinguish between them.

After that, I explored alternative vibration-based features, particularly those based on changes in mode shapes. I also began reformulating the model for Bayesian risk optimization in vibration-based SHM. In parallel, I developed a simple case where I implemented the Bayesian risk framework and evaluated all possible sensor configurations.


## Meeting

* [Model for Bayesian risk](https://thygeminator.github.io/research-notebook/#mathematical-model)
* [Simple model implementation of Bayesian risk](https://thygeminator.github.io/research-notebook/#level-1---model-mcs) – using Monte Carlo Simulation (MCS) to integrate the risk function
* [Vibration features](https://thygeminator.github.io/research-notebook/#features-shm)



## My work since last time:

* Set up a cantilever FEM model and extracted model properties

* Compared vibration periods across different damage cases

* Investigated vibration-based features:

  * Natural frequencies
  * Mode shapes

    * Modal Assurance Criterion (MAC)
    * Mode shape curvature *(possibly too sensor-demanding for global SHM?)*
    * Modal Strain Energy (MSE)
    * Modal flexibility
  * Modal damping ratio

* Studied how stochasticity is introduced in the paper:
  “An optimal sensor placement design framework for structural health monitoring using Bayes risk” ([Yang et al., 2022, p. 1](zotero://select/library/items/ZX4LZYUV)) ([pdf](zotero://open-pdf/library/items/BJRVXU2W?page=1&annotation=QBGHRMIK))

  * Stochasticity is modeled as multivariate Gaussian noise in the output features:
    $y = g(\theta, x(e)) + \epsilon, \quad \epsilon \sim \mathcal{N}(0, \Sigma)$

* Set up a similar model for vibration-based SHM with simplifying assumptions:

  <!-- * To make Bayesian risk optimization computationally feasible, the stochasticity is assumed Gaussian
  * This enables the use of **Gaussian quadrature** for efficient integration of the risk function -->

* Developed a simple model where Bayesian risk is computed using MCS:

  * A simplified stochastic model where the number and placement of sensors affect the noise level (via the covariance matrix $\Sigma$)
  * Sensor cost is included



## Most important problems / decisions:

* How should **stochasticity be introduced in the model** in a way that is both:

  * Computationally efficient
  * Realistic

  Possible approaches:

  * Reduce computational cost: Gaussian quadrature, surrogate models, ...
  * Increase realism: make some simulations??? 

* What should be the capability of the SHM system?
  The goal is a global system that triggers more detailed inspection when needed:

  * Level 1: Damage vs. no damage
  * Level 2: Damage location (which element is damaged)
  * Level 3: Damage severity (degree of stiffness reduction)



## Other problems:

* Develop a realistic cost model for sensor and damage consequences
* Gather sensor options, including:
  * Measurement frequencies
  * Installation and maintenance costs
  * Noise characteristics
* Set up a realistic structural model (from the last meeting????)

