# math-utils
Math functions to help game development 

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
        Vector3 lineDirection = (lineEnd - lineStart).normalized;
        float projectLength = Mathf.Clamp(Vector3.Dot(point - lineStart, lineDirection), 0f, lineDirection.magnitude);
        return lineStart + lineDirection * projectLength;
    }
```

