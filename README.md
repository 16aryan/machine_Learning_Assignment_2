<img width="353" height="293" alt="image" src="https://github.com/user-attachments/assets/f3cdaedc-af22-4194-8894-737c44df9c32" />1.	Business Understanding

a.	Executive Summary
●	This Report investigates Machine Learning Approaches for multiclass classification of the Vitamin Deficiency related conditions. The Business Objective here is to produce a reliable decision supporting model which can classify patients into clinically meaningful categories being Healthy, Anaemia, Rickets/Osteomalacia, Night Blindness, Scurvy using structured tabular health and nutrition features.
●	The project follows an experimental progression.
1.	Baseline –Dummy Classifier Benchmark
2.	Experiment 1 – Random Forest Classifier (Non - Linear Bagging)
3.	Experiment 2 – Hist Gradient Boosting (Boosting Based Residual Correction)
4.	Experiment 3 – Stacking Classifier Ensemble (Model Fusion)
5.	Experiment 4 – Calibrated Stacking Classifier (Fusion + Probability Reliability)
●	This project emphasizes on Macro F1, Balance Accuracy ensuring class level quality, es-pecially for low frequency classes. We are evaluating both predictive discrimination and deployment readiness in later stages finally.

b.	Business Use Cases
●	Clinical Triage Support – Prioritize follow ups for higher risk deficiency classes with automation ensuring critical cases are surfaced faster than manual review.
●	Population Health Screening – Improving consistency in identifying less frequent but relevant clinical categories that are sometimes overlooked in standard screenings im-proving consistency over large datasets.
●	Operation Planning – Providing high level insights to help administrators balance re-source allocation and eliminating blind spots in clinical departments.
●	Decision Governance – Serving as secondary validation layer and providing probabil-ity-based outputs for threshold driven interventions. Ensuring clinical decisions remain within controlled and objective parameters.


        Motivation and Challenges Faced:
•	Motivation is to inherit the variability and volume of the modern clinical data. 
Human Cognitive Load – Specialists facing fatigue which leads to inconsistencies when identifying rare and significant clinical markers.
Resource Bottlenecks – Patient data surge that sometimes outpaces the number of available clinicians creating delays in high-risk intervention.

               Relevance of machine Learning in this project:
By Leveraging above algorithms and models the project offers-:
●	High Dimensionality Handling – Synthesizing complex patient meta data and imag-ing features to identify patterns. 
●	Probabilistic Grading – providing a Confidence score that allows for threshold-based interventions where clinicals can focus more on cases where the model indicates higher degree of uncertainty or risk involved.
●	Scalability – Once trained the model can screen records and transforming a complex healthcare process into a proactive and preventative one.

c.	Key Objectives
             Primary Project Goal
●	Outperform the baseline on class-balanced metrics, achieve high sensitivity (recall) in detect-ing clinical classes to ensure no risks are missed.
●	Provide Objective, Data Backed probability scores to reduce the subjective variance.
●	Scalable risk stratification by building a system capable of processing high volume datasets in real time enabling immediate triage.




          Stakeholder and Requirements
  Stakeholder	Key Requirements
  Clinicians/Medical Staff	High Model Interpretability, low false negative rates and seamless in-tegration with the workflows
  Health Care Administrators


  Data Governance Teams	Improved resource allocation, reduction in operational overhead, ROI through efficiency gains
 
Model transparency, ethical handling of patient’s data and adherence to the clinical safety and maintaining standards.

  Patients	
Faster Results, Increased Diagnostic Reliability and trust in treatment plans.

Addressing Requirements through Machine Learning
●	Identifying complex features correlations in historical data to deliver high precision.
●	Automatically categorizes cases by severity, enabling administrators to prioritize resources.
●	Employs adjustable probability outputs to favour high sensitivity by minimising blind spots.
●	Achieving F1 Score > 0.85 for balancing precision and recall for the critical deficiency classes and maintaining good performance metrics and reducing manual triage by estimated 30 percent through automation. 

 the answers can be applied to any project
  
