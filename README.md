# Cloud Security with AWS IAM

## Objective

To design and implement a secure Identity and Access Management (IAM) framework that enforces the Principle of Least Privilege (PoLP) for managing Amazon EC2 resources. This lab demonstrates how to move away from using high-risk "Root" account credentials by establishing granular access controls for users and groups.

### Skills Learned

- Identity & Access Management (IAM): Authored complex JSON policy documents utilizing Allow and Explicit Deny logic to enforce the Principle of Least Privilege.
- Attribute-Based Access Control (ABAC): Engineered dynamic security permissions by using resource tags (Env: development) to define access boundaries.
- Principle of Least Privilege (PoLP): Authoring and attaching specific IAM policies to ensure users only have the access necessary for their job function.
- Infrastructure as a Service (IaaS): Provisioning and managing Amazon EC2 instances, including AMI selection and instance type configuration.
- Credential Management: Securely managing SSH Key Pairs (.pem) and IAM user credentials while avoiding the use of the high-risk Root account.
- Security Architecture: Designing workflows that prioritize the separation of duties and secure authentication.
- Security Validation & Auditing: Conducted "Failure Testing" to verify that authorization logic correctly blocks unauthorized actions, even when resource naming conventions are similar.



### Tools Used

- IAM (Identity and Access Management): Used for creating users, groups, and defining JSON-based security policies.
- EC2 (Elastic Compute Cloud): Used to provision and host the virtual Linux server.
- Key Pair Generator (.pem): AWS tool used to create the asymmetric encryption keys for secure authentication.


## Steps
drag & drop screenshots here or use imgur and reference them using imgsrc

Every screenshot should have some text explaining what the screenshot is about.

Example below.


*Ref 1: Cloud security


<img width="905" height="463" alt="Screenshot 2026-02-03 173737" src="https://github.com/user-attachments/assets/3da69710-c24c-4fc3-beaa-8a4e3f51a874" />

In this lab, I provisioned two t3.micro EC2 instances to simulate a real-world split between "Development" and "Production" environments. To secure these resources, I engineered a custom IAM policy using Attribute-Based Access Control (ABAC), which granted a hypothetical intern full control over instances tagged Env: development. The policy allowed account-wide read-only visibility via Describe permissions but utilized an explicit deny on all tagging actions. This prevented the user from bypassing security boundaries by re-tagging production assets to gain unauthorized access.

*Ref 2: Cloud security

<img width="869" height="592" alt="Screenshot 2026-02-03 163506" src="https://github.com/user-attachments/assets/87054e40-d027-4908-baa0-c4d59222ac07" />

This lab implemented a secure IAM policy using Attribute-Based Access Control (ABAC) to regulate an intern's access. The policy grants full EC2 management power only to resources tagged Env: development, while providing account-wide read-only visibility via Describe permissions. To prevent privilege escalation, an explicit deny on tagging actions ensures the intern cannot bypass these restrictions by re-tagging production assets.


*Ref 3: Cloud security

<img width="589" height="343" alt="Screenshot 2026-02-03 165629" src="https://github.com/user-attachments/assets/5cce14d6-bc70-4e4c-88b9-9e3a081a3179" />

In this lab, I implemented a secure AWS environment by first creating a custom Account Alias to replace the 12-digit Account ID, providing a more professional and human-readable sign-in URL for users. I then engineered an IAM policy using Attribute-Based Access Control (ABAC) to strictly regulate a hypothetical intern's access. This policy allows the intern full EC2 management power only for resources tagged Env: development, while providing account-wide read-only visibility. To ensure high security, I included an explicit deny on all tagging actions, preventing the intern from bypassing restrictions by re-tagging production assets.


*Ref 4: Cloud security

<img width="885" height="371" alt="Screenshot 2026-02-03 173842" src="https://github.com/user-attachments/assets/f5d88596-27ab-4ca3-8685-a75ede4a8947" />

To verify the Principle of Least Privilege, I logged in as the IAM user via the custom Account Alias and attempted to stop the "Production" instance. This triggered an immediate Authorization Failure, confirming that the JSON policy successfully blocked unauthorized actions on resources lacking the Env: development tag. This real-world test proved that the security boundaries effectively protect critical infrastructure from junior-level or unauthorized modifications.

*Ref 5: Cloud security

<img width="881" height="354" alt="Screenshot 2026-02-03 175618" src="https://github.com/user-attachments/assets/a7bcdd9a-7182-4199-91a4-915609462b49" />

This lab successfully demonstrated the Principle of Least Privilege by implementing Attribute-Based Access Control (ABAC) within a multi-instance AWS environment. After establishing a custom Account Alias (nextwork-alias-gary) and launching two t3.micro instances, I applied a JSON policy designed to restrict a hypothetical intern's management capabilities to resources specifically tagged with Env: development. Real-world validation testing confirmed the policy’s effectiveness, as the intern user was correctly blocked from stopping the "Production" instance. Interestingly, the "Development" instance was also blocked, providing a critical lesson in cloud security: AWS policies require a literal metadata tag match rather than just a matching resource name, and the inclusion of an explicit deny on tagging prevents users from circumventing these strict security boundaries.igh
