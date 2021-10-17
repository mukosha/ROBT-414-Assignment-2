# ROBT-414-Assignment-2

# “Follow Me” application on a NAO robot using Python NaoQi.
### Note: This assignment requires you to implement a “Follow Me” application on a Pepper robot using Python NaoQi.

## Requirements:
* I have used Windows 10)
* Python 2.7.18
* Choregraphe



## Goal:
Upon the start of the
application, the robot should wave hello and say: “Hi, human! I want to come with you”.
Then, the robot raises one of its arms for the user to hold it.

## You have to program your application in Python NaoQi and test with a virtual robot in Choreographe. 
There is a video on moodle on how to install and setup Python
NaoQi.


from naoqi import ALProxy
import time




## Just like in the test file:
## Use the same IP for the simulated robot

tts = ALProxy("ALTextToSpeech", "127.0.0.1", 9559)

names = list()
times = list()
keys = list()


## These are the positions of the joints that were obtained from the Choreographe
## By right-clicking on the keyframe on the timeline
## And then choosing the store joints on the keyframe
## Finally exporting motion to clipboard:
## Choose Python -> Bezier
## Paste the position into the Python
## The following settings for the Hello-motion were obtained:


names.append("HeadPitch")
times.append([1.16, 1.96])
keys.append([[0.00687858, [3, -0.4, 0], [3, 0.266667, 0]], [0.00687858, [3, -0.266667, 0], [3, 0, 0]]])

names.append("HeadYaw")
times.append([1.16, 1.96])
keys.append([[0.0128947, [3, -0.4, 0], [3, 0.266667, 0]], [0.0128947, [3, -0.266667, 0], [3, 0, 0]]])

names.append("LElbowRoll")
times.append([1.16, 1.96])
keys.append([[-0.563347, [3, -0.4, 0], [3, 0.266667, 0]], [-0.42083, [3, -0.266667, 0], [3, 0, 0]]])

names.append("LElbowYaw")
times.append([1.16, 1.96])
keys.append([[-1.18831, [3, -0.4, 0], [3, 0.266667, 0]], [-1.21014, [3, -0.266667, 0], [3, 0, 0]]])

names.append("LHand")
times.append([1.16, 1.96])
keys.append([[0.3213, [3, -0.4, 0], [3, 0.266667, 0]], [0.290926, [3, -0.266667, 0], [3, 0, 0]]])

names.append("LShoulderPitch")
times.append([1.16, 1.96, 6.4])
keys.append([[1.48725, [3, -0.4, 0], [3, 0.266667, 0]], [1.44734, [3, -0.266667, 0.0399129], [3, 1.48, -0.221517]], [-1.3439, [3, -1.48, 0], [3, 0, 0]]])

names.append("LShoulderRoll")
times.append([1.16, 1.96])
keys.append([[0.19986, [3, -0.4, 0], [3, 0.266667, 0]], [0.215891, [3, -0.266667, 0], [3, 0, 0]]])

names.append("LWristYaw")
times.append([1.16, 1.96])
keys.append([[0.106985, [3, -0.4, 0], [3, 0.266667, 0]], [0.106985, [3, -0.266667, 0], [3, 0, 0]]])

names.append("RElbowRoll")
times.append([1.16, 1.96])
keys.append([[0.410161, [3, -0.4, 0], [3, 0.266667, 0]], [0.586431, [3, -0.266667, 0], [3, 0, 0]]])

names.append("RElbowYaw")
times.append([1.16, 1.96])
keys.append([[1.19688, [3, -0.4, 0], [3, 0.266667, 0]], [1.309, [3, -0.266667, 0], [3, 0, 0]]])

names.append("RHand")
times.append([1.16, 1.96])
keys.append([[0.304904, [3, -0.4, 0], [3, 0.266667, 0]], [0.302336, [3, -0.266667, 0], [3, 0, 0]]])

names.append("RShoulderPitch")
times.append([1.16, 1.96, 3.12, 4, 5, 5.76])
keys.append([[-1.37183, [3, -0.4, 0], [3, 0.266667, 0]], [-1.37183, [3, -0.266667, 0], [3, 0.386667, 0]], [-0.963422, [3, -0.386667, -0.0759217], [3, 0.293333, 0.0575958]], [-0.905826, [3, -0.293333, 0], [3, 0.333333, 0]], [-1.19381, [3, -0.333333, 0], [3, 0.253333, 0]], [1.53938, [3, -0.253333, 0], [3, 0, 0]]])

names.append("RShoulderRoll")
times.append([1.16, 1.96, 3.12, 4, 5])
keys.append([[-0.235619, [3, -0.4, 0], [3, 0.266667, 0]], [-0.905826, [3, -0.266667, 0], [3, 0.386667, 0]], [0.0977384, [3, -0.386667, 0], [3, 0.293333, 0]], [-1.01404, [3, -0.293333, 0], [3, 0.333333, 0]], [0.0558505, [3, -0.333333, 0], [3, 0, 0]]])

names.append("RWristYaw")
times.append([1.16, 1.96])
keys.append([[-0.944223, [3, -0.4, 0], [3, 0.266667, 0]], [-0.944223, [3, -0.266667, 0], [3, 0, 0]]])



## The use of the Text-to-Speech to produce a message:

tts.say("Hi, Mukhamedzhan! I would like to come with you!")

try:
  motionProxy = ALProxy("ALMotion", "127.0.0.1", 9559)
  motionProxy.angleInterpolationBezier(names, times, keys)
except BaseException, err:
  print err

shoulder = "RShoulderPitch"
wrist = "RWristYaw"

Sensoring = 0



## The loop for the motion of the robot:
## + the left hand of the robot gets lifted and goes
## back to its original position
## by the end of the motion of the robot
while(1):
        
	x = motionProxy.getAngles(shoulder, Sensoring)
        y = motionProxy.getAngles(wrist, Sensoring)



        if x[0] <= (-0.59) :
             if y[0] < -0.69 :
                 motionProxy.moveTo(0.0, 0.0, 1.57) #postion given in radians & same as +90 deg
                 motionProxy.move(3.0, 0.0, 0.0)
             elif y[0] > 0.69 :
                 motionProxy.moveTo(0.0, 0.0, -1.57) #postion given in radians & same as -90 deg
                 motionProxy.move(3.0, 0.0, 0.0)
             else :
                 motionProxy.move(3.0, 0.0, 0.0)

        elif x[0] > (-0.59) and x[0] <= 0.79 :
             if y[0] < -0.69 :
                 motionProxy.moveTo(0.0, 0.0, 1.57) #postion given in radians & same as +90 deg
                 motionProxy.move(0.5, 0.0, 0.0)
             elif y[0] > 0.69 :
                 motionProxy.moveTo(0.0, 0.0, -1.57) #postion given in radians & same as -90 deg
                 motionProxy.move(0.5, 0.0, 0.0)
             else :
                 motionProxy.move(0.5, 0.0, 0.0)

        elif x[0] > 0.79:
             if y[0] < -0.69 :
                 motionProxy.moveTo(0.0, 0.0, 1.57) #postion given in radians & same as +90 deg
                 motionProxy.move(0.0, 0.0, 0.0)
             elif y[0] > 0.69 :
                 motionProxy.moveTo(0.0, 0.0, -1.57) #postion given in radians & same as -90 deg
                 motionProxy.move(0.0, 0.0, 0.0)
             else :
                 motionProxy.move(0.0, 0.0, 0.0)

  
        time.sleep(2)
