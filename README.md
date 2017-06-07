# Ionic Mobile App

This Ionic Mobile App comes with a pre-configured [AWS Mobile Hub](https://aws.amazon.com/mobile/) project to set up with Amazon DynamoDB, S3, Pinpoint, and Cognito.

## Using the Mobile App

### Installing Ionic CLI 3.0

This Mobile App requires Ionic CLI 3.0, to install, run

```bash
npm install -g ionic@latest
```

Make sure to add `sudo` on Mac and Linux. If you encounter issues installing the Ionic 3 CLI, uninstall the old one using `npm uninstall -g ionic` first.

### Installing AWS CLI

To install the AWS CLI, first ensure your pip installation is up to date:

```
pip install --upgrade pip
```

Next, install the AWS CLI:

```
pip install awscli
```

Note: add `sudo` to the above commands on Mac and Linux.

### Creating the Ionic Project

To create a new Ionic project using this AWS Mobile Hub Mobile App, run

```bash
ionic start myApp aws
```

Which will create a new app in `./myApp`.

Once the app is created, `cd` into it:

```bash
cd myApp
```

Proceed to the next steps on importing the auto-generated AWS Mobile Hub project.

### Creating AWS Mobile Hub Project

Visit the [AWS Mobile Hub](https://aws.amazon.com/mobile/) and enter the Mobile Hub Console.

In the Mobile Hub dashboard, click the "Import your project" button. Next, find the `mobile-hub-project.zip` included
in this Mobile App project, and drag and drop it to the import modal. Set the name of the project, and then click "Import project."

Once the project is imported, you'll be directed to the dashboard for this Mobile Hub project. To continue configuring the app, you'll need to find the name of the Amazon S3 bucket auto generated through the App Content Delivery system. To do this, click the "Resources" button on the left side of the Mobile Hub project dashboard, find the "Amazon S3 Buckets" card, and then copy the bucket name that contains `hosting-mobilehub`.

Next, assuming your terminal is still open inside of the `myApp` folder, run:

```bash
aws s3 cp s3://BUCKET_NAME/aws-config.js src/assets
```

Replacing `BUCKET_NAME` with the full name of the S3 bucket found above. This will copy the auto-generated `aws-config.js` file into the `src/assets` folder in your Ionic app, which pre-configures all your AWS settings automatically.

### Running the app

Now the app is configured and wired up to the AWS Mobile Hub and AWS services. To run the app in the browser, run

```bash
ionic serve
```

To run the app on device, first add a platform, and then run it:

```bash
ionic cordova platform add android
ionic cordova run android
```

### Hosting app on Amazon S3

Since your Ionic app is just a web app, it can be hosted as a static website in an Amazon S3 bucket. To do this, copy the web assets to the S3 bucket:

```
npm run build
aws s3 cp --recursive ./www s3://WEBSITE_BUCKET
```

Where `WEBSITE_BUCKET` is an S3 bucket configured with static hosting.
