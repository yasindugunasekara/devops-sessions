# Jenkins Basics

This document serves as a beginner-friendly guide to Jenkins and its dashboard. Follow the steps below to understand Jenkins and set up your first jobs and pipelines.

---

## **What is Jenkins?**

Jenkins is an open-source automation server that helps automate building, testing, and deploying software projects. It supports:

- **Continuous Integration (CI):** Automatically test and integrate code changes.
- **Continuous Delivery (CD):** Automate the deployment process.

**Why Jenkins?**

- Saves time by automating repetitive tasks.
- Reduces errors by following a consistent process.

---

## **Jenkins Dashboard Overview**

### **Main Features**

1. **Home Page:** Displays all jobs/pipelines with status indicators:

   - **Blue/Green:** Successful builds.
   - **Red:** Failed builds.
   - **Grey:** Not built yet.

2. **Main Menu Options:**

   - **New Item:** Create new jobs or pipelines.
   - **Manage Jenkins:** Configure settings and plugins.
   - **Build History:** View logs of previous builds.
   - **People:** List users with access to Jenkins.

3. **Search Box:** Quickly find jobs, builds, or configurations.

---

## **Installing Plugins**

Extend Jenkins functionality using plugins. Key plugins include:

- **Git:** Integrate Git repositories.
- **Pipeline:** Create pipeline jobs.
- **Docker:** Work with Docker containers.
- **GitHub:** Set up webhooks and integrate GitHub.

### **Steps to Install Plugins:**

1. Go to **Manage Jenkins > Manage Plugins**.
2. In the **Available** tab, search for the required plugin (e.g., "Git").
3. Install and restart Jenkins.

---

## **Creating a Freestyle Job**

Freestyle jobs allow you to execute basic tasks, like running a script or building a project.

### **Steps:**

1. Click **New Item** and enter a name (e.g., `HelloWorldJob`). Select **Freestyle project**.
2. Configure the job:
   - **Source Code Management:** Add a GitHub repository URL (e.g., `https://github.com/user/repo.git`).
   - **Build Step:** Add a shell command:
     ```bash
     echo "Hello, Jenkins!"
     ```
3. Save and click **Build Now**. View the console output to see the results.

---

## **Pipelines**

Pipelines are Jenkins' modern approach to CI/CD workflows using code.

### **Example Script:**

```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing the project...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the project...'
            }
        }
    }
}
```

### **Steps to Create a Pipeline Job:**

1. Click **New Item** and name the job (e.g., `SamplePipeline`). Select **Pipeline**.
2. Add the script in the **Pipeline** section.
3. Save and click **Build Now**. View the pipeline stages visually in the dashboard.

---

## **Build Triggers**

Automate job execution using triggers:

1. **Manual Trigger:** Default method where users click **Build Now**.
2. **SCM Trigger:** Trigger jobs when code is pushed to a repository. Example:
   - Enable **Poll SCM** and set `* * * * *` (every minute).
3. **Webhook Trigger:** Use GitHub webhooks for real-time triggers.

---

## **Configuring Credentials**

Securely store credentials (e.g., GitHub tokens, Docker Hub passwords) in Jenkins.

### **Steps:**

1. Go to **Manage Jenkins > Credentials**.
2. Add a credential with your GitHub username and token.
3. Use credentials in a pipeline:
   ```groovy
   withCredentials([usernamePassword(credentialsId: 'github-creds', usernameVariable: 'GIT_USER', passwordVariable: 'GIT_PASS')]) {
       sh 'git clone https://$GIT_USER:$GIT_PASS@github.com/user/repo.git'
   }
   ```

---

## **Viewing Build Results**

- **Build Logs:** Check the console output for build steps and debug errors.
- **Build History:** View a job's success and failure history.
- **Artifacts:** Archive and download build files (e.g., `.jar`, `.zip`).

---

## **Notifications**

Send build status notifications to developers:

- **Email Notifications:** Configure in **Manage Jenkins > Configure System**.
- **Slack Notifications:** Use the Slack plugin and integrate Slack Webhooks.

---

## **User Management**

Manage access and permissions:

1. Enable **Role-Based Authorization** in **Manage Jenkins > Configure Global Security**.
2. Add users and assign roles (Admin, Developer, Viewer).

---

## **Backup and Restore Jenkins**

Secure Jenkins data by backing up the `/var/jenkins_home` directory:

### **Steps:**

1. Backup all files regularly.
2. Restore by copying the files back to the same directory.

---
