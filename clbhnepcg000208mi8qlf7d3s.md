# Deploy to the server with pm2 and custom log

### 👋What is pm2

> PM2 is a daemon process manager that will help you manage and keep your application online 24/7

Other features:

*   Monitoring CPU/Memory
    
*   The **cluster mode** allows networked Node.js applications (HTTP (s)/TCP/UDP server) to be scaled across all CPUs available (load balancer), without any code modifications.
    
*   **Serve static files over HTTP**
    
*   Manage logs easily
    
*   watch & restart the app on any file change
    
*   [Startup Script Generator](https://pm2.keymetrics.io/docs/usage/startup/) and that script automatically restart the service list at boot.
    

It is really helpful when you deploy an app to a server like AWS EC2. For example, you can use pm2 when [deploy Next.js App with AWS EC2](https://gist.github.com/ArcRanges/3d1d95421984c40fffaf3fabc9ea7396).

[pm2](https://pm2.keymetrics.io/) is written in *Node.js*. However, It can run any <mark>shell script</mark> or run <mark>sh</mark>, <mark>js</mark> file directly.

To install Node.js and NPM you can use [fnm](https://github.com/Schniz/fnm), then install pm2:

```bash
npm install pm2@latest -g
# or
yarn global add pm2
# or
pnpm add -g pm2
```

### 🥦Prepare an example

Create an <mark>test-pm2.js</mark> file:

```javascript
let count = 0;

/**
 * Keep running 🏃 to serve.
 * Determine whether running or not by logger.
 */
const testPm2 = () => {
  setInterval(() => {
    console.log('🙏👋 from testPm2!');
  }, 1000);
};

testPm2();
```

### 🎶Using configuration file

Create an <mark>ecosystem.config.js</mark> file:

```javascript
module.exports = {
  apps: [
    {
      name: 'my-app',
      script: 'test-pm2.js',
      watch: false,
      error_file: 'pm2-log/error.log',
      out_file: 'pm2-log/info.log',
      time: true,
    },
  ],
};
```

### 🪁Run

```bash
pm2 start ecosystem.config.js
```

View <mark>pm2-log/info.log</mark>:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1670655087697/xQFD4usSA.png align="center")

View process list:

```bash
pm2 ls
```

Output:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1670655220550/5AAfa-iwc.png align="center")

Stop <mark>my-app</mark> :

```bash
pm2 stop my-app
# or stop all
pm2 stop all

# confirm
pm2 ls
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1670655618185/9tcmHv9AA.png align="center")

To delete <mark>my-app</mark> from process management:

```bash
pm2 delete my-app
# or
pm2 delete all

# confirm
pm2 ls
```

### For AWS CloudWatch Logs service

You have to [install and configure the CloudWatch Logs agent on a running EC2 Linux instance](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/QuickStartEC2Instance.html) for example. Then, you choose which files it should monitor for changes by [customs the log agent configuration file](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/CloudWatch-Agent-Configuration-File-Details.html#CloudWatch-Agent-Configuration-File-Logssection):

```bash
sudo vim /opt/aws/amazon-cloudwatch-agent/bin/config.json
```

```bash
{
     "agent": {
         "run_as_user": "root"
     },
     "logs": {
         "logs_collected": {
             "files": {
                 "collect_list": [
                     {
                         "file_path": "/path/to/pm2-log/error.log",
                         "log_group_name": "pm2-error-log",
                         "log_stream_name": "{ec2_instance_id}"
                     },
                     {
                         "file_path": "/path/to/pm2-log/info.log",
                         "log_group_name": "pm2-info-log",
                         "log_stream_name": "{ec2_instance_id}"
                     }
                 ]
             }
         }
     }
 }
```

### Reference

*   [https://stackoverflow.com/questions/62534276/send-pm2-logs-from-ec2-instance-to-cloudwatch](https://stackoverflow.com/questions/62534276/send-pm2-logs-from-ec2-instance-to-cloudwatch)
    
*   [https://www.rapidspike.com/blog/how-to-send-log-files-to-aws-cloudwatch-ubuntu/](https://www.rapidspike.com/blog/how-to-send-log-files-to-aws-cloudwatch-ubuntu/)