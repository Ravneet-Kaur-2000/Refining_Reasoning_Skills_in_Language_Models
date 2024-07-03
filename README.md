
<p align="center">

  <h2 align="center">Refining Reasoning Skills in Language Models(RRSLM)</h2>
</p>



<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary><h2 style="display: inline-block">Table of Contents</h2></summary>
    <li><a href="#about-the-project">About The Project</a></li>
      <li><a href="#technology-used">Technology Used</a></li>
      <li><a href="#fine-tuning">Fine tuning</a></li>
    <li><a href="#conclusion">Conclusion</a></li>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project

Developed RRSLM by leveraging teacher models, such as GPT-4 (1.7 trillion parameters), and Llama-2 (13 billion parameters), to generate reasoning samples for fine-tuning smaller models like GPT-3 and GPT-2. 
Assessed the approach across 6 diverse datasets, covering complex reasoning tasks in arithmetic (SingleEq, AddSub, MultiArith, SVAMP) and miscellaneous challenges (Date Understanding, Tracking Shuffled Objects).

### Technology Used

* Python
* GPT
* Llama-2


### Fine Tuning

For fine-tuning the student models three-step approach used:
* Reasoning generation: Employed the GPT-4 model and Llama2 13B to generate sequential reasoning explanations (ri) for the questions (qi) within the dataset. The prompt was structured as follows: "qi. Think step by step.
* Prompt completion pairs generation: Utilizing all questions and reasoning explanations, constructed prompt completion pairs
to fine-tune the student models. These pairs were formatted as follows: prompt="qi", completion="ri –> ai END"
* Fine-tuning: Used 70% of the data as train data while holding out the remaining 30% data as test data. Prompt completion
pairs were then serialized into a JSON file to serve as training data, which is subsequently utilized as input for fine-tuning the student
model. For GPT-3 following hyperparameters were used:(n_epochs=30, batch_size=5,
learning_rate_multiplier=2). For GPT-2 following hyperparameters were used: 
(n_epochs=50, per_device_train_batch_size

### Conclusion
* Larger teacher models (models with more parameters) generate better reasoning samples thus imparting better reasoning ability in the
student models during fine-tuning.
* The optimal token length depends upon the
task to be performed. Date Understanding has
a smaller maximum token limit than AddSub
and MultiArith which is smaller than the Shuffled Objects task.
