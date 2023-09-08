# azurepipeline

# Readme for CI/CD Pipeline

This readme provides an overview of the Continuous Integration and Continuous Deployment (CI/CD) pipeline configuration for your project. This pipeline automates the building, testing, and deployment process of your applications.

## Pipeline Configuration

### Trigger

The pipeline is triggered on the following branches:

- `master`
- `staging`
- `develop`

### Pull Request Trigger

The pipeline is triggered on pull requests targeting the following branches:

- `develop`
- `staging`
- `master`

### Variables

- `latestTag`: This variable stores the latest Git tag in the repository.

### Jobs

#### Job 1: BuildAndTest

This job is responsible for building and testing the applications. It utilizes a matrix strategy to build and test multiple apps in parallel.

- **Matrix Configuration**: The matrix configuration defines two apps, `app1` and `app2`.

- **Virtual Machine Image**: The job runs on an `ubuntu-latest` virtual machine image.

##### Steps:

1. **Fetch Tags**: This step fetches Git tags to determine the latest tag.

2. **Install Dependencies**: Installs project dependencies for the specified app.

3. **Lint & Test**: Runs linting and testing for the specified app. If there's a latest tag, it uses affected commands to optimize the process.

4. **Build**: Builds the specified app. If there's a latest tag, it uses affected commands to optimize the process.

5. **Check Build Output**: Checks if the build output exists and sets a variable accordingly.

6. **Publish Build Artifacts**: Publishes build artifacts if the build was successful and there are generated files.

#### Job 2: Release

This job handles the deployment and release tasks based on the success of the BuildAndTest job and certain conditions.

##### Dependencies:

- Depends on the success of the `BuildAndTest` job.
- Executes if there are generated files.

##### Steps:

1. **Download Build Artifacts**: Downloads build artifacts from the BuildAndTest job.

2. **Deploy to Azure Static Web App**: Deploys the application to Azure Static Web App if the build is successful, the branch is `develop`, and there are generated files.

3. **Deploy Artifacts**: Placeholder for your deployment script.

4. **Tag Source Code**: Tags the source code with a production release tag when the branch is `master`.

## Usage

1. Ensure that your repository's CI/CD configuration matches the provided pipeline configuration.

2. Customize deployment scripts and other tasks as needed, especially in the "Deploy Artifacts" step.

3. Be mindful of the conditions specified in the pipeline to control when specific steps run.

4. Configure the pipeline's triggers and variables to align with your project's requirements.

## Notes

- This README is a template and should be customized to match your specific project and pipeline requirements.
- Make sure to keep your CI/CD pipeline configuration up-to-date as your project evolves.