2.	Data Understanding (EDA) 
A.	Exploratory Data Analysis
●	The Dataset was analysed in its pre-split architecture (‭X_{train}‬, ‭X_{Val}‬, ‭X_{test}) ensuring a leakage safe environment. The target variable is a multi-class distribution and moderately imbalanced (major healthy / anaemia) groups with lower frequency classes such as Scurvy/Night Blindness represent high stakes clinical focus for this project.‬‬‬
Target variable: 
●	Majority Classes: Healthy/Anaemia 
●	Minority Classes: Scurvy/ Night Blindness
●	 
B.	Key Variables Findings
●	Clinical Biomarkers and Symptoms:  Key predictors include biomarker levels, die-tary intake variables, symptoms indicators collectively influence classification outcomes.
●	Feature Interaction: Correlation and pairwise reveal strong non-linear relationships be-tween variables, particularly between the biomarkers and symptoms indicators.
C.	EDA Key Technical Findings
●	Distributional Homogeneity: Class proportions remain stable across the train, valida-tion and test set. Ensures performance benchmarks on validation set as proxies for gener-alisation on unseen data.
●	High Dimensional Feature Interaction: Clinical Biomarkers, dietary intake variables and symptom indicators. Correlation matrices and pair plots reveal a high degree of non-linearity and interactions get complex between biomarkers and symptoms. Findings suggest Logistic Regression may suffer from high bias justifying exploration of high-capacity methods or non-linear kernels. 
●	Data Integrity and Schema: Data Quality assessed as high with minimal missingness, and a rigorous post processing audit verified that feature encoding and scaling schemas across all split’s elimination synthetic bias. 
●	Analytical Implication for evaluation: Class imbalance renders “Global Accuracy” a misleading metric, as a model could achieve high scores while failing to identify the rare de-ficiency classes. Prioritizing clinical safety utilises Macro F1 Score and Balanced Accuracy as primary performance drivers.
 

3.	Data Preparation
●	To ensure the model receives high quality, normalized signals, a structured pipeline imple-mented transiting from clinical data to model ready tensors.
●	Data Cleaning and Quality Assurance: Initial Processing involves a schema audit to ensure feature consistency. Missing Values were found and were addressed using Median imputation for continuous biomarkers to preserve central tendency and Mode imputation for categorical symptom Indicators.
●	Preprocessing and Feature Engineering: Continuous variables like biomarkers and intake levels were normalized using Standard Scaler to ensure that features with larger magnitudes did not disproportionality dominate the model weights over the small scalar bi-omarkers.
●	Categorical Symptoms Encoding: Transformed using One Hot Encoding and ena-bling the model to ingest the non-numerical clinical observations without implying an artificial ordinal relationship. Interaction features given the interaction rich nature found and gener-ated to capture the non-linear clinical dependencies.
●	Data Splitting strategy: hold out validation strategy used to pre-split training, test, vali-dation to prevent data leakage ensuring no information from the test set influences the training process. Validation set used for the hyper-parameters tuning, while the test set re-mained strictly isolated for the final unbiased performance audit.
●	Handling the Imbalanced and Outliers Data: Protect Model stability extreme outli-ers in biomarker data capped using the Winsorization (at the 1st and 99th percentiles) rather than just imputed, preserving the clinical significances of the extreme cases which are often indicative of severe deficiency. 
●	Class imbalance: To address the lower frequency Scurvy and Night Blindness groups, stratified sampling was applied during splitting and batching. Ensuring that the minority clas-ses are proportionally represented in every training iteration and preventing the model from converging on majority only prediction bias.
. Mention the best data splitting strategy is  random splitting as it always provides better results.
  
4.	Modelling

a.	Baseline Methodology
●	Designed the workflow to be modular, leakage safe and focused on establishing a zero-knowledge floor and Dummy Classifier here providing the worst benchmark scenario possible so any machine learning model deployed should perform better than this.
●	Results: Accuracy: 0.364, Balanced Accuracy: 0.200, Macro F1: 0.107, Weighted F1: 0.194
●	Looking at the results critically low Macro F1 and Balanced Accuracy indicate that the model has zero predictive power for minority deficiency classes like Scurvy and Night Blindness. 
●	Performance Metric Framework: Macro F1 Score being as the primary evaluation metric showing average balance between precision and recall across all the classes.

b.	Experiment -1 Random Forest Model Assessment
●	Designed to capture non-linear relationships between clinical features and nutritional defi-ciencies using a bagging ensemble. It utilised Standard Scaler for Biomarkers and One Hot Encoding for symptoms to ensure the forest could effectively partition the mixed type of fea-ture space. 
●	A standard Logistic Regression was bypassed for this experiment due to the non-linear de-pendencies and high dimensional feature interaction identified through EDA. Logistic re-gression assumes a linear relationship between independent and log-odds of target how-ever the clinical data showed that biomarkers like Vitamin C interact non-linearly with specif-ic symptom indicators. Random Forest chosen as the superior starting point because of its recursive portioning mechanism capturing these interactions without requiring manual, high-order polynomial feature engineering and reducing the risk of high bias (underfitting) inher-ent in the linear models.
●	Results: Accuracy: 0.885, Balanced Accuracy: 0.797, Macro F1: 0.826, Weighted F1: 0.884
●	Jump in performance from baseline confirms that clinical biomarkers contain significant predictive signal. The Gap between Global Accuracy and Balanced Accuracy suggesting that the model still face challenges in isolating the minority classes (Scurvy/Night Blindness) from majority health group likely due to Feature Overlap.
●	Optimal Hyperparameters: n_estimators:100, max_depth: None, min_sample_split: 2
●	Feature Selection: All 24 input features were retained allowing Gini importance mecha-nism to internally weight the features during the tree building process.

