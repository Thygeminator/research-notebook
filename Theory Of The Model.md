# Theory of the Model

## Definition of Variables

| Symbol | Meaning |
|---|---|
| $e$                                       | Sensor configuration (sensor locations) |
| $\theta$                                  | Structural state (damage scenario) |
| $x(e)$                                    | Sensor data for an given sensor configuration |
| $y = g(\theta, x(e, \theta)) + \epsilon(e)$       | Measured vibration feature vector with noise/uncertainty |
| $g(x(e, \theta))$                         | Vibration features (From OMA - Operational Modal Analysis or directly from the FEM model) |
| $\epsilon(e) \sim \mathcal{N}(0, \Sigma)$ | Measurement noise/uncertainty |
| $\Sigma$                                  | Noise covariance matrix |
| $P(\theta)$                               | Prior probability of structural state |
| $f(y \mid \theta)$                        | Likelihood of measurement |
| $P(\theta \mid y)$                        | Posterior probability of structural state |
| $L(d(\_),\theta\| C(d(\_),\theta))$       | Loss function given the cost function |
| $C(d(...),\theta)$                         | Cost function |
| $d(\_)$                                   | Decision rule for choosing structural state given the features |
| $\Psi(e)$                                 | Bayes risk for sensor configuration |

## Mathematical Model

Here is the mathematical model for the problem of optimal sensor placement for structural health monitoring using a Bayesian decision-theoretic framework. The structural state $\theta$ is assumed to be a discrete variable representing different damage scenarios. 

$$
\theta \in \{\theta_1, \theta_2, \ldots, \theta_K\}
$$

If we want an Level 1 SHM system where the SHM is only able to detect if there is damage or not, then we can define the structural state as:

$$
\theta \in \{H_0, H_1\}
$$

where $H_0 \in \{\theta_1, \theta_2, \ldots, \theta_n\}$ represents the undamaged state and $H_1 \in \{\theta_{n+1}, \theta_{n+2}, \ldots, \theta_K\}$ represents the damaged state.

- As an simple approximation can we assume that heathy is the stat whit no damage in non of the elements and that the damaged state is the state whit one damaged element.   

---
### Feature Model
The measured vibration features $y$ are modeled as a function of the structural state $\theta$, the sensor configuration $e$, and the measurement noise/uncertainty $\epsilon(e)$.

$$
y = g(x(e, \theta)) + \epsilon(e)
$$

where $\epsilon(e)$ is the feature noise/uncertainty, which is assumed to be Gaussian with zero mean and covariance $\Sigma$. The function $g(\theta, x(e))$ represents the relationship between the structural state $\theta$, the sensor configuration $e$, and the measured features $y$. This function can be derived from the physics of the problem, such as using a finite element model (FEM) to simulate the structural response for different damage scenarios and sensor configurations, or it can be obtained from operational modal analysis (OMA) of the structure under ambient excitations.

$$
\epsilon(e) \sim \mathcal{N}(0, \Sigma), \text{ Multivariate Gaussian noise}
$$

One of the main assumptions / difficulties in this model is the link between the sensor configuration $e$ and the noise model. The most accurate way to model the noise is to perform OMA for the chosen sensor configuration, where the noise and stochasticities are introduced directly into the signal obtained from the ambient excitations of the structure $x(e)$. However, this is computationally expensive and not feasible for the optimization process. An alternative way to model the noise is to make a simple assumption that the noise is Gaussian with zero mean and a covariance matrix $\Sigma$ that is a function of the sensor configuration $e$. This is a simplification, but it allows us to proceed with the optimization process.


## Likelihood Function  (pdf)

Under the assumption that the noise/uncertainty follows a multivariate Gaussian distribution, the likelihood for observing a measurement $y$ given a structural state $\theta$ and sensor configuration $e$ can be expressed as: 

$$
f(y \mid \theta)=
\frac{1}{\sqrt{(2\pi)^n |\Sigma|}}
\exp\left(
-\frac{1}{2}
(y - g(\theta, e))^T
\Sigma^{-1}
(y - g(\theta, e))
\right)
$$

