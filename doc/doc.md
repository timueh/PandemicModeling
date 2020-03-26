# Deterministic equations

The so-called
<span data-acronym-label="seir" data-acronym-form="singular+short">seir</span>
model is often used to model pandemics. Assuming no births or deaths,
the dynamics can be modelled in the form of a system of ordinary
differential equations

<span id="eq:SEIR_dynamics" label="eq:SEIR_dynamics">\[eq:SEIR\_dynamics\]</span>
\[\begin{aligned}
    \diff{S}{t} &= - \frac{R_0}{t_{\text{inf}}N} \, SI, && S(0) = S_0 \geq 0, \\
    \diff{E}{t} &= \frac{R_0}{t_{\text{inf}}N} SI- \frac{E}{t_{\text{lat}}}, && E(0) = E_0 \geq 0, \\
    \diff{I}{t} &= \frac{E}{t_{\text{lat}}} - \frac{I}{t_{\text{inf}}}, && I(0) = I_0 \geq 0, \\
    \diff{R}{t} &= \frac{I}{t_{\text{inf}}}, && R(0) = R_0 \geq 0. \end{aligned}\]

The meaning of the parameters of the
<span data-acronym-label="seir" data-acronym-form="singular+short">seir</span>
model is explained in .

<div id="tab:SEIR_parameters">

| Name               | Meaning                   |
| :----------------- | :------------------------ |
| \(N\)              | Total population          |
| \(R_0\)            | Basic reproduction number |
| \(t_{\text{inf}}\) | Infectious period         |
| \(t_{\text{lat}}\) | Latent period             |

Parameters for
<span data-acronym-label="seir" data-acronym-form="singular+short">seir</span>
model [\[eq:SEIR\_dynamics\]](#eq:SEIR_dynamics).<span id="tab:SEIR_parameters" label="tab:SEIR_parameters">\[tab:SEIR\_parameters\]</span>

</div>

In addition to the
<span data-acronym-label="seir" data-acronym-form="singular+short">seir</span>
model, we would like to model the number of people in need of intensive
care (\(IN(t)\)), for which we introduce another two equations (which we
call
<span data-acronym-label="icu" data-acronym-form="singular+short">icu</span>
system)

<span id="eq:ICU_dynamics" label="eq:ICU_dynamics">\[eq:ICU\_dynamics\]</span>
\[\begin{aligned}
        \diff{L}{t} &= \frac{\beta}{t_{\text{lat}}} \, E- \frac{L}{t_{\text{lag}}}, && L(0) = L_0 \geq 0, \\
        \diff{IN}{t} &= \frac{L}{t_{\text{lag}}} - \frac{IN}{t_{\text{lay}}}, && IN(0) = IN_0 \geq 0.
    \end{aligned}\]

Reading the system [\[eq:ICU\_dynamics\]](#eq:ICU_dynamics) bottom-up,
we see that the number of people in intensive care decreases according
to the average lay time \(t_{\text{lay}}\), and increases according to
the average lag time \(t_{\text{lag}}\). The fictitious
compartment \(L(t)\) models the people who are transitioning from the
infected compartment (\(I(t)\)) to the intensive-care
compartment (\(IN(t)\)).

The meaning of the parameters of the
<span data-acronym-label="icu" data-acronym-form="singular+short">icu</span>
model is given in .

<div id="tab:ICU_parameters">

| Name               | Meaning                                            |
| :----------------- | :------------------------------------------------- |
| \(\beta\)          | Fraction of infected people needing intensive care |
| \(t_{\text{lag}}\) | Lag period from infection to intensive care        |
| \(t_{\text{lay}}\) | Period of hospitalization                          |

Parameters for
<span data-acronym-label="icu" data-acronym-form="singular+short">icu</span>
model [\[eq:ICU\_dynamics\]](#eq:ICU_dynamics).<span id="tab:ICU_parameters" label="tab:ICU_parameters">\[tab:ICU\_parameters\]</span>

</div>

# Introducing uncertainty

A key issue with both the
<span data-acronym-label="seir" data-acronym-form="singular+short">seir</span>
model and the
<span data-acronym-label="icu" data-acronym-form="singular+short">icu</span>
model is parametric uncertainty: the precise numerical values of the
parameters from either or are not known. To account for this uncertainty
explicitly, we can model the parameters as random variables. For
instance, \[\begin{aligned}
    \mathsf{R_0} \sim \mathcal{N}(\mu_{R_0}, \sigma_{R_0})\end{aligned}\]
means to model the basic reproduction rate as a Gaussian random variable
with mean \(\mu_{R_0}\) and standard deviation \(\sigma_{R_0}\).

What is the effect of this uncertainty on the solution of the
<span data-acronym-label="seir" data-acronym-form="singular+short">seir</span>-<span data-acronym-label="icu" data-acronym-form="singular+short">icu</span>
model? One way to study this effect is to do Monte Carlo simulation:

1.  draw samples of the random variable,

2.  solve the respective system of differential
    equations [\[eq:SEIR\_dynamics\]](#eq:SEIR_dynamics) &
    [\[eq:ICU\_dynamics\]](#eq:ICU_dynamics),

3.  and repeat.

Another way is to use
<span data-acronym-label="pce" data-acronym-form="singular+short">pce</span>,
a method that is to a random variable what a Fourier series is to a
periodic signal: an orthogonal decomposition. This method allows to
propagate uncertainties through differential equations in a single shot.
By that we mean the following

1.  introduce
    <span data-acronym-label="pce" data-acronym-form="singular+short">pce</span>
    for all uncertaint quantities,

2.  derive a new set of equations via so-called Galerkin projection, and

3.  solve this new system *once*.

The advantage of
<span data-acronym-label="pce" data-acronym-form="singular+short">pce</span>
over Monte-Carlo is that no sampling is required whatsoever; by solving
the new set of equations, all statistical information are available such
as expected value and/or standard deviations over time.
