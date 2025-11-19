# DevOps pour Mainframe : Guide Complet Mondial

**🔗 Repository GitHub :** [Learning Schooling Foundation - DevOps Mainframe](https://github.com/learning-schooling-foundation)

---

## 📖 Table des Matières

1. [Introduction](#1-introduction)
2. [Pourquoi DevOps Mainframe ?](#2-pourquoi-devops-mainframe)
3. [Architecture et Composants](#3-architecture-et-composants)
4. [Pipeline CI/CD Complet](#4-pipeline-cicd-complet)
5. [Tests Automatisés](#5-tests-automatisés)
6. [Stratégies de Déploiement](#6-stratégies-de-déploiement)
7. [Monitoring et Observabilité](#7-monitoring-et-observabilité)
8. [Sécurité DevSecOps](#8-sécurité-devsecops)
9. [Best Practices Production](#9-best-practices-production)
10. [Outils Essentiels](#10-outils-essentiels)
11. [Roadmap d'Implémentation](#11-roadmap-dimplémentation)
12. [Métriques de Succès](#12-métriques-de-succès)

---

## 1. Introduction

### Qu'est-ce que le DevOps Mainframe ?

**DevOps mainframe = Moderniser les pratiques de développement sur z/OS.**

**Le challenge unique :**
- Systèmes hérités depuis 60+ ans
- Stabilité et fiabilité CRITIQUES
- Culture traditionnelle
- Tooling legacy (ISPF, JCL, TSO)

**Le but :**
- Garder la stabilité mainframe
- Adopter la vitesse DevOps
- Automatiser TOUT
- Réduire les coûts (MIPS)

### Le Problème Sans DevOps

**Scénario typique dans une banque :**

```
Developer: "J'ai un fix urgent pour un bug critique."
Process: 
  1. Éditer code dans ISPF (30 min)
  2. Soumettre JCL de compilation (15 min)
  3. Attendre validation QA (2 jours)
  4. Créer change request (1 heure)
  5. Attendre CAB approval (1 semaine)
  6. Déployer manuellement (2 heures)
  7. Espérer que ça marche (🙏)
  
Total: 2 semaines pour un fix de 5 lignes 😱
```

**Avec DevOps :**

```
Developer: "J'ai un fix urgent."
Process:
  1. Commit dans Git (2 min)
  2. Pipeline auto : build + test + deploy DEV (10 min)
  3. Tests automatiques passent ✅
  4. Review + merge (30 min)
  5. Auto-deploy en PROD avec approval (15 min)
  
Total: 1 heure pour le fix complet 🚀
```

**C'est ça, le pouvoir du DevOps mainframe.**

---

## 2. Pourquoi DevOps Mainframe ?

### Les Enjeux Business

**1. Vitesse** ⚡

```
AVANT:  Release tous les 3-6 mois
APRÈS:  Release chaque semaine

Impact: Time-to-market 10-20x plus rapide
```

**2. Qualité** ✅

```
AVANT:  Tests manuels, régressions fréquentes
APRÈS:  Tests automatisés, CI/CD

Impact: 90% moins de bugs en production
```

**3. Compétences** 👨‍💻

```
AVANT:  Experts mainframe vieillissants, pas de relève
APRÈS:  Jeunes devs attirés par pratiques modernes

Impact: Retention et attraction de talents
```

**4. Coûts** 💰

```
AVANT:  Utilisation CPU inefficace, gaspillage MIPS
APRÈS:  Optimisation, automatisation

Impact: 30-50% réduction coûts mainframe
```

### Les Défis Spécifiques

**❌ Challenge #1 : Culture**

```
Problème: "On a toujours fait comme ça pendant 40 ans"
Solution: Change management, formation, quick wins
```

**❌ Challenge #2 : Tooling**

```
Problème: ISPF et green screen des années 70
Solution: Zowe CLI, VS Code extensions, APIs modernes
```

**❌ Challenge #3 : Coûts CPU**

```
Problème: Chaque test coûte des MIPS ($$$$)
Solution: Tests smart, parallélisation, environnements virtuels
```

**❌ Challenge #4 : Environnements**

```
Problème: Seulement 1-2 LPARs de test, file d'attente
Solution: z/OS cloud, containerisation, scheduling intelligent
```

**❌ Challenge #5 : Expertise**

```
Problème: Peu de gens connaissent COBOL + DevOps
Solution: Upskilling, docs, abstractions
```

---

## 3. Architecture et Composants

### Architecture z/OS Moderne

**Environnements typiques :**

```
┌─────────────────────────────────────────────────────────┐
│  DEVELOPMENT (LPAR DEV)                                  │
│  - Sandbox individuel par developer                      │
│  - Tests unitaires                                       │
│  - Expérimentation libre                                 │
│  - Coût CPU: Bas                                         │
└────────────────────────┬────────────────────────────────┘
                         │ git push → pipeline trigger
                         ↓
┌─────────────────────────────────────────────────────────┐
│  INTEGRATION (LPAR INT)                                  │
│  - Tests d'intégration automatiques                      │
│  - Validation fonctionnelle                              │
│  - Multiple features testées ensemble                    │
│  - Coût CPU: Moyen                                       │
└────────────────────────┬────────────────────────────────┘
                         │ tests pass → auto promote
                         ↓
┌─────────────────────────────────────────────────────────┐
│  PRE-PRODUCTION (LPAR PREP)                              │
│  - Tests de charge/performance                           │
│  - Validation finale avant PROD                          │
│  - Données de prod masquées                              │
│  - Coût CPU: Élevé                                       │
└────────────────────────┬────────────────────────────────┘
                         │ manual approval → deploy
                         ↓
┌─────────────────────────────────────────────────────────┐
│  PRODUCTION (LPAR PROD)                                  │
│  - Environnement live                                    │
│  - Millions de transactions/jour                         │
│  - Monitoring 24/7                                       │
│  - Coût CPU: TRÈS élevé                                  │
└─────────────────────────────────────────────────────────┘
```

### Stack Technique Moderne

**Gestion de Version**

```
┌──────────────────────────────────────┐
│  Git (GitHub/GitLab/Bitbucket)       │
│  - Code source (COBOL, JCL, etc)    │
│  - Branching strategy (GitFlow)      │
│  - Pull requests + reviews           │
└──────────────────────────────────────┘
         ↓
┌──────────────────────────────────────┐
│  IBM DBB (Dependency Based Build)    │
│  - Gestion dépendances intelligente  │
│  - Build incrémental                 │
│  - Cache pour performance            │
└──────────────────────────────────────┘
         ↓
┌──────────────────────────────────────┐
│  Endevor / ChangeMan                 │
│  - SCM mainframe traditionnel        │
│  - Contrôle des promotions           │
│  - Audit trail complet               │
└──────────────────────────────────────┘
```

**CI/CD Pipeline**

```
┌──────────────────────────────────────┐
│  Jenkins / GitLab CI                 │
│  - Orchestration pipeline            │
│  - Plugins mainframe                 │
│  - z/OS agents                       │
└──────────────────────────────────────┘
         ↓
┌──────────────────────────────────────┐
│  Zowe CLI                            │
│  - Automatisation z/OS               │
│  - Upload/download datasets          │
│  - Submit JCL                        │
│  - Console commands                  │
└──────────────────────────────────────┘
         ↓
┌──────────────────────────────────────┐
│  UrbanCode Deploy                    │
│  - Déploiement multi-environnement   │
│  - Rollback automatique              │
│  - Approvals workflow                │
└──────────────────────────────────────┘
```

**Testing**

```
┌──────────────────────────────────────┐
│  COBOLUnit / zUnit                   │
│  - Tests unitaires COBOL             │
│  - Mocking                           │
│  - Code coverage                     │
└──────────────────────────────────────┘
         +
┌──────────────────────────────────────┐
│  Compuware Topaz for Total Test      │
│  - Tests fonctionnels                │
│  - Regression testing                │
│  - Test data management              │
└──────────────────────────────────────┘
         +
┌──────────────────────────────────────┐
│  IBM ADDI (App Discovery)            │
│  - Analyse impact changes            │
│  - Dépendances automatiques          │
│  - Documentation vivante             │
└──────────────────────────────────────┘
```

**Monitoring**

```
┌──────────────────────────────────────┐
│  Splunk / ELK Stack                  │
│  - Logs centralisés                  │
│  - Dashboards temps réel             │
│  - Alerting intelligent              │
└──────────────────────────────────────┘
         +
┌──────────────────────────────────────┐
│  IBM Instana / Dynatrace             │
│  - APM (Application Performance)     │
│  - Distributed tracing               │
│  - AI anomaly detection              │
└──────────────────────────────────────┘
         +
┌──────────────────────────────────────┐
│  Prometheus + Grafana                │
│  - Métriques système                 │
│  - Custom metrics                    │
│  - Time-series analysis              │
└──────────────────────────────────────┘
```

---

## 4. Pipeline CI/CD Complet

### Phase 1 : Structurer le Repository Git

**Organisation moderne d'un projet mainframe :**

```
mainframe-banking-app/
│
├── src/                          # Code source
│   ├── cobol/                    # Programmes COBOL
│   │   ├── CUST-CREATE.cbl
│   │   ├── CUST-UPDATE.cbl
│   │   ├── CUST-DELETE.cbl
│   │   └── ACCOUNT-POST.cbl
│   │
│   ├── copybooks/                # Copybooks COBOL
│   │   ├── CUSTOMER.cpy
│   │   ├── ACCOUNT.cpy
│   │   └── CONSTANTS.cpy
│   │
│   ├── jcl/                      # Job Control Language
│   │   ├── compile/
│   │   │   ├── COMPILE-COBOL.jcl
│   │   │   └── LINK-EDIT.jcl
│   │   ├── deploy/
│   │   │   └── DEPLOY-PROD.jcl
│   │   └── batch/
│   │       └── DAILY-PROCESS.jcl
│   │
│   ├── dbrm/                     # DB2 Database Request Modules
│   │   └── CUSTDB.dbrm
│   │
│   ├── bms/                      # CICS Screen maps
│   │   ├── CUSTMENU.bms
│   │   └── CUSTDET.bms
│   │
│   ├── pli/                      # PL/I programs
│   │   └── BATCH-PROCESS.pli
│   │
│   └── assembler/                # Assembler programs
│       └── UTILS.asm
│
├── build/                        # Build scripts
│   ├── dbb-scripts/              # IBM DBB
│   │   ├── build.groovy
│   │   ├── dependencies.json
│   │   └── build-config.properties
│   │
│   └── jenkins/
│       └── Jenkinsfile
│
├── test/                         # Tests
│   ├── unit/                     # Tests unitaires
│   │   ├── TEST-CUST-CREATE.cbl
│   │   └── run-unit-tests.jcl
│   │
│   ├── integration/              # Tests d'intégration
│   │   ├── test-cics-flow.sh
│   │   └── run-integration.jcl
│   │
│   └── performance/              # Tests de charge
│       └── load-test-script.jmx
│
├── deploy/                       # Déploiement
│   ├── scripts/
│   │   ├── deploy-dev.sh
│   │   ├── deploy-prod.sh
│   │   └── rollback.sh
│   │
│   └── rollback/
│       └── rollback-procedures.md
│
├── config/                       # Configuration
│   ├── dev/
│   │   ├── db2-config.properties
│   │   └── cics-regions.yml
│   │
│   ├── test/
│   └── prod/
│
├── docs/                         # Documentation
│   ├── architecture/
│   │   └── system-design.md
│   │
│   ├── runbooks/
│   │   ├── deployment.md
│   │   └── troubleshooting.md
│   │
│   └── api/
│       └── interfaces.md
│
├── .gitignore
├── README.md
└── CHANGELOG.md
```

### Phase 2 : Conversion EBCDIC ↔ UTF-8

**Le problème :** Mainframe utilise EBCDIC, Git utilise UTF-8.

**Solution 1 : iconv (Linux)**

```bash
# EBCDIC → UTF-8 (pour commit dans Git)
iconv -f IBM-1047 -t UTF-8 programme.cbl > programme.cbl.utf8

# UTF-8 → EBCDIC (pour upload sur mainframe)
iconv -f UTF-8 -t IBM-1047 programme.cbl.utf8 > programme.cbl
```

**Solution 2 : Zowe CLI (Recommandé)**

```bash
# Download depuis mainframe (auto-conversion)
zowe files download ds "USER.COBOL(PROG001)" \
    -f programme.cbl \
    --encoding IBM-1047

# Upload vers mainframe (auto-conversion)
zowe files upload file-to-data-set programme.cbl \
    "USER.COBOL(PROG001)" \
    --encoding IBM-1047
```

**Solution 3 : .gitattributes (Automatique)**

```gitattributes
# .gitattributes
*.cbl text eol=lf encoding=IBM-1047
*.cpy text eol=lf encoding=IBM-1047
*.jcl text eol=lf encoding=IBM-1047
*.bms text eol=lf encoding=IBM-1047
```

### Phase 3 : Build Automatisé avec IBM DBB

**Script DBB (Groovy) :**

```groovy
// build.groovy
@groovy.transform.BaseScript com.ibm.dbb.groovy.ScriptLoader baseScript
import com.ibm.dbb.build.*
import com.ibm.dbb.dependency.*
import com.ibm.dbb.repository.*

println "=========================================="
println "DBB Build Started"
println "=========================================="

// Configuration
def sourceDir = "/u/jenkins/workspace/banking-app/src/cobol"
def buildDir = "/u/jenkins/workspace/banking-app/build"
def hlq = "JENKINS.BUILD.${env.BUILD_NUMBER}"
def loadHLQ = "JENKINS.LOAD.${env.BUILD_NUMBER}"

println "Source: ${sourceDir}"
println "HLQ: ${hlq}"

// Créer build report
def buildReport = BuildReportFactory.getBuildReport()
buildReport.setState(buildReport.State.INPROGRESS)

try {
    // Scan des dépendances
    println "\n=== Scanning Dependencies ==="
    def scanner = new DependencyScanner()
    scanner.setSourceDir(sourceDir)
    
    def scanResults = scanner.scan(
        file: "**/*.cbl",
        scanType: DependencyScanner.COBOL_SCANNER
    )
    
    println "Found ${scanResults.size()} COBOL programs"
    
    // Déterminer ce qui a changé (incremental build)
    def repositoryClient = new RepositoryClient()
    def changedFiles = repositoryClient.getChangedFiles()
    
    println "\n=== Changed Files ==="
    changedFiles.each { file ->
        println "  - ${file}"
    }
    
    // Build chaque programme changé + dépendances
    println "\n=== Compiling Programs ==="
    
    def impactedFiles = []
    changedFiles.each { changedFile ->
        // Ajouter le fichier changé
        impactedFiles.add(changedFile)
        
        // Ajouter ses dépendants (qui l'appellent)
        def dependents = repositoryClient.getDependents(changedFile)
        impactedFiles.addAll(dependents)
    }
    
    // Dédupliquer
    impactedFiles = impactedFiles.unique()
    
    println "Building ${impactedFiles.size()} programs (including dependents)"
    
    def compileFailed = false
    
    impactedFiles.each { logicalFile ->
        println "\n--- Compiling ${logicalFile.file} ---"
        
        try {
            // Compilation COBOL
            def cobol = new MVSExec()
                .file(logicalFile.file)
                .pgm("IGYCRCTL")
                .parm("LIB,APOST,DYNAM,SQL")
                .dd(new DDStatement()
                    .name("SYSIN")
                    .dsn(logicalFile.file)
                    .options("shr"))
                .dd(new DDStatement()
                    .name("SYSLIN")
                    .dsn("${hlq}.OBJ")
                    .options("shr"))
                .dd(new DDStatement()
                    .name("SYSPRINT")
                    .options("sysout=*"))
                .dd(new DDStatement()
                    .name("SYSLIB")
                    .dsn("${hlq}.COPYLIB")
                    .options("shr"))
                
            def rc = cobol.execute()
            
            if (rc > 4) {
                println "❌ Compilation FAILED with RC=${rc}"
                buildReport.addRecord(logicalFile.file, BuildReport.Status.FAILED)
                compileFailed = true
            } else {
                println "✅ Compilation OK (RC=${rc})"
                buildReport.addRecord(logicalFile.file, BuildReport.Status.SUCCESS)
                
                // Link-edit si compilation OK
                println "--- Linking ${logicalFile.file} ---"
                
                def linkedit = new MVSExec()
                    .pgm("IEWL")
                    .parm("LIST,LET,XREF")
                    .dd(new DDStatement()
                        .name("SYSLIN")
                        .dsn("${hlq}.OBJ(${logicalFile.member})")
                        .options("shr"))
                    .dd(new DDStatement()
                        .name("SYSLMOD")
                        .dsn("${loadHLQ}(${logicalFile.member})")
                        .options("shr"))
                    .dd(new DDStatement()
                        .name("SYSPRINT")
                        .options("sysout=*"))
                
                def linkRc = linkedit.execute()
                
                if (linkRc > 4) {
                    println "❌ Link-edit FAILED with RC=${linkRc}"
                    compileFailed = true
                } else {
                    println "✅ Link-edit OK (RC=${linkRc})"
                }
            }
        } catch (Exception e) {
            println "❌ Exception during build: ${e.message}"
            buildReport.addRecord(logicalFile.file, BuildReport.Status.ERROR)
            compileFailed = true
        }
    }
    
    // Résultat final
    println "\n=========================================="
    if (compileFailed) {
        println "BUILD FAILED ❌"
        buildReport.setState(buildReport.State.FAILED)
        System.exit(1)
    } else {
        println "BUILD SUCCESSFUL ✅"
        buildReport.setState(buildReport.State.COMPLETE)
        println "Load library: ${loadHLQ}"
    }
    println "=========================================="
    
} catch (Exception e) {
    println "\n❌ BUILD ERROR: ${e.message}"
    e.printStackTrace()
    buildReport.setState(buildReport.State.FAILED)
    System.exit(1)
}
```

### Phase 4 : Pipeline Jenkins Complet

**Jenkinsfile production-ready :**

```groovy
// Jenkinsfile
pipeline {
    agent { 
        label 'zos-agent'  // Agent Jenkins sur z/OS ou avec accès z/OS
    }
    
    environment {
        // Credentials
        ZOWE_OPT_HOST = credentials('zos-host')
        ZOWE_OPT_USER = credentials('zos-user')
        ZOWE_OPT_PASSWORD = credentials('zos-password')
        
        // Build info
        BUILD_HLQ = "JENKINS.BUILD.${BUILD_NUMBER}"
        LOAD_HLQ = "JENKINS.LOAD.${BUILD_NUMBER}"
        
        // Environnements
        DEV_LOADLIB = "DEV.BANKING.LOADLIB"
        TEST_LOADLIB = "TEST.BANKING.LOADLIB"
        PROD_LOADLIB = "PROD.BANKING.LOADLIB"
        
        // CICS regions
        DEV_CICS = "CICSDEV"
        TEST_CICS = "CICSTEST"
        PROD_CICS = "CICSPROD"
    }
    
    options {
        // Garder seulement les 30 derniers builds
        buildDiscarder(logRotator(numToKeepStr: '30'))
        
        // Timeout global
        timeout(time: 2, unit: 'HOURS')
        
        // Pas de builds concurrents pour même branch
        disableConcurrentBuilds()
    }
    
    stages {
        stage('🔍 Checkout') {
            steps {
                script {
                    echo "=========================================="
                    echo "STAGE: Checkout"
                    echo "Branch: ${env.BRANCH_NAME}"
                    echo "Build: ${env.BUILD_NUMBER}"
                    echo "=========================================="
                }
                
                checkout scm
                
                script {
                    // Déterminer les fichiers changés
                    def changes = sh(
                        script: 'git diff --name-only HEAD~1',
                        returnStdout: true
                    ).trim()
                    
                    echo "Changed files:\n${changes}"
                    
                    env.CHANGED_FILES = changes
                }
            }
        }
        
        stage('📤 Upload Sources to z/OS') {
            steps {
                script {
                    echo "=========================================="
                    echo "STAGE: Upload Sources"
                    echo "Target HLQ: ${BUILD_HLQ}"
                    echo "=========================================="
                }
                
                // Créer les datasets
                sh """
                    zowe files create data-set-partitioned ${BUILD_HLQ}.COBOL \
                        --size 20CYL --secondary 5 --record-format FB \
                        --record-length 80 --block-size 27920
                    
                    zowe files create data-set-partitioned ${BUILD_HLQ}.COPYLIB \
                        --size 5CYL --secondary 1 --record-format FB \
                        --record-length 80 --block-size 27920
                    
                    zowe files create data-set-partitioned ${BUILD_HLQ}.JCL \
                        --size 5CYL --secondary 1 --record-format FB \
                        --record-length 80 --block-size 27920
                """
                
                // Upload COBOL sources
                sh """
                    zowe files upload dir-to-pds src/cobol ${BUILD_HLQ}.COBOL \
                        --encoding IBM-1047 --recursive
                """
                
                // Upload copybooks
                sh """
                    zowe files upload dir-to-pds src/copybooks ${BUILD_HLQ}.COPYLIB \
                        --encoding IBM-1047 --recursive
                """
                
                // Upload JCL
                sh """
                    zowe files upload dir-to-pds src/jcl ${BUILD_HLQ}.JCL \
                        --encoding IBM-1047 --recursive
                """
                
                echo "✅ Sources uploaded successfully"
            }
        }
        
        stage('🔨 Build with DBB') {
            steps {
                script {
                    echo "=========================================="
                    echo "STAGE: Build"
                    echo "=========================================="
                }
                
                // Lancer le build DBB
                sh """
                    groovy build/dbb-scripts/build.groovy \
                        --sourceDir /u/jenkins/workspace/${JOB_NAME}/src \
                        --buildHLQ ${BUILD_HLQ} \
                        --loadHLQ ${LOAD_HLQ}
                """
                
                echo "✅ Build completed"
            }
        }
        
        stage('🧪 Unit Tests') {
            steps {
                script {
                    echo "=========================================="
                    echo "STAGE: Unit Tests"
                    echo "=========================================="
                }
                
                // Soumettre les tests unitaires
                sh """
                    zowe jobs submit local-file test/unit/run-unit-tests.jcl \
                        --wait-for-output --view-all-spool-content \
                        > test-output.txt
                """
                
                // Parser les résultats
                script {
                    def testOutput = readFile('test-output.txt')
                    if (testOutput.contains('ALL TESTS PASSED')) {
                        echo "✅ All unit tests passed"
                    } else {
                        error "❌ Unit tests failed"
                    }
                }
                
                // Publier résultats JUnit (si format XML)
                junit allowEmptyResults: true, testResults: 'test-results/*.xml'
            }
        }
        
        stage('📊 Code Quality') {
            steps {
                script {
                    echo "=========================================="
                    echo "STAGE: Code Quality"
                    echo "=========================================="
                }
                
                // SonarQube scan
                withSonarQubeEnv('SonarQube') {
                    sh """
                        sonar-scanner \
                            -Dsonar.projectKey=banking-app \
                            -Dsonar.sources=src/cobol \
                            -Dsonar.cobol.file.suffixes=cbl,cob \
                            -Dsonar.cobol.copy.suffixes=cpy \
                            -Dsonar.cobol.copy.directories=src/copybooks
                    """
                }
                
                // Quality gate
                timeout(time: 10, unit: 'MINUTES') {
                    def qg = waitForQualityGate()
                    if (qg.status != 'OK') {
                        error "❌ Quality gate failed: ${qg.status}"
                    }
                }
                
                echo "✅ Code quality checks passed"
            }
        }
        
        stage('🚀 Deploy to DEV') {
            steps {
                script {
                    echo "=========================================="
                    echo "STAGE: Deploy to DEV"
                    echo "=========================================="
                }
                
                // Copier load library vers DEV
                sh """
                    zowe files copy data-set ${LOAD_HLQ} ${DEV_LOADLIB} --replace
                """
                
                // NEWCOPY des programmes CICS
                sh """
                    zowe console issue command "F ${DEV_CICS},NEWCOPY PROG(*)"
                """
                
                // Vérifier health
                sh './deploy/scripts/healthcheck.sh DEV'
                
                echo "✅ Deployed to DEV"
            }
        }
        
        stage('🔬 Integration Tests') {
            when {
                branch 'main'
            }
            steps {
                script {
                    echo "=========================================="
                    echo "STAGE: Integration Tests"
                    echo "=========================================="
                }
                
                // Tests d'intégration
                sh """
                    zowe jobs submit local-file test/integration/run-integration.jcl \
                        --wait-for-output
                """
                
                // Tests CICS
                sh './test/integration/test-cics-flow.sh'
                
                echo "✅ Integration tests passed"
            }
        }
        
        stage('📦 Deploy to TEST') {
            when {
                branch 'main'
            }
            steps {
                script {
                    echo "=========================================="
                    echo "STAGE: Deploy to TEST"
                    echo "=========================================="
                }
                
                // Backup current
                sh """
                    zowe files copy data-set ${TEST_LOADLIB} \
                        ${TEST_LOADLIB}.BACKUP.${BUILD_NUMBER}
                """
                
                // Deploy
                sh """
                    zowe files copy data-set ${LOAD_HLQ} ${TEST_LOADLIB} --replace
                """
                
                // NEWCOPY
                sh """
                    zowe console issue command "F ${TEST_CICS},NEWCOPY PROG(*)"
                """
                
                // Health check
                sh './deploy/scripts/healthcheck.sh TEST'
                
                echo "✅ Deployed to TEST"
            }
        }
        
        stage('⚡ Performance Tests') {
            when {
                branch 'main'
            }
            steps {
                script {
                    echo "=========================================="
                    echo "STAGE: Performance Tests"
                    echo "=========================================="
                }
                
                // JMeter load tests
                sh """
                    jmeter -n -t test/performance/load-test-script.jmx \
                        -l results.jtl \
                        -j jmeter.log
                """
                
                // Analyser résultats
                perfReport sourceDataFiles: 'results.jtl'
                
                echo "✅ Performance tests completed"
            }
        }
        
        stage('🎯 Deploy to PROD') {
            when {
                branch 'main'
            }
            input {
                message "Deploy to Production?"
                ok "Deploy"
                submitter "tech-lead,release-manager"
            }
            steps {
                script {
                    echo "=========================================="
                    echo "STAGE: Deploy to PRODUCTION"
                    echo "=========================================="
                }
                
                // Backup PROD actuel
                sh """
                    zowe files copy data-set ${PROD_LOADLIB} \
                        ${PROD_LOADLIB}.BACKUP.${BUILD_NUMBER}
                """
                
                // Créer change record
                sh """
                    curl -X POST https://changemanagement.company.com/api/changes \
                        -H "Content-Type: application/json" \
                        -d '{
                            "build": "${BUILD_NUMBER}",
                            "deployer": "${env.BUILD_USER}",
                            "timestamp": "'$(date -u +%Y-%m-%dT%H:%M:%SZ)'"
                        }'
                """
                
                // Deploy
                sh """
                    zowe files copy data-set ${LOAD_HLQ} ${PROD_LOADLIB} --replace
                """
                
                // NEWCOPY CICS (gradual si multiple régions)
                sh """
                    zowe console issue command "F ${PROD_CICS},NEWCOPY PROG(*)"
                """
                
                // Health check
                sh './deploy/scripts/healthcheck.sh PROD'
                
                // Smoke tests
                sh './test/smoke/smoke-tests.sh'
                
                echo "✅ Deployed to PRODUCTION"
                
                // Notification
                slackSend(
                    color: 'good',
                    message: """
                        ✅ Production Deployment Successful
                        Build: ${BUILD_NUMBER}
                        Branch: ${BRANCH_NAME}
                        Deployer: ${env.BUILD_USER}
                    """
                )
            }
        }
    }
    
    post {
        always {
            script {
                echo "=========================================="
                echo "POST: Cleanup"
                echo "=========================================="
            }
            
            // Cleanup datasets temporaires
            sh """
                zowe files delete data-set ${BUILD_HLQ}.COBOL -f || true
                zowe files delete data-set ${BUILD_HLQ}.COPYLIB -f || true
                zowe files delete data-set ${BUILD_HLQ}.JCL -f || true
                zowe files delete data-set ${BUILD_HLQ}.OBJ -f || true
            """
            
            // Archiver artifacts
            archiveArtifacts artifacts: '**/*.log', allowEmptyArchive: true
        }
        
        success {
            echo "✅ Pipeline completed successfully"
            
            slackSend(
                color: 'good',
                message: "✅ Build ${BUILD_NUMBER} succeeded"
            )
        }
        
        failure {
            echo "❌ Pipeline failed"
            
            slackSend(
                color: 'danger',
                message: """
                    ❌ Build ${BUILD_NUMBER} failed
                    Stage: ${env.STAGE_NAME}
                    Branch: ${BRANCH_NAME}
                """
            )
            
            // Email
            mail to: 'devops-team@company.com',
                 subject: "Pipeline Failed: ${env.JOB_NAME} #${BUILD_NUMBER}",
                 body: """
                     Build failed at stage: ${env.STAGE_NAME}
                     
                     See: ${env.BUILD_URL}
                 """
        }
        
        unstable {
            echo "⚠️ Pipeline unstable"
            
            slackSend(
                color: 'warning',
                message: "⚠️ Build ${BUILD_NUMBER} unstable"
            )
        }
    }
}
```

---

## 5. Tests Automatisés

### Tests Unitaires COBOL

**Framework: COBOLUnit**

**Programme à tester (CALCULATE.cbl) :**

```cobol
       IDENTIFICATION DIVISION.
       PROGRAM-ID. CALCULATE.
       
       DATA DIVISION.
       LINKAGE SECTION.
       01  LS-RESULT           PIC 9(5).
       01  LS-VALUE1           PIC 9(3).
       01  LS-VALUE2           PIC 9(3).
       
       PROCEDURE DIVISION USING LS-RESULT LS-VALUE1 LS-VALUE2.
           COMPUTE LS-RESULT = LS-VALUE1 * LS-VALUE2
           GOBACK.
```

**Test unitaire (TEST-CALCULATE.cbl) :**

```cobol
       IDENTIFICATION DIVISION.
       PROGRAM-ID. TEST-CALCULATE.
       
       DATA DIVISION.
       WORKING-STORAGE SECTION.
       01  WS-TEST-NAME        PIC X(50).
       01  WS-RESULT           PIC 9(5).
       01  WS-EXPECTED         PIC 9(5).
       01  WS-VALUE1           PIC 9(3).
       01  WS-VALUE2           PIC 9(3).
       01  WS-TEST-COUNT       PIC 99 VALUE 0.
       01  WS-PASS-COUNT       PIC 99 VALUE 0.
       01  WS-FAIL-COUNT       PIC 99 VALUE 0.
       
       PROCEDURE DIVISION.
       MAIN-LOGIC.
           DISPLAY '========================================='
           DISPLAY 'UNIT TESTS FOR CALCULATE'
           DISPLAY '========================================='
           
           PERFORM TEST-MULTIPLY-POSITIVE
           PERFORM TEST-MULTIPLY-ZERO
           PERFORM TEST-MULTIPLY-LARGE
           
           DISPLAY ' '
           DISPLAY '========================================='
           DISPLAY 'TEST RESULTS:'
           DISPLAY 'Total:  ' WS-TEST-COUNT
           DISPLAY 'Passed: ' WS-PASS-COUNT
           DISPLAY 'Failed: ' WS-FAIL-COUNT
           DISPLAY '========================================='
           
           IF WS-FAIL-COUNT > 0
              DISPLAY 'TESTS FAILED ❌'
              MOVE 8 TO RETURN-CODE
           ELSE
              DISPLAY 'ALL TESTS PASSED ✅'
              MOVE 0 TO RETURN-CODE
           END-IF
           
           STOP RUN.
       
       TEST-MULTIPLY-POSITIVE.
           MOVE 'Multiply 10 * 15 = 150' TO WS-TEST-NAME
           ADD 1 TO WS-TEST-COUNT
           
           MOVE 10 TO WS-VALUE1
           MOVE 15 TO WS-VALUE2
           MOVE 150 TO WS-EXPECTED
           
           CALL 'CALCULATE' USING WS-RESULT WS-VALUE1 WS-VALUE2
           
           IF WS-RESULT = WS-EXPECTED
              ADD 1 TO WS-PASS-COUNT
              DISPLAY '✓ PASS: ' WS-TEST-NAME
           ELSE
              ADD 1 TO WS-FAIL-COUNT
              DISPLAY '✗ FAIL: ' WS-TEST-NAME
              DISPLAY '   Expected: ' WS-EXPECTED
              DISPLAY '   Got:      ' WS-RESULT
           END-IF.
       
       TEST-MULTIPLY-ZERO.
           MOVE 'Multiply by zero = 0' TO WS-TEST-NAME
           ADD 1 TO WS-TEST-COUNT
           
           MOVE 100 TO WS-VALUE1
           MOVE 0 TO WS-VALUE2
           MOVE 0 TO WS-EXPECTED
           
           CALL 'CALCULATE' USING WS-RESULT WS-VALUE1 WS-VALUE2
           
           IF WS-RESULT = WS-EXPECTED
              ADD 1 TO WS-PASS-COUNT
              DISPLAY '✓ PASS: ' WS-TEST-NAME
           ELSE
              ADD 1 TO WS-FAIL-COUNT
              DISPLAY '✗ FAIL: ' WS-TEST-NAME
              DISPLAY '   Expected: ' WS-EXPECTED
              DISPLAY '   Got:      ' WS-RESULT
           END-IF.
       
       TEST-MULTIPLY-LARGE.
           MOVE 'Multiply large numbers' TO WS-TEST-NAME
           ADD 1 TO WS-TEST-COUNT
           
           MOVE 999 TO WS-VALUE1
           MOVE 99 TO WS-VALUE2
           MOVE 98901 TO WS-EXPECTED
           
           CALL 'CALCULATE' USING WS-RESULT WS-VALUE1 WS-VALUE2
           
           IF WS-RESULT = WS-EXPECTED
              ADD 1 TO WS-PASS-COUNT
              DISPLAY '✓ PASS: ' WS-TEST-NAME
           ELSE
              ADD 1 TO WS-FAIL-COUNT
              DISPLAY '✗ FAIL: ' WS-TEST-NAME
              DISPLAY '   Expected: ' WS-EXPECTED
              DISPLAY '   Got:      ' WS-RESULT
           END-IF.
```

**JCL pour run tests :**

```jcl
//RUNTEST JOB (TEST),'RUN UNIT TESTS',CLASS=A,MSGCLASS=X
//STEP1   EXEC PGM=TEST-CALCULATE
//STEPLIB  DD DSN=TEST.LOADLIB,DISP=SHR
//SYSOUT   DD SYSOUT=*
//SYSPRINT DD SYSOUT=*
```

### Tests d'Intégration CICS

**Script de test (test-cics-transaction.sh) :**

```bash
#!/bin/bash
# test-cics-transaction.sh

set -e

echo "=========================================="
echo "CICS Integration Tests"
echo "=========================================="

# Test 1: Créer un customer
echo ""
echo "Test 1: Create Customer"
response=$(zowe cics invoke transaction "CUSC" \
    --region-name "CICSTEST" \
    --program "CUST-CREATE" \
    --input-data "CREATE|CUST001|John Doe|john@example.com" \
    --timeout 30)

if echo "$response" | grep -q "SUCCESS"; then
    echo "✓ PASS: Customer created"
else
    echo "✗ FAIL: Customer creation failed"
    echo "Response: $response"
    exit 1
fi

# Test 2: Lire le customer créé
echo ""
echo "Test 2: Read Customer"
response=$(zowe cics invoke transaction "CUSR" \
    --region-name "CICSTEST" \
    --program "CUST-READ" \
    --input-data "READ|CUST001" \
    --timeout 30)

if echo "$response" | grep -q "John Doe"; then
    echo "✓ PASS: Customer read correctly"
else
    echo "✗ FAIL: Customer read failed"
    echo "Response: $response"
    exit 1
fi

# Test 3: Update customer
echo ""
echo "Test 3: Update Customer"
response=$(zowe cics invoke transaction "CUSU" \
    --region-name "CICSTEST" \
    --program "CUST-UPDATE" \
    --input-data "UPDATE|CUST001|Jane Doe|jane@example.com" \
    --timeout 30)

if echo "$response" | grep -q "SUCCESS"; then
    echo "✓ PASS: Customer updated"
else
    echo "✗ FAIL: Customer update failed"
    echo "Response: $response"
    exit 1
fi

# Test 4: Vérifier l'update
echo ""
echo "Test 4: Verify Update"
response=$(zowe cics invoke transaction "CUSR" \
    --region-name "CICSTEST" \
    --program "CUST-READ" \
    --input-data "READ|CUST001" \
    --timeout 30)

if echo "$response" | grep -q "Jane Doe"; then
    echo "✓ PASS: Update verified"
else
    echo "✗ FAIL: Update verification failed"
    echo "Response: $response"
    exit 1
fi

# Test 5: Delete customer
echo ""
echo "Test 5: Delete Customer"
response=$(zowe cics invoke transaction "CUSD" \
    --region-name "CICSTEST" \
    --program "CUST-DELETE" \
    --input-data "DELETE|CUST001" \
    --timeout 30)

if echo "$response" | grep -q "SUCCESS"; then
    echo "✓ PASS: Customer deleted"
else
    echo "✗ FAIL: Customer deletion failed"
    echo "Response: $response"
    exit 1
fi

# Test 6: Vérifier la deletion
echo ""
echo "Test 6: Verify Deletion"
response=$(zowe cics invoke transaction "CUSR" \
    --region-name "CICSTEST" \
    --program "CUST-READ" \
    --input-data "READ|CUST001" \
    --timeout 30)

if echo "$response" | grep -q "NOT FOUND"; then
    echo "✓ PASS: Deletion verified"
else
    echo "✗ FAIL: Customer still exists"
    echo "Response: $response"
    exit 1
fi

echo ""
echo "=========================================="
echo "ALL INTEGRATION TESTS PASSED ✅"
echo "=========================================="
```

### Tests de Performance (JMeter)

**Script JMeter (load-test-script.jmx) :**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jmeterTestPlan version="1.2">
  <hashTree>
    <TestPlan guiclass="TestPlanGui" testclass="TestPlan">
      <stringProp name="TestPlan.name">CICS Load Test</stringProp>
      <elementProp name="TestPlan.user_defined_variables" elementType="Arguments">
        <collectionProp name="Arguments.arguments">
          <elementProp name="HOST" elementType="Argument">
            <stringProp name="Argument.name">HOST</stringProp>
            <stringProp name="Argument.value">cics.mainframe.com</stringProp>
          </elementProp>
          <elementProp name="PORT" elementType="Argument">
            <stringProp name="Argument.name">PORT</stringProp>
            <stringProp name="Argument.value">3270</stringProp>
          </elementProp>
        </collectionProp>
      </elementProp>
    </TestPlan>
    
    <hashTree>
      <ThreadGroup guiclass="ThreadGroupGui" testclass="ThreadGroup">
        <stringProp name="ThreadGroup.name">User Load</stringProp>
        <intProp name="ThreadGroup.num_threads">100</intProp>
        <intProp name="ThreadGroup.ramp_time">60</intProp>
        <longProp name="ThreadGroup.duration">300</longProp>
        <boolProp name="ThreadGroup.scheduler">true</boolProp>
      </ThreadGroup>
      
      <hashTree>
        <!-- Test transaction CICS -->
        <HTTPSamplerProxy guiclass="HttpTestSampleGui" testclass="HTTPSamplerProxy">
          <stringProp name="HTTPSampler.domain">${HOST}</stringProp>
          <stringProp name="HTTPSampler.port">${PORT}</stringProp>
          <stringProp name="HTTPSampler.path">/cics/transaction</stringProp>
          <stringProp name="HTTPSampler.method">POST</stringProp>
          <stringProp name="HTTPSampler.name">CICS Transaction</stringProp>
        </HTTPSamplerProxy>
        
        <!-- Assertions -->
        <ResponseAssertion guiclass="AssertionGui" testclass="ResponseAssertion">
          <stringProp name="Assertion.test_field">Assertion.response_data</stringProp>
          <intProp name="Assertion.test_type">16</intProp>
          <stringProp name="Assertion.test_string">SUCCESS</stringProp>
        </ResponseAssertion>
        
        <DurationAssertion guiclass="DurationAssertionGui" testclass="DurationAssertion">
          <longProp name="DurationAssertion.duration">1000</longProp>
        </DurationAssertion>
      </hashTree>
    </hashTree>
  </hashTree>
</jmeterTestPlan>
```

---

## 6. Stratégies de Déploiement

### Blue-Green Deployment

**Concept :**

```
┌──────────────────────────────────────────┐
│  CICS REGION A (Blue) - Version 1.0      │
│  ← 100% du trafic                        │
│  ← PROD actuelle                         │
└──────────────────────────────────────────┘

┌──────────────────────────────────────────┐
│  CICS REGION B (Green) - Version 1.1     │
│  ← 0% du trafic                          │
│  ← Nouvelle version                      │
│  ← Tests en cours                        │
└──────────────────────────────────────────┘

        ↓↓↓ SWITCH ↓↓↓

┌──────────────────────────────────────────┐
│  CICS REGION A (Blue) - Version 1.0      │
│  ← 0% du trafic                          │
│  ← Standby pour rollback                 │
└──────────────────────────────────────────┘

┌──────────────────────────────────────────┐
│  CICS REGION B (Green) - Version 1.1     │
│  ← 100% du trafic                        │
│  ← PROD actuelle                         │
└──────────────────────────────────────────┘
```

**Script de switch (switch-blue-green.sh) :**

```bash
#!/bin/bash
# switch-blue-green.sh

set -e

echo "=========================================="
echo "Blue-Green Deployment Switch"
echo "=========================================="

# Déterminer quelle région est active
CURRENT_ACTIVE=$(zowe cics get region "CICSPROD" \
    --region-type "active" | jq -r '.name')

if [[ "$CURRENT_ACTIVE" == "CICSBLUE" ]]; then
    NEW_ACTIVE="CICSGREEN"
    OLD_ACTIVE="CICSBLUE"
else
    NEW_ACTIVE="CICSBLUE"
    OLD_ACTIVE="CICSGREEN"
fi

echo "Current active: $OLD_ACTIVE"
echo "Switching to: $NEW_ACTIVE"

# Step 1: Vérifier la santé de la nouvelle région
echo ""
echo "Step 1: Health check on $NEW_ACTIVE"
./healthcheck.sh $NEW_ACTIVE

if [ $? -ne 0 ]; then
    echo "❌ Health check failed on $NEW_ACTIVE"
    exit 1
fi

echo "✅ $NEW_ACTIVE is healthy"

# Step 2: Activer la nouvelle région (graduel)
echo ""
echo "Step 2: Routing traffic to $NEW_ACTIVE"

# 10% du trafic d'abord
echo "Routing 10% traffic..."
zowe console issue command "MODIFY WLM,ROUTE=$NEW_ACTIVE,PERCENT=10"
sleep 30

# Vérifier métriques
./check-metrics.sh $NEW_ACTIVE
if [ $? -ne 0 ]; then
    echo "❌ Metrics check failed, rolling back"
    zowe console issue command "MODIFY WLM,ROUTE=$OLD_ACTIVE,PERCENT=100"
    exit 1
fi

# 50% du trafic
echo "Routing 50% traffic..."
zowe console issue command "MODIFY WLM,ROUTE=$NEW_ACTIVE,PERCENT=50"
sleep 60

# Vérifier métriques
./check-metrics.sh $NEW_ACTIVE
if [ $? -ne 0 ]; then
    echo "❌ Metrics check failed, rolling back"
    zowe console issue command "MODIFY WLM,ROUTE=$OLD_ACTIVE,PERCENT=100"
    exit 1
fi

# 100% du trafic
echo "Routing 100% traffic..."
zowe console issue command "MODIFY WLM,ROUTE=$NEW_ACTIVE,PERCENT=100"
sleep 30

# Step 3: Mettre l'ancienne région en standby
echo ""
echo "Step 3: Putting $OLD_ACTIVE in standby"
zowe console issue command "F $OLD_ACTIVE,CEMT SET SYSTEM QUIESCE"

echo ""
echo "=========================================="
echo "✅ Switch completed successfully"
echo "Active region: $NEW_ACTIVE"
echo "Standby region: $OLD_ACTIVE (ready for rollback)"
echo "=========================================="
```

### Canary Deployment

**Concept :** Déployer graduellement à un petit % d'utilisateurs d'abord.

```
┌─────────────────────────────────────────┐
│  PRODUCTION v1.0                         │
│  ← 100% trafic                          │
└─────────────────────────────────────────┘

        ↓↓↓ Deploy Canary ↓↓↓

┌─────────────────────────────────────────┐
│  PRODUCTION v1.0                         │
│  ← 90% trafic                           │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│  CANARY v1.1                            │
│  ← 10% trafic (monitoring intensif)     │
└─────────────────────────────────────────┘

   ↓ Si OK, augmenter graduellement ↓

┌─────────────────────────────────────────┐
│  CANARY v1.1                            │
│  ← 100% trafic                          │
└─────────────────────────────────────────┘
```

**Configuration WLM (Workload Manager) :**

```jcl
//WLMSETUP JOB (PROD),'CANARY DEPLOYMENT',CLASS=A
//STEP1    EXEC PGM=IWMREXEC
//SYSPRINT DD SYSOUT=*
//SYSIN    DD *
  *************************************************
  * Workload Manager - Canary Deployment Setup
  *************************************************
  
  * Définir workload pour nouvelle version
  ALTER WORKLOAD(BANKING_APP)
    CLASSIFICATION(
      * Router 10% vers canary
      QUALIFIER(VERSION,EQ,'1.1')
      IMPORTANCE(1)
      SERVICECLASSNAME(CANARY10)
      
      * 90% reste sur version stable
      QUALIFIER(VERSION,EQ,'1.0')
      IMPORTANCE(1)
      SERVICECLASSNAME(STABLE90)
    )
    
  * Service class pour canary (10%)
  DEFINE SERVICECLASS(CANARY10)
    DESCRIPTION('Canary deployment 10% traffic')
    ROUTINGTARGET(CICSCANARY)
    IMPORTANCE(1)
    
  * Service class pour stable (90%)
  DEFINE SERVICECLASS(STABLE90)
    DESCRIPTION('Stable version 90% traffic')
    ROUTINGTARGET(CICSPROD)
    IMPORTANCE(1)
/*
```

**Script de canary deployment :**

```bash
#!/bin/bash
# canary-deploy.sh

set -e

CANARY_PERCENTAGES=(10 25 50 75 100)
MONITORING_DURATION=300  # 5 minutes entre chaque étape

echo "=========================================="
echo "Canary Deployment Started"
echo "Version: $1"
echo "=========================================="

VERSION=$1

for PERCENT in "${CANARY_PERCENTAGES[@]}"; do
    echo ""
    echo "=========================================="
    echo "Deploying to $PERCENT% of traffic"
    echo "=========================================="
    
    # Ajuster le routing
    zowe console issue command \
        "MODIFY WLM,ROUTE=CANARY,VERSION=$VERSION,PERCENT=$PERCENT"
    
    echo "Monitoring for $MONITORING_DURATION seconds..."
    
    # Monitoring pendant la durée spécifiée
    END_TIME=$(($(date +%s) + MONITORING_DURATION))
    
    while [ $(date +%s) -lt $END_TIME ]; do
        # Check error rate
        ERROR_RATE=$(./get-error-rate.sh CANARY)
        
        if (( $(echo "$ERROR_RATE > 5.0" | bc -l) )); then
            echo "❌ Error rate too high: $ERROR_RATE%"
            echo "Rolling back..."
            
            # Rollback immédiat
            zowe console issue command \
                "MODIFY WLM,ROUTE=STABLE,VERSION=1.0,PERCENT=100"
            
            exit 1
        fi
        
        # Check response time
        AVG_RESPONSE=$(./get-avg-response.sh CANARY)
        
        if (( $(echo "$AVG_RESPONSE > 1000" | bc -l) )); then
            echo "❌ Response time too high: ${AVG_RESPONSE}ms"
            echo "Rolling back..."
            
            zowe console issue command \
                "MODIFY WLM,ROUTE=STABLE,VERSION=1.0,PERCENT=100"
            
            exit 1
        fi
        
        echo "✓ Error rate: $ERROR_RATE% | Avg response: ${AVG_RESPONSE}ms"
        
        sleep 30
    done
    
    echo "✅ $PERCENT% deployment successful, metrics OK"
done

echo ""
echo "=========================================="
echo "✅ Canary deployment completed"
echo "Version $VERSION now serving 100% traffic"
echo "=========================================="
```

### Rollback Rapide

**Script de rollback automatique :**

```bash
#!/bin/bash
# rollback.sh

set -e

BUILD_TO_ROLLBACK=$1

if [ -z "$BUILD_TO_ROLLBACK" ]; then
    echo "Usage: ./rollback.sh <build-number>"
    exit 1
fi

echo "=========================================="
echo "ROLLBACK TO BUILD $BUILD_TO_ROLLBACK"
echo "=========================================="

# Step 1: Backup current (just in case)
echo ""
echo "Step 1: Backing up current version..."
TIMESTAMP=$(date +%Y%m%d%H%M%S)
zowe files copy data-set PROD.LOADLIB \
    "PROD.LOADLIB.ROLLBACK.$TIMESTAMP"
echo "✅ Current version backed up"

# Step 2: Restore from backup
echo ""
echo "Step 2: Restoring build $BUILD_TO_ROLLBACK..."
zowe files copy data-set \
    "PROD.LOADLIB.BACKUP.$BUILD_TO_ROLLBACK" \
    PROD.LOADLIB --replace
echo "✅ Build $BUILD_TO_ROLLBACK restored"

# Step 3: NEWCOPY all CICS programs
echo ""
echo "Step 3: Refreshing CICS programs..."
zowe console issue command "F CICSPROD,CEMT SET PROG(*) NEW"
echo "✅ CICS programs refreshed"

# Step 4: Health check
echo ""
echo "Step 4: Running health checks..."
./healthcheck.sh PROD

if [ $? -eq 0 ]; then
    echo "✅ Health check passed"
else
    echo "❌ Health check failed after rollback"
    echo "MANUAL INTERVENTION REQUIRED"
    
    # Alert on-call
    curl -X POST https://pagerduty.com/api/incidents \
        -H "Authorization: Token token=$PAGERDUTY_TOKEN" \
        -H "Content-Type: application/json" \
        -d "{
            \"incident\": {
                \"type\": \"incident\",
                \"title\": \"Rollback failed - health check failed\",
                \"service\": {
                    \"id\": \"$SERVICE_ID\",
                    \"type\": \"service_reference\"
                },
                \"urgency\": \"high\",
                \"body\": {
                    \"type\": \"incident_body\",
                    \"details\": \"Rollback to build $BUILD_TO_ROLLBACK completed but health check failed\"
                }
            }
        }"
    
    exit 1
fi

# Step 5: Smoke tests
echo ""
echo "Step 5: Running smoke tests..."
./smoke-tests.sh

if [ $? -eq 0 ]; then
    echo "✅ Smoke tests passed"
else
    echo "❌ Smoke tests failed"
    exit 1
fi

echo ""
echo "=========================================="
echo "✅ ROLLBACK SUCCESSFUL"
echo "System rolled back to build $BUILD_TO_ROLLBACK"
echo "=========================================="

# Notification Slack
curl -X POST $SLACK_WEBHOOK_URL \
    -H 'Content-Type: application/json' \
    -d "{
        \"text\": \":warning: Rollback completed\",
        \"attachments\": [{
            \"color\": \"warning\",
            \"fields\": [
                {\"title\": \"Build\", \"value\": \"$BUILD_TO_ROLLBACK\", \"short\": true},
                {\"title\": \"Status\", \"value\": \"Successful\", \"short\": true},
                {\"title\": \"Time\", \"value\": \"$(date)\", \"short\": false}
            ]
        }]
    }"
```

---

*[... La suite du guide continue avec Monitoring, Sécurité, Best Practices, Outils, Roadmap, etc. ...]*

**📚 À SUIVRE DANS LA PARTIE 2 DU GUIDE**

---

**💎 100% Gratuit • Pour Tous • À Jamais**  
**🔗 GitHub : Learning Schooling Foundation**

---

## Pour Qui On Fait Ça ?

**Pour le dev de 24 ans à Abidjan qui veut bosser en banque.**  
**Pour la reconversion pro à 35 ans à Marseille.**  
**Pour l'étudiant à Rabat sans les €5000 d'une formation IBM.**  
**Pour le talent à Buenos Aires que les recruteurs ignorent.**

**Le DevOps mainframe peut payer €80-120K/an.**  
**Ce savoir ne devrait PAS coûter des milliers d'euros.**  
**Il devrait être gratuit. Pour tous. Pour toujours.**

**C'est notre mission. 💚**

---

**De Berkeley à Bordeaux.**  
**De Stallman à toi.**  
**Le savoir est libre.**

**🚀 Learning Schooling Foundation**
