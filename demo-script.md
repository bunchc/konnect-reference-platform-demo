# Kong Konnect Reference Platform: Technical Demo Script

**Objective:** Showcase how the Kong Konnect Reference Platform enables multiple teams to manage their own services through a centralized, automated, and self-service platform.

**Duration:** 15-30 minutes

**Personas:**
*   **Platform Engineer:** Responsible for setting up and maintaining the Konnect Reference Platform.
*   **Team A Developer:** A developer on Team A, responsible for the "Product" service.
*   **Team B Developer:** A developer on Team B, responsible for the "Inventory" service.

---

## Part 1: Platform Setup (Platform Engineer)

**(Scene: The Platform Engineer is in their terminal and has the prerequisites installed.)**

**Persona:** Platform Engineer

**Talking Points:**
"Hello everyone. Today, I'm going to walk you through the Kong Konnect Reference Platform. Our goal is to create a centralized API platform that empowers our development teams to manage their own services in a self-service manner, while we, the platform team, maintain governance and control."

"First, I'll act as the Platform Engineer to set up the initial infrastructure. This is a one-time setup."

### Step 1: Initialize the Platform Repository

**Talking Points:**
"The heart of our reference platform is a single Git repository, which we call the 'platform' repository. This repository will store our APIOps workflows, service configurations, and API specifications. I'll use the `koctl` command-line tool, our Konnect Orchestrator, to initialize this repository."

**(Action: Run the `koctl init` command and fill in the prompts.)**

```bash
koctl init
```

**Talking Points:**
"As you can see, `koctl` has created a pull request in our platform repository. This PR contains all the necessary GitHub Actions workflows and configurations to get us started. I'll go ahead and merge this."

**(Action: Show the PR in GitHub and merge it.)**

### Step 2: Add a Konnect Organization

**Talking Points:**
"Now that our platform repository is initialized, I need to connect it to our Kong Konnect organization. This will allow the platform to manage our API gateway configuration, developer portal, and other Konnect resources."

**(Action: Run the `koctl add organization` command and fill in the prompts.)**

```bash
koctl add organization
```

**Talking Points:**
"Similar to the init step, this command creates another pull request. This PR adds the necessary configuration to link our platform repository with our Konnect organization. I'll merge this as well."

**(Action: Show the PR in GitHub and merge it.)**

### Step 3: Run the Self-Service UI

**Talking Points:**
"One of the key features of the reference platform is the self-service UI. This is a web application that our development teams will use to onboard their services. I'll start it locally using `koctl`."

**(Action: Run the `koctl run` command and fill in the prompts.)**

```bash
koctl run
```

**Talking Points:**
"The self-service UI is now running locally. This UI allows developers to log in with their GitHub accounts and add their services to the platform. Now, let's switch hats and see this from a developer's perspective."

---

## Part 2: Team Onboarding (Team A & Team B)

**(Scene: The developers from Team A and Team B will use the self-service UI to onboard their services.)**

### Team A: Onboarding the "Product" Service

**Persona:** Team A Developer

**Talking Points:**
"Hi, I'm a developer on Team A. We have a new 'Product' service that we need to expose through the API gateway. I've been told I can use the new self-service portal to do this."

**(Action: Open a browser to `http://localhost:8080`, log in with GitHub, and select the 'Product' service repository.)**

**Talking Points:**
"I'll log in with my GitHub account, select my team's organization, and choose our 'Product' service repository. I'll also select our production and development branches. I can either select an existing team or create a new one. I'll add this service to 'Team A'."

**(Action: Click "Add Service to Platform".)**

**Talking Points:**
"And that's it! The portal tells me a pull request has been created in the platform repository. Now, it's up to the platform team to review and approve it."

### Team B: Onboarding the "Inventory" Service

**Persona:** Team B Developer

**Talking Points:**
"Now, I'm a developer from Team B. We also have a service, the 'Inventory' service, that needs to be added to the platform. I'll follow the same process as Team A."

**(Action: In the self-service UI, select the 'Inventory' service repository and add it to "Team B".)**

**Talking Points:**
"I've added our 'Inventory' service. Just like Team A, a pull request has been created for the platform team to review."

---

## Part 3: APIOps in Action (Platform Engineer)

**(Scene: The Platform Engineer is back in GitHub, looking at the pull requests created by the developers.)**

**Persona:** Platform Engineer

**Talking Points:**
"Welcome back. As the platform engineer, I can see two new pull requests in our platform repository, one for the 'Product' service from Team A and one for the 'Inventory' service from Team B."

**(Action: Open one of the PRs, for example, the one for the 'Product' service.)**

**Talking Points:**
"Let's look at the PR for the 'Product' service. It adds a simple configuration file that tells our platform about the new service. This looks good, so I'll merge it."

**(Action: Merge the pull request for the 'Product' service. Then, merge the PR for the 'Inventory' service.)**

**Talking Points:**
"I've now merged both pull requests. Merging these PRs triggers our APIOps workflow. This workflow automatically copies the OpenAPI specification from the service repository into our platform repository and creates new pull requests with the declarative configuration for our gateway."

**(Action: Go to the "Actions" tab in the platform repository to show the workflow running. Then, go to the "Pull requests" tab to show the new PRs created by the orchestrator.)**

**Talking Points:**
"Here are the new PRs created by our APIOps workflow. There's one for each environment, dev and prod, for each service. These PRs contain the generated Kong gateway configuration based on the OpenAPI specs from the teams' repositories. This is where we can enforce policies, add plugins, and ensure governance."

"For this demo, we'll just approve them. Merging these PRs will trigger the final step of our APIOps workflow, which applies the configuration to our Konnect control plane."

**(Action: Merge one of the generated PRs, for example, `dev` for the 'Product' service.)**

---

## Part 4: Verification and Conclusion (All Personas)

**(Scene: The Platform Engineer is in the Kong Konnect UI.)**

**Persona:** Platform Engineer

**Talking Points:**
"Now that the APIOps workflow has completed, let's look at our Kong Konnect organization. We can see that the 'Product' service has been added, with a route, and is now exposed through our gateway. If we had merged the other PRs, we would see the 'Inventory' service here as well."

**(Action: Show the Service Hub in Kong Konnect, and navigate to the newly created service and its routes.)**

**Talking Points:**
"So, what did we see today?
*   **For Platform Engineers:** We have a fully automated, GitOps-driven workflow for managing our API platform. We can enforce governance and maintain control, all from a central platform repository.
*   **For Developers:** We have a simple, self-service way to onboard and manage our services. We can focus on building our applications, and the platform takes care of the rest.

This reference platform allows us to scale our API program, improve developer productivity, and ensure consistency and governance across all our services. Thank you."
