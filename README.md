# DevOps Checklist

This is an effort to begin codifying an authoritative technical 'Pilots Checklist' for DevSecFinOps practices.

In the age of AI, and so much OpenSource, we tried to 'Google' and 'ChatGPT' a helpful list, but failed. This, then, aims to be an amalgum of a variety of sources, including https://devopschecklist.com/, https://devops.com, linearloop.com, Google's DORA metrics, https://atlassian.com, and more.

We would appreciate and encourage contributions from the community!


## Technical 
- [ ] All environments are built for zero-downtime from day-one
- [ ] Minimal variance between environments
- [ ] Implementation of abstraction technologies to accelerate new environment creation, increate development velocity, and reduce documentation needs
- [ ] All infrastructure is contractual, repeatable and reliable (Infrastructure as Code (IaC), eg: Terraform / CloudFormation).  **Nothing** is setup manually.
- [ ] New employee spin-up time is minimal due to…
    - [ ] Codebases all have coding standards defined and linting automatically
    - [ ] Codebases all have documentation both in a README and inline code
    - [ ] Getting access to various systems, codebases, portals, etc to do their job is not a complex task.  Ideally all delegated and granted access through SSO / OAuth.
    - [ ] Diagramming / Flowcharting / ERD / Wireframes
    - [ ] In-Cluster Development
    - [ ] Developer Velocity Tools (BackStage, or similar)
- [ ] New service creation is simple due to…
    - [ ] Defined company-wide standards for code (language-specific)
        - [ ] I.e. GitRepo templates per language, along with all relevant best practices
    - [ ] Defined company-wide standards for automation (language-specific)
        - [ ] I.e. Reusable helm charts; modular, opinionated IaC; GitOps-driven workflows everywhere
    - [ ] Defined company-wide standards for service deployment
        - [ ] I.e. Full CI/CD automation, with well-disseminated education re usage and user contribution
    - [ ] Developer Self-Service Framework/Platform
    - [ ] Standards are packaged, SCM-managed, and made available for consumption downstream
- [ ] Services are built for reliability, maintainability and scalability from day-one
    - [ ] All software is built for high-availability (multiple concurrent servers/containers with autoscaling, fault-tolerance, failover, etc)
    - [ ] Requests which need processing time can and should be delegated to a background worker and/or task engine technology
    - [ ] Code is maintainable (see below)
    - [ ] Code is modular (see below)
    - [ ] Code is secure (security scanning used across CI pipeline)
    - [ ] Code is Cloud Agnostic (where possible)
    - [ ] Has testing built-into the codebase which is used automatically by CI and is required to run before merges are accepted
    - [ ] Deploys automatically from CI with definition files stored in the codebase
    - [ ] Deployments are configurable per service, environment, deployment, developer
    - [ ] Deployments are aggressively optimised for performance and cost
    - [ ] Above is done in a way which is digestible and accessible for ALL engineers
- [ ] Code is maintainable
    - [ ] Using language formatting/styling best-practices and standards (per-language)
    - [ ] Has documentation on how to quickly get familiar with the codebase and get a development environment working
    - [ ] Have a company emphasis on knowledge sharing / team pairing / etc
    - [ ] Has automated testing of some kind (unit, end to end, acceptance, etc)
    - [ ] Uses continuous integration to automatically verify code is within standards and passes all tests before allowing merges and/or deploys
    - [ ] All code is DRY (Don’t Repeat Yourself).  Library code is in a shared codebase / module if needed for re-use across multiple projects.
    - [ ] gitOps-driven Single Source Of Truth for IaC, Code, Configs, Documentation, Websites, etc
    - [ ] KISS.  Keep it simple, stupid.  Don’t over or re-engineer something if there’s an existing project, module, library out there to do 99% of what you need.  Use existing technologies, modules, libraries and standards as often as possible, minimize your work to only domain-specific nuances as much as possible.
