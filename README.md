## Integrating SonarQube with Jenkins

This comprehensive guide will walk you through the process of seamlessly integrating SonarQube with Jenkins while establishing a straightforward pipeline for testing.

### 1. Create a Jenkins Container

Initiate the creation of a Jenkins container by executing the following Docker commands:

```bash
docker network create jenkins
docker run -it -d --name jenkins --network jenkins -p 8080:8080 -p 50000:50000 --restart=on-failure -v /home/ubuntu/jenkins_home:/var/jenkins_home jenkins/jenkins
```

### 2. Create a SonarQube Container

Execute the subsequent Docker command to generate a SonarQube container:

```bash
docker run --network=jenkins -d --name sonarqube -p 9000:9000 -p 9092:9092 sonarqube
```

### 3. Configure Webhooks on SonarQube

1. Log in to the SonarQube Administrative Console.
2. Navigate to Administration → Configuration → Webhooks.
3. Set the URL to `http://jenkins:8080/sonarqube-webhook/`.

### 4. Generate Token for Admin User in SonarQube

1. Navigate to Administration → Security → Users → Select the admin user.

### 5. Configure Token for the Admin User from SonarQube

1. Navigate to Administration → Security → Users → Token.

### 6. Add SonarQube Scanner Plugin on Jenkins

1. Navigate to Manage Jenkins → Plugins → Available Plugins.
2. Search for "SonarQube Scanner for Jenkins" and install the plugin.

### 7. Add the Sonarqube Credential

Navigate to Manage Jenkins → SonarQube → Add SonarQube.

### 8. Configure SonarQube on Jenkins

1. Navigate to Manage Jenkins → Configure System.
2. Add SonarQube with a name and server URL.

### 9. Create a Jenkins Pipeline

1. Navigate to New Item → Pipeline → Pipeline script from SCM.
2. Choose SCM → GIT and provide the repository URL: (https://github.com/ZiadSamehShehawy/Integrating-SonarQube-with-Jenkins.git).
