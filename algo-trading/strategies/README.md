# Pine Coding Recommended Rules

# Naming Conventions

We recommend the use of:

camelCase for all identifiers, i.e., variable or function names: ma, maFast, maLengthInput, maColor, roundedOHLC(), pivotHi().
All caps SNAKE_CASE for constants: BULL_COLOR, BEAR_COLOR, MAX_LOOKBACK.
The use of qualifying suffixes when it provides valuable clues to the nature of the variable: maShowInput, bearColor, bearColorInput, volumesArray, maPlotID, resultsTable, levelsColorArray.

# Script organization

The Pine compiler is quite forgiving of the positioning of specific statements or compiler directives in the script. While other arrangements are syntactically correct, this is how we recommend organizing scripts:

<license>
<version>
<indicator/strategy/library_declaration_statement>
<import_statements>
<constant_declarations>
<inputs>
<function_declarations>
<calculations>
<strategy_calls>
<plots>
<alerts>

=============
====License===
=============
The reuse of code from those scripts is governed by our House Rules on Script Publishing which preempt the author’s license.

==============
====Version====
==============
//@version=5

===================================================
===<indicator/strategy/library_declaration_statement>===
===================================================
This is the call to indicator(), strategy() or library(), which defines the type of your script.

===================================================
==================<import_statements>===============
===================================================

If your script uses one or more Pine here, your import statements belong here.

===================================================
==============<constant_declarations>================
===================================================

What we consider to be constant definitions to be included in this section — and thus named using our SNAKE_CASE convention — are variables:

Initialized using a literal (e.g., 100 or "AAPL") or a built-in of “const” form (e.g., color.green)
Whose value does not change during the script’s execution
Literals used in more than one place in a script should always be used to initialize a constant. Using the constant rather than the literal makes it more readable if it is given a meaningful name, and the practice makes code easier to maintain. Even though the quantity of milliseconds in a day is unlikely to change in the future, MS_IN_1D is more meaningful than 1000 _ 60 _ 60 \* 24.

Note that:

Constants only used in the local block of a function or if, while, etc., statement for example, can be declared in that local block.
Using the var to initialize constants is unnecessary, and will incur a minor penalty on script performance.

============================================================
==========================<inputs>===========================
It is much easier to read scripts when all their inputs are in the same code section. Placing that section at the beginning of the script also corresponds to how they are processed, i.e., before the script begins execution.
===========================================================
=========================<function_declarations>=============
All user-defined functions must be defined in the script’s global scope; nested function definitions are not allowed in Pine.

The same syntax used in libraries can be used to document your functions.

=============================================================
=========================<calculations>=======================
This is where the script’s core calculations and logic should be placed. Code can be easier to read when variable declarations are placed near the code segment using the variables. Some coders prefer to place all their non-constant variable declarations at the beginning of this section, which is not always possible for all variables, as some may require some calculations to have been executed before their declaration.

============================================================
====================<strategy_calls>==========================
Strategies are easier to read when strategy calls are grouped in the same section of the script.

============================================================
==========================<plots>===========================
===========================================================
This section should ideally include all the statements producing the script’s visuals, whether they be plots, drawings, background colors, candle-plotting, etc. See the User Manual’s section on here for more information on how the relative depth of visuals is determined.

============================================================
==============================<alerts>=======================
============================================================
Alert code will usually require the script’s calculations to have executed before it, so it makes sense to put it at the end of the script.

============================================================
===========================Spacing==========================
===========================================================
A space should be used on both sides of all operators, except unary operators (-1). A space is also recommended after all commas and when using named function arguments, as in plot(series = close):

=============================================================
==========================Line Wrapping=======================
=============================================================
Line wrapping can make long lines easier to read. Line wraps are defined by using an indentation level that is not a multiple of four, as four spaces or a tab are used to define local blocks. Here we use two spaces:

=============================================================
========================Collapsible code sections===============
============================================================
Code sections in larger projects can be more cleanly defined using comments that make them easily identifiable and expandable/collapsible. Curly braces can be used in comments to define the beginning and end of code sections, which you can then expand or collapse using the small arrows in the Editor’s left margin:

// ———————————————————— Constants {
<constant_declarations>
// }

=============================================================
=======================Vertical alignment======================
=============================================================
Vertical alignment using tabs or spaces can be useful in code sections containing many similar lines such as constant declarations or inputs. They can make mass edits much easier using the Editor’s multi-cursor feature (ctrl + alt + 🠅/🠇):

// ———————————————————— Constants {

// Colors used as defaults in inputs.
color COLOR_AQUA = #0080FFff
color COLOR_BLACK = #000000ff
color COLOR_BLUE = #013BCAff
color COLOR_CORAL = #FF8080ff
color COLOR_GOLD = #CCCC00ff
// }

=============================================================
=======================Explicit typing=========================
=============================================================
Including the type of variables when declaring them is not required and is usually overkill for small scripts; we rarely use it in this manual. It can be useful to make the type of a function’s result clearer, and to distinguish a variable’s declaration (using =) from its reassignments (using :=). Using explicit typing can also make it easier for readers to find their way in larger scripts. We use explicit typing in both variable declarations here:

//@version=5
indicator("", "", true)
var float allTimeHi = high
allTimeHi := math.max(allTimeHi, high)
bool newAllTimeHi = ta.change(allTimeHi)
plot(allTimeHi)
plotchar(newAllTimeHi, "newAllTimeHi", "•", location.top, size = size.tiny)
============================================================
