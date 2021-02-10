# Deployment Strategies

A **deployment strategy** is a way to change or upgrade an application. The aim is to make the change without downtime in a way that the user barely notices the improvements. The most common **strategy** is to use a blue-green **deployment**.

### Recreate (All-In)

The old version is shut down; then, the new one is activated. This process is what happens when you have a simple server, and you update your web site.

### Blue-Green

The new version (the blue version) is brought up for testing and evaluation, while the users still use the stable version (the green version). When ready, the users are switched to the blue version. If a problem arises, you can switch back to the green version.

### Canary

The so-called canary is a candidate version of a service that catches some subset percentage of incoming requests (say, 1% of the users) to try out new features or builds. Teams can then examine the results, and if things go smoothly, gradually increase deployment to 100% of servers or nodes.

### A/B testing

A/B testing is similar to canary deployments, with one important difference. While canary deployments tend to focus on identifying bugs and performance bottlenecks, A/B testing focuses on gauging *user acceptance* of new application features.
