# kinesis-streamer
This project is a demonstration Node.JS application that sends messages with structured, random data continuously to a predefined AWS Kinesis Stream.

The way the application works is that it creates a number of CronJobs, with each [CronJob](https://www.npmjs.com/package/cron) running every second. The CronJob's logic sends one or many messages to a Kinesis Stream. This Kinesis Stream must be running under AWS before the application starts.

The credentials required to access to the Kinesis Stream are defined according to the environment variables `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`.

The name of a particular Kinesis Stream to bind to is also defined by an environment variable `AWS_KINESIS_STREAM_NAME`. These values are in a file named `.env`.

The file `.env` needs to be created and configured. (A section that follows describes the details of creating and configuring the file `.env`.) Also, overriding the default number of CronJobs that will run simultaneously and the number of messages that will be sent by each CronJobs are defined in the `.env` file. 

# Installation

`npm install`

# Testing

`npm test`

The tests that run in this project check that the credential information is available in the runtime environment. Also, a test will check that a ShardId is returned from the Kinesis Stream to which the application is bound.

Operationally this means that all the values assigned to the [required environment variables](https://github.com/reselbob/kinesis-streamer#configuring-the-environment-variables) work as expected.

# Running the project

This project depends on the existence of an accessible Kinesis Stream running on AWS.


## Configuring the environment variables

This project uses the [`dotenv`](https://www.npmjs.com/package/dotenv) NPM package to inject environment variables into the application at runtime.

This project looks in the root directory for a file named `.env`. This project does **not** ship with the `.env` file. You need to create it in the root of this project.

The environment variables are defined in the `.env` file like so:

```text
AWS_ACCESS_KEY_ID="a^ACcEsS_KEY_tokEN!"
AWS_SECRET_ACCESS_KEY="a^SecRET_accESS_k3y_TOken"
AWS_KINESIS_STREAM_NAME=my-stream-kinesis
CRON_JOBS_TO_GENERATE=50
MESSAGES_PER_CRON_JOB=20
```

The following sections describe the particulars of each environment variable.

----

**`AWS_ACCESS_KEY_ID`**

REQUIRED

The access key that gets generated by AWS when a user is created within the AWS Dashboard or via the AWS CLI tool.

`AWS_ACCESS_KEY_ID="<YOUR_AWS_ACCESS_KEY_ID>"`

**Example:**

`GKIAWSDDTX85L1PDD3EG`

----
**`AWS_SECRET_ACCESS_KEY`**

REQUIRED

The secret access key that gets generated by AWS when a user is created.

`AWS_SECRET_ACCESS_KEY="<YOUR_AWS_SECRET_ACCESS_KEY>"`

**Example:**

`+hjIhOwyOUkD0inqvu0EJiRs+XmlXmLawmJGE4V`

----

**`AWS_KINESIS_STREAM_NAME`**

REQUIRED

This project reads the name for the Kinesis stream from environment variable. Thus, you need to set the environment variable as follows:

`AWS_KINESIS_STREAM_NAME=<STREAM_NAME>`

**Example:**

`AWS_KINESIS_STREAM_NAME=my-stream-kinesis`

----

**`CRON_JOBS_TO_GENERATE`**

OPTIONAL

Defines to the number of CronJobs to generate and run against the AWS Kinesis stream. If you do not provide this environment variable, the default number of CronJobs generated is 10.

**Example:**

`CRON_JOBS_TO_GENERATE=50`

----

**`MESSAGES_PER_CRON_JOB`**

OPTIONAL

Defines to the number of messages to generate to send to the AWS Kinesis Stream in a single submission. If you do not provide this environment variable, the default number of CronJobs generated is 10.

**Example:**

`MESSAGES_PER_CRON_JOB=20`

----

## Starting the application

To start the application, execute the following command:

`npm start`