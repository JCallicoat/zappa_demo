Simple Demo of Zappa
====================

[Zappa](https://github.com/Miserlou/Zappa) lets you upload python WGSI applications to Amazon Lambda, and creates an API Gateway config that updates your assigned hostname to available Lambda instances, effectively creating a "serverless" WSGI "server" that is actually a lightweight Flask app ready to spin up on a Lamba instance as required. Neat!

Clone this repo and create a virtualenv inside the repo directory and install requirements:

```
git clone git@github.com:JCallicoat/zappa_demo.git
cd zappa demo
virtualenv venv
. venv/bin/activate
pip install flask flask-restful zappa awscli
```

Then create an an IAM user (create one at [Amazon IAM](https://console.aws.amazon.com/iam/home#/users), call it whatever you want -- "zappa-deploy" for example) and grant "Programatic access". On the next screen choose "Attach existing policies directly" and check the "AdministratorAccess" box. Click "Next: Review" and finally click "Create User" and note both the ID and the Key (you will need those in the next step--click "show" for the Key).

Now run `aws configure` and enter the ID and Key and set the region to 'ius-east-1' (or whatever you like).

Finally call `zappa init` and press enter at all the prompts. Zappa is now ready to deploy your Flask server to Lamba. Run `zappa deploy dev` to kick of the process.

This will build a Lambda package with all your dependencies and upload it to Lambda, create the API Gateway entries, and return a URL you can access the WSGI server from. 

["The dishes are done, man!"](https://www.youtube.com/watch?v=wn8XFiAwLkM)

Now you have the tools, go make an actually useful app :wink:
