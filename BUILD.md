# GitHub Actions Build Workflows

This repository includes several GitHub Actions workflows to build the .NET and Angular applications.

## Available Workflows

### 1. Main Build Workflow (`build.yml`)
**Trigger:** Push to `main`/`develop` branches, Pull Requests to `main`

This workflow builds both the Angular client and .NET server applications:
- Sets up Node.js 20.x and .NET 8.0
- Installs Angular dependencies with npm
- Builds the Angular application (`ng build`)
- Runs Angular tests with ChromeHeadless
- Restores .NET dependencies
- Builds .NET projects (ClassLibrary1 and AngularApp2.Server)
- Runs .NET tests
- Publishes the server application
- Uploads build artifacts

### 2. .NET Only Build Workflow (`build-dotnet-only.yml`)
**Trigger:** Manual dispatch, Push to specified paths

This workflow focuses on building only the .NET components:
- Builds ClassLibrary1 independently
- Builds AngularApp2.Server with skip Angular properties
- Runs .NET tests
- Publishes server application
- Uploads .NET artifacts

### 3. CI/CD Pipeline (`ci-cd.yml`)
**Trigger:** Push to `main`/`develop` branches, Pull Requests, Manual dispatch

Advanced pipeline with parallel builds:
- **Angular Build Job**: Builds and tests Angular application independently
- **.NET Build Job**: Builds and tests .NET applications independently
- **Integration Build Job**: Combines artifacts from both jobs
- Includes comprehensive caching and error handling
- Creates deployment packages

## Build Artifacts

All workflows upload build artifacts that include:
- Published .NET server application
- Built Angular distribution files
- Test results and coverage reports
- Build logs and summaries

Artifacts are retained for 30 days and can be downloaded from the GitHub Actions interface.

## Manual Execution

You can manually trigger the workflows from the GitHub Actions tab:
1. Go to the "Actions" tab in the repository
2. Select the workflow you want to run
3. Click "Run workflow"
4. Choose the branch and click "Run workflow"

## Development

### Prerequisites
- .NET 8.0 SDK
- Node.js 20.x
- npm

### Local Build Commands
```bash
# Build .NET projects
dotnet restore
dotnet build --configuration Release

# Build Angular project
cd angularapp2.client
npm install
npm run build
npm test
```

### Project Structure
- `AngularApp2.Server/` - ASP.NET Core Web API
- `angularapp2.client/` - Angular client application
- `ClassLibrary1/` - Shared .NET class library
- `.github/workflows/` - GitHub Actions workflow definitions