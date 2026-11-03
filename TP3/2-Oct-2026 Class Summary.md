1. Hugging Face: An AI platform and community that provides pretrained models, datasets, and tools for developing AI applications.


2. Unsloth: An open-source library that makes LLM fine-tuning faster and more memory-efficient.


3. Fine-Tuning: Adapting a pretrained model to a specific task by continuing its training on a smaller, task-specific dataset.


4. Model: A trained neural network that processes input data and produces predictions or outputs.


5. Preprocessor: Prepares raw data into the format required by the model.
- Text: Tokenizer
- Image: Image Processor
- Audio: Audio Processor


6. Model Selection: Choosing a suitable model based on:
- Task Alignment
- Model Architecture
- Model Size and Complexity
- Performance Benchmarking
- Community Support and Documentation


7. Model Loader: Loads pretrained model architecture and weights into memory.

Two main types in Hugging Face Transformers:
- Model-Specific Loaders: Load a specific model architecture.
- BertForSequenceClassification
- GPT2LMHeadModel
- T5ForConditionalGeneration

- AutoModel Loaders: Automatically select the appropriate model architecture based on the model identifier.
- AutoModel: General-purpose model.
- AutoModelForSequenceClassification: Text classification.
- AutoModelForTokenClassification: Token classification (NER).
- AutoModelForQuestionAnswering: Question answering.
- AutoModelForCausalLM: Text generation (GPT).
- AutoModelForMaskedLM: Masked language modeling (BERT).
- AutoModelForSeq2SeqLM: Translation and summarization.
- AutoModelForSpeechSeq2Seq: Speech-to-text.


8. Processor Loader: Automatically loads the appropriate processor based on the model type.
Processor types include:
- Tokenizer
- Image Processor
- Audio Processor
- Multimodal Processor
- Audio-Text Processor
Example:
AutoProcessor.from_pretrained(model_name)


9. Quantization: Reduces the precision of model weights or activations to make models smaller and more efficient.
- FP32: 32-bit floating point.
- FP16: 16-bit floating point.
- INT8: 8-bit integer.
- 4-bit: Further reduces memory usage.


10. LoRA (Low-Rank Adaptation): A parameter-efficient fine-tuning (PEFT) method that freezes original model weights and trains two smaller matrices (A and B).
Example:
- Original matrix: 512 × 512 = 262,144 parameters.
- Matrix A: 512 × 8.
- Matrix B: 8 × 512.
- LoRA trainable parameters: 8,192.
- Parameter reduction: Approximately 97%.

Formula: W'=W+AB