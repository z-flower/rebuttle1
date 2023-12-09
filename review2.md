__Q1:__ Introduction Section is well written. The problem definition is clear, and limitations of existing approaches to ASQP and datasets is supported with a simple and understandable example. I think it would make it more clear if the author(s) could have done the same for the template problem. Maybe also giving an example and explaining by that example why BvSP like approach is needed. If they mention this later in the paper, they should refer the reader to that Section.

__A1:__ 
Thanks for your input. We apologize for the lack of a clear definition of the template problem in the Introduction section. Additionally, **in the case study, we conducted an in-depth analysis of BVSP**. In the camera remedy, we'll refer the reader to that section.

Now, I'll **explain why methods similar to BVSP are needed**.
To extract aspect sentiment quadruplets (aspect category (AC), aspect term (AT), opinion term (OT), sentiment polarity (SP)), some approaches transform quadruplet extraction into a paraphrase generation problem. They map the four elements (AC, AT, OT, SP) into semantic values (XAC, XAT, XOT, XSP) using pre-defined rules, which are then fed into a template to generate a natural language target sequence.

However, ASQP is not a typical generation task. The order of the quadruplet's elements doesn't need to be fixed as long as it's accurately extracted. Aspect sentiment quadruplets are order-free, implying that various orders, such as {XAC → XSP → XAT → XOT} and {XAT → XAC → XOT → XSP}, or statements like "{XAC is XSP because XAT is XOT}" are all correct.
Hence, when large language models reply to the same sentence using different templates, the results differ. Due to the relevance of the problem, the information contained in these results greatly assists in the final prediction.

Given an example: "it's a beautiful building."

The target tuple is: (building, beautiful, building, great).

With different templates, we get different results:
T1: "building is great because building is beautiful"
T2: "[AC] **room_overall** [OT] beautiful [AC] building [SP] great"
T3: (building, beautiful, building, great)

Hence, we obtain:
(building, beautiful, room_overall, great) × 1

(building, beautiful, building, great) × 2 **(selected)**

We notice an error in one of the three templates (marked in bold), and **after applying our voting mechanism(marked in bold), the final prediction is corrected**. This demonstrates that considering the similarities between templates can aggregate accurately predicted quadruplets from multiple templates while filtering out error predictions.

Therefore, **enhancing results by utilizing the correlation among these various templates is beneficial**. Our method not only considers this correlation but also adopts a broader perspective on these templates, resulting in more accurate predictions.

 

__Q2:__Can you discuss whether there are limitations of the annotation of the dataset。 In Section 2, where the annotation of the dataset is explained, I think its limitation also should be discussed. Yes, more aspect categories are added. However, a proxy that gives an idea how expensive time wise the annotation procedure would be good to see to estimate the annotation. Manually annotating and checking categories and its similarity seems time consuming. I also think that, being a MSc student who is well-versed in aspect based sentiment analysis itself does not make someone an expert annotator. Depending on the data to be annotated, even if annotator know everything about aspect based sentiment analysis, they may as well not be familiar with aspects or aspect categories for some domains. That is why, authors should mention this as a potential limitation of the annotation.

__A2:__
Thanks for your comments and suggestions. 

During the dataset annotation process, **we prioritized the credibility and rigor of the dataset. Undoubtedly, this process was time-consuming**. Over the six-month annotation period, although annotators were allowed to communicate with each other, their annotation processes remained relatively independent. After the annotations were completed, if any annotator raised objections to any quadruple content, discussions were held to reach a consensus. Meanwhile, the leader of the master students assisted in making the final decision. Following this, there was a two-month period dedicated to checking the accuracy of the annotations. **Throughout the checking period, we rigorously enforced consistency. We followed the methodology of previous annotation work[^1], and the strict quads matching F1 score between two annotators was 78.63%, indicating substantial agreement between them. **These measures significantly ensured the quality of our dataset, making it reliable.

Though **we invested considerable effort in ensuring the reliability of the dataset, this process was worthwhile**. We look forward to the emergence of more convenient and effective tools in the future to assist in annotating datasets.

__Q3:__I could understand what exactly means to map the quads to semantic values after looking at the cited paper "Improving Aspect Sentiment Quad Prediction via Template-Order Data Augmentation ". A reader that is not fully familiar with the topic should be able to understand the details from the paper. That is why I think it will make the section more readable if they explain more clearly. For instance, at the beginning of Section 3.2 though there are several available templates, how many, is it because of the permutation of the four elements in the quad? If so, specify that. Later in the text, I can see that this information is given in Appendix. In the text, please refer to that Section.
__A3:__ 
Thanks for your feedback. We apologize for any confusion caused by the lack of clarity in our paper's content, particularly regarding the ASQP task, which might hinder readers unfamiliar with it. **In the camera remedy, we'll make revisions to the introduction and other sections to provide a more detailed explanation of our method's problem definition and its content.**

