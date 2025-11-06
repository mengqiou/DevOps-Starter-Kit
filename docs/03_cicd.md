# ⚙️ 07 — CI/CD (Continuous Integration & Continuous Delivery)

> **Goal:** Understand what CI/CD actually means, why it matters, and how tools like GitHub Actions, Jenkins, and GitLab CI fit together.

---

## 🧩 The Big Idea

Modern software projects don’t just “run once and done”.  
They evolve constantly — new code, bug fixes, testing, deployments.  
Without automation, it’s chaos.

That’s why we use **CI/CD**, which stands for:

- **Continuous Integration (CI)** — automatically build and test your code every time someone commits.
- **Continuous Delivery (CD)** — automatically package and deploy that tested code to servers or cloud environments.

Together, they create a **software assembly line**.

---

## 🏗️ Continuous Integration (CI)

**What happens during CI:**

1. You push code to GitHub (or GitLab, Bitbucket, etc.).
2. A CI service (like GitHub Actions, Jenkins, or CircleCI) detects the change.
3. It automatically runs:
   - Unit tests
   - Linting or code style checks
   - Build steps (compile, bundle, etc.)

If anything fails, the CI job reports back instantly — no more “works on my machine”.


# 🚀 Continuous Delivery (CD)

Once CI passes, CD automates **deployment**. It can:

1. Build Docker images.
2. Push them to registries (e.g. AWS ECR, Docker Hub).
3. Deploy to staging or production servers.
4. Run smoke tests to confirm the service is healthy.

Example (simplified):

```yaml
name: Deploy
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Deploy to AWS ECS
        run: aws ecs update-service --cluster my-cluster --service my-app --force-new-deployment
```

When you merge into `main`, GitHub Actions automatically deploys your app — no manual SSH or FTP needed.

---

# 🗂️ Where Workflows Live: `.github/workflows/`

GitHub Actions looks for YAML files inside `.github/workflows/`.
Each file defines one **workflow** — think of it as a mini automation script.

Examples:

* `.github/workflows/test.yml` → runs CI tests
* `.github/workflows/deploy.yml` → deploys your app
* `.github/workflows/docs.yml` → builds documentation

These files are version-controlled, so your automation setup is transparent and reproducible.

**Analogy:**
It’s like having a “smart home” folder inside your repo — each YAML file is a scheduled robot with specific chores.

---

# ⚡ Triggers: When Workflows Run

The `on:` key defines **what event starts your workflow**.
Here are the common types:

| Trigger                 | Meaning                             | Example                           |
| ----------------------- | ----------------------------------- | --------------------------------- |
| `on: push`              | Run every time someone pushes code  | Run tests automatically           |
| `on: pull_request`      | Run when a PR is opened or updated  | Verify code before merging        |
| `on: schedule`          | Run periodically (CRON syntax)      | Nightly builds or cleanups        |
| `on: workflow_dispatch` | Run manually from GitHub UI         | Trigger deployment manually       |
| `on: release`           | Run when a new release is published | Build & publish release artefacts |

Example:

```yaml
on:
  push:
    branches: [main]
  workflow_dispatch:
```

This workflow runs automatically on `push`, but you can *also* run it manually from the GitHub Actions tab.

---

# 🪽 Webhooks — The Event Bell

Behind the scenes, webhooks connect GitHub → CI/CD tools.
When you push new code, GitHub sends a **webhook** (a small HTTP POST message) to notify your automation server (e.g. Jenkins, GitHub Actions, CircleCI).
┌──────────────┐
│   Developer  │
└──────┬───────┘
       │ git push
       ▼
┌──────────────┐
│   Webhook    │  ← GitHub notifies CI system
└──────┬───────┘
       ▼
┌──────────────┐
│ Build & Test │  ← Continuous Integration
└──────┬───────┘
       ▼
┌──────────────┐
│ Deploy & Run │  ← Continuous Delivery
└──────────────┘


**Analogy:**
A webhook is like a doorbell.
When GitHub rings it, your CI/CD system wakes up and starts the workflow.

Without webhooks, you’d have to constantly poll for changes (“did someone push?”).

---

# ☁️ Real-World Integrations — AWS Commands

Larger organisations often define **command-style workflows** so DevOps teams can trigger infrastructure actions directly from GitHub.

Example:
A company might have these reusable workflows in `.github/workflows/`:

* `ecs-stop-container.yml` — stop a specific ECS container.
* `invoke-lambda.yml` — call an AWS Lambda function.
* `rotate-keys.yml` — rotate credentials via AWS CLI.

Such workflows usually rely on:

```yaml
- name: Configure AWS credentials
  uses: aws-actions/configure-aws-credentials@v4
  with:
    aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
    aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
    aws-region: ap-southeast-2
```

Once credentials are loaded, you can run **any AWS CLI command**, such as:

```yaml
- name: Stop ECS Service
  run: aws ecs update-service --cluster myCluster --service api --desired-count 0
```

This allows secure, auditable infrastructure operations — directly from version-controlled workflows.
