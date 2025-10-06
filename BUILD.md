# GitHub Actions Build Workflow

This repository includes a GitHub Actions workflow to build both the .NET and Angular applications.

## Build Workflow (`build.yml`)

**Trigger:** Push to `main`/`develop` branches, Pull Requests to `main`, Manual dispatch

This workflow builds both the Angular client and .NET server applications in a single job:

### Build Steps:
1. **Checkout code** - Gets the latest source code
2. **Setup .NET 8.0** - Installs .NET SDK
3. **Setup Node.js 20.x** - Installs Node.js with npm caching
4. **npm ci** - Installs Angular dependencies from package-lock.json
5. **npm run build** - Builds the Angular application
6. **dotnet restore** - Restores .NET dependencies
7. **dotnet build** - Builds all .NET projects in Release configuration
8. **dotnet publish** - Publishes the server application
9. **Upload artifacts** - Uploads both Angular dist and .NET publish folders

## Build Artifacts

The workflow uploads build artifacts that include:
- Published .NET server application (`./publish/`)
- Built Angular distribution files (`./angularapp2.client/dist/`)

Artifacts are retained for 30 days and can be downloaded from the GitHub Actions interface.

## Manual Execution

You can manually trigger the workflow from the GitHub Actions tab:
1. Go to the "Actions" tab in the repository
2. Select "Build and Publish" workflow
3. Click "Run workflow"
4. Choose the branch and click "Run workflow"

## Development

### Prerequisites
- .NET 8.0 SDK
- Node.js 20.x
- npm

### Local Build Commands
```bash
# Build Angular project
cd angularapp2.client
npm ci
npm run build

# Build .NET projects
dotnet restore
dotnet build --configuration Release
dotnet publish AngularApp2.Server/AngularApp2.Server.csproj --configuration Release --output ./publish
```

### Project Structure
- `AngularApp2.Server/` - ASP.NET Core Web API
- `angularapp2.client/` - Angular client application
- `ClassLibrary1/` - Shared .NET class library
- `.github/workflows/build.yml` - GitHub Actions workflow definition