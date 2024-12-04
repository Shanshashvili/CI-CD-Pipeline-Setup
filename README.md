# CI/CD Pipeline Setup

## task:
- Write a simple CI/CD pipeline configuration (e.g., in GitLab CI/CD or GitHub Actions) that:
  1. Builds a basic Node.js application.
  2. Runs tests using npm test.
  3. Deploys the application to a staging server.
- Explain the YAML file structure and its components.

---
### **Explain YAML File Structure**

- `name:`  
  Defines the name of the workflow.  

- `on:` 
  Specifies the events that trigger the workflow:  
  - A push to the `main` branch.  
  note: I configured a trigger to automate the build, test, and deployment processes on specific events.

- `jobs:`  
  Defines the tasks to execute. Each job runs independently.  

#### **Build Job**
1. `runs-on:` 
   Specifies the environment to run the job (`ubuntu-latest`).  
2. `steps:` 
   Contains a sequence of actions:
   - **Checkout code:** Use the GitHub-provided `checkout` action to retrieve the code;  
   - **Set up Node.js:** Install the required Node.js version using the `setup-node` action;  
   - **Install dependencies:** Use `npm install` to fetch dependencies;  
   - **Run tests:** Execute tests using `npm test`;  
   - **Build application:** Build the app with `npm run build`.  

#### **Deploy Job**
1. `needs:`  
   Specifies a dependency on the `build` job. This ensures that deployment only happens if the build succeeds.  
2. `env:`  
   Defines environment variables like staging server details. These are stored securely in GitHub Secrets.  
3. `run:`  
   Executes deployment commands:
   - Uploads the `build` directory to the staging server using `scp`;  
   - Restarts the application service on the server using `ssh`.  



