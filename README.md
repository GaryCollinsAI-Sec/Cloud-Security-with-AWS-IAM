<h1>Cloud Security with AWS IAM</h1>

<h2>Objective</h2>
<p>
Designed and implemented a secure Identity and Access Management (IAM) framework enforcing the Principle of Least Privilege (PoLP) for managing Amazon EC2 resources. Reduced reliance on high-risk "Root" credentials by establishing granular access controls for users and groups.
</p>

<hr>

<h2>Skills Learned</h2>
<ul>
  <li>Authored complex IAM JSON policies with Allow and Explicit Deny logic</li>
  <li>Implemented Attribute-Based Access Control (ABAC) using resource tags</li>
  <li>Applied Principle of Least Privilege (PoLP) to user permissions</li>
  <li>Provisioned and managed Amazon EC2 instances, including AMI selection and instance types</li>
  <li>Securely managed SSH key pairs (.pem) and IAM credentials</li>
  <li>Designed workflows for separation of duties and secure authentication</li>
  <li>Performed security validation and failure testing to confirm proper access enforcement</li>
</ul>

<hr>

<h2>Tools Used</h2>
<ul>
  <li>AWS IAM: Create users, groups, and define JSON-based security policies</li>
  <li>AWS EC2: Provision and host virtual Linux servers</li>
  <li>Key Pair Generator (.pem): Secure authentication for EC2 instances</li>
</ul>

<hr>

<h2>Steps</h2>

<h3>Ref 1 – Provisioning EC2 Instances</h3>
<p>Provisioned two t3.micro EC2 instances to simulate "Development" and "Production" environments. Created a custom IAM policy using ABAC granting full control over instances tagged Env: development and read-only visibility account-wide. Explicit deny on tagging prevents bypassing security boundaries.</p>
<img width="905" height="463" src="https://github.com/user-attachments/assets/3da69710-c24c-4fc3-beaa-8a4e3f51a874" />


<h3>Ref 2 – IAM Policy Implementation</h3>

<p>Applied ABAC-based IAM policy to regulate intern access. Full EC2 management limited to Env: development-tagged resources. Describe permissions granted account-wide, with explicit deny on tagging to prevent privilege escalation.</p>
<img width="869" height="592" src="https://github.com/user-attachments/assets/87054e40-d027-4908-baa0-c4d59222ac07" />

<h3>Ref 3 – Account Alias & Policy Enforcement</h3>


<p>Created a custom Account Alias for a human-readable sign-in URL. Implemented ABAC IAM policy to strictly regulate intern access. Policy allows full EC2 management only for Env: development resources, with account-wide read-only visibility and explicit deny on tagging actions.</p>

<img width="589" height="343" src="https://github.com/user-attachments/assets/5cce14d6-bc70-4e4c-88b9-9e3a081a3179" />


<h3>Ref 4 – Authorization Failure Testing</h3>

<p>Tested the PoLP by logging in as the IAM user and attempting to stop the "Production" instance. Triggered Authorization Failure, confirming the policy successfully blocked unauthorized actions.</p>

<img width="885" height="371" src="https://github.com/user-attachments/assets/f5d88596-27ab-4ca3-8685-a75ede4a8947" />


<h3>Ref 5 – Final Validation</h3>

<p>Validated ABAC and PoLP: custom Account Alias, two t3.micro instances, and JSON policy restricted intern access to Env: development resources. Testing confirmed Production instance blocking. Highlighted AWS behavior: tag matches must be literal, and explicit deny prevents bypassing security boundaries.</p>

<img width="881" height="354" src="https://github.com/user-attachments/assets/a7bcdd9a-7182-4199-91a4-915609462b49" />

