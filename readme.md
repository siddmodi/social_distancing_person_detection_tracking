1. Track people and assign them unique id in a video file :

• I am using centroid tracking algorithm (They keep on tracking the coordinates of the object in the
frame)

• I am using mobinenetSSD model to detect person in a frame.

• In our case i am tracking the person and thus what i do is i keep on feeding the coordinates of the
person to the tracker and what tracker will do is it'll save the coordinates and then it'll compare
and calculate the distance btw the current coordinates and the previous coordinates and if it is below
some threshold value it'll keep tracking the object or else it'll not track and i will consider it to
be a new object.

• Tracker will do for the first frame it'll assign object some id's

• In the second frame the person will move slightly from their previous position, can't move very far
in one frame so our tracker will compare the coordinates of the next position to the previous
position coordinates and if it is below some threshold value , it'll keep assigning the same object id.

• Let's say for some reason the person gone out of the frame then the object id will wait from their
last location for some particular time for some particular frame which i will define in the tracker
itself, so if within that particular number of frames the person returns it'll assign the same object id
otherwise it'll assign the new object id.

• This cycle keeps on happening and in this way the tracker keeps on tracking a particular object in
the frame.

• I use Non-max-supression here bcz here the model can detect multiple bounding box for the same
person so to eliminate the extra boxes and keep the most perfect one i use this algorithm.

• I am reading the frames, resizing them , converting the frame to the blob , passing the blob to our
detector , In a for loop i am getting all the detections and appending them in a particular list and
after for loop i am passing all the rectangles to our non-max supression algorithm which'll remove
all the noises from it and i will have the correct detection in a list, then i pass all the coordinates or
bounding boxes to our tracker, tracker will accept this and give us object id and particulare
bounding box, i draw rectangle around the person using opencv and also put the object id on top of
the bounding boxes.




2. Monitor social distance:

• Here i am going to draw red bounding box when the social distancing is false and draw green
bounding box when the social distancing is true with the label on top of red bounding box as
'maintain social distance'.

• For detecting the person here i usee mobilenetSSD again.

• I detect person and based on bounding box of those person i will calculate the centroid, once i
have the centroid of a particular person i am going to calculate the distance between centroid 1 and
centroid 2 and if that distance is less then a threshold value i simply mark it as red which means
social distancing is false otherwise the bounding box will be green.

• Calculate centroid as int((x1+x2)/2.0) and i save all the centroids and the bounding box of the
person in the centroid dictionary.

• I iterate over that dictionary and use iter tools for using combinations of differnt persons and there
distances using centroids of there boundind boxes.

• I am adding all the centroids , bounding box of a particular id in a dictionary then i iterate over
that dictionary and calculating the distance between any 2 person and if that particular distance is
less then our defined threshold then i'm saying add it to the red zone otherwise don't add it.

• Those id which are in red zone i display them in red color otherwise it's in green color.



4. Detect person and state person detected

• Here i am using mobilenetSSD detection model

• I am reading the frames from the video file and resizing them, i calculate height and width of the
frame and convert the frame in blob and passing them in our detector and we are getting all the
detections

• I initialize a for loop for iterating over all the detections we got displaying the rectangular box for
the person.