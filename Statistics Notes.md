# Statistics Notes

### Tools

#### Moment  Generating Functions (MGF)

nth derivative of MGF gives nth moment. fully determines distribution if exists

​				M(t) = E(e^tX)		t is dummy variable. must be finite on (-ep,ep)

* used to compute sums of independent distributions (add to mult.)

#### Probability Generating Functions (PGF)

generating function of the PMF. guaranteed to exist for non-negative integer-valued r.v.s

​				E(t^X) = sum_k p_k t^k

#### Cumulant Generating Functions (K(t))

generates the cumulants. cumulant 1:mean, 2nd variance, 3rd: 3rd central moment, 4th no correspondance. for independent r.v.s  cumulant( sum_i X_i ) = sum_i k_i

​				K(t) = log(E(t^X))

#### Change of Variables

​			f_Y(y) = f_X(x) * |dx/dy|



#### Math Identities

##### Conditional Probability

​				P(A|B) = P(A int B) / P(B)

##### Baye's Rule

derived from intersection 	P(A|B)P(B) = P(B|A)P(A) = P(A int B)

​				P(A|B) = P(B|A)P(A)  / P(B)

Odd's Form:		P(A|B) / P(Ac|B) = P(B|A)P(A)  / P(B|Ac)P(Ac)

##### Law of Total Probability (LOTP)

probability of B given condition on many A_i is sum over all A_i space. 

​				P(B) = sum_i P(B|Ai)P(Ai)

##### Law of the Unconscious Statistician (LOTUS)

expected value of a function on a r.v. X is found by summing up value of function over probabilities of X

​				E(g(X)) = sum_x g(x) P(X=x) 		(discrete)

​				E(g(X))) = int_x g(x) f(x) dx		(continuous)

##### Location-Scale Transform

applied to r.v. X to obtain new r.v. Y = sX+u . Maintains linearity and keeps distribution in family.

##### Universiality of the Uniform

if you can find the inverse CDF **F'** for a distribution, can generate it from the uniform through

​			X ~ F' (U)		so that X ~ (dist. with CDF F)

Also, 		F(X) ~ U		where X is plugged into own CDF (similar to quintiles)

Can use to construct any discrete r.v. by chopping (0,1) into pices of length p_i . 

##### Indicator r.v.s and fundamental bridge

any space splits into success (A) or failures (Ac), so can use Bern(p) to indicate ( I_A).

​			P(A) = E( I_A)

## Distributions

#### Distribution Descriptions 

**Probability Mass Functions** (**PMF**) - P(X=x) - gives probability of each discrete value

**Probability Density Fuctions** (**PDF**) - f(x) - gives probability density near value x

**Cumulative Density Functions** (**CDF**)  - F(x) = P(X<=x) gives cumulative probability below x

#### Moments

**Mean**  - expected value, 1st moment, weighted sum of values & probabilities. balancing point of PDF/PMF

**Median** - 50% data falls above/below value - could be ill-defined. halves area of PDF/PMF.

**Mode** - peak of PMF/PDF (most likely point) - non-unique

**Variance** - denotes spread of distribution, 2nd moment

**Skew** - measures non-symmetry, related to 3rd moment

**Kurtosis**  - measures tail weight, related to 4th moment

#### Properties

**joint** distribution - full pdf of multiple variables (many-dimensional)

**marginal** distribution - pdf of one variable, summed over other vars. (i.e. written in *margin* next to table as sum of rows)

**conditional** distribution - pdf of one or several variables, given (conditioned) on a set (known) value of one or more other variables. 



## Discrete Distributions

### Discrete Uniform

equal chance of choosing any of $n$ numbers in a set. 

​	$P(X=x) = \frac{1}{n}$

### Binomial

Obtained from $n$ repeated Bernoulli Trials with success $p$. (AKA sampling *with replacement*.)

​	$ P(X=k)= {n\choose k}p^kq^{n-k}$

