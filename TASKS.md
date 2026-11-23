# DevOps Team Project

Team: Mava and Amir  
Repository: <https://github.com/mavomen/DnkrDevOpsTeamProject>  
Assignment: Deploy a web application with Docker, Nginx, SSL/TLS, and Ansible  
Assignment brief: `docs/HW_L4_03_Team_Project.pdf`

This is our shared checklist for the project. We'll use it to keep track of the work, split responsibilities, and make sure we don't forget the evidence the instructor asked us to submit.

A task is done when we've implemented it, tested it, and saved any required output in the repository. A checked box should mean the work is actually complete, not just that we tried a command once.

---

## 1. What we're building

We'll choose a small web application that uses a database, containerize it, and deploy it to an Ubuntu 22.04 server. Nginx will handle incoming web traffic, HTTPS will be configured with a self-signed certificate, and Ansible will automate the server setup and deployment.

The work breaks down into these stages:

1. Prepare the Ubuntu server and check that we can connect to it.
2. Use Ansible to prepare the server.
3. Choose a suitable web application and understand how it works.
4. Write or adapt its Dockerfile and Compose configuration.
5. Run the application on the server.
6. Put Nginx in front of the application as a reverse proxy.
7. Enable HTTPS with a self-signed certificate.
8. Automate deployment and Nginx configuration with Ansible.
9. Document how the project works and how to run it.
10. Review the repository and prepare the final submission.

One important distinction: `DnkrDevOpsTeamProject` is our team repository. The web application we'll containerize is a separate project that we'll choose from GitHub in Stage 3.

## 2. The team

### Mava

Self-taught programmer with 8 years of programming experience. Mava will mainly take care of the server, infrastructure, and Ansible work.

### Amir

Computer science student. Amir will mainly take care of choosing and understanding the application, then building and testing its Docker setup.

These are starting responsibilities, not walls between us. We'll review each other's work and make sure we both understand the full project.

### Who takes the lead on what?

| Work                                              | Main lead | Working together                                     |
| ------------------------------------------------- | --------- | ---------------------------------------------------- |
| Server setup, SSH, and system checks              | Mava      | Amir reviews and tests the connection                |
| Ansible installation, inventory, and server setup | Mava      | Amir reviews the playbook                            |
| Choosing and understanding the web application    | Amir      | Mava reviews the choice and application requirements |
| Dockerfile, Compose, and local testing            | Amir      | Mava reviews the container setup                     |
| Deploying the application to the server           | Mava      | Amir checks the application behavior                 |
| Nginx reverse proxy                               | Both      | Review the config and test it together               |
| SSL/TLS and HTTPS                                 | Both      | Review certificate handling and test the connection  |
| Full deployment and troubleshooting               | Both      | Both should be able to reproduce the main tests      |
| README and project documentation                  | Both      | Review each other's sections                         |
| Final report and submission                       | Both      | Check the final repository together                  |

### How we'll work together

- [ ] Agree on the responsibility split before implementation. Update the table if we change it.
- [ ] Keep `main` usable. Do the work in focused branches and merge changes after review.
- [ ] Make commits that explain what changed. Avoid giant commits that mix unrelated work.
- [ ] Review each other's important Docker, Ansible, Nginx, and SSL changes.
- [ ] Test each stage before moving on to the next one.
- [ ] Save real command output and test results where the assignment asks for them.
- [ ] Keep each other in the loop when a decision or implementation detail changes.
- [ ] Write the final contribution report based on what we actually did, not just the plan in this file.

### Before we call the project finished

- [ ] Amir can explain how the Ansible inventory and server-preparation playbook work.
- [ ] Mava can explain the application runtime, its dependencies, Dockerfile, Compose services, and database persistence.
- [ ] Both of us can explain the request path: browser/client → Nginx → application → database.
- [ ] Both of us can explain how Ansible deploys the application and configures Nginx.
- [ ] Both of us can show the HTTP-to-HTTPS redirect and explain why a self-signed certificate triggers a browser warning.
- [ ] Both of us can run the important verification commands without depending on the other person to do it.