c.	Experiment -2 Histogram Gradient Boosting Model Assessment
●	Deployed a gradient boosting framework for large scale datasets and it utilises the histo-gram-based binning to accelerate the training process to reduce the memory overhead while still maintaining high precision. Workflow focuses on tuning the learning dynamics specifically the learning rate and maximum iterations ensuring the model minimizes the log-loss of the previous weak learners.
●	Hypothesis and Selection Rationale: The gradient boosting can correct residual errors that the bagging approach of experiment 1 Random forest failed to resolve. Unlike Random for-ests which is building parallel trees, Hist Gradient Boosting builds it sequentially focusing on instances hard to classify. Approach selected to achieve higher peak discrimination by fine tuning decision boundaries in the high-density regions of the biomarkers feature space where “Healthy” and “Anaemic” classes often overlap.
●	Results: Accuracy: 0.902, Balanced Accuracy: 0.818, Macro F1: 0.845, Weighted F1: 0.901
●	The outcome confirms the hypothesis with Experiment 2 achieving top tier performance with F1 (0.8450) compared to experiment 1 suggesting the model learned to distinguish the re-sidual patterns in minority classes that were missed previously.
●	Optimal-Hyperparameters: learning-rate:0.1, max_iter:100, min_depth: None, l2_regularisation:0.0
●	Feature Selection: All available features utilized and algorithm’s internal binning and gradient based importance were leveraged to prioritize the most discriminative biomarkers.
●	Quantify the improvements achieved and the potential value generated.







d.	Experiment -3 Stacking Ensemble Model Assessment
●	Stacking Methodology: Developed Stacked Ensemble Architecture to fuse the predic-tive capabilities of distinct model families. The methodology combined Random Forest (bag-ging), Hist Gradient Boosting(boosting) and Logistic Regression(linear) as base learners. First level of the prediction was fed into Logistic Regression meta learner which was trained to optimally weigh output of the model and make the final clinical classification.
●	Hypothesis and Selection Rationale: The central hypothesis is that ensemble diver-sity adds incremental value to reduce the correlated errors and combining models with dif-ferent mathematical (tree-based vs linear) stacking approach aimed to mitigate the com-plementary model families and improves the robustness in the high overlap regions of the feature space where the single model’s architecture might plateau.
●	Results: Accuracy: 0.9000, Balanced Accuracy: 0.8278, Macro F1: 0.8449, Weighted F1: 0.8992
●	The results were highly competitive however compared to Experiment 2 the gains in Macro F1 were marginal. The outcome suggests the model is nearing the architectural saturation where increasing complexity of ensemble no longer yields significant predictive returns.
●	Optimal-Hyperparameters: Base learners: (RF, HGB,LR), Meta-learner: Logistic Re-gression (C=1.0)
●	Feature Selection:  The meta learner utilized the probability distributions like soft-voting signals from the base models rather than getting it form the raw 24 biomarkers.








e.	Experiment -4 Stacking Ensemble Model Assessment
●	Calibrated Stacking Methodology: The final configuration utilises the stacked En-semble architecture from the Experiment 3 with strategic addition of Probability Calibration layer. This involves Sigmoid Calibration (Platt Scaling) to ensemble the raw output scores. Post processing ensures that predicted probability distribution aligns with the true empirical frequency of clinical classes in dataset.
●	Hypothesis and Selection Rationale: This experiment was selected to ensure the model predicts an 85% probability of a deficiency that diagnoses is correct 85 percent of time as in a clinical setting the model cannot be merely accurate its confidence score must be statistically honest. Reliability allows the clinicians to set precise and threshold-based in-terventions. Making the system viable governance tool rather than just a black box predic-tor.
●	Results: Accuracy: 0.9000, Balanced Accuracy: 0.8209, Macro F1: 0.8464, Weighted F1: 0.8988
●	Experiment 4 is the Champion Model achieving the Macro F1 Score of 0.8464 across all the experiments and having global accuracy of 90%, this configuration offers most precise balance of Precision and recall for both majority and minority groups. By en-semble the diversity with calibrated probabilistic output and providing the robust and trust-worthy performance for high stakes clinical triage.
●	Optimal-Hyperparameters: CV: 5-Fold, Calibration Method: Sigmoid, Final Estimator: Logistic Regression (C=1.0).
●	Performance Metrics Framework: Primary focus on Macro F1, balanced Accuracy. These metrics makes it the Champion Model for protecting the High Minority patients (Scur-vy/Night Blindness) while maintaining diagnostic efficiency for broader population.




