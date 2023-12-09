__Q1:__ The main shortcoming of this paper is that the experiment on only one data set compared with four baseline models is somewhat weak. Of course, probably due to the requirements of the task itself and BvSP method, there are few datasets that can meet the requirements and baseline models suitable for this task.

__A1:__ 
Thanks for pointing out the shortcomings in our work. Indeed, in the paper, we only presented experimental results on the new dataset. **The reason for not conducting experiments on other datasets is that we considered the new dataset to have significant advantages over previously proposed datasets, offering richer and more diverse information.** Therefore, demonstrating the effectiveness of our method solely on the new dataset was deemed sufficient to validate its efficacy.
However, **recognizing readers' interest in seeing our method's performance across different datasets, we plan to conduct experiments on additional datasets.** This will provide a stronger validation of our method's effectiveness, and the experimental results will be detailed in the camera remedy of the paper.


__Q2:__ Is the more aspect categories and the finer granularity the better? For example, can the internet in Figure 1 be classified into service general? In addition, to solve this problem, in addition to the construction of FSQP dataset, what processing method is adopted in ASQP extraction?

__A2:__ 
Thanks for your query. 

Having more categories and finer granularity is indeed beneficial in a few-shot scenario. **In a few-shot task, the concept of "k-shot" refers to the number of labeled instances available for each class**. For instance, in a 1-shot setting, only one labeled instance exists per class.The challenge of few-shot task lies in adapting quickly to unseen aspects with minimal labeled samples. **This necessitates that aspect categories in the dataset be more diverse, reflecting real-world applications more closely.** Generic categorizations do not represent specific aspect categories and fail to enable the model to learn specific knowledge. Hence, having more aspect categories and finer granularity is preferable. Furthermore, previous ASQP datasets often have a limited number of categories, insufficient to meet the requirements of the few-shot scenario and adapt to current information needs. For these reasons, we annotated the few-shot ASQP dataset - FSQP.
From a few-shot perspective, categorizing "Internet" might vary based on the analysis context or task requirements. **While "service general" and "Internet" may intersect, they are not necessarily inclusive of each other.** Simply classifying the "Internet" under "service general" contradicts the requirements of the few-shot task. **For the ASQP task, more specific and realistic aspect categories enable the model to acquire a broader range of knowledge.**
In the realm of few-shot ASQP tasks, recent work [^1] has employed a method of shuffling data with a fixed random seed and selecting the first few samples to ensure there are at least k samples from each aspect category. In cases where datasets lack aspect category annotations, some work [^2] only select k examples per sentiment class. Consequently, **there isn't an effective method yet to address the deficiency in aspect categories for few-shot ASQP.** This observation highlights the current lack of a proper benchmark dataset in the few-shot ASQP domain.

In light of this observation, we propose annotating a few-shot ASQP dataset - FSQP. This dataset aims to provide a more balanced representation and encompass a wider range of categories. FSQP intends to serve as a comprehensive benchmark for evaluating few-shot ASQP, addressing the current limitations in aspect categories and offering a more robust evaluation framework.


__Q3:__ Implicit sentiment analysis is a hot research issue. But for ASQP task, what do the implicit aspect terms and implicit opinion terms refer to? Please give an example.

__A3:__
I apologize for not providing detailed explanations in the paper regarding implicit aspect terms and implicit opinion terms. 
**I'll elaborate on what implicit aspect terms and implicit opinion terms refer to.** Implicit aspect terms and implicit opinion terms refer to aspects or opinions that aren't explicitly mentioned in the text but are implied or inferred from the context. 

For instance, consider the review sentence: "Looks nice and the surface is smooth, but certain apps take seconds to respond." 

Here, "surface" is an explicit aspect term categorized under "Design" and "smooth" is the explicit opinion term towards this aspect, indicating a positive sentiment. This forms an explicit quadruple: surface-Design-smooth-Positive.

However, there are other quadruples that need extraction: "Null-Design-nice-Positive," which contains an implicit aspect term, and "apps-Software-Null-Negative," containing an implicit opinion term.

**Research[^3] indicates that product reviews often contain a significant number of implicit aspects and opinions.** In the Laptop domain, nearly 44% of review sentences contain implicit aspects or opinions, with over 8% containing both implicit aspects and opinions. Similar percentages are observed in the Restaurant domain. Constructing quadruples containing implicit aspects and opinions poses a challenge. Therefore, annotating implicit information is highly meaningful for dataset construction. FSQP encompasses implicit aspect terms and implicit opinion terms, showcasing one of the outstanding contributions of our work.


__Q4:__ Figure 3 is the overall framework of this paper's BvSP, then why isn't the final output an aspect sentiment quad (no sentiment polarity is visible)?

__A4:__  
Figure 3 illustrates the overall framework of our method. I regret that it didn't sufficiently convey the details of our approach. 

In ASQP task, the order of the quadruplet's elements doesn't need to be fixed as long as it's accurately extracted. Therefore, aspect sentiment quadruplets are order-free, implying that various orders, such as {XAC → XSP → XAT → XOT} and {XAT → XAC → XOT → XSP}, or statements like "{XAC is XSP because XAT is XOT}" are all correct. Hence, when large language models reply to the same sentence using different templates, the results differ. **BvSP aggregates the quad results generated by all selected templates. The final output of our method is an aspect sentiment quad, **denoted as ([AC] [SP] [AT] [OT]), where [AC] represents the aspect category, [SP] signifies the sentiment polarity, [AT] stands for the aspect term, and [OT] refers to the opinion term. The sentiment polarity ([SP]) is a crucial element within this quadruple.



__Q5:__ On what basis was the baseline model chosen for experimental comparison? How are they representative? Why is there no aspect sentiment analysis model based on prompt learning?

__A5:__ 