---

## 3. Decisions to make first

Let's settle these before we build around assumptions. We'll record the choices in the relevant project documentation as we go.

- [ ] Web application: Find a small GitHub project with a web interface, an application/backend component, and a database.
- [ ] Application stack: Identify its language, runtime, package manager, dependencies, entry point, and startup command.
- [ ] Database: Identify the database engine and version, required configuration, internal port, and data directory.
- [ ] Server: Choose an Ubuntu 22.04 Server VM or VPS.
  - [ ] Make sure it has at least 2 GB RAM and 20 GB of disk space.
  - [ ] Make sure the machine running Ansible can reach it over SSH.
- [ ] Hostname: Choose a local hostname, for example `myapp.local`, and map it to the server IP in the client machine's `/etc/hosts` file.
- [ ] Ports: Write down the application's listening port, database port, and public HTTP/HTTPS ports.
- [ ] Deployment method: Decide whether the server will clone the application/repository or receive files through Ansible.
- [ ] Secrets: Decide how we'll provide passwords and environment-specific values without committing them to Git.
- [ ] Evidence: Agree where we'll save command output, test results, and screenshots. Remove credentials and other secrets before committing evidence.

---

## 4. When is the project done?

We'll be ready to submit when:

- [ ] We've selected, cloned, and documented a suitable database-backed web application.
- [ ] The Ubuntu 22.04 server is reachable over SSH and its system information is recorded.
- [ ] Ansible can connect to the server and install/configure the required tools, Docker, Nginx, and firewall rules.
- [ ] The application Docker image builds successfully.
- [ ] Docker Compose runs the application and database with the required network, configuration, persistence, dependencies, and restart behavior.
- [ ] We've tested the application locally and saved the build output, container status, and test results.
- [ ] The application is running on the remote server and can be reached from the client machine.
- [ ] Nginx forwards requests to the application and sets the required headers.
- [ ] HTTP redirects to HTTPS, and the application is available over HTTPS with the self-signed certificate.
- [ ] Ansible can run the application deployment and Nginx/SSL setup in the right order.
- [ ] We've run the automation more than once and checked that the second run doesn't make unnecessary changes.
- [ ] The required evidence files are present and contain real output.
- [ ] The README, architecture, deployment, and troubleshooting documents are complete.
- [ ] The Git history, project summary, final directory structure, and team contribution report are committed.
- [ ] Both of us have reviewed the result and can explain how the whole setup works.

---

# Work checklist

## Stage 1 — Get the server ready

Lead: Mava  
Review: Amir

### 1.1 Set up the Ubuntu server

- [x] Create an Ubuntu 22.04 Server VM or get an Ubuntu 22.04 VPS.
- [x] Check that it has at least 2 GB RAM and 20 GB disk space.
- [x] Set up networking so the machine running Ansible can reach the server.
- [x] Record the server IP address and SSH username.
- [x] Set up SSH access and make sure it works.
- [x] Keep passwords and private SSH keys out of the repository.

Save this:

- [x] `01_environment/server_info.md`
  - [x] Server IP address.
  - [x] SSH username and connection method.
  - [x] CPU, RAM, and disk information.
  - [x] No passwords, private keys, or other secrets.

### 1.2 Connect and inspect the server

- [x] Connect to the server over SSH.
- [x] Check the kernel version.
- [x] Check the Ubuntu version.
- [x] Check disk usage.
- [x] Check memory usage.
- [x] List the network interfaces.
- [x] Save the commands and their output in a readable format.

Save this:

- [x] `01_environment/server_connection.txt`

Stage 1 is complete when: SSH works from the machine we'll use to run Ansible, and we've recorded the server's OS and hardware details. **DONE (Mava, solo)**.

---

## Stage 2 — Prepare the server with Ansible

Lead: Mava  
Review: Amir

### 2.1 Install Ansible

