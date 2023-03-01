# math-utils
Math functions to help game development 

1- Checking if 2 points are on the same side of the line (Y axis reference check)

```c#
public static bool AreBothPointsOnTheSameSideOfTheLine(Vector3 lineStart, Vector3 lineEnd, Vector3 p1, Vector3 p2)
    {
        Vector3 crossNext = Vector3.Cross(lineEnd - lineStart, p2 - lineStart);
        Vector3 cross = Vector3.Cross((crossNext.y > 0 ? lineEnd - lineStart : lineStart - lineEnd), p1 - lineStart);
        return cross.y > 0;
    }
```

![](https://github.com/Your_Repository_Name/Your_GIF_Name.gif)