**Let me provide a more detailed explanation of why we chose the four baselines mentioned in the paper**:

1.GAS[^4]: This work redefines ABSA tasks as generation problems, unifying sub-tasks within a generation framework. They propose annotation-style and extraction-style paradigms to formulate target sentences, solving multiple sentiment pair or triplet extraction tasks using a unified generation model. Our modification directly treats sentiment quads sequences as the target for the generation model.

2.Paraphrase[^5]: This work addresses ASQP as a paraphrase generation problem, predicting sentiment quads in a single shot and leveraging semantic information from natural language labels. Experiments on datasets (Rest15 and Rest16) demonstrate its superiority over previous state-of-the-art models, including GAS.

3.DLO and ILO[^6] : These methodologies aim to identify appropriate orders and combine multiple templates for data augmentation to enhance the ASQP task. The work achieve state-of-the-art performance compared to GAS and Paraphrase.

These works have made significant progress in the ASQP task, showcasing strong superiority. Hence, we selected these models as our baselines.

**Additionally, while we used Soft-Prompting for template selection, our focus was on template enhancement and its application in the few-shot learning domain by considering relationships between templates. This learning process is prompt learning. **Therefore, our method can be easily adapted to prompt learning, and in future research, we intend to explore and evaluate some aspect sentiment analysis models based on prompt learning as baselines to assess the strengths and weaknesses of our approach. Some recent models, like LEGO-ABSA[^7], utilize prompt-based generative frameworks for ABSA tasks using T5 as the backbone. These models will be considered as baselines in our future research to evaluate our method.


__Q6:__ Intuitively, explicit analysis should be easier and produce better results than implicit analysis. But in Table 5, almost all of the models do well in implicit analysis. In addition to the data distribution mentioned in the paper, is it related to the model and the process?

__A6:__ 
Thank you for your query. **In our analysis of the Implicit Information Prediction in section 4.4.4, we noticed the similar upward trend in the F1 score for the implicit subset as observed in the explicit subset.** Furthermore, our investigation revealed similar findings in some research studies[^8], indicating that BERT models perform better on IA & IO compared to EA & EO. This indeed is an intriguing phenomenon.

One reason behind this variation in model performance could be the uneven distribution of explicit and implicit information across quad categories in the FSQP dataset. **Another factor could be the model's reliance on ample data to enhance its performance.** Present-day large models are trained on massive datasets, and during pre-training, they acquire more inclinations towards implicit knowledge, empowering the model with robust reasoning capabilities. Explicit information, on the other hand, relies on existing knowledge for predictions, which is significantly smaller in comparison to the knowledge the model acquired during training. Hence, the model might perform better in handling implicit information compared to explicit information.

Additionally, **large models might encounter semantic illusions, resulting in errors in assessing semantic similarity within explicit information.** These inaccuracies, classified as incorrect, could impact explicit analysis. In contrast, implicit information mapped to NULL does not exhibit semantic similarity errors. Therefore, both the nature of the model and its processing mechanisms might contribute to why implicit analysis produces better results than explicit analysis.


__Q7:__ At present, large language models (LLMs) have been applied in many fields, including sentiment analysis. Has this paper tried to implement ASQP task using a LLM? I think that should be discussed in Limitation Section.

__A7:__ 
For implementing the ASQP task using a Language Model, we intend to discuss this in the Limitation Section of the camera remedy.

[^1]:Vacareanu R, Varia S, Halder K, et al. A Weak Supervision Approach for Few-Shot Aspect Based Sentiment[J]. arXiv preprint arXiv:2305.11979, 2023.https://arxiv.org/pdf/2305.11979.pdf
[^2]:Varia S, Wang S, Halder K, et al. Instruction tuning for few-shot aspect-based sentiment analysis[J]. arXiv preprint arXiv:2210.06629, 2022.https://arxiv.org/pdf/2210.06629.pdf
[^3]:Cai H, Xia R, Yu J. Aspect-category-opinion-sentiment quadruple extraction with implicit aspects and opinions[C]//Proceedings of the 59th Annual Meeting of the Association for Computational Linguistics and the 11th International Joint Conference on Natural Language Processing (Volume 1: Long Papers). 2021: 340-350.https://aclanthology.org/2021.acl-long.29.pdf
[^4]:Zhang W, Li X, Deng Y, et al. Towards generative aspect-based sentiment analysis[C]//Proceedings of the 59th Annual Meeting of the Association for Computational Linguistics and the 11th International Joint Conference on Natural Language Processing (Volume 2: Short Papers). 2021: 504-510.https://aclanthology.org/2021.acl-short.64
[^5]:Zhang W, Deng Y, Li X, et al. Aspect sentiment quad prediction as paraphrase generation[J]. arXiv preprint arXiv:2110.00796, 2021.https://aclanthology.org/2021.emnlp-main.726
[^6]:Hu M, Wu Y, Gao H, et al. Improving aspect sentiment quad prediction via template-order data augmentation[J]. arXiv preprint arXiv:2210.10291, 2022.https://arxiv.org/abs/2210.10291
[^7]:Gao T, Fang J, Liu H, et al. LEGO-ABSA: A prompt-based task assemblable unified generative framework for multi-task aspect-based sentiment analysis[C]//Proceedings of the 29th international conference on computational linguistics. 2022: 7002-7012. https://aclanthology.org/2022.coling-1.610.pdf
[^8]:Cai H, Xia R, Yu J. Aspect-category-opinion-sentiment quadruple extraction with implicit aspects and opinions[C]//Proceedings of the 59th Annual Meeting of the Association for Computational Linguistics and the 11th International Joint Conference on Natural Language Processing (Volume 1: Long Papers). 2021: 340-350.https://aclanthology.org/2021.acl-long.29.pdf
