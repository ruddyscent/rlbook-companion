# Exercise 3.1: Three Example MDP Tasks

The Markov decision process (MDP) framework describes an interaction between an
agent and an environment. At each time step, the agent observes a state, chooses
an action, receives a reward, and moves to a next state according to the
environment dynamics. Below are three different example tasks that can be
modeled this way.

## 1. Warehouse Robot Navigation

In this task, an autonomous robot moves through a warehouse to pick items from
shelves and deliver them to a packing station.

**States:** A state could include the robot's current grid location, its battery
level, whether it is carrying an item, the location of the requested item, the
positions of nearby obstacles or workers, and the current queue of pending
orders.

**Actions:** The robot's actions might be to move north, south, east, or west;
stay still; pick up an item; drop off an item; or go to a charging station.

**Rewards:** The robot could receive a positive reward for successfully
delivering an item, a small negative reward for each time step to encourage
efficiency, a larger negative reward for collisions or unsafe proximity to
workers, and a negative reward for running out of battery before completing the
task.

This is a fairly standard MDP example because the state can be represented
physically, the actions are concrete, and the rewards are closely tied to task
performance.

## 2. Personalized Medical Treatment Planning

In this task, an agent recommends treatment decisions for a patient over time,
for example adjusting medication dosage for a chronic condition.

**States:** A state could include the patient's recent test results, symptoms,
age, weight, current medications, treatment history, side effects, and relevant
risk factors. In practice, the true physiological state is only partially
observed, so the observed state would be an imperfect summary of the patient.

**Actions:** The actions could include increasing a dose, decreasing a dose,
keeping the treatment unchanged, switching to a different medication, ordering
an additional test, or scheduling a follow-up visit.

**Rewards:** Rewards could reflect improved health indicators, symptom
reduction, fewer side effects, lower treatment cost, and avoidance of dangerous
events such as hospitalization. A severe negative reward could be assigned to
harmful outcomes.

This example differs from the warehouse robot because the environment is
biological, uncertain, and ethically constrained. The reward is also not just a
simple measure of immediate success; it must balance long-term health, safety,
comfort, and cost.

## 3. Interactive Storytelling Assistant

In this task, an AI assistant collaboratively writes a story with a human user.
At each step, it chooses how to continue the story or how to ask the user for
input.

**States:** A state could include the story so far, the genre, known characters,
open plot threads, the user's previous preferences, the current emotional tone,
and an estimate of whether the user seems engaged. Since the full state of the
user's imagination and preferences is not directly observable, the state would
be a constructed representation rather than a fully measurable physical state.

**Actions:** The assistant's actions might include adding a plot event,
developing a character, asking the user a question, resolving a conflict,
introducing a new setting, changing the tone, or ending the story.

**Rewards:** Rewards could be based on explicit user feedback, continued user
engagement, coherence of the story, novelty, emotional impact, and whether the
assistant respects the user's stated constraints. Negative rewards could be
given for contradictions, boring continuations, unwanted tone shifts, or content
that violates the user's preferences.

This example stretches the MDP framework. The "state" is not an objective
physical configuration, and the reward is difficult to define precisely because
story quality and user satisfaction are subjective. The Markov property is also
questionable: the best next action may depend on subtle details from the whole
conversation, not just a compact state summary. Nevertheless, it can still be
treated approximately as an MDP if we define the state representation broadly
enough and accept that the model is an abstraction.

## Summary

These three examples show how flexible the MDP framework is. The warehouse robot
task is a concrete physical-control problem, the medical treatment task is a
high-stakes sequential decision problem under uncertainty, and the storytelling
assistant is a subjective human-interaction problem that pushes the limits of
what counts as a state and a reward.

# Exercise 3.2: Adequacy of the MDP Framework

The MDP framework is very broad and is adequate for representing many
goal-directed learning tasks. If an agent repeatedly interacts with an
environment, chooses actions, receives rewards, and tries to improve its future
outcomes, then the task can often be described as an MDP.

However, this does not mean that the MDP representation is always simple,
natural, or practically useful. To represent a task as an MDP, the state must
contain all information relevant to predicting future rewards and next states.
If the chosen state representation omits important information from the past,
then the Markov property fails.

For example, a partially observed task may not be well represented as an MDP
using only the current observation. Suppose a robot has sensors that cannot see
behind a wall. Its best action may depend on something it saw a few moments ago,
not just on its current camera image. The underlying world may still be Markov,
but the robot's observation is not. In that case, a partially observable MDP
(POMDP), or an augmented state including memory or belief over hidden states,
would be more appropriate.

