# instructAR -- Enhancing Teaching Experience with AR

**Derek Zhang and Chih-Yun Tseng**

Welcome to our Advances in XR (CMSC498F/CMSC838C) final project ***instructAR***.

## Project Description
**instructAR** (pronounced *"instructor"*) is an mobile app that facilitates classroom teaching experience for instructors. There are 3 features that we are proposing for the app:
1. **Sentiment dectection with our original ML model:** During the pandemic, many teachers are having a hard time learning how students are doing (e.g. confusion or frustration) in class due to mask mandates. Our first step is to implement a user friendly system for sentiment detection on unoccluded faces. We are hopeful but not yet sure if this can be extended to masked faces (that's research?).

2. **AR studentID:** When teachers want to get to know their students better, they can use our app to scan a student's ID card and a mini AR resume will pop out listing the key informations about a student.

3. **Speak-into-text memo:** Many times, teachers ask students to "Remind me after class" or "Remind me on Piazza" if a question arouses during lecture. However, this usually causes both parties to forget about the reminder. Our app aims to enable the speak-into-text feature for teachers to transcribe in-class announcements into text memos.


## April 5th Project Proposal
[838c_final_project_presentation.pdf](https://github.com/chromestone/Advances-In-XR/files/8421427/838c_final_project_presentation.2.pdf)


## April 28th Project Progress Report
[838c_final_project_progress_report.pdf](https://github.com/chromestone/Advances-In-XR/files/8585267/838c_final_project_progress_report.pdf)

![Example](https://chromestone.github.io/Advances-In-XR/example.jpg =250x250)


## Mid-May Project Presentation
To be updated.

## References
1. Speech-to-text
   * 
2. AR student bussiness card
   * Vuforia Engine: https://library.vuforia.com/
3. Sentiment Detection Model

## Instructions
1. Before building the app on Xcode, activate speech-to-text feature by downloading required libraries: <br /><br />
  * ***Recommended***<br />
    * step 1) Clone the library manually
    ```
    git clone https://github.com/nhorvath/Pyrebase4.git
    ```
    * step 2) Find the path to your python3 site-packages directory (e.g. Library/Python/3.9/lib/python/site-packages) 
    ```
    python3 -m site
    the path should be under USER_SITE:
    ```
    * step 3) Drag ONLY the pyrebase folder to your local python3 directory from step (2)<br /><br />
  
  * ***Alternative (NOT recommended)***<br />
    ```
    pip install pyrebase4
    ```
2. In your local terminal, type in (be sure to add the quotes around the path)
  ```
  python3 audioProcessing.py "<path to the local directory that you want to test this project in>"
  ```

