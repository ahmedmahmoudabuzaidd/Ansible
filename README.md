# Ansible Automation for Sonatype Nexus

![Ansible Banner](./ansible.jfif)

## What I Did in This Project

In this repository, I used **Ansible** to automate the deployment and configuration of **Sonatype Nexus Repository Manager**. The main tasks I implemented include:

- Provisioning a Nexus server on a target host(s) defined in the `inventory` folder.  
- Installing the required system dependencies (e.g. Java) to run Nexus.  
- Downloading and installing Nexus OSS (or a specific Nexus version) on the target machine.  
- Setting up Nexus as a service: configuring systemd (or equivalent) so Nexus runs automatically and reliably.  
- Configuring Nexus repositories (e.g., Maven, Docker, or other formats) via Ansible tasks or API calls.  
- Setting up blob stores (storage) for Nexus artifacts, enabling persistent storage.  
- Managing Nexus credentials and admin password (potentially using Ansible Vault so secrets are encrypted).  
- (Optionally) configuring cleanup policies, security settings, or roles/users in Nexus to enforce access control.  

By defining everything in **playbooks** and **roles**, I created a repeatable, idempotent, and version-controlled way to deploy Nexus across environments.

## Why Use Ansible to Deploy Nexus

Using Ansible for Nexus deployment brings a number of advantages:

1. **Infrastructure as Code**  
   Your Nexus deployment is codified: installation steps, configuration, and policies are all written as Ansible playbooks and roles. This makes the setup repeatable, auditable, and maintainable.

2. **Idempotency**  
   Ansible ensures that when you run your playbooks multiple times, you don’t break things — it only applies changes when needed, preserving Nexus’s current desired state.

3. **Scalability & Consistency**  
   If you have multiple Nexus instances (e.g., for dev, staging, production), Ansible ensures they are configured in the same way. This avoids “snowflake” servers with drifted settings.

4. **Security & Secrets Management**  
   Using **Ansible Vault**, you can safely manage sensitive data such as admin passwords or license keys. This keeps secrets out of plain text in your git repository.

5. **Automation of Repetitive Tasks**  
   Tasks like creating blob stores, setting up repositories, or configuring cleanup policies that are error-prone when done manually can be automated reliably using Ansible. This saves time and reduces human error.

6. **Flexibility and Extensibility**  
   You can extend your Ansible roles to include future Nexus features: e.g., provisioning new repository types (PyPI, npm, Docker), integrating with LDAP or other authentication backends, or managing backups and snapshots.

7. **Integration with CI/CD**  
   Because everything is scripted, you can integrate your Ansible deployment into your CI/CD pipelines. For example, you can run a playbook after you build a new Nexus version, or as part of a “bootstrap infrastructure” job.

## How to Use This Repository (Getting Started)

1. Clone this repository
   
   git clone https://github.com/ahmedmahmoudabuzaidd/Ansible.git
   cd Ansible

2. Configure the inventory
   In the inventory folder, define the target hosts for your Nexus deployment. For example, add your Nexus server under a group like [nexus].

3. Set variables

   Use group or host vars files to define Nexus-related variables (e.g., nexus_version, nexus_install_dir, admin password).

   Use Ansible Vault to encrypt sensitive variables, such as nexus_admin_password.

4. Run the playbook
   ansible-playbook -i inventory/web.yml playbooks/sonatype-nexus.yml --ask-become-pass



## Benefits Gained in My Project

Automated Setup: Reduced the time to provision a Nexus instance from manual installation (~30–60 minutes) to a few minutes.

Reliability: Each run produces the same result — no manual misconfigurations.

Maintainability: Future updates (e.g., upgrading Nexus) can be automated through Ansible.

Security: Passwords and secrets are stored securely using Ansible Vault.

Scalability: New environments (dev, QA, prod) can be provisioned with the same playbook, reducing drift and ensuring parity.
