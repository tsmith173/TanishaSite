# Smith & Daughters: AWS Cloud Migration Project

## 🎯 Project Overview
**Role:** Cloud Engineer & DevOps Lead  
**Objective:** Migrate a legacy static web application created in 2021 from Netlify (PaaS) to AWS, implementing a fully serverless 3-tier architecture with CI/CD automation.

**Live Site:** http://tanisha-smith-portfolio.s3-website-us-east-1.amazonaws.com  
**GitHub Repository:** https://github.com/tsmith173/TanishaSite

---

## 🏗️ Architecture Diagram

### Data Flow
```
User Browser
    ↓
Amazon S3 (Static Website)
    ↓
API Gateway (REST API)
    ↓
AWS Lambda (Python Function)
    ↓
DynamoDB (Form Data Storage)

CI/CD Flow:
GitHub → CodePipeline → S3 (Auto-deployment)

Security:
IAM Roles → Lambda & CodePipeline Permissions
```

### Architecture Components

**Frontend Tier**
- Amazon S3: Static website hosting
- Content: HTML, CSS, JavaScript

**Application Tier**
- API Gateway: RESTful API endpoints (`POST /submit`, `OPTIONS /submit`)
- AWS Lambda: Serverless Python function for form processing

**Data Tier**
- DynamoDB: NoSQL database for persistent storage

**DevOps Pipeline**
- GitHub: Source code repository
- CodePipeline: Automated CI/CD deployments

