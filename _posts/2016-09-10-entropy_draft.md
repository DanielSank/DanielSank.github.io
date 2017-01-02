---
title: Entropy
excerpt: What it is, why it is, and how it works
header:
  overlay_image: header.png
comments: true
---

# Introduction/Welcome

# Probability of a particular sequence

Suppose we have a coin which, when flipped, has a probability <span>$$p$$</span> of giving heads and probability <span>$$q=1-p$$</span> of giving tails.
We flip the coin ten times and ask how likely it is that the first five results are heads and the last five are tails.
Representing heads with `X` and tails with `O`, we're asking for the probability of the sequence

```
XXXXXOOOOO  (I)
```

We might think that this arrangment is pretty unlikely.
Let's compare to another sequence:

```
XXOOOXOXXO  (II)
```

Sequence `II` might look a bit more random, so we might think that it's more likely than sequence `I`.
However, sequences `I` and `II` are actually equally (un)likely.

Consider sequence `I`.
In either case, the probability of the first coin flip being `X` is <span>$$p$$</span>, as is the probability of the second, third, four, and fifth flip.
Therefore, the probability of the first five flips giving `XXXXX` is <span>$$p^5$$</span>.
Similarly, the probability of the second five flips giving `OOOOO` is <span>$$q^5$$</span>, so the probability of sequence `I` is <span>$$p^5 q^5$$</span>.

Now consider sequence `II`.
Just like sequence `I`, each `X` ocurrs with probability <span>$$p$$</span> and each `O` ocurrs with probability <span>$$q$$</span>, so the probability of the sequence is again <span>$$p^5 q^5$$</span>.

The two sequences are equally probable!
The only thing affecting the probabilities here is the number of `X`'s and `O`'s; the order doesn't matter.

Interestingly, sequence `I` looks somehow "more organized" than `II`, and as such we might expect it to have had a lower probability.

# Probability of a class of sequences

Now, instead of considering the probabilities of specifc individual sequences, let's consider the probabilities of two classes of sequences.
We'll see that while classes of sequences can have very different probabilities.

## Half `X`, half `O`

First, consider the class of sequences in which there is an equal number of `X`'s and `O`'s, e.g.

```
0010111001, or 0000101111, or 1101101000, ...
```

Let's also go to the more general case of <span>$$N$$</span> coin tosses.
The probability of any *particular* such sequence is <span>$$p^{N/2} q^{N/2}$$</span>, but we have to take into account the fact that there are many such sequences.
In fact, we can re-arrange our `X`'s and `O`'s in any order without changing the fact that half are `X` and half are `O`; that gives <span>$$N!$$</span> arrangements.
That's overcounting though, because swapping e.g. two `X`'s isn't actually a new arrangement.
We have to divide by those overcountings.
There are <span>$$(N/2)!$$</span> ways to rearrange the `X`'s amongst themselves, and similarly for the `O`'s, so the total number of arrangements, denoted <span>$$\Omega$$</span>, with <span>$$N/2$$</span> `X`'s is
<div>
$$
\Omega(N/2) = \frac{N!}{(N/2)! (N/2)!}
$$
</div>
and the probability of getting any of those arrangements is
<div>
$$
P(N/2) = p^{N/2} q^{N/2} \Omega(N/2) =
p^{N/2}q^{N/2} \frac{N!}{(N/2)! (N/2)!} \, .
$$
</div>

For <span>$$N=10$$</span> and <span>$$p=q=1/2$$</span>, we get
<div>
$$
\Omega(N/2) = 252 \qquad P(N/2) \approx 0.25 \, .
$$
</div>

## All `X`'s

Now consider the class of sequences with all `X`s, i.e.

```
XXXXXXXXXX
```

There's only one such sequence, so <span>$$\Omega(N)=1$$</span>, and the probability of getting it is <span>$$P(N) = q^N$$</span>.
For <span>$$N=10, p=q=1/2$$</span>, this gives <span>$$P(N) \approx 0.000977$$</span>.

We see that there is a much higher probability to get half `X`'s and half `O`'s than there is to get all `X`'s.
Not that this isn't because `X`'s are easier to get; in both cases we put <span>$$p=q$$</span>.
The case with half `X`'s and half `O`'s is more probably because there are so many different ways to get the half/half situation.
In other words, <span>$$\Omega(N/2) \gg \Omega(N)$$</span>.

# Entropy (and other vocabulary)

The coin flipping example illustrates the essential idea of entropy.
Entropy is the number of ways a physical or mathematical system can be arranged while satisfying a given set of descriptions or *constraints*.
In the coin flip example, our constraints were the total number of `X`'s.
We saw that certain total numbers of `X` can happen many more ways than others, i.e. <span>$$\Omega(N/2) \gg \Omega(N)$$</span>.

In the physics community, each way the system can be arranged is called a **microstate**.
The name makes sense because in physics we'd be talking about all the possible arrangements of the microscopic constituents of the system.
A set of constraints is called a **macrostate**.
That name also makes sense, because things like the total number of gas atoms in a container is something we can actually measure with macroscopic instruments.

Given a set of constraints defining a macrostate, the **entropy** is the logarithm of the the number of microstates satisfying those constraints.


# Definition

* Linear in number of system constituents

* Concatenating systems: add entropy


# Random walk

Random walk (chain of spins).
Show number of walks which wind up in center is very large.
Strongly peaked.
Similarly, magnetization centered near zero, very sharp.
Macroscopic variable: highly degenerate function of microstate.

# Statistical mechanics

* Previous item more or less proves second law, but you have to understand what it means.
"Entropy maximized" means the macroscopic variable is such that the degeneracy is as large as  possible, i.e. most microstates.

# Temperature

* Systems in contact

* Lagrange multiplier



# Beans

Suppose you have ten beans, half black and half white, all in a line.
You shake up the beans so that they land in random order and I ask you, is it likely that all the black beans are on the left and all the white beans are on the right, like this:

```
BBBBBWWWWW   (A)
```

It's pretty intuitive that the answer is "no, that's not likely".
Now suppose I ask for the probability that the beans wind up arranged like this

```
WWBBWBWBBW   (B)
```

The second situation may look more likely because it kind of looks "more random".
Let's see if that's right; how likely *are* these two situations?
There are ten slots for beans.
Assuming that shaking the beans results in each bean landing in a random spot, we can compute the probability of each arrangement as follows.
Consider the slots occupied by black beans.
Place the black bens in those slots one at a time, each time noting the probability of the occupant of that slot being a black bean.
For the first slot, we have 5 black beans and ten total, so the probabiliy that the slot gets a black bean is <span>$$5/10$$</span>.
For the second slot, we have four black beans left and nine total, so the probability is <span>$$4/9$$</span>.
Multiplying all the probabilities for the black bean slots in this way gives
<div>
$$P_A = \underbrace{\frac{5}{10}}_\text{slot 1} \times \frac{4}{9} \times \frac{3}{8} \times \frac{2}{7} \times \underbrace{\frac{1}{6}}_\text{slot 5}$$
</div>


