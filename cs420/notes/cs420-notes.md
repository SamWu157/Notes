9/22/2016
## Introduction

### What is AI?

* > the science and engineering of making intelligent machines, especially intelligent computer programs


### Four Categories Views of AI

1. Thinking Humanly
2. Acting Humanly
3. Thinking Rationally
4. Acting Rationally

### Acting Humanly: Turing Test

* Can you tell who is human and who is an AI system?

### Thinking Humanly: Cognitive Modeling

* Requires scientific theories of internal activities of the brain

### Thinking Rationally: Laws of Thoughts

* Aristotle  
 > what are correct arguments/thought process?
* Problems:
 * not easy to state informal knowledge in formal terms
 * difference between solving a problem in principle and practice

### Acting Rationally: Rational Agent

* Agent: something that acts
* Rational: doing the right thing
 * maximize goal achievement given available information


9/27/2016
## Intelligent Agents

### Agents
* **agent**: anything that can be viewed as **perceiving** its **environment** through **sensors** and **acting** upon that environment through **actuators**


### Terminology
* **Percepts**: agent's perceptual inputs
* **Percept sequence**: complete history of everything the agent has perceived
* **Agent function**: maps any given percept sequence to an action [_f_ : p* -> A]
* The **agent program** runs on the physical architecture to produce _f_
* Agent = architecture + program


### Questions
* Can there be more than one agent program that implements a given agent function?
 * Yes
* Given a fixed machine architecture, does each agent program implement exactly one agent function?
 * Yes


### Vacuum-Cleaner World
* **Percepts**: location and contents
    * e.g. [A, dirty]
* **Actions**: Left, Right, Suck, NoOp


### Simple Agent Function
| **Percept sequence**               | **Action**        |
| ---------------------------------- | ----------------- |
| [A, clean]                         | NoOp              |
| [A, dirty]                         | Suck              |
| [B, clean]                         | NoOp              |
| [B, dirty]                         | Right, Suck       |
| [A, clean], [A, clean]             | NoOp              |
| [A, clean], [A, dirty]             | Suck              |
| ...                                | ...               |
| [A, clean], [A, clean], [A, clean] | NoOp              |
| [A, clean], [A, clean], [A, dirty] | Suck              |
| ...                                | ...               |

### Rationality
* agent should _do the right thing_ based on what it can perceive and actions it can perform
    * right action: one that will cause the agent to be most successful
* **Performance measure**: An objective criterion for success of an agent's behavior
* Vacuum cleaner example:
    * Amount of dirt cleaned within certain time
    * +1 credit for each clean square per unit time
* General rule: measure what one wants rather than how one thinks the agent should behave


### Rational Agent
* For each possible **percept sequence**, a rational agent should select an **action** that is expected to maximize its **performance measure**, given the evidence provided by the percept sequence and whatever built-in **knowledge** the agent has


### Vacuum Cleaner Example
* simple agent that cleans square if dirty and moves to other side if not
* rational? **Yes**
* **Assumption**:
    * performance measure: 1 point for each clean square at each time step
    * environment is known a priori
    * actions = {left, right, suck, no-op}
    * agent is able to perceive the location and dirt in that location
* Given different assumption, it might not be rational


### Omniscience, Learning, and Autonomy
* Distinction between **rationality** and **omniscience**
    * expected performance vs actual performance
* **information gathering** / **exploration**: Agents can perform actions in order to modify future percepts so as to obtain useful information
* agent can **learn** from what it perceives
* agent is **autonomous** if its behavior is determined by its own experience
    * ability to learn and adapt


### Questions
* Given the assumption on slide 12. Describe a rational agent function for the modified performance measure that deducts one point for each movement. Does the agent program require internal state?
* Discuss possible agent designs for the cases in which clean squares can become dirty and the geography of the environment is unkown


### PEAS
* specify task environment is always the first step in designing agent
* **PEAS**:
    * **P**erformance
    * **E**nvironment
    * **A**ctuators
    * **S**ensors