- [x] Install Ansible on the control machine.
- [x] Check that Ansible runs and record its version.
- [x] Confirm that SSH authentication and privilege escalation are set up correctly.

### 2.2 Create the inventory and test the connection

- [x] Create `02_ansible_setup/inventory` in INI or YAML format.
- [x] Add the Ubuntu server to the inventory.
- [x] Set the connection variables we need.
- [x] Set the Python interpreter if the target needs it.
- [x] Run `ansible -m ping` against the server.
- [x] Run `ansible -m setup` and save the host facts.

Save these:

- [x] `02_ansible_setup/inventory`
- [x] `02_ansible_setup/ping_test.txt`
- [x] `02_ansible_setup/facts.txt`

### 2.3 Write the server setup playbook

- [x] Create `02_ansible_setup/server_setup.yml`.
- [x] Update the package index and upgrade packages as appropriate.
- [x] Install `curl`, `wget`, `git`, `vim`, and `htop`.
- [x] Install and configure UFW.
- [x] Install Docker and Docker Compose using a method that works on the target Ubuntu version.
- [x] Enable and start the Docker service.
- [x] Add the intended remote user to the `docker` group.
- [x] Install, enable, and start Nginx.
- [x] Allow SSH (22), HTTP (80), and HTTPS (443) through the firewall.
- [x] Use `become` where administrative permissions are needed.
- [x] Run the playbook and save its output.
- [x] Check the Docker and Nginx versions.
- [x] Check that the required services are running and the firewall rules are in place.

Save these:

- [x] `02_ansible_setup/server_setup.yml`
- [x] `02_ansible_setup/playbook_output.txt`
- [x] `02_ansible_setup/verification.txt` — Docker version, Nginx version, service status, and firewall status/rules.

Stage 2 is complete when: Ansible connects successfully and the playbook leaves the server with the required packages, services, user permissions, and firewall rules. **DONE (Mava, solo lead)**.

---

## Stage 3 — Choose and inspect the web application

Lead: Amir  
Review: Mava

### 3.1 Choose an application

- [ ] Find a small web application on GitHub that uses a database.
- [ ] Make sure it has a web interface and an application/backend component.
- [ ] Check that the project is a reasonable size for this assignment and that we can understand how it runs.
- [ ] Check its license and save the upstream repository URL.
- [ ] Look at its setup instructions and recent activity to see whether it's practical to use.
- [ ] Agree on the application and database before starting the Docker work.

Some places and search terms to start with:

- `docker/awesome-compose`
- `docker compose flask mysql example`
- `docker compose nginx flask mysql`
- `docker example voting app`

### 3.2 Clone it and understand how it works

- [ ] Clone the chosen repository under `03_project_clone/`.
- [ ] Inspect the directory structure and list the important files.
- [ ] Find the application's entry point and startup command.
- [ ] Identify its runtime, dependencies, and build/install requirements.
- [ ] Find the application and database ports.
- [ ] List the environment variables and configuration files it needs.
- [ ] Understand how the application connects to the database.
- [ ] Check whether the database needs initialization scripts or migrations.
- [ ] Look for an existing Dockerfile or Compose file and decide what we can reuse.
- [ ] Record how to run the application outside Docker, if the project supports it.
- [ ] Where practical, run the application once using its own instructions before containerizing it.

Save these:

- [ ] `03_project_clone/project_structure.txt` — directory tree and important files.
- [ ] `03_project_clone/project_info.md` — upstream URL, short description, technologies, dependencies, and ports.

Stage 3 is complete when: We both understand how the application starts, how it talks to the database, and which ports and settings it needs.

---

## Stage 4 — Containerize the application

Lead: Amir  
Review: Mava

### 4.1 Check what the project already provides

- [ ] Check whether the upstream project already has a Dockerfile.
- [ ] Check whether it already has a Compose file.
- [ ] Read the existing container configuration and note anything missing or unsafe.
- [ ] Write down the required ports, environment variables, volumes, and service dependencies.
- [ ] Decide what belongs in the image and what should be passed in at runtime.

