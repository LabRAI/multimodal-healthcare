# Safety, Socioeconomic, and Ethical Risks of Multimodal AI in Healthcare


> **Scope**: This document focuses on risks arising from the deployment of multimodal AI models — particularly Medical Large Vision-Language Models (Med-LVLMs) — in clinical and healthcare settings. For each major risk category, at least four specific sub-risks are identified, each illustrated with a concrete real-world or literature-grounded example, followed by representative papers and their research angles.

---

## Table of Contents

1. [Clinical Safety Risks](#1-clinical-safety-risks)
2. [Privacy & Cybersecurity Risks](#2-privacy--cybersecurity-risks)
3. [Algorithmic Bias & Health Equity Risks](#3-algorithmic-bias--health-equity-risks)
4. [Multimodal-Specific Adversarial & Reasoning Safety](#4-multimodal-specific-adversarial--reasoning-safety)
5. [Ethics & Liability Risks](#5-ethics--liability-risks)
6. [Socioeconomic Impact Risks](#6-socioeconomic-impact-risks)

---

## 1. Clinical Safety Risks

**Core Problem**: Multimodal models in clinical settings generate inaccurate, unreliable, or harmful medical information that directly threatens patient safety.

---

### 1.1 Hallucination and Misdiagnosis

**Description**: Models generate plausible-sounding but factually incorrect medical information — fabricating findings, producing erroneous diagnoses, or confabulating non-existent references.

**Case Example**: The MedVH benchmark revealed that medical-domain fine-tuned LVLMs (e.g., LLaVA-Med, Med-Flamingo) perform *worse* on hallucination tasks than general-purpose models (e.g., GPT-4V) — a striking "fine-tuning paradox" where domain specialization increases susceptibility to hallucination in chest X-ray VQA and report generation tasks.

**Key Papers**:
- **MedVH: Toward Systematic Evaluation of Hallucination for Large Vision Language Models in the Medical Context** (Gu et al., 2024) — Constructs a six-task hallucination evaluation framework (MedVH), systematically quantifying hallucination tendencies across Medical and general LVLMs; reveals the fine-tuning–hallucination tradeoff.
- **Can We Trust AI Doctors? A Survey of Medical Hallucination in LLMs and LVLMs** (Zhu et al., ACL 2025) — Taxonomizes medical hallucinations as consistency (misdiagnosis) and completeness (missed diagnosis) types; surveys mitigation strategies across 100+ papers.
- **CARES: A Comprehensive Benchmark of Trustworthiness in Medical Vision Language Models** (Xia et al., NeurIPS 2024) — Evaluates Med-LVLMs across five trust dimensions (truthfulness, fairness, safety, privacy, robustness) over 41K QA pairs and 16 imaging modalities.
- **Medical Hallucination in Foundation Models and Their Impact on Healthcare** (Survey, 2025) — Classifies hallucination types (input-conflicting, outdated reference, spurious correlation, fabricated sources); validated by a global clinician survey (n=70) finding 91.8% had encountered medical hallucinations.
- **Hallucination Benchmark in Medical Visual Question Answering** (Wu et al., ICLR 2024) — Dedicated benchmark for hallucination patterns in medical VQA tasks.

---

### 1.2 Unreliable Clinical Decision Support

**Description**: Models exhibit systematic vulnerability to erroneous embedded information, amplifying clinical errors under realistic conditions rather than flagging inconsistencies.

**Case Example**: A study in *Communications Medicine* (Omar et al., 2025) embedded single deliberate errors (false lab values, signs, or diagnoses) into 300 clinician-designed vignettes and tested six leading LLMs. Models repeated or elaborated on the planted error in **up to 83%** of cases; a mitigation prompt reduced this to ~41% — still clinically unacceptable.

**Key Papers**:
- **Multi-model Assurance Analysis: LLMs Are Highly Vulnerable to Adversarial Hallucination Attacks During Clinical Decision Support** (Omar et al., *Communications Medicine*, 2025) — Quantifies LLM susceptibility to clinician-planted errors (83% propagation rate) in 300 structured clinical vignettes across six leading models.
- **GPT-4V(ision) Unsuitable for Clinical Care and Education** (Bedi et al., 2024) — Clinician-led assessment of GPT-4V outputs across real clinical cases; concludes current multimodal models are not fit for clinical deployment.
- **First, Do NOHARM: Towards Clinically Safe Large Language Models** (2024) — Introduces the NOHARM framework to evaluate frequency and pattern of harmful option generation in LLM medical advice.
- **A Framework to Assess Clinical Safety and Hallucination Rates of LLMs for Medical Text Summarisation** (*npj Digital Medicine*, 2025) — Derives clinical error metrics from 12,999 clinician-annotated sentences; finds 1.47% hallucination rate and 3.45% omission rate with omissions posing greater clinical danger.

---

### 1.3 Visual-Language Cross-Modal Misinterpretation

**Description**: Models fail to correctly integrate imaging information with textual context, producing outputs that contradict the visual content — or answering correctly without genuinely perceiving the image.

**Case Example**: *MediConfusion* specifically tests cases where clinicians expect easy correct diagnoses. Mainstream Med-VLMs are shown to produce misleading diagnostic conclusions on exactly these "obviously correct" cases — revealing a fundamental failure in cross-modal clinical reasoning, not merely a knowledge gap.

**Key Papers**:
- **MediConfusion: Can You Trust Your AI Radiologist? Probing the Reliability of Multimodal Medical Foundation Models** (2024) — Designs a confusion test set targeting cases clinicians identify as unambiguous; reveals systematic failures in seemingly straightforward visual diagnostic tasks.
- **Beyond the Hype: A Dispassionate Look at Vision-Language Models in Medical Scenarios** (Nan et al., 2024) — Multi-dimensional objective evaluation of VLMs' medical capabilities; finds fundamental limitations in visual perception layer, not only knowledge.
- **An Embarrassingly Simple Probing Evaluation of Large Multimodal Models in Medical VQA** (Yan et al., 2024) — Shows via image-swapping probes that many Med-LVLMs answer correctly without genuinely processing the image, relying instead on text-only biases.
- **Detecting and Evaluating Medical Hallucinations in Large Vision Language Models** (Chen et al., 2023) — One of the earliest systematic investigations into hallucination detection methods for medical LVLMs; establishes methodological foundations for image hallucination evaluation.

---

### 1.4 Outdated Medical Knowledge and Knowledge Cutoff Risks

**Description**: Medical evidence and clinical guidelines evolve rapidly, but models have training cutoffs. They may cite retracted studies, apply superseded guidelines, or recommend outdated dosing regimens with real patient harm potential.

**Case Example**: Research on warfarin dosing AI demonstrates that models trained without sufficient representation of African-American genetic variants (e.g., *CYP2C9* alleles) systematically recommend overdoses for this population — a form of "outdated knowledge" that intersects with bias, causing direct pharmacological harm.

**Key Papers**:
- **Medical Hallucination in Foundation Models** (Survey, 2025) — Explicitly classifies "Outdated Reference Hallucination" as a major hallucination subtype where models rely on obsolete guidelines or retracted literature.
- **Safety Challenges of AI in Medicine in the Era of Large Language Models** (Multi-institution, 2024) — Jointly published by leading academic institutions; identifies knowledge cutoff risk as a core safety challenge with specific implications for rapidly evolving therapeutic areas.
- **The Clinicians' Guide to Large Language Models: A General Perspective With a Focus on Hallucinations** (*IJMR*, 2025) — Practical guide for clinicians covering knowledge-temporality as a root cause of hallucinations and its cascade effects on clinical reasoning.
- **MedHalu: Hallucinations in Responses to Healthcare Queries by Large Language Models** (Agarwal et al., 2024) — Evaluates hallucination type distribution in real patient healthcare queries; finds outdated knowledge a substantial contributor to error.

---

### 1.5 Over-reliance and the Halo Effect

**Description**: Clinicians and patients over-trust AI outputs, suppressing independent judgment — even when outputs are wrong. "Automation bias" means AI errors go unchallenged, and the AI's confident tone amplifies unwarranted trust.

**Case Example**: A systematic review of LLMs in mental health care (*PMC*, 2025) identifies the "halo effect" as a primary risk: users systematically overestimate AI output accuracy. Critically, even when LLMs explicitly recommend consulting a human professional, only ~50% of users comply — undermining safety net recommendations.

**Key Papers**:
- **"It's Not Only Attention We Need": Systematic Review of LLMs in Mental Health Care** (*PMC*, 2025) — Quantifies halo effect prevalence in 55 mental health AI studies; links it to delayed treatment-seeking and erosion of therapeutic relationships.
- **Rapid Integration of LLMs in Healthcare Raises Ethical Concerns: Deceptive Patterns in Social Robots** (2024) — Examines deceptive trust-formation patterns when LLMs are embedded in medical social robots; analyzes the mechanics of automation bias induction.
- **Safety Challenges of AI in Medicine in the Era of LLMs** (Multi-institution, 2024) — Lists automation bias as a core safety challenge; discusses the tension between AI-enhanced clinical efficiency and erosion of independent reasoning.
- **Towards Safe AI Clinicians: A Comprehensive Study on LLM Jailbreaking in Healthcare** (2024) — Notes that over-reliance on AI clinical advice constitutes a safety hazard even in the absence of adversarial attacks.

---

## 2. Privacy & Cybersecurity Risks

**Core Problem**: Medical multimodal models handle highly sensitive patient data, facing end-to-end privacy and security threats from training through deployment.

---

### 2.1 Patient Data Leakage and Membership Inference Attacks

**Description**: Models may memorize and reproduce patient data from training sets. Membership inference attacks can determine whether a specific patient's data was used for training, enabling sensitive health information inference without direct data access.

**Case Example**: Models trained on MIMIC-CXR and similar large medical datasets have been shown — via black-box API access — to inadvertently reproduce specific patient image-report pairs, violating HIPAA protections. The attack requires no internal model access, only query access to the deployed API.

**Key Papers**:
- **SoK: Privacy-aware LLM in Healthcare: Threat Model, Privacy Techniques, Challenges and Recommendations** (2024) — Systematically maps medical LLM privacy threat models (membership inference, model inversion, attribute inference); surveys defensive techniques and remaining challenges.
- **Medical Multimodal Model Stealing Attacks via Adversarial Domain Alignment (ADA-Steal)** (2025) — Demonstrates the first model-stealing attack against medical MLLMs using only natural images, enabling model replication without any medical data access; raises IP and privacy dual risks.
- **Data Poisoning Vulnerabilities Across Health Care AI** (*JMIR*, 2026) — Comprehensive threat analysis synthesizing 41 security studies; addresses privacy exposure in federated learning deployments.
- **Robustness in Deep Learning Models for Medical Diagnostics** (*AI Review*, 2024) — Surveys privacy attack types (membership inference, model inversion, attribute inference) in medical deep learning, covering theoretical foundations and practical threat surfaces.

---

### 2.2 Prompt Injection Attacks

**Description**: Attackers embed malicious instructions inside medical inputs (DICOM metadata, patient record text fields, report annotations) to hijack model behavior — redirecting it to leak information or generate dangerous medical recommendations, entirely invisible to clinicians.

**Case Example**: Researchers conducted real-world prompt injection experiments on a VLM-assisted oncology system. Malicious instructions were embedded in DICOM metadata fields. When the model processed the image, the hidden instructions activated, causing it to alter its diagnostic recommendation and transmit patient names and clinical summaries to an external address — completely undetected by clinical staff.

**Key Papers**:
- **Prompt Injection Attacks on Large Language Models in Oncology** (2024) — First systematic demonstration of prompt injection in clinical oncology AI; shows attacks can be delivered via imaging metadata channels with information leakage and diagnostic manipulation outcomes.
- **Emerging Cyber Attack Risks of Medical AI Agents** (2024) — Analyzes novel attack surfaces for medical AI agents (agentic systems); classifies prompt injection as the highest-severity attack vector due to its invisibility and clinical consequence.
- **How to Make Medical AI Systems Safer? (MedThreatRAG)** (2025) — Proposes a multimodal poisoning framework for RAG-augmented medical systems; demonstrates cross-modal conflict injection can destabilize retrieval and generation without model access.
- **A Practical Framework for Evaluating Medical AI Security** (2024) — Builds a medical AI security evaluation framework classifying prompt injection alongside jailbreaking as top-tier vulnerabilities; proposes layered defense strategies.

---

### 2.3 Adversarial Example Attacks on Medical Imaging

**Description**: Imperceptibly perturbed medical images fool AI into producing grossly incorrect diagnoses — changes invisible to radiologists can reduce diagnostic accuracy from 95% to near zero.

**Case Example**: A landmark paper in *Science* (Finlayson et al., 2019) added pixel-level perturbations to chest X-rays, causing AI to diagnose pneumonia-positive cases as normal with high confidence. Detection accuracy dropped from 95% to near 0% — with the perturbed images appearing indistinguishable from originals to board-certified radiologists. The paper also outlined realistic attacker motivations (e.g., insurance fraud).

**Key Papers**:
- **Adversarial Attacks on Medical Machine Learning** (Finlayson et al., *Science*, 2019) — Landmark paper systematically demonstrating medical ML vulnerability to adversarial examples; outlines realistic adversary motivations in healthcare settings (insurance fraud, malpractice).
- **Assessing the Adversarial Robustness of Multimodal Medical AI Systems** (*Frontiers in Medicine*, 2025) — Compares single-modality vs. multimodal medical model robustness; finds multimodal fusion improves robustness but introduces novel attack surfaces.
- **Medical LLMs Are Susceptible to Targeted Misinformation Attacks** (*npj Digital Medicine*, 2024) — Shows that modifying only 1.1% of model weights stably injects false biomedical facts; errors propagate in outputs while other task performance is preserved.
- **Data Poisoning Vulnerabilities Across Health Care AI** (*JMIR*, 2026) — Analyzes poisoning attack feasibility across CNN, LLM, and RL architectures in healthcare; includes adversarial imaging scenarios.

---

### 2.4 Training Data Poisoning and Backdoor Attacks

**Description**: Attackers inject malicious samples during training to embed "backdoor triggers." The deployed model behaves normally on clean inputs but produces attacker-specified outputs when a specific trigger is present — potentially enabling silent, targeted medical discrimination.

**Case Example**: A *JMIR* analysis (2026) describes a technically grounded scenario: an attacker poisons training data for an organ transplant prioritization AI, causing it to systematically lower priority scores for patients with a specific demographic marker. The attack is undetectable by existing transplant oversight systems, which monitor utilization rates and aggregate outcomes — not AI system forensics.

**Key Papers**:
- **Data Poisoning Vulnerabilities Across Health Care AI** (*JMIR*, 2026) — Constructs eight technically grounded attack scenarios across healthcare AI architectures; analyzes detectability gaps in current oversight systems for backdoor attacks.
- **How to Make Medical AI Systems Safer? (MedThreatRAG)** (2025) — Demonstrates knowledge base poisoning where a single malicious image-text injection can persistently corrupt RAG-augmented model outputs without direct model access.
- **Medical LLMs Are Susceptible to Targeted Misinformation Attacks** (*npj Digital Medicine*, 2024) — Provides mechanistic understanding of weight-level injection of false medical knowledge; foundational for understanding internal poisoning pathways.
- **Emerging Cyber Attack Risks of Medical AI Agents** (2024) — Analyzes backdoor propagation in multi-agent medical systems, where a compromised sub-agent can silently spread poisoned outputs through an entire clinical workflow.

---

## 3. Algorithmic Bias & Health Equity Risks

**Core Problem**: Medical multimodal models learn and amplify social biases from historical data, producing systematic diagnostic disparities that harm marginalized populations and deepen healthcare inequality.

---

### 3.1 Racial and Skin Tone Bias

**Description**: Training data severely underrepresents dark skin tones; models perform substantially worse for dermatological, pathological, and imaging tasks on darker-skinned patients, causing missed cancers and delayed diagnoses.

**Case Example**: Oxford researchers (Wen et al., *Lancet Digital Health*) examined 21 open-access skin cancer AI datasets comprising 106,950 images. Only 2,436 recorded skin type; among these, just **10 images** were from people with brown skin and **1** from dark/black skin. Researchers warned this means widely deployed AI may cause "avoidable surgery, missed treatable cancers, and unnecessary anxiety" for patients with dark skin.

**Key Papers**:
- **Are Generative Models Fair? A Study of Racial Bias in Dermatological Image Generation** (2024) — Quantifies racial bias in dermatological image generation; shows that generative models amplify rather than correct the underrepresentation already present in training data.
- **Demographic Bias of Expert-Level Vision-Language Foundation Models in Medical Imaging** (*Science Advances*, 2024) — Demonstrates consistent demographic biases in medical VLM foundation models on chest X-rays; expert-level AI models show notable underdiagnosis bias for Black patients compared to certified radiologists.
- **Unmasking and Quantifying Racial Bias of LLMs in Medical Report Generation** (2024) — Finds statistically significant racial differences in GPT-3.5 and GPT-4's radiology report generation outputs, documenting racial bias in medical text generation.
- **Underdiagnosis Bias of Artificial Intelligence Algorithms Applied to Chest Radiographs in Underserved Patient Populations** (Seyyed-Kalantari et al., *Nature Medicine*, 2021) — Benchmarks AI underdiagnosis bias across three large chest X-ray datasets; finds highest underdiagnosis rates for intersectional underserved groups (e.g., Hispanic female patients).

---

### 3.2 Gender and Physiological Bias

**Description**: Historical training data has been male-dominated. Models underperform on female-specific symptom presentations (e.g., atypical MI symptoms), or reproduce historically discriminatory clinical practices in their recommendations.

**Case Example**: U.S. Senator Ben Ray Luján presented congressional testimony citing documented cases where medical AI trained predominantly on male data performed substantially worse when applied to female patients. A 2024 UK government-commissioned independent review ("Equity in Medical Devices") found that women, minority ethnic groups, and people from deprived communities systematically receive lower-quality care from biased medical AI tools.

**Key Papers**:
- **Sociodemographic Bias in Clinical Machine Learning Models: A Scoping Review** (*Journal of Clinical Epidemiology*, 2024) — Scoping review identifying gender bias as one of the most pervasive bias types in clinical ML, particularly in cardiology and mental health domains.
- **Does Sex Matter? Analysis of Sex-related Differences in Diagnostic Performance of a Market-Approved CNN for Skin Cancer Detection** (*European Journal of Cancer*, 2022) — Evaluates a market-approved skin cancer AI; finds statistically significant sex-based AUC disparities for certain lesion types.
- **Addressing Bias in Big Data and AI for Health Care: A Call for Open Science** (*PMC*, 2021) — Documents systematic absence of LGBTQ+ identifiers in EHR data, rendering AI blind to this population's specific healthcare needs and biases.
- **Bias Recognition and Mitigation Strategies in AI Healthcare Applications** (*npj Digital Medicine*, 2025) — Systematic review of gender bias sources (labeling bias, representation bias, historical bias) and their propagation throughout the medical AI lifecycle.

---

### 3.3 Geographic and Resource Inequality Bias

**Description**: Medical AI training data predominantly originates from high-income urban hospitals. Models fail to generalize to low-resource settings, rural environments, or different imaging equipment standards — amplifying global health gaps.

**Case Example**: A 2024 mixed-methods study (*The Case for Globalizing Fairness*) found that over 90% of medical AI fairness research focuses on Western contexts. African nations face a dual disadvantage: inadequate local training data representation *and* legacy medical infrastructure disparities from colonial history — making Western-trained AI systems systematically unreliable in these settings, a risk largely invisible in mainstream AI safety research.

**Key Papers**:
- **The Case for Globalizing Fairness: A Mixed Methods Study on Colonialism, AI, and Health in Africa** (2024) — Applies postcolonial theory to medical AI fairness; identifies how historical colonial power structures translate into current data representation failures and AI deployment inequity.
- **Algorithmic Bias in Public Health AI: A Silent Threat to Equity in Low-resource Settings** (*Frontiers in Public Health*, 2025) — Multi-stage analysis of bias sources in low-resource medical systems (data collection, labeling, algorithm optimization, deployment); proposes setting-specific mitigation strategies.
- **AI-Driven Healthcare: A Review on Ensuring Fairness and Mitigating Bias** (2024) — Reviews fairness failures in cardiology, ophthalmology, and dermatology across resource-diverse settings; highlights model generalization collapse under distribution shift.
- **Addressing Bias in Big Data and AI for Health Care** (*PMC*, 2021) — Documents genomic data representational gaps (predominantly European-origin databases) that render precision medicine AI fundamentally less effective for non-Western populations.

---

### 3.4 Proxy Variable Bias and Amplification of Historical Discrimination

**Description**: Removing protected attributes (race, gender) from training data is insufficient — models exploit correlated proxy variables (zip code, insurance type, historical cost) to reconstruct and amplify historical discrimination patterns.

**Case Example**: Obermeyer et al. (*Science*, 2019) analyzed a widely deployed U.S. health management algorithm that used "historical healthcare costs" as a proxy for medical need. Because Black patients historically received *less* healthcare (due to systemic inequality), they were assigned lower health risk scores than equally sick white patients — with the algorithm never explicitly encoding race, yet implementing racial discrimination at scale across millions of patients.

**Key Papers**:
- **Dissecting Racial Bias in an Algorithm Used to Manage the Health of Populations** (Obermeyer et al., *Science*, 2019) — Landmark empirical demonstration of proxy variable bias operating invisibly through cost-based health algorithms; foundational for the medical AI fairness field.
- **AI in Healthcare: Counteracting Algorithmic Bias** (*Boston University*, 2024) — Explains why removing sensitive attributes fails to eliminate bias; argues mitigation must address the societal conditions that produced biased training data.
- **Sociodemographic Bias in Clinical Machine Learning: A Scoping Review** (*JCE*, 2024) — Identifies proxy variable bias as the hardest-to-detect bias type in clinical ML; catalogs its manifestations across multiple specialties.
- **Guiding Principles to Address the Impact of Algorithm Bias on Racial and Ethnic Disparities** (*JAMA Network Open*, 2023) — Governance principles framework for addressing proxy variable bias through the full algorithm lifecycle: design, validation, and post-deployment monitoring.

---

## 4. Multimodal-Specific Adversarial & Reasoning Safety

**Core Problem**: Multimodal architectures introduce attack surfaces absent in unimodal systems — attackers can exploit visual modalities to bypass text-based safety alignment, or combine benign inputs to trigger dangerous reasoning chains. In clinical settings, consequences can be lethal.

---

### 4.1 Cross-Modality Jailbreak Attacks

**Description**: Attackers encode harmful instructions within medical images (X-rays, dermoscopy images) rather than text, bypassing text-only safety alignment mechanisms to elicit otherwise-refused dangerous medical outputs (lethal drug doses, dangerous procedures).

**Case Example**: The *Medical MLLM is Vulnerable* paper (2024) constructs the 3MAD dataset and tests LLaVA-Med. Using Multimodal Cross-optimization (MCM) — simultaneously optimizing adversarial image perturbations and text tokens — Attack Success Rate (ASR) substantially exceeds pure-text or pure-image jailbreaks. Medical models' text safety guardrails are rendered nearly ineffective when the visual modality is weaponized.

**Key Papers**:
- **Medical MLLM is Vulnerable: Cross-Modality Jailbreak and Mismatched Attacks on Medical Multimodal Large Language Models** (Huang et al., 2024) — First systematic definition and validation of cross-modality jailbreak attacks against medical MLLMs; introduces the 3MAD attack dataset and MCM algorithm.
- **Visual Adversarial Examples Jailbreak Aligned Large Language Models** (Qi et al., AAAI 2024) — Establishes that visual modality is an effective vector for bypassing text-safety alignment in LLMs; provides theoretical and empirical foundations for medical cross-modal jailbreak research.
- **Jailbreak Large Vision-Language Models Through Multi-Modal Linkage (MML)** (ACL 2025) — Proposes visual-textual linkage attacks that achieve high success rates without exposing obviously malicious content — stealthy enough to evade manual review.
- **A Practical Framework for Evaluating Medical AI Security** (2024) — Classifies cross-modality jailbreaks as the highest-severity vulnerability in medical AI; proposes standardized red-team evaluation and defense assessment protocols.

---

### 4.2 Mismatched Input Attacks

**Description**: Normal-use scenarios (no malicious intent required) with mismatched image-text pairs exploit cross-modal reasoning vulnerabilities, generating hallucinated pathology confirmations that conform to text expectations rather than image reality. Clinical mishaps (mislabeled images, wrong patient association) can trigger this inadvertently.

**Case Example**: In *Medical MLLM is Vulnerable*, a healthy lung X-ray paired with the text "patient suspected of lung cancer, awaiting imaging confirmation" causes multiple medical models to generate fabricated nodule descriptions "confirming" the text's expectation — contradicting the actual image content. In real clinical deployment, this scenario can arise from EHR system errors or image archive misidentification.

**Key Papers**:
- **Medical MLLM is Vulnerable: Cross-Modality Jailbreak and Mismatched Attacks** (Huang et al., 2024) — Simultaneously defines and demonstrates mismatched attacks; models realistic clinical error scenarios (e.g., wrong image-patient pairing) as inadvertent attack vectors.
- **CARES: A Comprehensive Benchmark of Trustworthiness in Medical Vision Language Models** (Xia et al., NeurIPS 2024) — Includes cross-modal consistency testing in its robustness dimension; systematically quantifies Med-VLM failure under mismatched inputs.
- **Assessing the Adversarial Robustness of Multimodal Medical AI Systems** (*Frontiers in Medicine*, 2025) — Experiments with differential adversarial attacks per modality (image vs. text vs. joint); characterizes multimodal fusion responses to mismatched inputs.
- **An Embarrassingly Simple Probing Evaluation of Medical VQA** (Yan et al., 2024) — Simple substitution probes showing models answer correctly without image processing, directly demonstrating the cross-modal understanding deficit underlying mismatched input vulnerability.

---

### 4.3 Implicit Reasoning Safety Risks

**Description**: Combinations of individually benign inputs trigger dangerous reasoning chains — a blood test image + academic pharmacology question may be reasoned into an overdose guide. Traditional single-input safety filters cannot detect or prevent this.

**Case Example**: *Safe Semantics, Unsafe Interpretations* introduces a medical case: a patient's blood panel image (benign) combined with an academic question about a drug's mechanism of action (benign text) leads the model — through chain-of-thought reasoning — to generate specific toxic dose guidance. Neither input alone would be flagged by standard content filters.

**Key Papers**:
- **Safe Semantics, Unsafe Interpretations: Tackling Implicit Reasoning Safety in Large Vision-Language Models** (2024) — First formal introduction of "implicit reasoning safety" as a concept; constructs a benign-input-combination attack paradigm and demonstrates its effectiveness in medical scenarios.
- **Towards Safe AI Clinicians: A Comprehensive Study on LLM Jailbreaking in Healthcare** (2024) — Identifies implicit reasoning jailbreaks as the hardest-to-defend attack class; surveys medical-domain jailbreaking research comprehensively.
- **Medical MLLM is Vulnerable** (Huang et al., 2024) — Cross-modality attack experiments also capture implicit dangerous reasoning combinations emerging from multimodal inputs.
- **Jailbreak in Pieces: Compositional Adversarial Attacks on Multi-Modal Language Models** (Shayegani et al., 2024) — Proposes splitting harmful content across image and text modalities for in-context model reassembly; directly operationalizes implicit reasoning safety risk.

---

### 4.4 Knowledge Base Poisoning in Medical RAG Systems

**Description**: RAG-augmented medical multimodal systems that rely on external knowledge bases (medical literature, image-report pairs) for accuracy face a new attack surface: knowledge base poisoning. A single adversarial injection can persistently corrupt model outputs without any direct model access.

**Case Example**: MedThreatRAG (2025) operates in a simulated semi-open hospital knowledge base environment. A single adversarial injection — a chest X-ray of pleural effusion mislabeled as "normal" — causes the RAG system to consistently retrieve and apply this incorrect mapping for all related subsequent queries, without the attacker ever touching model weights or parameters.

**Key Papers**:
- **How to Make Medical AI Systems Safer? (MedThreatRAG)** (2025) — First systematic poisoning attack framework for multimodal medical RAG systems; introduces three attack strategies (textual, visual, cross-modal conflict injection) and evaluates single-injection impact.
- **RULE: Reliable Multimodal RAG for Factuality in Medical Vision Language Models** (Xia et al., EMNLP 2024) — Defensive counterpart: improves factual reliability of medical RAG; implicitly reveals the security-reliability tradeoff in retrieval-augmented medical AI.
- **Medical LLMs Are Susceptible to Targeted Misinformation Attacks** (*npj Digital Medicine*, 2024) — Mechanistic analysis of misinformation propagation at the weight level; provides theoretical grounding for understanding RAG poisoning analogues.
- **Data Poisoning Vulnerabilities Across Health Care AI** (*JMIR*, 2026) — Places RAG knowledge base poisoning in the broader medical AI poisoning threat landscape; analyzes differences from traditional training data poisoning in technical and governance dimensions.

---

## 5. Ethics & Liability Risks

**Core Problem**: Medical multimodal AI introduces fundamental ethical and legal conflicts around informed consent, liability, transparency, and deceptive system design — existing frameworks cannot adequately address these.

---

### 5.1 Ambiguous Liability and Accountability Vacuums

**Description**: When AI-assisted diagnosis causes patient harm, no clear legal or ethical framework determines who bears responsibility — the clinician, hospital, AI developer, or regulator — creating accountability vacuums that undermine trust and safety incentives.

**Case Example**: A radiologist relies on an AI's "low suspicion" recommendation and defers a biopsy; the patient is later diagnosed with early-stage cancer. Courts must determine: Did the physician adequately "oversee" the AI? Does the developer's performance specification constitute a medical recommendation? Is the hospital liable for deploying AI without adequate training? — All three parties may escape full accountability under current legal frameworks.

**Key Papers**:
- **Ethical and Legal Considerations in Healthcare AI: Innovation and Policy for Safe and Fair Use** (*Royal Society Open Science*, 2025) — Comprehensively maps the accountability gap in medical AI; analyzes the inadequacy of current legal and professional norms for hybrid human-AI decision-making.
- **Ethical Challenges and Evolving Strategies in AI-Clinical Practice Integration** (*PLOS Digital Health*, 2025) — Frames accountability within a five-principle ethical framework (justice, transparency, consent, accountability, patient-centered care); examines clinical AI liability in real implementation cases.
- **Ethics and Governance of Artificial Intelligence for Health: Guidance on LMMs** (WHO, 2024) — WHO's first guidance document dedicated to medical large multimodal models; proposes 40+ governance recommendations with accountability as a core principle.
- **Towards Accountable, Legitimate and Trustworthy AI in Healthcare: Effective Data Stewardship** (*Body & Society*, 2025) — Proposes data stewardship as an institutional accountability mechanism; examines operationalizability in medical AI contexts.

---

### 5.2 Black-Box Decision-Making and Lack of Explainability

**Description**: Multimodal foundation model decisions are opaque to clinicians and patients. Physicians cannot understand *why* the AI produced a specific diagnosis, cannot challenge outputs meaningfully, and cannot explain AI-assisted decisions to patients — undermining informed medical practice.

**Case Example**: A qualitative study of healthcare professionals (Yoo et al., 2023) found clinicians' primary concern about medical AI is not its accuracy but the **inability to understand its reasoning**. When AI recommendations conflict with clinical judgment, physicians can neither validate nor explain the AI's reasoning — effectively facing a choice between two black boxes, one algorithmic and one intuitive.

**Key Papers**:
- **Ethics and Governance of AI for Health** (WHO, 2024) — Positions "intelligibility" as a foundational governance principle; establishes that explainability is not merely technical but a prerequisite for patient autonomy protection.
- **The Intersection of Law, Ethics, and Healthcare AI** (*Advances in Consumer Research*, 2025) — Argues explainability is a means to accountability, not an end; must be integrated with documentation, calibration, and uncertainty quantification to serve its intended safety function.
- **Safety Challenges of AI in Medicine in the Era of LLMs** (Multi-institution, 2024) — Pairs black-box risk with clinical workflow restructuring dangers; examines long-term safety culture effects of opaque AI integration.
- **Ethical Challenges and Evolving Strategies in AI-Clinical Practice Integration** (*PLOS Digital Health*, 2025) — Identifies transparency as the most practically challenging dimension of its five-principle ethical framework; proposes "pharmacovigilance-inspired" continuous AI transparency auditing.

---

### 5.3 Informed Consent and Patient Autonomy

**Description**: Patients are frequently unaware of the extent of AI involvement in their diagnoses, the provenance of training data (which may include their own records), or the specific limitations of AI tools — making genuine informed consent structurally impossible under current practices.

**Case Example**: An NHS survey (2024) found over 70% of patients did not know AI was being used to analyze their imaging studies. When informed, many expressed they would have withheld consent if aware their data was used to train commercial AI systems — creating a fundamental contradiction with existing "implied consent" data use practices in many healthcare systems.

**Key Papers**:
- **Ethical and Legal Considerations in Healthcare AI** (*Royal Society Open Science*, 2025) — Redefines informed consent for the AI era; analyzes dynamic consent models as alternatives to one-time authorization in contexts of ongoing AI model updates.
- **SoK: Privacy-aware LLM in Healthcare** (2024) — Examines legal compliance gaps between patient data use for LLM training and HIPAA/GDPR protections; identifies the structural tension between multimodal model data appetites and consent frameworks.
- **Ethics and Governance of AI for Health** (WHO, 2024) — Operationalizes patient autonomy protection through clear AI disclosure requirements and opt-out mechanisms; distinguishes between AI use in care delivery vs. AI training data use.
- **Towards Accountable AI in Healthcare: Data Stewardship** (*Body & Society*, 2025) — Reframes consent as continuous participation rather than one-time authorization; proposes stewardship institutions to bridge patient interests and AI development needs.

---

### 5.4 Deceptive Design Patterns and Anthropomorphization

**Description**: Medical AI systems embedded in chatbots or social robots deliberately blur the boundary between AI and human clinicians through anthropomorphized interfaces, false empathy, and persuasive language — creating false trust that overrides patient judgment and obscures AI limitations.

**Case Example**: The *Rapid Integration of LLMs in Healthcare* study (2024) analyzed multiple commercial AI medical assistant products and identified systematic deceptive patterns: interfaces designed to obscure the AI/human boundary, emotional language ("I'm deeply concerned about your symptoms") creating false empathy, and "stabilizing" scripts deployed to prevent dissatisfied patients from seeking second opinions rather than honestly acknowledging AI limitations.

**Key Papers**:
- **Rapid Integration of LLMs in Healthcare Raises Ethical Concerns: Deceptive Patterns in Social Robots** (2024) — First systematic identification and taxonomy of deceptive design patterns in medical AI social robots; examines conflicts with established medical ethics norms.
- **Ethical Challenges and Evolving Strategies in AI-Clinical Practice Integration** (*PLOS Digital Health*, 2025) — Within its patient-centered ethics framework, analyzes how anthropomorphized AI design undermines genuine patient autonomy and the therapeutic alliance.
- **"It's Not Only Attention We Need": LLMs in Mental Health Care** (*PMC*, 2025) — Analyzes dual effects of anthropomorphized mental health AI: improved engagement alongside deepened over-reliance and erosion of human therapeutic relationships.
- **Ethics and Governance of AI for Health** (WHO, 2024) — Mandates clear disclosure of AI identity as a core governance requirement; frames anti-deception as essential to maintaining patient trust in healthcare systems.

---

## 6. Socioeconomic Impact Risks

**Core Problem**: Medical multimodal AI deployment is not merely a technical question but a profound distributive question — it restructures access to healthcare resources, transforms the medical workforce, creates new forms of data extraction, and embeds commercial logic into clinical decisions.

---

### 6.1 Technology-Driven Healthcare Resource Gaps

**Description**: State-of-the-art medical AI deploys first at well-resourced elite institutions, while community hospitals serving disadvantaged populations face longer adoption lags — creating a paradox where the populations most harmed by algorithmic bias are served by institutions with least AI access.

**Case Example**: Research indicates that as of 2024, more than 75% of FDA-cleared medical AI algorithms are deployed in the top 20% of large U.S. healthcare institutions, while community hospitals serving majority minority and low-income populations remain largely outside the AI deployment wave — a structural compounding of existing healthcare inequality.

**Key Papers**:
- **The Case for Globalizing Fairness: A Mixed Methods Study on Colonialism, AI, and Health in Africa** (2024) — Political-economy analysis of how high-income-country-dominated medical AI ecosystems reproduce and deepen historical health inequalities globally.
- **Algorithmic Bias in Public Health AI: A Silent Threat to Equity in Low-resource Settings** (*Frontiers*, 2025) — Quantifies technology access gaps in low-resource health systems; analyzes interaction with existing health inequalities.
- **Ethics and Governance of AI for Health** (WHO, 2024) — Positions accessibility and affordability as core principles for equitable medical AI deployment; proposes international coordination mechanisms for low-income country access.
- **AI-Driven Healthcare: A Review on Ensuring Fairness and Mitigating Bias** (2024) — Reviews how unequal AI deployment itself constitutes a form of structural bias compounding algorithmic bias.

---

### 6.2 Healthcare Workforce Disruption and Skill Degradation

**Description**: Medical AI rapidly reaches expert-level performance in imaging-intensive specialties (radiology, pathology, dermatology), restructuring training pipelines, eroding baseline clinical skills, and creating new professional identity crises — with long-term patient safety implications.

**Case Example**: Radiology residency programs in the U.S. have begun reducing traditional high-volume repetitive reading rotations, with AI replacing these formative skill-building experiences. Paradoxically, this reduces the very clinical experience needed for trainees to effectively *supervise* AI systems in complex edge cases — creating a structural skill-degradation risk for the next generation of clinicians.

**Key Papers**:
- **Safety Challenges of AI in Medicine in the Era of LLMs** (Multi-institution, 2024) — Discusses AI's systemic impact on medical professional identity and training; examines long-term patient safety implications of reduced foundational skill development.
- **Ethical Challenges and Evolving Strategies in AI-Clinical Practice Integration** (*PLOS Digital Health*, 2025) — Addresses the transformation of clinician roles to "AI supervisors"; analyzes what new training requirements this entails and what existing competency frameworks must change.
- **GPT-4V(ision) Unsuitable for Clinical Care and Education** (Bedi et al., 2024) — From an educational perspective, warns that premature introduction of multimodal AI in medical education risks damaging clinical reasoning capacity development.
- **Ethics and Governance of AI for Health** (WHO, 2024) — Includes human professional capacity development in its governance agenda; advocates for policies ensuring human expertise and AI capability co-develop rather than compete.

---

### 6.3 Data Colonialism and Intellectual Property Inequality

**Description**: Large technology companies and high-income-country research institutions collect patient data from low-income countries under "global health progress" framing, train commercial AI products, and sell them at prices beyond the originating institutions' reach — a new form of knowledge dispossession.

**Case Example**: Multiple African nations have documented cases where hospital imaging data was incorporated into global medical AI databases (e.g., for diabetic retinopathy detection) used to train commercial products. The resulting AI systems are then licensed at prices completely beyond the economic capacity of the contributing hospitals — making data contributors systematically excluded from the technology they helped create.

**Key Papers**:
- **The Case for Globalizing Fairness: A Mixed Methods Study on Colonialism, AI, and Health in Africa** (2024) — Introduces data colonialism framing to medical AI; reveals power asymmetries in data ownership, benefit distribution, and technology access through mixed-methods African case studies.
- **Addressing Bias in Big Data and AI for Health Care: A Call for Open Science** (*PMC*, 2021) — Proposes open science as a counter to data colonialism; advocates for globally equitable data co-ownership and sharing mechanisms preserving data sovereignty.
- **Ethics and Governance of AI for Health** (WHO, 2024) — Explicitly identifies "high-income country bias" as a critical global governance challenge; requires global representativeness throughout development, validation, and deployment.
- **Medical Multimodal Model Stealing Attacks via Adversarial Domain Alignment** (2025) — From a technical IP perspective, demonstrates vulnerabilities in medical model knowledge ownership, complementing the policy discussion on data and model IP inequity.

---

### 6.4 Healthcare Commercialization and Conflicts of Interest

**Description**: The commercial logic of medical AI (optimizing for performance metrics and market scale) structurally conflicts with medical ethics logic (optimizing for patient welfare). This creates conditions where AI systems may be optimized for commercially favorable metrics rather than clinical safety — and where motivated actors (insurers, pharma) have strong financial incentives to manipulate medical AI systems.

**Case Example**: The *JMIR* data poisoning analysis (2026) explicitly models commercial actors as realistic adversaries: insurers have strong incentives to train AI toward "low-risk" diagnoses to reduce claim payouts; pharmaceutical companies may exploit prescribing AI to favor proprietary medications. These attacks are more persistent and harder to detect than random malicious attacks, precisely because they are commercially motivated to remain invisible.

**Key Papers**:
- **Data Poisoning Vulnerabilities Across Health Care AI** (*JMIR*, 2026) — Explicitly models insurance companies, pharmaceutical firms, and competitors as medical AI adversaries with specific commercial motivations; integrates commercial conflict of interest into the security threat framework.
- **Dissecting Racial Bias in an Algorithm Used to Manage the Health of Populations** (Obermeyer et al., *Science*, 2019) — Landmark case of commercial optimization logic (cost-as-proxy-for-need) producing systematic racial discrimination; canonical example of how commercial framing distorts medical AI objectives.
- **Ethical Challenges and Evolving Strategies in AI-Clinical Practice Integration** (*PLOS Digital Health*, 2025) — Within a conflict-of-interest ethical analysis, examines how institutional design and regulatory mechanisms can suppress commercial interest penetration into medical AI decision logic.
- **The Intersection of Law, Ethics, and Healthcare AI** (*Advances in Consumer Research*, 2025) — Analyzes how the EU AI Act, FDA regulatory framework, and WHO guidelines are beginning to classify commercial medical AI under mandatory high-risk oversight regimes.

---

## Risk Overview: Summary Table

| Category | Key Sub-risks | Primary Harm | Representative Papers |
|---|---|---|---|
| **Clinical Safety** | Hallucination, unreliable decision support, cross-modal misinterpretation, knowledge cutoff, over-reliance | Misdiagnosis, delayed treatment, patient harm | CARES, MedVH, MediConfusion |
| **Privacy & Security** | Data leakage, prompt injection, adversarial examples, backdoor attacks | Patient privacy violation, system manipulation | SoK Privacy, 3MAD, MedThreatRAG |
| **Algorithmic Bias** | Racial bias, gender bias, geographic bias, proxy variable bias | Systematic underdiagnosis in vulnerable groups | Obermeyer Science, Science Advances |
| **Multimodal-Specific** | Cross-modal jailbreak, mismatched attacks, implicit reasoning, RAG poisoning | Safety guardrail failure, dangerous content | Medical MLLM Vulnerable, Safe Semantics |
| **Ethics & Liability** | Accountability vacuum, black-box opacity, consent, deceptive design | Legal gray zones, patient autonomy erosion | WHO LMM Guidance, Royal Society |
| **Socioeconomic** | Technology gap, workforce disruption, data colonialism, commercial conflict | Health inequality amplification, systemic exploitation | Colonialism Africa, JMIR Poisoning |

---

## References

> All papers cited in this document are listed below with links where available.

**[R1]** Gu et al. (2024). *MedVH: Toward Systematic Evaluation of Hallucination for Large Vision Language Models in the Medical Context.* PhysioNet/arXiv. https://pmc.ncbi.nlm.nih.gov/articles/PMC12363988/

**[R2]** Zhu et al. (ACL 2025). *Can We Trust AI Doctors? A Survey of Medical Hallucination in LLMs and LVLMs.* https://github.com/Zhihong-Zhu/Medical_Hallucination_Survey

**[R3]** Xia et al. (NeurIPS 2024). *CARES: A Comprehensive Benchmark of Trustworthiness in Medical Vision Language Models.* https://arxiv.org/abs/2406.06007

**[R4]** (Survey, 2025). *Medical Hallucination in Foundation Models and Their Impact on Healthcare.* medrxiv. https://arxiv.org/abs/2503.05777

**[R5]** Wu et al. (ICLR 2024). *Hallucination Benchmark in Medical Visual Question Answering.* arXiv.

**[R6]** Omar et al. (2025). *Multi-model assurance analysis showing LLMs are highly vulnerable to adversarial hallucination attacks during clinical decision support.* Communications Medicine. https://www.nature.com/articles/s43856-025-01021-3

**[R7]** Bedi et al. (2024). *GPT-4V(ision) Unsuitable for Clinical Care and Education: A Clinician-Evaluated Assessment.* npj Digital Medicine.

**[R8]** (2024). *First, Do NOHARM: Towards Clinically Safe Large Language Models.* arXiv.

**[R9]** (2025). *A Framework to Assess Clinical Safety and Hallucination Rates of LLMs for Medical Text Summarisation.* npj Digital Medicine. https://www.nature.com/articles/s41746-025-01670-7

**[R10]** (2024). *MediConfusion: Can You Trust Your AI Radiologist?* arXiv.

**[R11]** Nan et al. (2024). *Beyond the Hype: A Dispassionate Look at Vision-Language Models in Medical Scenarios.* arXiv.

**[R12]** Yan et al. (2024). *An Embarrassingly Simple Probing Evaluation of Large Multimodal Models in Medical VQA.* arXiv.

**[R13]** Chen et al. (2023). *Detecting and Evaluating Medical Hallucinations in Large Vision Language Models.* arXiv.

**[R14]** Multi-institution (2024). *Safety Challenges of AI in Medicine in the Era of Large Language Models.* arXiv.

**[R15]** Agarwal et al. (2024). *MedHalu: Hallucinations in Responses to Healthcare Queries by LLMs.* arXiv.

**[R16]** (2025). *"It's Not Only Attention We Need": Systematic Review of LLMs in Mental Health Care.* PMC. https://pmc.ncbi.nlm.nih.gov/articles/PMC12627976/

**[R17]** (2024). *Rapid Integration of LLMs in Healthcare Raises Ethical Concerns: Deceptive Patterns in Social Robots.* arXiv.

**[R18]** (2024). *Towards Safe AI Clinicians: A Comprehensive Study on LLM Jailbreaking in Healthcare.* arXiv.

**[R19]** (2024). *SoK: Privacy-aware LLM in Healthcare: Threat Model, Privacy Techniques, Challenges and Recommendations.* arXiv.

**[R20]** (2025). *Medical Multimodal Model Stealing Attacks via Adversarial Domain Alignment (ADA-Steal).* arXiv. https://arxiv.org/abs/2502.02438

**[R21]** (2026). *Data Poisoning Vulnerabilities Across Health Care AI.* JMIR. https://www.jmir.org/2026/1/e87969

**[R22]** (2024). *Robustness in Deep Learning Models for Medical Diagnostics: Security and Adversarial Challenges.* AI Review. https://link.springer.com/article/10.1007/s10462-024-11005-9

**[R23]** (2024). *Prompt Injection Attacks on Large Language Models in Oncology.* arXiv.

**[R24]** (2024). *Emerging Cyber Attack Risks of Medical AI Agents.* arXiv.

**[R25]** (2025). *How to Make Medical AI Systems Safer? (MedThreatRAG).* arXiv. https://arxiv.org/abs/2508.17215

**[R26]** (2024). *A Practical Framework for Evaluating Medical AI Security.* arXiv. https://arxiv.org/abs/2512.08185

**[R27]** Finlayson et al. (Science, 2019). *Adversarial Attacks on Medical Machine Learning.* https://www.science.org/doi/10.1126/science.aaz7888

**[R28]** (2025). *Assessing the Adversarial Robustness of Multimodal Medical AI Systems.* Frontiers in Medicine. https://www.frontiersin.org/journals/medicine/articles/10.3389/fmed.2025.1606238/full

**[R29]** (2024). *Medical LLMs Are Susceptible to Targeted Misinformation Attacks.* npj Digital Medicine. https://www.nature.com/articles/s41746-024-01282-7

**[R30]** (2024). *Are Generative Models Fair? A Study of Racial Bias in Dermatological Image Generation.* arXiv.

**[R31]** (Science Advances, 2024). *Demographic Bias of Expert-Level Vision-Language Foundation Models in Medical Imaging.* https://www.science.org/doi/10.1126/sciadv.adq0305

**[R32]** (2024). *Unmasking and Quantifying Racial Bias of LLMs in Medical Report Generation.* arXiv.

**[R33]** Seyyed-Kalantari et al. (Nature Medicine, 2021). *Underdiagnosis Bias of AI Algorithms Applied to Chest Radiographs in Underserved Patient Populations.* https://www.nature.com/articles/s41591-021-01595-0

**[R34]** (JCE, 2024). *Sociodemographic Bias in Clinical Machine Learning Models: A Scoping Review.* https://www.jclinepi.com/article/S0895-4356(24)00362-7/fulltext

**[R35]** (Frontiers, 2025). *Algorithmic Bias in Public Health AI: A Silent Threat to Equity in Low-resource Settings.* https://pmc.ncbi.nlm.nih.gov/articles/PMC12325396/

**[R36]** (PMC, 2021). *Addressing Bias in Big Data and AI for Health Care: A Call for Open Science.* https://pmc.ncbi.nlm.nih.gov/articles/PMC8515002/

**[R37]** (2024). *The Case for Globalizing Fairness: A Mixed Methods Study on Colonialism, AI, and Health in Africa.* arXiv.

**[R38]** (2024). *AI-Driven Healthcare: A Review on Ensuring Fairness and Mitigating Bias.* arXiv.

**[R39]** Obermeyer et al. (Science, 2019). *Dissecting Racial Bias in an Algorithm Used to Manage the Health of Populations.* https://www.science.org/doi/10.1126/science.aax2342

**[R40]** (BU, 2024). *AI in Healthcare: Counteracting Algorithmic Bias.* https://www.bu.edu/deerfield/2024/04/14/stone2-2/

**[R41]** (JAMA Network Open, 2023). *Guiding Principles to Address the Impact of Algorithm Bias on Racial and Ethnic Disparities.* https://jamanetwork.com/journals/jamanetworkopen/fullarticle/2812289

**[R42]** (npj Digital Medicine, 2025). *Bias Recognition and Mitigation Strategies in AI Healthcare Applications.* https://www.nature.com/articles/s41746-025-01503-7

**[R43]** Huang et al. (2024). *Medical MLLM is Vulnerable: Cross-Modality Jailbreak and Mismatched Attacks.* arXiv. https://arxiv.org/abs/2405.20775

**[R44]** Qi et al. (AAAI, 2024). *Visual Adversarial Examples Jailbreak Aligned Large Language Models.* arXiv. https://arxiv.org/abs/2306.13213

**[R45]** (ACL, 2025). *Jailbreak Large Vision-Language Models Through Multi-Modal Linkage (MML).* https://aclanthology.org/2025.acl-long.74.pdf

**[R46]** (2024). *Safe Semantics, Unsafe Interpretations: Tackling Implicit Reasoning Safety in Large Vision-Language Models.* arXiv.

**[R47]** Shayegani et al. (2024). *Jailbreak in Pieces: Compositional Adversarial Attacks on Multi-Modal Language Models.* arXiv. https://arxiv.org/abs/2307.04218

**[R48]** Xia et al. (EMNLP, 2024). *RULE: Reliable Multimodal RAG for Factuality in Medical Vision Language Models.* arXiv. https://arxiv.org/abs/2410.05524

**[R49]** (Royal Society Open Science, 2025). *Ethical and Legal Considerations in Healthcare AI.* https://royalsocietypublishing.org/rsos/article/12/5/241873/

**[R50]** (PLOS Digital Health, 2025). *Ethical Challenges and Evolving Strategies in the Integration of AI into Clinical Practice.* https://pmc.ncbi.nlm.nih.gov/articles/PMC11977975/

**[R51]** WHO (2024). *Ethics and Governance of AI for Health: Guidance on Large Multi-modal Models.* https://www.who.int/publications/i/item/9789240084759

**[R52]** (Body & Society, 2025). *Towards Accountable, Legitimate and Trustworthy AI in Healthcare: Effective Data Stewardship.* https://www.tandfonline.com/doi/full/10.1080/20502877.2025.2482282

**[R53]** (IJMR, 2025). *The Clinicians' Guide to Large Language Models: A General Perspective With a Focus on Hallucinations.* https://pmc.ncbi.nlm.nih.gov/articles/PMC11815294/

**[R54]** (Advances in Consumer Research, 2025). *The Intersection of Law, Ethics, and Healthcare AI.* https://acr-journal.com/article/the-intersection-of-law-ethics-and-healthcare-ai-policy-pathways-for-responsible-innovation-1695/

---

*Last updated: April 2026*
