
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

For fine-tuning the student models, a three-step approach was used:
* Reasoning generation: The GPT-4 model and Llama2 13B were employed to generate sequential reasoning explanations (ri) for the questions (qi) within the dataset. The prompt was structured as follows: "qi. Think step by step."
* Prompt completion pairs generation: Using all questions and reasoning explanations, prompt completion pairs were constructed to fine-tune the student models. These pairs were formatted as follows: prompt="qi", completion="ri –> ai END".
* Fine-tuning: 70% of the data was used as train data, while the remaining 30% was held out as test data. Prompt completion pairs were serialized into a JSON file to serve as training data, which was subsequently used as input for fine-tuning the student models. For GPT-3, the following hyperparameters were used: (n_epochs=30, batch_size=5, learning_rate_multiplier=2). For GPT-2, the following hyperparameters were used: (n_epochs=50, per_device_train_batch_size= 8, overwrite_output_dir = False).


### Conclusion
* Larger teacher models (models with more parameters) generate better reasoning samples, thereby imparting better reasoning ability to the student models during fine-tuning.
* The optimal token length depends on the task to be performed. Date Understanding has a smaller maximum token limit than AddSub and MultiArith, which is smaller than the Shuffled Objects task.
