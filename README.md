# Установка Jenkins с Docker

## How to install to local dev
- run commad `make init`
- see working URL:
    - Jenkins - http://localhost:8000/
- for show initial password:
    - `make show-initial-password`

## How to install to production
- go to provision directory and prepare target servers
  - `cd pro*`
  - `make server`
  - `make authorize`
  - `make generate-agent-key`
  - `make authorize-agents`
- in project directory run deploy to production server by example command:
    - `HOST=147.78.67.252 PORT=2222 make deploy`
- Go to production URL:
  - http://jenkins.demo-auction.phpqa.ru
- For show Jenkins initial password:  
  - `cd pro*`
  - `make show-initial-password`
- After register your admin user, don't forget to write login-password to somewhere place for future!
- For restore settings from backup file use plugin ThinBackup:
  - https://plugins.jenkins.io/thinBackup/
  - go to http://jenkins.demo-auction.phpqa.ru/thinBackup/
  - in settings set Backup directory to /var/jenkins_home (printenv JENKINS_HOME)
  - move backup file to /var/lib/docker/volumes/jenkins_jenkins-data/_data
  - now you can press button `Restore`
- or https://plugins.jenkins.io/periodicbackup/
- Add multibranch pipeline with GitHub repository, there: https://jenkins.demo-auction.phpqa.ru/view/all/newJob
- Fill all credential there: http://jenkins.demo-auction.phpqa.ru/credentials/
- install Jenkins plugin "SSH Agent"

### Создание Jenkins агентов
- Сгенерировать ключ для дженкинс агента  
    - `make generate-agent-key`  
- Закинуть сгенерированные ключи на агентов  
    - `make authorize-agents`  
- Возвращаемся в Дженкинс добавляем новую ноду
  - Remote root directory: `/home/jenkins/app`  
  - launch agent via SSH  
  - SSH username with private key   
  - ID - node-1  
  - Username - jenkins  
  - private key - `agent_rsa` (PRIVATE KEY)  
  - Host Key Verification Strategy - Non



## Another remarks
### Test jenkins script pipeline
```
pipeline {
  agent any 
  stages {
      stage("One") {
          steps {
              sh "sleep 1"
          }
      }
      stage("Two") {
          steps {
               sh "sleep 3"
          }
      }
      stage("Three") {
          steps {
               sh "sleep 1"
          }
      }
  }
}
```

### Очистка внутреннего докера у Jenkins
`docker-compose exec docker docker system prune -af --filter until=240h`

### Список переменных дженкинса 
- https://wiki.jenkins.io/display/JENKINS/Building+a+software+project
- мы будем использовать BUILD_NUMBER


