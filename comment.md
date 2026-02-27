  
Reviewer 1: This paper presents SemCast, a simple three-stage framework that combines probabilistic traffic forecasting with LLM-based semantic reasoning. A pre-trained generative time-series model produces multiple candidate future trajectories, and an LLM incorporates textual event information to select a context-consistent forecast and generate interpretable reports and management suggestions. The method targets robustness under anomalous traffic conditions.

Strengths:
Intuitive and simple design: The framework cleanly separates numerical forecasting and semantic reasoning, using each component for what it does best.
Practical use of LLMs: LLMs are applied only at inference time without fine-tuning, preserving zero-shot generalization and reducing system complexity.
Improved robustness under anomalies: Incorporating event text clearly improves predictions in non-recurring and semantically complex scenarios.

Weaknesses:
No guarantee of event-aware coverage: Event information is only introduced after candidate trajectories are generated, implicitly assuming the generative model already covers event-induced dynamics, which may not hold true, especially when introducing new event types.
Limited discussion of scalability: The computational and latency costs of using large LLMs in the forecasting loop are not sufficiently analyzed.

Minor:
There are many LaTeX errors in the use of quotation marks, where ``'' should be used instead of "". This issue appears frequently in Section 5.4; please proofread carefully.


Reviewer 2: This paper presents a new framework for traffic forecasting, with enhanced capabilities in context-awareness and explanability. Overall, I think it is a novel framework. Here are my detailed comments: 
- As the contextual information is incorporated in Stage 2, what happens if the Stage 1 does not provide a good candidate trajectory? For example, if there is a car crash, but in Stage 1 only outputs recurrent and regular trajectories. 
- How the Foundational probabilistic forecasting is trained? Whether it is trained on multiple datasets?
- Please provide some statistics and examples of the contextual data.
- Please further clarify the probabilistic trajectory generation, what does the randomness come from? Is it from the random seed or other sources?
- How to assess the quality of explainable report and recommendations? More experiments should be incorporated
- Overall, I think the numerical experiments are limited, more discussions and experiments should be included to reflect the performance of the proposed methods in various aspects.




Reviewer 3: This paper introduces SemCast, a hybrid framework combining a probabilistic forecasting model with an LLM to improve traffic forecasting during non-routine events. The focus on non-recurrent traffic forecasting is valuable, and the method is interesting and reasonable. However, some methodological details, baseline comparisons, and presentation aspects require further clarification to ensure the paper's quality and reproducibility. I recommend a minor revision before publication.

Major Comments
1.	The mechanism in Stage 2 requires clarification regarding whether the LLM generates new numerical values or strictly selects from the candidate set. The text mentions adjustment, but Equation 10 implies a selection process. If the LLM generates new values, the authors should explain how the model ensures these values remain within realistic traffic distributions.
2.	The semantic serialization process in Section 4.3.1 needs more detail for reproducibility. Specifically, the authors should define the rules or thresholds used to map numerical gradients to linguistic descriptors. Providing examples of this mapping would strengthen the methodology section.
3.	The comparison with the Chronos baseline needs further discussion regarding fairness. SemCast benefits from pre-training on the specific Beijing dataset, whereas Chronos is evaluated in a zero-shot setting. The authors should acknowledge this distinction or discuss how domain adaptation contributes to the performance gap.
4.	The computational feasibility for real-time applications should be addressed. Given the use of a 14B parameter LLM for reasoning, the authors need to provide a brief analysis of the inference latency to confirm the system can meet the time constraints of operational traffic management.

Minor Comments
1.	The legibility of Figure 2 should be improved. The font sizes for axis labels and legends are currently too small to read easily. Additionally, clearly marking the start and end times of the anomalous events on the time axis would help readers interpret the results.
2.	In the ablation study, the authors should briefly explain how the vague and incorrect contexts were generated. Describing the specific method of degrading the context will help readers better understand the robustness results presented in Figure 4c.
3.	The role of historical case retrieval in Stage 3 needs clarification. The authors should specify whether the retrieved cases act merely as context for the prompt or if there is a mechanism to enforce adherence to historical patterns to prevent hallucination.
4.	The notation for the context variable s should be checked for consistency. The manuscript should clearly distinguish between the raw context data and the processed textual representations used in the LLM components.
