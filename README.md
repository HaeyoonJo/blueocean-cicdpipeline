# creating-a-pipeline-in-blue-ocean

This repository has been forked from [jenkins-docs](https://github.com/jenkins-docs/simple-node-js-react-npm-app)  
This README.md is written in Korean in order to get understanding and planned to be published on my personal GitHub blog.

This repository is for the
[Create a Pipeline in Blue Ocean](https://jenkins.io/doc/tutorials/create-a-pipeline-in-blue-ocean/)
tutorial in the [Jenkins User Documentation](https://jenkins.io/doc/).

This tutorial uses the same application that the [Build a Node.js and React app
with
npm](https://jenkins.io/doc/tutorials/build-a-node-js-and-react-app-with-npm/)
tutorial is based on. Therefore, you'll be building the same application
although this time, completely through Blue Ocean.

The `jenkins` directory contains an example of the `Jenkinsfile` (i.e. Pipeline)
that Blue Ocean will create for you during the tutorial and the `scripts`
subdirectory contains shell scripts with commands that are executed when Jenkins
processes the "Test" and "Deliver" stages of your Pipeline.

## Jenkins principle

1. Jenkins란?

Jenkins [site](https://www.jenkins.io/) 및 [docs](https://www.jenkins.io/doc/#what-is-jenkins)에 보면 아래와 같이 소개하고 있다.

- `build great things at any scale`

- `Jenkins is a self-contained, open source automation server which can be used to automate all sorts of tasks related to building, testing, and delivering or deploying software. Jenkins can be installed through native system packages, Docker, or even run standalone by any machine with a Java Runtime Environment (JRE) installed.`

그리고 infoworld.com [사이트](https://www.infoworld.com/article/3239666/what-is-jenkins-the-ci-server-explained.html)에서는 Jenkins를 다음과 같이 소개하고 있다.

`Jenkins offers a simple way to set up a continuous integration or continuous delivery (CI/CD) environment for almost any combination of languages and source code repositories using pipelines, as well as automating other routine development tasks.`

*참고: 더불어, 해당사이트에서 continuous integration or continuous delivery (CI/CD)에 대해서 [링크](https://www.infoworld.com/article/3271126/what-is-cicd-continuous-integration-and-continuous-delivery-explained.html)하여 설명하고 있으니 참고해도 될 것 같다.


즉, Jenkins는 대부분 개발언어와 레파지토리를 통해 자동화 및 빌드 파이프라인 지원하는 CI tool로써, 각 단계에 대해 쉽고 빠르게 Build, Test 및 Deployment 체인된 통합도구로 제공을 하고 있다.  
추가적으로 Jenkins에서 간단한 작업은 bash, python과 같은 스크립트 언어로 작성하여 필요한 작업을 할 수 있다.

2. Use cases

- hook: 훅을 이용하여 Github와 같은 버전관리시스템에 개발자가 커밋을 하면, 커밋을 트리거하여 빌드하는 빌드통합 서비스를 제공한다.
- OAuth: OAuth를 통해 안전하게 젠킨스에서 접근할 수 있도록하는 Github 인증을 의미한다. Github 외에도 다른 버전관리시스템에서 발급하여 연동가능하다.

*참고: Hudson과 Jenkins에 대해서는 다른 블로그에도 많이 소개되고 있으므로 스킵

3. 플러그인

+1500여개가 넘는 커뮤니티의 컨트리뷰트를 통해 1000여개가 넘는 플러그인을 지원하며 필요한 빌드 툴, 분석 툴, 클라우드 providers 등을 설치하여 기능적인 확장이 가능하다. 젠킨스 문서에서도 아래와 같이 소개하고 있다.  
`Jenkins is a highly extensible product whose functionality can be extended through the installation of plugins.`

필요한 플러그인에 대한 설명은 plugins.jenkins.io [사이트](https://plugins.jenkins.io/ui/search/?categories=userInterface)에서 찾을 수 있고, 유용한 다양한 플러그인들을 아래 사이트들에서 찾을 수 있다.  
- [useful-jenkins-plugins](https://www.hugeinc.com/articles/list-of-useful-jenkins-plugins)  
- [essential-jenkins-plugins](https://www.functionize.com/blog/4-essential-jenkins-plugins/)  
- [jenkins-plugins](https://caylent.com/jenkins-plugins)  

## Building a simple Node.js and React webapp using Blueocean plugin

1. What I get: CICD deployment using Jenkinsfile, understanding Jenkinsfile

2. Process:  
  - Create docker Network, Volume using docker and pull 'jenkinsci/blueocean' docker image
  - Get 'Docker TLS certs' from docker:dind docker image
  - Binding 3000 port to the worker node for Node.js app using Jenkinsfile
  - it's needs to commit the code changes to local or remote git server then, it will deploy the modified web app in order to build up
