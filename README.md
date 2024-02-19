# Argo CD For Kubernetes 

# Prerequisites :
    1. Docker
    2. Kubernetes
    3. Git
    4. Knowledge of Yaml files.
   
# Course Introduction :
    1. Intro to GitOps & diff GitOps tools.
    2. Importance of Argo CD & it's Architecture.
    3. Argo CD with Kubernetes.
    4. Deploy applications using Argo CD.
    5. Automate Infrastructure Deployment.   
   

# 01. What is GitOps ?
        GitOps uses git as a single source of truth to deliver the app & infra.
        Apply CI/CD Practice. 
        Git Repo. - Single source of truth.

# 02. Why GitOps ?
       Works as standered workflow for application development.
       Increses Security.Improver reliability with version control.
	  
# 03. GitOps Workflow :
       Developer will commit the source code in GitHub then DevOps engineer will configure the changes/Yaml files
       and according to that Argo CD will pull the files & apply it on Kubernetes

       Argo CD is working in between Source code repository and Kubernetes cluster. Developer can make the changes and commit 
       to the Source code repository like Git or a Git based Private repository such as Cloud Source Repository, Code commit.
       Argo CD pulls Kubernetes manifest changes and applies them to the cluster. If any changes are detected, then Argo CD 
       applies those changes automatically to the cluster.

# 04. GitOps Tools :
          1. Argo CD :
               It is an populer GitOps tool for Kubernetes. It is easy to setup & has GUI mode.
          2. Flux :
               Also an GitOps tool but here we have to configure dashboard manually.

# 05. Introduction & Why we need Argo CD :
       Argo CD is an continuous delivery tool for Kubernetes. 
       It is most populer GitOps tool with fully loaded user interface. (GUI)
       Also can be accesed using command line interface. (CLI)
       Works on Pull Model Design. (Pulls data from GitHub)
	 
# 06. Why we need Argo CD :
       1. It tracks the changes made in source files if there is any change it will auto sync the change.
       2. It checks the state visibility.
       3. Allows to make Rollback easily.
       4. It is highely secure.
	   	   
# 07. Argo CD Core Concepts :	   
       1. Project :
            It is an collection of applications.
       2. Application :
            It has source code in GitHub & after pulled by Argo CD it will deploy on Kubernetes cluster.
            Application Source Tool :
                1. Helm
                2. Yaml'

				
# 08. Desired & Actual State :
         Desired State :
           It is the state where the source code is present of GitHub.
      
	 Actual State :
           It is the stste where the source code is applied in Kubernetes cluster.
      
	 Sync :
           With help of Sync we can check that Actual & Desired states are matching or not, if not it will	
           auto sync the states.
      
	 Refresh/Compare :
           Compare the live state with Updated Git Code	  
	     Argo CD automatically refreshes in every 3 min to sync the data.
	 
	 
# 09. Argo CD Architecture :
        It has 3 main components :
          1. Argo CD server (API & Web Server) :
		The main component with which user can intract. It creates,updates,deletes the applications.
	        Performs application operations such as sync,rollback.
	        It can manager Repos & Cluster. Also used for Authentication
			 
          2. Argo CD Repo Server :
               It is an internal service that is responsible for cloaning remote git repos & generate the necessory 
               k8s manifests.
             
          3. Argo CD Application Controller		
               It is an k8s controller which continuously monitor the applications & compares the current/live state
               against the desired state.
	       Deploy apps manifests to destination cluster.
	       Detect's autosync apps and takes action if needed.
		
	  4. Redies :
              Redies used for caching.
			 
	  5. Application Set :
              It is used to deploy the application to other multiple clusters.

	  6. Dex :
              Identity Server.

	
# 10. Argo CD Benifits :
        Any changes updated in configuration files , Argo CD track the changes and realized that actual state does not equal 
	to desired state, and it will update the application Out of Sync. It automatically pull changes and will deploy to 
	Kubernetes cluster. It can track updates to branches, tags and versions.
        It provides application Health visibility, Real Time updates and last sync status as well as current status. 
	It Keeps cluster in Sync with Git Repo. Argo CD provides easy roll back to applications with previous state with 
	revert to back commit.

	
