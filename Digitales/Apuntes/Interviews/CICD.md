# CI / CD

CI/CD is a method to frequently deliver apps to customers by introducing automation into the stages of app development. The main concepts attributed to CI/CD are continuous integration, continuous delivery, and continuous deployment. CI/CD is a solution to the problems integrating new code can cause

### Contnious Integration

Continuous Integration is a development practice where developers integrate code into a shared repository frequently, preferably several times a day. Each integration can then be verified by an automated build and automated tests. One of the key benefits of integrating regularly is that you can detect errors quickly and locate them more easily.

### Continuous Deployment

It is closely related to continuous integration and refers to keeping your application deployable at any point. It involves frequent, automated deployment of the master branch to a production environment following automated testing.

### Continuous Delivery

Continuous delivery is a software development practice that uses automation to speed the release of new code.

It establishes a process through which a developer’s changes to an application can be pushed to a code **repository** or **container registry** through automation.

## CI/CD Example on K8S

- Gitflow on a Github Repo
  
  - Branch a new `feature/users_login` from `develop`
  
  - Create a new Pull Request to `develop`
  
  - Send it to a friend to make a nice peer-review to your code.
  
  - Run some Pipes the Pull request.
    
    - Check Pull Request test coverage
    
    - Check total test coverage
    
    - Check harcoded  credentials
    
    - Inject variables/secret on buildtime
    
    - Check Linting and Code Quality
    
    - Check if the code builds.
  
  - Merge to `develop`
  
  - Branch a new `release/1.0` and create a new `release candidate (rc)` version. 
  
  - Perform some integration testing with that branch and see how it behaves.
    
    - Optionally branch a new `fix/bug#123` to fix some issues and merge back to `release/1.0`
    - If everything's ok merge into `master` that will automatically trigger the whole Jenkins / Github Actions pipeline where the application will be built

- Merging into `master` will automatically trigger the whole Jenkins / Github Actions pipeline to delivery de app automatically where the application (Docker Image) will be built and pushed to a Docker Registry
  
  - `docker build -t "myApp:v1"`
  
  - `docker push`

- Once the image is available the user can manually trigger the deployment depending the case this could be done automatically by the same Delivery Pipeline.
  
  - `kubectl apply ...`

- 
