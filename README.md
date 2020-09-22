# Explain

Explain is a project developed from Aries to create explanation from plan.
You can use explain on your own plan generated by your own planer. 

## Building

Build relies on `cargo` can be triggered like so:

```
cargo build # debug non-optimized build
cargo build --release ## optimized build
```

This build compile artifacts and place them in the `target/debug` or `target/release` directory.

## Executable

- `explain`: a tool to create explanation for a plan from a PDDL problem.


```
cargo install --path . 
``` 

To use explain you should pass the pddl problem file (`explain` will try to find the associated domain file by itself), a valid plan for this problem and some additional options:
```
./target/release/explain <path/to/problem.pddl> <path/to/plan> <Options>
```

Options available for explain:
```
-d <domain-file>    # To give explicitly the domain of the problem
-s                  # To create dot file for support
-m                  # To create dot file for threat
-t                  # To create dot file for temporal representation
-q question         # Ask question
-i                  # interactive mode
```

Form of the question "question parameters"

Questions available:

 - `support <step>`                             : Display others steps support by step 
 - `supported <step>`                           : Display others steps support of step
 - `goal <step>`                                : Display true if step accomplish a goal
 - `necessary <step>`                            : Display if step participates to the accomplishment of a goal, necessary-d to have the shortest path
 - `path <source-step> <target-step>`           : Display path between two steps, path-d to have the path.
 - `threat <source-step> <target-step>`         : Display if source-step threats target-step if it put right before.
 - `betweeness <n-score>`                       #Display all step with a betweeness upper than the n-th score.
 - `synchro <parameters>`                       : Display step that make link between group based on parameters
 - `parallelizable <step> <step>`               : Display a boolean to know if the two steps are parallelizable, parallelizable-d to have more detail
 - `weight <weight> <step> <step> <parameters>` : Display a path between two steps with the least possible parameters of the list (weight is a number)


Example of question : "support 4"

# Interactive mode

When using the option `-i` you will enter the interactive mode in which you have access to the following commands

    support-graph   Generate dot support and display matrix support
    threat-graph    Generate dot threat and display matrix threat
    <question>      A question in same format as option -q without "" 
    gg              Make plan with aries planificator if you have suspicion about your plan
    p               Display plan
    h               Help
    e or q          Exit

if you want to use your dot file to make a graph, use graphviz with:

```
dot -Tpng graphique.dot -o graph.png
```

Or display it directly with xdot:

```
xdot graphique.dot
```