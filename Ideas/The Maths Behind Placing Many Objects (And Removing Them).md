# The Maths Behind Placing Many Objects (And Removing Them)

[Original Project](https://github.com/huchi57/GameObjectPainter)

| <img src="https://github.com/huchi57/GameObjectPainter/blob/main/Images/img-gameobjectpainter-example-demoassets.gif" alt="Example-of-object-painter-with-demo-assets" width="400"> |
| --- |
| This GIF demonstration uses Unity's 3D Game Kit demo assets. |

Inspired by Unity's 3D Game Kit, I created my own imlementation of an object painter, where users can define multiple sets of object brushes, and paint them in the world.

Here are some of the geometric maths behind this tool:

## Placing Objects
Here is the psuedo code of the object painting function:

```
function PaintObjects
    for i = 0 : maxItemNum
        set Ray R = Random ray casting in the direction shooting from the cursor, from brush volume V's top surface
        if Physics.Raycast(R, out Hit H)
            Place object O on H.point
            Orient O according to H.normal
```

It is very straightforward to implement placing objects - casting random rays down to a raycast surface, and we can get the hit point's position and normal direction, which is good for deciding the orientation of each element. The problem becomes more complex when the inverse function is implemented, that is making a brush that deletes objects that are in the brush volume.

When a deletion is executed, the brush finds all children objects under the object painter, and deletes any child object if it is inside the brush volume.

This problem can be breakdown into solving this generic question: *Given an arbitrary point, how can we know if it is inside a convex polyhedron?*

It can be break down into three types of shapes: general convex polyhedron, cylinder, and sphere.

## General Solution: Determine whether a point is inside a convex polyhedron
- V = 0
  - There are no vertecies. No point can be in this shape.
- V = 1 (Dot)
  - A dot. A point is only in this shape if they are at the same position. 
- V = 2 (Line segement)
  - Connecting two dots and we get a line segment. An arbitrary point is considered in this shape if it is on this line segment.
- V = 3 (Triangle)
  - Three dots make a triangle, or a fraction of an infinite plane. Using Unity's built-in function we can easily determine whether a point is in this triangle.
- V = 4 (Tetrahedron / triangular pyramid)
  - The simplest 3D-shape in a euclidean space is tetrahedron. It contains 4 vertices, 4 faces, and 6 edges. A point is in this tetrahedron only if for any plane constructed by picking random 3 vertices of the tetrahedron, the 4th vertex and the random point is on the same side.
  - A special case occurs when the tetrahedron has a heigh of 0, essentially turning it into a plane. In this case we fall back to solving this question considering V = 3.
```
function IsPointInTetrahedron(Point P, Tetrahedron T)
    for each combination of 3 vertices of the tetrahedron T:
        Construct a plane E using these 3 vertices, V0, V1, and V2.
        if the remaining vertex V3 of T is on the same side with E:
            return false 
return true
```
- V >= 5 (Polyhedron)
  - Any convex polyhedron (for simplicity, we assume all shapes using this method are convex) with 5 or more vertices can be break down into multiple tetrahedrons. We can iterate these sub-tetrahedrons and check if a random point is in these sub-shapes. If the point is in any of the tetrahedrons, we can guarantee that the point is also in this polyhedron.
```
for each combination of sub-tetrahedron T constructed by picking 4 vertices from the polyhedron H:
    if P is in T:
        return true
return false
```

Combining all the above steps, we have this pseudo code:

```
function IsPointInConvexPolyhedron(Point P, Polyhedron H)
    if H.numOfVerts == 0:
        return false

    if H.numOfVerts == 1:
        return P == H.verts[0]

    if H.numOfVerts == 2:
        set P' = P projected on Line(H.verts[0], H.verts[1])
        return P == P'

    if H.numOfVerts == 3:
        set E = Plane(H.verts[0], H.verts[1], H.verts[2])
        set P' = P projected on E
        return P == P'

    if H.numOfVerts == 4:
        set T = Tetrahedron from H
        return IsPointInTetrahedron(P, T)

    if H.numOfVerts >= 5:
        for each combination of sub-tetrahedron T constructed by picking 4 vertices from the polyhedron H:
            if P is in T:
                return true
return false
```

## Special Case - Cylinder
To determine if a point is inside a cylinder, we need to know the two center of the both surface on the two ends, and the radius of the cylinder. The point is in the cylinder if both conditions meet:
- The distance between the axis of the cylinder is less than the radius.
- The point is inside the space between the two planes expanded from both end surfaces of the cylinder.

## Special Case - Sphere
It is very straightforward to determine if a point is in a sphere. We only need to see if the distance to the point to the center of the sphere is greater than the radius.