### Taxi Driver Example
| **Performance Measure** | **Environment** | **Acutators** | **Sensors** |
| ----------------------- | --------------- | ------------- | ----------- |
| safe, fast, legal,      | roads,          | steering,     | camera,     |
| comfortable, trip,      | other traffic,  | accelerator,  | sonar,      |
| maximize profits        | pedestrians,    | brake, signal,| speedometer,|
|                         | customers       | horn, display | GPS,        |
|                         |                 |               | odometer,   |
|                         |                 |               | engine,     |
|                         |                 |               | sensors,    |
|                         |                 |               | keyboard,   |
|                         |                 |               | accelerator |

### Properties of Task Environments
* **Fully observable** (vs. **partially observable**):
    * agent's sensors give it access to the complete state of the environment at each point in time
* **Deterministic** (vs. **stochastic**):
    * next state of the env. determined by current state and agent's action
    * **strategic**: if environment is deterministic except for the actions of other agents
* **Episodic** (vs. **sequential**):
    * Agent's experience is divided into atomic _episodes_
    * Choice of action in each episode depends only on the episode itself
* **Static** (vs. **dynamic**):
    * environment is unchanged while agent is deliberating
    * **Semidynamic**: environment itself doesn't change with time but the agent's performance score does
* **Discrete** (vs. **continuous**):
    * A limited number of distinct, clearly defined percepts and actions
* **Single agent** (vs. **multiagent**):
    * An agent operating by itself in an environment
    * competitive vs. cooperative


### Example
| **Task Environment** | **Observable** | **Deterministic** | **Episodic** | **Static** | **Discrete** | **Agents** |
| -------------------- | -------------- | ----------------- | ------------ | ---------- | ------------ | ---------- |
| _Crossword puzzle_   | fully          | deterministic     | sequential   | static     | discrete     | single     |
| _Chess with a clock_ | fully          | stategic          | sequential   | semi       | discrete     | multi      |
| _Taxi driver_        | partially      | stochastic        | sequential   | dynamic    | continuous   | multi      |
| _mushroom-picking_   | partially      | stochastic        | episodic     | dynamic    | continuous   | single     |

* environment type largely determines the agent design
* real world: partially observable, stochastic, sequential, dynamic, continuous, multi-agent


### Exercises
* Develop PEAS description for following;
    * Robot Soccer Player
    * Shooping for used AI books on the Internet
* Analyze the properties of the above environments


### True/False Questions
* agent that senses only partial information about the state cannot be perfectly rational **False**
* suppose an agent selects its actions uniformly at random from the set of possible actions. There exists a deterministic task environment in which this agent is rational **True**
* It is possible for a given agent to be perfectly rational in two distinct task environments **True**
* A perfectly rational poker-playing agent never loses **False**


### Agent = Architecture + Program
* job of AI is to design the **agent program** that implements the **agent function** mapping percepts to actions
* Aim: find a way to implment the **rational** agent function concisely
* Same skeleton for agent program: takes the **current percept** as input from the sensors and returns an action to the actuators


### Agent Program vs. Agent Function
* **Agent program** takes teh current percept as input
    * Nothing is available from the environment
* **Agent function** takes the entire percept history
    * to do this: remember all the percepts


### Table-Driven Agent
* Designer needs to construct a table that contains the appropriate action for every possible percept sequence
* **Drawbacks**?
    * huge table
    * takes a long time to construct
    * no autonomy
    * even with learning, needs a long time to learn table entries


### Five Basic Agent Types
* Arranged in order of increasing generality:  
 1. Simple reflex agents
 2. Model-based reflex agents
 3. Goal-based agents
 4. Utility-based agents
 5. Learning agents

### Simple Reflex Agent
* Psuedo-Code

   * **function** Simple-Reflex-Agent (_percept_) **returns** an action  
    **static**: _rules_, a set of condition-action rules  
    _state_  - INTERPRET-INPUT (_percept_)  
    _rule_   - RULE-MATCH (_state_, _rules_) 
    _action_ - RULE-ACTION [ _rule_]
    **return** _action_
