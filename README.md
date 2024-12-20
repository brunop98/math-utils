# math-utils
Math functions to help game development 
You can support me checking my website: http://harpiagames.com

Code for Unity 3D

<h2>Checking if 2 points are on the same side of the line (Y axis reference check)</h2>

<img src="https://raw.githubusercontent.com/brunop98/math-utils/main/gifs/20230301_115704.gif" height="250"/>

```c#
public static bool AreBothPointsOnTheSameSideOfTheLine(Vector3 lineStart, Vector3 lineEnd, Vector3 p1, Vector3 p2)
    {
        Vector3 crossNext = Vector3.Cross(lineEnd - lineStart, p2 - lineStart);
        Vector3 cross = Vector3.Cross((crossNext.y > 0 ? lineEnd - lineStart : lineStart - lineEnd), p1 - lineStart);
        return cross.y > 0;
    }
```

<h2>Get Closest Point On Finite Line</h2>

<img src="https://raw.githubusercontent.com/brunop98/math-utils/main/gifs/20230301_135552.gif" height="250"/>

```c#
public static Vector3 GetClosestPointOnFiniteLine(Vector3 point, Vector3 lineStart, Vector3 lineEnd)
    {
        Vector3 lineDirection = lineEnd - lineStart;
        float lineLength = lineDirection.magnitude;
        lineDirection.Normalize();
        float projectLength = Mathf.Clamp(Vector3.Dot(point - lineStart, lineDirection), 0f, lineLength);
        return lineStart + lineDirection * projectLength;
    }
```

<h2>Draw Bounds on Gizmos</h2>

```c#
private static void DrawBoundsOnGizmos(GameObject objWithRenderer)
        {
            if (objWithRenderer == null) return;

            Bounds bounds = objWithRenderer.GetComponentInChildren<MeshRenderer>().bounds;

            Gizmos.color = Color.red;
            Gizmos.DrawWireCube(bounds.center, bounds.size);

            Vector3[] vertices = new Vector3[8];
            vertices[0] = bounds.center + new Vector3(bounds.extents.x, bounds.extents.y, bounds.extents.z);
            vertices[1] = bounds.center + new Vector3(-bounds.extents.x, bounds.extents.y, bounds.extents.z);
            vertices[2] = bounds.center + new Vector3(-bounds.extents.x, -bounds.extents.y, bounds.extents.z);
            vertices[3] = bounds.center + new Vector3(bounds.extents.x, -bounds.extents.y, bounds.extents.z);
            vertices[4] = bounds.center + new Vector3(bounds.extents.x, bounds.extents.y, -bounds.extents.z);
            vertices[5] = bounds.center + new Vector3(-bounds.extents.x, bounds.extents.y, -bounds.extents.z);
            vertices[6] = bounds.center + new Vector3(-bounds.extents.x, -bounds.extents.y, -bounds.extents.z);
            vertices[7] = bounds.center + new Vector3(bounds.extents.x, -bounds.extents.y, -bounds.extents.z);

            Gizmos.color = Color.green;
            foreach (Vector3 vertex in vertices)
                Gizmos.DrawSphere(vertex, 0.05f);
        }
```

<h2>Inverse Bisector</h2>

<img src="https://raw.githubusercontent.com/brunop98/math-utils/main/gifs/bissector.gif" height="250"/>

Returns the blue line direction

```c#
public static Vector3 GetInverseBissector(Vector3 p1, Vector3 p2, Vector3 p3)
    {
        Vector3 newP1 = (p1 - p2).normalized + p2;
        Vector3 newP3 = (p3 - p2).normalized + p2;
        Vector3 bisector = (newP1 + newP3) / 2;
        return (p2 - bisector).normalized;
    }
```
<h2>Bounds Center</h2>

Returns the bounds center of the object and it`s children.

```c#
public static Bounds GetBounds(Transform obj)
        {
            Renderer[] renderers = obj.GetComponentsInChildren<Renderer>();
            
            if (renderers.Length == 0) return new Bounds(obj.position, Vector3.zero);

            Bounds bounds = renderers[0].bounds;
            for (int index = 1; index < renderers.Length; index++)
            {
                Renderer renderer = renderers[index];
                bounds.Encapsulate(renderer.bounds);
            }

            return bounds;
        }
```

<h2>Area of ant triangle</h2>

Returns the area of a triangle giben its 3 vertices point.

```c#
    public static float CalculateAreaOfTriangle(Vector3 a, Vector3 b , Vector3 c)
    {
        float res  = Mathf.Pow(((b.x * a.y) - (c.x * a.y) - (a.x * b.y) + (c.x * b.y) + (a.x * c.y) - (b.x * c.y)), 2.0f);
        res += Mathf.Pow(((b.x * a.z) - (c.x * a.z) - (a.x * b.z) + (c.x * b.z) + (a.x * c.z) - (b.x * c.z)), 2.0f);
        res += Mathf.Pow(((b.y * a.z) - (c.y * a.z) - (a.y * b.z) + (c.y * b.z) + (a.y * c.z) - (b.y * c.z)), 2.0f);
        return Mathf.Sqrt(res) * 0.5f;
    }
```