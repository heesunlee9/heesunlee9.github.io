---
title:  "Fundamental Limitations of Deep Learning and Solutions"
excerpt: "I am skeptical of the fundamental methodologies of deep learning. I will review the main limitations of deep learning, and their solutions.  "

categories:
  - Blog
tags:
  - Blog
last_modified_at: 2019-04-13T08:06:00-05:00
---

[PDF](https://drive.google.com/file/d/1fxqZGX4iVP0l-T4mLQl-otNEgeNQTOas/view?usp=sharing) 

I wrote this paper out of personal interest.  

I am skeptical of the fundamental methodologies of deep learning. I will review the main limitations of deep learning, and their solutions.  

According to Deep Learning: A Critical Appraisal by Gary Marcus, deep learning has some fun-damental  defects.   Fundamentally,  it  lacks  adaptability.   Specifically,  deep  learning  models  have difficulty in dealing with deviations.  We put data into a model and have the model optimize itself. We repeat this process until we get satisfactory results.  If a certain model has not been trained by specific examples, a test set differs from a training data set or some conditions change, the failure rate increases drastically.  Besides, current deep learning methods based on math and statistics areironic.  Although we may have no mathematical errors in the process of training, we may discover basic errors which humans may not have made.  Also, deep learning is not good at using contextual information when discerning objects.  

The above trial-and-error strategy may be especially unsuitable for embedded software with a limited specification, safety-critical software, and real-time systems.  Even in a desktop environment, neural network computation takes substantial time to generate meaningful results.  Thus, embedded software may have less operational speed due to such computations.  Also, in safety-criticalor  real-time  systems,  we  do  not  have  much  time  to  garner  a  large  amount  of  data  in  advance,preprocess the data, optimize it, and examine the results.  It may lead to an unexpected situation. What I am seeking are solutions on how to build reliable, fit for purpose applications.  

Marcus  proposes  unsupervised  learning  as  an  alternative  to  the  above  problems.   Similarly,  hepresents replacing labeled data sets with things such as videos that change over time.  He addsthat one problem of deep learning is that it requires a large number of data sets.  We especiallyneed such data in supervised learning and we have to add labels to each training data set.  On theother hand, unsupervised learning is convenient in that we need less data and do not have to label it.  

The lack of need for labels is a significant advantage of unsupervised learning.  However, unsuper-vised learning may not be a fundamental solution.  Let us say we develop an application and it fits well with supervised learning.  Do we have to use unsupervised learning in that situation?  Also,unsupervised learning still needs a substantial amount of data.  It is also important to evaluate efficiency when replacing labels with videos or frames. According to Marcus, frames in the videowork as labels.  Nonetheless, if we process a high-volume video, it may take too much time andcomputing resources to train data using frames.  For this reason, using conventional labels can bemore profitable in some cases.  

Marcus  then  suggests  another  alternative  may  be  to  integrate  deep  learning,  which  is  good  atclassification, with symbolic systems, which excel at inference and abstraction.  This ‘hybrid model’ may be a more plausible idea than the solutions already discussed.  The advantages of symbolicsystems may partially prevent a model from giving absurd results.  Also, Marcus contends that it would be valuable to integrate microprocessor-like operations into neural networks, more closely approximating the structure of the human brain.  In detail, we may set Python classes for eachbrain area and make each class process our data according to their role.  In this case, we may escape from the current input layer-hidden layer-output layer simplicity of neural network structure.  We may  also  resolve  some  difficulties  of  deep  learning  such  as  debuggability,  interpretability,  and open-ended inference.  

Marcus also contends that we can gain insight from cognitive science and developmental psychologyas well as from statistics.  What matters is how to teach human knowledge to computers.  Let usassume that we understood how a human develops common sense knowledge and integrates it intotheir existing thinking system.  In the end, it would be important to determine how to translate our knowledge into algorithms and programming languages which our computers can understand.The challenge is that the human thinking process is too complex to apply to a neural network withweight and bias.  In this regard,  combining microprocessor-like operations with neural networkscan be a more intuitive way to manifest human cognitive function. 

Unless  we  come  up  with  a  breakthrough  to  the  above  limitations,  full-service  artificial  general intelligence might be a mere fantasy.  From this point of view, focusing on what computers and humans can do well may be a more productive aspiration.  Computers are good at multitasking and complicated, massive computations.  Humans are good at abstraction, generalization, and real-time logical inference.  We may have computers perform computations and integrate our knowledge with the results to make a final judgment.  To sum up, we have to define exactly what expectations we can reasonably have for artificial intelligence.
