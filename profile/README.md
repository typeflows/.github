# 🚀 Typeflows: **Stop configuring CI/CD. Start programming it.**

**GitHub Actions is the [9th most disliked developer tool](https://newsletter.pragmaticengineer.com/p/the-pragmatic-engineer-2025-survey). We're fixing that.**

Write workflows as code. Test them locally. Ship with confidence.

## Why Typeflows?

**Stop debugging YAML in production.** Write type-safe workflows in Kotlin, Java, TypeScript, Python, or your favorite language. Your IDE catches errors before you push.

**Test workflow orchestration locally.** Know which jobs run when. Validate trigger conditions. Test job dependencies. No more push-and-pray.

**Share workflows as packages.** Import proven patterns. Version your CI/CD. Build a library of tested deployment strategies.

## See It In Action

```kotlin
class Deploy : WorkflowBuilder {
    override fun toWorkflow() = Workflow("Deploy to Production") {
        on += Push {
            branches = Branches.Only("main")
            paths = Paths.Only("src/**")
        }

        val buildJob = Job("build", UBUNTU_LATEST) {
            steps += checkout()
            steps += UseAction("actions/setup-node@v4") {
                with["node-version"] = "20"
            }
            steps += RunCommand("npm run build && npm test")
        }

        jobs += buildJob

        jobs += Job("deploy", UBUNTU_LATEST) {
            needs += buildJob
            steps += UseAction("actions/deploy@v2") {
                with["target"] = "production"
                with["token"] = "${{ secrets.DEPLOY_TOKEN }}"
            }
        }
    }
}
```

Generates standard GitHub Actions YAML. Import existing workflows. **Zero lock-in.**

## Get Started

**Free during beta.** SDK coming Q3 2025.

🌐 [typeflows.io](https://typeflows.io) - Join the waitlist  
💬 [Discord](https://discord.gg/6XR2MSwVdK) - Chat with us  
🐦 [Twitter](https://twitter.com/typeflows) - Follow updates  

---

*Built by developers who've debugged one too many YAML files at 3am.*
