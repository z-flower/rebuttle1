__Q1:__ 1:The model presents limited novelty (the improvement likely comes from the use of more contemporary LLMs rather than the method itself), but the experimentation is interesting as a benchmark validating this dataset. Overall, I feel that the dataset is the main contribution of this work, which would be useful for future research.  
2:I would suggest the authors to enlist the help of a proficient English speaker to improve readability of the paper. It's overall understandable, but would benefit from being polished.

__A1:__ 
Your insights into our work are greatly appreciated! 

1. **The improvement comes from the method itself.** We need to clarified that BvSP uses the same pre-trained language model (i.e. T5) as all baseline methods. To show a significant difference between methods, we compute the standard deviations on F1 scores, all the reported results are the average of 5 seeds.
<table>
    <tr>
        <th rowspan = "1">Methods</th>
        <th colspan = "1">One-shot</th>
        <th colspan = "1">Two-shot</th>
        <th colspan = "1">Five-shot</th>
        <th colspan = "1">Ten-shot</th>
    </tr>
    <tr>
        <th>GAS</th>
        <td>26.54±2.03</td>
        <td>40.81±1.38</td>
        <td>50.50±0.88</td>
        <td>52.34±0.76</td>
    </tr>
    <tr>
        <th>Paraphrase</th>
        <td>23.38±1.06</td>
        <td>38.98±1.23</td>
        <td>49.29±1.54</td>
        <td>52.26±1.09</td>
    </tr>
    <tr>
        <th>DLO</th>
        <td>26.23±1.84</td>
        <td>37.72±1.10</td>
        <td>50.38±0.94</td>
        <td>51.62±0.62</td>
    </tr>
    <tr>
        <th>ILO</th>
        <td>24.98±1.79</td>
        <td>38.12±1.12</td>
        <td>50.95±0.96</td>
        <td>51.94±1.04</td>
    </tr>
    <tr>
        <th>BvSP</th>
        <td><strong>30.07±2.24</strong></td>
        <td><strong>41.26±1.67</strong></td>
        <td><strong>51.13±0.63</strong></td>
        <td><strong>52.42±1.48</strong></td>
    </tr>
</table>
   Otherwise，compared with contemporary LLM (i.e. ChatGPT), our work still performs significantly improvement.
   <table>
    <tr>
        <th rowspan = "1">Methods</th>
        <th colspan = "1">One-shot</th>
        <th colspan = "1">Two-shot</th>
        <th colspan = "1">Five-shot</th>
        <th colspan = "1">Ten-shot</th>
    </tr>
    <tr>
        <th>ChatGPT</th>
        <td>23.56</td>
        <td>35.52</td>
        <td>38.97</td>
        <td>42.96</td>
    </tr>
    <tr>
        <th>BvSP</th>
        <td><strong>30.07</strong></td>
        <td><strong>41.26</strong></td>
        <td><strong>51.13</strong></td>
        <td><strong>52.42</strong></td>
    </tr> </table>

2. **The dataset is the main contribution.** We are thrilled by your positive evaluation of the dataset! Creating the FSQP dataset was a pivotal aspect of our work, aiming to provide an effective platform to validate few-shot ASQP methods. FSQP provides a more balanced representation and covers more categories, offering as a comprehensive benchmark for evaluating few-shot ASQP. We hope it can serve as a valuable resource for future research, driving advancements in this field. 

3. **Highlights of this work besides dataset.** Besides the contribution of the dataset, our method has also made significant progress in the ASQP task, demonstrating strong superiority.
To demonstrate the validity of our approach, we also report p-value values. Note that the improvements are significant if the p-value is less than 0.05.<table>
    <tr>
        <th rowspan = "2">Method</th>
        <th colspan = "3">One-shot</th>
    </tr>
    <tr>
        <th>P</th>
        <th>R</th>
        <th>F1</th>
    </tr>
    <tr>
        <th>BvSP VS GAS</th>
        <td><span style="color:#ff0000">0.0091</span></td>
        <td>0.1333</td>
        <td><span style="color:#ff0000">0.0262</span></td>
    </tr>
    <tr>
        <th>BvSP VS Paraphrase</th>
        <td><span style="color:#ff0000">0.0002</span></td>
        <td><span style="color:#ff0000">0.0002</span></td>
        <td><span style="color:#ff0000">0.0001</span></td>
    </tr>
    <tr>
        <th>BvSP VS DLO</th>
        <td><span style="color:#ff0000">0.0050</span></td>
        <td>0.0832</td>
        <td><span style="color:#ff0000">0.0140</span></td>
    </tr>
    <tr>
        <th>BvSP VS ILO</th>
        <td><span style="color:#ff0000">0.0001</span></td>
        <td><span style="color:#ff0000">0.0004</span></td>
        <td><span style="color:#ff0000">0.0003</span></td>
    </tr></table>

4. **Improve readability.** 
We will certainly take your advice into account and seek assistance from proficient English speakers to enhance the paper's readability and overall quality. 

