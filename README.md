# Facial-Expression-Recognition-in-Unconstrained-Environment
Mathematical Foundation of the Ensemble Model Construction

This section describes the ensemble methodology for Facial Emotion Recognition (FER) using three deep learning models, each providing confidence scores. The ensemble leverages a rank-based fusion strategy with non-linear functions (exponential and hyperbolic tangent) to generate fuzzy ranks, enhancing the robustness and accuracy of emotion classification. Here’s a breakdown of each step:

    Confidence Scores of Base Models:
        Each base model ii (i.e., DenseNet169, EfficientNetB7, InceptionV3) provides confidence scores for CC emotion classes. Let the confidence scores from each base model ii be:
       $ Pri1,Pri2,Pri3,…,PriC$
        Pri1​,Pri2​,Pri3​,…,PriC​ where i∈{1,2,3}i∈{1,2,3}.
        Each model’s confidence scores sum up to 1, ensuring a valid probability distribution:
        ∑k=1CPrik=1,∀i∈{1,2,3}
        k=1∑C​Prik​=1,∀i∈{1,2,3}

    Non-linear Fuzzy Rank Transformation:
        To transform the confidence scores into ranks, two non-linear functions, exponential and hyperbolic tangent, are applied:
        y=1−exp⁡(−(x−1)22)
        y=1−exp(−2(x−1)2​)
        y=1−tanh⁡((x−1)22)
        y=1−tanh(2(x−1)2​)
        Here, xx represents the confidence score for a class, and these functions transform scores into fuzzy ranks, adding non-linearity that enhances discrimination among classes.

    Applying Non-linear Functions to Confidence Scores:
        The confidence scores PrikPrik​ are passed through each function to obtain fuzzy ranks:
        Ranki1k=1−tanh⁡((Prik−1)22)
        Ranki1k​​=1−tanh(2(Prik​−1)2​)
        Ranki2k=1−exp⁡(−(Prik−1)22)
        Ranki2k​​=1−exp(−2(Prik​−1)2​)
        Significance of Each Function:
            Exponential function: Has a downward concavity, creating a rank output that approaches 1 as probability approaches 1.
            Hyperbolic tangent function: Has an upward concavity in the [0,1] domain, resulting in rank values that increase as probability moves closer to 0.

    Fused Rank Scores Calculation:
        The fuzzy ranks from both functions are combined to calculate a fused rank score for each class:
        RSik=Ranki1k×Ranki2k
        RSik​=Ranki1k​​×Ranki2k​​
        Here, Ranki1ki1k​​ offers a reward for correct classifications (higher scores for probable classes), while Ranki2ki2k​​ captures the divergence, ensuring balanced influence on the final rank.

    Final Fused Score Calculation:
        The fused scores RSikRSik​ are aggregated across all models to produce a final score tuple:
        FSk=∑i=1LRSik,∀k=1,2,3,…,C
        FSk​=i=1∑L​RSik​,∀k=1,2,3,…,C
        This step aggregates the rank information from each base model, capturing the degree of confidence towards each class.

    Emotion Class Selection:
        The class with the minimum fused score FSkFSk​ is selected as the predicted emotion class:
        Emotion class (I)=min⁡∀kFSk
        Emotion class (I)=∀kmin​FSk​
        This approach helps in selecting the most probable emotion class, based on the fused confidence across models.

This ensemble strategy, with its rank-based fusion approach, provides a unique method to combine the strengths of different models, achieving a robust FER system suited for real-world scenarios. Each step contributes to the system's accuracy by fine-tuning the handling of confidence scores and enhancing the model's interpretability.
