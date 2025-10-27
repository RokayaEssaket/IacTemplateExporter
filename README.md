
```markdown
# 🧩 IacTemplateExporter

> 🇫🇷 **Outil .NET 8 d’automatisation IaC (Infrastructure as Code) pour Azure.**  
> 🇬🇧 **.NET 8 automation tool for Azure IaC (Infrastructure as Code).**

---

## 🌍 Description | Description

### 🇫🇷 Français
**IacTemplateExporter** est un outil CLI développé en **.NET 8** qui permet de **scanner automatiquement un projet .NET** afin de **générer un template ARM prêt à déployer** sur Azure.  
L’objectif est d’accélérer la **mise en place d’environnements cloud reproductibles** dans les pipelines CI/CD.

Fonctionnalités principales :
- 🔍 Analyse automatique des dépendances Azure dans un projet .NET (Storage, SQL, App Service, etc.)  
- 🧠 Génération dynamique d’un template ARM (`template.json`)  
- ✏️ Suggestion et ajustement automatique des noms de ressources  
- ⚙️ Intégration transparente dans des pipelines **Azure DevOps** ou **GitHub Actions**  
- 🧾 Export des templates vers un dossier `artifacts/templates`  
- 💬 CLI interactive (Spectre.Console)  

### 🇬🇧 English
**IacTemplateExporter** is a **.NET 8 CLI tool** designed to **scan any .NET project** and **automatically generate an Azure ARM template**.  
Its purpose is to streamline the **automation of cloud infrastructure deployment** within CI/CD pipelines.

Key features:
- 🔍 Automatic Azure dependency detection in .NET projects (Storage, SQL, App Service, etc.)  
- 🧠 Dynamic ARM template generation (`template.json`)  
- ✏️ Intelligent resource name suggestions  
- ⚙️ Smooth CI/CD integration (Azure DevOps or GitHub Actions)  
- 🧾 Export templates to `artifacts/templates`  
- 💬 Interactive CLI using Spectre.Console  

---

## 🧠 Architecture

---

## ⚙️ Installation

### 🇫🇷
```bash
git clone https://github.com/RokayaEssaket/IacTemplateExporter.git
cd IacTemplateExporter/src/IacTemplateExporter.Cli
dotnet build
````

### 🇬🇧

```bash
git clone https://github.com/<your_username>/IacTemplateExporter.git
cd IacTemplateExporter/src/IacTemplateExporter.Cli
dotnet build
```

---

## 🧩 Utilisation | Usage

### 🇫🇷 Français

**Scanner un projet .NET pour détecter ses dépendances Azure :**

```bash
dotnet run --project ./src/IacTemplateExporter.Cli scan ./MonProjet.csproj
```

**Générer le template ARM automatiquement :**

```bash
dotnet run --project ./src/IacTemplateExporter.Cli export ./MonProjet.csproj
```

Le template sera exporté dans :

```
/artifacts/templates/template.json
```

### 🇬🇧 English

**Scan a .NET project to detect Azure dependencies:**

```bash
dotnet run --project ./src/IacTemplateExporter.Cli scan ./MyProject.csproj
```

**Generate the ARM template automatically:**

```bash
dotnet run --project ./src/IacTemplateExporter.Cli export ./MyProject.csproj
```

Template will be exported to:

```
/artifacts/templates/template.json
```

---

## 🧱 Exemple de sortie ARM | Sample ARM Output

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2021-09-01",
      "name": "mystorageaccount",
      "location": "[resourceGroup().location]"
    }
  ]
}
```

---

## 🤖 Intégration CI/CD

Le projet est conçu pour être intégré directement dans un pipeline Azure ou GitHub Actions.

### Exemple `build.yml` (GitHub Actions)

```yaml
name: Build & Export IaC Template

on:
  push:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup .NET
        uses: actions/setup-dotnet@v3
        with:
          dotnet-version: 8.0.x
      - name: Build
        run: dotnet build
      - name: Run Scan & Export
        run: dotnet run --project ./src/IacTemplateExporter.Cli export ./MyProject.csproj
      - name: Upload Templates
        uses: actions/upload-artifact@v3
        with:
          name: arm-templates
          path: artifacts/templates/
```

---

## 🧩 Stack technique

| Domaine        | Technologie                   |
| -------------- | ----------------------------- |
| Langage        | C# (.NET 8)                   |
| CLI            | Spectre.Console               |
| Analyse projet | Microsoft.Build + Roslyn      |
| Templates      | ARM / Bicep                   |
| Tests          | xUnit                         |
| CI/CD          | GitHub Actions / Azure DevOps |
| Export         | JSON ARM Template             |

---

## 🧑‍💻 Auteur | Author

**Rokaya Essaket**
Développeuse .NET & Cloud | Passionnée par l’automatisation, Azure et DevOps.
📫 Contact : [LinkedIn]([https://www.linkedin.com/](https://www.linkedin.com/in/rokaya-essaket-916904220) • [GitHub](https://github.com/rokayaessaket)

---

## 🪪 Licence | License

Ce projet est distribué sous licence **MIT** — voir le fichier [LICENSE](./LICENSE) pour plus de détails.
This project is licensed under the **MIT License** — see the [LICENSE](./LICENSE) file for details.

---

## 🧠 Roadmap (prochaine étapes / next steps)

* [ ] Support du format **Bicep**
* [ ] Analyse des ressources KeyVault et AppInsights
* [ ] Interface Web minimale (Blazor)
* [ ] Intégration Terraform (expérimental)
* [ ] Publication en **dotnet tool global**

✨ *“Automate your cloud, one template at a time.”* ☁️


