# preview-test

What solutions does Preview Environment solves?

We can consider a scenario where a complex product is being developed by dozens of engineers working on different features of a product. Not only the development environment is the same, but the staging environment is also shared. As different features are merged into the shared environment, they break the code. So QA has to wait until this is fixed. 

A feature or bug fix may be working perfectly on the developer’s own machine, but there is no way for the QA team to test that one feature in isolation. 

This problem is intensified when the product has a lot of integrations and different data sources. 

We simply cannot provision so many different environments on time. If developers keep using the same shared staging environment, it will take lot of time to deliver a mature product to the market.

This is where the concept of preview environments comes into play.






Automating Feature Dynamic Deployments: A Streamlined Workflow with GitHub Actions, ArgoCD  and Kubernetes.

Preview environment is being created through an automated pipeline that leverages GitHub Actions, Kubernetes, and GitOps principles to manage, test and deploy new features seamlessly. 

The Pipeline Workflow
Here’s a step-by-step breakdown of how the pipeline handles the code from creating PR to deployment:

1. Triggering GitHub Actions
GitHub Actions, a powerful CI/CD tool, is configured to trigger a build process if the PR created with prefix matches feature/**. This ensures that only feature-related PR activate the pipeline, keeping the process streamlined and efficient.

2. Updating Kubernetes Manifests and AWS ECR
Once triggered, the pipeline updates the Kubernetes manifests in the GitOps Repo to reflect the changes in the code. Additionally, it updates the AWS ECR image to include the latest version of the application. These manifests define how applications are deployed and managed within the Kubernetes cluster.

3. ArgoCD Manages New Pull Request Applications and Pull Request Environments
ArgoCD continuously monitors the GitOps repository for any new applications. When it detects a new application, it creates a new pull request environment. ArgoCD then updates the manifests associated with that specific pull request environment based on the application's specifications.

4. Creating a Pull Request Comment
As a final touch, a comment is added to the pull request on GitHub. This comment provides the environment URL where the new feature is deployed and details the time taken to spin up the new feature environment. This transparency helps developers track the deployment progress and troubleshoot any issues if they arise.




Automated Cleanup of Dynamic Feature Environments: Streamlining PR Management with GitHub Actions and ArgoCD

Here’s how an automated pipeline using GitHub Actions and ArgoCD can simplify and streamline this process.

The Automated Teardown Process
1. Triggering the Cleanup Process

The automation process kicks off when a pull request with the designated prefix "feature/**" is either closed or drafted. This action serves as the signal to initiate the cleanup sequence. 

2. Commenting on the PR

As part of the workflow, a comment is automatically added to the PR. This comment informs developers that the "feature env" has been closed and is no longer active. This step ensures clear communication and documentation of the environment's status.

3. Interaction with ArgoCD & Deleting the Application

The workflow then interfaces with ArgoCD, a tool designed to manage applications on Kubernetes. ArgoCD takes action by deleting the application linked to the closed PR. This step is crucial for ensuring that no obsolete applications remain in the system, which could otherwise consume resources and create unnecessary overhead.

4. Tearing Down Resources

Finally, the resources used by the application in Kubernetes are dismantled. This teardown process involves removing any pods, services, and other infrastructure components associated with the feature environment. By cleaning up these resources, the system remains efficient and clutter-free.