# 🚀 CI/CD Implementation for Fullstack Web Application

This project demonstrates a complete DevOps pipeline with a **FastAPI backend** and a **Next.js frontend**. The application is containerized using **Docker**, deployed on **AWS ECS (Fargate)**, infrastructure provisioned with **Terraform**, and integrated with **CI/CD using GitHub Actions**.

---

## 🔧 Tech Stack

- **Frontend**: Next.js
- **Backend**: FastAPI (Python)
- **Containerization**: Docker
- **Infrastructure**: AWS ECS (Fargate), ECR, ALB, IAM, VPC (via Terraform)
- **CI/CD**: GitHub Actions
- **Monitoring**: CloudWatch

---

## 📁 Project Structure

DevOps-Assignment/
├── backend/ # FastAPI backend
│ └── app/main.py
│ └── requirements.txt
├── frontend/ # Next.js frontend
│ └── pages/index.js
│ └── .env.production
├── terraform/ # Infrastructure as Code
│ └── main.tf
│ └── variables.tf
│ └── outputs.tf
├── .github/
│ └── workflows/deploy.yml # GitHub Actions CI/CD Workflow
├── Dockerfile (both in backend/ and frontend/)
└── README.md


---

## 📸 Project Screenshots

Below are some screenshots demonstrating the application's functionality:

![Frontend Page](https://github.com/user-attachments/assets/92338857-c5cd-4868-b84f-fcbc348a4204)

![AWS ECS](https://github.com/user-attachments/assets/442fba62-902b-45b2-96a9-b8c998712ad7)

![Frontend ECS1](https://github.com/user-attachments/assets/0dbda10e-cf3d-41d1-a8fc-7dc67f3ba60e)

![Backend ECS](https://github.com/user-attachments/assets/98f870d9-04e4-4bff-95fb-521a7af1b2e0)

![AWS ECR](https://github.com/user-attachments/assets/04963030-9a33-4140-adfb-227dcf026f72)

![AWS ALB](https://github.com/user-attachments/assets/51055b2f-d587-4207-b28c-0ad575bf0a61)

![AWS CloudWatch Alarm](https://github.com/user-attachments/assets/ca07dd92-57ea-420e-a85f-847e3d45366d)

![AWS CloudWatch DashBoard](https://github.com/user-attachments/assets/ab297d10-c004-40fd-b1ca-5943d41f304a)





---

## ⚙️ Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/Rajeswararao89/CI-CD-Implementation-with-fullstack-webapp.git
cd CI-CD-Implementation-with-fullstack-webapp

Backend Setup (FastAPI)
cd backend
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
uvicorn app.main:app --host 0.0.0.0 --port 8000
Visit: http://localhost:8000/docs


Frontend Setup (Next.js)
cd frontend
npm install

# Update API URL
echo "NEXT_PUBLIC_API_URL=http://localhost:8000" > .env.local

npm run dev
Visit: http://localhost:3000

Dockerize Backend & Frontend
# Backend
cd backend
docker build -t fastapi-backend .

# Frontend
cd ../frontend
docker build -t nextjs-frontend .

Push Docker Images to AWS ECR
# Login to AWS ECR
aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin <your-account>.dkr.ecr.ap-south-1.amazonaws.com

# Push images
docker tag fastapi-backend <your-ecr>/fastapi-backend
docker push <your-ecr>/fastapi-backend

docker tag nextjs-frontend <your-ecr>/nextjs-frontend
docker push <your-ecr>/nextjs-frontend

Provision Infrastructure (Terraform)
cd terraform
terraform init
terraform apply -auto-approve


CI/CD Setup (GitHub Actions)
Add secrets in GitHub repo under:

nginx
Copy
Edit
Settings > Secrets and variables > Actions
Required Secrets:

AWS_ACCESS_KEY_ID

AWS_SECRET_ACCESS_KEY

Workflow file: .github/workflows/deploy.yml


CI/CD Workflow Summary
On every push to main:
Code is checked out
Docker images are built and pushed to ECR
Terraform deploys infrastructure
ECS services are updated


✅ Output
Deployed frontend:
🔗 ALB Endpoint (ECS)

👨‍💻 Author
Rajeswara Rao
DevOps Intern | B.Tech CSE, LPU
GitHub: Rajeswararao89



