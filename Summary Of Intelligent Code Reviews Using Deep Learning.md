# Summary Of Intelligent Code Reviews Using Deep Learning
I just learnt about the importance of Code Reviews and some automated Static and Dynamic code analysis methods and tools which could be used to achieve the Code Review process. Lets see some intelligent code review literature in the Deep Learning world.

**https://www.kdd.org/kdd2018/files/deep-learning-day/DLDay18_paper_40.pdf**

### Summary of Above paper

They build a deep learning based system in order to recommend a review of the common issues in the codebase. The system is called **DeepCodeReviewer (DCR)** and uses deep learning to learn review relevance to a code snippet and recommend the right review. 

DCR has been trained from Historical Code Reviews from Microsofts Internal Repositories.

Studies in retrospect show that reviewers tend to focus on reviews related to apparent bugs or best practices. These commonplace bugs distract reviewers from some areas of the code which are rare bugs in the program and takes a lot of developer time. DCR can alleviate this issue by recommending reviews associated with these common issues and let reviewers perform code on the important code with **high focus on essential defects**