# 11. Argo CD GUI Installation as per (Just me and Opensource channel):
         1. kubectl create namespace argocd
         2. kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v2.10.0/manifests/install.yaml
	 3. kubectl get all -n argocd
	 4. In service file change clusterip to nodeport type named argo-cd server service.
	      1. You can edit the existing service file by - kubectl edit svc service_name
	      2. Also you can perform the following command through cli as
		    kubectl patch svc service_name -n argocd -p '{"spec":{"type":"LoadBalancer"}}'
         5. The ID & Pass will be - ID- admin & Pass will be the name of the pod 
	 6. Also you can generate the pass as -
	      kubectl -n argocd get secret argocd-initial-admin-secret -o jasonpath="{.data.password}" | base64 -d && echo
 
 
# 12. Installation of Argo CD CLI on Kubernetes Cluster :
        In above step we have installed Argo CD GUI in this step will install CLI :
	   1. curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
           2. sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
           3. rm argocd-linux-amd64
           4. Now see the Argo CD CLI version by using command.
                argocd version
           5. You can also see the client version of Argo CD CLI by using command.
                argocd version - -client

	  
# 13. Argo CD privileges :
        Argo CD privileges are of two types
          1. Cluster-admin Privileges – it is used when you are planning Argo CD to deploy applications in the same cluster in 
     	     which Argo CD is running ( Kubernetes.svc.default). Argo CD has cluster admin privileges.
          2. Namespace level Privileges – it is used when you are do not need Argo CD to deploy applications in the same cluster 
	     in which Argo CD is running.


# 14. Connect Argo CD with Source Code Repository and Deploy Application :
        (https://lex.infosysapps.com/web/en/viewer/pdf/lex_auth_013857562757169152881?collectionId=lex_auth_013848878844796928111&coll
	ectionType=Course&pathId=lex_auth_013851907660398592373)
	   
	   
# 15. Argo CD Source Tool :
       1. Helm :
	    It is an package manager for k8s. It deploys & manages the applications.
	    Argo CD provides built in support for helm charts.

       2. Kustomize :
           It is an configuration managment tool. Customize & manages the application.

       3. Jsonnet :
           It is an data templating lang. Easier to manage complex json structure.


# 16. Defining a k8s cluster on Argo CD :
         We can deploy app in two ways 
	    1. Local Cluster  : The cluster where k8s & argo-cd is deployed  
	    2. Remote Cluster : The k8s cluster is seperate than argo-cd cluster.
		 
		 
# 17. Maintaining High Avalability in Argo CD :
         1. Multiple replicas
	 2. Load balancing
	 3. Database Replication
	 4. Automatic back-up & restore.
	 
	 
# 18. Security Consideration in Argo CD :
     


# 19. Creating app in Argo CD using custom resource defination :
         1. In other way we created app using web UI.
	 2. So in this case will create app using CLI as follows :
	 3. Apply this file and see in web UI the app is created.

     apiVersion: argoproj.io/v1alpha1
     kind: Application
     metadata:
       name: guestbook    # Add your app name
       namespace: argocd  # Namespace where this app will be deployed
     spec:
       project: default   
       source:
         repoURL: https://github.com/argoproj/argocd-example-apps.git   # Your repo url where yaml files are present.
         targetRevision: HEAD
         path: guestbook           # In this repo in which folder all yaml files are present.
       destination:
         server: https://kubernetes.default.svc
         namespace: guestbook	   # Default
	  
    When creating an application from a Helm repository, the chart attribute must be specified instead of the path attribute within spec.source.

     spec:
       source:
         repoURL: https://argoproj.github.io/argo-helm
         chart: argo


# 20. Argo CD with Customize : (Just Me & Opensource)
        Customize is an object in k8s to customize the yaml files.
	  
      apiVersion: kustomize.config.k8s.io/v1beta1
      kind: Kustomization
      namePrefix: kustomize-
      resources:
        - nginx-deployment.yaml
        - nginx-svc.yaml
      
	  # The yaml files are already present in same directory where this customize yaml file is present. 



# 21. How to add external server to Argo CD ?