* write a simple reflex agent for the vacuum cleaner example
* **Infinite loops** are often unavoidable for simple reflex agent operating in partially observable environments
    * No location sensor
* **Randomization** will help
    * A randomized simple reflex agent might outperform a deterministic simple reflex agent
* Better way: Keep track of the part of the world it can't see now
    * maintain internal states


### Model-Based Reflex Agent
* psuedo-cde

    * **function** REFLEX-AGENT-WITH-STATE (_percept) **returns** an action
    * **static**: 
       * _state_, a description of the current world state
       * _rules_, a set of condition-action rules
       * _action_, the most recent action, initially none  
    * _state_  - UPDATE-STATE (_state_, _action_, _percept_)
    * _rule_   - RULE-MATCH (_state_, _rules_)
    * _action_ - RULE-ACTION [_rule_]
    * **return** _action_


### Goal Based Agent

### Utility-Based Agent
* Utility function maps a state or a sequence of states onto a real number -> degree of happiness
* Conflicting goals
    * speed and safety
* Multiple goals


### Learning Agent
* Critic: Determines performance
* Learning element: Making improvements
* Problem generator: Suggest exploratory actions
* performance element: selects the best action


### Exercise
* Select a suitable agent design for:
    * Robot soccer player
    * Shopping for used AI books on the Internet


9/29/2016

## Uninformed Search 1

### Problem Solving Agent
* Problem-solving agent: a type of goal based agent
    * Decide what to do by finding sequences of actions that lead
* **Goal formulation**: based on current situation and agent's performance measure
* **Problem formulation**: deciding what actions and states to consider, given a goal
* **search**: The process of looking for such a sequence


### Example: Romania Touring
* On holiday in Romania; currently in Arad
* Non-refundable ticket to fly out of Bucharest tomorrow
* **Formulate goal** (**perf. evaluation**):
    * be in Bucharest before the flight
* **Formulate problem**:
    * **states**: various cities
    * **actions**: drive between cities
* **Search**:
    * sequence of cities


### Problem-Solving Agents
* **function** SIMPLE-PROBLEM-SOLVING-AGENT (_percept_) **returns** an action
    * **persistent**:
        * _seq_, an action sequence, initially empty
        * _state_, some description of the current world state
        * _goal_, a goal, initially null
        * _problem_, a problem formulation
    * _state_ - UPDATE-STATE (_state_, _percept_)
    * **if** _seq_ is empty **then**
        * _goal_ - FORMULATE-GOAL (_state_)
        * _problem_ - FORMULATE-PROBLEM (_state_, _goal_)
        * _seq_ - SEARCH (_problem_)
        * **if** _seq_ = _failure_ **then return** a null action
    * _action_ - FIRST (_seq_)
    * _seq_ - REST (_seq_)
    * **return** _action_


### Aspects of the Simple Problem Solver
* Where does it fit into the agents and environment discussion?
    * Static environment
    * observable
    * Discrete
    * Deterministic
    * **Open-loop** system: percepts are ignored, thus break the loop between agent and environment


### Well-Defined Probelems
* A problem can be defined formally by five components:
    1. Initial state
    2. Actions
    3. Transition Model: description of what each action does (successor)
    4. Goal test
    5. Path cost


### Problem Formulation - 5 Components
* **Intial state**: In(_Arad_)
* **Actions**, if current state is In(Arad), actions = {Go(Sibu), Go(Timisoara), Go(Zerind)}
* **Transition model**:
    * e.g. Results(In(Arad), Go(_Sibiu_)) = In(_Sibiu_)
* **Goal test**, determines whether a given state is a goal state
    * explicit, e.g. In(_Bucharest_)
    * implicit, e.g. checkmate
* **Path cost function** that assigns a numeric cost to each path
    * e.g distance traveled
    * step cost: _c(x, a, y)_
* **Solution**, a path from the initial state to a goal state
* **Optimal solution**: the path that has the lowest path cost among all solutions; measured by the path cost function


