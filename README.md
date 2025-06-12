# GitHubActions_Learning
Learning Github Actions how to utilize it and compare it to AzureDevOp

## Navigate to the Actions Tab
- Go to repository Page
- Select Actions Tab
- Create "Your own Workflow" Or Choose a template

## Action Runner
Action runner is the Agent used and installed on your machine. (_ensure all dependencies are installed)

### Creating an Agent
- In the Repo, Create a "Actions-Runner" Folder
- Change directory into the *Action-Runner* folder and run the following command
- On Github Webiste go to your Repo ,
- Settings / Actions Tab / Runners
- Choose Your operating System and follow the commands to downlaod and configure your Self hosted agent
- Runner Groups -  Organise multiple self-hosted runners for different environments ( Development, Testing , Production)  Or Target specific runners for certain workflows or jobs based on thier group. 

### Run as Service
- This will allow the Agent to run as a Service on your system.


## Self-Hosted
Add in Jobs: / Build: / runs-on: self-hosted. This tell GitHub to use self-hosted runner 

If you have muiltiple self-hosted runners you can define by tag
Jobs: / Build: / runs-on: [self-hosted, DEV]
### Example:
jobs:
  build:
    runs-on: [self-hosted, PHANTOM]  