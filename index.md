# instructAR -- Enhancing Teaching Experience with AR

**Derek Zhang (838C) and Chih-Yun Tseng (498F)**

Welcome to our Advances in XR (CMSC498F/CMSC838C) final project ***instructAR***.

## Table of contents
* [Introduction](#introduction)
  * [Example Images](#ex)   
* [Project Description](#pd)
  * [Problem Statement](#ps)
  * [Contributions](#contri)
  * [Challenges](#cha)
* [Related Work](#rwork)
* [Methodology](#method)
* [Results & Analysis](#res)
  * [Demo](#demo)
* [May 18th Project Presentation](#mmay)
* [April 28th Project Progress Report](#a28)
* [April 5th Project Proposal](#a5)
* [Instructions](#inst)
* [Links to our source code](#code)
* [References](#ref)

## Introduction <a name="introduction"></a>
_Imagine you're a teacher in a classroom of students wearing masks. You have no idea if they understand the lecture. Our project idea is to create a teaching aid using AR that can hint at what a student is feeling (e.g. confusion or frustration). Our first step is to implement a user-friendly system for sentiment detection on unoccluded faces. We are hopeful but unsure if this can be extended to masked faces._

_Want to get to know your students better? Our app aims to provide a quick scan of their student ID that will show links to their resume (e.g. LinkedIn site) and social media pages._

_Lastly, we also support the speech recognition feature that transcribes important information teachers might want to record during lecture time. It is often difficult to keep a memo while teaching at a fast pace. Teachers will be able to receive their transcribed memos from our website easily after class._

### Example images <a name="ex"></a>
<p>
  <img src="https://chromestone.github.io/Advances-In-XR/depth_estimation.gif" alt="Depth Estimation">
 <img src="https://chromestone.github.io/Advances-In-XR/example.jpg" alt="sentiment-detection" width="360" height="auto">
  <img src="https://user-images.githubusercontent.com/55725395/165830203-ad6de07b-94df-4308-84d4-e25e399afc8c.jpg" alt="Ar Card demo" width="250" height="auto">
  <div style="text-align: right;"><em>&#8679; (first pic) Left: 2D canvas without depth. Right: Using iris based depth estimation.</em></div>
</p>

## Project Description <a name="pd"></a>
**instructAR** (pronounced *"instructor"*) is an mobile app that facilitates classroom teaching experience for instructors. There are 3 features that we are proposing for the app:
1. **Sentiment dectection with our original ML model:** During the pandemic, many teachers are having a hard time learning how students are doing (e.g. confusion or frustration) in class due to mask mandates. Our first step is to implement a user friendly system for sentiment detection on unoccluded faces. We are hopeful but not yet sure if this can be extended to masked faces (that's research?).

2. **AR studentID:** When teachers want to get to know their students better, they can use our app to scan a student's ID card and a mini AR resume will pop out listing the key informations about a student.

3. **Speak-into-text memo:** Many times, teachers ask students to "Remind me after class" or "Remind me on Piazza" if a question arouses during lecture. However, this usually causes both parties to forget about the reminder. Our app aims to enable the speak-into-text feature for teachers to transcribe in-class announcements into text memos.

### Problem Statement <a name="ps"></a>

**TODO**

### Contributions <a name="contri"></a>
**Derek Zhang**: 
<br>
**Chih-Yun Tseng**: AR student ID, Speech-to-text feature, emoji overlay for sentiment dectection (without depth).

### Challenges <a name="cha"></a>

**TODO**

## Related Work <a name="rwork"></a>

**TODO**

## Methodology <a name="method"></a>

### Face Emotion Recognition (FER)

**What has already been done:**

TODO talk about only free APIs.
As far as we're aware mediapipe can handle everything up to face emotion recognition.

As for the deep learning side, as far as I'm aware there isn't research on this.

What I turned up by searching on Google Scholar were papers on the effect of masks on _humans_ performing face emotion recognition.

**What Derek Did:**

### AR Student ID 
This is built with the Vuforia engine. Vuforia supports image tracking which is very helpful for this feature. We set our UMD student IDs as image targets and then created game objects in Unity that serve as our AR cards. 

### Speech-to-Text Memo
At first, we wanted to see if there is any built-in support in Unity for speech recognition. However, most online sources are out-of-date or are not compatible with our devices (iOS). Some online blog posts suggest writing a wrapper that takes the speech recognition library (in Object-C) and turns it into C# code. This solution is quite hard to implement as we are not familiar with both languages (seems like the wrappers are based in CPP and also require knowledge of what Unity supports). Therefore, we chose to use Python which has well-established speech-recognition libraries (the one we are using is the google speech recognition). However, we soon realized that Unity does not support Python in any way. It has a pre-released Python package that is only functional in Unity Editor, which means any Python code would not run after build. Thus, we decided to run Python externally and host a website that can process speech recognition without having to mess with Unity. As a result, audio files are now uploaded to our Firebase Storage and user information is uploaded to Firebase Firestore. The reason that we use both Firebase Storage and Firebase Firestore is that audio files (e.g. wav files) cannot be stored in a normal NoSQL database. We have tried to convert the audio file into a byte array and recover it into a wav file but the content gets very distorted and often times it would not even work. The two databases communicate with a special key that is auto-generated whenever users hit the “save” button in our app. The probability of a key collision is extremely small (in fact, 1/36<sup>10</sup>). When users want to retrieve their speech-to-text memo, they can click on the “Speech-to-Text” button on our app and visit our [website](http://instructar.pythonanywhere.com/) and fill out a query to our backend. Our backend first checks whether the specified file has been processed before. If so, then it fetches the corresponding text memo from Firebase Firestore and sends the txt file directly to the user’s email address. If not, then our backend fetches the audio file from Firebase Storage and performs speech recognition internally. Before doing speech recognition, we filter out ambient noises that may affect the conversion. This is important because google’s speech recognition library is pretty sensitive to pre-recorded audio (i.e. a recording of another recording) and background noise. Lastly, it will update the speech-to-text result to Firebase Firestore to prevent redundant processing in the future.

## Results & Analysis <a name="res"></a>

### Demo <a name="demo"></a>
* [Speech-to-text Youtube Demo](https://youtu.be/bBLVGbJORTQ)
* AR Student ID 
<img src="https://user-images.githubusercontent.com/55725395/168929202-ab5fade5-7cd6-48f7-80d6-9f1148f24b26.gif" alt="AR Student ID" width="500">


### eyeFER on Paper

<img src="https://chromestone.github.io/Advances-In-XR/results/tradeoffs.png" alt="Trade Offs" loading="lazy">

<img src="https://chromestone.github.io/Advances-In-XR/results/model_accuracy.png" alt="Model Accuracy" loading="lazy">


### eyeFER in Practice

### Speech-to-Text Memo

* [Our website for speech-to-text memo](http://instructar.pythonanywhere.com/)

## May 18th Project Presentation <a name="mmay"></a>
To be updated.

## April 28th Project Progress Report <a name="a28"></a>
[498F/838c_final_project_progress_report.pdf](https://github.com/chromestone/Advances-In-XR/files/8585267/838c_final_project_progress_report.pdf)

## April 5th Project Proposal <a name="a5"></a>
[498F/838c_final_project_presentation.pdf](https://github.com/chromestone/Advances-In-XR/files/8421427/838c_final_project_presentation.2.pdf)

## Instructions <a name="inst"></a>
1. When running the project on Xcode, be sure to run the entire build file (open from the root folder) and not just the xcodeproj file.
2. Speech-To-Text recording instruction: <br> <img src="https://user-images.githubusercontent.com/55725395/168931265-c7b88d14-ca4e-4817-957d-d23359fe6ef2.png" alt="SP Instruction" width="600">

3. If you would like to perform queries on the database, please make sure that the specified email address and filename exists, and that the date is also relevant. By default, if an user only inputs their email address, they will receive all memos since May 1st 2022.

## Links to our source code <a name="code"></a>
* [Unity app code distribution](https://github.com/ctseng98/cmsc498F/tree/main/FinalProject%20(1))
* [Website + speech-to-text code](https://github.com/ctseng98/cmsc498F/tree/main/SpeechToText)
* [Face Emotion Recognition (ML) code](https://github.com/ctseng98/cmsc498F/tree/main/FinalProjectML)

## References <a name="ref"></a>
1. Speech-to-text
   * [Python tutorial](https://realpython.com/python-speech-recognition/)
   * [Firebase + Unity tutorial](https://youtu.be/Cq1JVjYfRXY)
   * [Google firebase](https://firebase.google.com/docs)
2. AR student bussiness card
   * [Vuforia Engine](https://library.vuforia.com/)
3. Sentiment Detection Model
   * [Affectnet Dataset](http://mohammadmahoor.com/affectnet/)
   * [Affectnet Subset (that we actually used)](https://www.kaggle.com/datasets/mouadriali/affectnetsample)
   * Keijiro's ports of MediaPipe to Unity using the Barracuda library: [BlazeFace](https://github.com/keijiro/BlazeFaceBarracuda), [Face Landmark](https://github.com/keijiro/FaceLandmarkBarracuda), and [Iris Landmark](https://github.com/keijiro/IrisBarracuda).
   * [MediaPipe ](https://google.github.io/mediapipe/)  (mainly for the face landmark model which we used to create the augmented dataset) and their [GitHub](https://github.com/google/mediapipe) where we found math for iris size to depth.
