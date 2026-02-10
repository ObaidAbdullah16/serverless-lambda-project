# Serverless Newsletter Subscription System

A serverless web application that handles newsletter subscriptions automatically using AWS services. When users subscribe, they receive a confirmation email, the admin is notified, and the subscription data is stored in a database - all without managing any servers!

> **Note**: This is a demo project built to learn AWS serverless architecture. The website template is for demonstration purposes only.

---

## 🌐 Live Demo

**Check it out**: [https://jhgalkj.xyz/](https://jhgalkj.xyz/)

Try subscribing with your email to see the serverless workflow in action!

---

## 🎯 What Does This Project Do?

This application handles the complete newsletter subscription workflow:

1. **User subscribes** on the website with their email
2. **Lambda function** processes the subscription
3. **Email sent to user** confirming their subscription (via SES)
4. **Email sent to admin** notifying them of the new subscriber (via SES)
5. **Data stored** in DynamoDB for future reference

All of this happens automatically, without any server management!

---

## 🏗️ AWS Services Used

### **Amazon S3**
- **What it does**: Stores the static website files (HTML, CSS, JavaScript, images)
- **Why I used it**: S3 is perfect for hosting static websites - it's cheap, reliable, and scales automatically

### **Amazon CloudFront**
- **What it does**: Content Delivery Network (CDN) that delivers the website to users worldwide
- **Why I used it**: Makes the website load super fast by caching content in edge locations close to users, plus provides HTTPS

### **AWS Lambda**
- **What it does**: Runs the subscription processing code without needing to manage servers
- **Why I used it**: I only pay when someone subscribes (pay-per-use), and it scales automatically from 0 to thousands of requests

### **Amazon DynamoDB**
- **What it does**: NoSQL database that stores subscriber information
- **Why I used it**: Serverless database that scales automatically and has millisecond response times

### **Amazon SES (Simple Email Service)**
- **What it does**: Sends confirmation emails to subscribers and notification emails to admin
- **Why I used it**: Reliable, cost-effective email service that integrates seamlessly with Lambda

### **Amazon API Gateway**
- **What it does**: Creates the API endpoint that the website calls when users subscribe
- **Why I used it**: Acts as the "front door" for the Lambda function, handling HTTP requests from the website

---

## 🔄 How It Works - Complete Workflow

Here's exactly what happens when someone subscribes:

### **Step-by-Step Process:**

```
1. User visits website (CloudFront → S3)
   ↓
2. User enters email and clicks "Subscribe"
   ↓
3. Website sends request to API Gateway
   ↓
4. API Gateway triggers Lambda function
   ↓
5. Lambda function processes the subscription:
   - Validates the email
   - Stores data in DynamoDB
   - Sends confirmation email to user (SES)
   - Sends notification email to admin (SES)
   ↓
6. User sees "Successfully subscribed!" message
   ↓
7. User receives confirmation email
   ↓
8. Admin receives notification email
```

### **Visual Flow:**

```
┌─────────────┐
│    User     │
└──────┬──────┘
       │
       ▼
┌─────────────────┐      ┌──────────┐
│   CloudFront    │◄─────┤    S3    │
│      (CDN)      │      │ (Website)│
└────────┬────────┘      └──────────┘
         │
         ▼
┌─────────────────┐
│  API Gateway    │
└────────┬────────┘
         │
         ▼
┌─────────────────┐      ┌──────────────┐      ┌──────────┐
│     Lambda      │─────►│  DynamoDB    │      │   SES    │
│   (Function)    │      │  (Database)  │      │ (Email)  │
└─────────────────┘      └──────────────┘      └────┬─────┘
                                                     │
                                                     ▼
                                        ┌────────────────────┐
                                        │  User & Admin      │
                                        │  Receive Emails    │
                                        └────────────────────┘
```

---

## 🎯 Real-World Problem Solved

### **The Traditional Approach (Without Serverless):**

To build a subscription system the old way, you would need:
- ❌ A server running 24/7 (costs money even when no one is subscribing)
- ❌ Manual server maintenance, security patches, and updates
- ❌ Setting up and managing an email server or third-party integration
- ❌ Database server setup and maintenance
- ❌ Load balancer if you expect high traffic
- ❌ Manual scaling during traffic spikes

**Monthly Cost**: $20-$100+ for a server running 24/7

### **The Serverless Approach (This Project):**

With serverless architecture:
- ✅ No servers to manage - AWS handles everything
- ✅ Pay only when someone subscribes (could be $0-$5/month for moderate traffic)
- ✅ Automatically scales from 0 to thousands of subscriptions
- ✅ Built-in email service (SES)
- ✅ Serverless database (DynamoDB)
- ✅ No maintenance required

**Monthly Cost**: ~$1-$5 for hundreds of subscribers (mostly under AWS free tier!)

### **Benefits:**
- **Cost-Effective**: Only pay for what you use
- **Scalable**: Handles 1 subscriber or 10,000 subscribers automatically
- **Reliable**: 99.99% uptime guaranteed by AWS
- **Fast**: Global content delivery via CloudFront
- **Secure**: HTTPS, encryption, and AWS security built-in
- **No Maintenance**: No servers to patch or update

---

## 📁 Project Structure

```
serverless-lambda-project/
├── index.html              # Main website page with subscription form
├── css/                    # Website styling
├── js/                     # Frontend JavaScript (handles form submission)
├── img/                    # Website images
└── README.md              # This file
```

---

## 💡 What I Learned

This project taught me:
- ✅ How to build serverless applications on AWS
- ✅ Integrating multiple AWS services together
- ✅ Creating Lambda functions to process data
- ✅ Using API Gateway to expose Lambda functions
- ✅ Sending automated emails with SES
- ✅ Storing data in DynamoDB
- ✅ Hosting static websites with S3 and CloudFront
- ✅ Cost optimization with serverless architecture

---

## 🎓 Course Reference

This project was built following Section 2 of:
**AWS Mastery: Hands-On Cloud Projects for Engineers** on Udemy

Course Link: [Udemy Course](https://www.udemy.com/course/aws-mastery-hands-on-cloud-projects-for-engineers/)

---

## 💰 Estimated Cost

**AWS Free Tier includes:**
- Lambda: 1M free requests/month
- DynamoDB: 25GB storage + 25 write/read capacity units
- S3: 5GB storage + 20,000 GET requests
- CloudFront: 50GB data transfer + 2M requests
- SES: 62,000 emails/month (when called from Lambda)

**For moderate usage (100-500 subscribers/month):**
- Lambda: $0 (within free tier)
- DynamoDB: $0 (within free tier)
- S3: $0.50
- CloudFront: $1-2
- SES: $0 (within free tier)

**Total: ~$1-3/month** 🎉

---

## 🚀 Key Features

✅ Serverless architecture (no server management)  
✅ Automatic email confirmation to subscribers  
✅ Admin notification emails  
✅ Data storage in DynamoDB  
✅ Fast global content delivery  
✅ HTTPS enabled  
✅ Auto-scaling from 0 to thousands of requests  
✅ Cost-effective (pay-per-use model)

---

## 📧 Contact

For questions or feedback about this project, feel free to open an issue or reach out!

---

**Built with ☁️ AWS Serverless Services