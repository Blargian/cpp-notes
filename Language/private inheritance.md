> is an is-implemented-in-terms-of relationship

makes the `public` and `protected` members of the base class `private` in the derived class.
The compiler will generally not automatically convert a derived class object into a base class object if needed.  (see [[item 39 - use private inheritance judiciously]])