### Problem Abstraction
* Real world is complex and has more details 
* **abstraction**: Irrelevant details should be removed from state space and actions
    * abstraction is **valid**, if we can expand it into a solution in the more detailed world
    * abstraction is **useful**, if carrying out the actions in the solution is easier than the original problem
    * remove as much detail as possible while retaining validity and usefullness


### Example Vacuum-Cleaner
* **States**
    * 8 states
* **Initial state**
    * any state
* **Actions**
    * Left, Right, Suck
* **Transition model**
    * complete state space
* **Goal test**
    * whether both squares are clean
* **Path cost**
    * each step costs 1


### Example: 8-puzzle
* **States**:
    * location of each tile and the blank
* **Initial state**: any, 9!/2
* **Actions**:
    * blank moves Left, Right, Up, or Down
* **Transition model**:
    * Given a state and action, returns the resulting state
* **Goal Test**: Goal configuration
* **Path cost**: Each step costs 1


### Missionaries and Cannibals
* 3 missionaries and 3 cannibals need to cross a river
* 1 boat can carry 1 or 2 people
* Find a way to get everyone to the other side, without ever leaving the group of missionaries in one place outnumbered by the cannibals in that place


### Problem Formulation
* **States**:
    * <m, c, b> representing the # of missionaries and the # of cannibals, and the position of the boat
* **Initial state**:
    * <3, 3, 1>
* **Actions**:
    * take 1 missionary, 1 cannibal, 2 missionaries, 2 cannibals, or 1 missionary and 1 cannibal across the river
* **Transition model**:
    * state after an action
* **Goal test**:
    * <0, 0, 0>
* **Path cost**:
    * number of crossing


### Real World Problems
* Touring problem: visit every city at least once, starting and ending in Bucharest
* Traveling sales problem: exactly once
* Robot navigation
* Internet searching: software robots


10/4/2016

## Uninformed Search 2

### Searching for Solutions
* **Search tree**: generated by initial state and possible actions
* Basic idea:
* offline, simulated exploration of state space by generating successors of already-explored states (**expanding** states)
* **search stategy** determines the choice of which state to expand


### Terminologies
* **Frontier**: set of all leaf nodes available for expansion at any given point
* **Repeated state**
* **Loopy path**: Arad to Sibiu to Arad
* **Redundant path**: more than one way to get from one state to another
* Sometimes, redundant paths are unavoidable
    * SLiding-block puzzle


### General Tree Search Algorithm
* **function** TREE-SEARCH (_problem_) **returns** a solution, or failure
    * inialize the frontier using the initial state of _problem_
    * **loop do**
        * **if** the frontier is empty **then return** failure
        * choose a leaf node and remove it from the frontier
        * **if** the node contains a goal state **then return** the corresponding solution
        * expand the chosen node, adding the resulting nodes to the frontier


### Avoiding Repeated States
* failure to detect repeated states can turn a linear problem into an exponential one!
* algorithms that forget their history are doomed to repeat it
* state space size: d ace size: d + 1 -> search tree leaves: 2^d


### General Graph Search Algorithm
* **function** GRAPH-SEARCH (_problem_) **returns** a solution, or failure
    * inialize the frontier using the initial state of _problem_
    * **_initialize the explored set to be empty_**
    * **loop do**
        * **if** the frontier is empty **then return** failure
        * choose a leaf node and remove it from the frontier
        * **if** the node contains a goal state **then return** the corresponding solution
        * **_add the node to the explored set_**
        * expand the chosen node, adding the resulting nodes to the frontier
            * **_only if not in the frontier or explored set_**
* We augment Tree-Search with a explored set, which remembers every expanded node


### Implementation: States vs Nodes
* **state**: representation of a physical configuration
* **node**: data structure constituting part of a search tree includes **state**, **parent node**, **action**, **path cost** _g(n)_, **depth**
* A solution path can be easily extracted


