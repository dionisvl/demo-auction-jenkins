# Установка Jenkins с Docker

### Jenkins initial password
`docker-compose exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword`
### Извлечение Initial pass
Ansible ad-hoc команда по требованию  
`make show-initial-password`

### Jenkins deploy - УСТАНОВКА ДЖЕНКИНСА на сервак
`HOST=deploy@1.1.1.1 port=22 make deploy`

## ulr
http://jenkins.demo-auction.phpqa.ru

### Сгенерировать ключ для дженкинс агента
`make generate-agent-key`

### Закинуть сгенерированные ключи на агентов
`make authorize-agents`


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