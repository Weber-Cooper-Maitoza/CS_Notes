## 3.2 BOOLEAN ALGEBRA:
---
Three common Boolean operators are ==AND==, ==OR==, and ==NOT==

A ==TRUTH TABLE== is a table that lists the inputs, all possible values for these inputs, and the resulting values of the operation for all possible combinations of these inputs.

#### Truth Table for AND:
the Boolean expression ==xy== is equivalent to the expression ==x · y== and is read “x and y
![[Pasted image 20230919092422.png]]

#### Truth Table for OR:
The expression for OR uses a '+' sign therefore,  ==x + y== is read “x or y"
![[Pasted image 20230919092631.png]]

#### Truth Table for NOT:
NOT is represented typically by a prime '. Therefore, x’ is read “not x.”
![[Pasted image 20230919092826.png]]

#### Combined Boolean Expressions:
F (x, y, z) = x + y’z

is represented by a Boolean expressions involving the three Boolean variables x, y, and z and the logical operators OR, NOT, and AND. ==How do we know which operator to apply first?== The rules of precedence for Boolean operators give ==NOT top priority==, followed by AND, and then OR. For our previous function F, we would negate y first, then perform the AND of y’ and z, and finally OR this result with x.

![[Pasted image 20230919093251.png]]

### Boolean Identities:
==identities are used to reduce circuits==

![[Pasted image 20230919093745.png]]

Associative Law: (xy)z = x(yz) -> (x + y) + z = x + (y + z)

![[Pasted image 20230919093908.png]]

#### Examples of simplification:
![[Pasted image 20230919094655.png]]

![[Pasted image 20230919094716.png]]

![[Pasted image 20230919094730.png]]

## 3.3 LOGIC GATES:
---
![[Pasted image 20230919094924.png]]

#### exclusive-OR (XOR) gate:
represented by the Boolean expression x (+) y.
![[Pasted image 20230919095037.png]]


Two other common gates are NAND and NOR, which produce complementary output to AND and OR, respectively.
#### NAND and NOR Gates:
NAND
![[Pasted image 20230919095143.png]]

NOR
![[Pasted image 20230919095157.png]]

The NAND gate is commonly referred to as a universal gate, because any electronic circuit can be constructed using only NAND gates.

![[Pasted image 20230919100524.png]]

Why not simply use the AND, OR, and NOT gates we already know exist? There are two reasons for using only NAND gates to build any given circuit. First, NAND gates are cheaper to build than the other gates. Second, complex integrated circuits (which are discussed in the following sections) are often much easier to build using the same building block (i.e., several NAND gates) rather than a collection of the basic building blocks (i.e., a combination of AND, OR, and NOT gates).

#### ==sum-of-products==:
Truth Table can be represented by a digital circuit consisting of an AND gate for each 1 in the output column connected to a single, multiple input OR gate (referred to on page 145 as the “sum-of-products”)
## 3.4 KARNAUGH MAPS:
---
Karnaugh maps, or Kmaps, are a graphical way to represent Boolean functions.
==K-Maps are used to go from truth table to function==

<iframe width="560" height="315" src="https://www.youtube.com/embed/RO5alU6PpSU?si=M6W2yKq9jXHVCT3l" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## 3.5 DIGITAL COMPONENTS:
---
#### 3.5.1 Digital Circuits and Their Relationship to Boolean Algebra:

Consider the function F(x, y, z) = x + y′z
![[Pasted image 20230919104537.png]]

consider the function F(x, y, z) = xy + yz′ + xyz
![[Pasted image 20230919104721.png]]

##### Use Cases:
A good example is the use of the XOR operator to clear a storage location, as in A XOR A.

#### Bit Masks:
Boolean bit ==masking operations== are indispensable for ==processing individual bits in a byte==.

#### 3.5.3 Putting It All Together: From Problem Description to Circuit:
The steps for designing a Boolean circuit are as follows: (1) read the problem carefully to determine the input and output values; (2) establish a truth table that shows the output for all possible inputs; (3) convert the truth table into a Boolean expression; and (4) simplify the Boolean expression.

## 3.6 COMBINATIONAL CIRCUITS:
---
Combinational logic is used to build circuits that contain ==basic Boolean operators==, ==inputs==, and ==outputs==.

