[![Build Status](https://travis-ci.org/cfn-modules/lambda-event-source-dynamodb-stream.svg?branch=master)](https://travis-ci.org/cfn-modules/lambda-event-source-dynamodb-stream)
[![NPM version](https://img.shields.io/npm/v/@cfn-modules/lambda-event-source-dynamodb-stream.svg)](https://www.npmjs.com/package/@cfn-modules/lambda-event-source-dynamodb-stream)

# cfn-modules: AWS Lambda event source: DynamoDB stream

DynamoDB stream event source for AWS Lambda function.

## Install

> Install [Node.js and npm](https://nodejs.org/) first!

```
npm i @cfn-modules/lambda-event-source-dynamodb-stream
```

## Usage

> You have to set the `StreamViewType` parameter in the lambda-function module to != DISABLED to make this event source work.

```
---
AWSTemplateFormatVersion: '2010-09-09'
Description: 'cfn-modules example'
Resources:
  EventSource:
    Type: 'AWS::CloudFormation::Stack'
    Properties:
      Parameters:
        LambdaModule: !GetAtt 'Function.Outputs.StackName' # required
        TableModule: !GetAtt 'Table.Outputs.StackName' # required
        BatchSize: '10' # optional
        StartingPosition: LATEST # optional
      TemplateURL: './node_modules/@cfn-modules/lambda-event-source-dynamodb-stream/module.yml'
```

## Parameters

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Description</th>
      <th>Default</th>
      <th>Required?</th>
      <th>Allowed values</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>LambdaModule</td>
      <td>Stack name of <a href="https://www.npmjs.com/package/@cfn-modules/lambda-function">lambda-function module</a></td>
      <td></td>
      <td>yes</td>
      <td></td>
    </tr>
    <tr>
      <td>TableModule</td>
      <td>Stack name of <a href="https://www.npmjs.com/package/@cfn-modules/dynamodb-table">dynamodb-table module</a> module (with StreamViewType != DISABLED)</td>
      <td></td>
      <td>yes</td>
      <td></td>
    </tr>
    <tr>
      <td>BatchSize</td>
      <td>The largest number of messages that Lambda retrieves from your queue at once.</td>
      <td>10</td>
      <td>no</td>
      <td>[1-10000]</td>
    </tr>
    <tr>
      <td>StartingPosition</td>
      <td>The position in the stream where Lambda starts reading</td>
      <td>LATEST</td>
      <td>no</td>
      <td>[LATEST, TRIM_HORIZON]</td>
    </tr>
  </tbody>
</table>
