# UUG Web Apps - Front-End Demo
This repository captures the final result of our REST API code-along from last week.

## 1. Installing
To run this API locally, fork or clone the repo and inside your working directory run `npm install`.

Make sure you have [Node JS](https://nodejs.org/en/download/) installed already.

## 2. Running the Development Server
Once the project is installed, run `npm run serve` in your working directory.

This should start the web server at `http://localhost:8080`.

## 3. Building the project
If you want to do a local build run `npm run build` in your working directory.

This should generate a `dist/` directory with the output files inside.  We will deploy this `dist/` directory.

## 4. Deploying
This repository can be deployed quickly using the DigitalOcean App Platform.  Make sure to deploy the API before proceeding.

### 4.1 Manual Deployment
We will be deploying this second component manually.  You will need to [fork this repo](https://github.com/funkybunch/uug-demo-vue/fork) under your own account in order for DigitalOcean to recognize it.

Once you select the repository in the DO App Platform, set the Static Site settings to the following:
- Routes: `/`
- Environment Variables: `empty`
- Build Command: `npm run build`

Then give your static site a name.

Keep your current plan selected.  NOTE: you are not adding another container instance, static sites are free and this is just giving you the option to upgrade your container instance if you need to.  The Additional Monthly Cost at the bottom of the page should be $0.00.

### 4.2 Reference App Spec
You could use a similar automatic deployment function like with the API, but since we already created our app when deploying the API, we can simply add a static site component to our existing app.  This will be done manually, but here is the yaml that will be added to your app spec for reference.
```yaml
...
 static_sites:
 - build_command: |-
     npm run preinstall
     npm run build
   environment_slug: node-js
   github:
     branch: main
     deploy_on_push: true
     repo: funkybunch/uug-demo-vue
   name: uug-demo-front-end
   routes:
   - path: /
```
