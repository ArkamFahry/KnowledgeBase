tags:: [[CS]]

- # State Machine
	- A state machine is a conceptual model used in computer science and various fields to represent the behavior of systems. It's designed to capture the different states that a system can be in, the transitions between these states, and the events that cause these transitions.
	- ## Understanding State Machines
		- States
			- These are distinct conditions or situations in which a system can exist. For instance, in a vending machine, states might include "idle," "waiting for coins," "item selected," "dispensing," and "out of stock." Each state represents a specific configuration or condition of the system.
		- Transitions
			- These are the pathways or changes between states. Transitions occur in response to events. For example, when you insert a coin into a vending machine, it transitions from the "idle" state to the "waiting for coins" state. Transitions define how the system moves from one state to another.
		- Events
			- These are occurrences that trigger state transitions. Events can be various inputs, stimuli, or conditions such as user actions, sensor readings, or internal changes. In the vending machine example, events could be "coin inserted," "item selected," or "out of stock detected."
	- State machines can be represented visually as directed graphs or diagrams, with nodes representing states, edges representing transitions, and labels on edges indicating the triggering events. This graphical representation helps in understanding and designing the system's behavior.
	- ## There are two main types of state machines
		- ### Finite State Machines (FSM)
			- These have a finite number of states and specific rules determining which state the system moves to based on the current state and input.
		- ### Hierarchical State Machines (HSM)
			- These extend FSMs by allowing states to have sub-states, enabling more complex and structured modeling of system behavior.
	- State machines are widely used in software engineering, robotics, control systems, and many other domains to design, model, and implement the logic and behavior of systems in a clear and organized manner. They provide a systematic way of handling the dynamic behavior of systems and are crucial in ensuring predictability and reliability in complex systems.