Here is the likelihood for the Level 1 SHM system where we want to detect if there is damage or not:

$$
f(y \mid H_i)= \sum_{\theta \in H_i} f(y \mid \theta) P(\theta \mid H_i)
$$


---

## Prior Distribution (Discrete)

Each structural state is assigned a prior probability, this prior probability represents our beliefs about the likelihood of each damage scenario before observing any measurements. The prior distribution can be based on expert knowledge, historical data, or assumptions about the damage scenarios. For example, if we have no prior knowledge about the damage scenarios, we can assign equal probabilities to each state.

$$
P(\theta)
$$

This priors can be fromed in to $P(H)$ for the Level 1 SHM system where we want to detect if there is damage or not:

$$
P(H) = \sum_{\theta \in H} P(\theta)  
$$

or the conditional prior probability can be used:

$$
P(\theta \mid H_i) = \frac{P(\theta^\star)}{P(H_i)} \text{, where } \theta^\star \text{ is the state that belongs to the class } H_i
$$


---

## Posterior Distribution

The posterior probability of a structural state given the measurement is computed using Bayes' theorem.

$$
P(\theta \mid y) =
\frac{f(y \mid \theta) P(\theta)}{f(y)}
$$

For the Level 1 SHM system where we want to detect if there is damage or not, the posterior probability can be expressed as:

$$
P(H_i \mid y) = \frac{f(y \mid H_i) P(H_i)}{f(y)}
$$


---

## Decision Rule

There are many discisions rules to chose from, one of them is the maximum a posteriori (MAP) decision rule, which chooses the structural state that has the highest posterior probability given the measurement. The MAP decision rule can be expressed as:

$$
d^*(y) =
\arg\max_{H_i} P(H_i \mid y) 
$$



---

## Bayes Risk

The Bayes risk represents the expected loss for a sensor configuration.given the decision rule and the loss function. The Bayes risk can be expressed as:

$$
\Psi(e) =
\mathbb{E}_{H, y}\left[
L(d^*(y), H_i)
\right] = \sum_{H_i} P(H_i) \int f(y \mid H_i) L(d^*(y), H_i) dy
$$


- Use dimension reduction and or Gauss–Hermite quadrature to evaluate the integral over the measurement space efficiently.


---

## Optimal Sensor Configuration

The optimal sensor configuration is obtained by solving

$$
e^* =
\arg\min_e
\Psi(e)
$$



# Algorithmic cost
## big O notation

### Bayes risk estimation given a sensor configuration $e$

here is the computational cost of the Estimation of the Bayes risk for a given sensor configuration $e$:

| MCS - monte carlo simulation | Gaussian quadrature |
|---|---|
| $O(\sharp  \theta \cdot N \cdot (\sharp  y^3 + \sharp  \theta \cdot \sharp  y^2))$ | $O(\theta \cdot M^{\sharp y})$ |
| Explanation | Explanation |
| $(\sharp y^3 + \sharp \theta \cdot \sharp y^2)$ this is the cost of the Monte Carlo simulation |   |
| $\sharp y^3$ this is the cost of generating the multivariate normal samples |   |
| $\sharp \theta \cdot \sharp y^2$ this is the cost of evaluating the likelihood for each structural state given the one MCS sample |   |


note: I need some dimension reduction techniques to reduce the cost of the Gaussian quadrature method, because the cost grows exponentially with the dimensionality of the measurement space $\sharp y$.

where:
- $\sharp$ is the number of elements in the set
    - so $\sharp  \theta$ is the number of structural states (damage scenarios), $\sharp  y$ is the dimensionality of the measurement space (length of the feature vector).
- $N$ is the number of Monte Carlo samples.
- $M$ is the number of quadrature points per dimension in the Gaussian quadrature method.

### Cost of the stochastic in the likelihood function 





# Appendix: General Theory

## Risk for an event A:
Risk for the event A is defined as the product of the probability of the event A occurring and the utility or loss associated with the consequence of that event. 

$$
R(A) = P(A) \cdot L(A)
$$

where:
- $P(A)$ is the probability of an event A occurring.
- $L(A)$ is the utility or loss do to the consequence associated with event A.

