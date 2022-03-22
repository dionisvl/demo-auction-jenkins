# Установка Jenkins с Docker
## Installation to dev
- run commad `make init`
- see working URL:
    - Jenkins - http://localhost:8000/
- for show initial password:
    - `make show-initial-password`

## Installation to production
- go to provision directory and prepare target servers
  - `cd pro*`
  - `make server`
  - `make authorize`
  - `make generate-agent-key`
  - `make authorize-agents`
- in project directory run deploy to production server by example command:
    - `HOST=164.215.102.205 PORT=22 make deploy`
- Go to production URL:
  - http://jenkins.demo-auction.phpqa.ru
- For show Jenkins initial password:  
  - `cd pro*`
  - `make show-initial-password`


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


