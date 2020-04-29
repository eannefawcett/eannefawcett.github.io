---
layout: post
title:  "Where Data Science and Traditional Science Collide"
date:   2019-09-09 13:51:11
categories: non-technical, data science, science
paginator: Where Data Science and Traditional Science Collide
---

The word science illicits images of plants and microbiomes, the color changes from chemical reactions and Bohr's atomic models, and systems interacting kinetically and on the quantum level. Data science, however, drives these dancing figures to a halt as numbers take over. Data science is the creation of a model from interpreted data for the purposes of making informed decisions based on feature analysis. From a research standpoint, this data science perspective addresses the primary goal of all research: how can I display what I have discovered in order to communicate my results to various audiences effectively? With this connection in place, there must be additional similarities between what I know as a scientist and what haver learned as a data scientist. To discover where these points of overlap are, I will evaluate the methodology commonly used by which each discipline.

The scientific method is largely agreed on by the scientific community as the following:

<img src="/images/The_Scientific_Method_as_an_Ongoing_Process.svg" alt="Scientific Method" width="400px" />
Figure 1. The Scientific Method as an Ongoing Process

Typically, the process starts with an internal **Observation** of the world followed by a **Question** pertaining to the observation, generally sparked by curiosity. Then a **Hypothesis** to test is derived from the question and observation, typically about a relationship between observed objects. Next, the studier will make a **Prediction** about what will happen when testing occurs. Subsequently this a test **Design** is developed the **Test** is performed with the collection of data. Then an **Analysis** of the data is done and a working **Theory** is developed. This results in starting the process over again or generating new observations based on the working theory.

A common data science process is shown below in Figure 2.:

<img src="/images/osemn_method.png" alt="OSEMN Data Science Method" width="400px" />
Figure 2. The OSEMN Data Science Method

Many data science methods begin in a similar place, with a background exploration.Or more commonly, with a question about the validity of a potential pattern in a business case. After the business context is developed, data gathering, also known as **Obtain** begins. This can occur in many different fashions: data gathered from a database generated internally from within a company, data gathered from an external database, data gathered from websites that provide access to data, to web scraping. After this occurs, the data scientist will do what is known as **Scrub**. In this step of the process all of the data that was gathered is transformed into a usable form for modeling. This will often start with making sure that continuous data is labeled appropriately as integer or float data, and that categorical data is handled appropriately either by binning or one hot encoding.After usable data is generated, a data **Explore** is conducted. At this point,the data scientist will run some statistics to understand the composition of the dataset, introduce useful features that expand upon the original data passed in, and develop some visuals to assist with import relationships in the data. To prepare for the next step **Model**, a test-train, and sometimes validation split is performed to maintain the integrity of the data passed into the model, and the model itself. The statistics and data exploration performed earlier will inform the data scientist what types of modeling will be appropriate for the question developed in the Obtain stages. After modeling, the data scientist must **iNterpret** what is happening in the model. In this stage conclusions are reached, and based on these conclusions a solution is developed and deployed.

The methodologies for both science and data science, respectively are below:
1. Observe - Obtain
2. Question - Scrub
3. Hypothesize - Explore
4. Predict - Model
5. Design - Interpret
6. Test
7. Analyze
8. Theorize

At first glance, *I see* the science method seems to be longer than the data science method. Also in the science method, there is a lot of thinking happening in the following steps: observation, question, hypothesis, prediction, design, theory. In the data science method, the only outwardly obvious thinking type step is interpret. Most of the other steps seem to be quite active with a physical output. In this science method, all of the steps have a physical output, but explain in words a thought process, except for test which outputs data, and analyze which outputs an equation. Each step in the data science method has varying outputs: from data, to a data frame, to graphs and visuals, to an equation, to an interactive tool.

Although these two processes sound very different, it has been my experience that they are framed similarly. The focus within the frame, however, is in two different places. The scientific method focuses more energy prior to scientific testing. Whereas, the OSEMN method focuses more on what happens after scientific testing. *I think* that despite these differences, these two fields of study merge together very well. The science observations give meaning and context to the data that is later to be studied. The interpretation and deployment steps in the data science method give meaning to the results produced my that aforementioned observation. Not only do the results have meaning, but there is an emphasis on making the results accessible especially to those that don't understand how the model was generated.

*I wonder* if, moving forward, knowing data science will give a scientist a better format to communicate results to superiors and editors; and if knowing science will give a data scientist the tools to ask better questions during the obtain stages in order to generate more meaningful features that lead to better models. I wonder if these two fields, which are considered separate today, will merge. I wonder if these two fields will celebrate over the shared knowledge of test/model design and statistics.

To conclude, while these processes come from different desires and currently deliver to different audiences, I think they are different enough to learn from each other, and similar enough to find common ground.

Sources:
- Garland, Jr., Theodore. “The Scientific Method as an Ongoing Process”. U C Riverside.   Archived from the original on 19 Aug 2016.
- Shearer, C. (2000) The CRISP-DM Model: The New Blueprint for Data Mining. Journal of Data Warehousing, 5, 13-22.
- https://miro.medium.com/max/1935/1*eE8DP4biqtaIK3aIy1S2zA.png
