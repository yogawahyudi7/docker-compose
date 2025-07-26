# Docker Compose Services

A comprehensive Docker Compose setup for running RabbitMQ and MongoDB services with proper networking and data persistence.

## 📋 Services Included

- **RabbitMQ** (v3.13) - Message broker with management UI
- **MongoDB** (v7.0) - NoSQL database with authentication

## 🚀 Quick Start

### Prerequisites
- Docker installed on your system
- Docker Compose installed

### Start All Services
```bash
# Start all services in the background
docker-compose up -d

# View running containers
docker-compose ps

# View logs from all services
docker-compose logs -f
```

### Stop All Services
```bash
# Stop all services
docker-compose down

# Stop and remove volumes (⚠️ This will delete all data)
docker-compose down -v
```

## 🎯 Running Individual Services

You can run specific services instead of starting everything:

### Run Only RabbitMQ
```bash
# Start only RabbitMQ service
docker-compose up -d rabbitmq

# View RabbitMQ logs
docker-compose logs -f rabbitmq

# Stop only RabbitMQ
docker-compose stop rabbitmq
```

### Run Only MongoDB
```bash
# Start only MongoDB service
docker-compose up -d mongodb

# View MongoDB logs
docker-compose logs -f mongodb

# Stop only MongoDB
docker-compose stop mongodb
```

### Run Multiple Specific Services
```bash
# Start both RabbitMQ and MongoDB (same as up -d in this case)
docker-compose up -d rabbitmq mongodb
```

## 🔗 Service Connection Details

### RabbitMQ
- **Management UI**: http://localhost:15672
- **AMQP Port**: localhost:5672
- **Username**: admin
- **Password**: admin
- **From other containers**: `rabbitmq:5672`

### MongoDB
- **Connection URI**: `mongodb://admin:admin@localhost:27017/myapp`
- **Host**: localhost
- **Port**: 27017
- **Username**: admin
- **Password**: admin
- **Database**: myapp
- **From other containers**: `mongodb:27017`

## 📁 Data Persistence

All data is persisted using Docker volumes:
- `rabbitmq_data` - RabbitMQ data and configuration
- `mongodb_data` - MongoDB database files
- `mongodb_config` - MongoDB configuration files

## 🛠️ Useful Commands

### Health Checks
```bash
# Check service status
docker-compose ps

# Check resource usage
docker stats

# Execute commands inside containers
docker-compose exec rabbitmq bash
docker-compose exec mongodb mongosh
```

### Logs and Debugging
```bash
# View logs for all services
docker-compose logs

# View logs for specific service
docker-compose logs rabbitmq
docker-compose logs mongodb

# Follow logs in real-time
docker-compose logs -f --tail=100

# View only recent logs
docker-compose logs --tail=50
```

### Data Management
```bash
# Backup MongoDB data
docker-compose exec mongodb mongodump --host localhost --port 27017 --username admin --password admin --out /data/backup

# View volume information
docker volume ls
docker volume inspect docker-compose_mongodb_data
```

## 🔧 Configuration

### Environment Variables
You can customize the services by modifying the environment variables in `docker-compose.yml`:

**RabbitMQ:**
- `RABBITMQ_DEFAULT_USER` - Default username
- `RABBITMQ_DEFAULT_PASS` - Default password

**MongoDB:**
- `MONGO_INITDB_ROOT_USERNAME` - Root username
- `MONGO_INITDB_ROOT_PASSWORD` - Root password
- `MONGO_INITDB_DATABASE` - Default database name

### Port Mapping
- RabbitMQ: `5672` (AMQP), `15672` (Management UI)
- MongoDB: `27017`

## 🚨 Troubleshooting

### Common Issues

1. **Port already in use**
   ```bash
   # Check what's using the port
   netstat -an | grep :27017
   # Change port mapping in docker-compose.yml if needed
   ```

2. **Container won't start**
   ```bash
   # Check container logs
   docker-compose logs [service-name]
   
   # Restart specific service
   docker-compose restart [service-name]
   ```

3. **Data not persisting**
   ```bash
   # Verify volumes exist
   docker volume ls
   
   # Check volume mount points
   docker-compose config
   ```

4. **Can't connect to services**
   ```bash
   # Verify services are running
   docker-compose ps
   
   # Check network connectivity
   docker-compose exec rabbitmq ping mongodb
   ```

### Reset Everything
```bash
# Stop all services and remove everything (including data)
docker-compose down -v
docker system prune -f

# Start fresh
docker-compose up -d
```

## 📝 Development Tips

- Use `docker-compose logs -f [service]` during development to monitor specific services
- The `app_network` allows services to communicate using container names as hostnames
- Data persists between container restarts thanks to volume mapping
- Use `docker-compose restart [service]` to restart individual services without affecting others

## 🤝 Contributing

1. Make changes to `docker-compose.yml`
2. Test with `docker-compose config` to validate syntax
3. Test services individually before running all together
4. Update this README if you add new services

---

**Happy Coding!** 🚀
