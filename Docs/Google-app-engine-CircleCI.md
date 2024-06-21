


# Building a CI/CD pipeline for a Google App Engine site using CircleCI

In this project, we built a CI/CD pipeline for a Google App Engine Site using CircleCI.

## Prerequisite

* Python installed on your system
* Google Cloud CLI installed

## What we are building

* Documentation site and connect it to GCP (Google Cloud Platform)
* Using CircleCI for automation

## What is CircleCI?
[CircleCI](https://circleci.com/) is a popular choice for software engineers, particularly DevOps engineers when working on [automation](https://www.aviator.co/blog/automating-integration-tests/) and overall CI/CD integrations. The CI/CD platform helps software teams automate the process of building, testing, and deploying code. As a cloud-based platform, CircleCI allows you to seamlessly integrate with any version control system you choose, such as GitHub, Bitbucket, or GitLab. However, we will be working with GitHub on this article.

One cool thing about CircleCI is that it lets developers define pipelines that automate the process of building, testing, and deploying code. Pipelines are composed of jobs, which are individual steps in the CI/CD process. Jobs can be configured to run on various platforms, including Linux, macOS, and Windows.

## Why Circle CI?
CircleCI is a friendly tool for teams of all sizes, ranging from small startups to large enterprises. No wonder the tool is usually “top of the ladder” during CI/CD integrations. It is a powerful tool that can help teams improve the quality and speed of their software development process.

* Improved code quality: CircleCI can help enhance code quality by automating the testing process.
* Reduced deployment time: CircleCI can help reduce the time it takes to deploy code by automating the process of building and deploying.
* Increased confidence in releases: CircleCI can help increase confidence in releases by ensuring that code is thoroughly tested before deployment.
* Improved team communication: CircleCI can help to improve team communication by providing a central location for monitoring the progress of builds and tests.

## Getting started

To get started, we first need to create a free GitHub repo (I assume you already know how to do that). The next step is to clone the empty repo. After this, let’s create a Python virtual environment by running the following command on your terminal:

```shell
pipenv shell
```

This is what it should look like after a successful installation:


<img width="778" alt="s_762DC8729D6070F874B9A6C8613F9867EBE8E5E337A9107440BC3B666C3AB306_1700597968958_Screenshot+2023-11-21+211806" src="https://github.com/ChisomUma/Google-app-engine-CircleCI/assets/98381486/6ff7016d-ef18-46dd-b29a-01a5f25bea3a">


Next, run the command:

```shell=
pip install sphinx
```

[Sphinx](https://www.sphinx-doc.org/en/master/) is a popular documentation generator written in Python that is widely used for creating high-quality documentation for Python projects. It is known for its ease of use, comprehensive features, and extensive support for various output formats.

The next step is to get a Sphinx quick start. To do this, head over to the [get started](https://www.sphinx-doc.org/en/master/usage/quickstart.html) section of Sphinx’s official site and run this command:

```shell=
sphinx-quickstart
```

Once you run the command, you get asked a series of questions, exactly the ones in the image below:


<img width="422" alt="s_762DC8729D6070F874B9A6C8613F9867EBE8E5E337A9107440BC3B666C3AB306_1700599745595_Screenshot+2023-11-21+214746" src="https://github.com/ChisomUma/Google-app-engine-CircleCI/assets/98381486/7f3c109d-e468-46d8-b904-d3bfa9034987">


Respond to these questions until the whole process is complete.

This whole process creates a build and source directory. We are also going to install Sphinx make files by running this command:

```shell!
make html
```
After running the command, your project should look like this in your code editor:

<img width="227" alt="s_762DC8729D6070F874B9A6C8613F9867EBE8E5E337A9107440BC3B666C3AB306_1700600224195_Screenshot+2023-11-21+215541" src="https://github.com/ChisomUma/Google-app-engine-CircleCI/assets/98381486/e0a84a49-1738-46b6-a6f2-594e9b963887">


Within the `build` directory, we have our website files, which look this:
```
📦build
 ┣ 📂doctrees
 ┃ ┣ 📜environment.pickle
 ┃ ┗ 📜index.doctree
 ┗ 📂html
 ┃ ┣ 📂_sources
 ┃ ┃ ┗ 📜index.rst.txt
 ┃ ┣ 📂_static
 ┃ ┃ ┣ 📜alabaster.css
 ┃ ┃ ┣ 📜basic.css
 ┃ ┃ ┣ 📜custom.css
 ┃ ┃ ┣ 📜doctools.js
 ┃ ┃ ┣ 📜documentation_options.js
 ┃ ┃ ┣ 📜file.png
 ┃ ┃ ┣ 📜language_data.js
 ┃ ┃ ┣ 📜minus.png
 ┃ ┃ ┣ 📜plus.png
 ┃ ┃ ┣ 📜pygments.css
 ┃ ┃ ┣ 📜searchtools.js
 ┃ ┃ ┗ 📜sphinx_highlight.js
 ┃ ┣ 📜.buildinfo
 ┃ ┣ 📜genindex.html
 ┃ ┣ 📜index.html
 ┃ ┣ 📜objects.inv
 ┃ ┣ 📜search.html
 ┃ ┗ 📜searchindex.js
 ```
 
 When we run our project on `localhost:8000`, this is what it looks like on the browser:
 
 <img width="842" alt="s_762DC8729D6070F874B9A6C8613F9867EBE8E5E337A9107440BC3B666C3AB306_1700602624194_Screenshot+2023-11-21+223633" src="https://github.com/ChisomUma/Google-app-engine-CircleCI/assets/98381486/04d68613-c801-4b89-9bdb-725ac3414de3">

Congratulations, we have our documentation site live!

## Creating a GCP project
In this section, we will create a brand new [GCP](https://cloud.google.com/gcp?utm_source=google&utm_medium=cpc&utm_campaign=emea-ng-all-en-bkws-all-all-trial-e-gcp-1011340&utm_content=text-ad-none-any-DEV_c-CRE_501794636587-ADGP_Hybrid+%7C+BKWS+-+EXA+%7C+Txt+~+GCP+~+General%23v2-KWID_43700061569959221-aud-1641092902540:kwd-26415313501-userloc_1010294&utm_term=KW_google+cloud+platform-NET_g-PLAC_&&gad_source=1&gclid=CjwKCAiAx_GqBhBQEiwAlDNAZmnpZ1smTjDIwh0PFBZ6hT-NNobPRD5uYG-SDpNd84A6eiw8ZiDMeRoCDkAQAvD_BwE&gclsrc=aw.ds&hl=en) project to figure out which settings need to be tweaked or updated from the base. The next thing is to create our app engine app.yaml. Google provides a detailed [walkthrough](https://cloud.google.com/appengine/docs/standard/hosting-a-static-website) on how to host a static website using GAE. Here, we can copy this YAML file:

```yaml
runtime: python27
api_version: 1
threadsafe: true

handlers:
- url: /
  static_files: www/index.html
  upload: www/index.html

- url: /(.*)
  static_files: www/1
  upload: www/(.*)
```

Create an `app.yaml` file on your editor and paste this code. We then have to edit the YAML file to point it to the proper location where the website files live. To point your Gcloud command line install to this project, use this command:

```shell
gcloud init --project=<"project ID">
```

Here, you will prompted to log in to Google Cloud like this:

<img width="386" alt="s_762DC8729D6070F874B9A6C8613F9867EBE8E5E337A9107440BC3B666C3AB306_1700650957553_Screenshot+2023-11-22+120153" src="https://github.com/ChisomUma/Google-app-engine-CircleCI/assets/98381486/1d617e33-aa8c-430e-b5ec-61a7e75e8a29">


Follow the link provided to get your authorization code.

On the GCP dashboard, navigate to “App Engine” and run the command shown there on your terminal:

```shell
glcloud app deploy
```

You will get a prompt asking you to choose the location you would like your app to be deployed:

<img width="398" alt="s_762DC8729D6070F874B9A6C8613F9867EBE8E5E337A9107440BC3B666C3AB306_1700654477879_Screenshot+2023-11-22+130059" src="https://github.com/ChisomUma/Google-app-engine-CircleCI/assets/98381486/4c6980c3-43f0-4ee7-8684-2310305beece">



Choose anyone, and your app will successfully deploy. It’s time to push our code to Github! Alternatively, you can clone my GitHub repo [here](https://github.com/ChisomUma/Google-app-engine-CircleCI).

**Note:** The documentation file for this project is located in this repo. You can remove it when make changes to the cloned repo.

## Link Github repo to CircleCI
The first thing you need to do is create a [CircleCI account](https://circleci.com/) and link your Github to it. The process is pretty straightforward. Our dashboard should look like this after creating and connecting our project to CircleCI.

<img width="754" alt="s_762DC8729D6070F874B9A6C8613F9867EBE8E5E337A9107440BC3B666C3AB306_1700668023418_Screenshot+2023-11-22+164548" src="https://github.com/ChisomUma/Google-app-engine-CircleCI/assets/98381486/73608596-7755-4ee9-a2f3-b7908f5cd9ca">


Next, in our code editor, we will create a folder named `.circleci` and a `config.yaml` file inside it which contains a code that works like this: first, it defines a workflow, then, the workflow will say; each time we push to the main branch, run this set of jobs. We will also define that job, which will contain the logic of where we build our documentation site and deploy it to the Google App engine.

```yaml
workflows:
  version: 2
  build_and_deploy:
    jobs:
      - build_and_deploy:
        filters:
          branches:
            only:
              - main
```

CircleCI will only run this workflow when we push to the main branch. Now, to define the job:

```yaml
jobs:
  build_and_deploy:
    docker:
      - image: busybox
    steps:
      - run:
          name: hello world
          command: |
            echo "Hello world"
```

You can check your formatting with CircleCI. To do this, first [install CircleCI CLI](https://circleci.com/docs/local-cli/) and run this command:

```shell
circleci config validate
```

Response:


<img width="330" alt="s_762DC8729D6070F874B9A6C8613F9867EBE8E5E337A9107440BC3B666C3AB306_1700671583544_Screenshot+2023-11-22+174555" src="https://github.com/ChisomUma/Google-app-engine-CircleCI/assets/98381486/d026ae4f-0cc2-4e50-9dd4-b4ff9bf2ebb7">


In our CircleCI, you can see the tests, processes, and workflows whenever we push to the main branch on GitHub:

<img width="744" alt="s_762DC8729D6070F874B9A6C8613F9867EBE8E5E337A9107440BC3B666C3AB306_1700672537776_Screenshot+2023-11-22+180013" src="https://github.com/ChisomUma/Google-app-engine-CircleCI/assets/98381486/6c509478-b5fd-49fd-a7a5-8c8c17ea998d">


Awesome! We have successfully created a CI/CD pipeline. Now, whenever we make changes to our code base or documentation, we can just push to the main, and CircleCI will pick up that change (as demonstrated in the image above) and the job or workflow and make deployments a few minutes later.

> For a more visually appealing read, refer to the [published blog version](https://www.aviator.co/blog/ci-cd-google-app-engine/) of this documentation on [Aviator](https://www.aviator.co/).
