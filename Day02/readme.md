# AWS Security Group – Nautilus App Servers

The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the AWS cloud. Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive transition. To achieve this, they have segmented large tasks into smaller, more manageable units.

This granular approach enables the team to execute the migration in gradual phases, ensuring smoother implementation and minimizing disruption to ongoing operations. By breaking down the migration into smaller tasks, the Nautilus DevOps team can systematically progress through each stage, allowing for better control, risk mitigation, and optimization of resources throughout the migration process.

## Task

Create a security group under the **default VPC** with the following requirements:

* The name of the security group must be `devops-sg`.
* The description must be `Security group for Nautilus App Servers`.
* Add an inbound rule of type **HTTP**, with port `80`.
* Set the HTTP source CIDR range to `0.0.0.0/0`.
* Add another inbound rule of type **SSH**, with port `22`.
* Set the SSH source CIDR range to `0.0.0.0/0`.

## Requirements

* Create the resource only in the `us-east-1` region.
* AWS credentials are provided separately for the lab environment.
