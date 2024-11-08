# Facial-Expression-Recognition-in-Unconstrained-Environment
the mathematical steps involved in your ensemble model, along with their significance:

    Confidence Scores of Base Models (Eqn. 2):
        The confidence scores (Pri1,Pri2,…,PriC)(Pri1​,Pri2​,…,PriC​) are provided by each base model for each of the CC classes.
        Equation (2) ensures that for each model ii, the sum of these probabilities over all classes equals 1, meaning that the scores are normalized to form a probability distribution.
        This normalization is essential as it aligns the outputs of the base models and makes the ensemble calculations consistent.

    Fuzzy Rank Generation with Non-linear Functions (Eqn. 3 & 4):

        Exponential (Eqn. 3):
        y=1−exp⁡(−(x−1)22)
        y=1−exp(−2(x−1)2​)
            This function maps the confidence score to a fuzzy rank. Because of its downward concavity in the interval [0,1], higher probabilities result in ranks that are closer to 1.
            This reflects a "reward" as confidence increases, which is a property that contributes to distinguishing high-confidence predictions from low-confidence ones.

        Tanh (Eqn. 4):
        y=1−tanh⁡((x−1)22)
        y=1−tanh(2(x−1)2​)
            This function similarly transforms the confidence scores into ranks, but with an upward concave shape, moving values closer to 0 as confidence decreases.
            The choice of tanh contributes a contrast in behavior compared to the exponential function, capturing different aspects of the rank score as the probabilities vary.

    Application of Fuzzy Ranking Functions (Eqn. 5 & 6):
        Rank Calculation (Eqn. 5 & 6):
        Ranki1,k=1−tanh⁡((Prik−1)22)
        Ranki1,k​=1−tanh(2(Prik​−1)2​)
        Ranki2,k=1−exp⁡(−(Prik−1)22)
        Ranki2,k​=1−exp(−2(Prik​−1)2​)
        These equations replace xx with the actual confidence score PrikPrik​ from each base model and assign a fuzzy rank for each class confidence score, balancing both the exponential and tanh responses.
        Together, these ranks capture subtle variations in the confidence scores, with the exponential function controlling rapid score changes and the tanh providing a softer gradient, which improves robustness in final rank estimation.

    Fused Rank Scores (Eqn. 7):
    RSik=Ranki1×Ranki2
    RSik​=Ranki1​×Ranki2​
        By multiplying the fuzzy ranks from both functions, the fused rank score captures the cumulative confidence across models, with the exponential function’s narrower range influencing the final rank score more.
        This approach gives more weight to the highest-confidence classes by dampening lower-confidence ranks, enhancing class distinctions for the ensemble.

    Final Fused Score (Eqn. 8):
    FSk=∑i=1LRSik
    FSk​=i=1∑L​RSik​
        The final score for each class FSkFSk is calculated by summing the fused rank scores across all models, which aggregates the contributions of each base model’s confidence toward that class.
        This sum enables the ensemble to synthesize the base model outputs, with higher scores signifying greater confidence from multiple models in a specific class.

    Winner Class Selection (Eqn. 9):
    Emotion class(I)=min⁡∀kFSk
    Emotion class(I)=∀kmin​FSk
        The final classification is determined by identifying the class with the lowest FSkFSk value, which represents the class that the ensemble is most confident about.
        This fusion-based approach, with a focus on the minimum score, minimizes the error in cases where confidence diverges across models and helps in achieving accurate class selection.

Overall Significance:

    By employing both exponential and tanh functions, the ensemble model benefits from a nuanced ranking strategy that captures high-confidence scores and minimizes lower-confidence influences, yielding reliable class predictions.
    This method allows the ensemble to exploit the strengths of each base model's score distribution, ensuring robustness and accuracy in classification.