* properties
  * sum of binomials is binomial
    if $X\sim Bin(n,p)$ and $Y\sim Bin(m,p)$ then $X+Y\sim Bin(n+m,p)$.
  * *condition* to **Hypergeometric** by conditioning on $X+Y=r$  which gives 
    $X+Y\sim HGeom(n,m,r)$ 

#### Bernoulli Trials

Binary distribution, success with probability $p$ failure with probability $q=1-p$ .

* used for *indicator random variables*. 
* *properties* 
  * sum of $n$ Bernoulli trials $p$  is Bin(n,p)

### Negative Binomial

Number of failures before rth success in series of iid $Bern(p)$ trials. 

​	$P(X=n) = {n+r-1 \choose r-1 } p^r q^n$

- properties
  - sum of r iid Geom(p) are NBin(r,p)

#### Geometic

Number of failures before the first success in a series of iid $Bern(p)$ trials.

​	$P(x=k)=q^kp$ 

- *limit* to Expo($\lambda$) when $p=\lambda \Delta t$ and $\Delta t \rightarrow 0$. (do lots of low-success trials super fast to get to continuous case)

### Hypergeometric

Obtained by sampling from $n$ balls, where there are $w$ white or 'success' balls, $b$ black or 'failure' balls, *without replacement*. 

​	$P(X=k)=\frac{{w\choose k} {b \choose n-k}}{{w+b \choose n}}$

- properties
  - *limit* to Bin in the case of $n\rightarrow\infty$, with $p=w/n$.

### Negative Hypergeometric

number of black balls chosen before the first white ball in $HGeom(w,b,n)$. 

### Poisson

counts the number of successes in a particular interval, space, or time, with success "rate" $\lambda$. 

​	$P(X=k) = \frac{e^{-\lambda}\lambda^k}{k!}, \qquad k=0,1,2…$

* properties
  * approximately equal to sum of weakly dependent or ind. events with low probability $p$ , with $\lambda =\sum p$ . This is Poisson approx of Binomial.
  * if  $X \sim Pois(\lambda_1)$ and $Y \sim Pois(\lambda_2)$ then  $X+Y \sim Pois(\lambda_1 + \lambda_2)$ 
  * $X$ *conditioned* on $X+Y=n$  is $Bin(n, \lambda_1 / (\lambda_1+\lambda_2))$.
    * this is analogous to $HGeom\rightarrow Bin$  
    * $X$ represents success, $Y$ failure
  * for *Poisson process* the waiting time between success is $Expo(\lambda)$.


#### Poisson Process

* X waiting time between sucesses ~ Expo($\lambda$). 	(each interval independent, memoryless)
* T$_n$ arrival times ~ Gamma(n, $\lambda$).	(arrival times are waiting times for nth arrival)
* Given N(t$_2$) = n in total interval, with sub-interval t$_1$ < t$_2$, then 
  ​	N$_1$ | (N$_2$ = n ) ~ Bin(n,t$_1$/t$_2$)			(in or out of sub-interval is binomially distributed)
* T$_n$ | (N(t) = n)  ~ Unif(0, t)		 (n known arrivals uniformly distributed in interval)
* Two Poisson processes with rates  $\lambda_1$ and $\lambda_2$ added is Poisson process, $\lambda = \lambda_1+ \lambda_2$
  * probability of type-1 arrival before type-2 is lam1 / (lam1 + lam2)
* ​


## Continuous Distributions

### Uniform

used with $F^{-1}$ for any CDF to generate $F$ through *universality of the Uniform*. 

#### Triangle

Sum of n iid Unif(a,b) distributions is Triangle(a,b,n)

### Normal 

Obtained by summing large numbers of independent distributions by central limit theorem

* Properties
  * **68-95-99.7% Rule** governs amount of data falling within 1,2,3 $\sigma$ of $\mu$ .
* Convergence
  * Bern(1/2) 	-> 	Y ~ N(1/2, 1/4n)
  * Pois(n) 		-> 	Y ~ N(n,n)
  * Gamma(n,l) 	-> 	Y ~ N(n/l , n / l$^2$ )
  * Bin(n,p) 		-> 	Y~ N(np, npq)
