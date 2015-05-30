title: "OpenCV in a Choregraph Box"
date: 2015-05-30 21:18:43
tags:
---


[2] The last time, we developed a way to analyze movement on our computer. Thus the next logical step is to put that code on the NAO in order to process image from its own camera.

After struggling a bit on how to use the NAO camera service, we were soon able to fetch a frame from the camera and display its characteristics (width, height). The working code in the form of a Chrregraph box is available here:

``` python
#
# Cette box est une box basique permettant de récupérer une image
# de la caméra de NAO (grâve au service ALVideoDevice)
#

class MyClass(GeneratedClass):
    def __init__(self):
        GeneratedClass.__init__(self)

        self.avd = None
        self.strMyClientName = None

    def onLoad(self):
        self.connectToCamera()
        self.getImageFromCamera()
        self.disconnectFromCamera()

    def onUnload(self):
        self.avd = None
        self.strMyClientName = None

    def onInput_onStart(self):
        #self.onStopped() #activate the output of the box
        pass

    def onInput_onStop(self):
        self.onUnload() #it is recommended to reuse the clean-up as the box is stopped
        self.onStopped() #activate the output of the box


    def connectToCamera(self):
        self.log("STARTNAO: connecting to camera...")

        try:
            self.avd = ALProxy("ALVideoDevice")

            self.strMyClientName = self.avd.subscribeCamera(
                # Name              # CameraNum     # Resolution    # Colorspace        # FPS
                self.getName(),     0,              1,              11,                 5
            )

            self.log("STARTNAO: connected to camera")
        except BaseException, err:
            self.log("STARTNAO: error connecting to camera: %s" % err)


    def disconnectFromCamera(self):
        self.log("STARTNAO: disconnecting from camera...")

        try:
            self.avd.unsubscribe( self.strMyClientName )
        except BaseException, err:
            self.log("STARTNAO: error disconnecting from camera: %s" % err)

        self.log("STARTNAO: disconnected from camera")


    def getImageFromCamera(self):
        self.log("STARTNAO: getting camera image...")

        try:
            dataImage = self.avd.getImageRemote(self.strMyClientName)

            self.log("STARTNAO: camera image is null: %s" % dataImage is None)

            if dataImage is not None:
                self.log("STARTNAO: camera image property [0]: %s" % dataImage[0])
                self.log("STARTNAO: camera image property [1]: %s" % dataImage[1])
                self.log("STARTNAO: camera image property [2]: %s" % dataImage[2])

        except BaseException, err:
            self.log("STARTNAO: error getting camera image: %s" % err)

        self.log("STARTNAO: camera image got")

        return None
```

This box is the basis we are currently using to implement the algorithm we tested on our computer. It uses the log system of Choregraph to display frame properties to test the camera.