### CHILD-NODE function
* takes a parent node and an action and returns the resulting child node
* **function** CHILD-NODE(problem, parent, action) **returns** a node
    * **return** a node with 
        * STATE = problem.RESULT(parent.STATE, action)
        * PARENT = parent
        * ACTION = action
        * PATH-COST = parent.PATH-COST + problem.STEP-COST(parent.STATE, action)


### Frontier and Explored Set
* Goal of frontier: the next node to expand can be easily located in the frontier
    * Possible data structure?
* Goal of explored set: efficient checking for repeated states
    * Possible data structure?


### Search Strategies
* defined by picking the **order of node expansion**
* Strategies are evaluated along the following dimensions:
    * **completeness**: does it always find a solution if one exists?
    * **optimality**: does it always find a least-cost solution?
    * **time complexity**: number of nodes generated
    * **space complexity**: maximum number of nodes in memory
* Time and space complexity are measured in terms of 
    * *b*: maximum branching factor of the search tree
    * *d*: depth of the least-cost solution
    * *m*: maximum depth of the state space (may be infinity)
* Search cost(time), total cost(time + space)


### Uniformed Search Stategies
* **Uniformed search** (**blind search**) strategies use only the information availablein the problem definition
* **informed-search** / **heuristic search**: Strategies that know whether one non-goal state is better than another
* General uninformed search stategies:
    * Breadth-first search
    * Uniform-cost search
    * Depth-first search
    * Depth-limited search
    * Iterative deepening search


### Breadth-First Search
* Expand shallowest unexpanded node
* **Implementation**:
    * _Frontier_ is a FIFO queue, i.e. new successors go at end


### BFS on a Graph
* **function** BREADTH-FIRST-SEARCH (_problem_) **returns** a solution, or failure
    * _node_ - a node with STATE = _problem_.INTITIAL-STATE, PATH-COST = 0
    * **if** _problem_.GOAL-TEST(_node_.STATE) **then return** SOLUTION(_node_)
    * _frontier_ - a FIFO queue with _node_ as the only element
    * _explored_ - an empty set
    * **loop do**
        * **if** EMPTY?(_frontier) **then return** failure
        * _node_ - Pop(_frontier_) /*chooses the shallowest node in _frontier_ */
        * add _node_.STATE to _explored_
        * **for each** _action_ **in** _problem_.ACTIONS(_node_.STATE) **do**
            * _child_ - CHILD-NODE(_problem_, _node_, _action_)
            * **if** _child_.STATE is not in _explored_ or _frontier_ **then**
                * **if** problem_.GOAL-TEST(_child_.STATE) **then return** SOLUTION(_child_)
                * _frontier_ - INSERT(_child_._frontier_)



### Analysis of Breadth-First Search
* **Complete?**
    * Yes (if b _is_ finite), the shallowest solution is returned
* **Time?**
    * b + b^2 + b^3 + ... + b^d = O(b^d)
* **Space?**
    * O(b^d) (keeps every node in memory)
* **Optimal?**
    * Yes if step costs are all identical or path cost is a nondecreasing function of the depth of the node
* **Space** is the bigger problem (more than time)
* **Time** requirement is still a major factor


### How bad is BFS?
* with b = 10; 1 millin nodes/sec; 1k bytes/node
    * takes 13 days for the solution to a problem with search depth 12, nodes 10^12
    * 350 years at depth 16
* Memory is more of a problem than time
    * Requires 103G when d = 8
* Exponential-complexity search problems cannot be solved by uninformed methods for any but the smallest instances


### Uniform-Cost Search
* Expand least-cost unexpanded node
* **Implementation**:
    * _Frontier_ = priority queue ordered by path cost g(n)