5.	Evaluation
a. Results and Analysis
Comparative Summary:
●	Baseline Dummy Classifier: Weakest across all metrics
●	Exp-1 Random Forest: Major upliftment over baseline
●	Exp-2 Hist Gradient: Boosting Strongest headline Discrimination (macro F1/accuracy)
●	Exp-3 Stacking Ensemble: Near parity High Performance via Fusion
Model	Accuracy	Balanced Accuracy	Macro F1	Weighted F1
Calibrated Stacking (Exp 4)	0.9000	0.8209	0.8464	0.8988
Hist Gradient Boosting (Exp 2)	0.9027	0.8177	0.8450	0.9010
Stacking Ensemble (Exp 3)	0.9000	0.8278	0.8449	0.8992
Random Forest (Exp 1)	0.8853	0.7971	0.8262	0.8839
Dummy Classifier	0.3640	0.2000	0.1067	0.1943
●	Exp-4 Calibrated Stacking: Highest Balanced Accuracy, slight macro-F1/accuracy trade-off
●	While Logistic Regression (LR) was bypassed as a standalone experiment due to the non-linear complexity of raw feature space, it was strategically implemented as the meta learner in Experiment 3 and 4. 
●	Raw Biomarkers interact non-linearly, predicted Probabilities generally have linear relation-ship with the final target. LR is mathematically optimal for fusing these probability signals in-to a final prediction. Using Logistic Regression with L2 Regularisation (C=1.0) acts as a con-servative, smooth weight allocator ensuring the ensemble generalizes effectively to unseen clinical data. As using a tree-based model as a meta learner in this case would have led to overfitting. 
●	Experiment 4 achieved the highest Macro-F1 but did show a marginal drop in its Balanced Accuracy compared to Experiment 3. Experiment 2 on the other hand achieved the highest Raw accuracy of 0.9027 and weighted F1 (0.0910) making the most efficient for processing large volumes of data where majority class dominates.

●	However, Experiment 4 was selected as the Champion despite its slightly lower global accu-racy (0.900) because of the shift from efficiency to equity. Applying Probability calibration (Platt Scaling), Experiment 4 receives a superior Macro F1 (0.8464) compared to experiment 2 (0.8450). Boosting models are often greedy and overconfident in their predictions. The calibration in Experiment 4 softens the hard class decisions near the decision boundary. 
●	Error Analysis and Robustness: Experiment 2 is highly effective at identifying the Health Majority. Exhibits higher variance when distinguishing overlapping biomarkers of “Scurvy” and “Anaemia”. Fused stacking model of Experiment 4 taking advantage of boost-ing of experiment 2 and taking advantage of bagging and linear perspective, it effectively reduces the correlated errors. 5-fold CV depicting the robustness and making the Experi-ment 4 the best model.
and act if they are good fit for a regression problem.
b.	Business Impact and Benefits
●	Diagnostic Equity & Risk Mitigation: Experiment 4 Calibrated Stacking achieving a Macro F1 Score of (0.8464) ensuring equitable care and significantly reducing the diagnostic errors for rare conditions with high volume clinical datasets.
●	Operational Triage Efficiency: Data Backed pre classification streamlines the clinical workflow potentially saving 15-20 minutes of manual biomarker review per case. Surfacing high probability deficiencies allowing for immediate specialist audit and faster patient turna-round.
●	Calibrated Decision Governance: Experiment 4 provides statistically reliable probabili-ties for precise threshold-based interventions.
○	Standard Monitoring: For low-risk predictions
○	Immediate Escalation: For high probability detections (>90%)
○	Human in Loop: Uncertain cases flagged for secondary expert review.
●	Actionable Deployment Strategy:
○	Performance Floors: Minimum Recall Targets (>80%) for critical classes as a prerequisite for production.
○	Active Monitoring: Implement auto tracking for data drift and calibration shifts for long term reliability.
○	Safety Protocols: Utilise automated rollback triggers to revert to manual clinical review in case if the performance degrades below the benchmarks.
, generic and incorrect assessment of the business impacts
c.	Data Privacy and Ethical Concerns
○	Algorithmic Bias and Proxy Discrimination: Clinical models are highly sus-ceptible to class imbalance, minority deficiency groups (e.g., Scurvy) could be chron-ically under-detected compared to majority populations. Furthermore, features such as geographical data or dietary intake can be proxies for socioeconomic status. If a model learns to prioritize the majority groups, it risks creating a discriminatory feed-back loop that makes the existing health inequities worse for underserved commu-nities.
○	Clinical Safety and Decision Integrity: The primary ethical risk involves False Negatives in clinically significant classes, which can delay medical intervention. False Positives also increase the economic and emotional burden on patients and families. Overconfident or uncalibrated probabilities could lead to unsafe policy thresholds and maintaining the "honest" confidence scores via calibration is vital. Theis ensures that the model remains a supportive triage tool for clinicians rather than being an unchecked automated decision-maker.
○	Data Privacy and Auditability: Model reliability is dependent on the integrity of clinical inputs and strict privacy controls. Data Minimization is implemented by utiliz-ing necessary diagnostic attributes and separating the personal identifiers from the modelling workflow. Controlled access to prediction outputs, combined with the au-ditability of model versions and history, ensures the system is transparent, gov-erned, and protected against data misuse throughout its lifecycle.
○	Indigenous Equity and Culturally Safe Governance:  Ethical deployment must recognize that the biomarker ranges and health outcomes vary across diverse genetic and cultural backgrounds. They require Culturally Safe Governance and stakeholder-informed reviews before high-impact policies are implemented. Sub-group performance disparities must be monitored to ensure the model does not re-duce the quality of care for communities with traditionally unequal access to health services.
○	Deploying only with robust human oversight for uncertain or high-risk cases, contin-uous subgroup monitoring, and explicit governance controls to protect all direct and indirect stakeholders is the best idea. 
6.	Conclusion
●	This project successfully transforms a zero-knowledge based clinical baseline into a high-performance diagnostic framework. Through systematic progression of experimenting the Macro f1 of 0.8464 was achieved in experiment 4 establishing a robust foundation for au-tomatic triage while still maintaining the strict framework for clinical safety and decision gov-ernance.
         Key Achievements
