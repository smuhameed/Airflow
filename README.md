# Airflow
Steps to update Airflow Postgres Database to another Postgres Database. 
Pre-requisite: 
* Login to Azure using Service principle 
* Know how to access kubelogin and kubectl commands 

Step 1: Get the current db details from repository or from airflow cli.
  - Login to Airflow-scheduler pod (in my case, we have used helm chart)
      kubectl exec -it <scheduler-pod-name> -- /bin/bash
  - After login to the pod, execute below commands using Airflow cli.
       airflow db check
       Output:
       [xxxxxxxxx] {xxxxxx} INFO - Connection successful. 
       airflow config get-value databse sql_alchemy_conn
       Output:
       postgresql://<username>:<password>@<DB_NAME>:5432/airflow?sslmode=require
Step 2: Execute below kubectl commands
  - kubectl get deployment
  - kubectl get deployment <xxx-scheduler> -o yaml > airflow-scheduler.yaml
  - Open "airflow-scheduler.yaml" file and look for env: and get the secret key refernce.
  - kubectl get secrets 

    