* breadth-first = uniform-cost search when? **edges have equal weight**
* **function** UNIFORM-COST-SEARCH(_problem_) **returns** a solution, or failure
* _node_ - a node with STATE = _problem_.INITIAL-STATE = _problem_.INITIAL-STATE, PATH-COST = 0
    * _frontier_ - a priority queue ordered by PATH-COST, with _node_ as the only element
    * _explore_ - an empty set
    * **loop do**
        * **if** EMPTY? (_frontier_) **then return** failure
        * _node_ - Pop(_frontier_) /*chooses the lowest-cost node in _frontier_*/
        * **if** _problem_.GOAL-TEST(_node_.STATE) **then return** SOLUTION(_node_)
        * add._node_.STATE to _explored_
        * **for each** _action_ **in** _problem_.ACTIONS(_node_.STATE) **do**
            * _child_ - CHIlD-NODE(_problem_, _node_, _action_) 
            * **if** _child_.STATE is not in _explored_ or _frontier_ **then**
                * _frontier_ - INSERT(_child_, _frontier_)
            * **else if** _child_.STATE is in _frontier_ with higher PATH-COST **then**
                * replace that _frontier_ node with _child_


### Analysis
* **Complete?**
    * Yes, if step cost >= e
* **Time?**
    * O (b ^ ceiling(C*/e)) where C* is the cost of the optimal solution
    * # of nodes with g less than or equal to cost of optimal solution
* **Space**?
    * O (b ^ ceiling (C*/e))
    * # of nodes with g less than or equal to cost of optimal solution
* **Optimal**?
    * Yes - nodes expanded in increasing order of g(n)


### Uniform-Cost Search is Optimal
* expands nodes in order of their optimal path cost
* Hence, the first goal node selected for expansion must be the optimal solution 


### Depth First Search
* Expand deepest unexpanded node
* **Implementation:
    * _frontier_ = LIFO queue, i.e. put successors at front
    * Or a recursive function


### Properties of DFS
* depend strongly on whether the graph-search or tree-search version is used


### Analysis of DFS + Tree Search
* **Complete?**
    * No: fails in infinite-depth spaces, or spaces with loops
    * Modify to avoid repeated states along path
        * complete in finite spaces
* **Time?**
    * O (b^m): terrible if _m_ is much larger than _d_
    * but if solutions are dense, may be faster than breadth-first
**Space?**
    * O (bm), i.e. linear space!
**Optimal**
    * No


### Analysis of DFS + Graph Search
* **Complete?**
    * No: also fails in infinite-depth spaces
    * Yes: for finite state spaces
* **Time?** 
    * O (b^m): terrible if _m_ is much larger than _d_
    * but if solutions are dense, may be much faster than bread-first
* **Space?**
    * Not linear any more, because of explored set
* Optimal?
    * No


### Backtracking Search
* is a variant of DFS
    * only one successor is generated at a time rather than all successors
    * Each partially expanded node remembers which successor to generate next
    * memory requirement: O(m) vs O(bm)


### Depth-Limited Search
* Is the same as depth-first search with depth limit _l_, nodes at depth _l_ are treated as if they have no successors
* **function** DEPTH-LIMITED-SEARCH (_problem_, _limit_) **retunrs** a solution, or failure/cutoff
    * **returns** RECURSIVE-DLS(MAKE-NODE(_problem_.INITIAL-STATE), _problem_, _limit_)
* **function** REUCRSIVE-DLS(_node_, _problem_, _limit_) **returns** a solution, or failure/cutoff
    * **if** _problem_.GOAL-TEST(_node_.STATE) **then return** SOLUTION(_node_)
    * **else if** _limit_ = 0 **then return** _cutoff_
    * **else**
        * _cutoff-occurred?_ -> false
        * **for each** _action_ **in** _problem_.ACTIONS(_node_.STATE) **do**
            * _child_ -> CHILD-NODE (_problem_, _node_, _action_)
            * _result_ -> RECURSIVE-DLS(_child_,_problem_,_limit_ - 1)
            * **if** _result_ = _cutoff_ **then** _cutoff-occurred_ -> true
            * **else if** _result_ != _failure_ **then return** _result_
        * **if** _cutoff-occurred_? **then return** _cutoff_ **else return** _failure_
