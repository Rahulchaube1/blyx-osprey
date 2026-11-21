## Score detections at the edge of a camera frame

Returns [visible IoU, matched, visible intersection area]. Match requires positive overlap and a score at least equal to the threshold. Invalid arguments and nonfinite results return an empty vector.

1. Open an empty file named `osprey-demo.blyx`.
2. Type `blyx-osprey-demo` and select **Osprey — runnable example**. You can also use **Snippets: Fill File with Snippet**.
3. Choose **Blyx: Run File** from the command palette. Change an argument near the end of `fn main()` to try another input.

Expected output

```text
0.5
1
4
```

[Work through the example in the browser](https://www.blyx-lang.space/play?example=package-osprey)
