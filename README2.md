# How Can You Create a Workflow with GitHub Actions?

## What is GitHub Actions?
GitHub Actions makes it easy to automate all your software workflows, now with world-class CI/CD. Build, test, and deploy your code right from GitHub. Make code reviews, branch management, and issue triaging work the way you want.
## GitHub Action is just another tool?
- Use same tool instead of third-party integration
- Setup the pipeline is easy
- Tool for developers
- Integraion with another technologies is important and hard to manage but you don't need this in GitHub action CI/CD pipeline.
##  Create a New Repository
I logged into my GitHub account and created a public repository named 'p13-MacOS_CI_github_actions'.

I pushed my java project using gradle in my local to my repository.

I clicked on the actions tab in my GitHub repo. On this page, you can see the worklows of additional very popular services. Using them, you can build your application without having to write a workflow from scratch.

So I chose the workflow template named `Java with Gradle` here.
Automatically created `.github/workflows/gradle.yml` file under my project.


The `name` part is the field where the name of the workflow is written, it is optional.
The `on` part is required. Specifies how the Workflow will be triggered. I have organized my workflow so that it will be triggered when a push or pull request is made to the main branch.
The Jobs section shows the events that will run when the workflow is triggered.
First, I pulled my repostory with the syntax `- uses: actions/checkout@v2 # pull repository `. You can see the details of what operations are done behind this syntax by looking at the repository where this action is located.

In `runs-on`, I set the operating system on which my application will be built as `macOS-latest`.


```yaml
- name: Set up JDK 1.8
  uses: actions/setup-java@v1 # install java env
    with:
        java-version: 1.8 # java version
``` 
this action performs the installation of the java environment by looking at the version I have specified here.

```yaml
- name: Grant execute permission for gradlew
  run: chmod +x gradlew
``` 
Unlike the others, this is a linux command. I converted the Gradlew file to executable and then

```yaml
- name: Build with Gradle
  run: ./gradlew build
``` 
 I did the build process with the command.


```yaml
- uses: docker-practice/actions-setup-docker@master
- run: set -x

- name: Build and Push Docker Image
  uses: mr-smithers-excellent/docker-build-push@v4
  with:
    image: drerdemsezgin/flask-app #docker id and repository name
    registry: docker.io
    username: ${{ secrets.DOCKER_USERNAME }} #docker hub credentials for username
    password: ${{ secrets.DOCKER_PASSWORD }} #docker hub credentials for password
```

For adding secret to your repository repository>secrets>new repository secret and Name=DOCKER_USERNAME, Value=drerdemsezgin
Name=DOCKER_PASSWORD, value=<MyPassword>


## Where does this code run?
- Managed by GitHub.
- Each job in a workflow runs in a fresh environment.
