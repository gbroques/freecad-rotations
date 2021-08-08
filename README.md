# FreeCAD Rotations

A guide on understanding how rotations work in FreeCAD.

## Prerequisites

Install [FreeCAD 19.2].

## Instructions

1. Start FreeCAD.
2. Select **Part** workbench from workbench dropdown.

   ![Part workbench](./part-workbench.png)

3. Click "*Create a cone solid*" button on toolbar.

   ![Create a cone solid](./Part_Cone.svg)

4. Set `Radius1` property of **Cone** to `0.00 mm`.
5. Select **View** > **Toggle axis cross** (`A`, `C`).
   * Red, Green, and Blue represents X, Y, and Z respectively.

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

[Euler angles] combine a series of rotations around X, Y, and Z axes into one rotation about one axis.

The order of multiplication is Z, Y, X[¹][1].

Ensure **View** > **Panels** > **Python console** is checked.

We can calculate the `Angle` and `Axis` vector and using FreeCAD.

```python
>>> from FreeCAD import Rotation, Vector
>>> x = Rotation(Vector(1, 0, 0), 90)
>>> z = Rotation(Vector(0, 0, 1), 90)
>>> r = z.multiply(x)
>>> r.Axis
Vector (0.5773502691896258, 0.5773502691896256, 0.5773502691896258)
>>> from math import degrees
>>> degrees(r.Angle)
119.99999999999999
```

How does FreeCAD caculate this though?

[FreeCAD 19.2]: https://github.com/FreeCAD/FreeCAD/releases/tag/0.19.2
[Euler angles]: https://en.wikipedia.org/wiki/Euler_angles
[1]: https://en.wikipedia.org/wiki/Euler_angles#Rotation_matrix