* Norm approx of Bin is used everywhere, works best when p~1/2, n\>\>1

#### Normal-Normal Conjugancy

Normal is the conjugate prior of the normal. i.e. estimate $\mu$ ~ N($\theta$ , $\tau^2$), then the posterior distribution of $\mu$ is normally distributed (complicated expression). 

#### Log-Normal

log of the r.v. has normal dist. so that Y ~ LN(u,s2) ~ e^X where X ~ N(u, s2)

### Multinomial

generalization of Binomial but can track multiple categories, not just yes/no. Creates random vector **X**.  $Mult_k(n,\bf{p})$.

​	$P(X_1=n_1, X_k=n_k) = \frac{n!}{n_1!n_2!…n_k!}p_1^{n_1}…p_k^{n_k}, \qquad n=\sum n_i$

* each $X_j$ is $Bin(n,p_j)$. 
* sum of any two variables in a Mult_k is $Bin(n,p_i +p_j)$

### Multivariate Normal

multi-dimensional generalization of Normal distribution. **X** has MVN if all linear combinations of $X_i$ has Normal dist. 

### Beta

generalization of Unif(0,1). parameters *a* and *b* so X~Beta(*a*,*b*). Can be constant, bell-shaped, skewed, or u-shaped.

* intuition
  * a,b < 1 gives u-shaped
  * a,b > 1 gives bell-shaped
  * a=b PDF symmetric
  * a>b gives values larger than 1/2, a<b smaller
  * Beta(1,1) = Unif(0,1)

#### Beta-Binomial Conjugancy

used to estimate parameter of Bin(n,p) distribution. 

​	if 		p ~ Beta(a,b)		where a,b contain our prior information

​	then 	X|p ~ Bin(n,p)	

​	and 	p|X = k~Beta(a+k,b+n-k)

### Gamma

waiting time until nth success of Poisson process. Gamma(1,$\lambda$ ) = Expo($\lambda$). continuous analog of NBin. 

​	Gamma(n, $\lambda$) ~ $\frac{\lambda^n}{\Gamma(n)}t^{n-1} e^{\lambda t}$

* represesnts the arrival times of events in Poisson process
  * sum (*convolution*) of Gammas is Gamma

####Exponential

Waiting time until 1st success. continuous counterpart to the *Geometric*.

​	$ f(x) = \lambda e^{-\lambda x}, \qquad x>0$ 

- properties
  - *memoryless* - only distribution with this property.
  - denotes waiting times of a *Poisson process*. 

#### Gamma-Poisson Conjugancy

Gamma is conjugate prior of Poisson, as it represents unknown *rate*.

​	if 		$\lambda$ ~ Gamma(r , b)		is arrival rate, r and b priors

​	then 	Y ~ NBin(r, b/(b+t))	y is # arrivals, t is waiting time

​	then 	$\lambda$|y ~ Gamma(r+y , b+t)	

#### Beta-Gamma Connection

​	if 		X ~ Gamma(a,$\lambda$) and Y ~ Gamma(b,$\lambda$) 

​	then 	X/(X+Y) ~ Beta(a,b)

​	and 	X+Y ~ Gamma

### Chi-Square

related to distribution of *sample variance*. 

sum of n squared N(0,1) distributions. Chi2(n) ~ Gamma(n/2, 1/2). 

### Student's-t 

if Z ~ N(0,1) and V ~ Chi2(n), 	then 	$T \sim \frac{Z}{\sqrt{V/n}}$    and    T ~ $t_n$ 

* Symmetric 	if T ~ $t_n$ then -T ~ $t_n$
* Cauchy ~ $t_1$ 
* $t_n\rightarrow$  N(0,1) as n $\rightarrow\infty$ 

#### Cauchy

- ratio of two iid Normals. 


- all moments do not exist (no $\mu$, $\sigma$ etc.)
- Student's-t with n=1

### Logistic

Simple CDF 

### Rayleigh

dunno?

### 