### 4.2 Write the Dockerfile

- [ ] Create `04_docker/Dockerfile`.
- [ ] Choose a suitable official base image and version.
- [ ] Set the working directory.
- [ ] Install the application's dependencies.
- [ ] Copy the required application files into the image.
- [ ] Document the port the application listens on.
- [ ] Set the correct command to start the application.
- [ ] Keep the image reasonably small. Use multi-stage builds if they make sense for this application.
- [ ] Add `04_docker/.dockerignore` if needed.
- [ ] Avoid putting secrets in the image. Use a non-root user where practical.
- [ ] Explain the important parts of the Dockerfile in plain language.

Save these:

- [ ] `04_docker/Dockerfile`
- [ ] `04_docker/.dockerignore` (if needed)
- [ ] `04_docker/dockerfile_explanation.md`

### 4.3 Write the Compose file

- [ ] Create `04_docker/docker-compose.yml`.
- [ ] Add the web application service.
- [ ] Add the database service.
- [ ] Put the services on an appropriate Compose network.
- [ ] Add a named volume so database data survives container recreation.
- [ ] Configure the required environment variables without committing real secrets.
- [ ] Set up port mappings. Don't expose the database port publicly unless the project actually needs it.
- [ ] Set the service dependencies.
- [ ] Add health checks where they're supported and useful.
- [ ] Choose restart policies.
- [ ] Explain how the services, network, volumes, and configuration fit together.

Save these:

- [ ] `04_docker/docker-compose.yml`
- [ ] `04_docker/compose_explanation.md`

### 4.4 Build and test it locally

