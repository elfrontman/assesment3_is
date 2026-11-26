Preprocessing – Key Information for Model Fine-Tuning

Project: ISY503 – Assessment 3
Task: NLP Sentiment Analysis on Amazon Product Reviews
Preprocessing: Heidy
Next stage: GPT-2 Fine-Tuning – Renato

1. Preprocessing Overview

The preprocessing stage is complete. The cleaned Amazon reviews have been split, tokenized and exported as Hugging Face datasets for the next stage of model development.

The original cleaned dataset contains 7,852 unique reviews across four product domains:

Books
DVD
Electronics
Kitchen & Housewares

The preprocessing workflow uses stratified sampling based on domain and label to maintain representative distributions across all subsets.

2. Dataset Splits
Split	Percentage	Samples
Train	70%	5,496
Validation	15%	1,178
Test	15%	1,178
Total	100%	7,852
Random state: 42
Stratification: domain + label
Binary sentiment labels: 0 = negative, 1 = positive

Data leakage prevention:

Train: model training.
Validation: performance monitoring and hyperparameter tuning.
Test: final evaluation only.

The test set must remain isolated from training and model selection.

3. GPT-2 Tokenizer Configuration
Parameter	Value
Model	gpt2
Tokenizer	GPT2TokenizerFast
Vocabulary size	50,257
Maximum sequence length	512
Padding token	EOS (`<
Padding token ID	50256
Padding side	Right
Truncation	Enabled
Sequence Length Selection

The maximum sequence length was determined using the 95th percentile of the Training dataset token length distribution.

95th percentile: approximately 524 tokens.
Rounded value: 528 tokens.
Selected maximum: 512 tokens, capped for computational efficiency.

The same maximum length is applied consistently across all three splits.

Reviews exceeding 512 tokens are truncated.

4. Tokenized Dataset Structure

The Hugging Face DatasetDict is exported to:

outputs/preprocessing/tokenized_dataset/hf_dataset/

Each split contains the following features:

Feature	Description
input_ids	GPT-2 token IDs
attention_mask	Identifies actual tokens and padding positions
labels	Binary sentiment targets

The original full_text and label columns are removed after tokenization. Sentiment targets are retained under labels.

5. Padding and Batch Preparation

Dynamic padding is configured using Hugging Face DataCollatorWithPadding.

Configuration:

Dynamic padding enabled.
Right-side padding.
pad_to_multiple_of=8.
PyTorch tensors.

Padding is applied at batch creation rather than permanently to the stored dataset.

Model Configuration Considerations

GPT-2 does not define a dedicated padding token by default. EOS is reused as PAD.

When initializing the classification model, ensure:

python
model.config.pad_token_id = tokenizer.pad_token_id


The generated attention_mask must be passed during training.

Use the exported tokenizer and maintain consistency with the preprocessing configuration.

6. Exported Resources

All preprocessing outputs are located under:

outputs/preprocessing/

Resource	Location
Training split	splits/train.csv
Validation split	splits/validation.csv
Test split	splits/test.csv
Tokenized datasets	tokenized_dataset/hf_dataset/
GPT-2 tokenizer	tokenized_dataset/tokenizer/
Preprocessing configuration	tokenized_dataset/preprocessing_config.json

The exported Hugging Face datasets can be loaded directly using load_from_disk().

No additional splitting or tokenization is required unless the preprocessing strategy is intentionally changed.

7. Fine-Tuning Considerations
The following points should be considered during model implementation:

Architecture: Use GPT2ForSequenceClassification or an equivalent GPT-2 binary classification architecture.
Output classes: Configure num_labels=2.
Padding: Ensure the model's pad_token_id matches the tokenizer's PAD token ID (50256).
Attention masks: Pass attention masks to the model to distinguish actual tokens from padding.
Labels: Preserve the existing binary label mapping.
Sequence length: Maintain MAX_LENGTH=512 for consistency with preprocessing.
Batch preparation: Reuse the exported tokenizer and dynamic padding configuration.
Evaluation: Use Validation for model selection and Test only for final performance evaluation.
8. Handover
The preprocessing outputs are ready for the GPT-2 fine-tuning stage.

The next stage can proceed directly with model initialization, training configuration, fine-tuning and sentiment classification evaluation.

Preprocessing completed by: Heidy
Next stage: GPT-2 Fine-Tuning – Renato