Another difficult case is a task in which the reward itself is unclear or
changes over time. For instance, a human may learn a skill while also changing
their goals, preferences, or definition of success. This can still sometimes be
forced into the MDP framework by expanding the state to include the person's
current preferences, but the model may become artificial and hard to use.

A more extreme exception would be a learning problem without a stable
environment or stable objective. If the rules of the task, the available
actions, and the meaning of reward are all changing in ways that are not part of
the state, then the standard MDP framework is not an adequate direct
representation.

Thus, the MDP framework is best viewed as a powerful abstraction rather than a
perfect description of every goal-directed learning problem. It is often
adequate if we are willing to define the state broadly enough, but clear
exceptions arise when the agent has partial observability, hidden history
dependence, changing goals, or nonstationary dynamics that are not captured in
the state.

# Exercise 3.3: Where to Draw the Agent-Environment Boundary

There is no single fundamentally correct level at which to draw the boundary
between the agent and the environment. The choice depends on the purpose of the
model, the available observations and controls, and the level at which learning
is intended to occur.

In the driving example, defining actions as accelerator, brake, and steering
commands is often natural. These are the controls available to a human driver,
and they are also close to the control interface of many driving systems. At
this level, the agent does not need to model every muscle contraction or every
tire-road interaction directly. Those details can be treated as part of the
environment dynamics.

If actions are defined at a lower level, such as muscle activations, then the
agent's problem becomes much more complex. It must learn not only how to drive,
but also how to move the body in order to operate the car. This may be useful if
the scientific question is about motor control, but it is unnecessarily detailed
if the goal is to study driving behavior.

If actions are defined farther out, such as tire torques, then the model may be
appropriate for an automated vehicle controller. This level avoids modeling the
human body and the pedals, but it requires direct control over the vehicle's
mechanical systems. It is a good boundary only if those are actually the actions
available to the agent.

At a higher level, actions could be choices such as "drive to the office" or
"take the highway." This may be appropriate for a route-planning agent, but it
hides the lower-level control problem. Such a model is useful when the details
of steering, braking, and acceleration are handled by another controller or are
irrelevant to the question being asked.

Thus, one boundary is preferred over another mainly for pragmatic reasons:

- The actions should correspond to decisions the agent can actually make.
- The state and action representation should make the learning problem as
  simple as possible without omitting important information.
- The boundary should match the timescale of the problem.
- The representation should support the predictions and rewards we care about.

There is no fundamental reason that one boundary is always best. In principle,
many different boundaries can describe the same overall system. However, the
choice is not completely arbitrary, because a poor boundary can make the problem
unnecessarily hard, hide relevant causal structure, or define actions that the
agent cannot really choose. The best boundary is the one that gives a useful and
tractable abstraction for the task being studied.

# Exercise 3.4: Table for \(p(s', r \mid s, a)\)

For the recycling robot example, the states are \(high\) and \(low\). The
available actions are \(search\), \(wait\), and, in the \(low\) state,
\(recharge\). The parameters \(\alpha\) and \(\beta\) are transition
probabilities, \(r_{search}\) is the reward for searching, \(r_{wait}\) is the
reward for waiting, and \(-3\) is the reward when the robot must be rescued
after its battery is depleted.

The table for \(p(s', r \mid s, a)\) is:

| \(s\) | \(a\) | \(s'\) | \(r\) | \(p(s', r \mid s, a)\) |
|---|---|---|---:|---:|
| \(high\) | \(search\) | \(high\) | \(r_{search}\) | \(\alpha\) |
| \(high\) | \(search\) | \(low\) | \(r_{search}\) | \(1 - \alpha\) |
| \(high\) | \(wait\) | \(high\) | \(r_{wait}\) | \(1\) |
| \(low\) | \(search\) | \(low\) | \(r_{search}\) | \(\beta\) |
| \(low\) | \(search\) | \(high\) | \(-3\) | \(1 - \beta\) |
| \(low\) | \(wait\) | \(low\) | \(r_{wait}\) | \(1\) |
| \(low\) | \(recharge\) | \(high\) | \(0\) | \(1\) |

All other 4-tuples have probability zero. For example, there is no row for
\((high, wait, low, r)\), because waiting in the high-battery state leaves the
robot in the high-battery state with probability \(1\). There is also no row for
\((high, recharge, s', r)\), because \(recharge\) is not an available action in
the \(high\) state in this example.
