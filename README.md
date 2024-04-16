# kunal Sharma

# Wide and Deep Learning Recommender Systems

## CODE TO BE ADDED SOON

## Introduction

In today's diverse digital landscape, user engagement with websites and interfaces is characterized by diverse patterns, shaped by individual preferences, distinct needs, and specific desired outcomes. The cornerstone of an outstanding user experience is the efficient and seamless realization of these objectives. Consequently, elevating user retention is contingent upon the delivery of a meticulously optimized User Experience (UX).

However, within the domain of sophisticated interfaces such as Bhuvan, which offers a plethora of interconnected services, the intricacies of navigation present a formidable challenge, potentially compromising the overarching user experience. Mitigating this challenge necessitates a strategic focus on refining navigation processes, directing users towards relevant information and services in alignment with their ongoing activities and prior interactions.

This proposal endeavors to explore the integration of Recommender Systems as a systematic approach to provide users with bespoke suggestions tailored to their specific objectives. The objective is to enhance user satisfaction and streamline interactions within the Bhuvan platform.

## Our Approach

### Gathering User Interaction Data

We will implement a script ( JavaScript for websites ) that records various features and data generated during user’s interaction with the interface.

### Exploratory Data Analysis

We conduct EDA on collected user interaction data to derive insight on how different feature interact and affect future user behaviour.

### Feature Engineering

We will use the insight gained from EDA to clean up the data, transform features as well as create new features through methods such as cross-product feature transformation.

### Model Selection

Common problem faced by Recommender Systems is “Cold-Start”, i.e. when we have insufficient data to make recommendation to user. To resolve this, we will be using Wide and Deep Learning Recommender System.

#### Recommender systems are broadly implemented in two ways:

<img align="right" src="./images/filtering-infographics.png" width="500"/>

### Collaborative Filtering :

It makes recommendation based on user activity and its relation to activity of other users. That is it makes recommendation based on user similarity and association.

### Content-Based Filtering:

Content-based filtering uses item features to recommend other items similar to what the user likes, based on their previous actions or explicit feedback.

# Wide and Deep Learning Recommender System

The WADL RS method represents a hybrid paradigm, incorporating elements of both Collaborative Filtering and Content-Based Filtering. The "wide" segment, commonly termed the linear model, is dedicated to memorizing user profiles and their historical preferences. Meanwhile, the "deep" segment employs deep neural networks to enhance generalization for unseen feature combinations by developing low-dimensional dense embeddings associated with sparse features.

In essence, the "wide" component facilitates Collaborative Filtering, capturing user interactions and preferences, while the "deep" counterpart supports Content-Based Filtering, leveraging neural networks to comprehend intricate feature relationships. This dual-pronged strategy adeptly addresses the "Cold Start" challenge often encountered in recommender systems, ensuring effective recommendations even in scenarios with limited user data.

<img src="./images/wide-and-deep-learning-architecture.png" />

## Architecture

Wide and Deep learning framework jointly trains feed-forward network with embeddings ( deep learning) and a linear model with feature transformations for generic recommender systems with sparse inputs ( wide learning ).

## Working

### The Wide Component:

It is generalized linear model in form:

$` y = W_{wide}^T * x + b `$

Where `y` is prediction, `x` is vector of features, `W` is vector of learned parameters and `b` is bias.

### The Deep Component:

It is feed-forward network, where each hidden layer performs following computation:

$` a_{l+1} = f( W_{deep}^T * a_l + b_l )`$

`l` is layer number, `f` is the activation function , $`a_l`$ is vector of activation for l-th layer , $`b_l`$ is vector of biases for l-th layer and `W` is the weight vector for deep learning

### Final Model:

It is attained by combining wide and deep component

$` P( Y = 1|X ) = sigmoid( W_{wide}^T  * x + W_{deep}^T * a_{last} + b )`$

where `Y` is the binary class label, $`W_{wide}`$ is the vector of all wide model weights, $`W_{deep}`$ is the vector of weights applied on the final activation $`a_{last}`$, and `b` is the bias term.

#### Sigmoid Function:

$` g(z) = \dfrac{1}{1+e^-z}`$ where $`0 < g(z) < 1`$

## Training

We will train the model using the data collected / logged during User Interaction with the Interface.

## Evalutaion

We will use **_AUC ( Area Under Receiver Operator Characteristic Curve )_** since we are “classifying” the recommendation as relevant or not.

## Real-Time Inference and Updates

<img align="right" src="./images/inference-diagram.png" />

The Real-Time User Activity Data collected through our script will be used as input to Infer a prediction / recommendation from our model.

After sufficient new data is collected, it will be used to retrain the model for assimilation of real-time data. However, retraining from scratch every time is computationally expensive and delays the time from data arrival to serving an updated model. To tackle this challenge, we implement a warm-starting system which initializes a new model with the embeddings and the linear model weights from the previous model thus saving us time of training model from scratch.

<br/>

## Generalized Model and High Transferability

<img align="left" src="./images/model-training-diagram.png" />

Given the incorporation of Neural Networks, our model is inherently multi-modal, allowing for broad generalization across diverse data types. When appropriately managed, the model seamlessly accommodates various media formats, including text, images, audio, and more. This versatility not only positions the model for providing recommendations on interface navigation but also extends its applicability to diverse data forms. Consequently, our model demonstrates a high degree of transferability, making it well-suited for adaptation and implementation in other fields.

<br/>

# References

1. [Wide and Deep Learning Paper](https://arxiv.org/pdf/1606.07792.pdf)
2. [Current research in Deep recommendation systems](https://arxiv.org/pdf/1606.07792.pdf)
3. [Building Deep Recommendation Systems](https://developer.nvidia.com/blog/how-to-build-a-winning-recommendation-system-part-2-deep-learning-for-recommender-systems/)
4. [Collaborative Filtering](https://www.analyticsvidhya.com/blog/2022/02/introduction-to-collaborative-filtering/)
5. [Various implementations of Collaborative Filtering](https://towardsdatascience.com/various-implementations-of-collaborative-filtering-100385c6dfe0)
6. [Matrix Factorization and its application in Collaborative Filtering](https://towardsdatascience.com/understanding-the-scaling-of-l%C2%B2-regularization-in-the-context-of-neural-networks-e3d25f8b50db)
7. [Application of AI in recommender systems](https://theaisummer.com/recommendation-systems/#wide-and-deep-learning)
