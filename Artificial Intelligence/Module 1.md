

# 2. Applications of AI

## 1. Games

An important characteristic of games is these are adversarial environments.
### 1. Adversarial Environments & Search

- **Adversarial Environment:** A setting where an opponent actively works against your goals (e.g., Chess, Go, card games). You cannot assume a cooperative environment; your opponent will choose actions beneficial to them and harmful to you.
    
- **Adversarial Search:** Unlike ordinary search (which simply maps a path from the current state to a goal), adversarial search accounts for alternating moves by factoring in the opponent's deliberate counter-responses.
```
             Current state
                  ↓
             My possible moves
                  ↓
         Opponent's responses
                  ↓
             My responses
                  ↓
         Opponent's responses
                  ↓
                ...
```
### 2. Game Trees & Players (MAX and MIN)

A game can be represented using a **game tree**.

A game tree represents:

> **possible future states of the game.**

For example:

```
                     Current State
                    /             \
                 Move A          Move B
                 /   \            /   \
               A1     A2        B1     B2
```

- The root represents the current position.
- Each branch represents a possible move.
- Each resulting node represents a new game state.
- The search continues by generating possible moves.
### 3. The Minimax Principle(Just read its easy)

- **Core Rule:** Evaluated from the bottom up. At MAX nodes, the highest value is chosen; at MIN nodes, the lowest value is chosen.
    
- **Strategic Insight:** MAX assumes MIN will always pick the worst-case scenario for MAX. Therefore, MAX selects the move whose worst-case outcome is optimized (the best of the worst).
    
    - _Example:_ Given a tree where branch A leads to MIN choices $(3, 5) \rightarrow 3$, and branch B leads to MIN choices $(2, 9) \rightarrow 2$; MAX chooses branch A because $\max(3, 2) = 3$. Choosing B risks MIN selecting $2$.
### 4. Game AI Pipeline

- **Input:** Current board/game state.
- **Process:** Generate possible moves $\rightarrow$ traverse game tree $\rightarrow$ apply Minimax considering opponent actions.
- **Output:** The next best move.

> **Key Takeaway:** Game AI uses adversarial search and the Minimax algorithm to select moves by anticipating that the opponent will always try to minimize the AI's success.

## 2. Theorem proving

###  What is Theorem Proving?

- **Definition:** A computer is given premises/facts and automatically determines whether a conclusion logically follows from them.
>A **premise** is a statement that we assume to be true.
 
### 2. Step-by-Step Deduction Example

- **Premises & Goal:**
    
    - **Premise 1:** $S(x) \to P(x)$ (All students who submit assignments on time pass)
        
    - **Premise 2:** $S(\text{Rahul})$ (Rahul submitted on time)
        
    - **Goal:** Prove $P(\text{Rahul})$ (Rahul passes)
        
- **Derivation Process:**
    
    1. **Substitute:** Set $x = \text{Rahul}$ in Premise 1 to get $S(\text{Rahul}) \to P(\text{Rahul})$.
        
    2. **Apply Modus Ponens:** Using the rule 
    ```
A
A → B
------
B
    ```
combine $S(\text{Rahul})$ with $S(\text{Rahul}) \to P(\text{Rahul})$.
    
**Conclusion:** $P(\text{Rahul}) = \text{TRUE}$ (Rahul passes).

## 3. Natural Language Processing (NLP)

### What is NLP?

- **Definition:** Natural Language Processing is the branch of AI that enables computers to **understand, interpret, and generate** human language.
    
- **The Challenge:** Unlike computers that rely on structured data, human language is nuanced and ambiguous, requiring a multi-stage processing pipeline to analyze.
    
### 2. The 5-Stage NLP Pipeline

1. **Tokenization:** Breaks raw text into smaller individual units (words, punctuation).
    
    - _Example:_ `"Robots learn quickly."` $\to$ `[Robots, learn, quickly, .]`
        
2. **Morphological Analysis:** Figuring out how words change based on tense or form
    
    - _Focus:_ Analyzes variations of words (e.g., _play, plays, played_).
        
3. **Syntactic Parsing:** Figuring out the role of every word plays in a sentence(e.g., mapping words to nouns, verbs, or adverbs).
    
