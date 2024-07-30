# Packaging-templates-using-helm

## Step-by-Step Guide to Package Helm Charts and Set Them Up on GitHub
# Step 1: Create a GitHub Public Repository and Clone It Locally
    
# Create a GitHub repository:

    Go to GitHub and create a new repository. Make sure to keep it public if you want the Helm repository to be accessible publicly.
    Clone the repository locally:


    git clone <repo-http-url>
    cd <cloned-folder-name>  # Switch to the cloned folder
    git checkout -b gh-pages  # Create a new branch named gh-pages

# Step 2: Create and Push an Empty index.yaml File
# Create an empty index.yaml file and push it to the repo:


    touch index.yaml
    git add index.yaml
    git commit -m "Add index.yaml"
    git push --set-upstream origin gh-pages

## Configure GitHub Pages:

    Go to your repository on GitHub.
    Navigate to Settings > Pages.
    Select the source branch as gh-pages and the directory as /root.
    Note the URL provided for the live GitHub Pages site. (e.g., https://aretec-inc.github.io/disearch-helm/).

## Step 3: Move Helm Charts to the Current Folder
    Move your Helm charts to the cloned GitHub repository folder:
    In your case, you would move redis, etcd, and gke-templates charts to this folder.

## Step 4: Create Packages Using Helm Command
    Package your Helm charts:

    helm package etcd
    helm package redis
    helm package gke-templates  # etcd, redis, gke-templates are the chart names

## Step 5: Organize Your Packages
    Create a folder named helm-templates and move your .tgz files:

    mkdir helm-templates
    mv *.tgz helm-templates/

## Step 6: Create an Index File
    Generate the index.yaml file:


    helm repo index helm-templates/ --url https://aretec-inc.github.io/disearch-helm/
    Verify the index.yaml file is live:


    curl https://aretec-inc.github.io/disearch-helm/index.yaml

## Step 7: Push Your Packages and Updated index.yaml File to GitHub
    
    Push your .tgz files and the updated index.yaml file:

    git add helm-templates/*.tgz index.yaml
    git commit -m "Add Helm chart packages and updated index.yaml"
    git push origin gh-pages
    Step 8: Add and Use the Helm Repository
    Add the Helm repository:

    helm repo add disearch-repo https://aretec-inc.github.io/disearch-helm/
    List the Helm repositories:

    
    helm repo list
    Show values of a specific chart:

    
    helm show values disearch-repo/redis
    Install a chart from the repository:

    
    helm install redis disearch-repo/redis
    Following these steps will set up your Helm charts in a GitHub repository, making them available for use via Helm commands.









