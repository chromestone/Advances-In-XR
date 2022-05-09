# instructAR -- Enhancing Teaching Experience with AR

**Derek Zhang (838C) and Chih-Yun Tseng (498F)**

Welcome to our Advances in XR (CMSC498F/CMSC838C) final project ***instructAR***.

_Imagine you're a teacher in a classroom of students wearing masks. You have no idea if they are understanding the lecture. Our project idea is to create a teaching aid using AR that can hint at what a student is feeling (e.g. confusion or frustration). Our first step is to implement a user friendly system for sentiment detection on unoccluded faces. We are hopeful but not yet sure if this can be extended to masked faces._

_Want to get to know your students better? Out app aims to provide a quick scan on their student ID that will show links to their resume (e.g. LinkedIn site) and social media pages._

_Lastly, we also support speech recognition feature that transcribes important information teachers might want to record during lecture time. It is often difficult to keep a memo while teaching in a fast pace. Teachers will be able to receive their transcribed memo from our website easily after class._

* Example images <br />
  <img src="https://chromestone.github.io/Advances-In-XR/example.jpg" alt="sentiment-detection" width="512" height="auto">
  <img src="https://user-images.githubusercontent.com/55725395/165830203-ad6de07b-94df-4308-84d4-e25e399afc8c.jpg" alt="Ar Card demo" width="250" height="auto">

![Depth Estimation](https://chromestone.github.io/Advances-In-XR/depth_estimation.gif)

_Left: 2D canvas without depth. Right: Using iris based depth estimation._

## Project Description
**instructAR** (pronounced *"instructor"*) is an mobile app that facilitates classroom teaching experience for instructors. There are 3 features that we are proposing for the app:
1. **Sentiment dectection with our original ML model:** During the pandemic, many teachers are having a hard time learning how students are doing (e.g. confusion or frustration) in class due to mask mandates. Our first step is to implement a user friendly system for sentiment detection on unoccluded faces. We are hopeful but not yet sure if this can be extended to masked faces (that's research?).

2. **AR studentID:** When teachers want to get to know their students better, they can use our app to scan a student's ID card and a mini AR resume will pop out listing the key informations about a student.

3. **Speak-into-text memo:** Many times, teachers ask students to "Remind me after class" or "Remind me on Piazza" if a question arouses during lecture. However, this usually causes both parties to forget about the reminder. Our app aims to enable the speak-into-text feature for teachers to transcribe in-class announcements into text memos.


## April 5th Project Proposal
[838c_final_project_presentation.pdf](https://github.com/chromestone/Advances-In-XR/files/8421427/838c_final_project_presentation.2.pdf)


## April 28th Project Progress Report
[838c_final_project_progress_report.pdf](https://github.com/chromestone/Advances-In-XR/files/8585267/838c_final_project_progress_report.pdf)

## Mid-May Project Presentation
To be updated.

## References
1. Speech-to-text
   * https://realpython.com/python-speech-recognition/
   * https://youtu.be/Cq1JVjYfRXY
   * Google firebase: https://firebase.google.com/docs
   * The website that we've setup: http://instructar.pythonanywhere.com/
2. AR student bussiness card
   * Vuforia Engine: https://library.vuforia.com/
3. Sentiment Detection Model

## Instructions
1. When running the project on Xcode, be sure to run the entire build file and not just the xcodeproj file.
2. If you would like to perform queries on the database, please make sure that the specified email address and filename exists, and that the date is also relevant. By default, if an user only inputs their email address, they will receive all memos since May 1st 2022.

