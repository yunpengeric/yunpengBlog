---
layout: post
title: Triggering Jenkins Parameterized Builds Behind A Firewall
---
# Background

In this post I would like to share with you the process of how to trigger Jenkins parameterized builds behind a firewall. 

Imagine your Jenkins is behind a corporate firewall but still able to receive webhooks from Github, DockerHub and Microsoft Automate. 

I have seen many posts discussing related topics, but most webhook forwarding services cannot forward query parameters, which means they do not have the ability to trigger Jenkins builds with parameters.

# Prerequisites

- Webhook Relay account - register [here](https://my.webhookrelay.com/).
- Jenkins server

# Process

## Configuring Webhook Relay

Create a New Bucket [here](https://my.webhookrelay.com/buckets) . Buckets allow you to group inputs and outputs.

A newly created bucket will have a default input and you will need to create an output destination where webhooks will be sent.

Click on `OUTPUT DESTINATION`> Fill in your custom `Output name`  > Fill in your Jenkins server address  in `Output destination`  > click `create output` 

```yaml
# Output Destination Example
# If your Jenkins allows anonymous users can have build access.
http://192.168.0.200:8080
# If only authenticated users can have build access.
http://username:token@192.168.0.200:8080
```

Click `CONFIGURE` under your Output Destinations > Switch off `Lock destination path` > Click on `SAVE`.

It will allow us to send any extra path([xyz.hooks.webhookrelay.com/foo/bar](http://xyz.hooks.webhookrelay.com/foo/bar) -> 192.168.0.200:8080/foo/bar).

![settings](../images/webhookrelay/webhooksettings.png)

## Configuring Webhookrelayd agent

Create an access token [here.](https://my.webhookrelay.com/tokens)  Access tokens are used to authenticate Webhook Relay agents.

On the Jenkins VM or  a VM that can talk on the Jenkins server, start a webhookrelayd agent.

Specify configuration through environment variables:

```bash
KEY=<your token key>
SECRET=<your token secret>
BUCKET=<bucket name>
```

Run the webhookrelayd container:

```bash
docker run -d \
	   --name webhookrelayd \
           --restart=unless-stopped \
           webhookrelay/webhookrelayd 
					
```

Now go back to your Bucket page, you should see the status has changed to `Client Connected`. If there are any problems, you should check your docker logs.

 

![status](../images/webhookrelay/status.png)

## Testing Jenkins Builds

Open your Terminal, let us test your Jenkins build.

Here is an example when trigger the Jenkins build normally:

```bash
curl http://192.168.0.200:8080/job/demo/buildWithParameters?token=<buildToken>&env=dev&version=20210804&user=john.doe
```

When using Webhook Relay, it will be converted to the following url:

```bash
curl https://<unique domain>.hooks.webhookrelay.com/job/demo/buildWithParameters?token=<buildToken>&env=dev&version=20210804&user=john.doe
```

You can also find the Relay Logs [here](https://my.webhookrelay.com/logs).
