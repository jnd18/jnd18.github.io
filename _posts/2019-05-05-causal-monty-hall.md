---
layout: post
title: The Monty Hall Paradox Through a Causal Lens
---

I've recently finished reading Pearl and Mackenzie's *The Book of Why: The New Science of Cause and Effect*. 
In the chapter on paradoxes, the book discusses the famous Monty Hall problem, but with a twist.
Rather than basing their analysis of the problem solely on probability theory, they show how formal causal reasoning can elucidate why most people find it so confusing.
I found this discussion so illuminating that I'd like to share it here, in my own words.

## The Monty Hall Problem
The Monty Hall problem is a classic 'paradox' of probability theory. 
While the problem was originally stated and solved by Steve Selvin in 1975, it became famous in 1990, when it appeared as a reader question in Marilyn vos Savant's magazine column:

> Suppose you're on a game show, and you're given the choice of three doors: 
> Behind one door is a car; behind the others, goats. You pick a door, say No. 1,
> and the host, who knows what's behind the doors, opens another door, say No. 3, 
> which has a goat. He then says to you, "Do you want to pick door No. 2?" Is it to your advantage to switch your choice? 

Vos Savant correctly answered (subject to some reasonable assumptions) that if you switch doors,
you have a 2/3 chance of winning the car, and if you don't switch you only have a 1/3 chance of winning the car.
This is called a paradox because most people have a strong intution that both of the remaining doors have a 1/2 chance of hiding the car.
In fact, in response to Vos Savant's correct answer and explanation, thousands of fans wrote in, many of them with PhDs in technical fields, to tell her that she got it wrong!
After all, if we already know that the host is going to open a door and reveal a goat, what can that possibly tell us?
Once there are two doors left, why should it be the one that you did not pick which has a higher chance of holding the car?
It is as if the showrunners are somehow reading your mind and putting the car behind the door you did not initially pick.

The clearest and simplest explanation of the solution that I have seen comes from Cecil Adams' column *The Straight Dope*. 
She writes:

> "You pick door #1. Now you're offered this choice: open door #1, or open door #2 and door #3.
> In the latter case you keep the prize if it's behind either door.
> You'd rather have a two-in-three shot at the prize than one-in-three, wouldn't you? If you think about it,
> the original problem offers you basically the same choice.
> Monty is saying in effect: you can keep your one door or you can have the other two doors,
> one of which (a non-prize door) I'll open for you." 

Now for the aforementioned assumptions.
This reasoning is correct if the host always opens a door with a goat behind it.
If the host opens a door completely at random (potentially revealing the car), then there is no benefit to switching. More on that later.
If the host is allowed to do whatever he wants with his knowledge of what's behind the doors, then all bets are off.
The problem as stated above doesn't fully specify the behavior of the host, so it is technically ambiguous. 
But I think most people do tend to assume that the host always opens a door with a goat behind it, and the confusion does not result from misunderstanding the problem.
Rather, the problem has an interesting causal structure that tends to violate most people's causal intuition.

## An Introduction to Causal Diagrams

We can represent causal information about a problem as a diagram. 
First we write down all the relevant variables, and then we draw arrows connecting the variables to represent direct causes. 
For example, $A \to B$ means that $A$ causes $B$.
I say "direct causes" above because in a situation like $A \to B \to C$, then $A$ does cause $C$ despite there being no arrow from $A$ to $C$.
$A$ does not directly cause $C$, however. $A$ only causes $C$ through its effect on $B$.
For simplicity, we require that there are no loops; basically, we require that causality flows in one direction always.
This type of diagram is known as a directed acyclic graph.

With only two variables, there are really only two possible graphs: $A \to B$ and $A \phantom{\to} B$.
Either one of them causes the other, or they are not causally related.

With three variables, things get much more interesting.
A three variable graph with two arrows is called a junction. 
Junctions are the basic building blocks of all causal diagrams.
There are three kinds of junctions.
The first kind is called a chain. 
It looks like $A \to B \to C$.
Sometimes we call $B$ the mediator of the effect of $A$ on $C$.
As an example, let $A$ be "eating limes", $B$ be "getting vitamin C", and $C$ be "not having scurvy."
Then $A$ causes $C$ (eating limes prevents scurvy), but only through $B$ (because limes contain vitamin C, and scurvy is caused by a vitamin C deficiency).
There is no direct effect of $A$ on $C$ in this example because if we somehow removed all of the vitamin C from a lime 
(say by cooking it away, as many misguided sailors did), then eating it would do nothing to prevent scurvy.
Lastly, if we control for $B$, then $A$ and $C$ become independent. In our example, this means that once we know how much vitamin C a person has, 
lime consumption no longer has any relationship with scurvy.
For example, once we know a person has low vitamin C, it makes no difference whether it is because they are not eating limes or because they cannot absorb
the vitamin C from the limes they do eat. They are at risk of scurvy all the same.
Similarly, whether a person has high vitamin C from eating limes or from eating oranges is irrelevant when assessing their risk of scurvy.

