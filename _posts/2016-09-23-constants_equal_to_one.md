---
title: Physical constants are not equal to one
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
Dropping the <span>$$c$$</span>'s is typically defended with a statement like
<div>$$ \text{We work in units wherein }c=1 \, . \tag{*}\phantom{*}$$</div>
In this article, we will discuss why saying <span>$$c=1$$</span> is confusing, explain how to rationalize it.

## Dimensions and units

A dimension is a class of physical quantity, such as length, time or charge.
Quantities of the same dimension can be added, i.e. the distance from me to my strawberries can be added to the distance from my strawberries to the moon.
Quantities of different dimensions cannot be added, i.e. it doesn't make sense to add my age to my height.

In most cases, the symbols we see in physics equations represent quantities with dimensions.
For example, in the Lorentz transformation equations, <span>$$c$$</span> has dimensions of velcity, i.e. length over time.

A unit is a granulation or "scale" of a dimension.
For example, one second is a unit for the dimension of time.

Dimensions and units are different!
The speed of light has dimensions of velocity, but it doesn't have any particular units.
We can specify the numerical value of the speed of light in various units, e.g. the speed of light, in units of meters per second, is three hundred million.
In math notation, that is
<div>
$$c = 3 \cdot 10^{8} \times \, \text{meter}/\text{second} \, .$$
</div>
While <span>$$c$$</span> has dimensions of velocity, we can define a new symbol
<span>$$c_\text{m/s} \equiv_\phantom{a} c / (\text{meter / second})$$</span> which refers to the dimensionless number giving <span>$$c$$</span> in units of meters per second.
We could say that <span>$$c_\text{m/s} \phantom{.}_\phantom{.}$$</span> is the speed of light written "in units of meters and seconds".

## Physics equations are not written "in units"

We usually think of the quantities in physics equations as things with dimensions.
In the equation
<div>
$$t' = \gamma \left( t - vx/c^2 \right) \, ,$$
</div>
we think of <span>$$c$$</span> as a velocity, and <span>$$x$$</span> as a length.
Therefore, it's awkward to talk about writing equations "in units".
Now, we *could* do as described above and redefine our symbols to actually mean the numerical values of physical quantities expressed in certain units, and we *could* pick those units such that in those units ,the numerical value of <span>$$c$$</span> is 1.
For example, we could choose a length unit of lightyear and a time unit of year, defining symbols:
<div>
$$
\begin{align}
x_\text{ly} & \equiv x / \left( \text{1 lightyear} \right) \phantom{.}_\phantom{.} \\
v_\text{ly/y} & \equiv v / \left( \text{1 lightyear / year} \right) = v / c \phantom{.}_\phantom{.} \\
t_\text{y} & \equiv t / \left( \text{1 year} \right) \phantom{.}_\phantom{.} \\
c_\text{ly/y} & \equiv c / \left(\text{1 lightyear / year} \right) = 1 \phantom{.}_\phantom{.}
\end{align}
$$
</div>
in which case the Lorentz transformation becomes
<div>
$$t'_\text{y} = \gamma \left( t_\text{y} - v_\text{ly/y} x_\text{ly} \right) \, . \tag{3}$$
</div>
This is the only way I can think of to arrive at a version of the Lorentz transformations in which the statement, that we're working "in units where <span>$$c=$$</span> 1" makes sense.
We've gotten rid of the <span>$$c$$</span>'s, but at a strange cost.
Our symbols now stand for dimensionless numbers, the numerical part of the various physical quantities expressed in a particular system of units.
There's nothing wrong with this in principle; it's perfectly reasonable to write equations involving numbers, but I find thinking of physics equations as relations between numbers confusing because numbers lack structure.
For example, suppose we'd like to get an idea of how <span>$$t'$$</span> depends on the speed of light.
Starting from Equation (3), we reason as follows:

* If the speed of light increases by a factor of <span>$$a$$</span>, then the distance light travels in a year increases by <span>$$a$$</span>.
Therefore, the "ly" unit is larger, so for a given length <span>$$x$$</span>, the *number* <span>$$x_\text{ly}$$</span> is lower by a factor of <span>$$a$$</span>.<span>$$\phantom{.}_\phantom{.}$$</span>

* By similar reasoning, <span>$$v_\text{ly/y}$$</span> is reduced by a factor of <span>$$a$$</span>.

* Therefore, 

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
