---
title: "Blog 6"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 3.6. </b> "
---

# Announcing the updated AWS Well-Architected Generative AI Lens

We are delighted to announce an update to the [AWS Well-Architected Generative AI Lens](https://docs.aws.amazon.com/wellarchitected/latest/generative-ai-lens/generative-ai-lens.html). 
This update features several new sections of the Well-Architected Generative AI Lens, including new best practices, advanced scenario guidance, and improved preambles on 
responsible AI, data architecture, and agentic workflows.

The AWS Well-Architected Framework provides architectural best practices for designing and operating [generative AI](https://aws.amazon.com/generative-ai/) workloads on AWS. 
The Generative AI Lens uses the Well-Architected Framework to outline the steps for performing a Well-Architected Framework review for your generative AI workloads.

![](/images/blog-6/image-1.png)

The Generative AI Lens provides a consistent approach for customers to evaluate architectures that use large language models (LLMs) to achieve their business goals. This lens addresses 
common considerations relevant to model selection, prompt engineering, model customization, workload integration, and continuous improvement. Specifically excluded from the Generative AI Lens 
are best practices associated with model training and advanced model customization techniques. We identify best practices that help you architect your cloud-based applications and workloads 
according to AWS Well-Architected design principles gathered from supporting thousands of customer implementations.

The Generative AI Lens joins a collection of Well-Architected lenses published under
[AWS Well-Architected Lenses](https://aws.amazon.com/architecture/well-architected/?wa-lens-whitepapers.sort-by=item.additionalFields.sortDate&wa-lens-whitepapers.sort-order=desc&awsm.page-wa-lens-whitepapers=1&wa-guidance-whitepapers.sort-by=item.additionalFields.sortDate&wa-guidance-whitepapers.sort-order=desc). 
For more information on the lens itself, check out the [launch announcement post](https://aws.amazon.com/blogs/architecture/announcing-the-aws-well-architected-generative-ai-lens/).

## What has changed in the updated Generative AI Lens?

The updated Generative AI Lens incorporates several new additions for customers to review. These additions keep the lens on-pace with the rapidly growing area of generative AI, helping customers 
stay up to date with architectural best practices.

### Amazon SageMaker HyperPod guidance

The updated lens features additional guidance for users of [Amazon SageMaker HyperPod](https://aws.amazon.com/sagemaker/ai/hyperpod/). SageMaker HyperPod is a highly resilient model training and hosting 
service that you can use to orchestrate complex, long-running generative AI workflows in the cloud. These workflows could be foundation model pre-training or serving model inference at scale.

We are excited to announce additional guidance for customers using SageMaker HyperPod in the Generative AI Lens. This guidance is built into the existing best practices, expanding the guidance for covered 
services to include SageMaker capabilities. This guidance joins the existing guidance on [Amazon Bedrock](https://aws.amazon.com/bedrock/), [Amazon Q Business](https://aws.amazon.com/q/business/), 
[Amazon Q Developer](https://aws.amazon.com/q/developer/), and [Amazon SageMaker AI](https://aws.amazon.com/sagemaker/ai/).

### Responsible AI preamble
The updated responsible AI preamble now includes a detailed discussion on the eight core dimensions of [responsible AI](https://aws.amazon.com/ai/responsible-ai/) as described by AWS. 
Customers can now learn more about the eight dimensions of responsibly developed AI systems directly within the lens. This is required reading for customers in all stages of their generative AI journey.

### Data architecture preamble
The updated data architecture preamble reviews strategic considerations associated with a modern data architecture supporting generative AI workloads. This section provides customers with a view into 
the high-level decisions and considerations needed to architect a data system that services generative AI workloads.

### Agentic AI preamble
New to the generative AI lens is the agentic AI preamble. Agentic systems, while technically classified as a subset of distributed computing, play an important role in modern generative AI workloads. 
This preamble introduces customers to a sampling of architecture paradigms common in agentic systems powered by foundation models.

### Scenarios
The Generative AI Lens now includes eight architecture scenarios. These scenarios cover a range of common generative AI powered business applications, including autonomous call centers, knowledge 
worker co-pilots, and multi-tenant generative AI service systems. The scenario section provides specific guidance for applying generative AI technologies to common business problems. The following image 
is an example of one of the new scenarios now included in the Generative AI Lens.

![](/images/blog-6/image-2.png)

## Who should use the Generative AI Lens?
The Generative AI Lens is useful to many roles. Business leaders can use this lens to acquire a broader appreciation of the end-to-end implementation and benefits of generative AI. Data scientists and 
engineers can read this lens to understand how to use, secure, and gain insights from their data at scale. Risk and compliance leaders can understand how generative AI is implemented responsibly by providing 
compliance with regulatory and governance requirements.

## Next steps
The updated [Well-Architected Generative AI Lens](https://docs.aws.amazon.com/wellarchitected/latest/generative-ai-lens/generative-ai-lens.html) is available now. Use the lens as a framework to verify that your 
generative AI workloads are architected with operational excellence, security, reliability, performance efficiency, cost optimization, and sustainability in mind.

If you require support on the implementation or assessment of your generative AI workloads, please contact your AWS Solutions Architect or Account Representative.

Special thanks to everyone across the AWS Solution Architecture, AWS Professional Services, and Machine Learning communities who contributed to the updated Generative AI Lens. These contributions encompassed 
diverse perspectives, expertise, backgrounds, and experiences in developing the new AWS Well-Architected Generative AI Lens.

For additional reading, refer to the [AWS Well-Architected Framework and pillar whitepapers](https://aws.amazon.com/architecture/well-architected/?wa-lens-whitepapers.sort-by=item.additionalFields.sortDate&wa-lens-whitepapers.sort-order=desc&wa-guidance-whitepapers.sort-by=item.additionalFields.sortDate&wa-guidance-whitepapers.sort-order=desc), 
or use the [AWS Well-Architected Machine Learning Lens](https://docs.aws.amazon.com/wellarchitected/latest/machine-learning-lens/machine-learning-lens.html) and its custom lens accessible from the 
AWS Well-Architected Tool.