## Bayes Rule
Bayes rule is a way to update our beliefs about the probability of an event A given new evidence B. 
$$
P(A|B) = \frac{P(B|A)P(A)}{P(B)} \Rightarrow \text{Posterior} = \frac{\text{Likelihood} \times \text{Prior}}{\text{Evidence}}
$$

Here is an refumulation of the Bayes rule there makes more sens with respect to Frequentist risk and the Bayes risk.

$$
    f(\theta|x) = \frac{f(x|\theta)f(\theta)}{f(x)} 
$$

where: 
- $f(\theta|x)$ is the posterior distribution of the parameter $\theta$ given the data $x$.
- $f(x|\theta)$ is the likelihood function, which describes the probability of observing the data $x$ given the parameter $\theta$.
- $f(\theta)$ is the prior distribution of the parameter $\theta$, which represents our beliefs about the parameter before observing the data.
- $f(x)$ is the evidence, which can be found by the marginalization of the likelihood and prior.


## Frequentist risk
Frequentist risk is the expected loss of a decision rule given the parameter $\theta$ of the data generating process. It is defined as:

$$
R(\theta, d(x))) = E_{X|\theta}[L(\theta, d(x)) | \theta] = \int L(\theta, d(x)) f(x|\theta) dx
$$

where:
- $\theta$ is the parameter of the data generating process.
- $d(x)$ is the decision rule that maps the data to a decision.
    - Example of a decision rule:  
        - Mean decision rule: $d(x) = E_{\theta|x}[\theta|x] = \int \theta f(\theta|x) d\theta$
        - Maximum a posteriori (MAP) decision rule: $d(x) = \text{argmax}_{\theta} f(\theta|x)$
        - Minimum risk decision rule: $d(x) = \text{argmin}_{d} R(\theta, d(x))$
- $L(\theta, d(x))$ is the loss function that quantifies the loss incurred by making a decision $d(x)$ when the true parameter is $\theta$.
    - Example of a loss function: 
        - Squared error loss: $L(\theta, d(x)) = (\theta - d(x))^2$
        - Absolute error loss: $L(\theta, d(x)) = |\theta - d(x)|$
        - utility / cost function: $L(\theta, d(x)) = C(\theta, d(x))$, where $C$ is a cost function that quantifies the cost of making a decision $d(x)$ when the true parameter is $\theta$.
- $f(x|\theta)$ is the likelihood function that describes the probability of observing the data $x$ given the parameter $\theta$. 



## Bayes Risk
Bayes Risk is the expected value of a loss function over both the data and the parameter space. It represents the "average" loss you incur when using a specific decision rule, weighted by your prior beliefs. 

See section 2.3 page 60-65 in the book "The Bayesian Choice From Decision-Theoretic Foundations to Computational Implementations" by Christian P. Robert there is some information on both the frequentist risk and bayesian risk.  
$$
r(\theta, d(x)) = E_{\theta}[E_{X|\theta}[L(\theta, d(x)) | \theta] \cdot f(\theta)] = \int R(\theta, d(x)) f(\theta)  \space d\theta
$$

$$
r(\theta, d(x)) = \int \int L(\theta, d(x)) f(x|\theta) f(\theta)  \space dx \space d\theta = \int \int L(\theta, d(x)) f(x|\theta) \space dx \space f(\theta)  \space d\theta
$$

Note: the inner and outer integrals can be switched because of Fubini’s Theorem. see Theorem 2.3.2 in the book "The Bayesian Choice From Decision-Theoretic Foundations to Computational Implementations" by Christian P. Robert.

# Appendix: General Notation
## Abbreviation

- PDF: Probability Density Function
- CDF: Cumulative Distribution Function

## Discreet vs Continuous probability distributions
- Discreet: 
    - PDF: $P(X=x)$, $P(X)$, $P(x)$
    - CDF: $P(X \leq x)$, $P(X \leq x)$
- Continuous: 
    - PDF: $f(X=x)$, $f(X)$, $f(x)$
    - CDF: $F(X \leq x)$, $F(X)$, $F(x)$