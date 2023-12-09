Review #1

__Q1:__ The annotation process is not rigorous as the annotators are allowed to communicate with each other, and this may inflate the agreement. Also, the agreement metric should follow previous works on ABSA (https://aclanthology.org/L18-1104/)

__A1:__ 
Thanks for your comments and suggestions. 
In the annotation process of the dataset, **we prioritized credibility and rigor**. Throughout the six-month annotation period, while annotators were allowed to communicate with each other, their annotation operations remained relatively independent. After the annotations were completed, if any of the annotators raised objections to any quadruple content, discussions were held to reach a consensus. Meanwhile, the leader of the master students will help to make the final decision. Following this, there was a two-month period dedicated to checking the accuracy of the annotations, during which we rigorously enforced consistency. 

**For the agreement metric，we followed the methodology of previous annotation work[^1]**, and the strict quads matching F1 score between two annotators was 78.63%(in section 2.2.2 Annotation Process, line 217), indicating substantial agreement between them. These measures greatly ensured the quality of our dataset, making it reliable.


__Q2:__ The authors should also consider or at least discuss large language models which have been shown to outperform supervised methods in some few-shot tasks.

__A2:__ 
Thanks for your suggestions. We will include discussions on how large language models outperform supervised methods in some few-shot tasks.

**Large Language Models have demonstrated impressive few-shot performance**, as evidenced in research such as [^2]. Specifically, these models have shown superiority over supervised methods in certain few-shot tasks. For instance, in text classification datasets, models like PATRON [^3] **achieve 91.0% and 92.1% of fully supervised performance with only 128 labels, using conventional fine-tuning and prompt-based learning, respectively**. Moreover, more informative representations of textual inputs often result in significantly higher performance in downstream Natural Language Processing (NLP) applications. This phenomenon explains the widespread adoption and success of models such as (Ro)BERT(a), GPT-3, and T5 [^4].

Additionally, given that aspect categories in practical scenarios are not fixed and can change, fast adaptation to unseen aspects using only labeled samples becomes crucial. Therefore, our work focuses on exploring the few-shot setting, where adaptation to new aspects with limited labeled data is central to our research.


__Q3:__ The results may not be solid as few-shot experiments need to be repeated and averaged across multiple random seeds. The authors should also report the standard deviation of methods to show a significant difference between methods.

__A3:__ 
Thanks for your input. To ensure a fair comparison, we've adhered to the settings of previous experiments. However, we recognize that solely reporting the average of results from 5 fixed seeds might not sufficiently showcase the superiority of our method. 

In the camera remedy, we intend to make adjustments by including the standard deviation of our method's performance, thereby illustrating significant differences between methods more effectively.

__Q4:__ What is the additional cost (time or memory) of predicting and aggregating with multiple templates?

__A4:__ 
Thanks for your question. Indeed, there is an additional time consumption during the phase of predicting and aggregating with multiple templates. We apologize for not mentioning this in the paper. We will make modifications in the camera remedy to report the additional cost (whether in time or memory) incurred during predicting and aggregating with multiple templates.

[^1]:Kim E, Klinger R. Who feels what and why? annotation of a literature corpus with semantic roles of emotions[C]//Proceedings of the 27th International Conference on Computational Linguistics. 2018: 1345-1359.
[^2]:Brown T, Mann B, Ryder N, et al. Language models are few-shot learners[J]. Advances in neural information processing systems, 2020, 33: 1877-1901.
[^3]:Yu Y, Zhang R, Xu R, et al. Cold-start data selection for few-shot language model fine-tuning: A prompt-based uncertainty propagation approach[J]. arXiv preprint arXiv:2209.06995, 2022.
[^4]:Chu T, Song Z, Yang C. Fine-tune language models to approximate unbiased in-context learning[J]. arXiv preprint arXiv:2310.03331, 2023.