- [ ] Build the images.
- [ ] Start the containers in the background.
- [ ] Check the services with `docker compose ps` (or `docker-compose ps` if that's what the installed version supports).
- [ ] Read the application and database logs.
- [ ] Open the application in a browser or test it with `curl`.
- [ ] Confirm that the application can connect to the database.
- [ ] Check that database data is still there after recreating the containers.
- [ ] Fix any problems and repeat the tests.
- [ ] Save the actual build output and test results.

Save these:

- [ ] `04_docker/build_log.txt`
- [ ] `04_docker/container_status.txt`
- [ ] `04_docker/test_results.txt`

Stage 4 is complete when: The full Compose stack builds and starts locally, the application responds, and we've tested the database connection and data persistence.

---

## Stage 5 — Deploy the application to the server

Lead: Mava  
Review: Amir

### 5.1 Move the project files to the server

- [ ] Choose how to get the files onto the server: `scp`, `rsync`, Git clone, or Ansible copy/synchronization.
- [ ] Transfer the application code, Dockerfile, Compose file, and required configuration.
- [ ] Keep the directory structure intact.
- [ ] Check file ownership and permissions on the server.
- [ ] Make sure secrets are provided securely and aren't added to tracked files.

### 5.2 Build and start the application on the server

- [ ] Connect to the server over SSH.
- [ ] Go to the deployment directory.
- [ ] Build the Docker images.
- [ ] Start the Compose services in detached mode.
- [ ] Check the container status.
- [ ] Read the application and database logs.
- [ ] Fix any issues that only appear on the server.

Save these:

- [ ] `05_deployment/deploy_log.txt`
- [ ] `05_deployment/container_status.txt`
- [ ] `05_deployment/container_logs.txt`

### 5.3 Check that we can reach the application

- [ ] Test the application from the server itself.
- [ ] Test it from the local/control machine using the server IP and mapped application port, where applicable.
- [ ] Check that the response comes from the application we deployed.
- [ ] Save the results and a response sample or screenshot.

Save this:

- [ ] `05_deployment/test_results.txt` — include the server-side test, local-machine test, and a response sample or screenshot.

Stage 5 is complete when: The application is running on the server, responds from the expected network location, and its containers and logs look healthy.

---

## Stage 6 — Put Nginx in front of the application

Owners: Both  
Coordination: Amir checks the application and upstream port; Mava checks the server-side Nginx setup.

### 6.1 Decide how Nginx will reach the application

- [ ] Choose the hostname we'll use, for example `myapp.local`.
- [ ] Confirm the application's host/container port.
- [ ] Decide how the Nginx service on the server will reach the application.
- [ ] Decide which requests Nginx should forward to the application.
- [ ] Plan to forward these headers: `Host`, `X-Real-IP`, `X-Forwarded-For`, and `X-Forwarded-Proto`.
- [ ] Think through what should happen when the application is unavailable.

### 6.2 Write the Nginx site configuration

- [ ] Create a site configuration for the chosen hostname.
- [ ] Listen on port 80.
- [ ] Set the correct `server_name`.
- [ ] Forward requests to the application with `proxy_pass`.
- [ ] Set the forwarding headers with `proxy_set_header`.
- [ ] Add sensible timeout or error handling if the application needs it.
- [ ] Explain the configuration so we can walk someone through it.

Save these:

- [ ] `06_nginx/nginx_config.txt`
- [ ] `06_nginx/nginx_explanation.md`

### 6.3 Enable the site

- [ ] Put the configuration in `/etc/nginx/sites-available/`.
- [ ] Create a symbolic link in `/etc/nginx/sites-enabled/`.
- [ ] Disable the default site if it conflicts with our configuration.
- [ ] Run `nginx -t` and fix any errors.
- [ ] Reload Nginx.
- [ ] Check that Nginx is running and listening on port 80.

### 6.4 Set up the hostname on the local machine

- [ ] Add an entry to the local machine's `/etc/hosts` that maps the hostname to the server IP.
- [ ] Save the relevant hosts-file entry as evidence.
- [ ] Check that the hostname resolves to the correct server.

Save this:

- [ ] `06_nginx/hosts_file.txt`

### 6.5 Test the reverse proxy

- [ ] Open the application using the hostname, not just the server IP.
- [ ] Check that Nginx forwards the request to the application.
- [ ] Inspect the response and relevant headers.
- [ ] Troubleshoot any routing issues or `502 Bad Gateway` responses.

Save this:

- [ ] `06_nginx/test_results.txt`

Stage 6 is complete when: The local hostname points to the server and Nginx successfully forwards HTTP requests to the application.

---

## Stage 7 — Add HTTPS with a self-signed certificate

Owners: Both  
Coordination: Mava handles the certificate and server integration; Amir reviews the HTTPS proxy behavior and tests the application.

### 7.1 Create the certificate

- [ ] Create a directory for the certificates on the server.
- [ ] Generate a private key.
- [ ] Create a certificate request and a self-signed certificate for our hostname.
- [ ] Set restrictive permissions on the private key and certificate directory.
- [ ] Check the certificate subject/SAN and expiry date.
- [ ] Keep the private key out of Git and out of logs or screenshots.

Save this:

- [ ] `07_ssl/certificate_info.txt` — include the certificate path, non-secret certificate details, and expiry date. Do not include the private key or its contents.

### 7.2 Update Nginx for HTTPS

- [ ] Redirect HTTP requests to HTTPS.
- [ ] Configure Nginx to listen on port 443 with SSL enabled.
- [ ] Point Nginx to the certificate and private key.
- [ ] Choose supported TLS protocol versions and sensible cipher settings for the installed Nginx/OpenSSL version.
- [ ] Keep the reverse-proxy behavior and required forwarding headers.
- [ ] Save the complete Nginx configuration.

Save this:

- [ ] `07_ssl/nginx_ssl_config.txt`

### 7.3 Reload Nginx and test HTTPS

- [ ] Run `nginx -t` and fix any configuration errors.
- [ ] Reload Nginx.
- [ ] Check that HTTP redirects to HTTPS.
- [ ] Check that the HTTPS endpoint responds. For this lab, `curl -k` can be used to bypass local certificate trust validation.
- [ ] Inspect the certificate details and expiry date.
- [ ] Note in the results that browsers normally warn about self-signed certificates unless the certificate is explicitly trusted.

Save this:

- [ ] `07_ssl/test_results.txt` — include the redirect test, HTTPS test, and certificate information.

Stage 7 is complete when: HTTP redirects to HTTPS and the application is available through Nginx on port 443 using our certificate.

---

## Stage 8 — Automate the deployment with Ansible

Lead: Mava  
Review: Amir

### 8.1 Plan the playbooks

Before writing the playbooks, let's agree on the order and what each one needs to do.

- [ ] Break the deployment into clear, repeatable steps.
- [ ] Identify which steps depend on earlier ones.
- [ ] Decide which values should be variables, such as the hostname, paths, and application port.
- [ ] Decide where handlers are needed to restart or reload services.
- [ ] Identify which configuration files should be Jinja2 templates.
- [ ] Decide how we'll provide secrets safely.
- [ ] Decide how each playbook will check whether its work succeeded.

### 8.2 Automate application deployment

- [ ] Create `08_ansible_automation/deploy_app.yml`.
- [ ] Create the application directory on the server.
- [ ] Copy or obtain the Dockerfile, Compose file, application code, and non-secret configuration.
- [ ] Build the Docker images using an appropriate Ansible module or a documented, repeatable command.
- [ ] Start the containers.
- [ ] Wait for the application to become ready.
- [ ] Check the container status and application response.
- [ ] Capture useful output for troubleshooting.
- [ ] Keep sensitive values out of tracked plaintext variable files.

Save these:

- [ ] `08_ansible_automation/deploy_app.yml`
- [ ] `08_ansible_automation/app_vars.yml` (only if we need it; no plaintext secrets)

### 8.3 Automate Nginx and SSL configuration

- [ ] Create `08_ansible_automation/deploy_nginx.yml`.
- [ ] Create the certificate directory with safe permissions.
- [ ] Generate or install the self-signed certificate using suitable Ansible modules or tools.
- [ ] Create `08_ansible_automation/templates/nginx.conf.j2`.
- [ ] Deploy the rendered Nginx configuration.
- [ ] Enable our site.
- [ ] Disable the default site if needed.
- [ ] Validate the Nginx configuration before reloading it.
- [ ] Use a handler so Nginx reloads only when its configuration changes.
- [ ] Keep the hostname, upstream, and certificate paths configurable.

Save these:

- [ ] `08_ansible_automation/deploy_nginx.yml`
- [ ] `08_ansible_automation/templates/nginx.conf.j2`
- [ ] `08_ansible_automation/nginx_vars.yml` (only if we need it)

### 8.4 Create the main playbook

- [ ] Create `08_ansible_automation/site.yml`.
- [ ] Import the application and Nginx playbooks in the right order.
- [ ] Keep host targeting and variables reusable.
- [ ] Make sure one command can run the full deployment.

Save this:

- [ ] `08_ansible_automation/site.yml`

### 8.5 Run and check the automation

- [ ] Run Ansible syntax checks on the playbooks.
- [ ] Review a dry run with `--check`. Use `--diff` where it is safe to do so.
- [ ] Run the complete playbook.
- [ ] Save the actual output.
- [ ] Review the output and fix any errors.
- [ ] Check the application containers and response after deployment.
- [ ] Check Nginx, the HTTP redirect, HTTPS, and certificate details.
- [ ] Run the playbook again and check that it doesn't make unnecessary changes.
- [ ] Review the automation together so both of us can explain it.

Save these:

- [ ] `08_ansible_automation/playbook_output.txt`
- [ ] `08_ansible_automation/verification.txt`

Stage 8 is complete when: One Ansible run can deploy the application and configure Nginx/SSL, the checks pass, and running it again is safe.

---

## Stage 9 — Write the documentation

Owners: Both  
Review: We'll read each other's sections and check that the instructions actually work.

### 9.1 README

- [ ] Explain what the project does.
- [ ] List the prerequisites.
- [ ] Explain how to install and configure it.
- [ ] Show how to run and deploy it.
- [ ] Include the project structure.
- [ ] Document configuration and environment variables without exposing secrets.
- [ ] Add links to the detailed guides and troubleshooting notes.
- [ ] Mention that this lab uses a self-signed certificate.

Save this:

- [ ] Root `README.md`

### 9.2 Architecture notes

- [ ] Explain the application, database, Docker network/volumes, server, Nginx, and Ansible components.
- [ ] Show how a request travels from the client through Nginx to the application and database.
- [ ] Show how Ansible deploys and configures the services.
- [ ] Add a text-based diagram using ASCII or Mermaid.

Save this:

- [ ] `09_documentation/architecture.md`

### 9.3 Deployment guide

- [ ] Write the deployment steps in the order someone should follow them.
- [ ] Include the commands needed at each step.
- [ ] Show how to check that each step worked.
- [ ] Explain how to run the Ansible deployment.
- [ ] Explain how to test HTTP-to-HTTPS redirection and HTTPS access.
- [ ] Explain the hostname and local `/etc/hosts` setup.

Save this:

- [ ] `09_documentation/deployment_guide.md`

### 9.4 Troubleshooting guide

- [ ] Cover common Docker build and startup problems.
- [ ] Cover Ansible, SSH, inventory, and permission problems.
- [ ] Cover Nginx `502 Bad Gateway` and incorrect upstream/port settings.
- [ ] Cover certificate path, permission, expiry, and trust problems.
- [ ] For each issue, explain the likely cause and how to fix or investigate it.

Save this:

- [ ] `09_documentation/troubleshooting.md`

Stage 9 is complete when: Someone who wasn't involved in building the project can follow the docs to understand, run, and check it.

---

## Stage 10 — Final review and submission

Owners: Both

### 10.1 Check Git and the commit history

- [ ] Make sure all required source, configuration, documentation, and evidence files are tracked.
- [ ] Check that `.gitignore` excludes secrets, private keys, local environment files, and unnecessary generated files.
- [ ] Review the commit history and make sure the messages describe the changes.
- [ ] Push the project to the GitHub repository.
- [ ] Save the commit graph.

Save this:

- [ ] `10_delivery/git_history.txt` — output from `git log --oneline --graph`.

### 10.2 Write the project summary

- [ ] Summarize what we built and how the pieces fit together.
- [ ] Describe the main problems we ran into.
- [ ] Explain how we solved them.
- [ ] Write down what we learned.
- [ ] Mention possible improvements, making it clear which ones are future work.

Save this:

- [ ] `10_delivery/project_summary.md`

### 10.3 Record the final project structure

- [ ] Generate a `tree` or `find` listing of the repository.
- [ ] Check that every required evidence file exists and can be read.

Save this:

- [ ] `10_delivery/final_structure.txt`

### 10.4 Record what each of us contributed

- [ ] Describe the final task split.
- [ ] Record Mava's actual contributions.
- [ ] Record Amir's actual contributions.
- [ ] Mention the challenges each of us faced and how we handled them.
- [ ] Make sure the report reflects what we really did, including any changes from the original plan.

Save this:

- [ ] `10_delivery/team_contribution.md`

### 10.5 Final check

- [ ] Review the entire repository together.
- [ ] Where the environment allows, follow the documented process from a clean state.
- [ ] Check that the final hostname and HTTPS behavior are documented.
- [ ] Search for accidentally committed passwords, tokens, private keys, or other secrets.
- [ ] Compare the repository against the assignment brief and make sure all required outputs are present.
- [ ] Submit the assignment through the instructor's platform.
- [ ] Check the required submission filename format: exercise name plus the student's name in English, as requested by the instructor.

We're ready to submit when: The project is working, the instructions are usable, both of us have reviewed it, and the repository contains the required evidence without exposing secrets.

---

## Required files checklist

Use this table for a quick final check. The detailed tasks above explain what each file should contain.

| Stage                 | Files to include                                                                                                                                                                                 |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1. Environment        | `01_environment/server_info.md`, `01_environment/server_connection.txt`                                                                                                                          |
| 2. Ansible setup      | `02_ansible_setup/inventory`, `ping_test.txt`, `facts.txt`, `server_setup.yml`, `playbook_output.txt`, `verification.txt`                                                                        |
| 3. Application        | `03_project_clone/project_structure.txt`, `03_project_clone/project_info.md`                                                                                                                     |
| 4. Docker             | `04_docker/Dockerfile`, optional `.dockerignore`, `dockerfile_explanation.md`, `docker-compose.yml`, `compose_explanation.md`, `build_log.txt`, `container_status.txt`, `test_results.txt`       |
| 5. Deployment         | `05_deployment/deploy_log.txt`, `container_status.txt`, `container_logs.txt`, `test_results.txt`                                                                                                 |
| 6. Nginx              | `06_nginx/nginx_config.txt`, `nginx_explanation.md`, `hosts_file.txt`, `test_results.txt`                                                                                                        |
| 7. SSL/TLS            | `07_ssl/certificate_info.txt`, `nginx_ssl_config.txt`, `test_results.txt`                                                                                                                        |
| 8. Ansible automation | `08_ansible_automation/deploy_app.yml`, optional `app_vars.yml`, `deploy_nginx.yml`, `templates/nginx.conf.j2`, optional `nginx_vars.yml`, `site.yml`, `playbook_output.txt`, `verification.txt` |
| 9. Documentation      | Root `README.md`, `09_documentation/architecture.md`, `deployment_guide.md`, `troubleshooting.md`                                                                                                |
| 10. Delivery          | `10_delivery/git_history.txt`, `project_summary.md`, `final_structure.txt`, `team_contribution.md`                                                                                               |

---

## A few things to keep in mind

### Security

- [ ] Don't commit passwords, API tokens, private SSH keys, database credentials, real `.env` files, or TLS private keys.
- [ ] Keep secret-bearing local files in `.gitignore`. Add safe example files such as `.env.example` when useful.
- [ ] Check logs, screenshots, `server_info.md`, and playbook output before committing them. Remove any secrets.
- [ ] Keep private-key permissions restrictive. Only record non-secret certificate details.

### Reliability and testing

- [ ] Prefer official base images and avoid installing packages the application doesn't need.
- [ ] Use a named volume for database data so it survives container recreation.
- [ ] Don't assume a running container means the application is ready. Use health checks or another readiness test.
- [ ] Test each stage before building on top of it.
- [ ] Use logs and command output when debugging.
- [ ] Run Ansible syntax checks and dry runs, then check idempotency before calling the automation finished.
- [ ] Save real results. Don't fill evidence files with made-up successful output.
- [ ] Update the documentation when we change the implementation.

### Assignment notes

- The server must run Ubuntu 22.04 Server. We can use a local VM or a VPS, with at least 2 GB RAM and 20 GB disk space.
- The assignment asks for a self-signed certificate. That's fine for this lab, but it is not the same as a publicly trusted production certificate.
- Database data must persist in a volume. We'll need to test that it survives container recreation.
- The file paths in this checklist follow the assignment's requested output structure. We can add supporting files when they make the project easier to understand or verify.
- Use `docker compose` if the installed Compose version supports it. If we need the older `docker-compose` command, note the version and use the same command consistently.
- Useful references: [Docker](https://docs.docker.com/), [Docker Compose](https://docs.docker.com/compose/), [Ansible](https://docs.ansible.com/), [Nginx](https://nginx.org/en/docs/), and [OpenSSL](https://www.openssl.org/docs/).
- The assignment specifically calls out Docker build failures, Ansible connection problems, Nginx `502 Bad Gateway` errors, and SSL certificate errors. Make sure our troubleshooting guide covers them.
