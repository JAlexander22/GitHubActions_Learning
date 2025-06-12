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


## On Push
Once a commit is made, it will auto trigger the pipeline
on:
  push:
    branches:
      - main

# Information Pipeline usage
NOTE: When making running workflow manually, you might need to refresh the page to view executions

NOTE: World flows are tied to repositories, you can use mutliple workflows for Repos.

## Pipeline Options
You can assidne options for your pipeline. not as clean as AzureDevOp Options and choices.
Set in the "on:" section. 

on:
  workflow_dispatch:
    inputs:
      action:
        description: 'Choose the action to perform: create or delete the file'
        required: true
        default: 'create'
        options:
          - 'create'
          - 'delete'

This is selected when running the pipeline in the *Action* section. 


### Create / Delete / Modifiy 
You need to add in Creditials to Add or delete anything from the Repo, even from with the pipeline. For example.
GithubLearning/
│
├── .github/
│   └── workflows/
│       └── <workflow-file.yml>  
│
├── Files/                      
│   └── <file1.txt>             
│   └── <file2.txt>             
│
├── .gitignore                  
└── README.md                   

If i wanted to add or modifiy this directory i would need to add

 - name: Set up Git user
        run: |
          git config --global user.name "GitHub Actions"
          git config --global user.email "actions@github.com"

   
      - name: Commit and push changes
        run: |
          git add -A  # Add all changes (file creation/deletion)
          git commit -m "Update file: $fileName" || echo "No changes to commit"  # Avoid failure if no file was created
          git push
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }} 

To authenticate.