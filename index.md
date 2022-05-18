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
  * [eyeFER on Paper](#eP)
  * [eyeFER in Practice](#ePr)
  * [Speech-to-Text Memo](#spAn)
  * [AR Student ID](#idAn)
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

The COVID-19 pandemic has caused an unprecendent number of individuals to begin wearing masks on a regular basis whether it be for regulatory or personal reasons. In the classroom setting, teachers rely on student's facial expression for cues on whether if students are understanding the lecture or not. In a masked classroom setting, face emotion recognition becomes challenging for the instructor.

However, deep learning models have been shown to be able to perform incredible tasks when given enough data. Thus, we want to investigate:

**How well can deep learning models perform on face emotion recognition without information about the lower half of the face, namely, the mouth?**

If this works even half of the times, it could aid teachers in identifying when students are confused over a complex topic.

### Contributions <a name="contri"></a>
**Derek Zhang**: integrated Keijiro's port of MediaPipe models (Face Detection, Face Landmarking, and Iris Landmarking) into our "pipeline", trained and analyzed deep learning models for FER/eyeFER, ported eyeFER/FER without locking up the app and added depth visualization to the app.
<br>
**Chih-Yun Tseng**: AR student ID, Speech-to-text feature, emoji overlay for sentiment dectection (without depth), app UI.

### Challenges <a name="cha"></a>

Face Emotion Recognition (FER) is a challenging task. In particular, the highest accuracy on AffectNet is 62.42% at the time of writing this report [(source)](https://paperswithcode.com/sota/facial-expression-recognition-on-affectnet).

Keep in mind that AffectNet has just 8 categories. Compare this to the performance on ImageNet, which has thousands of categories. Deep learning methods have already acheived over 90% top-1 accuracy on ImageNet [(source)](https://paperswithcode.com/sota/image-classification-on-imagenet).

We have to deal with the fact that we're creating a task, eye based face emotion recognition (eyeFER), that is even harder than an already hard task (FER)!

Not only did we have challenges with the high level task itself, we had multiple implementation challenges.

In particular, despite being advertised as mobile friendly, EfficientNet was over 10 times bigger than BlazeFace (Face Detection). That meant you could not call the entire model in one update loop.

Lastly, if we updated the world object too frequently (in depth estimation mode), (visually) it looked like as if it was the same thing as drawing on a 2D canvas. The solution was to use a exponential moving average to detect when new predictions started drifting from past predictions. (Simple Euclidean distance with thresholding).

* Speech-To-Text: Unity does not support native speech recognition.
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
* [Face Emotion Recognition Demo](https://youtu.be/2_4zIoR3mNc)
* [Speech-to-text Youtube Demo](https://youtu.be/bBLVGbJORTQ)
* AR Student ID 
<img src="https://user-images.githubusercontent.com/55725395/168929202-ab5fade5-7cd6-48f7-80d6-9f1148f24b26.gif" alt="AR Student ID" width="500">


### eyeFER on Paper <a name="eP"></a>

**Terminology**

* AffectNet - The original dataset (we used a subset that was publicly available). All other AffectNet datasets types mentioned are created by transforming this dataset in some way.
* Augmented - We performed face landmarking on the images in the dataset and zero-ed out the pixels below the nose line.
* Compressed - The emotions are redefined as follows:
  * activated - fear or surprise
  * irritated - anger or disgust
  * neutral - neutral or contempt
  * happiness - happiness
  * sadness - sadness

**Figures**

<div>
  <div style="width:50%; float:left;">
    <img src="https://chromestone.github.io/Advances-In-XR/results/tradeoffs.png" alt="Trade Offs" loading="lazy" width="50%">
  </div>
  <div style="width:50%; float:left">
    <img src="https://chromestone.github.io/Advances-In-XR/results/tradeoff_zoomed.jpg" alt="tradeoff_zoomed" loading="lazy" width="50%">
  </div>
  <div style="clear:both; display:table;"></div>
  <b>Figure 1 - Left: Ensemble model using weighted average on baseline and finetuned. Right: Zoomed in on the peformance on the augmented dataset (to better show the shape and characteristics of the curve).</b>
</div>

<img src="https://chromestone.github.io/Advances-In-XR/results/model_accuracy.png" alt="Model Accuracy" loading="lazy" width="70%">
<b>Figure 2 - Comparison of accuracies between the baseline and finetuned model on various dataset transformations. Note that the colored circles directly map to points in fig. 1.</b>

<div>
  <div style="width:50%; float:left;">
    <img src="https://chromestone.github.io/Advances-In-XR/results/baseline_affectnet_subset.jpg" alt="baseline_affectnet_subset" loading="lazy" width="50%">
  </div>
  <div style="width:50%; float:left">
    <img src="https://chromestone.github.io/Advances-In-XR/results/finetuned_affectnet_subset.jpg" alt="baseline_affectnet_subset" loading="lazy" width="50%">
  </div>
  <div style="clear:both; display:table;"></div>
  <b>Figure 3 - Confusion matrices on the original AffectNet dataset. The margins show the row and column totals.</b>
</div>

<div>
  <div style="width:50%; float:left;">
    <img src="https://chromestone.github.io/Advances-In-XR/results/baseline_affectnet_augmented.jpg" alt="baseline_affectnet_augmented" loading="lazy" width="50%">
  </div>
  <div style="width:50%; float:left">
    <img src="https://chromestone.github.io/Advances-In-XR/results/finetuned_affectnet_augmented.jpg" alt="baseline_affectnet_augmented" loading="lazy" width="50%">
  </div>
  <div style="clear:both; display:table;"></div>
  <b>Figure 4 - Confusion matrices on the augmented dataset where the lower half of the face is removed.</b>
</div>

<div>
  <div style="width:50%; float:left;">
    <img src="https://chromestone.github.io/Advances-In-XR/results/baseline_affectnet_compressed.jpg" alt="finetuned_affectnet_compressed" loading="lazy" width="50%">
  </div>
  <div style="width:50%; float:left">
    <img src="https://chromestone.github.io/Advances-In-XR/results/finetuned_affectnet_compressed.jpg" alt="finetuned_affectnet_compressed" loading="lazy" width="50%">
  </div>
  <div style="clear:both; display:table;"></div>
  <b>Figure 5 - Confusion matrices on the augmented dataset where the lower half of the face is removed and evaluation with compressed emotions.</b>
</div>

### eyeFER in Practice <a name="ePr"></a>

**Student Testimonies**

"I was impressed with how consistently the app could predict my mood even with a mask on." - Garrett (UMD Computer Science Undergrad)

"This is actually really useful." - Sahil M. (UMD Computer Science Undergrad)

**Feedback from Professionals**

_How useful would this app have been to your teaching in a masked classroom setting?_

* "4/5" - Dr. Raymond Tu (UMD FIRE Capital One Machine Learning Faculty Leader)
* "4/5" - Dr. Stefan Doboszczak (UMD Department of Mathematics)

Of course, we also report on negative results:

_What emotions does the model seem to get wrong when you wear a mask?_

* "Happiness" - Garrett
* "All emotions, but it's expected" - Dr. Tu
* "Irritated" - Dr. Doboszczak

_How useful would this app be once masking in classrooms becomes optional?_

"2/5" - Dr. Tu and Dr. Doboszczak

It's clear that once the pandemic has abated, eyeFER will not be very useful in all but the most niche scenarios.

However, after reading papers analyzing the effect of face masks on various populations such as [individuals with autistic traits](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0257740), I've realized that we may be able to flip this technology around. Hence, I remain hopeful that, even if no teachers want to use our app post pandemic, we can use this to help students with mental disorders.

### Speech-to-Text Memo <a name="spAn"></a>

* [Our website for speech-to-text memo](http://instructar.pythonanywhere.com/)
* Analysis: We tested the speech recognition feature on the following variables: content complexity, speaker fluency, and with/without wearing masks. For content complexity, we have two scripts where one is just a casual note that does not involve any uncommon/professional vocabulary and another that contains special vocabularies used in the math field. For the casual script, the result for both speakers are around a high 90% accuracy (with and without wearing a mask). However, our second script had more complicated vocabularies like "Lipschitz" as well as homophones "R<sup>n</sup>" and "R<sup>m</sup>" where the letter "n" and "m" can be easily confused. Our result shows that the speech recognition has a lower accuracy for the speaker with accent in this context. Nonetheless, the speech recognition feature can precisely distinguish even "n" and "m" for the native English speaker. Finally, all test results showed that speech recognition with masks is more difficult than without masks. Future work such as denoising the raw audio file can be done in order to improve the accuracy rate. 

<img width="703" alt="Screen Shot 2022-05-17 at 10 19 26 PM" src="https://user-images.githubusercontent.com/55725395/168944253-98a5f217-427f-43ad-ae47-c3c1a2625e80.png">
<img width="703" alt="Screen Shot 2022-05-17 at 10 19 30 PM" src="https://user-images.githubusercontent.com/55725395/168944266-83e3e6d4-f26f-4da1-82e7-22ede0cacc84.png">

### AR Student ID <a name="idAn"></a>
See [demo](#demo) in earlier section.

## May 18th Project Presentation <a name="mmay"></a>
To be updated.

## April 28th Project Progress Report <a name="a28"></a>
[498F/838c_final_project_progress_report.pdf](https://github.com/chromestone/Advances-In-XR/files/8585267/838c_final_project_progress_report.pdf)

## April 5th Project Proposal <a name="a5"></a>
[498F/838c_final_project_presentation.pdf](https://github.com/chromestone/Advances-In-XR/files/8421427/838c_final_project_presentation.2.pdf)

## Instructions <a name="inst"></a>
1. When running the project on Xcode, be sure to run the entire build file (open from the root folder) and not just the xcodeproj file.
2. Speech-To-Text recording instruction: <br /> <img src="https://user-images.githubusercontent.com/55725395/168931744-6b53a6d8-37a0-410b-9f63-e2d38b7f3ee5.png" alt="SP Instruction" width="600">

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
   * Face Emotion Recognition by A. Savchenko: [paper](https://arxiv.org/abs/2103.17107) and [code](https://github.com/HSE-asavchenko/face-emotion-recognition).
   * Keijiro's ports of MediaPipe to Unity using the Barracuda library: [BlazeFace](https://github.com/keijiro/BlazeFaceBarracuda), [Face Landmark](https://github.com/keijiro/FaceLandmarkBarracuda), and [Iris Landmark](https://github.com/keijiro/IrisBarracuda).
   * [MediaPipe ](https://google.github.io/mediapipe/)  (mainly for the face landmark model which we used to create the augmented dataset) and their [GitHub](https://github.com/google/mediapipe) where we found math for iris size to depth.
