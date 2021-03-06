Customising Your Animation
=====================================

If you would like to customise the stylistic attributes of your generated animation (for example, the colors of particular variables or data structures), you can create a **stylesheet JSON file** containing your choices.
You can then pass this stylesheet into the compiler using the ``-s`` or ``--stylesheet`` flag. For more on command-line arguments, see the :ref:`Usage section <usage>`.

.. _stylesheet:

Stylesheet
----------

A typical stylesheet may look something like this:

.. code:: json

    {
      "variables": {
        "stack1": {
          "textColor": "blue",
          "creationStyle": "Write",
          "animate": {
              "borderColor": "blue"
          }
        }
      },
      "dataStructures": {
        "Stack": {
          "borderColor": "yellow",
          "animate": {
              "borderColor": "red",
              "textColor": "red",
              "animationStyle": "CircleIndicate"
          }
        }
      }
    }

Here, we define styles for the variable ``"stack1"`` and the data structure ``"Stack"``, which both map to their respective style properties. 

The style properties for ``"stack1"`` are applied to *all* variables in the program named ``stack1``, whether in global or local scope. This logic can be extended to all variables throughout the program. 

Meanwhile, the style properties for ``"Stack"`` are applied to *all* variables in the program that are of the type ``Stack``, and this again applies throughout all scopes. This works similarly for other data structures. (For a full list of the data structures available in VAlgoLang, see :ref:`here <data_structures>`).


Hide Code
^^^^^^^^^^^^^^

The ``hideCode`` property controls if the input program code and variable state will be displayed on the left hand side of the generated animation.

.. code:: json

    {
      "hideCode": true
    }

The values accepted for this are ``true`` and ``false``, with a default value of ``false``. This default means that code and variable state will be rendered.

If ``hideCode`` is set to ``true``, the code and variable state will not appear on the left hand side and the animation takes up the entire frame. However, you can still use ``stepInto`` and ``stepOver`` statement blocks to specify implicit code tracking that the animation reflects.

Hide Variables
^^^^^^^^^^^^^^

The ``hideVariables`` property controls if the variable state will be displayed on the left hand side of the generated animation.

.. code:: json

    {
      "hideVariables": true
    }

The values accepted for this are ``true`` and ``false``, with a default value of ``false``. This default means that variable state will be rendered.

If ``hideVariables`` is set to ``true``, the variable state will not appear on the left hand side and the code block stretches to takes up the entire left hand side of the frame, with the animation on the right hand side.

if ``hideCode`` is also set to ``true``, the code block will not appear either and this will have the same effect as just setting ``hideCode`` to true.

Hide Data Structures
^^^^^^^^^^^^^^^^^^^^

To hide any data structure by using the stylesheet, set its height and width to 0 in their stylesheet property.

.. code:: json

    {
      "positions": {
        "datastructure_name": {
          "x": -2,
          "y": -2,
          "width": 0,
          "height": 0
        },
      }
    }

Code Tracking
^^^^^^^^^^^^^^

To set the default code tracking of the program you can modify the ``codeTracking`` property. This controls if the code tracking animation will step into function
calls by default. 

.. code:: json

    {
      "codeTracking": "stepInto"
    }

The values accepted for this are `stepInto` and `stepOver`, with a default value of `stepInto`. This default means all function calls will be stepped into and animated. This attribute can be 
overwritten in code by using ``stepInto`` and ``stepOver`` statement blocks described :ref:`over here <code_tracking>`. 

Code Syntax Highlighting
^^^^^^^^^^^^^^^^^^^^^^^^^

Syntax highlighting has been enabled as a default. To switch off the syntax highlighting, you can add the ``syntaxHighlightingOn`` property to your stylesheet and set it to `false`.

.. code:: json

    {
      "syntaxHighlightingOn": true
    }

The values accepted for this are `true` and `false`, with a default value of `true`. 

Code Syntax Highlighting Style
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Syntax highlighting utlizes the `Pygment <https://pygments.org/demo/>`_ library. The default syntax highlighting style is ``inkpot``, and you can modify the ``syntaxHighlightingStyle`` property in your stylesheet.

.. code:: json

    {
      "syntaxHighlightingStyle": "inkpot"
    }

The values accepted for this are the following:
 * "inkpot"
 * "solarized-dark"
 * "paraiso-dark"
 * "vim"
 * "fruity"
 * "native"
 * "monokai" 

Code Line Separation
^^^^^^^^^^^^^^^^^^^^^^

Displaying new lines entered in your DSL is enabled as a default. To switch off the display of new lines, you can add the ``displayNewLinesInCode`` property to your stylesheet and set it to `false`.

.. code:: json

    {
      "displayNewLinesInCode": false
    }


Code Syntax Highlighting Tabulation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

When syntax highlighting is switched on, tabulation is defaulted to 2. To modify the size of tabulation within your code, you can modify the ``tabSpacing`` property in your stylesheet.

.. code:: json

    {
      "tabSpacing": 2
    }


Style Properties
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Here is a definitive list of the style properties you can define in a stylesheet. Please note that style properties can only be applied to data structures.

Colors
~~~~~~~

The following properties take Manim colors* as their values. 

