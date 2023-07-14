+++
date = "2022-07-25"
title = "Agent-based Modeling of Simulations of the Spiral of Silence"
description = "The post demonstrates Mermaid JS support"
+++

This blog contains main content of my project. You can find it on my [Github](https://github.com/shen-yuxi/Simulations-of-the-Spiral-of-Silence) as well. Feel free to reach out to me for the full paper.



## Table of Contents
- [Table of Contents](#table-of-contents)
- [0. Research Questions](#0-research-questions)
- [1. Modeling Variable Settings and Rules](#1-modeling-variable-settings-and-rules)
  - [1.1. Initial Settings of Variables](#11-initial-settings-of-variables)
    - [(1) Netizens:](#1-netizens)
    - [(2) Hardcores:](#2-hardcores)
    - [(3) Opinion leaders:](#3-opinion-leaders)
  - [1.2 Patches variables: mainstream media](#12-patches-variables-mainstream-media)
    - [(1) Opinion value](#1-opinion-value)
    - [(2) Scope of influence](#2-scope-of-influence)
  - [1.3 Global variables](#13-global-variables)
    - [(1) Opinion value](#1-opinion-value-1)
    - [(2) Neighbors](#2-neighbors)
    - [(3) Opinion expression threshold](#3-opinion-expression-threshold)
    - [(4) Opinion distance](#4-opinion-distance)
    - [(5) Opinion climate of mainstream media](#5-opinion-climate-of-mainstream-media)
- [2. Control Variables and Monitor Data](#2-control-variables-and-monitor-data)
  - [2.1 Control variables](#21-control-variables)
  - [2.2 Monitor data](#22-monitor-data)
- [3. Analysis of Silent Spiral Phenomena in the Model](#3-analysis-of-silent-spiral-phenomena-in-the-model)
  - [3.1 Correlation analysis between opinion expression thresholds with opinion expression attitudes and opinion factions](#31-correlation-analysis-between-opinion-expression-thresholds-with-opinion-expression-attitudes-and-opinion-factions)
  - [3.2 Correlation analysis between opinion leaders with opinion expression attitudes and opinion factions](#32-correlation-analysis-between-opinion-leaders-with-opinion-expression-attitudes-and-opinion-factions)
  - [3.3 Correlation analysis between opinion climate of mainstream with opinion expression attitude and opinion factions](#33-correlation-analysis-between-opinion-climate-of-mainstream-with-opinion-expression-attitude-and-opinion-factions)


## 0. Research Questions 
 This project simulates the phenomenon of the "[spiral of silence](https://en.wikipedia.org/wiki/Spiral_of_silence)". By simplifying the behavioral features of the complex real society into the “agencies” as well as their interactive rules in a simulated environment, this project attempts to address the following questions:

Q1: What is the impact of individual opinion expression threshold on individual's attitude to express opinions and opinion factions?

Q2: How do opinion leaders influence individual's attitude to express opinions and opinion factions in social networks?

Q3: how does the opinion climate of mainstream media affect individual opinion expression attitude and opinion factions?

<center>

![img8](/images/imgfold/img8.png)

</center>


In our simulations, agents will make amendments to their initial opinions based on the influence of the above-mentioned variables “opinion expression threshold”, “mainstream media”, and “opinion leaders”. Before deciding whether to express opinions on social networks, individuals will make perceptual judgments about the climate of their surrounding opinions. Out of fear of being isolated, individuals will express their opinions publicly if they find that their opinions are at an advantage in the climate of public opinion after perception. On the contrary, individuals do not express their opinions and chooses to be silent if they find that their opinions are at a disadvantage in the climate of public opinion after perception.


## 1. Modeling Variable Settings and Rules

### 1.1. Initial Settings of Variables
In my NetLogo model, turtles are used to represent agencies, including netizens, hardcores, and opinion leaders. In the color setting, green agents represent the agents who express their opinions publicly, while red agents represent the silent agents. Types of agents are as follows:

#### (1) Netizens: 

The number of netizens is within the range of 100 to 1000. The specific value is controlled by the observer. The shape is human shape and the movement rule is random movement in the direction of 360° , which means that netizens can move anywhere and anytime in social networks since they are decentralized.

#### (2) Hardcores: 

Noelle-Neumann ponited out that hardcores are those who are not afraid to be isolated and choose to express opinions publicly even if they realize that their opinions are at a disadvantage. Hardcores usually consist of heretics, pioneers, and outsiders. Their personal opinions remain constant from beginning to end, their shape is human, their color are green, and their movement rule is the same as netizens.

#### (3) Opinion leaders: 

Opinion leaders refer to agents who have a relatively large influence in social networks, and their number ranges between [0-100]. The shape of opinion leaders is larger than that of netizens and hardcores. The color of opinion leaders is green. To simulate the influence of opinion leaders on netizens in social networks, I set the influence range of opinion leaders, that is, netizens on patches with a radius of 10 centered on an opinion leader.

In this project, I use “opinion distance” to characterize the difference between the opinion values of two agents, i.e., if the difference between the opinion values of a netizen and an opinion leader is too large, then netizen is more inclined not to change her/his opinion. In its influence range, if the opinion distance between opinion leaders and netizens is less than 1, the opinion value of netizens is closer to 0.1 in the direction of the opinion value of opinion leaders. If the opinion distance is greater than 1, the opinion value of netizens is not influenced by opinion leaders and the value of individual opinions remains unchanged.

### 1.2 Patches variables: mainstream media


#### (1) Opinion value 
In the real social environment, the opinion positions held by each mainstream media will have certain differences. To simulate this situation, this model sets a certain opinion value for each mainstream media. I uses three colors to represent the three opinion groups held by mainstream media (orange: indicates that its opinion value is between -1 and 0, excluding 0, blue: the opinion value is the interval from 0 to 1, excluding 0, white: the viewpoint value is 0, which means neutral).

#### (2) Scope of influence
To simulate the influence of mainstream media on agents, the scope of influence of mainstream media need to be set. Taking the media as the center, the agents within a radius of 20 patches are considered as the influence
range of mainstream media. In its scope of influence, if the opinion distance between the mainstream media and a netizen is less than 1, the opinion value of that netizen is closer to 0.1 toward the direction of the opinion value of that mainstream media, otherwise, the opinion value of that netizen remains the same.


### 1.3 Global variables

####  (1) Opinion value

 Each type of agents (including netizens, hardcores, opinion leaders) and each mainstream media has an opinion value, which ranges from [-1, 1]. Where the opinion values is divided into three factions, i.e., [-1,0) is considered as faction A, [0] is considered as faction B, and (0~1] is considered as faction C. The opinion value is taken as the last digit of the floating number.

#### (2) Neighbors
10 other agents around an agent are considered as its neighbors.

####  (3) Opinion expression threshold
 The opinion expression threshold is the minimum number of neighbors who could accept an agent’s opinion before that agent expresses it publicly. Among an agent’s neighbors who publicly express opinions, if the number of neighbors who agree with the agent is below the opinion expression threshold, that agent will choose to be silent, otherwise, the opinion of that agent will be expressed publicly.
#### (4) Opinion distance
Opinion distance refers to the difference in opinion values between agents and the difference in opinion values between agents and mainstream media.
#### (5) Opinion climate of mainstream media
In order to simulate the difference of the spiral of silence in different socio-political contexts, I add the variable "opinion climate of mainstream media", which is used to simulate the social intervention in mainstream media. The degree of pluralism in the opinion climate of mainstream media is affected by the intensity of social intervention and government intervention in mainstream media. 


## 2. Control Variables and Monitor Data


### 2.1 Control variables
Based on the research questions of this essay, the variables controlled by observer in this model are mainly as follows: the number of netizens, the number of opinion leaders, the number of mainstream media, social intervention in mainstream media,
and the opinion expression threshold of netizens. My main observation as an observer is the effect of changes in the above variables on the spiral of silence phenomenon.

### 2.2 Monitor data
(1) Comparison of the number of agents who express their opinions publicly and those who choose to be silent.
(2) Comparison of the number of A, B, and C faction opinions of agents.


## 3. Analysis of Silent Spiral Phenomena in the Model


### 3.1 Correlation analysis between opinion expression thresholds with opinion expression attitudes and opinion factions


To test the impact of netizens’ opinion expression thresholds on the spiral of silence, I set constant conditions in this module of 500 netizens, 10 opinion leaders, 20 mainstream media and no social intervention in the mainstream media. Based on these condition, I then adjust the value of the opinion expression threshold to observes the effect of expression threshold on silence by adjusting the value of the expression threshold with other conditions remaining unchanged. In this essay, I will set the threshold of opinion expression at 10%, 30%, 50%, 70%, and 90%. The results presented by the experiments are shown in Figure 3.1:



![img9](/images/imgfold/img9.png)

(Fig 3.1 Model plots under different opinion expression thresholds)




According to Figure 3.1, with increasing opinion expression thresholds, after 100 iterations, the number of red turtles (i.e., the number of netizens who choose to be silent) in this model becomes more numerous, and gradually shows a trend of turtles of the same color gathering.

![img10](/images/imgfold/img10.png)

(Figure 3.2 Graph of the number of silent versus expressed agents under different opinion expression thresholds)

From Figure 3.2, it can be seen that different opinion expression thresholds have impacts on the ratio of the number of agents who choose to be silent and who publicly express opinions. As shown in the figure, the number of agents who choose to be silent gradually increases as the opinion threshold increases. Although there is a brief period when the number of silent agents exceeds the number of publicly expressing agents at a threshold of 70% and 90%, the number of silent agents begins to gradually fall below the number of publicly expressing agents as the iterations of the subject's actions continue, and finally the number of silent agents starts to be lower than the number of openly expressing agents, and then the two stabilize. It can be seen that there seems to be a positive correlation between the opinion expression threshold and the number of silent agent in the model, and a negative correlation between the opinion expression threshold and the number of public expressing agents.


![img11](/images/imgfold/img11.png)

(Figure 3.3: Comparison of opinion factions held by agents under different opinion expression thresholds)

In summary, the “spiral of silence” did not occur as expected in experiments
under different opinion expression thresholds. However, the results of the experiments with different opinion expression thresholds shows that the opinion expression thresholds have a certain influence on agents’ expression attitudes and opinion faction. In particular, there is a positive correlation between the threshold of expression and the number of agents who choose to be silent, and a negative correlation with the number of agents who express opinions publicly. As for the effect on personal opinion factions, the final experimental results shows that as the expression threshold increased, the opinion factions become more diverse.


### 3.2 Correlation analysis between opinion leaders with opinion expression attitudes and opinion factions

To answer the second research question, “how do opinion leaders influence individual opinion expression attitudes and opinion factions in social networks? ” In my experiments, while keeping the number of netizens, the number of mainstream media, and opinion expression thresholds constant, I will control the number of opinion leaders to observe the changes in the number of opinion factions and agents’ opinion expression attitudes. I set up five experiments, respectively representing 0, 5, 10, 15, and 20 opinion leaders in the model, and the final experiments presents the results as shown in Figure 3.4.


![img12](/images/imgfold/img12.png)

(Figure 3.4: influence of the number of opinion leaders)

As can be seen in Figure 3.4, when there is no opinion leader in the model, the number of silent agents (i.e., red turtles) are about the same as the number of publicly expressing agents (i.e., green turtles) after 100 iterations of the model, and silent agents are discrete in the population. Silent agents are scattered in the crowd and have not formed a cluster. As the number of opinion leaders increases, the number of silent people in the model decreases continuously and finally reaches 0.


![img13](/images/imgfold/img13.png)

(Figure 3.5: Chart of the number of silent agents and expressing agents under the influence of the number of opinion leaders)

It can be seen that with the continuous iteration of ticks, the number of public expressing agents gradually exceeds the number of silent agents, gains the upper hand and tends to be stable. Comparing the number of silent agents under the number of different opinion leaders, we can see that the number of silent agents gradually decreases as the number of opinion leaders increases, and finally, when the number of opinion leaders reaches 20, after 100 iterations, the whole model is occupied by the public expressing agents.

In terms of the influence of opinion leaders on agents' opinion factions, as shown in Figure 4.6, there is no significant pattern of change.

![img14](/images/imgfold/img14.png)

(Figure 3.6: Changes of opinion factions under the influence of the number of opinion leaders)


We can see that opinions are relatively more diverse when the number of opinion leaders is 0 and 10. When the number of opinion leaders is 5, 15, 20, the oligarchization of opinion emerged.

In summary, there is certain correlation between the number of opinion leaders and attitude of expressing opinions. The number of opinion leaders is negatively correlated with the number of silent people in the experiments, and is significantly positively correlated with the number of public opinion leaders, that is, as the number of opinion leaders increases, the number of silent agents decreases, while the number of agents who publicly express opinions increase, it can be seen that opinion leaders have a positive effect on the expression of opinions in the entire public opinion environment. And the number of opinion leaders does not appear to have a significant effect on opinion factions.


### 3.3 Correlation analysis between opinion climate of mainstream with opinion expression attitude and opinion factions


To answer the second third question, “how does the opinion climate of mainstream media affect individual opinion expression attitude and opinion factions? ” In my experiments, while keeping the number of netizens, the number of mainstream media, he number of opinion leaders, and opinion expression thresholds constant, I will control the intensities of social inventions to observe the changes in the number of opinion factions and agents’ opinion expression attitudes. I set up three experiments, respectively under no social intervention, weak social intervention and strong social intervention, and the final experiments presents the results as shown in Figure 3.7.

![img15](/images/imgfold/img15.png)

(Figure 3.7 Changes of opinion expression attitude and opinion factions under the influence of
different intensities of mainstream media intervention)

It seems that the intensities of social intervention in the mainstream media do not have a very significant effect on agents’ opinion expression attitude in our experiments. Regardless of the intensities of intervention, the number of silent agents is much larger than the number of publicly expressing agents in the early stage of models. However, after the crossover point, the number of silent agents start to be lower than the number of public expressing agents in the models, and become stabilized over time.

In terms of opinion factions, as shown in Figure 3.7, the intensity of social interventions in the mainstream media does not seem to have a significant impact on netizens' opinion factions. The envisaged “spiral of silence” did not occur under the different levels of social intervention in the mainstream media.