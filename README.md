# Docker Security for "todo-app" - Project Report

## Context

To ensure maximum security in application deployment, it is essential to follow best practices that minimize the risks of exploitation. In this project, we focus on deploying the "todo-app" application within Docker containers.

The main goal is to ensure that the containers are configured to run with a non-root user. This measure is crucial because, by limiting the container's privileges, the risk of potential vulnerabilities being exploited is significantly reduced. In this way, if an attacker manages to compromise the container, their actions will be restricted, preventing greater impact on the host system.

## Environment Configuration and Database Settings

To prepare the environment and ensure that the SQLite database operates correctly under a non-root user, follow these steps:

First, navigate to the project's main directory and find the `.env` file. This file is crucial as it contains the environment variables needed for the system to run properly. Open the `.env` file and look for the `MY_USER_NAME` variable. You need to set this variable to indicate the non-root user who will run the container. For example, if you want the user to be `Larry`, modify the variable as follows:


```env
MY_USER_NAME=Larry
```

Making this change ensures that the container runs under the specified user instead of as root, which is a recommended practice for security reasons.

Next, make sure that the `sqlite.js` configuration file matches the non-root username you specified. Open the `src/persistence/sqlite.js` file and find the SQLite file path on line 3. This path should match the username defined in the `.env` file. For instance, if the username is `Larry`, update the path as follows:

```javascript
  const dbPath = '/home/Larry/app/todos/todo.db';
```

Save the changes made to the `sqlite.js` file. This step is crucial to ensure that the SQLite database uses the correct path corresponding to the non-root user, making sure that this user has the appropriate permissions to access and modify the database.

By following these steps, you ensure that both the environment configuration and the SQLite database settings are correctly set up to operate under the specified non-root user, enhancing the system's security and management.

## Building and Running Containers

To build the Docker image and deploy the containers, execute the following command in your terminal:

```bash
docker-compose up --build
```
This command triggers the Docker build process as defined in the Dockerfile and starts the containers based on the docker-compose.yml configuration. The --build flag forces a rebuild of the Docker image, ensuring that any recent changes are included.

### Detailed Steps:

1. Navigate to the Project Directory: Ensure you are in the root directory of the project where the docker-compose.yml file is located.
2. Execute the Command: Run the docker-compose up --build command. Docker Compose will parse the docker-compose.yml file, build the necessary images, and start the defined services.
3. Monitor the Output: Monitor the terminal output for any errors or warnings that might indicate issues during the build or startup process. Resolve any issues as needed.

## Accessing the Application
Once the containers are running, you can access the "todo-app" by navigating to:

http://localhost:3000

This URL will open the application in your web browser. Ensure that port 3000 is not blocked by any firewall or security group settings on your machine.

### Detailed Steps:

1. Open a Web Browser: Use any web browser such as Chrome, Firefox, or Edge.
2. Navigate to the URL: Enter http://localhost:3000 in the address bar and hit Enter.
3. Interact with the Application: Verify that the application loads correctly and that you can interact with its features as expected.

## Project Execution

### Steps Taken
1. Environment Setup: Configured the `.env` file and adjusted `src/persistence/sqlite.js` to ensure the application runs with a non-root user. This step involved setting the MY_user variable and ensuring the SQLite database path matched the non-root user.
2. Building Containers: Successfully built the `Docker image using the docker-compose up --build` command. This process included creating the necessary Docker images and starting the application services.
3. Application Deployment: Deployed the "todo-app" within Docker containers and confirmed it runs without root privileges. This was verified by checking the running processes within the container to ensure they were executed by the non-root user.

### Testing and Validation

1. Functionality Tests: Verified that the application operates as expected within the Docker containers. This included testing the core features of the "todo-app" to ensure they function correctly.
2. Security Checks: Conducted security audits to ensure no vulnerabilities are present with the non-root user configuration. This involved reviewing the container's security posture, ensuring there are no excessive privileges, and confirming that best practices were followed.

### Maintenance and Recommendations
1. Regular Updates: Ensure Docker and Docker Compose are regularly updated to benefit from the latest security patches. This involves periodically checking for updates and applying them as necessary.
2. Backup Procedures: Implement regular backup procedures for the SQLite database located at `/home/[user]/app/todos/todo.db`. This includes setting up automated backups and verifying that backups can be restored successfully.
3. Documentation: Maintain comprehensive documentation for deployment and troubleshooting, including updating the README with any changes to the configuration process. This documentation should provide clear instructions for setting up the environment, building the containers, and accessing the application.

By following these steps, the project achieved a secure deployment of the "todo-app" within Docker containers, aligning with best practices for containerized application security. This ensures that the application is both functional and secure, minimizing the risk of exploitation and maintaining the integrity of the deployment.
