# homework_10_lms

## Огляд Кроків та Команд

### 1. Створення репозиторію ECR
Створено репозиторій в Amazon ECR через AWS Management Console.

### 2. Створення Користувача IAM та політик
Створено користувача IAM та прикріплено політики з повними правами доступу до ECR (бо можу).

### 3. Генерація ключів доступу для користувача IAM
Створено ключі доступу для користувача IAM у AWS Management Console.

### 4. Налаштування AWS CLI
Налаштовано AWS CLI з використанням облікових даних користувача IAM за допомогою команди 

```bash
aws configure
```

### 5. Локальне Завантаження Docker Зображення 
Завантажено Docker зображення командою з https://gallery.ecr.aws.
```bash
docker pull nginx:latest
``` 

### 6. Автентифікація Docker з AWS ECR
Автентифіковано Docker до AWS ECR за допомогою команди:

```bash
aws ecr get-login-password --region [регіон] | docker login --username AWS --password-stdin [номер-облікового-запису].dkr.ecr.[регіон].amazonaws.com
```

### 7. Присвоєння Тега Docker Зображенню для ECR
Присвоєно тег Docker зображенню для ECR за допомогою команди:

```bash
docker tag nginx:latest [номер-облікового-запису].dkr.ecr.[регіон].amazonaws.com/my-repository:my-tag
```


### 8. Завантаження Docker Зображення до ECR
Завантажено теговане зображення до ECR за допомогою команди:

```bash
docker push [номер-облікового-запису].dkr.ecr.[регіон].amazonaws.com/my-repository:my-tag
```

### 9. Створення ECS Кластеру
Створено ECS кластер через AWS Management Console, вибравши необхідний тип запуску задач.

### 10. Створення Опису Задачі (Task Definition)
У ECS створено новий Task Definition, де обрано Docker зображення з нашого ECR репозиторію та налаштовано перевірку здоров'я контейнера:

```json
{
    "portMappings": [
      {
        "containerPort": 80,
        "hostPort": 80
      }
    ],
    "healthCheck": {
      "command": [
        "CMD-SHELL",
        "curl -f http://localhost/ || exit 1"
      ],
      "interval": 30,
      "timeout": 5,
      "retries": 3,
      "startPeriod": 0
    }    
  ]
}
```
### 11. Створення Target Group
Створено нову target group у EC2 Management Console, вибравши протокол HTTP і вказавши порт 80. Для типу цілей вибрано "ip", а не "instance".

### 12. Створення Application Load Balancer
У EC2 Management Console створено Application Load Balancer, який використовує раніше створену target group. Load balancer налаштовано на прийом вхідного трафіку HTTP на порт 80.

### 13. Створення Service в ECS Cluster
У ECS cluster створено новий service, вибравши task definition, Application Load Balancer, і target group. Вказано кількість бажаних реплік задачі. Service автоматично розпочне моніторинг здоров'я контейнерів і управління доступом до них через DNS ім'я Application Load Balancer.

### P.S Важливо налаштувати security group for VPS і дозвонили вхідний трафік :)