4. **Semantic Analysis:** Extracts the actual **meaning** of the sentence and defines the roles of each word (e.g., who performed the action vs. what received it).
    
5. **Discourse and Pragmatics:** Interprets meaning beyond a single sentence.
    
    - **Discourse:** Examines how sentences connect across a conversation or text.
        
    - **Pragmatics:** Interprets meaning based on real-world context and user intent (e.g., understanding that "Can you open the window?" is a request, not a physical ability question).
## 4. Computer Vision & Image Processing

### The Computer Vision Pipeline

1. **Image Acquisition:** Capturing the raw visual data (e.g., a self-driving car's camera photographing the road).
    
2. **Pre-processing:** Cleaning the raw image to handle poor quality, and **noise removal**.
    
3. **Feature Extraction:** Identifying distinct, useful properties that help differentiate objects (e.g., detecting **edges and corners**).
    
4. **Object Recognition:** Identifying the object from the features(e.g., recognizing a **stop sign** by its octagonal edge pattern and red color).

## 5. Speech Processing

### 1. What is Speech Processing?

- **Definition:** The branch of AI focused on extracting information from acoustic waveforms and audio signals to convert spoken words into readable text.
    
- **Core Pipeline:** Audio signal $\rightarrow$ Framing & feature extraction $\rightarrow$ Acoustic model $\rightarrow$ Language model $\rightarrow$ Decoded text.
### 2. The Speech Processing Pipeline Steps

- **Framing & Feature Extraction:** Raw audio waveforms are split into short frames (eg: approx. 30 ms) to extract meaningful representations.
    
    - **MFCC (Mel-Frequency Cepstral Coefficients):** The primary feature that highlights the most important parts of the sound.
        
- **Acoustic Model:** Maps audio features (like MFCC vectors) to basic linguistic sound units or phonemes.
    
- **Language Model:** Determines the sequence of words based on the phoneme combination and context (e.g., resolving ambiguous sounds into "Turn on the lights").

## 6. Robotics in AI

### 1. What is Robotics?

- **Definition:** Intelligent systems capable of perceiving the physical world, making decisions, and performing physical actions.
    
- **Core Workflow:** **Perceive $\rightarrow$ Plan $\rightarrow$ Act**
    

### 2. The Three Components

1. **Sensing:** Gathering environmental data using tools like **Cameras** (to detect objects) and **LiDAR** (to measure surroundings).
    
2. **Planning:** Determining the best course of action (e.g., path and trajectory planning to reach a destination safely).
    
3. **Actuation:** Executing physical movements via **motors** based on the decisions made.

## 7. Expert Systems

### 1. What is an Expert System?

- **Definition:** An AI system that encodes human specialist knowledge so a computer can use it to make decisions or diagnoses.
    
- **Core Mechanism:** Specialist knowledge is stored as **IF–THEN rules**, and an **inference engine** applies those rules to case facts.
      
- **Case Facts $\rightarrow$ Inference Engine + Knowledge Base $\rightarrow$ Decision/Diagnosis**
    

### 2. Rule Chaining Example

- **Initial Facts:** `fever = true`, `cough = true`, `breathlessness = true`
    
- **Rule 1 (`IF fever AND cough THEN respiratory_infection`):** Fires first because initial facts match, creating a _new fact_ (`respiratory_infection = true`).
    
- **Rule 2 (`IF respiratory_infection AND breathlessness THEN priority = HIGH`):** Uses that newly derived fact along with the existing facts to trigger and reach the final conclusion (`priority = HIGH`).
    
- **Rule Chaining:** Using an intermediate conclusion from one rule as a fact to trigger subsequent rules.

# 3. The Three Pillars of AI Techniques

Solving complex problems in AI relies on three foundational pillars working together: **Search**, **Knowledge**, and **Abstraction**.

### The Three Pillars

1. **Search:** Systematically exploring possible states to find a path from a start state to a goal.
    
    - _Examples of control strategies:_ DFS, BFS, Hill climbing, Best-first search, and Branch and bound.
        
2. **Knowledge:** Representing facts and rules about the world so the system can reason and make decisions (e.g., combining facts and rules to deduce outcomes, as seen in theorem proving and expert systems).
    
3. **Abstraction:** Removing irrelevant real-world details (like traffic, weather, or driver fatigue) to make a problem manageable to search.
    
    - _Example:_ Simplifying a map by representing towns as nodes and roads as edges with costs, turning it into a graph-search problem.
        

### How They Work Together

- **Abstraction** simplifies the real-world problem into a manageable formal representation.
    
- **Knowledge** provides the background facts and rules governing that problem domain.
    
- **Search** explores the possibilities within that framework to find the final solution.

# 4. State Space Representation & Search Problem Components

### 1. State Space Representation

- **State:** A formal representation of the situation at a particular point in a problem (e.g., chess piece arrangement, or water amounts in jugs like `(3,2)`).
    
- **State Space:** The collection of _all_ possible states for the problem.
### 2. The Four Components of a Search Problem

Every search problem is formally defined by these four core components:

1. **Initial State:** The starting point where problem-solving begins (e.g., empty jugs `(0,0)`).
    
2. **Operators / Actions:** Legal moves that transform one state into another (e.g., applying "Fill B" to `(0,0)` yields `(0,3)`).
    
3. **Goal Test:** A condition used to determine whether the current state achieves the objective (e.g., checking if water in Jug A equals 2 liters, `x == 2`).
    
4. **Path Cost:** A numeric cost assigned to a sequence of actions (e.g., assigning a cost of 1 per operation, meaning 6 actions equals a path cost of 6).

e.g. The Water Jug Problem

Formal state-space definition 
• State: (x, y) — litres currently in jug A (0-4), jug B (0-3) 
• Initial state: (0, 0) 
• Goal test: x = 2 
• Operators: fill A, fill B, empty A, empty B, 
 pour A→B, pour B→A (6 operators) 
  - Path cost: 1 per operator applied (we count total steps)
## State-Space Search

### 1. What is State-Space Search?

- **Definition:** Searching through all possible problem states to find a sequence of actions that transforms the **initial state** into a **goal state**.

```
Initial State
     ↓
Generate possible states
     ↓
Search through state space
     ↓
Find goal state
```

## Production Systems

### 1. What is a Production System?

- **Definition:** A problem-solving framework driven by a rule-based architecture.
    
- **The Three Core Components:**
    
    1. **Global Database:** Represents the current state of the problem (facts/current configuration, e.g., `(jugA = 0, jugB = 0)`).
        
    2. **Production Rules:** Condition-action pairs (`IF condition THEN action`) describing what actions can be performed under what circumstances.
        
    3. **Control Strategy:** The decision-making mechanism that chooses which applicable rule to execute next when multiple rules match.

### 2. The Production System Execution Cycle

The system loops continuously until a stopping condition is met:

1. Look at the current database.
2. Find rules whose conditions match.
3. Control strategy selects a rule to fire.
4. Apply the rule's action.
5. Update the database.
6. Repeat.

- **Stopping Conditions:** The cycle terminates when either:
    
    1. The **Goal Test is TRUE** (Goal achieved).
    2. **No rule applies** (No applicable rules exist, even if the goal wasn't reached).

### 3. Production System vs. State-Space Representation

- **State Space:** Focuses on _what the states and transitions are_ (States + Operators + Goal + Cost).
    
- **Production System:** Focuses on _how rules dictate actions_ (Database + Rules + Control Strategy).

# 5. Search Space Control
## Depth-First Search (DFS)

### 1. What is DFS?

- **Definition:** An uninformed search strategy that always explores the deepest unexpanded node first, backtracking when it hits a dead end.
    
- **Core Philosophy:** Pick a branch, follow it as deep as possible until it stops, then backtrack and try the next branch.

### 2. Implementation: The Stack (LIFO)

- **Data Structure:** Uses a **Stack** operating on a **LIFO** (Last In, First Out) principle.
    
- **Why a Stack?** By popping the most recently pushed node, the search is forced down the current branch.
    
- **Handling Order:** To preserve a left-to-right traversal order, children must be pushed onto the stack in **reverse order** (e.g., pushing C then B ensures B is popped first).

### 3. Backtracking & The Visited Set

- **Backtracking:** When a node has no children/unexplored paths (a dead end), DFS pops it and returns to the most recent node with unvisited branches.
    
- **Visited Set:** Essential for graph searches to prevent infinite loops (e.g., cycles) by skipping nodes that have already been processed.

### 4. Complexity & Properties
b = branching factor , m = maximum depth.

- **Time Complexity:** O(b^m) (where b is the branching factor and m is the maximum depth). Grows exponentially.
    
- **Space Complexity:** O(b×m). Highly memory-efficient because it only stores the current path and pending siblings rather than the entire frontier.
    
- **Complete?** No (can get trapped in infinite or very deep branches even if a solution exists elsewhere).
    
- **Optimal?** No (does not guarantee the shortest or cheapest path).
    

```
DFS(Graph, start):

    create an empty stack
    create a visited set

    push start into stack

    while stack is not empty:

        node = pop(stack)

        if node is not visited:
            mark node as visited
            print node

            for each neighbor of node:
                if neighbor is not visited:
                    push neighbor into stack
```

Given:

```
        A
       / \
      B   C
     / \
    D   E
```

Goal = E.

Start:

```
Stack = [A]
```

Pop A:

```
Visited = A
```

Push C then B:

```
Stack = [B,C]
```

Pop B:

```
Visited = A,B
```

Push E then D:

```
Stack = [D,E,C]
```

Pop D:

```
Visited = A,B,D
```

Dead end.

Pop E:

```
Visited = A,B,D,E
```

Goal found.

So:

```
DFS traversal until goal:
A → B → D → E
```

Notice that DFS did **not** go:

```
A → B → E
```

immediately.

It first explored B's left child D because DFS goes as deep as possible.

### 5. Summary Table

| Property                | DFS Characteristic                                              |
| ----------------------- | --------------------------------------------------------------- |
| **Strategy**            | Go as deep as possible                                          |
| **Data Structure**      | Stack (LIFO)                                                    |
| **Backtracking**        | Yes                                                             |
| **Time Complexity**     | O(b^m)                                                          |
| **Space Complexity**    | O(b.m)                                                          |
| **Complete / Optimal?** | No / No                                                         |
| **Main Advantage**      | Low memory usage                                                |
| **Main Weakness**       | Can loop on deep/infinite branches; finds non-optimal solutions |

## Breadth-First Search (BFS)

### 1. What is BFS?

- **Definition:** An uninformed search strategy that explores a problem space level by level, expanding all nodes at depth $d$ before moving to depth $d+1$.

- **Core Philosophy:** Spread wide across the current level rather than diving deep into a single branch.

### 2. Implementation: The Queue (FIFO)

- **Data Structure:** Uses a **Queue** operating on a **FIFO** (First In, First Out) principle.

- **Why a Queue?** By processing older elements first, nodes wait their turn in line, ensuring that sibling nodes at the same level are fully explored before any children at deeper levels are touched.

- **Handling Order:** Unlike DFS, BFS does **not** require reversing child order. Children can be enqueued in standard left-to-right order because the FIFO queue naturally preserves level-order sequence.
### 3. The Visited Set & Queue Mechanics

- **Visited Tracking:** Marks nodes as visited at the moment they are _enqueued_ (unlike DFS which marks them upon _popping_). This prevents duplicate entries and handles cycles safely.

- **Frontier:** The set of discovered, unexpanded nodes currently sitting in the queue waiting to be processed.

### 4. Complexity & Properties

- **Time Complexity:** $\mathcal{O}(b^d)$ (where $b$ is the branching factor and $d$ is the depth of the shallowest goal).
- **Space Complexity:** $\mathcal{O}(b^d)$. Because BFS must hold the entire frontier (all waiting nodes at the current/next level) in memory, it is **memory-hungry**.
    
- **Complete?** Yes (guaranteed to find a solution if one exists, provided the branching factor $b$ is finite).
   
- **Optimal?** Yes, **for unit-cost edges** (because the first goal encountered is the shallowest, meaning it uses the fewest equal-cost steps).
    

```
BFS(Graph, start):

    create an empty queue
    create a visited set

    enqueue start into queue
    mark start as visited

    while queue is not empty:

        node = dequeue from queue
        print node

        for each neighbor of node:
            if neighbor is not visited:
                mark neighbor as visited
                enqueue neighbor into queue
```

### 5. Summary Table: DFS vs. BFS

|**Feature**|**DFS (Depth-First Search)**|**BFS (Breadth-First Search)**|
|---|---|---|
|**Data Structure**|Stack|Queue|
|**Operation Principle**|LIFO (Last In, First Out)|FIFO (First In, First Out)|
|**Strategy**|Go as deep as possible|Go level by level (wide)|
|**Backtracking**|Yes|No (handled by queue order)|
|**Time Complexity**|$\mathcal{O}(b^m)$|$\mathcal{O}(b^d)$|
|**Space Complexity**|$\mathcal{O}(bm)$|$\mathcal{O}(b^d)$|
|**Complete?**|No (can loop infinitely)|Yes (if $b$ is finite)|
|**Optimal?**|No|Yes (for unit-cost edges)|
|**Main Advantage**|Low memory usage ($\mathcal{O}(bm)$)|Finds the shallowest/shortest path|
|**Main Weakness**|Can get stuck; non-optimal|High memory consumption ($\mathcal{O}(b^d)$)|


# Hill climbing and Best First Search
### 1. Why Heuristic Search?

- **The Limitation of Blind Search:** DFS and BFS are "blind" because they follow strict structural rules without knowing which direction actually gets closer to the goal.

- **The Solution:** Use problem-specific knowledge via a **heuristic function**, $h(n)$, which estimates the remaining cost (or distance) from node $n$ to the goal. Lower $h(n)$ values mean a state looks more promising.

### 2. Hill Climbing

- **Definition:** A greedy local search algorithm that inspects immediate neighboring states, moves to the neighbor with the highest value (or best heuristic score), and stops when no neighbor is better.

- **The Numeric Example Summary:** Starting at $x=0$ ($f=2$), it moves sequentially to $x=1$ ($3$), $x=2$ ($4$), $x=3$ ($6$), $x=4$ ($7$), and $x=5$ ($9$), where it stops because both neighboring points have lower values ($7$).

- **The Major Flaw:** **Local Maxima.** Because it is short-sighted and looks _only_ at immediate neighbors, it can get trapped on a local peak and miss the true global maximum.

- **Escape Strategies:**  
    1. _Random Restarts_ (starting over from different points).
    
    2. _Simulated Annealing_ (occasionally accepting worse moves to escape traps).
    
    3. _Tabu Search_ (maintaining a memory of visited states to avoid looping).
### 3. Best-First Search

- **Definition:** An informed search that evaluates all available candidates in the **entire frontier** (using a **priority queue**) and expands the node with the **lowest $h(n)$**.

>Look at all currently available candidates and expand the one that looks best according to the heuristic.

- **Hill Climbing vs. Best-First Search:**      
    - _Hill Climbing:_ Local scope (looks _only_ at immediate neighbors).
    
    - _Best-First Search:_ Global frontier scope (evaluates all currently discovered, unexpanded nodes).
    
- **Worked Example Result:** Starting at $A(6)$, it expands to $C(3)$ over $B(4)$, then directly to the goal $G(0)$, requiring only 3 expansions.

- **Limitation:** Relying solely on $h(n)$ ignores the cost already spent ($g(n)$), meaning the heuristic can sometimes mislead the search, and it does not guarantee the shortest path.

### 4. Manhattan Distance Heuristic (8-Puzzle)

- **Formula:** $h(n) = \sum (\mid \text{current row} - \text{goal row} \mid + \mid \text{current column} - \text{goal column} \mid)$ for all numbered tiles (excluding the blank space).
    
      
    
- **Purpose:** Provides a straightforward numerical estimate of how far a puzzle configuration is from the target layout, allowing the algorithm to prioritize more promising board states.
    

### 5. Summary Table: Blind vs. Heuristic Search

|**Feature**|**DFS / BFS (Blind)**|**Hill Climbing (Heuristic)**|**Best-First Search (Heuristic)**|
|---|---|---|---|
|**Guidance**|Structural rules only|Local neighbors via heuristic|Entire frontier via $h(n)$|
|**Data Structure**|Stack / Queue|None (local tracking)|Priority Queue|
|**Main Weakness**|Explores many unnecessary / deep nodes|Gets trapped at local maxima|Heuristic can mislead; ignores $g(n)$|