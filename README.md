Commit and push code to GitHub.

Jenkins will automatically detect changes and trigger the pipeline.

Steps will be:
✅ Checkout code
✅ Build Docker image
✅ Run tests
✅ Push image to DockerHub
✅ Deploy app locally (or on server)

You can then access your app at:
👉 http://localhost:5000 → should show “Hello, Jenkins CI/CD World!”

Steps:
1 Install git -- sudo yum install -y
2 install docker -- sudo install docker -y
   systemctl restrat docker
   systemctl enable docker
   systemctl status docker
3 Add jenkins to docker group:
  sudo usermod -aG docker jenkins

4- Restart Jenkins:
   sudo systemctl restart jenkins

5- Log out & log back in (or restart server) so group change takes effect.
6. sudo su - jenkins
   docker ps
7 Add docker credential in jenkis

  username : <dockerhub_username>
  password: <dockerhub_password>
  id: docker_cred
  save
8-Install stage viwe plugin
  jenkins manage --> plugins --> Pipeline stage view
9- Create job with pipeline with poll SCM and source SCM and give gir URL