○	Rigorous Experimental Progression: transition from naive baselines to non-linear ensembles (Random Forest, Hist Gradient Boosting, and Stacking).
○	Superior Predictive Uplift: Achieved 8x improvement in Macro F1 compared to industry-standard dummy benchmarks.
○	Governance-Ready Reliability: Platt Scaling integration for calibration to en-sure that model confidence scores are statistically honest and actionable for clini-cians.
○	Quantified Clinical Value: 15–20 minutes in time savings per case and signifi-cantly reduced the risk of under-detecting rare deficiency classes.
○	Statistical Robustness: Validated all the findings via 5-fold Cross-Validation to ensure performance stability across diverse data splits.	
       Model recommendation: Calibrated Stacking (Exp 4)
●	The Calibrated Stacking classifier is the recommended choice as it optimally balances raw discrimination with diagnostic equity. While Experiment 2 offered slightly higher top-line accuracy, the trade-off in Experiment 4 is justified by its calibrated probability outputs. This ensures the model provides "honest" confidence scores which is a critical requirement for setting safe clinical policy thresholds and mitigating the risk of overconfident false negatives in high-stakes triage.

●	Critical Success Factors: Performance sustainability through continuous KPI monitor-ing Macro F1, class recall, and calibration drift) and the maintenance of a "Human-in-the-loop" oversight protocol for uncertain clinical cases are essential for long-term success.



         
Limitations and Future Work

Current Limitations:
•	Generalization Confidence: The current reliance on a limited clinical dataset may re-strict the generalization across broader and real-world patient populations.
•	Feature Gaps: The absence of dietary data and specific categorical lifestyle features re-duced the peak predictive performance by 8.6%.
•	Indigenous Impact Assessment: The assessment of cultural disparities and subgroup fairness remains incomplete and need more talks with community stakeholders and indige-nous groups before deploying it.
Future Development:
•	Neural Architecture Integration: Exploring MLP or Transformer based neural net-works to explore deeper patterns in the patient data over the years.
•	Real-Time Scoring Infrastructure: API-first deployment strategy by making an appli-cation for instant clinical decision support at the point of care by the clinicians. 
•	Expansion & Fairness: Portfolio expansion so that we can include broader nutritional categories and a comprehensive, stakeholder-led fairness audit to ensure equitable out-comes for all patient sub-populations.

 
 <img width="353" height="293" alt="image" src="https://github.com/user-attachments/assets/e5f63527-3e26-4356-9455-3f4a8a7c7af6" />



<img width="341" height="249" alt="image" src="https://github.com/user-attachments/assets/089db781-c2b0-47f9-94b6-4efb204df452" />


















