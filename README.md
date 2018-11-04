# Getting started

To get this running on your Raspberry Pi, you will need to clone this repository and then install OpenCV. As of November 3rd, 2018, I have a script that does all of this for you on a fresh install of Raspian Stretch!
Open up your terminal and type:
```
git clone https://github.com/lesreaper/pi-face-recognition.git
cd pi-face-recognition
chmod +x installOpenCV.sh
./installOpenCV.sh
```
Go and take a rest. This will take from 6 - 8 hours to install. We're building openCV 3.4.0 from source using only 1 CPU core (to make sure we don't run into any race condition errors). It's slow, but accurate.

This will create a virtual environment called "cv". So, anytime you want to work with OpenCV enabled, when you first open your terminal you'll type:
```
workon cv
```

# Once OpenCV is installed

You'll need to download some pictures of yourself, and put them in a folder you create with your name. If your name is Rich, and you downloaded images of yourself from the internet to your Downloads folder as "image1.jpg", etc, you would do that this way:

```
cd ~/pi-face-recognition/dataset
mkdir Rich
cd ~/Downloads
sudo mv image1.jpg ~/pi-face-recognition/dataset/Rich
repeat for each image, or you can drag and drop via the file explorer icon in your top toolbar
```

Then, create your embeddings:
```
python encode_faces.py --dataset dataset --encodings encodings.pickle \
	--detection-method hog
``` 

Finally, you're ready to run your webcam, or run it on an image to test it.
To run on webcam:
```
python pi_face_recognition.py --cascade haarcascade_frontalface_default.xml --encodings encodings.pickle
```

To run on a single image:
```
python pi_face_recognition_image.py --cascade haarcascade_frontalface_default.xml --encodings encodings.pickle` --image 6892945.jpeg
```

You can download your own image and replace it above.

This is all taken for the most part from Adrian's awesome blog here:
https://www.pyimagesearch.com/2018/06/25/raspberry-pi-face-recognition/

Buy his stuff. I've never taken a course that hasn't paid for itself many times over.

