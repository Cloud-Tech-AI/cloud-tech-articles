Amazon S3 was launched 15 years ago on Pi Day, March 14, 2006, and created the first generally available AWS service. Over that time, data storage and usage has exploded, and the world has never been the same.

 
Amazon S3 has virtually unlimited scalability, and unmatched availability, durability, security, and performance. Customers of all sizes and industries can use S3 to store and protect any amount of data for a range of use cases, such as data lakes, websites, mobile applications, backup and restore, archive, and big data analytics.

![image](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/yi4a4eewnuqctydvn3vv.png)

My Background: I am Cloud , DevOps & Big Data Enthusiast | 4x AWS Certified | 3x OCI Certified | 3x Azure Certified . 

When you store data in Amazon Simple Storage Service (S3), you can easily share it for use by multiple applications. However, each application has its own requirements and may need a different view of the data. For example, a dataset created by an e-commerce application may include personally identifiable information (PII) that is not needed when the same data is processed for analytics and should be redacted. On the other side, if the same dataset is used for a marketing campaign, you may need to enrich the data with additional details, such as information from the customer loyalty database.

To provide different views of data to multiple applications, there are currently two options. You either create, store, and maintain additional derivative copies of the data, so that each application has its own custom dataset, or you build and manage infrastructure as a proxy layer in front of S3 to intercept and process data as it is requested. Both options add complexity and costs, so the S3 team decided to build a better solution.

![image](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/5v5g9yctrz1uaoong0gp.png)

Watch the On-Demand AWS Pi Week 4-day , virtual event which was hosted from March 15-18, 2021 hosted on the AWS channel on Twitch as AWS celebrated the 15th birthday of the AWS Cloud. the event included talks from AWS leaders and experts as they took us back in time reviewing the history of AWS and the key decisions involved in the building and evolution of Amazon S3. they also dived into how you can leverage S3 to control costs and continuously optimize your spend, while building modern, scalable applications.
 
The event is ideal to watch for anyone ( on-demand ) who is eager to learn more about:

How S3 and other AWS services are architected for availability and durability inside AWS Regions and Availability Zones
How S3's strong consistency model works to support many different workloads
The history of and best practices for S3 data security
How AWS architects evolvable services that provide new features and greater scalability with no disruption to customers
Detailed ways to move data into and out of the AWS Cloud 

[pi-week](https://pages.awscloud.com/pi-week-2021.html)

On-demand AWS Pi Week Twitch video streams

Day 1 - Amazon S3 origins - foundations of cloud infrastructure
[Video 1](https://www.twitch.tv/videos/950331443) | [Video 2](https://www.twitch.tv/videos/950384494)
Day 2 - Building data lakes and enabling data movement
[Video 1](https://www.twitch.tv/videos/951537246?filter=archives&sort=time) | [Video 2](https://www.twitch.tv/videos/951772985?filter=archives&sort=time)
Day 3 - Amazon S3 security framework and best practices
{% twitch 952756254 %}
Day 4 - Amazon S3 and the foundations of a serverless infrastructure
{% twitch 953961080 %}

# What's New

S3 Object Lambda was announced by AWS, a new capability that allows you to add your own code to process data retrieved from S3 before returning it to an application. S3 Object Lambda works with your existing applications and uses AWS Lambda functions to automatically process and transform your data as it is being retrieved from S3. The Lambda function is invoked inline with a standard S3 GET request, so you don’t need to change your application code.

In this way, you can easily present multiple views from the same dataset, and you can update the Lambda functions to modify these views at any time.

![image](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/j6fwlcikcl8nfqbsbw9v.png)

There are many use cases that can be simplified by this approach, for example:

Redacting personally identifiable information for analytics or non-production environments.
Converting across data formats, such as converting XML to JSON.
Augmenting data with information from other services or databases.
Compressing or decompressing files as they are being downloaded.
Resizing and watermarking images on the fly using caller-specific details, such as the user who requested the object.
Implementing custom authorization rules to access data.
You can start using S3 Object Lambda with a few simple steps:

Create a Lambda Function to transform data for your use case.
Create an S3 Object Lambda Access Point from the S3 Management Console.
Select the Lambda function that you created above.
Provide a supporting S3 Access Point to give S3 Object Lambda access to the original object.
Update your application configuration to use the new S3 Object Lambda Access Point to retrieve data from S3.

## Availability and Pricing

S3 Object Lambda is available today in all AWS Regions with the exception of the Asia Pacific (Osaka), AWS GovCloud (US-East), AWS GovCloud (US-West), China (Beijing), and China (Ningxia) Regions. You can use S3 Object Lambda with the AWS Management Console, AWS Command Line Interface (CLI), and AWS SDKs. Currently, the AWS CLI high-level S3 commands, such as aws s3 cp, don’t support objects from S3 Object Lambda Access Points, but you can use the low-level S3 API commands, such as aws s3api get-object.

With **S3 Object Lambda**, you pay for the AWS Lambda compute and request charges required to process the data, and for the data S3 Object Lambda returns to your application. You also pay for the S3 requests that are invoked by your Lambda function. For more pricing information, please see the Amazon S3 pricing page.

This new capability makes it much easier to share and convert data across multiple applications. 

## Amazon S3 Glacier announces a 40% price reduction for PUT and Lifecycle requests

Amazon S3 is reducing the cost to move data to Amazon S3 Glacier by lowering PUT and Lifecycle request charges by 40% for all AWS Regions. You can use the S3 PUT API to directly store compliance and backup data in S3 Glacier that does not require immediate access. You can also use S3 Lifecycle policies to move data from S3 Standard, S3 Standard-Infrequent Access, or S3 One Zone-Infrequent Access to S3 Glacier to save on storage costs when data becomes rarely accessed.

**Amazon S3 Glacier** is a secure, durable, and extremely low-cost Amazon S3 cloud storage class for data archiving and long-term backup. S3 Glacier provides a low-cost option for archiving data accessed once per quarter that needs to be accessible within minutes to a few hours.

In addition to being durable and secure, the S3 Glacier storage class is now even more cost-effective than before. Effective March 1, 2021, AWS is lowering the charges for PUT and Lifecycle requests to S3 Glacier by 40% for all AWS Regions. This includes the AWS GovCloud (US) Regions, the AWS China (Beijing) Region, operated by Sinnet, and the AWS China (Ningxia) Region, operated by NWCD. To learn more, see the S3 pricing page, and get started in the S3 console.

I hope this guide helps you understand all the new aws s3 features that were launched during the pi week, I know it's a little late to give a recap on "pi week" but I had like to do it anyways, feel free to contact me on [LinkedIn.](https://www.linkedin.com/in/adit-modi-2a4362191/)
You can view my badges [here.](https://www.youracclaim.com/users/adit-modi/badges)
If you are interested in learning more about AWS then follow me on [github.](https://github.com/AditModi)
If you liked this content then do clap and share it . Thank You .