**Security Layer**
- IAM: Role-based access control for all services
```

---

## 📊 Technical Architecture

### **Frontend Layer**
- **Amazon S3**: Static website hosting with public access
- **Bucket**: `tanisha-smith-portfolio`
- **Content**: HTML5, CSS3, JavaScript (ES6+)

### **CI/CD Pipeline**
- **AWS CodePipeline**: Automated deployment from GitHub to S3
- **Pipeline Name**: `tanisha-portfolio-cicd`
- **Trigger**: Manual release (webhook configuration available)
- **Deployment Time**: ~2 minutes

### **Backend Layer (Serverless)**
- **Amazon API Gateway**: HTTP API for RESTful endpoints
  - `POST /submit` - Form submission endpoint
  - `OPTIONS /submit` - CORS preflight handling
- **AWS Lambda**: Serverless compute function
  - **Runtime**: Python 3.12
  - **Function**: `ContactFormHandler`
  - **Features**: Form validation, data transformation, CORS handling

### **Data Layer**
- **Amazon DynamoDB**: NoSQL database for form submissions
  - **Table**: `ContactFormSubmissions`
  - **Pricing Model**: On-demand (pay-per-request)
  - **Primary Key**: `submissionId` (UUID)

### **Security & Access**
- **AWS IAM**: Role-based access control
  - Lambda execution role with DynamoDB permissions
  - CodePipeline service role
  - S3 bucket policy for public read access

---

## 💻 Technology Stack

### **AWS Services** (7 total)
- Amazon S3 (Storage & Hosting)
- AWS CodePipeline (CI/CD)
- AWS Lambda (Serverless Compute)
- Amazon API Gateway (REST API)
- Amazon DynamoDB (NoSQL Database)
- Amazon SES (Email Service - Sandbox)
- AWS IAM (Identity & Access Management)

### **Development**
- **Frontend**: HTML5, CSS3, JavaScript (Fetch API)
- **Backend**: Python 3.12
- **Data Format**: JSON
- **Version Control**: Git/GitHub
- **Documentation**: Markdown, Mermaid diagrams

---

## 🚀 Features

### ✅ Implemented
- Static website hosting on S3 with custom error pages
- CI/CD pipeline for automated deployments
- Serverless contact form with real-time submission
- NoSQL data persistence in DynamoDB
- CORS-enabled API for cross-origin requests
- Form validation and error handling
- IAM role-based security

### 🔄 In Progress
- CloudFront CDN for global content delivery
- Custom domain configuration (Route 53)
- SSL/TLS certificate management
- Email notifications (pending SES production access)

---

## 📋 Project Management

This project follows **Agile methodology** with sprint-based development.

**Project Board:** [View on GitHub Projects](../../projects)

### Completed Sprints

**Sprint 1: Infrastructure Setup** ✅
- Created S3 bucket with static hosting
- Configured public access policies
- Deployed initial static assets

**Sprint 2: CI/CD Implementation** ✅
- Set up CodePipeline
- Connected GitHub repository
- Configured automated S3 deployment

**Sprint 3: Serverless Backend** ✅
- Created Lambda function
- Configured API Gateway routes
- Integrated DynamoDB
- Resolved CORS configuration

### Future Enhancements
- CloudFront distribution for CDN
- Route 53 DNS management
- Infrastructure as Code (Terraform/CloudFormation)
- Automated testing pipeline
- CloudWatch monitoring and alerts

---

## 🛠️ Setup Instructions

### Prerequisites
- AWS Account with appropriate permissions
- GitHub Account
- Git installed locally
- AWS CLI configured (optional)

### Deployment Steps

**1. Clone Repository**
```bash
git clone https://github.com/tsmith173/TanishaSite.git
cd TanishaSite
```

**2. Create S3 Bucket**
- Bucket name: `your-unique-bucket-name`
- Region: US East (N. Virginia)
- Enable static website hosting
- Configure bucket policy for public access

**3. Set Up CodePipeline**
- Create pipeline connected to GitHub repository
- Configure deployment to S3 bucket
- Enable automatic deployments on push

**4. Create DynamoDB Table**
- Table name: `ContactFormSubmissions`
- Partition key: `submissionId` (String)
- Capacity mode: On-demand

**5. Deploy Lambda Function**
- Runtime: Python 3.12
- Add DynamoDB permissions to execution role
- Deploy function code

**6. Configure API Gateway**
- Create HTTP API
- Add routes: `POST /submit`, `OPTIONS /submit`
- Connect to Lambda function
- Enable CORS

**7. Update Contact Form**
- Replace API endpoint in `Contact.html`
- Test form submission

---

## 📈 Skills Demonstrated

### Cloud Engineering
✅ AWS service configuration and integration  
✅ Serverless architecture design  
✅ Infrastructure deployment and management  
✅ Cost optimization strategies

### DevOps Practices
✅ CI/CD pipeline implementation  
✅ Automated deployment workflows  
✅ Version control with Git/GitHub  
✅ Infrastructure documentation

### Software Development
✅ RESTful API development  
✅ Backend logic with Python  
✅ Frontend JavaScript integration  
✅ JSON data manipulation

### Problem Solving
✅ CORS troubleshooting and resolution  
✅ API Gateway integration debugging  
✅ IAM permission configuration  
✅ Systematic debugging approach

### Project Management
✅ Agile sprint planning  
✅ Issue tracking and documentation  
✅ Technical specification writing  
✅ Kanban board management

---

## 💰 Cost Analysis

**Monthly Operating Cost**: ~$0.05 - $0.50

### Cost Breakdown
- **S3**: ~$0.023/GB storage + $0.09/GB transfer (minimal for portfolio site)
- **Lambda**: First 1M requests free, then $0.20/1M requests
- **DynamoDB**: On-demand pricing, ~$0.25 per million writes
- **API Gateway**: First 1M requests free, then $1.00/1M requests
- **CodePipeline**: First pipeline free

**Free Tier Coverage**: This project operates entirely within AWS Free Tier limits for the first 12 months.

---

## 🔒 Security Considerations

### Implemented
- IAM role-based access control with least privilege principle
- S3 bucket policies for controlled public access
- CORS configuration to prevent unauthorized API access
- Environment-specific configuration management

### Best Practices Followed
- No hardcoded credentials in code
- Separate execution roles for each service
- Public access limited to static assets only
- API Gateway rate limiting (default)

---

## 📚 Lessons Learned

### Technical Insights
1. **CORS Configuration**: Understanding preflight OPTIONS requests is critical for cross-origin API calls
2. **Case Sensitivity**: S3 object keys are case-sensitive; maintain consistent file naming
3. **IAM Permissions**: Lambda functions require explicit permissions for each AWS service they access
4. **API Gateway Integration**: HTTP APIs differ from REST APIs in configuration and features

### Process Improvements
1. **Testing Strategy**: Test each layer independently before integration
2. **Documentation**: Clear issue tracking prevents context-switching overhead
3. **Iterative Development**: Sprint-based approach allows for manageable complexity
4. **Troubleshooting**: Browser developer tools are essential for debugging API calls

---

## 🎓 Learning Resources

### AWS Documentation
- [AWS Lambda Developer Guide](https://docs.aws.amazon.com/lambda/)
- [Amazon S3 User Guide](https://docs.aws.amazon.com/s3/)
- [API Gateway Developer Guide](https://docs.aws.amazon.com/apigateway/)
- [DynamoDB Developer Guide](https://docs.aws.amazon.com/dynamodb/)

### Related Projects
- [AWS Serverless Application Model (SAM)](https://aws.amazon.com/serverless/sam/)
- [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/)

---

## 👤 About

This project was developed as a portfolio piece demonstrating cloud engineering and DevOps capabilities for junior-level cloud positions.

**Project Timeline**: December 2024  
**Development Time**: 6-8 hours  
**Status**: Production-ready (Phase 1 complete)

### Contact
- **GitHub**: [@tsmith173](https://github.com/tsmith173)
- **Email**: tansmith@gmail.com
- **Portfolio**: [Live Demo](http://tanisha-smith-portfolio.s3-website-us-east-1.amazonaws.com)

---

## 📄 License

This project is available for educational and portfolio demonstration purposes.

---

## 🙏 Acknowledgments

- AWS Free Tier for providing accessible cloud resources
- GitHub for project management and version control tools
- Open source community for documentation and best practices

---

**⭐ If you found this project helpful, please consider starring the repository!**
