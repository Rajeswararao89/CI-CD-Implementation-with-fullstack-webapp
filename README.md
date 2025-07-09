# 🚀 CI/CD Implementation with Fullstack Web Application

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

## 📸 Screenshots

### ✅ Frontend Connected to Backend (Successful Integration)

![Frontend Screenshot](./assets/frontend-success.png)

- **Status**: `Backend is connected!`
- **Message**: `You've successfully integrated the backend!`
- **Backend URL**: `http://localhost:8000`

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



