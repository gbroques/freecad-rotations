# FreeCAD Rotations

A guide on understanding how rotations work in FreeCAD.

Understanding a rotation about one axis is simple to understand.

This guide focuses on rotating about more than one axis.

## Prerequisites

Install [FreeCAD 19.2].

## Rotating About More Than One Axis

1. Start FreeCAD.
2. Select **Part** workbench from workbench dropdown.

   [![Part workbench](./part-workbench.png)](https://wiki.freecadweb.org/Part_Module)

3. Click "*Create a cone solid*" button on toolbar.

   [![Create a cone solid](./Part_Cone.svg)](https://wiki.freecadweb.org/Part_Cone)

4. Set the `Radius1` property of the **Cone** to `0.00 mm`.
5. Select **View** > **Toggle axis cross** (`A`, `C`).
   * Red, Green, and Blue represents X, Y, and Z axes respectively.

   ![Cone before rotations](./cone-before-rotations.png)

7. With Cone selected, select **Edit** > **Placement** from the top main file menu.
9. Select "*Euler Angles (xy'z'')*" from the dropdown under "*Rotation*".
8. Enter 90° around x-axis.

   ![Cone rotated around x-axis by 90 degrees](./cone-rotated-around-x-axis-by-90-degrees.png)

9. and 90° around z-axis.

   ![Cone rotated around x and z axes by 90 degrees](./cone-rotated-around-x-and-z-axes-by-90-degrees.png)

10. Click the **OK** button.
11. The `Angle` is **120°**, and `Axis` is (**0.58**, **0.58**, **0.58**).
   * But *how is this calcuated*?

[Euler angles] combine a series of rotations around X, Y, and Z axes into a *single* rotation about *one* axis.

A rotation about Z, Y, and X axes is also know as a rotation about **Y**aw, **P**itch, and **R**oll axes ([from aircraft axes]).

|Yaw (Z)|
|:-----:|
|![Yaw](./yaw.gif)|

|Pitch (Y)|
|:-------:|
|![Pitch](./pitch.gif)|

|Roll (X)|
|:------:|
|![Roll](./roll.gif)|

> ***GIF Source:** [FreeCAD Wiki: Position and Yaw, Pitch and Roll].*

The order of multiplication is Yaw, Pitch, Roll[¹][1].

Ensure **View** > **Panels** > **Python console** is checked.

We can calculate the `Angle` and `Axis` vector and using FreeCAD.

```python
>>> from FreeCAD import Rotation, Vector
>>> yaw = Rotation(Vector(0, 0, 1), 90)
>>> roll = Rotation(Vector(1, 0, 0), 90)
>>> rotation = yaw.multiply(roll)
>>> rotation.Axis
Vector (0.5773502691896258, 0.5773502691896256, 0.5773502691896258)
>>> from math import degrees
>>> degrees(rotation.Angle)
119.99999999999999
```

How does FreeCAD caculate this though?

[FreeCAD 19.2]: https://github.com/FreeCAD/FreeCAD/releases/tag/0.19.2
[Euler angles]: https://en.wikipedia.org/wiki/Euler_angles
[from aircraft axes]: https://en.wikipedia.org/wiki/Aircraft_principal_axes
[FreeCAD Wiki: Position and Yaw, Pitch and Roll]: https://wiki.freecadweb.org/Placement#Position_and_Yaw.2C_Pitch_and_Roll
[1]: https://en.wikipedia.org/wiki/Euler_angles#Rotation_matrix
