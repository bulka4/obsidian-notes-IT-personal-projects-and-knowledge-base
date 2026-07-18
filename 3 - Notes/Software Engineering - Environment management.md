Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Environment management in E2E testing is about creating and controlling the environments (dev, test, stage and prod) where full user workflow tests run.

Because E2E tests involve the whole system, they need many components:
```
id="0l4h2m"
E2E Test Environment

Browser
   |
Frontend
   |
Backend API
   |
Database
   |
Message broker
   |
External services
```
Managing this environment means ensuring all these parts are available, configured correctly, and consistent.
# Main aspects of environment management
1. Environment provisioning - Creating the environment required for tests, for example:
	- start application servers
	- create databases
	- deploy containers
	- configure networks
2. Configuration management - Providing correct settings for the test environment
3. Test data management - Preparing data needed for workflows
4. Environment isolation - Preventing tests from affecting each other
5. Environment lifecycle - Managing the environment during the test process: create environment, run tests, destroy environment