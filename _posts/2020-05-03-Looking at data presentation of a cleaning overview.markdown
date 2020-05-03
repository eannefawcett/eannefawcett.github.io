---
layout: post
title:  "Looking at Data Presentation of Cleaning Overview"
date:   2020-05-03 13:46:22
categories: technical, data science, graph interpretation
paginator: Looking at Data Presentation of Cleaning Overview
---

# Cleaning Overview

I wanted to share the technical details I used to generate an article about cleaning methods for another site. The article summarizes the primary ways to address household cleaning for bacteria and viruses. The cleaning necessary is different, and spoiler alert, cleaning for viruses requires extra steps. This article will explore how I arrived at that conclusion by evaluating the content in each article reviewed. The content evaluation is mostly comprised of looking at graphs. To protect the copyrights of the original content creators, I have linked to the original articles rather than embedding the images within the article. After all, they did spend a lot of time and funding generating the data that we will be discussing today. It doesn't hurt anyone to click on a link to see what's being discussed.

# [Floor cleaning: effect on bacteria and organic materials in hospital rooms][article1]

In the first article, various types of floor cleaning methods are evaluated. You'll see in both [Figure 1 and Figure 2][article1_figures], that two types of bacteria were tested. The graphs show the percentage of the bacteria left after mopping for each test performed. These graphs show a lot of variation. The numbers are generally less in the biotrace study, and it seems like all of the types of mopping are kind of equal at this point.

The differences start to appear much more in [Figure 3][article1_figures]. In this graph, you see the same information as in the previous two graphs. The primary difference is that [Figure 3][article1_figures] shows the averages of all of the studies. The moist and we mopping look very different than the dry and spray mopping, especially in the case of the hygiena study.

Then we see in [Table 1][article1_tables] a statistical test that actually communicates whether or not there were differences between the mopping techniques. We see that for the hygiena study the wet technique is better than the dry and spray techniques based on the p-value being less than 0.05. However for the biotrace study there is no difference between the wet technique and the other techniques. The discussion then talks about some of the limitations of the study. It appears that the hygiena and biotrace studies had different scales, and this, of course, will affect the results of the statistics ran. There is no mention of scaling the data to compare results between the two studies. This table is actually what gives the other figures meaning, and is where I drew my conclusions about what to recommend to the reader.

What this communicates is that for some bacteria, moist and wet mopping can reduce the amount of some bacteria present, but not necessarily all bacteria. The reason why I suggested wet mopping over moist mopping in my review comes down to prep time. The moist preparation of the mop includes soaking the mop head in nearly boiling soapy water, wrapping it in plastic, and leaving it alone overnight in an airtight space, like a household dryer. This is not easy to do. Whereas, with the wet method, you get a mop, get some warm water, pour some soap in, mix it up with the mop, and get to mopping, a much more friendly practice, easily adopted for a household.

Additionally, this source illustrates that having a surface wet, dripping wet, is important to reducing bacterial presence. I, personally, think that creating the expectation of a wet floor that has just been mopped, and transferring that expectation to something like a countertop will create a more solid visual for the reader.



# References

[1)][article1] Andersen, B. M., Rasch, M., Kvist, J., Tollefsen, T., Lukkassen, R., Sandvik, L., & Welo, A. (2009). Floor cleaning: effect on bacteria and organic materials in hospital rooms.Journal of Hospital Infection,71(1), 57-65.
[2] Bergen, L. K., Meyer, M., Høg, M., Rubenhagen, B., & Andersen, L. P. (2009). Spread of bacteria on surfaces when cleaning with microfibre cloths.Journal of hospital infection,71(2), 132-137.
[3] Gonzalez, E. A., Nandy, P., Lucas, A. D., & Hitchins, V. M. (2015). Ability of cleaning-disinfecting wipes to remove bacteria from medical device surfaces.American journal of infection control,43(12), 1331-1335.
[4] Egert, M., Späth, K., Weik, K., Kunzelmann, H., Horn, C., Kohl, M., & Blessing, F. (2015). Bacteria on smartphone touchscreens in a German university setting and evaluation of two popular cleaning methods using commercially available cleaning products.Folia microbiologica,60(2), 159-164.
[5] Gibson, K. E., Crandall, P. G., & Ricke, S. C. (2012). Removal and transfer of viruses on food contact surfaces by cleaning cloths.Appl. Environ. Microbiol.,78(9), 3037-3044.
[6] Tuladhar, E., Hazeleger, W. C., Koopmans, M., Zwietering, M. H., Beumer, R. R., & Duizer, E. (2012). Residual viral and bacterial contamination of surfaces after cleaning and disinfection.Appl. Environ. Microbiol.,78(21), 7769-7775.
[7] Barker, J., Vipond, I. B., & Bloomfield, S. F. (2004). Effects of cleaning and disinfection in reducing the spread of Norovirus contamination via environmental surfaces.Journal of hospital infection,58(1), 42-49.

[article1]: https://www.journalofhospitalinfection.com/article/S0195-6701(08)00389-7/fulltext
[article1_figures]: https://www.journalofhospitalinfection.com/article/S0195-6701(08)00389-7/fulltext#figures
[article1_tables]: https://www.journalofhospitalinfection.com/article/S0195-6701(08)00389-7/fulltext#tables
