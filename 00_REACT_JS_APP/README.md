
# References
- [Amplify Getting Started](https://docs.amplify.aws/start)
- [Policy AWS Simulator](https://policysim.aws.amazon.com)
- [Scalar types in AWS AppSync](https://docs.aws.amazon.com/appsync/latest/devguide/scalars.html)
- [GraphQL API Security with AWS AppSync and Amplify](https://aws.amazon.com/blogs/mobile/graphql-security-appsync-amplify/)

# Starting React App

```sh
source ~/.bash_profile
npx create-react-app kio-jup-places-reserve-rjs-app
```

# Design
ref: [Creative Time with Material UI Tutorial](https://demos.creative-tim.com/material-kit-react/?_ga=2.240478787.1362901605.1628185760-743588370.1626883218#/documentation/tutorial)

1. [Download](https://www.creative-tim.com/product/material-kit-react?ref=mkr-navbar&_ga=2.213288532.1362901605.1628185760-743588370.1626883218#) the template 
2. Unzip
3. Copy dependencies from tempalte package.json to kio-jup-places-reserve-rjs-app/package.json
4. Install template dependencies
```sh
npm install
npm audit fix
```
5. Copy jsconfig.json from template to project root 
6. Copy folders (assets, components, views) to src/
7. Add "import "assets/scss/material-kit-react.scss?v=1.10.0";" to index.js

```js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import reportWebVitals from './reportWebVitals';

import "assets/scss/material-kit-react.scss?v=1.10.0";

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();

```
8. Conf app.js like this:

```js
import React, { Component } from 'react'
import { createBrowserHistory } from "history"

// pages for this product
import Components from "views/Components/Components.js";
import LandingPage from "views/LandingPage/LandingPage.js";
import ProfilePage from "views/ProfilePage/ProfilePage.js";
import LoginPage from "views/LoginPage/LoginPage.js";

// Routing
import { BrowserRouter as Router, Switch, Route } from 'react-router-dom'

var hist = createBrowserHistory();

class App extends Component{
  
  constructor() {
    super();
    this.state = {
      
    }
  }

  
  render() {
    
    return (   
        <Router history={hist}>
            <Switch>
                <Route path="/landing-page" component={LandingPage} />
                <Route path="/profile-page" component={ProfilePage} />
                <Route path="/login-page" component={LoginPage} />
                <Route path="/components" component={Components} />
                <Route path="/" component={LandingPage} />
            </Switch>
        </Router>
    )
  }
}

export default App
```



# Amplify

## configure

- Just when is a new aws account
```sh
amplify configure
```


## init

```sh
amplify init
# Note: It is recommended to run this command from the root of your app directory
# ? Enter a name for the project kiojupplacesreserver
# ? Enter a name for the environment kiojuplrev
# ? Choose your default editor: Visual Studio Code
# ? Choose the type of app that you're building javascript
# Please tell us about your project
# ? What javascript framework are you using react
# ? Source Directory Path:  src
# ? Distribution Directory Path: build
# ? Build Command:  npm run-script build
# ? Start Command: npm run-script start
# Using default provider  awscloudformation

# For more information on AWS Profiles, see:
# https://docs.aws.amazon.com/cli/latest/userguide/cli-multiple-profiles.html

# ? Do you want to use an AWS profile? Yes
# ? Please choose the profile you want to use jupiter-electronics
# Adding backend environment kiojuplrev to AWS Amplify Console app: d12mq8x0d6vvbw
# ⠴ Initializing project in the cloud...

# CREATE_IN_PROGRESS UnauthRole                                    AWS::IAM::Role             Fri Aug 06 2021 09:40:40 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# CREATE_IN_PROGRESS AuthRole                                      AWS::IAM::Role             Fri Aug 06 2021 09:40:40 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# CREATE_IN_PROGRESS DeploymentBucket                              AWS::S3::Bucket            Fri Aug 06 2021 09:40:40 GMT-0500 (Colombia Standard Time)                            
# CREATE_IN_PROGRESS AuthRole                                      AWS::IAM::Role             Fri Aug 06 2021 09:40:39 GMT-0500 (Colombia Standard Time)                            
# CREATE_IN_PROGRESS UnauthRole                                    AWS::IAM::Role             Fri Aug 06 2021 09:40:39 GMT-0500 (Colombia Standard Time)                            
# CREATE_IN_PROGRESS amplify-kiojupplacesreserver-kiojuplrev-94031 AWS::CloudFormation::Stack Fri Aug 06 2021 09:40:35 GMT-0500 (Colombia Standard Time) User Initiated             
# ⠙ Initializing project in the cloud...

# CREATE_IN_PROGRESS DeploymentBucket AWS::S3::Bucket Fri Aug 06 2021 09:40:40 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# ⠴ Initializing project in the cloud...

# CREATE_COMPLETE UnauthRole AWS::IAM::Role Fri Aug 06 2021 09:40:53 GMT-0500 (Colombia Standard Time) 
# CREATE_COMPLETE AuthRole   AWS::IAM::Role Fri Aug 06 2021 09:40:53 GMT-0500 (Colombia Standard Time) 
# ⠦ Initializing project in the cloud...

# CREATE_COMPLETE amplify-kiojupplacesreserver-kiojuplrev-94031 AWS::CloudFormation::Stack Fri Aug 06 2021 09:41:04 GMT-0500 (Colombia Standard Time) 
# CREATE_COMPLETE DeploymentBucket                              AWS::S3::Bucket            Fri Aug 06 2021 09:41:01 GMT-0500 (Colombia Standard Time) 
# ✔ Successfully created initial AWS cloud resources for deployments.
# ✔ Initialized provider successfully.
# Initialized your environment successfully.

# Your project has been successfully initialized and connected to the cloud!

# Some next steps:
# "amplify status" will show you what you've added already and if it's locally configured or deployed
# "amplify add <category>" will allow you to add features like user login or a backend API
# "amplify push" will build all your local backend resources and provision it in the cloud
# “amplify console” to open the Amplify Console and view your project status
# "amplify publish" will build all your local backend and frontend resources (if you have hosting category added) and provision it in the cloud

# Pro tip:
# Try "amplify add api" to create a backend API and then "amplify publish" to deploy everything

```

# Codecommit

[Create repo](https://docs.aws.amazon.com/cli/latest/reference/codecommit/create-repository.html)
```sh
nano ~/.aws/credentials
export PATH=~/Library/Python/3.8/bin:$PATH
# source ~/.bash_profile
# test
aws s3 ls --profile jupiter-electronics
export AWS_PROFILE=jupiter-electronics

# aws codecommit create-repository --repository-name MyDemoRepo --repository-description "My demonstration repository" --tags Team=Saanvi
aws codecommit create-repository --repository-name kio-jup-places-reserve-rjs-app --repository-description "Building places reserve" --tags Team=kio --region us-east-1 

```

## result
```json
{
    "repositoryMetadata": {
        "accountId": "953845147077",
        "repositoryId": "c6ceab50-6edb-46fd-a0cd-747a01975578",
        "repositoryName": "kio-jup-places-reserve-rjs-app",
        "repositoryDescription": "Building places reserve",
        "lastModifiedDate": "2021-08-06T10:03:05.069000-05:00",
        "creationDate": "2021-08-06T10:03:05.069000-05:00",
        "cloneUrlHttp": "https://git-codecommit.us-east-1.amazonaws.com/v1/repos/kio-jup-places-reserve-rjs-app",
        "cloneUrlSsh": "ssh://git-codecommit.us-east-1.amazonaws.com/v1/repos/kio-jup-places-reserve-rjs-app",
        "Arn": "arn:aws:codecommit:us-east-1:953845147077:kio-jup-places-reserve-rjs-app"
    }
}
```


# git

```sh
ssh-keygen
/Users/robin8a/.ssh/jupiter_codecommit_rsa

cat ~/.ssh/jupiter_codecommit_rsa.pub

```


```sh
cd ~/.ssh
ls
nano config

# Add

# CodeCommit hosts
# Host jupiter_codecommit_rsa
#    HostName git-codecommit.us-east-1.amazonaws.com
#    User AKIAWIFIFHURQXRLUPPD
#    IdentityFile ~/.ssh/jupiter_codecommit_rsa

```

https://xiaolishen.medium.com/use-multiple-ssh-keys-for-different-github-accounts-on-the-same-computer-7d7103ca8693

```sh
# git remote -v
# git remote rm origin
git remote add origin ssh://jupiter/v1/repos/kio-jup-places-reserve-rjs-app
git push --set-upstream origin master
git push
```



# Install libraries
```sh
# npm install react-bootstrap bootstrap
# npm i react-external-link
# npm i react-router-dom
npm i aws-amplify @aws-amplify/ui-react
npm i aws-amplify-react
# npm i --save react-select
# npm i styled-components
# npm i uuid
```


# Amplify hosting
```sh
amplify add hosting
```
## Result
```sh
amplify add hosting
? Select the plugin module to execute Hosting with Amplify Console (Managed hos
ting with custom domains, Continuous deployment)
? Choose a type Continuous deployment (Git-based deployments)
? Continuous deployment is configured in the Amplify Console. Please hit enter 
once you connect your repository 
Amplify hosting urls: 
┌──────────────┬──────────────────────────────────────────────┐
│ FrontEnd Env │ Domain                                       │
├──────────────┼──────────────────────────────────────────────┤
│ master       │ https://master.d12mq8x0d6vvbw.amplifyapp.com │
```

# Amplify auth

```sh
amplify add auth
# Using service: Cognito, provided by: awscloudformation
 
#  The current configured provider is Amazon Cognito. 
 
#  Do you want to use the default authentication and security configuration? Default configuration
#  Warning: you will not be able to edit these selections. 
#  How do you want users to be able to sign in? Username
#  Do you want to configure advanced settings? No, I am done.
# Successfully added resource kiojupplacesreserver83258164 locally

# Some next steps:
# "amplify push" will build all your local backend resources and provision it in the cloud
# "amplify publish" will build all your local backend and frontend resources (if you have hosting category added) and provision it in the cloud
```

# Amplify push

```sh
amplify push
```

# Amplify api

```sh
amplify add api

# ? Please select from one of the below mentioned services: GraphQL
# ? Provide API name: kiojupplacesreserver
# ? Choose the default authorization type for the API API key
# ? Enter a description for the API key: 
# ? After how many days from now the API key should expire (1-365): 365
# ? Do you want to configure advanced settings for the GraphQL API No, I am done.
# ? Do you have an annotated GraphQL schema? No
# ? Do you want a guided schema creation? Yes
# ? What best describes your project: One-to-many relationship (e.g., “Blogs” with “Posts” and “Comments”)
# ? Do you want to edit the schema now? Yes
# Please edit the file in your editor: /Users/robin8a/Documents/react_ws/kio-jup-places-reserve-rjs-app/amplify/backend/api/kiojupplacesreserver/schema.graphql
```


# amplify storage
```sh
amplify add storage
# Scanning for plugins...
# Plugin scan successful
# ? Please select from one of the below mentioned services: Content (Images, audio, vide
# o, etc.)
# ? Please provide a friendly name for your resource that will be used to label this cat
# egory in the project: s3bf54301f
# ? Please provide bucket name: kio-smart-contracts-ipfs
# ? Who should have access: Auth and guest users
# ? What kind of access do you want for Authenticated users? create/update, read
# ? What kind of access do you want for Guest users? create/update, read
# ? Do you want to add a Lambda Trigger for your S3 Bucket? Yes
# ? Select from the following options 
# ❯ Choose an existing function from the project 
#   Create a new function 
# ➜  kio-smart-contract-rjs-app git:(development) amplify add storage
# ? Please select from one of the below mentioned services: Content (Images, audio, vide
# o, etc.)
# ? Please provide a friendly name for your resource that will be used to label this cat
# egory in the project: s307b7a237
# ? Please provide bucket name: kio-smart-contracts-ipfs
# ? Who should have access: Auth and guest users
# ? What kind of access do you want for Authenticated users? create/update, read
# ? What kind of access do you want for Guest users? create/update, read
# ? Do you want to add a Lambda Trigger for your S3 Bucket? No
# Successfully updated auth resource locally.
# Successfully added resource s307b7a237 locally

# Some next steps:
# "amplify push" builds all of your local backend resources and provisions them in the cloud
# "amplify publish" builds all of your local backend and front-end resources (if you added hosting category) and provisions them in the cloud
```


# Amplify API

```sh
amplify add api
# ? Please select from one of the below mentioned services: GraphQL
# ? Provide API name: kiojupplacesreserver
# ? Choose the default authorization type for the API API key
# ? Enter a description for the API key: 
# ? After how many days from now the API key should expire (1-365): 365
# ? Do you want to configure advanced settings for the GraphQL API No, I am done.
# ? Do you have an annotated GraphQL schema? No
# ? Do you want a guided schema creation? Yes
# ? What best describes your project: One-to-many relationship (e.g., “Blogs” with “Posts” and “Comments”)
# ? Do you want to edit the schema now? Yes
# Please edit the file in your editor: /Users/robin8a/Documents/react_ws/kio-jup-places-reserve-rjs-app/amplify/backend/api/kiojupplacesreserver/schema.graphql
# ? Press enter to continue 

# The following types do not have '@auth' enabled. Consider using @auth with @model
#          - Place
#          - Reserve
# Learn more about @auth here: https://aws-amplify.github.io/docs/cli-toolchain/graphql#auth 


# GraphQL schema compiled successfully.

# Edit your schema at /Users/robin8a/Documents/react_ws/kio-jup-places-reserve-rjs-app/amplify/backend/api/kiojupplacesreserver/schema.graphql or place .graphql files in a directory at /Users/robin8a/Documents/react_ws/kio-jup-places-reserve-rjs-app/amplify/backend/api/kiojupplacesreserver/schema
# Successfully added resource kiojupplacesreserver locally

# Some next steps:
# "amplify push" will build all your local backend resources and provision it in the cloud
# "amplify publish" will build all your local backend and frontend resources (if you have hosting category added) and provision it in the cloud

```

## Result

```sh
amplify push   
# ✔ Successfully pulled backend environment kiojuplrev from the cloud.

# Current Environment: kiojuplrev

# | Category | Resource name                | Operation | Provider plugin   |
# | -------- | ---------------------------- | --------- | ----------------- |
# | Api      | kiojupplacesreserver         | Create    | awscloudformation |
# | Hosting  | amplifyhosting               | No Change |                   |
# | Auth     | kiojupplacesreserver83258164 | No Change | awscloudformation |
# ? Are you sure you want to continue? Yes

# The following types do not have '@auth' enabled. Consider using @auth with @model
#          - Place
#          - Reserve
# Learn more about @auth here: https://aws-amplify.github.io/docs/cli-toolchain/graphql#auth 


# GraphQL schema compiled successfully.

# Edit your schema at /Users/robin8a/Documents/react_ws/kio-jup-places-reserve-rjs-app/amplify/backend/api/kiojupplacesreserver/schema.graphql or place .graphql files in a directory at /Users/robin8a/Documents/react_ws/kio-jup-places-reserve-rjs-app/amplify/backend/api/kiojupplacesreserver/schema
# ? Do you want to generate code for your newly created GraphQL API Yes
# ? Choose the code generation language target javascript
# ? Enter the file name pattern of graphql queries, mutations and subscriptions src/graphql/**/*.js
# ? Do you want to generate/update all possible GraphQL operations - queries, mutations and subscriptions Yes
# ? Enter maximum statement depth [increase from default if your schema is deeply nested] 2
# ⠙ Updating resources in the cloud. This may take a few minutes...

# UPDATE_IN_PROGRESS amplify-kiojupplacesreserver-kiojuplrev-94031 AWS::CloudFormation::Stack Fri Aug 06 2021 16:11:45 GMT-0500 (Colombia Standard Time) User Initiated
# ⠇ Updating resources in the cloud. This may take a few minutes...

# UPDATE_IN_PROGRESS authkiojupplacesreserver83258164 AWS::CloudFormation::Stack Fri Aug 06 2021 16:11:51 GMT-0500 (Colombia Standard Time) 
# CREATE_IN_PROGRESS apikiojupplacesreserver          AWS::CloudFormation::Stack Fri Aug 06 2021 16:11:51 GMT-0500 (Colombia Standard Time) 
# ⠴ Updating resources in the cloud. This may take a few minutes...

# UPDATE_COMPLETE    authkiojupplacesreserver83258164 AWS::CloudFormation::Stack Fri Aug 06 2021 16:11:52 GMT-0500 (Colombia Standard Time)                            
# CREATE_IN_PROGRESS apikiojupplacesreserver          AWS::CloudFormation::Stack Fri Aug 06 2021 16:11:52 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# ⠋ Updating resources in the cloud. This may take a few minutes...

# CREATE_IN_PROGRESS amplify-kiojupplacesreserver-kiojuplrev-94031-apikiojupplacesreserver-1VMDXWBKYEZ81 AWS::CloudFormation::Stack Fri Aug 06 2021 16:11:52 GMT-0500 (Colombia Standard Time) User Initiated
# ⠋ Updating resources in the cloud. This may take a few minutes...

# CREATE_IN_PROGRESS GraphQLAPI AWS::AppSync::GraphQLApi Fri Aug 06 2021 16:11:57 GMT-0500 (Colombia Standard Time) 
# ⠇ Updating resources in the cloud. This may take a few minutes...

# CREATE_COMPLETE    GraphQLAPI AWS::AppSync::GraphQLApi Fri Aug 06 2021 16:12:00 GMT-0500 (Colombia Standard Time)                            
# CREATE_IN_PROGRESS GraphQLAPI AWS::AppSync::GraphQLApi Fri Aug 06 2021 16:12:00 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# ⠇ Updating resources in the cloud. This may take a few minutes...

# CREATE_COMPLETE    GraphQLSchema AWS::AppSync::GraphQLSchema Fri Aug 06 2021 16:12:06 GMT-0500 (Colombia Standard Time)                            
# CREATE_COMPLETE    GraphQLAPIKey AWS::AppSync::ApiKey        Fri Aug 06 2021 16:12:06 GMT-0500 (Colombia Standard Time)                            
# CREATE_IN_PROGRESS GraphQLAPIKey AWS::AppSync::ApiKey        Fri Aug 06 2021 16:12:06 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# CREATE_IN_PROGRESS GraphQLSchema AWS::AppSync::GraphQLSchema Fri Aug 06 2021 16:12:05 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# CREATE_IN_PROGRESS GraphQLAPIKey AWS::AppSync::ApiKey        Fri Aug 06 2021 16:12:03 GMT-0500 (Colombia Standard Time)                            
# CREATE_IN_PROGRESS GraphQLSchema AWS::AppSync::GraphQLSchema Fri Aug 06 2021 16:12:03 GMT-0500 (Colombia Standard Time)                            
# ⠙ Updating resources in the cloud. This may take a few minutes...

# CREATE_IN_PROGRESS Place   AWS::CloudFormation::Stack Fri Aug 06 2021 16:12:09 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# CREATE_IN_PROGRESS Reserve AWS::CloudFormation::Stack Fri Aug 06 2021 16:12:09 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# CREATE_IN_PROGRESS Place   AWS::CloudFormation::Stack Fri Aug 06 2021 16:12:08 GMT-0500 (Colombia Standard Time)                            
# CREATE_IN_PROGRESS Reserve AWS::CloudFormation::Stack Fri Aug 06 2021 16:12:08 GMT-0500 (Colombia Standard Time)                            
# ⠧ Updating resources in the cloud. This may take a few minutes...

# CREATE_IN_PROGRESS amplify-kiojupplacesreserver-kiojuplrev-94031-apikiojupplacesreserver-1VMDXWBKYE-Place-17BAOD8XXTD8Q AWS::CloudFormation::Stack Fri Aug 06 2021 16:12:09 GMT-0500 (Colombia Standard Time) User Initiated
# ⠇ Updating resources in the cloud. This may take a few minutes...

# CREATE_IN_PROGRESS amplify-kiojupplacesreserver-kiojuplrev-94031-apikiojupplacesreserver-1VMDXWBK-Reserve-NK4N0JJCMGNJ AWS::CloudFormation::Stack Fri Aug 06 2021 16:12:09 GMT-0500 (Colombia Standard Time) User Initiated
# ⠼ Updating resources in the cloud. This may take a few minutes...

# CREATE_IN_PROGRESS PlaceTable   AWS::DynamoDB::Table Fri Aug 06 2021 16:12:17 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# CREATE_IN_PROGRESS PlaceIAMRole AWS::IAM::Role       Fri Aug 06 2021 16:12:16 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# CREATE_IN_PROGRESS PlaceTable   AWS::DynamoDB::Table Fri Aug 06 2021 16:12:16 GMT-0500 (Colombia Standard Time)                            
# CREATE_IN_PROGRESS PlaceIAMRole AWS::IAM::Role       Fri Aug 06 2021 16:12:16 GMT-0500 (Colombia Standard Time)                            
# ⠴ Updating resources in the cloud. This may take a few minutes...

# CREATE_IN_PROGRESS ReserveIAMRole AWS::IAM::Role       Fri Aug 06 2021 16:12:17 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# CREATE_IN_PROGRESS ReserveTable   AWS::DynamoDB::Table Fri Aug 06 2021 16:12:16 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# CREATE_IN_PROGRESS ReserveTable   AWS::DynamoDB::Table Fri Aug 06 2021 16:12:16 GMT-0500 (Colombia Standard Time)                            
# CREATE_IN_PROGRESS ReserveIAMRole AWS::IAM::Role       Fri Aug 06 2021 16:12:16 GMT-0500 (Colombia Standard Time)                            
# ⠴ Updating resources in the cloud. This may take a few minutes...

# CREATE_COMPLETE PlaceIAMRole AWS::IAM::Role Fri Aug 06 2021 16:12:30 GMT-0500 (Colombia Standard Time) 
# ⠦ Updating resources in the cloud. This may take a few minutes...

# CREATE_COMPLETE ReserveIAMRole AWS::IAM::Role Fri Aug 06 2021 16:12:31 GMT-0500 (Colombia Standard Time) 
# ⠴ Updating resources in the cloud. This may take a few minutes...

# CREATE_COMPLETE    PlaceDataSource AWS::AppSync::DataSource Fri Aug 06 2021 16:12:35 GMT-0500 (Colombia Standard Time)                            
# CREATE_IN_PROGRESS PlaceDataSource AWS::AppSync::DataSource Fri Aug 06 2021 16:12:35 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# CREATE_IN_PROGRESS PlaceDataSource AWS::AppSync::DataSource Fri Aug 06 2021 16:12:33 GMT-0500 (Colombia Standard Time)                            
# ⠦ Updating resources in the cloud. This may take a few minutes...

# CREATE_COMPLETE    ReserveDataSource AWS::AppSync::DataSource Fri Aug 06 2021 16:12:35 GMT-0500 (Colombia Standard Time)                            
# CREATE_IN_PROGRESS ReserveDataSource AWS::AppSync::DataSource Fri Aug 06 2021 16:12:35 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# CREATE_IN_PROGRESS ReserveDataSource AWS::AppSync::DataSource Fri Aug 06 2021 16:12:33 GMT-0500 (Colombia Standard Time)                            
# ⠼ Updating resources in the cloud. This may take a few minutes...

# CREATE_IN_PROGRESS GetPlaceResolver    AWS::AppSync::Resolver Fri Aug 06 2021 16:12:38 GMT-0500 (Colombia Standard Time) 
# CREATE_IN_PROGRESS CreatePlaceResolver AWS::AppSync::Resolver Fri Aug 06 2021 16:12:38 GMT-0500 (Colombia Standard Time) 
# CREATE_IN_PROGRESS ListPlaceResolver   AWS::AppSync::Resolver Fri Aug 06 2021 16:12:38 GMT-0500 (Colombia Standard Time) 
# CREATE_IN_PROGRESS UpdatePlaceResolver AWS::AppSync::Resolver Fri Aug 06 2021 16:12:38 GMT-0500 (Colombia Standard Time) 
# ⠦ Updating resources in the cloud. This may take a few minutes...

# CREATE_IN_PROGRESS ListReserveResolver   AWS::AppSync::Resolver Fri Aug 06 2021 16:12:38 GMT-0500 (Colombia Standard Time) 
# CREATE_IN_PROGRESS DeleteReserveResolver AWS::AppSync::Resolver Fri Aug 06 2021 16:12:38 GMT-0500 (Colombia Standard Time) 
# ⠴ Updating resources in the cloud. This may take a few minutes...

# CREATE_COMPLETE    DeletePlaceResolver AWS::AppSync::Resolver Fri Aug 06 2021 16:12:41 GMT-0500 (Colombia Standard Time)                            
# CREATE_IN_PROGRESS DeletePlaceResolver AWS::AppSync::Resolver Fri Aug 06 2021 16:12:40 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# CREATE_COMPLETE    GetPlaceResolver    AWS::AppSync::Resolver Fri Aug 06 2021 16:12:40 GMT-0500 (Colombia Standard Time)                            
# CREATE_COMPLETE    CreatePlaceResolver AWS::AppSync::Resolver Fri Aug 06 2021 16:12:40 GMT-0500 (Colombia Standard Time)                            
# CREATE_IN_PROGRESS GetPlaceResolver    AWS::AppSync::Resolver Fri Aug 06 2021 16:12:40 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# CREATE_COMPLETE    UpdatePlaceResolver AWS::AppSync::Resolver Fri Aug 06 2021 16:12:40 GMT-0500 (Colombia Standard Time)                            
# CREATE_IN_PROGRESS CreatePlaceResolver AWS::AppSync::Resolver Fri Aug 06 2021 16:12:40 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# CREATE_IN_PROGRESS UpdatePlaceResolver AWS::AppSync::Resolver Fri Aug 06 2021 16:12:40 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# CREATE_COMPLETE    ListPlaceResolver   AWS::AppSync::Resolver Fri Aug 06 2021 16:12:40 GMT-0500 (Colombia Standard Time)                            
# CREATE_IN_PROGRESS ListPlaceResolver   AWS::AppSync::Resolver Fri Aug 06 2021 16:12:40 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# CREATE_IN_PROGRESS DeletePlaceResolver AWS::AppSync::Resolver Fri Aug 06 2021 16:12:38 GMT-0500 (Colombia Standard Time)                            
# ⠦ Updating resources in the cloud. This may take a few minutes...

# CREATE_COMPLETE    CreateReserveResolver AWS::AppSync::Resolver Fri Aug 06 2021 16:12:41 GMT-0500 (Colombia Standard Time)                            
# CREATE_IN_PROGRESS CreateReserveResolver AWS::AppSync::Resolver Fri Aug 06 2021 16:12:41 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# CREATE_COMPLETE    UpdateReserveResolver AWS::AppSync::Resolver Fri Aug 06 2021 16:12:41 GMT-0500 (Colombia Standard Time)                            
# CREATE_IN_PROGRESS UpdateReserveResolver AWS::AppSync::Resolver Fri Aug 06 2021 16:12:41 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# CREATE_COMPLETE    DeleteReserveResolver AWS::AppSync::Resolver Fri Aug 06 2021 16:12:40 GMT-0500 (Colombia Standard Time)                            
# CREATE_IN_PROGRESS DeleteReserveResolver AWS::AppSync::Resolver Fri Aug 06 2021 16:12:40 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# CREATE_COMPLETE    GetReserveResolver    AWS::AppSync::Resolver Fri Aug 06 2021 16:12:40 GMT-0500 (Colombia Standard Time)                            
# CREATE_COMPLETE    ListReserveResolver   AWS::AppSync::Resolver Fri Aug 06 2021 16:12:40 GMT-0500 (Colombia Standard Time)                            
# CREATE_IN_PROGRESS GetReserveResolver    AWS::AppSync::Resolver Fri Aug 06 2021 16:12:40 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# CREATE_IN_PROGRESS ListReserveResolver   AWS::AppSync::Resolver Fri Aug 06 2021 16:12:40 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# CREATE_IN_PROGRESS CreateReserveResolver AWS::AppSync::Resolver Fri Aug 06 2021 16:12:39 GMT-0500 (Colombia Standard Time)                            
# CREATE_IN_PROGRESS GetReserveResolver    AWS::AppSync::Resolver Fri Aug 06 2021 16:12:38 GMT-0500 (Colombia Standard Time)                            
# CREATE_IN_PROGRESS UpdateReserveResolver AWS::AppSync::Resolver Fri Aug 06 2021 16:12:38 GMT-0500 (Colombia Standard Time)                            
# ⠇ Updating resources in the cloud. This may take a few minutes...

# CREATE_COMPLETE PlaceTable AWS::DynamoDB::Table Fri Aug 06 2021 16:12:48 GMT-0500 (Colombia Standard Time) 
# ⠏ Updating resources in the cloud. This may take a few minutes...

# CREATE_COMPLETE ReserveTable AWS::DynamoDB::Table Fri Aug 06 2021 16:12:48 GMT-0500 (Colombia Standard Time) 
# ⠇ Updating resources in the cloud. This may take a few minutes...

# CREATE_COMPLETE amplify-kiojupplacesreserver-kiojuplrev-94031-apikiojupplacesreserver-1VMDXWBKYE-Place-17BAOD8XXTD8Q AWS::CloudFormation::Stack Fri Aug 06 2021 16:12:50 GMT-0500 (Colombia Standard Time) 
# ⠋ Updating resources in the cloud. This may take a few minutes...

# CREATE_COMPLETE amplify-kiojupplacesreserver-kiojuplrev-94031-apikiojupplacesreserver-1VMDXWBK-Reserve-NK4N0JJCMGNJ AWS::CloudFormation::Stack Fri Aug 06 2021 16:12:50 GMT-0500 (Colombia Standard Time) 
# ⠋ Updating resources in the cloud. This may take a few minutes...

# CREATE_COMPLETE Reserve AWS::CloudFormation::Stack Fri Aug 06 2021 16:12:57 GMT-0500 (Colombia Standard Time) 
# ⠋ Updating resources in the cloud. This may take a few minutes...

# CREATE_COMPLETE Place AWS::CloudFormation::Stack Fri Aug 06 2021 16:12:57 GMT-0500 (Colombia Standard Time) 
# ⠋ Updating resources in the cloud. This may take a few minutes...

# CREATE_IN_PROGRESS ConnectionStack AWS::CloudFormation::Stack Fri Aug 06 2021 16:13:00 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# CREATE_IN_PROGRESS ConnectionStack AWS::CloudFormation::Stack Fri Aug 06 2021 16:12:59 GMT-0500 (Colombia Standard Time)                            
# ⠦ Updating resources in the cloud. This may take a few minutes...

# CREATE_IN_PROGRESS amplify-kiojupplacesreserver-kiojuplrev-94031-apikiojupplacesreserver-ConnectionStack-TIRY9TBK0P36 AWS::CloudFormation::Stack Fri Aug 06 2021 16:13:00 GMT-0500 (Colombia Standard Time) User Initiated
# ⠧ Updating resources in the cloud. This may take a few minutes...

# CREATE_IN_PROGRESS ReserveplaceResolver  AWS::AppSync::Resolver Fri Aug 06 2021 16:13:06 GMT-0500 (Colombia Standard Time) 
# CREATE_IN_PROGRESS PlacereservesResolver AWS::AppSync::Resolver Fri Aug 06 2021 16:13:05 GMT-0500 (Colombia Standard Time) 
# ⠇ Updating resources in the cloud. This may take a few minutes...

# CREATE_COMPLETE    ReserveplaceResolver  AWS::AppSync::Resolver Fri Aug 06 2021 16:13:08 GMT-0500 (Colombia Standard Time)                            
# CREATE_IN_PROGRESS ReserveplaceResolver  AWS::AppSync::Resolver Fri Aug 06 2021 16:13:08 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# CREATE_COMPLETE    PlacereservesResolver AWS::AppSync::Resolver Fri Aug 06 2021 16:13:08 GMT-0500 (Colombia Standard Time)                            
# CREATE_IN_PROGRESS PlacereservesResolver AWS::AppSync::Resolver Fri Aug 06 2021 16:13:07 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# ⠼ Updating resources in the cloud. This may take a few minutes...

# CREATE_COMPLETE ConnectionStack AWS::CloudFormation::Stack Fri Aug 06 2021 16:13:11 GMT-0500 (Colombia Standard Time) 
# ⠹ Updating resources in the cloud. This may take a few minutes...

# CREATE_IN_PROGRESS CustomResourcesjson AWS::CloudFormation::Stack Fri Aug 06 2021 16:13:14 GMT-0500 (Colombia Standard Time) Resource creation Initiated
# CREATE_IN_PROGRESS CustomResourcesjson AWS::CloudFormation::Stack Fri Aug 06 2021 16:13:13 GMT-0500 (Colombia Standard Time)                            
# ⠧ Updating resources in the cloud. This may take a few minutes...

# CREATE_IN_PROGRESS amplify-kiojupplacesreserver-kiojuplrev-94031-apikiojupplacesreser-CustomResourcesjson-5C95OXAUGBTW AWS::CloudFormation::Stack Fri Aug 06 2021 16:13:14 GMT-0500 (Colombia Standard Time) User Initiated
# ⠇ Updating resources in the cloud. This may take a few minutes...

# CREATE_COMPLETE amplify-kiojupplacesreserver-kiojuplrev-94031-apikiojupplacesreser-CustomResourcesjson-5C95OXAUGBTW AWS::CloudFormation::Stack Fri Aug 06 2021 16:13:18 GMT-0500 (Colombia Standard Time) 
# ⠼ Updating resources in the cloud. This may take a few minutes...

# CREATE_COMPLETE CustomResourcesjson AWS::CloudFormation::Stack Fri Aug 06 2021 16:13:25 GMT-0500 (Colombia Standard Time) 
# ⠸ Updating resources in the cloud. This may take a few minutes...

# CREATE_COMPLETE amplify-kiojupplacesreserver-kiojuplrev-94031-apikiojupplacesreserver-1VMDXWBKYEZ81 AWS::CloudFormation::Stack Fri Aug 06 2021 16:13:27 GMT-0500 (Colombia Standard Time) 
# ⠏ Updating resources in the cloud. This may take a few minutes...

# CREATE_COMPLETE apikiojupplacesreserver AWS::CloudFormation::Stack Fri Aug 06 2021 16:13:46 GMT-0500 (Colombia Standard Time) 
# ⠇ Updating resources in the cloud. This may take a few minutes...

# UPDATE_COMPLETE                     amplify-kiojupplacesreserver-kiojuplrev-94031 AWS::CloudFormation::Stack Fri Aug 06 2021 16:13:51 GMT-0500 (Colombia Standard Time) 
# UPDATE_COMPLETE                     authkiojupplacesreserver83258164              AWS::CloudFormation::Stack Fri Aug 06 2021 16:13:50 GMT-0500 (Colombia Standard Time) 
# UPDATE_COMPLETE_CLEANUP_IN_PROGRESS amplify-kiojupplacesreserver-kiojuplrev-94031 AWS::CloudFormation::Stack Fri Aug 06 2021 16:13:49 GMT-0500 (Colombia Standard Time) 
# ✔ Generated GraphQL operations successfully and saved at src/graphql
# ✔ All resources are updated in the cloud

GraphQL endpoint: https://oq2wwe5hgjegzltql7ol77uzxq.appsync-api.us-east-1.amazonaws.com/graphql
GraphQL API KEY: da2-5golr3ets5cglf4qk6x5m6uini

```