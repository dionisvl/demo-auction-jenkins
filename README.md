# Установка Jenkins с Docker

### Jenkins initial password
`docker-compose exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword`
### Извлечение Initial pass
Ansible ad-hoc команда по требованию  
`make show-initial-password`

### Jenkins deploy - УСТАНОВКА ДЖЕНКИНСА на сервак
`HOST=140.238.212.163 PORT=22 make deploy`

## ulr
http://jenkins.demo-auction.phpqa.ru

## Test jenkins script pipeline
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

## Очистка внутреннего докера у Jenkins
`docker-compose exec docker docker system prune -af --filter until=240h`

## Список переменных дженкинса 
- https://wiki.jenkins.io/display/JENKINS/Building+a+software+project
- мы будем использовать BUILD_NUMBER


## Создание агентов

1 Сгенерировать ключ для дженкинс агента
`make generate-agent-key`

2 Закинуть сгенерированные ключи на агентов
`make authorize-agents`

3 Возвращаемся в Дженкинс добавляем новую ноду  
-- Remote root directory: `/home/jenkins/app`  
-- launch agent via SSH  
--- SSH username with private key   
--- ID - node-1  
--- Username - jenkins  
--- private key - `agent_rsa` (PRIVATE KEY)  
--- Host Key Verification Strategy - Non
