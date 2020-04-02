---
post: page
title: CI Best practices
tags: [CI]
comment: true
---


Continuous Integration Best Practices
While sifting through Wikipedia, one occasionally finds pearls of wisdom amid the endless sea of trivia facts. The section on continuous integration (CI) best practices is particularly well done and informative. 

■ Maintain a code repository— getting yourself familiar with GitHub is essential for working.

■ Automate the build—Setting up build automation is the goal 

■ Make the build self-testing—Test-Driven Development isn’t just something we do once in a while, it is part of the way of the cloud, as you’ll see in Chapter 5. All code we write is tested, and CI servers must execute those tests.

■ Commit to the baseline every day—Another virtue of the way of the cloud is release early, release often. This is reflected in CI best practices by constantly committing to the baseline. The longer you wait before committing to the baseline (the branch that produces production releases), the less confidence you have and the more you fear the release process.

■ Build every commit—Every time you check in code, your CI tool should execute a build, which involves running unit tests, evaluating test coverage, and often running static analysis tools.

■ Keep the build fast—If your build is too slow or cumbersome to automate, this is a smell that something else may be wrong. Your builds should be fast, so you can see them pass Continuous Integration with Wercker 
 
 Delivering Continuously

■ Make it easy to get deliverables—As we mentioned in the previous section, our deliverables will all be exposed in Docker Hub, making it brain-dead simple to fetch our build artifacts. Wercker doesn’t force you to use Docker Hub, however, as you can pull build artifacts from the website or the command-line tools.

■ Everyone can see the results of the latest build—If no one knows the build is failing, there is absolutely no reason to have automated builds. If a build goes red, it should immediately become top priority to make it go green again. Wercker makes it easy to see the results of builds, but also has a client application that will notify you instantly when builds fail. It’s important that your tool make build status visible, but it’s up to you and your team to build the discipline to treat failed builds with the severity they demand.

■ Automate deployment— use Wercker to deploy Docker images automatically at the end of a successful build. If deploying is a manual process, it becomes an error-prone process. Manual deployments are slow and cumbersome, and teams tend to avoid them, leading to longer delays between deploys and a loss of confidence.