- [ ] Code Modularity
    - [ ] Pieces of the codebase are engineered with modularity in mind from day-one
    - [ ] Libraries should be able to be re-used in other projects as a simple drop-in
- [ ] Documentation & Diagramming should be available…
    - [ ] For infrastructure
    - [ ] For codebases
    - [ ] For services and service (inter)dependencies
    - [ ] Flowcharts
    - [ ] For deployment and rollback workflow
    - [ ] For edge cases
    - [ ] For Disaster Recovery
    - [ ] ... and should, ideally, be auto-generated.
- [ ] Infrastructure deployments and modifications are fully automated/scripted
    - [ ] Not a single thing on any cloud service you use should be manually configured, ideally even remove permissions from anyone to even have write access to your cloud service (except for key individuals for emergencies).  There are rare exceptions to this however.
    - [ ] Do not run kubectl apply / terraform apply on your own terminal to apply changes to any environment (except briefly during testing/development)
    - [ ] Code deployments are automated, optionally with a manual circuit breaker for live
    - [ ] Codebases are split into separate repositories per service, microservice, purpose
- [ ] Leveraging git using defined best practices
    - [ ] Define and use a branching and release (versioning/tagging) model company-wide
    - [ ] See: https://semver.org
    - [ ] See: https://datasift.github.io/gitflow/IntroducingGitFlow.html
    - [ ] Always use merge/pull requests
    - [ ] Require maintainer / owner / peer(s) to approve before being allowed to merge
    - [ ] Make squashing code from Merge Requests mandatory to keep a clean git history in your master branch and remove “merge commits”.
- [ ] Service deployments are using zero-downtime mechanism such as Blue/Green or Canary
- [ ] Using the best tool for the job, for each individual concern is often better than trying to use one tool for every job
- [ ] Having NO (or minimal) tools with overlapping responsibilities. (Eg: Not having more than one CI system, more than one SCM, more than one Cloud Provider (unless HA dictates it), not more than one automation tool, testing tool, deployment tool, monitoring tool, etc).
- [ ] Every aspect of an environment has resiliency, redundancy, health checks, monitoring, alerting, cost-optimisation, auto-healing capabilities and backups from day one.
- [ ] Observability Tools are easy to use, enriched with relevant data, and expose feature-rich APIs
- [ ] Deploys are painless, single-click or fully automated, no humans are involved and no human error is possible.  Removing access from humans to even be able to deploy (besides clicking the deploy button)
- [ ] Rollbacks are painless, single-click or fully automated.  Is well-documented if necessary and recommend testing/validating these function before going live with any new service.
- [ ] IAM
    - [ ] Quarterly Audit
    - [ ] Use of MFA mandatory for all humans
    - [ ] static credentials eradicated from lifecycles
    - [ ] ZeroTrust implemented globally
    - [ ] Automated Audit Scanning for outliers
    - [ ] LeastPrivilege per user, service, pod
- [ ] DR systems
    - [ ] meets company requirements re key metrics inc. RTO, RPO, etc
    - [ ] tested quarterly
    - [ ] Optimised for cost and performance objectives
- [ ] Cost Optimisation/FinOps
    - [ ] implemeted across all systems
    - [ ] rightsizing evaluated quarterly
    - [ ] tagging and cost allocation strategy enforced programatically
    - [ ] relevant discounts requested and applied
- [ ] Robust tests for any/all aspects of code (IaC / backend / API / frontend)
- [ ] Automated performance (load/soak) testing in place, run regularly, preferably automatically on every major release candidate or merge request to compare to baseline
- [ ] Multi-faceted monitoring solution in place, monitoring typically USE/RED metrics and/or traditional server metrics where relevant.
    - [ ] Monitoring solution should be redundant, and should monitor application-stacks from both within and outside environments
    - [ ] Alerting should be rational, minimise flapping and false-positives/negatives, and be auto-directed to on-call engineer
    - [ ] Support staff sufficiently knowledgeable and contextually aware to solve issues
    - [ ] Clear escalation paths documented, with automated switch-over between on-call engineers
