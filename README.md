# Traverser
Routines to traverse a room intelligently using range finding

### Abstract
The robot will continuously check the distance of 180 degrees in front of it.
The robot will choose the path with the furthest distance. As it travels, it will
stop periodically and survey its distance options again for 180 degrees. It may then
alter its path based upon the new results. The robot will also constantly survey the
distance directly in front of it, and maintain a minimum distance in front of itself.
Violating this threshold will trigger a 180 degree survey.

### For the next steps
The robot will be aware of its last positions. It will choose to not travel near
paths, or along paths that it has already visited. 

### Routine Breakdown
#### Thread 1
The robot will first take a 180 degree survey and start its journey along the furthest
path. The increments for taking readings along this 180 degree span can vary. For instance,
it is possible to split 180 degrees into however many readings one desires.

#### Thread 2
Another thread will process the image frames for the minimum distance threshold in front of 
the robot. This will occur even when the robot is in motion. If the minimum distance is violated,
then the robot will automatically trigger a new 180 degree reading. 

If the new readings are even less than the threshold value, one will still be chosen. The
furthest distance, of the new readings, besides the one directly in front, will be chosen.

#### Thread 3
As a last resort, a bump sensor will still be in place. If a bump is detected, the robot will back
up and turn *away* from the direction in which the bump occurred. The robot will then contine forward
as normal.
