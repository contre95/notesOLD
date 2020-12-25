# Domain Drive en Design Reference

*Definitions and Pattern Summaries - (Eric Evans)*

# Definitions

### Domain

**Definition:** *A sphere of knowledge, influence, or activity. The subject area to which the user applies a program is the domain of the software.*

### Models

**Definition:** A system of abstraction that describes selected aspects of a domain and can be used to solve problems related to that domain.

### Ubiquitous language

**Definition:** *A language structured around the domain model and used by all team members within a bounded context to connect all the activities of the team with the software*

**Discussion:** The terminology of day-to-day discussions is disconnected from the terminology embedded in the code (ultimately the most important product of a software project).
Find easier ways of saying what you need to say, and then take the new ideas back down to the diagrams and code.
Play with the model as you talk about the system. Describe scenarios out loud using the elements and interactions of the model, combining concepts in ways allowed by the model.
Commit the team to use that language within the team and in the code. Refactor the code in order to commit to the language. Resolve confusion over term in conversation, in just the way we come to agree on the meaning of ordinary words

### Context

**Definition:** *The setting in which a word or statement appears that determines its meaning. Statements about a model can only be understood in a context.*

### Bounded context

**Definition:** *A description of a boundary (typically a subsystem, or the work of a particular team) within which a particular model is defined and applicable.*

Explicitly define the context within which a model applies. Explicitly set boundaries in terms of team organization, usage within specific parts of the application, and physical manifestations such as code bases and database schema.
Apply CI to keep model concepts and term strictly consistent within these bounds, but don't be distracted or confused by issues outside.
Standardize a single development process within the context, which need not be used elsewhere.
