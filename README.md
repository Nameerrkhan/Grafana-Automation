Manual 1: Creating the CloudFormation stacks
Open AWS Academy Learner Lab and go to CloudFormation.
Delete any old failed lab-application stack first. Do not use Update; delete and recreate instead.
Click Create stack → With new resources (standard).
Upload lab-network.yml.
Set stack name as lab-network.
Click Next until the review page, then click Submit.
Wait until the stack status is CREATE_COMPLETE.
Create another stack the same way.
Upload lab-application.yml.
Set stack name as lab-application.
Click Next until the review page, then click Submit.
Wait until the stack status is CREATE_COMPLETE.
After both stacks complete, open CloudFormation > lab-application > Outputs and copy the EC2 public IP. The brief requires the two CloudFormation files and successful stack creation evidence.
Manual 2: Connecting to EC2 and checking the setup
Open EC2 in AWS Console.
Go to Instances and select the Grafana instance.
Click Connect.
Choose EC2 Instance Connect.
Use username ec2-user and click Connect.
In the terminal, run:
sudo -i
tail -100 /var/log/cloud-init-output.log
ls -l /tmp
cat /tmp/grafana.yml
cat /tmp/grafanainstall.sh
systemctl status docker --no-pager
docker --version
minikube status
minikube kubectl -- get nodes
minikube kubectl -- get pods -A
minikube kubectl -- get pvc
minikube kubectl -- get pods
minikube kubectl -- get svc

Expected results:
/tmp/grafana.yml exists
/tmp/grafanainstall.sh exists
Docker is active
Minikube is running
node is Ready
grafana-pvc is Bound
Grafana pod is Running
Grafana service exists

    7. If Grafana page is not already reachable, run:
nohup minikube kubectl -- port-forward --address 0.0.0.0 service/grafana 3000:3000 > /tmp/grafana-portforward.log 2>&1 &
sleep 5
curl -I http://localhost:3000/login

Open Grafana in browser:
http://EC2-PUBLIC-IP:3000

Ensure these are working:
lab-network = CREATE_COMPLETE
lab-application = CREATE_COMPLETE
grafana-pvc
Grafana page
/var/log/cloud-init-output.log
If you want to reset Minikube manually,:
minikube stop
minikube delete


