# homework_10_lms

## Огляд Кроків та Команд

### 1. Створення Репозиторію ECR
Створено репозиторій в Amazon ECR через AWS Management Console.

### 2. Створення Користувача IAM та політик
Створено користувача IAM та прикріплено політики з повними правами доступу до ECR.

### 3. Генерація Ключів Доступу для Користувача IAM
Створено ключі доступу для користувача IAM у AWS Management Console.

### 4. Налаштування AWS CLI
Налаштовано AWS CLI з використанням облікових даних користувача IAM за допомогою команди 

```bash
aws configure
```

### 5. Локальне Завантаження Docker Зображення 
Завантажено Docker зображення командою з https://gallery.ecr.aws/jldeen/name.
```bash
docker pull imageName:tag
``` 

### 6. Автентифікація Docker з AWS ECR
Автентифіковано Docker до AWS ECR за допомогою команди:

```bash
aws ecr get-login-password --region [регіон] | docker login --username AWS --password-stdin [номер-облікового-запису].dkr.ecr.[регіон].amazonaws.com
```

### 7. Присвоєння Тега Docker Зображенню для ECR
Присвоєно тег Docker зображенню для ECR за допомогою команди:

```bash
docker tag imageName:tag [номер-облікового-запису].dkr.ecr.[регіон].amazonaws.com/my-repository:my-tag
```


### 8. Завантаження Docker Зображення до ECR
Завантажено теговане зображення до ECR за допомогою команди:

```bash
docker push [номер-облікового-запису].dkr.ecr.[регіон].amazonaws.com/my-repository:my-tag
```