* Compete? **No** Time? **O (b^m)** Space? **Graph: not linear, Tree: O(bm)** Optimal? **No**


### Iterative Deepening DF-Search
* Gradually increase the depth limit until a goal is found
* Combines the benefits of **depth-first** and **breadth-first** search
* **function** ITERATIVE-DEEPENING-SEARCH(_problem_) **returns** a solution, or failure
* **inputs:** _problem_, a problem
* **for** _depth_ -> 0 **to** infinity **do**
* _result_ -> DEPTH-LIMITED-SEARCH(_problem_, _depth_)
* **if** _result_ != _cutoff_ **then return** _result_


### Analysis of Iterative Deepening Search
* Number of nodes generated in a depth-limited search to depth _d_ with branching factor _b_:
* N-_DLS_ = b^0 + b^1 + b^2 + ... + b^d-2 + b^d-1 + b^d
* Number of nodes generated in an iterative deepening search to depth _d_ with branching factor _b_:
* N-_IDS_ = (d+1)b^0 + db^1 + (d-1)b^2 + ... + 3b^d-2 + 2b^d-1 + b^d
* For b = 10, d = 5
* N-dls = 1 + 10 + 100 + 1000 + 10000 + 100000 = 111111
* N-IDS = 6 + 50 + 400 + 3000 + 20000 + 100000 = 123456
* Overhead = (123456 - 111111)/111111 = 11%
* IDS is the preferred uninformed search method when search space is large and depth of solution is unknown
* **Complete**
* yes
* **Time?**
* (d+1)b^0 + db^1 + (d-1)b^2 + ... + b^d = O(b^d)
* **Space?**
* O(bd) (tree search version)
* **Optimal?**
* Yes, if step costs are identical or path cost is a nondecreasing function of the depth of the node


### Summary of Uninformed Tree Search Strategies
| Criterion | Breadth-First | Uniform-cost | Depth-First | Depth-Limited | Iterative Deepening |
| --------- | ------------- | ------------ | ----------- | ------------- | ------------------- |
| Complete? | Yes           | Yes          | No          | No            | Yes                 |
| Time?     | O(b^d+1)      | O(b^C*/e)    | O(b^m)      | O(b^l)        | O(b^d)              |
| Space     | O(b^d+1)      | O(b^C*/e)    | O(bm)       | O(bl)         | O(bd)               |
| Optimal?  | Yes           | Yes          | No          | No            | Yes                 |
* Complete and optimal under certain conditions
* Discussion on bidirectional search


### Analysis of Graph Search
* Much more efficient than Tree-Search
* Time and space are proportional to the size of the state space
* Optimality:
    * uniform-cost search or breadth-first search with identical step costs are still optimal even if it returns the first path found
    * iterative-deepening, identical step cost or non-decreasing function of depth of a node
* Tradeoff: depth-first or iterative deepening are **not linear** anymore


### Bidirectional Search
* Runs two simultaneous searches
    * Forward from initial state
    * Backward from goal state


### Searching with Partial Information
* **Deterministic, fully observable** -> **single-state problem**
    * agent knows exactly which state it will be in
    * solution is a sequence
* **Deterministic, non-observable** -> **multi-state problem**
    * also called **sensorless problems (conformant problems)**
    * agent may have no idea where it is
    * solution is a sequence
* **Nondeterministic and/or partially observable** -> **contigency problem**
    * percepts provide **new** information about current state
    * often **interleave** search, execution
    * solution is a tree or policy
* **Unknown state space** -> **exploration problem ("online")**
    * states and actions of the environment are unknown


### Example: Vacuum World
* **Single-state** start in #5
* Solution? **[Right, Suck]**
* **Multi-state**, start in #[1, 2, ... ,8]
* Solution? [Right, Suck, Left, Suck]


### Contingency Problem
* **Contingency** start in #5 & #7
* _Nondeterministic_: suck may dirty a clean carpet
* _local sensing_: dirt, location only at current location
* Solution? Percept: [Left, Clean] -> [Right, **if** dirty **then** Suck]
