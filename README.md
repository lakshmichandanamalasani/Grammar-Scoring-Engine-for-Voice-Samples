# Grammar-Scoring-Engine-for-Voice-Samples
In this solution, we combined deep audio representations from Wav2Vec2 with lightweight linguistic features extracted from transcripts to predict a continuous label. Here's a breakdown of our approach, results, and some thoughts on further improvement:

Approach
Audio Embeddings: We used facebook/wav2vec2-base-960h, a pretrained model for speech representation learning. From each audio file, we extracted the mean pooled hidden states as feature vectors, capturing the semantic and phonetic properties of the speech.

Text Features: For each corresponding transcript, we extracted features using spaCy, including:

Number of tokens
Sentence count
Noun chunk count
Average token length
Grammar error count via LanguageTool API
These features aim to capture syntactic and grammatical fluency.
Model: We trained an MLPRegressor (Multi-Layer Perceptron) with two hidden layers (256 and 128 units), which learns non-linear patterns in the combined feature space.

Evaluation: The model was evaluated using:

Root Mean Square Error (RMSE) for regression accuracy
Pearson Correlation Coefficient to measure how closely our predictions align with actual labels
Results
Metric	Score
Training RMSE	0.5181
Validation RMSE	0.7956
Pearson Corr.	0.7519
The model performs reasonably well with strong correlation between predicted and true scores. While the RMSE indicates a moderate error, it’s within an acceptable range for human-like assessments.

Insights & Future Improvements
Wav2Vec2 is powerful, but fine-tuning it (instead of using frozen features) could further improve accuracy — especially if we have enough labeled data.

Text features help, but can be expanded by including:

Readability metrics (e.g., Flesch score)
Semantic similarity to prompts or references
Named entity or POS tag distributions
Modeling Alternatives:

Try LightGBM or XGBoost on the same features for better interpretability
Use transformer-based fusion to learn from both modalities jointly
Data Quality matters: mislabeled or noisy transcripts can impact text feature quality, so validating or cleaning those inputs would help.

Conclusion
This hybrid audio-text pipeline showcases how combining pretrained deep models with linguistic intuition can result in a robust, interpretable system. With some additional tuning and creativity, this framework can definitely reach even more competitive performance.