Regarding the reference to "several available templates" mentioned at the beginning of Section 3.2, we'll include a more detailed description in the camera remedy and refer readers to the content in the appendix to help them understand the intricacies of our method.

Moreover, we'll make modifications in Section 3.1, specifically at line 285 in the "Formulation and Overview" subsection. The revised statement will read: "As illustrated in Figure 3, we initially employ the pre-trained language model with JS divergence to select appropriate subsets from the available templates (for template details, refer to Appendix B)."


__Q4:__ In Section 3.1., by referring Figure 3, authors explain using JS divergence to selecting subsets of templates, due to efficiency and effectiveness of optimization. Please either briefly explain why it is efficiency and effectiveness or cite a study that explains so. Besides, generating multiple quads from diverse views is not clear to me. Diverse view based on which criteria? For instance, by covering more aspect categories?

__A4:__ 
Thanks for your comments and inquiries. 
Firstly, **regarding the selection of templates based on efficiency and effectiveness, our consideration stems from the understanding that the more templates utilized, the longer the voting and reasoning processes become**. Additionally, an excess of templates generates redundant information, imposing unnecessary burdens on the reasoning process. **JS divergence allows the selection of a more representative and diverse subset of templates**. Thus, considering both efficiency and effectiveness, we adopted JS divergence to select subsets of templates. By focusing on diverse templates, this method allows for a varied representation within the subset, potentially capturing a broader spectrum of patterns and information. Considering dissimilarities between templates promotes the selection of a diverse set that encompasses various aspects of the data. This diversity aids in the model's generalization, enhancing its ability to adapt to new or unseen examples during the few-shot learning process.
**The concept of "generating multiple quads from diverse views" represents our notion of a "Broad view." Let me clarify further what this "Broad view" entails within the context of the paper.** "Broad view" refers to an approach that goes beyond relying on a single template to train a language model. **Diverse view-based learning employs multiple templates with different styles and orders to guide the learning process, rather than solely covering more aspect categories.** By integrating diverse templates, the language model encounters a wider range of linguistic patterns and variations. This enables the model to comprehend the quadruple extraction task more comprehensively and strengthens its ability to generalize to new examples. Therefore, through the "Broad view," the model captures the essence of the quadruple extraction task from different angles and perspectives, resulting in an improvement in its capabilities.

__Q5:__Why in the experiments only the new dataset is used? Yes, in the paper, the advantages of creating new data are explained clearly. However, one would be interested to see proposed approaches' performance on other datasets as well.
For Section 4.1, maybe briefly mention why you are not using existing datasets, maybe by referring to Section 5.1. As a reader, I would be interested to see your methods performance on other datasets as well. One can claim that the advantage of the new dataset is, it is a rich aspect category dataset, which is true. However, for justifying that the developed method can be used and performs good on other datasets, some experimental results would be good to see in the paper.

__A5__ 
Firstly, thank you very much for your affirmation of the dataset we proposed. In the paper, we indeed only presented experimental results on the new dataset. **The reason for not conducting experiments on other datasets is because we considered the new dataset to have significant advantages over previously proposed datasets, offering richer and more diverse information.** Thus, demonstrating the effectiveness of our method solely on the new dataset was sufficient to prove its efficacy.

**However, understanding readers' desire to see our method's performance across multiple datasets, we plan to conduct experiments on other datasets.** This will provide a more robust illustration of the advantages of our method. We intend to include these experimental results in the camera remedy along with explanations.

__Q6:__ Are the improvements over second best performing approaches statistically significant?

__A6:__ 
Comparison with other methods: The experimental results in Table 2 demonstrate that **BvSP achieves the best performance across the four few-shot settings**. Particularly noteworthy is the significant improvement over the baseline GAS, with BvSP showing an absolute F1 score increase of +3.53% in the one-shot settings. Additionally, under the same few-shot settings and with the same number of selected templates, BvSP outperforms DLO and ILO. 

Furthermore, **when compared to the second-best performing approaches, BvSP shows improvements in precision, recall, and F1 scores by +1.49%, +1.35%, and +0.53% respectively. **This further underscores the effectiveness of BvSP in providing a broader view of templates.

Finally, in the camera remedy, **we will report the standard deviation of experimental results to demonstrate significant differences between methods.**

[^1]:Kim E, Klinger R. Who feels what and why? annotation of a literature corpus with semantic roles of emotions[C]//Proceedings of the 27th International Conference on Computational Linguistics. 2018: 1345-1359.https://aclanthology.org/C18-1114
