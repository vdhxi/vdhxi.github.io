---
title: "Blog 4"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 3.4. </b> "
---

# DISA STIG for Amazon Linux 2023 is now available

Today, we announce the availability of a Security Technical Implementation Guide (STIG) for [Amazon Linux 2023 (AL2023)](https://aws.amazon.com/linux/amazon-linux-2023/), 
developed through collaboration between Amazon Web Services (AWS) and the [Defense Information Systems Agency](https://public.cyber.mil/stigs/) (DISA). The STIG guidelines are important 
for [U.S Department of Defense](https://www.defense.gov/) (DOD) and Federal customers needing strict security compliance derived from the
[National Institute of Standards and Technology (NIST) 800-53](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final) and related documents. This new technical implementation guide provides 
detailed Operating System (OS) security hardening configurations for organizations deploying AL2023 in DOD environments and other agencies requiring DISA STIG alignment. The AL2023 STIG 
provides customers with access to an OS guide that complies with stringent government security standards. This guide for implementing STIG configurations will streamline security processes 
for organizations seeking robust cybersecurity controls, whether they are needed to maintain DOD compliance or voluntarily adopting these best security practices to enhance their security posture.
---

## Implementing the AL2023 DISA STIG with AWS

AWS Systems Manager (SSM) and EC2 Image builder offer native solutions for implementing the AL2023 DISA STIG configurations in your environment. For customers with existing AL2023 EC2 workload, 
they can utilize AWS Systems Manger (SSM) to streamline the STIG implementation. For customers who would like to build STIG compliant AL2023 EC2 instances to use for deployment, they can utilize 
EC2 Image Builder and automate the application of the AL2023 DISA STIG.

## Building STIG-Compliant Images via EC2 Image Builder

Customers can utilize EC2 Image builder to enhance and streamline their implementation of the AL2023 DISA STIG. This integrated approach significantly reduces the operational overhead traditionally 
associated with maintaining STIG compliance. Therefore, our customers can focus on their core missions while maintaining the highest security standards. Our customers can use AWS EC2 Image Builder’s 
existing Linux hardening components, which now support AL2023 Category I, II, and III findings to automatically create STIG-compliant AL2023 EC2 images with minimal manual intervention. This automation 
significantly reduces the time and effort typically needed for security hardening implementations. The EC2 Image Builder Linux hardening component extends its proven capabilities to AL2023, providing 
the same streamlined security configuration process available for other Linux distributions. For more information, refer to the [Image Builder documentation](https://docs.aws.amazon.com/imagebuilder/latest/userguide/ib-stig.html).

## Automating the STIG for Existing Fleets via Systems Manager

For existing AL2023 EC2 instances, you can use AWS-managed SSM command documents to automate the implementation of the STIG configurations. . These command documents can be executed through the SSM console, 
API, or AWS Command Line Interface (AWS CLI). The key mechanism here is the AWS managed Systems Manager command document, which contains the pre-defined STIG configurations. By leveraging these command documents 
through Systems Manager execution capabilities, customers can systematically deploy and maintain AL2023 STIG configurations across their fleet of EC2 instances. This generates consistent security baselines that 
meet government and enterprise requirements. This solution is particularly effective for environments with existing AL2023 EC2 instances as it allows customers to implement STIG controls without rebuilding or 
redeploying instances. For more information about the command document, refer to [Apply STIG settings with Systems Manager](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-stig-ssm-cmd-doc.html) in the 
EC2 User Guide.

The AL2023 STIG represents the continued commitment of Amazon Linux to providing customers with the security tools and guidance they need to succeed in highly regulated environments. Amazon Linux, in collaboration with 
DISA is providing their customers with access to authoritative, government-validated security configurations that meet the most demanding compliance requirements.

Ready to implement AL2023 STIG in your environment? Explore our comprehensive documentation and begin streamlining your security compliance journey today. To learn more about STIG hardening for your EC2 instances, 
refer to [STIG compliance for your EC2 instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-configure-stig.html) and for STIG settings that are applied to EC2 Linux instances, refer to 
the [STIG settings for EC2 Linux instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-stig-settings.html#ec2-linux-os-stig). To apply STIG settings to your AL 2023 EC2 instance, 
[download the AL2023 DISA STIG](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-stig-downloads.html).