- [ ] Custom application monitoring & metrics in place to detect sub-service failures / outages
- [ ] All applications should be (as) self-contained as possible without being dependent on other applications to minimize complexity and potential downtime.
    - [ ] Where dependencies occur especially external ones (SaaS cloud services) ensure your service can tolerate limited or no availability of such service.  This typically requires testing.
- [ ] Having circuit breakers / feature flags in place to detect and act/react accordingly if certain features or dependent services are down.  Allowing your application to fail gracefully and/or certain features to be temporarily unavailable while a fix is underway
- [ ] All environments/services are built securely (IAM, Service Accounts, Roles, Security Groups, etc)
    - [ ] All services have HTTPS/SSL/TLS, with no exception
    - [ ] Encryption is implemented for all Data-at-Rest
    - [ ] All endpoints and nodes are firewalled as much as possible
    - [ ] Services / Servers / Etc is designed with least-privilege in mind
    - [ ] Based on current provider, using their best-practice technologies/methodologies
    - [ ] Everything leaves an audit trail (Services / Services / Users) which is not editable by anyone (eg: push all logs to external aws account s3 bucket, no one with delete access only write, and no overwrite allowed)
- [ ] All services logging to a centralized logging platform, with read-only access given to engineers necessary to perform debugging/maintenance/etc
- [ ] Secret-free codebase
- [ ] Codebase contains sane default (but overrideable) values
- [ ] Remove secrets & private data from logs / regularly audit the presence of these
- [ ] Using a standardized log format (EG: json) for parsability in a centralized logging platform
- [ ] Environments and services are architected based on gathered use-cases/requirements and team skill-sets not a line drawn in the sand or a hard requirement
- [ ] Environments are as simple as they can be, using the least amount of technologies possible while still accomplishing the goal (KISS).  Also consider the value of having consistency of dependencies across multiple services, this gives your company and team more collective experience and knowledge in one technology and will usually result in higher velocity and reliability.
    - [ ] Eg: If you’re using MySQL in many places, unless your company goal is to change this underlying technology then keep using it on new services.  Don’t suddenly go add PostgreSQL, and then also don’t go add Oracle as well.
    - [ ] Clear path to sunsetting use of redundant technologies
- [ ] Secrets are managed centrally and via some automation (Eg: Vault / AWS KMS)
- [ ] Shift-Left mentality should be implemented across SSDLC lifecycle and DevSecFinOps processes
- [ ] All developers can access all systems even on production to monitor, maintain and debug.  If desired, using role/group based access limits their access to only specific components/areas.
    - [ ] Ideally, the use of a Developer Velocity Platform which exposes service telemetry, logs, and other useful data for troubleshooting
- [ ] For releasing software focus on small deploys (merge requests) and avoid big-bangs, break up big-bangs into smaller increments when possible
    - [ ] Aim for numerous deploys weekly.  A deploy once every two weeks (length of a typical “sprint” in agile) can have so many changes at the same time that it can be hard to single out which of those caused an issue.
- [ ] Avoid TRACE/DEBUG logging on Production environments to prevent wasted space in logging systems, ideally disable on dev as well but make it easy to enable if needed (feature-flag)
- [ ] DevOps team should continously review systems and processes against DORA KPIs, taking action to close gaps and address inefficiencies when appropriate
- [ ] Remote Deployment Support
    - Technologies in use
    - Automated Upgrade/Downgrade/Provision/Deprovision
    - Monitoring/Proactive Support mechanisms
- [ ] Education
    - [ ] DevOps tools and processes should be diseminated across R&D teams on an ongoing basis
    - [ ] Recordings of all sessions should be uploaded, and made available to all interested parties
    - [ ] Recordings should be reviewed quarterly for relevance, and updated when necessary
    - [ ] AI tools should be introduced, where appropriate, to improve experience, and make content more easily searchable




This checklist was originally inspired by: https://github.com/DevOps-Nirvana/DevOps-Checklist
