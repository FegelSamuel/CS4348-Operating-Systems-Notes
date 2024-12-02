# Cheat Sheet
* Can be double-sided
* Can't share during exam (before is fine probably)
# Notes
* UML is NOT a modeling technique
* "Wicked" problems that are difficult or impossible to completely solve
* Waterfall bad
* Agile good
* Scrum good (maybe)
* Type of system influences the selection of architectural style (website is probably going to be an interactive system)
* Repository -> Databases
* MVVC -> Interactive System
* MVC is indeed an architectural style
* Use case is a business process
* -> means A -> B == A is B
  * A is a subclass of B
* -<> means A -<> B B has an A
  * Aggregation (Owner has the diamond)
* -<> (dark diamond) means composition
  * Composition is aggregation but the non-diamonded class doesn't exist without the diamonded class
* A use case is a singular thing. There can be multiple steps, but when you're defining the use case, you're not going to say all the steps at once
* System engineering is a top-down, divide-and-conquer approach.
## Transitive Verbs
A transitive verb is basically a verb that describes relations between classes. It doesn't necessarily tell you if there is an association between classes or not
## TUCBW TUCEW
* TUCBW - System begins with
* TUCEW- System ends with
* We're talking about scope

__:Person__ means an instance of Person

# Object Interaction Modeling
* Exception handling should be postponed to coding
* A box in a communication diagram DOES NOT represent the same amount of items as the corresponding box in a domain model
