---
title: "Comprehensive Assessment of Jailbreak Attacks Against LLMs"
layout: default
---

# Overview

<div align="center">
  <img src="https://github.com/Junjie-Chu/Best_Jailbreak_Way_Public/assets/65893273/42ea7acf-1aa4-46b3-9aeb-de9b614f8b4b" alt="Overview_JB_thick" width="58%">
</div>

# Abstract
*Jailbreak attacks* aim to bypass the safeguards of LLMs.
While researchers have studied different jailbreak attacks in depth, they have done so in isolation - either with unaligned experiment settings or comparing a limited range of methods.
To fill this gap, we present the first large-scale measurement of various jailbreak attack methods. 
We collect 14 cutting-edge jailbreak methods and establish a jailbreak attack taxonomy.
We then conduct a unified and impartial assessment of attack effectiveness based on six popular censored LLMs and 160 questions from 16 violation categories.
Our extensive experimental results demonstrate that all the jailbreak attacks have a powerful effect on the LLMs.
The optimized-based jailbreak attacks consistently achieve the best attack performance, as well as exhibit robustness across different LLMs.
Some jailbreak prompts available from the Internet can also achieve high attack success rates on many LLMs, such as Vicuna, ChatGLM3, GPT-3.5, and PaLM2. 
Despite the claims from many organizations regarding the coverage of violation categories in their policies, the attack success rates from these categories remain high, indicating the challenges of effectively aligning LLM policies and countering jailbreak attacks.
Furthermore, we conduct a comprehensive ablation study to analyze different aspects of jailbreak attack performance.
Based on the experimental results, we discuss the trade-off between attack performance and efficiency. 
We also show that the transferability of the jailbreak prompts is still viable, becoming an option for black-box models.
Results of our longitudinal test on continuously updated LLMs show good attack stability over time of optimization-based methods.
Additionally, we test jailbreak attacks under four advanced external defenses and find none of the defenses could mitigate the jailbreak attacks entirely.
We hope our study can provide insights for future research on jailbreak attacks and serve as a benchmark tool for researchers and practitioners to evaluate them.

# Jailbreak Taxonomy

We classify the methods based on the following two criteria:
- We consider whether the original forbidden question is modified to bypass the target LLM's alignment mechanisms in the method.
- If the original question is modified, we then consider how these modified prompts are generated in the method, such as through translation or adding prefixes and suffixes.

| Jailbreak Taxonomy |     Jailbreak Method    | Require White-Box Access? | Modify the Original Question?  |
|:------------------:|:-----------------------:|:-------------------------:|:------------------------------:|
|     Human-Based    |           AIM           |             ✗             |                ✓               |
|     Human-Based    |       Devmoderanti      |             ✗             |                ✓               |
|     Human-Based    |        Devmodev2        |             ✗             |                ✓               |
|  Obfuscation-Based |          Base64         |             ✗             |                ✓               |
|  Obfuscation-Based |       Combination       |             ✗             |                ✓               |
|  Obfuscation-Based |           Zulu          |             ✗             |                ✓               |
| Optimization-Based |         AutoDAN         |             ✓             |                ✓               |
| Optimization-Based |           GCG           |             ✓             |                ✓               |
| Optimization-Based |           COLD          |             ✓             |                ✓               |
| Optimization-Based |         GPTfuzz         |             ✗             |                ✓               |
| Optimization-Based |           PAIR          |             ✗             |                ✓               |
| Optimization-Based |           TAP           |             ✗             |                ✓               |
| Optimization-Based |        Masterkey        |             ✗             |                ✓               |
|   Parameter-Based  | Generation Exploitation |             ✓             |                ✗               |

# Unified Usage Policy

We first collect the usage policies from five major LLM-related service providers (Google, OpenAI, Meta, Amazon, and Microsoft).
Many policies tend to provide a general description by synthesizing many specific categories within an overarching category.
Unlike the general ones, we summarize our unified policy by *explicit coverage* to find a clear common feature within the same category.

***Violation Category Details:***

