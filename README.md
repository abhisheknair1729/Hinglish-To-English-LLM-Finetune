### Finetune a foundational LLM model to translate *Hinglish* text to English text

For the purposes of this project, Hinglish means Hindi text written using Germanic characters and the occasional English word thrown in.


#### Model details

I chose the [OpenHathi](https://huggingface.co/sarvamai/OpenHathi-7B-Hi-v0.1-Base) 7B parameter base model from [Sarvam AI](https://www.sarvam.ai/) as my foundation model. Two major reasons for choosing this model:

1. It is pretrained on Hindi, English and Hinglish. Therefore, during finetuning, we can focus on teaching the model about translation, rather than the underlying structure of the languages themselves. This is important because Hindi has a different word-order as compared to English and we would require a lot of training data to teach the model this new sentence structure.

2. The model is compatible with the [HuggingFace](https://huggingface.co/) [transformers](https://huggingface.co/docs/transformers/en/index) library. I used this library extensively to efficiently finetune the model.

#### Finetuing dataset details

I used a [English-To-Hinglish](https://huggingface.co/datasets/findnitai/english-to-hinglish) dataset on huggingface for finetuning. Since I was training the model to only do unidirectional (Hinglish to English) translation, I had to swap the fields in this datset while training (used input as output and vice-versa).

#### Blog post I followed

There are plenty of blog posts describing how to finetune a model. I followed https://www.philschmid.de/fine-tune-llms-in-2024-with-trl.

#### Additional notes

The one aspect I had to change from the procedure in the blog post was to add an EOS (end-of-sentence) token to my training dataset and the embedding layer of the model. Without this, the finetuned model would first translate the input query, and would then continue to print out garbage text. Adding an EOS token fixed that.

Thanks for reading!
