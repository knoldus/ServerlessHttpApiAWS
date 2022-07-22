# Serverless Framework Python HTTP API on AWS

This template demonstrates how to make a simple HTTP API with Python running on AWS Lambda and API Gateway using the Serverless Framework.

This template does not include any kind of persistence (database). 


*************************************************************************************************************
## Requirements : 
*************************************************************************************************************
1. Account on AWS and Basic AWS Lambda Understanding
2. Create AWS User with exceution access 
3. Serverless installed on system
4. register with serverless
5. Provide AWS Access Role

### Ways to install serverless

#### 1 : using NPM

* install npm on system
```
$ sudo apt install npm 
```
* install serverless
```
npm install -g serverless
```
#### 2 : using bash script available online

```
curl -o- -L https://slss.io/install | bash
```

### Registration
```
$ serveless

Onboarding "aws-knoldus-project" to the Serverless Dashboard

? Do you want to login/register to Serverless Dashboard? Yes
Logging into the Serverless Dashboard via the browser
If your browser does not open automatically, please open this URL:
https://app.serverless.com?client=cli&transactionId=_hA7xE2E_MgimeYxwVsen

✔ You are now logged into the Serverless Dashboard

```
* On dashboard, in provider add Access Key and  Secret Key for the User

### access role 

* either start same way as before or serverless deploy
```
$ serveless

Onboarding "aws-knoldus-project" to the Serverless Dashboard

? Do you want to login/register to Serverless Dashboard? Yes
Logging into the Serverless Dashboard via the browser
If your browser does not open automatically, please open this URL:
https://app.serverless.com?client=cli&transactionId=_hA7xE2E_MgimeYxwVsen

✔ You are now logged into the Serverless Dashboard
? What org do you want to add this service to? vaibhavkuma779

✔ Your project is ready to be deployed to Serverless Dashboard (org: "vaibhavkuma779", app: "aws-knoldus-project")

? No AWS credentials found, what credentials do you want to use? (Use arrow keys)
❯ AWS Access Role (most secure) 
  Local AWS Access Keys 
  Skip 

? No AWS credentials found, what credentials do you want to use? AWS Access Role (most secure)

If your browser does not open automatically, please open this URL: https://app.serverless.com/vaibhavkuma779/settings/providers?source=cli&providerId=new&provider=aws

To learn more about providers, visit: http://slss.io/add-providers-dashboard
? 
 [If you encountered an issue when setting up a provider, you may press Enter to skip this step] 

⠏ Waiting for creation of AWS Access Role provider

```
*************************************************************************************************************

## Usage

### Deployment

```
$ serverless deploy
```

After deploying, you should see output similar to:

```bash
Deploying aws-python-http-api-project to stage dev (us-east-1, "default" provider)

⠼ Creating CloudFormation stack (24s)                                                                                                  ⠸ Creating CloudFormation stack (0/2) (35s)                               ✔ Service deployed to stack aws-python-http-api-project-dev (206s)

dashboard: https://app.serverless.com/vaibhavkuma779/apps/aws-http/aws-python-http-api-project/dev/us-east-1
endpoints:
  POST - https://lznw05o581.execute-api.us-east-1.amazonaws.com/dev/posts/create
  GET - https://lznw05o581.execute-api.us-east-1.amazonaws.com/dev/posts/get/{postId}
  GET - https://lznw05o581.execute-api.us-east-1.amazonaws.com/dev/posts/all
  PUT - https://lznw05o581.execute-api.us-east-1.amazonaws.com/dev/posts/update/{postId}
  DELETE - https://lznw05o581.execute-api.us-east-1.amazonaws.com/dev/posts/delete/{postId}
functions:
  create: aws-python-http-api-project-dev-create (29 MB)
  get: aws-python-http-api-project-dev-get (29 MB)
  all: aws-python-http-api-project-dev-all (29 MB)
  update: aws-python-http-api-project-dev-update (29 MB)
  delete: aws-python-http-api-project-dev-delete (29 MB)


```

_Note_: In current form, after deployment, your API is public and can be invoked by anyone. For production deployments, you might want to configure an authorizer. For details on how to do that, refer to [http event docs](https://www.serverless.com/framework/docs/providers/aws/events/apigateway/).

### Invocation

After successful deployment, you can call the created application via HTTP:

```bash
curl https://xxxxxxx.execute-api.us-east-1.amazonaws.com/
```

Which should result in response similar to the following (removed `input` content for brevity):

```json
{
  "message": "Go Serverless v3.0! Your function executed successfully!",
  "input": {
    ...
  }
}
```

### Local development

You can invoke your function locally by using the following command:

```bash
serverless invoke local --function hello
```

Which should result in response similar to the following:

```
{
  "statusCode": 200,
  "body": "{\n  \"message\": \"Go Serverless v3.0! Your function executed successfully!\",\n  \"input\": \"\"\n}"
}
```

Alternatively, it is also possible to emulate API Gateway and Lambda locally by using `serverless-offline` plugin. In order to do that, execute the following command:

```bash
serverless plugin install -n serverless-offline
```

It will add the `serverless-offline` plugin to `devDependencies` in `package.json` file as well as will add it to `plugins` in `serverless.yml`.

After installation, you can start local emulation with:

```
serverless offline
```

To learn more about the capabilities of `serverless-offline`, please refer to its [GitHub repository](https://github.com/dherault/serverless-offline).

*************************************************************************************************************

### Bundling dependencies

In case you would like to include 3rd party dependencies, you will need to use a plugin called `serverless-python-requirements`. You can set it up by running the following command:

```bash
$ serverless plugin install -n serverless-python-requirements

✔ Plugin "serverless-python-requirements" installed
```

Running the above will automatically add `serverless-python-requirements` to `plugins` section in your `serverless.yml` file and add it as a `devDependency` to `package.json` file. The `package.json` file will be automatically created if it doesn't exist beforehand. Now you will be able to add your dependencies to `requirements.txt` file (`Pipfile` and `pyproject.toml` is also supported but requires additional configuration) and they will be automatically injected to Lambda package during build process. For more details about the plugin's configuration, please refer to [official documentation](https://github.com/UnitedIncome/serverless-python-requirements).

*************************************************************************************************************
### delete or remove deployment

```bash
$ serverless remove
Running "serverless" from node_modules
Removing aws-python-http-api-project from stage dev (us-east-1)

✔ Service aws-python-http-api-project has been successfully removed
```