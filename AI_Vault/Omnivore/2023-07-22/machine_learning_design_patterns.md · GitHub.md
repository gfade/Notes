---
id: e1a89af9-4fe0-41eb-8763-9f7bb9dd9543
---

# machine_learning_design_patterns.md · GitHub
#Omnivore

[Read on Omnivore](https://omnivore.app/me/https-gist-github-com-veekaybee-58-b-9-fbd-0-fe-572-d-09143-e-69-1897dacf8ed)
[Read Original](https://gist.github.com/veekaybee/58b9fbd0fe572d09143e692e1a444c79)

## [Machine Learning Design Patterns](https://learning.oreilly.com/library/view/machine-learning-design/9781098115777/)

This book is all about patterns for doing ML. It's broken up into several key parts, building and serving. Both of these are intertwined so it makes sense to read through the whole thing, there are very many good pieces of advice from seasoned professionals. The parts you can safely ignore relate to anything where they specifically use GCP. The other issue with the book it it's very heavily focused on deep learning cases. Not all modeling problems require these. Regardless, let's dive in. I've included the stuff that was relevant to me in the notes.

## Most Interesting Bullets:

* Machine learning models are not deterministic, so there are a number of ways we deal with them when building software, including setting random seeds in models during training and allowing for stateless functions, freezing layers, checkpointing, and generally making sure that flows are as reproducible as possible.
* It's generally not a good idea to throw away outliers in data - a lot of ML prework is focused on scaling, clipping, and otherwise dealing with data that we still may want but to make sure they don't bias the distribution
* A couple of overarching patterns carry through everything: hashing (i.e. features, creating feature stores, embeddings in a way) to create a way to lookup inputs, features, etc and increase performances of our models and systems. Anywhere we can apply a hash insertion/loop strategy, we operate in `O(1)` time.
* We need to truly understand our data and the business domain we operate in to decide which strategy will make sense for our particular model

## High-Level

* Challenges in **building models** and ML intuition  
   * Data representation  
         * Hashed features  
         * Embeddings  
         * Feature Cross  
   * ML Problem representation  
         * reframing them,  
         * multilables,  
         * ensemble/cascade models, and  
         * rebalancing
* Challenges in **serving models**  
   * The way we train models  
         * understanding a typical training loop,  
         * checkpointing,  
         * transfer learning  
         * hyperparameter tuning  
   * Serving  
         * stateless  
         * batch  
         * continued evaluation  
         * two-phase prediction  
         * keyed prediction  
   * Reproducible design  
         * transform,  
         * bridged schema  
         * windowed infrenrece  
         * workflow pipelines  
         * feature stores  
         * model versioning

## Intro and high-level overview of ML modeling approaches to problems

> This is a catalog of patterns that we have observed in practice, among multiple teams. In some cases, the underlying concepts have been known for many years. We don’t claim to have invented or discovered these patterns. Instead, we hope to provide a common frame of reference and set of tools for ML practitioners. We will have succeeded if this book gives you and your team a vocabulary when talking about concepts that you already incorporate intuitively into your ML projects.

[![image](https://proxy-prod.omnivore-image-cache.app/0x0,sxhBI_cgHn36UftOu7Lh0VPt2qjZwW6GL25CgZ3ipRDg/https://user-images.githubusercontent.com/3837836/216646700-bd49adb8-3031-42e6-88ed-f2f43032d7b9.png)](https://user-images.githubusercontent.com/3837836/216646700-bd49adb8-3031-42e6-88ed-f2f43032d7b9.png)

## Challenges in building models and ML intuition

## Data Drift and Concept Drift

* There are several types of drift in models that mean that either the model becomes out of date or the data feeding the model become out of date and are things we need to watch for.

### Concept Drift:

[Concept drift](https://arxiv.org/pdf/2004.05785.pdf): When the underlying statistical properties of the response variable change over time. Concept drift occurs whenever the relationship between the model inputs and target have changed. This often happens because the underlying assumptions of your model have changed, such as models trained to learn adversarial or competitive behavior like fraud detection, spam filters, stock market trading, online ad bidding, or cybersecurity.

### Data Drift:

When the input data fed to the model changes over time e.g. if the season changes

> While machine learning models typically represent a static relationship between inputs and outputs, data can change significantly over time. Data drift refers to the challenge of ensuring your machine learning models stay relevant, and that model predictions are an accurate reflection of the environment in which they’re being used. For example, let’s say you’re training a model to classify news article headlines into categories like “politics,” “business,” and “technology.” If you train and evaluate your model on historical news articles from the 20th century, it likely won’t perform as well on current data. Today, we know that an article with the word “smartphone” in the headline is probably about technology. However, a model trained on historical data would have no knowledge of this word.

How to solve for these:

## Different modeling perspectives:

> Though there is often a single team responsible for building a machine learning model, many teams across an organization will make use of the model in some way. Inevitably, these teams may have different ideas of what defines a successful model.

> To understand how this may play out in practice, let’s say you’re building a model to identify defective products from images. As a data scientist, your goal may be to minimize your model’s cross-entropy loss. The product manager, on the other hand, may want to reduce the number of defective products that are misclassified and sent to customers. Finally, the executive team’s goal might be to increase revenue by 30%. Each of these goals vary in what they are optimizing for, and balancing these differing needs within an organization can present a challenge.

## Hashing [features pattern](https://en.wikipedia.org/wiki/Feature%5Fhashing)

[![Screen Shot 2023-02-01 at 8 49 30 PM](https://proxy-prod.omnivore-image-cache.app/592x0,snHFE0sSf_c56f9DrmSL3Vzaubu5Kf-uMc9x4l7TP-Zo/https://user-images.githubusercontent.com/3837836/216211220-13ced423-7621-4993-991b-ae9db12b9c55.png)](https://user-images.githubusercontent.com/3837836/216211220-13ced423-7621-4993-991b-ae9db12b9c55.png)

Note that the hashing trick isn't limited to text classification and similar tasks at the document level, but can be applied to any problem that involves large (perhaps unbounded) numbers of features.

## Data Representation

[![Screen Shot 2023-02-01 at 8 42 19 PM](https://proxy-prod.omnivore-image-cache.app/698x0,sQOlQVHPVJBSRbXqXeRqrkHOpMwxj9Khjt-ctE7JCRw4/https://user-images.githubusercontent.com/3837836/216210378-d2baa3ad-d82a-4ef6-99e0-52f5bffdcc71.png)](https://user-images.githubusercontent.com/3837836/216210378-d2baa3ad-d82a-4ef6-99e0-52f5bffdcc71.png)

> Most modern, large-scale machine learning models (random forests, support vector machines, neural networks) operate on numerical values, and so if our input is numeric, we can pass it through to the model unchanged.

Often with our numerical data, we want to scale it

[![Screen Shot 2023-02-01 at 8 43 10 PM](https://proxy-prod.omnivore-image-cache.app/719x0,snDpILgOMKasPiSgMhSNtWvVSuNwDUZEmP4Q5Xeo1LCY/https://user-images.githubusercontent.com/3837836/216210492-32849b2a-e233-47f4-afbe-5f08e4b532f7.png)](https://user-images.githubusercontent.com/3837836/216210492-32849b2a-e233-47f4-afbe-5f08e4b532f7.png)

Scaling techniques

[![Screen Shot 2023-02-01 at 8 43 35 PM](https://proxy-prod.omnivore-image-cache.app/615x0,sz0kxSTWaBGfkdO88fuwoZ320jiFge4p_rnIJhF6j_xY/https://user-images.githubusercontent.com/3837836/216210542-6e6fd00a-b186-4080-9b0c-f3234e2a25e6.png)](https://user-images.githubusercontent.com/3837836/216210542-6e6fd00a-b186-4080-9b0c-f3234e2a25e6.png)

Winsorizing - Clipping or rounding down to some statistical distribution:

> for example, a 90% winsorization would see all data below the 5th percentile set to the 5th percentile, and data above the 95th percentile set to the 95th percentile. Winsorized estimators are usually more robust to outliers than their more standard forms, although there are alternatives, such as trimming, that will achieve a similar effect.

It's important not to throw away outliers:

> Note that we defined clipping as taking scaled values less than –1 and treating them as –1, and scaled values greater than 1 and treating them as 1\. We don’t simply discard such “outliers” because we expect that the machine learning model will encounter outliers like this in production. Take, for example, babies born to 50-year-old mothers. Because we don’t have enough older mothers in our dataset, clipping ends up treating all mothers older than 45 (for example) as 45\. This same treatment will be applied in production, and therefore, our model will be able to handle older mothers. The model would not learn to reflect outliers if we had simply thrown away all the training examples of babies born to mothers aged 50+!

> Another way to think about this is that while it is acceptable to throw away invalid input, it is not acceptable to throw away valid data. Thus, we would be justified in throwing away rows where mother\_age is negative because it’s probably a data entry error. In production, validation of the input form will ensure that the admitting clerk has to reenter the mother’s age. However, we are not justified in throwing away rows where mother\_age is 50 because 50 is a perfectly valid input and we expect to encounter 50-year-old mothers once the model is deployed in production.

### Nonlinear distributions

> What if our data is skewed and neither uniformly distributed nor distributed like a bell curve? In that case, it is better to apply a nonlinear transform to the input before scaling it. One common trick is to take the logarithm of the input value before scaling it. Other common transformations include the sigmoid and polynomial expansions (square, square root, cube, cube root, and so on). We’ll know that we have a good transformation function if the distribution of the transformed value becomes uniform or normally distributed.

[![Screen Shot 2023-02-01 at 8 45 58 PM](https://proxy-prod.omnivore-image-cache.app/598x0,sKoks-DsfRDZWhbegJ9lrf9hCE8080JNxcxSNssmJ_ec/https://user-images.githubusercontent.com/3837836/216210824-1705a414-e6e2-4c41-86a6-bd0ad81b2381.png)](https://user-images.githubusercontent.com/3837836/216210824-1705a414-e6e2-4c41-86a6-bd0ad81b2381.png)

One-hot encoding and vectorization: [what's the difference between one-hot and dummy encoding?](https://stats.stackexchange.com/questions/224051/one-hot-vs-dummy-encoding-in-scikit-learn)

Technically, a 2-element feature vector is enough to provide a unique mapping for a vocabulary of size 3\. This is called dummy coding. Because dummy coding is a more compact representation, it is preferred in statistical models that perform better when the inputs are linearly independent. Modern machine learning algorithms, though, don’t require their inputs to be linearly independent and use methods such as L1 regularization to prune redundant inputs. The additional degree of freedom allows the framework to transparently handle a missing input in production as all zeros

## Reframing an ML Problem

> The first step of building any machine learning solution is framing the problem. Is this a supervised learning problem? Or unsupervised? What are the features? If it is a supervised problem, what are the labels? What amount of error is acceptable? Of course, the answers to these questions must be considered in context with the training data, the task at hand, and the metrics for success.

[![Screen Shot 2023-02-05 at 10 16 38 PM](https://proxy-prod.omnivore-image-cache.app/564x0,szXECpMQns7t_EMwOYYdiqnONX6RWLjdVi7QZKzPA64M/https://user-images.githubusercontent.com/3837836/216876204-6cc04e4b-5ff6-42ca-9399-b6b4437f3688.png)](https://user-images.githubusercontent.com/3837836/216876204-6cc04e4b-5ff6-42ca-9399-b6b4437f3688.png)

> Changing the context and reframing the task of a problem can help when building a machine learning solution. Instead of learning a single real number, we relax our prediction target to be instead a discrete probability distribution. We lose a little precision due to bucketing, but gain the expressiveness of a full probability density function (PDF). The discretized predictions provided by the classification model are more adept at learning a complex target than the more rigid regression model.

> In some scenarios, reframing a classification task as a regression could be beneficial. For example, suppose we had a large movie database with customer ratings on a scale from 1 to 5, for all movies that the user had watched and rated. Our task is to build a machine learning model that will be used to serve recommendations to our users.

## Challenges and patterns in productionizing ML Models

### Stateless Functions

Consider stateless function patterns, or functions whose outputs are determined purely by any inputs and do not carry any additional information. (I.e. [Functional core and imperative shell](https://www.destroyallsoftware.com/screencasts/catalog/functional-core-imperative-shell) is a great pattern of this)

* Because stateless components don’t have any state, they can be shared by multiple clients. Servers typically create an instance pool of stateless components and use them to service client requests as they come in. On the other hand, stateful components will need to represent each client’s conversational state. The life cycle of stateless components needs to be managed by the server. For example, they need to be initialized on the first request and destroyed when the client terminates or times out. Because of these factors, stateless components are highly scalable, whereas stateful components are expensive and difficult to manage.

These can be hard to use in ML models because we capture a lot of state.

Solutions:

1. Export the model into a format that captures the mathematical core of the model and is programming language agnostic. (e.g. ONNX)
2. In the production system, the formula consisting of the “forward” calculations of the model is restored as a stateless function.
3. The stateless function is deployed into a framework that provides a REST endpoint.

> The approach of exporting a model to a stateless function and deploying the stateless function in a web application framework works because web application frameworks offer autoscaling, can be fully managed, and are language neutral. They are also familiar to software and business development teams who may not have experience with machine learning. This also has benefits for agile development—an ML engineer or data scientist can independently change the model, and all the application developer needs to do is change the endpoint they are accessing.

> Instead of deploying the serving function as a microservice that can be invoked via a REST API, it is possible to implement the prediction code as a library function. The library function would load the exported model the first time it is called, invoke model.predict() with the provided input, and return the result. Application developers who need to predict with the library can then include the library with their applications.

> A library function is a better alternative than a microservice if the model cannot be called over a network either because of physical reasons (there is no network connectivity) or because of performance constraints. The library function approach also places the computational burden on the client, and this might be preferable from a budgetary standpoint. Using the library approach with TensorFlow.js can avoid cross-site problems when there is a desire to have the model running in a browser.

### Batch Serving

There are cases when we don't need realtime predictions. In these cases, we can use batch (eg MapReduce, Apache Spark, BigQuery, Apache Beam, and so on)

> The Stateless Serving Function design pattern is set up for low-latency serving to support thousands of simultaneous queries. Using such a framework for occasional or periodic processing of millions of items can get quite expensive. If these requests are not latency-sensitive, it is more cost effective to use a distributed data processing architecture to invoke machine learning models on millions of items. The reason is that invoking an ML model on millions of items is an embarrassingly parallel problem—it is possible to take the million items, break them down into 1,000 groups of 1,000 items each, send each group of items to a machine, then combine the results. The result of the machine learning model on item number 2,000 is completely independent of the result of the machine learning model on item number 3,000, and so it is possible to divide up the work and conquer it.

### Feature Stores

Sometimes we want to recompute features over and over again, or use them across different models. Here, we can build a system that allows us to do so, that has an API, access to a fast-retrieval store (i.e. Redis) and a system that will recompute the features in batch, i.e. Spark or similar.

[![Screen Shot 2023-02-05 at 9 52 56 PM](https://proxy-prod.omnivore-image-cache.app/632x0,s2opXUoqSPLVl8TDI2EZ_S_N-BNfDC-Ztl8gBYC2hQ3A/https://user-images.githubusercontent.com/3837836/216872766-3a678e87-ff70-4243-ae21-88b616a67ad4.png)](https://user-images.githubusercontent.com/3837836/216872766-3a678e87-ff70-4243-ae21-88b616a67ad4.png)

> A typical feature store is built with two key design characteristics: tooling to process large feature data sets quickly, and a way to store features that supports both low-latency access (for inference) and large batch access (for model training). There is also a metadata layer that simplifies documentation and versioning of different feature sets and an API that manages loading and retrieving feature data.

[![Screen Shot 2023-02-05 at 9 53 32 PM](https://proxy-prod.omnivore-image-cache.app/599x0,sUz9I1pxTf_UhkX_JPl_zQEGmDGbSViBLzeogwaM5N6c/https://user-images.githubusercontent.com/3837836/216872830-e86dab42-c904-45ae-9256-e8cc723a556c.png)](https://user-images.githubusercontent.com/3837836/216872830-e86dab42-c904-45ae-9256-e8cc723a556c.png)

> Feature stores work because they decouple feature engineering from feature usage, allowing feature development and creation to occur independently from the consumption of features during model development. As features are added to the feature store, they become available immediately for both training and serving and are stored in a single location. This ensures consistency between model training and serving.

[![Screen Shot 2023-02-05 at 9 54 01 PM](https://proxy-prod.omnivore-image-cache.app/606x0,ssSVHb135pzyB8OlaUzzkbXYm6sJz0b2zbgfcmGybHIA/https://user-images.githubusercontent.com/3837836/216872891-37a12309-5a6b-4097-ad04-293d5ac6aeb0.png)](https://user-images.githubusercontent.com/3837836/216872891-37a12309-5a6b-4097-ad04-293d5ac6aeb0.png)

### Continued Model Evaluation

How do you know a model is no longer good enough, when you need to update it? You may get data and concept drift.

> The most direct way to identify model deterioration is to continuously monitor your model’s predictive performance over time, and assess that performance with the same evaluation metrics you used during development. This kind of continuous model evaluation and monitoring is how we determine whether the model, or any changes we’ve made to the model, are working as they should.

> It is also necessary to capture the ground truth for each of the instances sent to the model for prediction. This can be done in a number of ways depending on the use case and data availability. One approach would be to use a human labeling service—all instances sent to the model for prediction, or maybe just the ones for which the model has marginal confidence, are sent out for human annotation. Most cloud providers offer some form of a human labeling service to enable labeling instances at scale in this way.

> When developing machine learning models, there is an implicit assumption that the train, validation, and test data come from the same distribution, as shown in Figure 5-4\. When we deploy models to production, this assumption implies that future data will be similar to past data. However, once the model is in production “in the wild,” this static assumption on the data may no longer be valid. In fact, many production ML systems encounter rapidly changing, nonstationary data, and models become stale over time, which negatively impacts the quality of predictions.