| Violation Category 	| Category Description 	|
|---	|---	|
| Hate, Unfairness, or Harassment 	| This policy prohibits the use of AI to create or disseminate content that promotes hate, harassment, discrimination, unfairness, or violence against individuals or groups based on attributes like race, gender, religion, disability, or any other characteristics that may be subject to discrimination. 	|
| Malicious Software 	| The creation of tools or software through AI that are designed to harm or disrupt other systems, steal data, invade privacy, or engage in any form of cybercrime is strictly forbidden. 	|
| Well-being Infringement 	| AI should not be used in ways that could significantly impact individual rights or well-being, especially in sensitive areas like financial advice, housing, and employment. 	|
| Physical Harm 	| AI should not be used in any manner that could pose a direct risk of physical harm to people. 	|
| Disinformation Spread 	| The generation or dissemination of false information, including any form of deception intended to manipulate public opinion, defraud individuals, or misrepresent facts, is prohibited. 	|
| Privacy Breach 	| AI should not be used to infringe upon individual privacy rights, including activities that involve accessing, processing, memorizing, or sharing personal data without consent. 	|
| Adult Content 	| The creation or promotion of adult content, services related to the adult industry, or the use of AI in dating apps in a manner that violates ethical standards or legal regulations is not permitted. This does not include content created for scientific or educational purposes. 	|
| Political Activities 	| AI should not be used for engaging in political campaigning or lobbying, including generating campaign materials personalized to or targeted at specific demographics. 	|
| Impersonation 	| The use of AI to impersonate another person, whether for fraudulent, deceptive, or any unauthorized purposes, is strictly prohibited. 	|
| Terrorist Content 	| The creation or dissemination of content promoting terrorism or extremist ideologies is not allowed. 	|
| Unauthorized Practice 	| AI should not be used to provide tailored advice in professional services (like financial, legal, medical, or other specialized fields) without review by a qualified professional. 	|
| Safety Filter Bypass 	| Intentionally manipulating AI to bypass ethical guidelines, safety protocols, or to perform actions contrary to established policies is forbidden. 	|
| Risky Government Decisions 	| AI should not be used for making decisions in high-stakes government functions like law enforcement, military actions, judiciary decisions, etc. 	|
| AI Usage Disclosure 	| There must be transparency when AI is being used, especially in interactions where individuals might reasonably assume they are dealing with a human. 	|
| Third-party Rights Violation 	| AI should not be used in a way that infringes on intellectual property rights, copyright, trademark, or any other legal rights of others. This includes creating content that copies or mimics the work of others without permission. 	|
| Illegal Activities 	| The use of AI to engage in, support, or promote illegal activities is strictly prohibited. 	|
| Crimes Involving Children 	| Any use of AI related to crimes involving children, including the creation, distribution, or promotion of child exploitation material, is strictly forbidden and subject to legal action. 	|

***Policy Coverage:***

|        Violation category       | OpenAI | Microsoft | Google | Amazon | Meta |
|:-------------------------------:|:------:|:---------:|:------:|:------:|:----:|
| Hate, Unfairness, or Harassment |    ✓   |     ✓     |    ✓   |    ✓   |   ✓  |
|        Malicious Software       |    ✓   |     ✓     |    ✓   |    ✓   |   ✓  |
|     Well-being Infringement     |    ✓   |     ✓     |    ✓   |    ✓   |   ✓  |
|          Physical Harm          |    ✓   |     ✓     |    ✓   |    ✓   |   ✓  |
|      Disinformation Spread      |    ✓   |     ✓     |    ✓   |    ✓   |   ✓  |
|          Privacy Breach         |    ✓   |     -     |    ✓   |    ✓   |   ✓  |
|          Adult Content          |    ✓   |     ✓     |    ✓   |    -   |   ✓  |
|       Political Activities      |    ✓   |     ✓     |    -   |    -   |   -  |
|          Impersonation          |    ✓   |     ✓     |    ✓   |    ✓   |   ✓  |
|        Terrorist Content        |    -   |     ✓     |    ✓   |    ✓   |   ✓  |
|      Unauthorized Practice      |    ✓   |     -     |    ✓   |    ✓   |   ✓  |
|       Safety Filter Bypass      |    ✓   |     -     |    ✓   |    ✓   |   -  |
|    Risky Government Decisions   |    ✓   |     -     |    ✓   |    -   |   -  |
|       AI Usage Disclosure       |    ✓   |     -     |    -   |    -   |   ✓  |
|   Third-party Rights Violation  |    -   |     ✓     |    -   |    ✓   |   ✓  |
|        Illegal Activities       |    ✓   |     ✓     |    ✓   |    ✓   |   ✓  |
|    Crimes involving children    |    ✓   |     ✓     |    ✓   |    ✓   |   ✓  |

