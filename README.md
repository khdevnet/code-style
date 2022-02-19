# Code Style and Formatting Tools
* [ReSharper](https://www.jetbrains.com/resharper)
* [Code style rule options](https://docs.microsoft.com/en-us/dotnet/fundamentals/code-analysis/code-style-rule-options)
* [Code style .editorconfig](/.attachments/editorconfig-0abef250-6c35-4b89-9401-afec0644f6db.txt)


## Configure
* Install nuget packages
  * [StyleCop.Analyzers](https://www.nuget.org/packages/StyleCop.Analyzers) to all projects
  * [Threading.Analyzers](https://www.nuget.org/packages/Microsoft.VisualStudio.Threading.Analyzers)
* Copy .editorconfig to folder from what do you want to apply rules
* Copy .ruleset and Directory.Build.props to folder

* **Phase 2** [SonarScanner Azure DevOps](https://docs.sonarqube.org/latest/analysis/azuredevops-integration/)

# Basic Principles
* The Principle of Least Surprise (or Astonishment), which means that you should choose a solution that does include any things people might not understand, or put on the wrong track.
* Keep It Simple Stupid (a.k.a. KISS), a funny way of saying that the simplest solution is more than sufficient.
* You Ain’t Gonne Need It (a.k.a. YAGNI), which tells you to create a solution for the current problem rather than the ones you think will happen later on (since when can you predict the future?)
* Don’t Repeat Yourself (a.k.a. DRY), which encourages you to prevent duplication in your code base without forgetting the Rule of Three heuristic.
# SOLID Principles
* [Single-responsiblity Principle](https://www.digitalocean.com/community/conceptual_articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design#single-responsibility-principle)
* [Open-closed Principle](https://www.digitalocean.com/community/conceptual_articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design#open-closed-principle)
* [Liskov Substitution Principle](https://www.digitalocean.com/community/conceptual_articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design#liskov-substitution-principle)
* [Interface Segregation Principle](https://www.digitalocean.com/community/conceptual_articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design#interface-segregation-principle)
* [Dependency Inversion Principle](https://www.digitalocean.com/community/conceptual_articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design#dependency-inversion-principle)

# Naming conventions
* The code should reads like paragraphs and sentences, or at least like tables and data structure (a sentence isn’t always the best way to display data)
* Choose descriptive and unambiguous names.
* Pick one word for an abstract concept and stick with it
* Don’t Pun. Converse to using one word per abstract concept, do not use the same word for two purposes
* Use Solution Domain Names
* Use Problem Domain Names. Problem domains refers to all the information that defines the problem (i.e. the problem you are solving with code).
* Class names should have a noun or noun phrase. Class names should not be verbs.
* Methods should have verb or verb phrases.

# Maintainability guidelines
* [Be reluctant with multiple `return` statements ](https://csharpcodingguidelines.com/maintainability-guidelines/#AV1540)
* [Inappropriate intimacy](https://refactoring.guru/smells/inappropriate-intimacy)

# Performance
* [Only use `async` for low-intensive long-running activities (AV1820)](https://csharpcodingguidelines.com/performance-guidelines/#AV1820)

# Migration guidelines
* if you merge the **master** branch with migrations to **develop** branch which contains feature migrations:
  * master migrations should be kept untouched, feature migrations should be moved to the end of this list
* if you merge **develop** branch with migrations to **feature** branch which contains feature migrations:
  * develop migrations should be kept untouched, feature migrations should be moved to the end of this list
* if you have merged your migration to develop branch and want to remove it:
  * remove migration and keep number empty
  * revert database changes manually
  * if migration has too many changes then it is better to restore the database from a clear database
* if you want to change existing migration what was applied:
  * remove this migration from the database manually (**do not change order**)
  * migration will be applied again during next deploy

# App configuration guidelines
## Add new configurations
* If requirements contain default values add these values to the code
* If in the future will be a request to overridden value dynamically on the env then the configuration will be added to App Configuration Service.

Benefits:
* This will avoid the unnecessary growth of app configuration service keys.

Example 1:
```
    public class ShowMpuForNewerCarsFeatureOptions
    {
        public bool Enabled { get; set; } = false;
        public uint AgeInYears { get; set; } = 3;
        public uint Mileage { get; set; } = 40000;
    }
``` 
Example 2:
```
configuration.GetValue("MemoryCache:kipperDiagramCacheLifeTimeInSeconds", 5 * 60)
```

# Ideas
## Add checklist with checkboxes to Pull request @<Egor Shymko> 

# Resources
* [Refactoring](https://refactoring.guru/refactoring)
* [csharpcodingguidelines](https://csharpcodingguidelines.com/)
* [SOLID](https://www.digitalocean.com/community/conceptual_articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design)