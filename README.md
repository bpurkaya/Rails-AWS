<!-- CI (Continues Integration)
Step 1

Let’s start creating a new workflow in GitHub actions that will perform those tasks. in your root rails project. -->

mkdir -p .github/workflows
touch .github/workflows/main.yml

<!-- Step 2

The main.yml where we defined our workflow CI and CD. We name our workflow CI/CD, Then list the name of our events which will trigger our workflow. -->

# main.yml
name: CI/CD
on: [push, pull_request]

<!-- Step 3

Use the ubuntu latest image to install all necessary libraries and PostgreSQL as database -->


main.yml
services can be used to create additional containers for a job or steps. In our case, we are using it to spin-off postgres and redis service.

<!-- Step 4

We can define a sequential task that we want to perform in the machine with steps statement. -->

Next thing we will do is check out our rails app. Github provides official, ready to use actions an one of those is action/checkout
we can directly use this action directly using statement use.

Similarly other actions actions/setup-ruby and bolares/actions-yarn is used to check out the ruby version and yarn package manager that we want to use for our rails app.


In the above snippet 👆, we just added steps for setting up ruby environment and yarn.

More about bolares/actions-yarn is here

<!-- Step5

Once the code has been checked out and correct ruby version is set up, we install the gems using bundler and then run the specs -->

Let’s add one more step for setting up our rails application.


In the above 👆 snippet, we are adding some necessary environment variables and executing the necessary commands.

First, we installed bundlergem, then create and migrate the database and finally running Rspec test cases.

Note: I’m using Rspec testing library you can put other as well

That’s it, we successfully integrate CI workflow for our Rails app successfully, now if push the changes you can see GitHub actions start executing.


CI Workflow
You can see your actions are executing successfully 🙂.

If you missed something below 👇 is the full snippet for CI workflow.


CD(Continuous delivery)
Now Let’s move to the CD(continues delivery)part, before moving further you must have an account onAWS

Step1

Install CLI elastic beanstalk on your local machine.

brew install aws-elasticbeanstalk
Go to your project directory and initialize elastic beanstalk using the command

eb init
During init, elastic beanstalk shows some CLI questions & it will create config.yml like below 👇


Step2

Create a project with Postgres.

eb create staging -db.engine postgres
Above 👆command will start creating our project ready for deployment.


Here is the sample log once we start creating it.

You might get an error here because we haven't set up database.yml correctly.

Step3

Add production configure like below 👇 in your database.yml file


Now, the setup environment variable

eb setenv SECRET_KEY_BASE= xxxxxx
ForSECRET_KEY_BASE just fire on terminal

RAILS_ENV=production bundle exec rake secret
That’s it we are done with all configuration lets deploy our application.

eb deploy staging

If you check on AWS Elastic Beanstalk dashboard you can see our application created successfully.

Step4

Beanstalk Deploy is a GitHub action (and command-line script) to deploy apps to AWS Elastic Beanstalk. It takes the application name, environment name, version name, region and filename as parameters, uploads the file to S3, creates a new version in Elastic Beanstalk, and then deploys that version to the environment. It will wait until the deployment is finished, logging any messages from the environment during the update and exiting with a non-zero exit code if the deployment fails. It does not handle rolling back the environment.

Now let’s add this to our Github Action workflow


Here you can see we need AWS_ACCESS_KEY and AWS_SECRET_ACCESS_KEY , using GitHub secrets you can add your credentials and those environmental variables accessible in your GitHub workflow.


Now let’s push our workflow changes & let's see the result…


Hureeeee 🎉, our code builds successfully and deployed to AWS Beanstalk.

Here is a full code snippet 👇


