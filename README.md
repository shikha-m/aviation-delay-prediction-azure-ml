# aviation-delay-prediction-azure-ml
End-to-end predictive system for aviation delays using 5.8M records and Weighted MLP on Azure ML.
# Aviation Delay Prediction: Scaling Neural Solutions on Azure ML

## **Executive Summary**
This repository documents the development of an end-to-end predictive system for aviation delays using a dataset of **5.8 million records**. The project is designed to solve the "Recall Crisis"—a common failure in logistics where standard models fail to predict minority-class delays. By transitioning from **Stochastic Gradient Descent (SGD)** and **Random Forest** baselines to a **Weighted Multi-Layer Perceptron (MLP)**, the system achieves a 10x improvement in recall for operational delay detection.

## **Systems Architecture**
The project is built on a **checkpoint-driven, modular design**, allowing for stateless execution of individual pipeline stages via the **Azure ML Registry**.

* **Platform**: Azure Machine Learning (SDK v2)
* **Compute**: `aviation-mlp-cluster` (Dedicated Managed Compute)
* **Strategy**: Checkpoint-based execution for 5.8M row scalability.

## **The Data Pipeline (Three-Tier Approach)**
1.  **Split Stage**: Implements a stratified 80/20 split with a strict "firewall" to eliminate data leakage.
2.  **Sanitization Stage**: Employs a stateful **AviationDataImputer** that fits strictly on training data to resolve null "poison."
3.  **Transformation Stage**: Projects temporal cycles via Sine/Cosine encoding and manages high-cardinality noise through Smoothed Target Encoding.

## **Experimentation & Results**
* **Stage 4: Baseline Modeling**: Established performance floors using **SGD** and **Random Forest**. While accurate, these models suffered from a **0.06 Recall**, failing to identify the majority of flight delays.
* **Stage 5: Neural Modeling**: Transitioned to a **Weighted MLP** architecture to capture non-linear interactions and penalize missed delays.
* **Final Outcome**: Achieved a **0.65 Recall**, providing an operationally viable model for high-fidelity logistics forecasting.

## **Project Structure**
* **0. Configuration & Utilities**: Single-source-of-truth parameters and Azure ML connectivity functions.
* **1-3. Pipeline Stages**: Sequential execution from raw data ingestion to feature engineering.
* **4. Baseline Experiments**: Comparative analysis of traditional machine learning models.
* **5. Neural Architecture**: Development and optimization of the final Weighted MLP.