The second kind of junction is called a fork.
It looks like $A \leftarrow B \to C$.
In this situation $B$ is called a confounder.
As an example, let $A$ be height, $B$ be gender, and $C$ be income.
The idea is that being a man makes you both taller and more likely to earn more money.
If we look just at height and income, we will see that being taller is associated with having a higher income, even though this association is not causal.
Not only is there no arrow from height to income, there's not even a path from one to the other (as there was from $A$ to $C$ in the chain junction).
As in the case of a chain, controlling for $B$ makes $A$ and $C$ independent.
So, once we look at men and women separately, height and income have no relationship.
(If this causal diagram reflects reality accurately, that is. Of course, there may be some other way height is associated with income.)
Even though controlling for $B$ has the same effect as in a chain (de-associating $A$ and $C$), the result has a very different character.
If we are trying to study the effect of height on income, then gender is just getting in our way, and we should definitely control for it to remove its confounding effect.
On the other hand, if we are trying to study the effect of limes on scurvy, we probably don't want to control for vitamin C, since that would control away the effect of the limes.
Now, if we want to know the direct effect of limes on scurvy, or we are searching for the mechanism by which limes prevent scurvy, then we might want to control for vitamin C.
The point is that it can be a mistake to control away part of what you are trying to study (a mediator), but it is always a good idea to control for confounding variables.

The final kind of junction is called a collider.
It looks like $A \to B \leftarrow C$.
This is perhaps the most interesting junction because controlling for $B$ has precisely the opposite effect compared to the other two types of junctions.
Without controlling for $B$, $A$ and $C$ have no association. But once we control for $B$, we introduce a spurious association!
For example, suppose that $A$ is beauty, $B$ is "you've dated this person", and $C$ is kindness.
Then the collider $A \to B \leftarrow C$ means that beauty and kindness are unrelated in the general population, but each has an effect on whether or not you'd date a person.
Perhaps, you'd date anyone who was kind or beautiful or both, but you wouldn't date anyone who was ugly and mean.
Then, looking back on the people you've dated (conditioning on $B$), you find that more beautiful people tend to be meaner, and uglier people tend to be nicer.
But this is purely an artifact of the way you choose to date people.
Colliders can be tricky because we tend to think that controlling for more variables can only give us a more accurate picture.
This is certainly true for confounders, and even in chains, controlling for the mediator does correctly give us a more fine-grained picture of the direct effect of $A$ on $C$.
But controlling for $B$ in a collider is purely a mistake. 
One of the great insights of formal causal inference was this discovery that sometimes controlling for more variables is a bad thing.

## The Causal Structure of the Monty Hall Problem

The Monty Hall problem has three variables of interest.
$A$ is "the door we pick", $B$ is "the door Monty Hall reveals a goat behind", and $C$ is "the door the car is behind."
Assuming that no one is cheating, the door we pick and the door the car is behind are independent.
But both affect the door that Monty opens, since he cannot open the door we picked, nor can he open the door the car is behind.
Thus, the problem looks like $A \to B \leftarrow C$.
We have a collider!
Once Monty reveals a goat, we have conditioned on $B$, so this introduces a spurious association between $A$ and $C$.
Even though this association is non-causal, it is real, and we can exploit it to increase our chances of getting the car.

As Pearl and Mackenzie argue, this collider structure is the reason why the problem is so unintuitive to most people.
Humans are generally very good at causal inference.
But humans also generally believe that two variables which are not causally related can only appear associated because of the presence of confounding variables.
So most people know, intuitively, that the door they pick and the door the car is behind are independent.
Then we gain more information from the door Monty opens, which clearly hasn't introduced any confounding variable into the situation.
So we should still have independence, right? And all we can say is that the car is equally likely to be behind either door.
But no! As we've just seen, variables can become spuriously associated by controlling for a third one.
So the association appears to come out of nowhere, which is deeply disturbing.
I found this explanation very satisfying.

As I mentioned earlier, if Monty randomly opens a door other than yours, possibly revealing the car, then there is no advantage to switching.
We can see this directly from the causal diagram, which I find neat.
Now $A$ (the door we picked) still affects which door Monty can reveal, but $C$ (the door the car is behind) has no effect on Monty.
So there is no collider structure, and conditioning on $B$ does nothing to relate $A$ and $C$.
Thus, we have no reason to believe switching is better.

As an interesting final note, researchers have noticed that pigeons, when exposed to the problem, can quickly figure out that switching is the optimal strategy,
unlike humans who will insist that switching makes no difference.
Perhaps this is because pigeons have such a limited capacity for causal reasoning that the problem does not violate their intuition at all.




