---
layout: post
title: "AWS CloudFormation Minimum Example"
---

template.yaml
```
Resources:
  TestInstance:
    Type: AWS::EC2::Instance
    Properties:
      ImageId: ami-0de53d8956e8dcf80
```
