# Excercise-2
Blue/Green deployment using jenkins/ Gitlab etc on K8s.

Blue/Green deployment is a strategy that allows you to deploy new application versions with minimal risk and zero downtime. This is commonly achieved in Kubernetes using Jenkins or GitLab CI/CD pipelines, where the new (green) version of the application is deployed alongside the current (blue) version. Once validated, traffic is switched to the new version. Here’s how to implement Blue/Green deployment on Kubernetes using Jenkins or GitLab:

Prerequisites:
1. Kubernetes Cluster: A running Kubernetes cluster with access configured.
2. CI/CD Pipeline: Jenkins or GitLab CI/CD is installed and configured.
3. Kubernetes Credentials: Cluster credentials configured on Jenkins or GitLab for deployment access.
4. Ingress Controller: For managing external traffic routing (optional but recommended).

Kubernetes Manifest for Blue/Green Deployment

Step 1: Define Services and Deployments
Service: Define a service that will route traffic to either the Blue or Green deployment.
Deployments: Create two deployments, app-blue and app-green, for Blue and Green versions.

Step 2: CI/CD Pipeline Configuration
Jenkins Pipeline (Jenkinsfile)
GitLab CI/CD (.gitlab-ci.yml)

Explanation
Deploy Blue Version: The initial blue deployment runs the current version of the application.
Deploy Green Version: Deploy the green version with updated features.
Test Green Version: Run tests on the green deployment to ensure everything works as expected.
Switch Traffic to Green: Update the service to route traffic to the green version.
Cleanup Blue: After the successful switch, delete the blue deployment.

Optional Step: Rollback Mechanism
Add a rollback stage to your pipeline to switch traffic back to the blue version if needed by running:

==> kubectl patch service app-service -p '{"spec":{"selector":{"version":"blue"}}}'



