\# 🚀 CI/CD Pipeline Project using Jenkins, Maven \& Tomcat



\## 📌 Project Overview



This project demonstrates a complete \*\*CI/CD (Continuous Integration \& Continuous Deployment) pipeline\*\* for a Java web application.



The pipeline automates:



\* Code integration from GitHub

\* Build process using Maven

\* Deployment to Apache Tomcat on EC2



\---



\## 🧩 Architecture



```

Developer → GitHub → Jenkins → Maven Build → Deploy to Tomcat (EC2)

```



\---



\## 🛠️ Technologies Used



\* ☁️ AWS EC2 (Jenkins Server \& Tomcat Server)

\* 🔧 Jenkins (CI/CD Automation)

\* 📦 Apache Maven (Build Tool)

\* 🌐 Apache Tomcat (Application Server)

\* 🗂️ Git \& GitHub (Version Control)

\* ☕ Java (Servlet-based Web Application)



\---



\## 📁 Project Structure



```

sample-app/

│── src/

│   ├── main/

│   │   ├── java/com/example/UserServlet.java

│   │   └── webapp/

│   │       ├── index.jsp

│   │       └── WEB-INF/web.xml

│── pom.xml

│── Jenkinsfile

```



\---



\## ⚙️ Setup \& Configuration



\### 1️⃣ Jenkins Server Setup



\* Install Jenkins on EC2

\* Install required tools:



&#x20; \* Java (JDK 17)

&#x20; \* Maven

&#x20; \* Git



\---



\### 2️⃣ Tomcat Server Setup



\* Install Apache Tomcat on EC2

\* Default deployment directory:



```

/opt/tomcat/webapps/

```



\---



\### 3️⃣ SSH Key Configuration



\* Generate SSH key on Jenkins server:



```bash

ssh-keygen

```



\* Copy public key to Tomcat server:



```bash

ssh-copy-id ec2-user@<TOMCAT\_PRIVATE\_IP>

```



\* Place private key in:



```

/var/lib/jenkins/.ssh/jenkinkey.pem

```



\---



\## 🔄 Jenkins Pipeline (Jenkinsfile)



```groovy

pipeline {

&#x20;   agent any



&#x20;   environment {

&#x20;       TOMCAT\_IP = "PRIVATE\_IP"

&#x20;       KEY = "/var/lib/jenkins/.ssh/jenkinkey.pem"

&#x20;   }



&#x20;   stages {



&#x20;       stage('Build') {

&#x20;           steps {

&#x20;               sh 'mvn clean package'

&#x20;           }

&#x20;       }



&#x20;       stage('Deploy') {

&#x20;           steps {

&#x20;               sh '''

&#x20;               scp -o StrictHostKeyChecking=no \\

&#x20;               -i $KEY target/sample-app.war \\

&#x20;               ec2-user@$TOMCAT\_IP:/opt/tomcat/webapps/

&#x20;               '''

&#x20;           }

&#x20;       }

&#x20;   }

}

```



\---



\## 🚀 Pipeline Flow



1\. Developer pushes code to GitHub

2\. Jenkins pulls latest code

3\. Maven builds WAR file

4\. WAR file is copied to Tomcat server

5\. Tomcat auto-deploys application



\---



\## 🌐 Access Application



After successful deployment:



```

http://<TOMCAT\_PUBLIC\_IP>:8080/sample-app/

```



\---



\## ✅ Output



\* Automated build \& deployment

\* Zero manual intervention after commit

\* Production-like CI/CD setup



\---



\## 🔥 Key Learnings



\* Jenkins Pipeline creation

\* Maven build lifecycle

\* SSH-based deployment

\* Debugging real-world CI/CD issues

\* Integration of multiple DevOps tools



\---



\## 🚀 Future Enhancements



\* Add GitHub Webhook (Auto trigger builds)

\* Integrate Docker for containerization

\* Deploy using Kubernetes (EKS)

\* Add Nginx + Load Balancer

\* Implement Blue-Green Deployment



\---



\## 🙌 Conclusion



This project demonstrates a \*\*real-world CI/CD pipeline\*\*, similar to industry practices, enabling automated and efficient software delivery.



\---



\### ⭐ If you like this project, give it a star!



