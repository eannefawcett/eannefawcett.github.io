---
layout: post
title:  "Proposal for the fluorescent detection of amoxicillin and recommendation for dosage required to eliminate the present infection"
date:   2020-08-06 16:27:18
categories: technical, chemistry
paginator: Proposal for the fluorescent detection of amoxicillin
---

Diagnostic testing for disease can take anywhere from three hours to three weeks to complete. If it were possible to observe bacterial interactions with antibiotics in real time, diagnosis could be sped up and an appropriate antibiotic could be prescribed. Currently, Pattern Bioscience is working on such a technology using single cell analysis and deep machine learning. [1][link1] This post will offer up a potential route to evaluate for amoxicillin efficacy. I will be working under the assumption that the deep machine learning technique being used is a convolutional neural network. This type of machine learning is what allows computers to evaluate visual information like photos. If this technique is being used, then the computer will be able to "see" what's going on at a cellular level. Amoxicillin inhibits a bacteria's ability to build a cell wall, meaning that over time, amoxicillin will prevent more cell wall from being formed, holes will develop, and the bacterial cell will rupture. [2][link2] This idea of visualizing bacteria *in vivo* has already been done before with fluorescently labelled vancomycin. [3][link3] In the past, amoxicillin has been prepped for fluorescent analysis in solid phase extraction [4][link4] [5][link5], in organic matrices [6][link6] [7][link7], and in bacterial cells themselves [8][link8]. Other types of antibacterial probes have also been evaluated in bacterial cells. [9][link9]

This proposal aims to translate similar principles to the commonly used antibiotic amoxicillin for the purposes of extending from diagnosis using amoxicillin alone to also allowing for quantification of consumed amoxicillin. This could lead to not only a diagnosis and prescription recommendation, but also to a dosage or duration recommendation. For this to work, a fluorescently enabled microscope would be needed to take measurements. The images collected by this microscope would then need to be fed into a convolutional neural network. At first, to build a knowledge base, manually labeling images with bacteria present, not present, and fluorescent tag concentration might be necessary. This labeled data could be used to develop a supervised network for classification of affected/unaffected samples and a regression for fluorescent tag concentration. Once this model is developed, patient samples could be tested against it, with traditional testing serving as a secondary form of validation. Once an acceptable error is reached during the training stages of the model, and it is appropriately validated, the time needed to evaluate a new sample would be similar to the amount of time it would take to collect the necessary input information. Meaning this approach would take the same amount of time as it takes for the bacteria to express the affects of the introduction of the amoxicillin. This rate could be calculated for using a similar approach developed by Dr. Spratt in *Properties of the penicillin-binding proteins of Escherichia coli K12*. [10][link10]

This is but one example of the possibilities of integrating machine learning techniques into the traditional laboratory setting.



References:

[1][link1] https://pattern.bio/pattern-secures-13m-in-development-funding/

[2][link2] Reed, M. D. (1996). Clinical pharmacokinetics of amoxicillin and clavulanate. The Pediatric Infectious Disease Journal, 15(10), 949-954. https://doi.org/10.1097/00006454-199610000-00033

[3][link3] van Oosten, M., Schäfer, T., Gazendam, J. A., Ohlsen, K., Tsompanidou, E., de Goffau, M. C., Harmsen, H. J., Crane, L. M., Lim, E., Francis, K. P., Cheung, L., Olive, M., Ntziachristos, V., van Dijl, J. M., & van Dam, G. M. (2013). Real-time in vivo imaging of invasive- and biomaterial-associated bacterial infections using fluorescently labelled vancomycin. Nature communications, 4, 2584. https://doi.org/10.1038/ncomms3584

[4][link4] Brittain, H. G. (2005). Solid-state fluorescence of the trihydrate phases of ampicillin and amoxicillin. AAPS PharmSciTech, 6(3), E444-E448. https://doi.org/10.1208/pt060355

[5][link5] Luo, W., & Ang, C. Y. (2000). Determination of amoxicillin residues in animal tissues by solid-phase extraction and liquid chromatography with fluorescence detection. Journal of AOAC International, 83(1), 20-25. https://doi.org/10.1093/jaoac/83.1.20

[6][link6] Xie, K., Jia, L., Xu, D., Guo, H., Xie, X., Huang, Y., ... & Wang, J. (2012). Simultaneous determination of amoxicillin and ampicillin in eggs by reversed-phase high-performance liquid chromatography with fluorescence detection using pre-column derivatization. Journal of chromatographic science, 50(7), 620-624. https://doi.org/10.1093/chromsci/bms052

[7][link7] Crissman, H. A., Stevenson, A. P., Orlicky, D. J., & Kissane, R. J. (1978). Detailed studies on the application of three fluorescent antibiotics for DNA staining in flow cytometry. Stain Technology, 53(6), 321-330. https://doi.org/10.3109/10520297809111954

[8][link8] Kocaoglu, O., & Carlson, E. E. (2013). Penicillin-binding protein imaging probes. Current protocols in chemical biology, 5(4), 239–250. https://doi.org/10.1002/9780470559277.ch130102

[9][link9] Kocaoglu, Ozden & Carlson, Erin. (2016). Progress and prospects for small-molecule probes of bacterial imaging. Nature Chemical Biology. 12. 472-478. https://dx.doi.org/10.1038%2Fnchembio.2109

[10][link10] Spratt, B. G. (1977). Properties of the penicillin‐binding proteins of Escherichia coli K12. European Journal of Biochemistry, 72(2), 341-352. https://doi.org/10.1111/j.1432-1033.1977.tb11258.x

[link1]: https://pattern.bio/pattern-secures-13m-in-development-funding/
[link2]: https://doi.org/10.1097/00006454-199610000-00033
[link3]: https://doi.org/10.1038/ncomms3584
[link4]: https://doi.org/10.1208/pt060355
[link5]: https://doi.org/10.1093/jaoac/83.1.20
[link6]: https://doi.org/10.1093/chromsci/bms052
[link7]: https://doi.org/10.3109/10520297809111954
[link8]: https://doi.org/10.1002/9780470559277.ch130102
[link9]: https://dx.doi.org/10.1038%2Fnchembio.2109
[link10]: https://doi.org/10.1111/j.1432-1033.1977.tb11258.x
