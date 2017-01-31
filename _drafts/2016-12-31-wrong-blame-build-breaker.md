---
published: false
layout: post
section-type: post
comments: true
date: '2016-12-31 16:30:23 +0530'
title: 21 Instances Where the Wrong Person Gets Blamed for a Build Failure
---

This is a continuation to my earlier post “[Is Chastising Build Breakers Correct?](http://vivekganesan.com/is-chastising-build-breakers-correct/)” in the spirit of practising Blameless CI.

In most of the teams that I have worked with, the build breaker is frowned upon, sometimes treated like a criminal. Until recently, even the Jenkins build monitor called the person who committed just before a failing build as a ‘culprit’.

Though there is no denying that developer’s inattention to detail causes some build failures but developer’s negligence is not the only cause of a build failure.

This drove me into writing a non-exhaustive list of ways, based on my experience, in which the wrong person gets blamed for a build failure just because he/she happened to be the last one to push a code change.

## Assumptions

### a. People Involved

Here are the names that I would like to give to the people involved in illustrations.

I - Myself, the sorry soul who gets blamed for the build failure
X - Previous Committer, who pushed a commit after my checkout

### b. Steps followed by developer to push new changes (assuming git)

1. I checkout the code
1. I make changes
1. I run tests
1. I commit
1. I push my commit to upstream (Rely on IntelliJ or IDE to rebase my commit on top of any commit that came in after my checkout - Essentially do a git pull and then a git push)

REMEMBER! It is very important and urgent for me to push as soon as the rebase happens or else someone will commit in the meantime and I have to rebase again. If you understand this fact clearly, there is no need to struggle to understand any items in the following list. 

The situation gets even more complicated if I have a pre-commit code review system like Gerrit, where I do not have control on how long it takes for a reviewer to give an approval.

Now that you know what the context is, here are the 21 instances. Oh wait! Remember! This is not an exhaustive list.

## 21 Instances Where ...

### Compilation Errors

1. I add a variable ‘myVar’ for some purpose. X also added a variable ‘myVar’ for a different purpose. This applies to names of class, method or any other identifier.
1. X deleted property/method of a class that my code uses.
1. X added an additional parameter to a method that my new code calls. This applies to removing/reshuffling parameters too.
1. X upgraded a library that the code is dependent on. My code calls a method that is unsupported in new version but supported in old version. This applies to downgrading versions too.

### Test Failures

1. I added a new test. X pushed code that does not pass my new test’s expectations
1. I write a test, taking some pre-conditions for granted, because that is always the case so far. X pushed a test, which while running, will mess with the expected pre-conditions of my new test. For example, test written by X might change a global variable to a value that will cause my new test to fail. This is not an issue in case of tech stacks which provide clean slate for each test.
1. I write a UI test that opens a dialog and checks its contents. X pushed a test that opens a modal dialog but forgot to close the modal dialog at the end of the test. This would prevent my test from even opening up my expected dialog.
1. I wrote an integration test that traverses the following classes : A-> B-> C. I wrote mocks for C. Meanwhile, X committed a test that mocks class B and let his test share my test’s environment. This is not an issue in case of tech stacks which provide clean slate for each test.

### Incorrect CI Configuration

1. Recent breaking change in CI Job configuration.
1. CI job generates an artifact/file based on the source files that I have in repository. I deleted a source file in the last commit. Expectation is that the generated file is also not present during building. But, CI job’s workspace still contains the last generated copy of the artifact, even if the source file is deleted from the repository. For example, I delete a class but my CI job has the .class file that was generated from the earlier build. Same is the case with typescript compilation from .ts files to .js files. This is usually a case where ‘not clean’ or incremental builds are performed (which is actually a good thing in some cases).
1. Till date, CI has been showing ‘green’ all time because of misconfiguration. Just before I pushed my commit, the CI job was corrected to show the actual results.
1. Another job is configured to use/modify the directory that my job also uses. Namespacing/isolation issues.

### Build Environment Issues

1. The test database ran out of space just before my commit. This does not apply to cases where a database is created fresh with every build.
1. The CI server ran out of disk space just before my commit.
1. The database/external service used by the CI job to run the build/tests was upgraded just before my commit.
1. Changes were being done on Access Control Lists of environments during the time my commit was being validated.
1. AWS has forcefully terminated the EC2 instances used by CI job for some reason just when my commit was being validated. (For example, doubtful malicious activity, overdues, etc)

### Just Setting up - Starting Troubles

1. The step to run tests in CI job was enabled just before my commit
1. X committed a test configuration file (especially something like karma.conf.js file) that would include my new files and fail when my new files are run inside tests.
1. CI job was using a trial version of a software involved in the build process till date. Now upgraded to paid version which enforces more stringent standards.
1. New rule added to SONAR (or any static code check) just before my commit.
1. There are ways to avoid a lot of the above wrong failures. But, rarely, many of them fall under the control of an individual developer. These preventive measures either end up with architects or the maintainers of CI environments, who, in fortunate cases, are part of development teams (Devops anyone??) and in most cases not.

Moreover, this list is not even exhaustive. I wrote this list from my context of work. I am sure the readers will come up with scenarios that fit their individual contexts.

## What do we learn from this?

Single piece of learning that I would take away from this list is this:

> Blaming the last committer for a build failure, without looking into the details, is just plainly gross and offensive! 

It is more efficient and cheaper to concentrate on ‘fixing’ builds rather than concentrating on ostracizing the build breaker.

What are your thoughts on this? I would love to know your view-points, particularly if I am fortunate to be corrected by yours.


