# Assessment

Azure Functions is a serverless platform that can be used to develop event-driven apps on Linux.

## Steps:
1. Create new repository on GitHub.
2. Set up Function App to deploy via CI/CD
3. The yaml file consists of 2 jobs. It includes all the procedures needed to create every piece of content and upload it to the cloud.
   - Build: Responsible for packaging the project into a zipped filed ready for deploy. This is where it connects to the host, configure      environment and build the project.
   - Deploy: Uploads and update the built project to the cloud.

## Security best practices:
1. Use of Secrets for Sensitive Data:
   - publish-profile: The Azure publish profile is stored in GitHub Secrets               (secrets.AZUREAPPSERVICE_PUBLISHPROFILE_B78793F730C14925918500A4B24477D1).
   - This prevents sensitive information from being exposed in the repository or workflow files.
2. Artifact Management:
   - Upload and Download Artifacts: Artifacts are uploaded in the build job and downloaded in the deploy job. This helps in ensuring     that only the necessary files are deployed and maintains a clear separation between build and deployment processes.
3. Scoped Environment:
   - environment: The deploy job specifies an environment (name: 'Production'). GitHub Actions environments allow you to configure specific security policies and approvals for deployments, adding a layer of control over production deployments.
4. Dependency Management:
   - Virtual Environment: Creating a virtual environment (python -m venv venv) isolates dependencies, reducing the risk of dependency- related vulnerabilities.
5. Avoiding Secrets in Logs:
   - zip and unzip: Ensure that no sensitive data or secrets are included in the zipped files or logs. Consider sanitizing or filtering logs if necessary to avoid accidental exposure.
6. Latest Versions:
   - The workflow uses up-to-date versions of actions (e.g., actions/checkout@v4, actions/setup-python@v4). Using the latest versions helps in benefiting from security patches and improvements.
