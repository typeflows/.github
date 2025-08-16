# 🚀 **Stop configuring CI/CD. Start programming it.**

[GitHub Actions is the 9th most disliked developer tool](https://newsletter.pragmaticengineer.com/p/the-pragmatic-engineer-2025-survey). We know why - you're debugging YAML in production instead of shipping features. 😤

Typeflows brings **Workflows-as-Code** to GitHub Actions. Write type-safe workflows in TypeScript, Python, Java, Kotlin + others. Test them locally. Share them as packages. 

## 🔥 The Problem

- **One typo breaks everything** ❌ - and you only find out after pushing
- **Copy-paste hell** 📋 - the same workflow across 50 repos, updated manually
- **No way to test** 🎰 - push and pray is not a strategy
- **Hidden limits** 🚧 - "workflow nesting too deep" errors appear from nowhere

## ✨ The Solution

Write workflows as real code:

```typescript
class Deploy implements WorkflowBuilder {
    toWorkflow(): Workflow {
        return Workflow("Deploy to Production")
        {
            on += Push
            {
                branches = Branches.only("main")
                paths = Paths.only("src/**")
            }

            const buildJob = Job("build", UBUNTU_LATEST)
            {
                steps += checkout()

                steps += useAction("actions/setup-node@v4")
                {
                    with["node-version"] = "20"
                }

                steps += runCommand("npm run build && npm test")
            }

            jobs += buildJob

            jobs += Job("deploy", UBUNTU_LATEST)
            {
                needs += buildJob

                steps += useAction("actions/deploy@v2")
                {
                    with["target"] = "production"
                        with["token"] = "${{ secrets.DEPLOY_TOKEN }}"
                }
            }
        }
    }
}
```

Then generate standard GitHub Actions YAML. Or import your existing YAML and convert to code. Zero lock-in.

## 🎯 What This Enables

- 🧪 **Test workflow orchestration locally** - know which jobs run when
- 📦 **Publish workflow libraries** - `@company/k8s-deploy v2.1.0`
- 🔧 **Refactor safely** - your IDE handles the heavy lifting
- 🏪 **Build workflow marketplaces** - share battle-tested patterns across your entire org

## 🌟 Get Early Access

We're building the future of CI/CD. Join us.

🚀 [typeflows.io](https://typeflows.io) | 💬 [Discord](https://discord.gg/6XR2MSwVdK) | 🐦 [Twitter](https://twitter.com/typeflows)

---

Made with ❤️ by developers who've had enough of YAML debugging.
