---
layout: post
title: "Use Standard runtime on AWS CodeCommit"
---

I realized that I should choose **Standard** runtime instead of **Node.js** even if the build target is a Node.js project because the default python version is 2.7.6 and pip is not installed on Node.js runtime by default.

I have checked with following buildspec.yml file.

**buildspec.yml**

```
version: 0.2
phases:
  install:
    commands:
      - python --version
      - python3 --version
      - pip --version
      - pip3 --version
```

- With **Node.js** runtime:

  ![Node.js runtime](/assets/img/codebuild-runtime-nodejs.png)

  The default python version is 2.7.6 and pip is not installed.

  ![Python Node.js runtime](/assets/img/codebuild-python-nodejs.png)

- With **Standard** runtime:

  ![Standard runtime](/assets/img/codebuild-runtime-standard.png)

  The default python version is 3.7.2 and pip is installed.

  ![Python Standard tuntime](/assets/img/codebuild-python-standard.png)
