# Horizontal Dilution of Precision

Horizontal Dilution of Precision is a single number that indirectly provides information about the accuracy of a GPS point. See the wikipedia article [here](https://en.wikipedia.org/wiki/Dilution_of_precision_(navigation)).

| DOP Value | Rating | Description                                             |
| --------- | ------ | ------------------------------------------------------- |
| < 1	      | Ideal  | Highest possible confidence level to be used for applications demanding the highest possible precision at all times. |
| 1-2       | Excellent |	At this confidence level, positional measurements are considered accurate enough to meet all but the most sensitive applications. |
| 2-5	      | Good   | Represents a level that marks the minimum appropriate for making business decisions. Positional measurements could be used to make reliable in-route navigation suggestions to the user. |
| 5-10	    | Moderate | Positional measurements could be used for calculations, but the fix quality could still be improved. A more open view of the sky is recommended. |
|10-20      | Fair   | Represents a low confidence level. Positional measurements should be discarded or used only to indicate a very rough estimate of the current location. |
| >20       | Poor   | At this level, measurements are inaccurate by as much as 300 meters with a 6-meter accurate device (50 DOP × 6 meters) and should be discarded. |
