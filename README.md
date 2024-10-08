# Statistician-Pre-Interview-Task

Dehua Tao

August 2024

The goal of moderating school assessments is to convert school-based scores into moderated scores that are comparable across different schools while retaining the properties of the raw scores. Raw scores are unsuitable due to variations in assessment types and scales. For a school with $N$ students, the raw scores are denoted as $\boldsymbol{X} = \left( x_1, x_2, \dots, x_N \right)$. The objective is to transform this vector into $\tilde{\boldsymbol{X}} = \left( \tilde{x}_1, \tilde{x}_2, \dots, \tilde{x}_N \right)$, representing the moderated scores. Linear adjustments or regression models are applied to $\boldsymbol{X}$ to derive $\tilde{\boldsymbol{X}}$, incorporating examination marks $\boldsymbol{Y} = \left( y_1, y_2, \dots, y_N \right)$ to ensure validity.

I selected the Bayesian segmented linear regression approach from Article 1 for moderating school assessments. This model uses the Wasserstein distance between the cumulative distributions of $\tilde{\boldsymbol{X}}$ and $\boldsymbol{Y}$ to measure similarity. By incorporating the empirical cumulative function, minimising the Wasserstein distance becomes equivalent to minimising the mean square error (MSE) in regression, aiding in parameter estimation.

There are several reasons for choosing this model. First, it offers flexibility by allowing different linear relationships across ranges. $\tilde{\boldsymbol{X}}$, determined by the highest examination score $y_{(N)}$ and $\boldsymbol{X}$, is modelled via a Bayesian segmented linear regression with up to two breakpoints, with the added constraint that the highest $\tilde{\boldsymbol{X}}$ equals $y_{(N)}$. The location of these breakpoints is determined using posterior probabilities, making the model more general than the MSR(1) model in Article 3, which sets the median of $\boldsymbol{X}$ as the breakpoint. The optimal number of breakpoints is decided by the Bayes factor, similar to Bayesian hypothesis testing.

Second, the model efficiently estimates parameters without relying on traditional MCMC procedures. By expressing the segmented regression in a matrix-vector form and applying conjugate priors, parameters can be directly sampled from the posterior distribution, offering a faster and more robust estimation process compared to iterative algorithms.

The third reason is the outlier detection procedure. A local linear estimator calculated from $\boldsymbol{Y}$ and $\tilde{\boldsymbol{X}}$ is used to flag underperforming students, with the tuning parameter determined by cross-validation. This approach is more sensible than the method in Article 3, which detects outliers by identifying differences greater than 7.5 between the $E_1$ value and the top $\boldsymbol{X}$ value, a threshold based on experience from Article 2, which the Article 1 model does not use. Additionally, the Article 3 model determines other outliers by directly deriving the nonparametric quantile, a less efficient method compared to the Article 1 approach, which first derives the nonparametric CDF from observed data before determining the boundary.

Finally, in real data applications, the model from Article 1 produces sensible results, with the CDF of $\tilde{\boldsymbol{X}}$ closely matching that of $\boldsymbol{Y}$. Sensitivity analysis confirms that the model is robust to prior parameter values, solidifying the analysis outcomes.

Some extensions of the Article 1 framework could be explored in future research, such as adding penalised terms to control the number of breakpoints, allowing nonlinear relationships within segments, and incorporating robust methods to make the model less sensitive to outliers.