* ``textColor``
* ``borderColor``

These colors can be written in upper case or lower case named format or as their hexadecimal value. The default for both is ``"white"``.

\*For a full list of compatible named colors available in Manim, see `here <https://github.com/3b1b/manim/blob/99952067c1a399e15a197310d35a39bb2864b1af/manimlib/constants.py#L199>`_. Please note that any color ending in ``_C`` can be replaced with just the name of the color (for example, ``BLUE_C`` can be written as ``BLUE``).

Creation style
~~~~~~~~~~~~~~~

You can specify the type of Manim ``Transform`` you would like to apply to data structures when they are being created, using the ``creationStyle`` property. The following options are available:

* ``FadeIn``
* ``FadeInFromLarge``
* ``Write``
* ``GrowFromCenter``
* ``ShowCreation``
* ``DrawBorderThenFill``

The default creation style is ``FadeIn``.

Animation Properties
~~~~~~~~~~~~~~~~~~~~~

Animation properties (denoted by ``"animate"``) are a subset of standard style properties. They define the stylistic attributes of data structures while they are being animated - for example, the color of any item being popped off the stack.

These take the ``textColor`` and ``borderColor`` properties listed in the `Colors <#colors>`_ section. You can also specify the type of Manim ``Transform`` you would like to apply to data structures when they are being animated, using the ``animationStyle`` property. The following options are available:

* ``FadeToColor``
* ``Indicate``
* ``ApplyWave``
* ``WiggleOutThenIn``
* ``CircleIndicate``
* ``TurnInsideOut``

The default animation style is ``FadeToColor``.

Precedence
~~~~~~~~~~~~~

The stylesheet for a ``.val`` program prioritises style properties associated with **variables** over those associated with **data structures**.

This can best be demonstrated using an example stylesheet:

.. code :: json

    {
      "variables": {
        "stack1": {
          "animate": {
              "borderColor": "blue",
              "textColor": "green"
          }
        }
      },
      "dataStructures": {
        "Stack": {
          "borderColor": "yellow",
          "animate": {
              "borderColor": "red",
              "textColor": "red"
          }
        }
      }
    }

In a program where ``stack1`` is a variable of type ``Stack``, ``stack1`` would have the following style properties:

* ``borderColor`` : ``"yellow"`` (defined for variables of type ``Stack``, and undefined for ``"stack1"``)
* ``textColor`` : ``"white"`` (defaults to ``"WHITE"`` as ``textColor`` is undefined for both ``"stack1"`` and ``"Stack"``)
* Animation properties (``"stack1"`` properties override ``"Stack"`` properties)

  * ``borderColor`` : ``"blue"``
  * ``textColor`` : ``"green"``

Positioning
^^^^^^^^^^^^^^^^^^^^^^

Data structures
^^^^^^^^^^^^^^^
The compiler runs an algorithm to automatically allocate space and position for each data structure defined as a variable in the program. However, you can manually define these positioning and sizes using the ``positions`` block.

The way to do this is by specifying a rectangular boundary where the data structure will always stay within. There are 4 compulsory fields to define a valid boundary:

* ``x`` - the bottom left x-coordinate of the boundary
* ``y`` - the bottom left y-coordinate of the boundary
* ``width`` - the width of the boundary
* ``height`` - the height of the boundary

The calculated coordinates will then be used to scale and place the data structure in the Manim coordinate system. By default, the scene in Manim is made up of an 8 x 14 grid, giving the possible ranges for each coordinate as follows:

* -7 ≤ ``x`` ≤ 7
* -4 ≤ ``y`` ≤ 4

Any data structure placed outside the above range will not be rendered and thus not show up in the animation. Note that if you choose to manually define the positioning for each data structure, then you have to make sure that the boundaries defined do not go out of the scene.

Below is an example of how you can define the positioning of a stack with the variable name ``stack1``:

.. code:: json

    {
      "positions": {
        "stack1": {
          "x": 1,
          "y": -3,
          "width": 2,
          "height": 6
        }
      }
    }

Another thing to note is that if you determine any positioning, the auto-allocation algorithm will not run. This means that if you choose to define the positioning of any variable of a data structure type, you need to do the same for all the variables of any data structure type defined in the program (including the ones defined inside called functions).

Code And Variable Blocks
^^^^^^^^^^^^^^^^^^^^^^^^

The code and variable blocks have a predetermined default positioning: The variable block is positioned at ``x = -7`` and ``y = 1.3`` with ``width = 5`` and ``height = 2.6``, and the code block at ``x = -7`` and ``y = -4`` with ``width = 5`` and ``height = 5.3``. This positions them at the very left of the screen, with the variable block taking up the top third and the code block taking up the bottom two thirds.
However, similar to data structures, it is possible to manually define these positioning and sizes using the ``positions`` attribute in the stylesheet.

Below is an example of how you can define the positioning of the code and variable blocks using the names ``_variables`` and ``_code`` respectively:

.. code:: json

    {
      "positions": {
        "_variables": {
          "x": 0,
          "y": -3,
          "width": 4,
          "height": 4
        },
        "_code": {
          "x": 0,
          "y": -2,
          "width": 4,
          "height": 4
        }
      }
    }
