# Modeling pandemics subject to stochastic uncertainties -- A polynomial chaos approach

The so-called [SEIR model](https://epubs.siam.org/doi/abs/10.1137/s0036144500371907) is commonly used to model the outbreak of pandemics.
The plain SEIR model consists of four differential equations, modeling the dynamics of *s*usceptible, *e*xposed, *i*nfected, and *r*ecovered people.
Undeniably, a portion of infected people needs intensive care.
To account for this fact variants of the model exist, [see for instance here for the current Covid-19 pandemic (German)](https://www.dgepi.de/assets/Stellungnahmen/Stellungnahme2020Corona_DGEpi-21032020-v2.pdf), or [here (German)](https://www.rki.de/DE/Content/InfAZ/N/Neuartiges_Coronavirus/Modellierung_Deutschland.pdf?__blob=publicationFile), or [here (English)](https://www.imperial.ac.uk/media/imperial-college/medicine/sph/ide/gida-fellowships/Imperial-College-COVID19-NPI-modelling-16-03-2020.pdf).
As with every mathematical model there are parameters that need to be chosen.
Usually, not precise figures exist.
Hence, uncertainty quantification can play a vital role.

This repository contains Julia code and a [documentation](doc/doc.pdf) to show how [polynomial chaos expansion](https://en.wikipedia.org/wiki/Polynomial_chaos) can help quantify uncertainties for the SEIR model.

*Note: This is work in progress and the code will be published soon.* 
