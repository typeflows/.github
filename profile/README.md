# 🎯 Typeflows: Configuration-as-Code for GitHub

**GitHub Actions is the [9th most disliked developer tool](https://newsletter.pragmaticengineer.com/p/the-pragmatic-engineer-2025-survey). We're making it less frustrating.**

Typeflows brings Configuration-as-Code to repository management. Write your workflows and entire .github/ folder as type-safe, testable code:

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
✅ Test locally - validate which jobs run when  
✅ Auto-generated visualisations - understand complex workflows  
✅ Share as versioned packages - `com.company:standard-workflows`  

## 📦 Beyond workflows: Your entire .github/ folder as code

Every repository starts by copying another's .github/ folder. They immediately diverge. Typeflows solves configuration drift through package management:

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
        
        // AI assistant instructions in .github/
        files += file(".github/copilot-instructions.md", KotlinStyleGuide())
    }
}
```

One command generates everything. Version it. Test it. Share it across your organisation.

## Why Configuration-as-Code?

### 🔧 **Complete Repository Management**
Not just workflows - manage Dependabot, CODEOWNERS, security policies, issue templates, and every .github/ file as type-safe code.

### 🧪 **Test Before Deployment**
Test workflow orchestration locally. Validate security policies. Ensure Dependabot coverage. Know your configuration works before it reaches production.

### 📦 **Package Management for Configuration**
Share proven GitHub setups across your organisation. Version your standards. Update everywhere through dependency management.
- JVM: `implementation("com.company:github-config:1.0")`
- JS/TS: `npm install @company/github-config` 
- Python: `pip install company-github-config`

### 🚀 **No Lock-in**
Generates standard GitHub configuration files. Import existing .github/ folders. All your configurations export to standard files that work with or without Typeflows.

## 🛠️ See It In Action

Find out more at [typeflows.io](https://typeflows.io), or check out working examples: [github.com/typeflows/examples](https://github.com/typeflows/typeflows)

## Getting Started

**Free during Early Access and Beta.**

**Available now:** JVM (Kotlin/Java) libraries  
**Coming soon:** TypeScript, Python  
**Planned:** Go, Rust, .NET based on demand

🌐 [typeflows.io](https://typeflows.io) - Documentation and early access  
💬 [Discord](https://discord.gg/6XR2MSwVdK) - Community support  
🐦 [Twitter](https://twitter.com/typeflows) - Updates  

---

*Configuration-as-Code for teams who've copy-pasted one too many .github/ folders.*
