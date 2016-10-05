---
title: Stop saying you work in units where constants are equal to one.
excerpt: In which Dan rants about how to improve a common, but confusing, phrase.
header:
  overlay_image: header.png
---

<div> $$\renewcommand{\ket}[1]{\left \lvert #1 \right \rangle}$$</div>

Most of the difficulty in learning physics comes from poor use of language and bad notation.
In this post, we look at a particularly common class of phrases used by physicists which I observe to confuse everyone from students to veterans.

The Lorentz transformation equations are
<div>
\begin{align}
t' &= \gamma \left( t - \frac{v x}{c^2} \right) \\
x' &= \gamma \left( x - v t \right) \tag{1} \\
\gamma &= \left( 1 - \left( \frac{v}{c} \right)^2 \right)^{-1} \, .
\end{align}
</div>
However, many physicists, including book authors, prefer to write them as
<div>
\begin{align}
t' &= \gamma \left( t - v x \right) \\
x' &= \gamma \left( x - v t \right) \tag{2} \\
\gamma &= \left( 1 - v^2 \right)^{-1} \, ,
\end{align}
</div>
i.e. without the <span> $$c$$ </span>'s.
The act of dropping the <span>$$c$$</span>'s is typically defended with a statement like
<div>$$ \text{We work in units wherein }c=1 \, . $$</div>
That statement is utter nonsense.
The same nonsense appears in other branches of physics: for example, some authors write the Schrodinger equation
<div>
$$i \hbar \frac{d}{d} \ket{\Psi(t)} = H \ket{\Psi(t)}$$
</div>
without the <span>$$\hbar$$</span>, as
<div>$$i \frac{d}{dt} \ket{\Psi(t)} = H \ket{\Psi(t)} \, ,$$</div>
with the statement that they've "set <span>$$\hbar=1$$</span>".


## Units and dimensions are different

A dimension is a kind of physical quantity such as length, time or charge.
Quantities of the same dimension can be added, i.e. the distance from me to my strawberries can be added to the distance from my strawberries to the moon.
Quantities of different dimensions cannot be added, i.e. it is nonsense to add my age to my height.

A unit is a granulation of a dimension.
For example, one second is a unit of time.
A quantity with the dimension of time can be measured in the units of seconds.

Units and dimensions are completely different things.
My age is a time, but my age doesn't have any particular units.
We can specify my age in a particular unit: my age in years is 31.
Note in particular that physical constants such as <span>$$\hbar, \, k_b,$$</span> and <span>$$c$$</span> have dimensions, but not units.
Those constants do have particular numerical values once a set of units is chosen, but the constants themselves exist independently of any units.

Take a look at the first line in Equations (2) where we have the phrase <span>$$t - vx$$</span>.
That phrase looks like nonsense, because <span>$$t$$</span> has dimensions of time while <span>$$vx$$</span> has dimensions of length squared over time.


## Physics equations are not written "in units"

Neither the Lortentz transformations, nor the Schrodinger equation, nor any other physics equation is usually written in any particular set of units.
In the Lorentz transformations, <span>$$c$$</span> means "the speed of light", not e.g. "the speed of light in fathoms per fortnight".
For this reason alone, it is utter nonsense to say that we write the Lortentz transformations or any other equations "*in units* where ...".


Now, we *could* redefine our symbols to actually mean the numerical values of physical quantities expressed in certain units.
For example, we could choose a length unit of lightyear and a time unit of year, and then redefine our symbols as follows:
<div>
$$
\begin{align}
x:& \quad \text{length / 1 lightyear} \\
v:& \quad \text{velocity / speed of light} \\
t:& \quad \text{time / 1 year}
\end{align}
$$
</div>


## So what's really going on?

When we write the Schrodinger equation as in Equation (2), we've really *divided both sides of Equation (1) by* <span>$$\hbar$$</span> *and redefined* <span>$$H$$</span> to mean <span>$$H/\hbar$$</span>.


## Saying that constants are equal to 1 is *very* confusing


## There is a case where we write equations "in units"

Consider the equation for the zero point fluctuation of the flux in a quantum mechanical LC oscillator
<div>
$$\Phi_\text{zpf}^2 = \frac{\hbar}{2}Z$$
</div>
where <span>$$Z = \sqrt{L/C}$$</span> is the characteristic impedance of the oscillator.
For a metrologist who thinks about their flux-ometer in units of Webers, it's convenient to define <span>$$\phi_\text{zpf} \equiv \Phi_\text{zpf} / 1\,\text{Weber}$$</span>, <span>$$z \equiv Z/1 \Omega$$</span>, and then rewrite the equation as
<div>
$$\phi_\text{zpf}^2 = z \cdot 1.05 \times 10^{-34} \, . $$
</div>
This new dimensionless form is convenient if you want to get numbers in the SI system of units.
Note that the set <span>$$\hbar = 1$$</span> "method" wouldn't help us here.

Now let's do the same thing but using the approach wherein we explicitly rescale our variables.
Define <span>$$\phi_\text{zpf} \equiv \Phi_\text{zpf} / \Phi_0$$</span> where <span>$$\Phi_0 \equiv h / 2e$$</span> is the [flux quantum](https://en.wikipedia.org/wiki/Magnetic_flux_quantum).
Also define the resistance quantum <span>$$R_K \equiv h / e^2$$</span> and <span>$$z \equiv Z_{LC} / R_K$$</span>.
Then
<div>
$$\phi_\text{zpf}^2 = \frac{z}{\pi} \, .$$
</div>
I like this because there aren't any crazy powers of ten lying around.
In essence, rather than pick the somewhat arbitrary SI system of untis, we invented our own system based on the flux and resistance quanta.
This is a good idea because the values of relevant quantities like <span>$$\phi_\text{zpf}^2$$</span> will generally be of order 1.
We only have to remember a few important scales e.g. <span>$$R_K = 25.8 \, \text{k}\Omega$$</span>.
From that, we easily see that an oscllator with <span>$$Z_{LC} = 50 \, \Omega$$</span> impedance has a zero point flux fluctuation of
<div>
$$\phi_{zpf} = \sqrt{50/25,800/\pi} = 0.016$$
</div>
or in other words, the zero point motion is about 1.6% of a flux quantum.
I like this because the flux quantum is a natural scale in experiments with the quantum LC oscillator.
