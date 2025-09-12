# 🎯 Typeflows: Stop configuring GitHub. Start programming it.

**GitHub Actions is the [9th most disliked developer tool](https://newsletter.pragmaticengineer.com/p/the-pragmatic-engineer-2025-survey). We're fixing that (and a lot more!).**

Tired of debugging YAML in production? Write workflows as code:

```kotlin
class Deploy : WorkflowBuilder {
    override fun build() = Workflow("deploy-to-production") {
        displayName = "Deploy to Production"
        on += Push { branches = Branches.Only("main") }
        
        val buildJob = Job("build", UBUNTU_LATEST) {
            steps += checkout()
            steps += gradleSetup()
            steps += RunCommand("./gradlew build test")
        }
        
        jobs += buildJob
        jobs += Job("deploy", UBUNTU_LATEST) {
            needs += buildJob
            steps += deployToProduction()
        }
    }
}
```

✅ Full IDE support - catch errors before you push  
✅ Test locally - know which jobs run when  
✅ Visualise your workflows - see how things run and why 
✅ Share as packages - `com.company:standard-workflows`  

**But here's the thing...** Workflows are just the beginning.

## 📦 Your entire .github/ folder as code

Every repo starts with copy-pasting .github/ folders. Typeflows solves that too:

```kotlin
class DotGitHub : DotGitHubBuilder {
    override fun build() = DotGitHub {
        // Those type-safe workflows
        workflows += Deploy()
        workflows += ContinuousIntegration()
        
        // Security that scales
        files += dependabot(Dependabot {
            updates += Update(Maven) { schedule = Schedule(Weekly) }
        })
        
        // Team standards
        files += codeowners(TeamOwnership())
        files += securityPolicy(CompanySecurityPolicy())
        
        // And everything else in .github/
        files += copilotInstructions("kotlin.md", KotlinStyleGuide())
    }
}
```

One command generates everything. Version it. Test it. Share it as a library.

## Why Typeflows?

### 🔧 **Complete GitHub Configuration**
Not just workflows - manage dependabot, CODEOWNERS, security policies, issue templates, and every .github/ file as type-safe code.

### 🧪 **Test Before You Push**
Test workflow orchestration locally. Validate security policies. Ensure dependabot coverage. Know your configuration works before deployment.

### 📦 **Share as Packages**
Share proven GitHub setups across your organization. Version your standards. Update everywhere at once.
- JVM: `implementation("com.company:github-config:1.0")`
- JS/TS: `npm install @company/github-config` 
- Python: `pip install company-github-config`

### 🚀 **Zero Lock-in**
Generates standard GitHub configuration files. Import existing .github/ folders. Switch back anytime.

## 🛠️ See It In Action

Check out working examples: [github.com/typeflows/examples](https://github.com/typeflows/examples)

## Getting Started

**Free during beta.** 

**Available now:** JVM (Kotlin/Java) SDK  
**Coming Q3 2025:** TypeScript, Python  
**Future:** Go, Rust, .NET based on demand

🌐 [typeflows.io](https://typeflows.io) - Join the waitlist  
💬 [Discord](https://discord.gg/6XR2MSwVdK) - Chat with us  
🐦 [Twitter](https://twitter.com/typeflows) - Follow updates  

---

*Built by developers who copy-pasted one too many .github/ folders.*