#### Half Adder:
Consider the problem of ==adding two binary digits== together.
There are only three things to remember: 
1. 0 + 0 = 0 
2. 0 + 1 = 1 + 0 = 1
3. 1 + 1 = 10
We need to specify two outputs, not just one, because we have a ==sum== and a ==carry== to address.

Truth Table:
![[Pasted image 20230919111035.png]]
A closer look reveals that Sum is actually an ==XOR==.
The Carry output is equivalent to that of an ==AND== gate

![[Pasted image 20230919111201.png]]

#### Full Adder:
![[Pasted image 20230919111448.png]]

==ripple-carry adder==:
we can build an adder capable of adding two 16-bit words, for example, by replicating the above circuit 16 times, feeding the carry out of one circuit into the carry in of the circuit immediately to its left

==black box approach==: Depicts a contained unit will all the individual gates hidden.
This is typically done with most circuits, including decoders, multiplexers, and adders.
![[Pasted image 20230919111746.png]]

#### Decoder:
A decoder uses the inputs and their respective values to select one specific output line.

Decoders are normally defined by the number of inputs and the number of outputs. For example, a decoder that has 3 inputs and 8 outputs is called a 3-to-8 decoder.

Decoders can take binary numbers and convert them into decimal outputs.
![[Pasted image 20230919113208.png]]

<iframe width="560" height="315" src="https://www.youtube.com/embed/7zffjsXqATg?si=Btxt-HgCP1y5bijO" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## 3.7 SEQUENTIAL CIRCUITS:
---
A sequential circuit defines its output as a function of both its current inputs and its previous inputs.
Therefore, the ==output depends on past inputs.==

*Synchronous sequential circuits* use ==clocks== to order events.
Most sequential circuits are ==edge triggered== (as opposed to being level triggered). This means they are allowed to change their states on either the rising or falling edge of the clock signal.
#### Flip-Flop:
Technically, a latch is level triggered, whereas a ==flip-flop is edge triggered==.

![[Pasted image 20230919125652.png]]
(a) SR Flip-Flop  
(b) Clocked SR Flip-Flop
(c) Characteristic Table for the SR Flip-Flop
(d) Timing Diagram for the SR Flip-Flop (assuming the initial state of Q is 0)

#### 3.7.4 Finite-State Machines:
**Finite-State Machines (FSMs)**:

1. **Definition**: FSMs are abstract mathematical models used to represent and control sequential processes or systems. They consist of a finite set of states, transitions between these states, and an initial state.

2. **Components**:
   - **States**: Discrete conditions or configurations that the system can be in.
   - **Transitions**: Rules or events that cause the system to change from one state to another.
   - **Initial State**: The starting point of the FSM.

3. **Types of FSMs**:
   - **Deterministic FSM (DFA)**: Each input uniquely determines the next state.
   - **Nondeterministic FSM (NFA)**: Multiple transitions from a state for the same input.
   - **Mealy Machine**: Outputs depend on both current state and input.
   - **Moore Machine**: Outputs depend only on the current state.

4. **Use Cases**:
   - FSMs are used in many areas, including automata theory, computer science, and control systems.
   - Regular expressions can be represented using FSMs for pattern matching.
   - In gaming, FSMs can model character behaviors and game state transitions.

5. **Advantages**:
   - Simplicity: FSMs are easy to understand and implement.
   - Predictability: Clear transitions make behavior easy to anticipate.
   - Scalability: FSMs can be extended for complex systems.

6. **Limitations**:
   - Limited Expressiveness: FSMs are not suitable for complex decision-making or memory-intensive tasks.
   - State Explosion: Complex systems may require a large number of states and transitions.
   - Lack of Context: FSMs do not capture historical information beyond the current state.

7. **Applications**:
   - Vending machines: FSMs model the sequence of actions when selecting and purchasing items.
   - Network protocols: FSMs define the sequence of messages and responses.
   - Text parsing: FSMs can tokenize and parse input strings based on patterns.

8. **Design Tips**:
   - Keep FSMs simple and well-documented for easier maintenance.
   - Use comments or diagrams to visualize the state-transition logic.
   - Consider the trade-off between determinism and flexibility when designing FSMs.

9. **Example**: Traffic light control can be modeled using an FSM with states like "Green," "Yellow," and "Red," transitioning based on a timer and sensor inputs.

10. **Conclusion**: Finite-State Machines are fundamental tools for modeling and controlling sequential processes, offering a clear and structured approach to solving various problems. Understanding their principles is valuable in various domains of computer science and engineering.