# Using sparse autoencoders for LLM interpretation on AWS

## Introduction

Explainability for ML models can be broadly grouped into three tiers.

- Traditional ML (e.g., xgboost or linear regression). Explainability is fairly easy, and often inherent in the model's design. Tree-based models like xgboost, for example, can literally draw decision trees showing what the model learned about split points.
- Neural networks (e.g., fully-connected networks, CNNs, NLP) cannot be directly interpreted. They contain thousands to millions of parameters that interact in a long series of math operations. However, a series of explainability techniques like SHAP have evolved to help with explainability. Many of these techniques are based on game theory, and help understand how a feature contributes to a model's output. This can be done for individual predictions or for an entire test set. 
- LLMs do not have a standard explainability technique. These models are orders of magnitude larger, and their outputs are potentially long and complex series of tokens, rather than specific predictions.

This [paper](https://arxiv.org/abs/2405.00208) is a good summary of active research into LLM explainability. It includes both open-source tools, and describes some of the more advanced work done by Anthropic. 

Sparse autoencoders (SAEs) are one of the most promising directions in LLM interpretation. An SAE is a model of the information that an LLM has learned, consisting of many small features, like a feature representing concepts about specific types of pets. At the higher layers of the model, these features can represent more abstract concepts like time travel. There's new research into constructing circuits of features that act together.

## Examples

[SAELens](https://jbloomaus.github.io/SAELens/) is an open-source library that makes it easier to start building and using SAEs. This repository has four notebooks that show how to use some of the features of SAELens. The first two are mostly just reproducing existing tutorials, while the latter two show how to use AWS services to train and interpret a new SAE.

* `feature-search-gemma` shows how to find the features that are activating during a specific prompt. This emulates the feature search from [Neuronpedia](https://www.neuronpedia.org/gemma-2-2b/?sourceSet=gemmascope-res-16k&selectedLayers=[]&sortIndexes=[]&ignoreBos=true&q=I%20hate%20cats%0A). 
* `steering.ipynb` shows how to steer a model by weighting a specific feature more heavily. This is similar to Anthropic's famous Golden Gate Bridge example.
* `sae-train-qwen.ipynb` shows how to train a new SAE for a model that isn't available in SAELens yet.
* `feature-search-qwen.ipynb` shows how to identify features activated by a specific prompt using our custom SAE for the Qwen 1.5B model, and then try to describe what those features do. (In this case we don't have a canned set of feature descriptions available from Neuronpedia.)

## Citations

This work relies heavily on two open-source projects.

### SAELens

    @misc{bloom2024saetrainingcodebase,
       title = {SAELens},
       author = {Joseph Bloom, Curt Tigges and David Chanin},
       year = {2024},
       howpublished = {\url{https://github.com/jbloomAus/SAELens}},
    }}

### TransformerLens

    @misc{nanda2022transformerlens,
        title = {TransformerLens},
        author = {Neel Nanda and Joseph Bloom},
        year = {2022},
        howpublished = {\url{https://github.com/TransformerLensOrg/TransformerLens}},
    }


## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.

