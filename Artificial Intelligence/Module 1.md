

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
    
3. **Abstraction:** Removing irrelevant real-world details (like traffic, weather, or driver fatigue) to make a problem manageable.
    
    - _Example:_ Simplifying a map by representing towns as nodes and roads as edges with costs, turning it into a graph-search problem.
        

### 3. How They Work Together

- **Abstraction** simplifies the real-world problem into a manageable formal representation.
    
- **Knowledge** provides the background facts and rules governing that problem domain.
    
- **Search** explores the possibilities within that framework to find the final solution.