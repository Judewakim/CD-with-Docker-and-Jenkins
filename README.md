# CD with Docker and Jenkins

This project demonstrates the implementation of a Continuous Integration and Continuous Deployment (CI/CD) pipeline using Jenkins within Docker containers. It emphasizes the use of persistent volumes to ensure data durability across container restarts and showcases automation techniques using Python and Docker Compose.

## 📁 Project Structure

```

CD-with-Docker-and-Jenkins/
├── jenkins-custom/
│   ├── Dockerfile
│   ├── automate.py
├── jenkins-docker-compose/
│   └── docker-compose.yml
└── README.md

````

- **jenkins-custom/**: Contains the custom Jenkins Dockerfile and a Python script (`automate.py`) to automate container setup.
- **jenkins-docker-compose/**: Holds the `docker-compose.yml` file for orchestrating Jenkins container deployment.

## 🚀 Getting Started

### Prerequisites

Ensure you have the following installed:

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)
- [Python 3.x](https://www.python.org/downloads/)
- Python packages: `docker`

Install the required Python package:

```bash
pip install docker
````

### 1. Using Docker Compose

Navigate to the `jenkins-docker-compose` directory and run:

```bash
docker-compose up -d
```

This command will:

* Pull the Jenkins LTS image from Docker Hub.
* Create a Docker volume for Jenkins data persistence.
* Run the Jenkins container with appropriate port mappings.

### 2. Using Custom Jenkins Image with Automation

Navigate to the `jenkins-custom` directory and execute:

```bash
python automate.py
```

This script will:

* Build a custom Jenkins Docker image using the provided Dockerfile.
* Create a Docker volume for persistent Jenkins data.
* Run the Jenkins container with specified configurations.
* Retrieve and display the initial admin password for Jenkins.

### 3. Access Jenkins

Once the Jenkins container is running, access the Jenkins UI by navigating to:

```
http://localhost:8080
```

Use the displayed admin password to unlock Jenkins and proceed with the setup.

## 🔄 Verifying Data Persistence

To ensure that Jenkins data persists across container restarts:

1. Stop and remove the running Jenkins container:

```bash
docker stop my-custom-jenkins
docker rm my-custom-jenkins
```

2. Re-run the Jenkins container using the same volume:

```bash
docker run -d `
  --name my-custom-jenkins `
  -p 8080:8080 `
  -v jenkins_data_custom:/var/jenkins_home `
  my-custom-jenkins
```

3. Access Jenkins at `http://localhost:8080` and verify that your previous configurations and user data are intact.

## 🧹 Cleanup

To remove the Jenkins container, image, and associated volume:

```bash
docker stop my-custom-jenkins
docker rm my-custom-jenkins
docker rmi my-custom-jenkins
docker volume rm jenkins_data_custom
```

## 📄 License

This project is licensed under the [MIT License](LICENSE).


