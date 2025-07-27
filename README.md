# Docker Compose Services

A comprehensive Docker Compose setup for running RabbitMQ, MongoDB, PostgreSQL, Elasticsearch, and OpenTelemetry (Jaeger) services with proper networking and data persistence.

## 📚 Table of Contents

- [📋 Services Overview](#-services-overview)
- [� Services Included](#-services-included)
- [�🚀 Quick Start](#-quick-start)
- [🎯 Running Individual Services](#-running-individual-services)
- [🔗 Service Connection Details](#-service-connection-details)
- [📁 Data Persistence](#-data-persistence)
- [🐰 What is RabbitMQ and Why Use It?](#-what-is-rabbitmq-and-why-use-it)
- [🍃 What is MongoDB and Why Use It?](#-what-is-mongodb-and-why-use-it)
- [🐘 What is PostgreSQL and Why Use It?](#-what-is-postgresql-and-why-use-it)
- [🔍 What is Elasticsearch and Why Use It?](#-what-is-elasticsearch-and-why-use-it)
- [🔍 What is OpenTelemetry and Why Use It?](#-what-is-opentelemetry-and-why-use-it)
- [🎯 User-Friendly Usage Guide](#-user-friendly-usage-guide)
  - [🚀 Getting Started (Beginner)](#-getting-started-beginner)
  - [🔧 Common Development Scenarios](#-common-development-scenarios)
  - [🛠️ Service-Specific Usage](#️-service-specific-usage)
    - [RabbitMQ Usage](#rabbitmq-usage)
    - [MongoDB Usage](#mongodb-usage)
    - [PostgreSQL Usage](#postgresql-usage)
    - [Elasticsearch Usage](#elasticsearch-usage)
    - [Jaeger (OpenTelemetry) Usage](#jaeger-opentelemetry-usage)
  - [🚀 Instrumenting Your Applications](#-instrumenting-your-applications)
  - [📊 Using Jaeger UI](#-using-jaeger-ui)
  - [🔧 Configuration for Different Languages](#-configuration-for-different-languages)
  - [🔍 Quick Health Checks](#-quick-health-checks)
  - [💡 Pro Tips](#-pro-tips)
- [🛠️ Useful Commands](#️-useful-commands)
- [🔧 Configuration](#-configuration)
- [🚨 Troubleshooting](#-troubleshooting)
- [📝 Development Tips](#-development-tips)
- [🤝 Contributing](#-contributing)
- [🔗 Quick Reference Links](#-quick-reference-links)

## 📋 Services Overview

| Service | Version | Function | Primary Use Cases | When to Use |
|---------|---------|----------|-------------------|-------------|
| **🐰 RabbitMQ** | v3.13 | **Message Broker & Queue System** | • Asynchronous communication<br>• Task queues & job processing<br>• Event-driven architecture<br>• Microservices messaging | • Building scalable applications<br>• Decoupling services<br>• Background job processing<br>• Real-time notifications |
| **🍃 MongoDB** | v7.0 | **NoSQL Document Database** | • Flexible schema storage<br>• JSON-like document storage<br>• Rapid prototyping<br>• Content management systems | • Storing unstructured data<br>• Agile development<br>• IoT data collection<br>• User profiles & preferences |
| **🐘 PostgreSQL** | v16 | **Relational SQL Database** | • ACID transactions<br>• Complex queries & joins<br>• Data integrity & consistency<br>• Structured data storage | • Financial applications<br>• E-commerce platforms<br>• Analytics & reporting<br>• Traditional web applications |
| **🔍 Elasticsearch** | v8.11 | **Search & Analytics Engine** | • Full-text search<br>• Log analysis & monitoring<br>• Real-time analytics<br>• Data visualization | • Search functionality<br>• Application monitoring<br>• Business intelligence<br>• Log aggregation |
| **📊 Jaeger** | v1.51 | **Distributed Tracing & Observability** | • Request tracing across services<br>• Performance monitoring<br>• Error tracking & debugging<br>• Service dependency mapping | • Microservices debugging<br>• Performance optimization<br>• Production monitoring<br>• API performance analysis |

### 🎯 **Service Categories:**

#### **📊 Data Storage**
- **PostgreSQL**: For structured, relational data requiring ACID compliance
- **MongoDB**: For flexible, document-based data with rapid schema changes
- **Elasticsearch**: For searchable data, logs, and analytics

#### **🔄 Communication & Processing**
- **RabbitMQ**: For reliable message passing and asynchronous processing
- **Jaeger**: For monitoring and tracing request flows across services

#### **🏗️ Architecture Patterns**
- **Microservices**: All services work together for distributed architecture
- **Event-Driven**: RabbitMQ enables event-based communication
- **Observability**: Jaeger provides full system visibility
- **Polyglot Persistence**: Use the right database for each use case

### 🎯 **Real-World Application Examples:**

#### **🛒 E-Commerce Platform**
```bash
# Perfect service combination for e-commerce
docker-compose up -d postgresql mongodb rabbitmq elasticsearch jaeger

# Architecture:
# • PostgreSQL: Orders, payments, inventory (ACID compliance needed)
# • MongoDB: Product catalog, user reviews (flexible schema)
# • RabbitMQ: Order processing, email notifications (async tasks)
# • Elasticsearch: Product search, recommendation engine
# • Jaeger: Monitor checkout flow, payment processing
```

#### **📱 Social Media Application**
```bash
# Social media backend services
docker-compose up -d mongodb rabbitmq elasticsearch jaeger

# Architecture:
# • MongoDB: User profiles, posts, comments (document-based)
# • RabbitMQ: Real-time notifications, feed updates
# • Elasticsearch: Content search, trending analysis
# • Jaeger: Track user engagement, API performance
```

#### **📊 Analytics Dashboard**
```bash
# Data analytics and reporting platform
docker-compose up -d postgresql elasticsearch jaeger

# Architecture:
# • PostgreSQL: Structured business data, user analytics
# • Elasticsearch: Log analysis, real-time dashboards
# • Jaeger: Monitor data pipeline performance
```

#### **🎮 Gaming Backend**
```bash
# Real-time gaming platform
docker-compose up -d mongodb rabbitmq jaeger

# Architecture:
# • MongoDB: Player profiles, game states, leaderboards
# • RabbitMQ: Real-time game events, matchmaking
# • Jaeger: Monitor game server performance
```

### 💡 **When to Choose Each Service:**

| Scenario | Recommended Services | Reason |
|----------|---------------------|---------|
| **Building a REST API** | PostgreSQL + Jaeger | Structured data + API monitoring |
| **Content Management** | MongoDB + Elasticsearch | Flexible content + search capability |
| **Real-time Chat App** | MongoDB + RabbitMQ + Jaeger | User data + messaging + performance tracking |
| **Analytics Platform** | PostgreSQL + Elasticsearch + Jaeger | Structured data + search/analytics + monitoring |
| **Microservices Architecture** | All services | Complete stack for distributed systems |
| **Rapid Prototyping** | MongoDB + RabbitMQ | Quick development with flexible schema |
| **Enterprise Application** | PostgreSQL + RabbitMQ + Jaeger | ACID compliance + async processing + monitoring |

## �📋 Services Included

- **RabbitMQ** (v3.13) - Message broker with management UI
- **MongoDB** (v7.0) - NoSQL database with authentication
- **PostgreSQL** (v16) - Relational database
- **Elasticsearch** (v8.11) - Search and analytics engine
- **Jaeger** (v1.51) - OpenTelemetry-compatible distributed tracing system

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

### Run Only PostgreSQL
```bash
# Start only PostgreSQL service
docker-compose up -d postgresql

# View PostgreSQL logs
docker-compose logs -f postgresql

# Stop only PostgreSQL
docker-compose stop postgresql
```

### Run Only Elasticsearch
```bash
# Start only Elasticsearch service
docker-compose up -d elasticsearch

# View Elasticsearch logs
docker-compose logs -f elasticsearch

# Stop only Elasticsearch
docker-compose stop elasticsearch
```

### Run Only Jaeger (OpenTelemetry)
```bash
# Start only Jaeger service
docker-compose up -d jaeger

# View Jaeger logs
docker-compose logs -f jaeger

# Stop only Jaeger
docker-compose stop jaeger
```

### Run Multiple Specific Services
```bash
# Start RabbitMQ and MongoDB only
docker-compose up -d rabbitmq mongodb

# Start databases only (MongoDB, PostgreSQL)
docker-compose up -d mongodb postgresql

# Start search stack (Elasticsearch and databases)
docker-compose up -d mongodb postgresql elasticsearch

# Start observability stack (Jaeger with databases)
docker-compose up -d jaeger mongodb postgresql

# Start full monitoring stack (all services)
docker-compose up -d
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

### PostgreSQL
- **Connection URI**: `postgresql://admin:postgres@localhost:5432/postgres`
- **Host**: localhost
- **Port**: 5432
- **Username**: admin
- **Password**: postgres
- **Database**: postgres
- **From other containers**: `postgres:5432`

### Elasticsearch
- **HTTP API**: http://localhost:9200
- **Username**: elastic
- **Password**: elastic
- **Health Check**: `curl http://localhost:9200/_cluster/health`
- **From other containers**: `elasticsearch:9200`

### Jaeger (OpenTelemetry)
- **Jaeger UI**: http://localhost:16686
- **HTTP Collector**: localhost:14268
- **gRPC Collector**: localhost:14250
- **UDP Agent**: localhost:6831, localhost:6832
- **From other containers**: `jaeger:14268` (HTTP), `jaeger:14250` (gRPC)

## 📁 Data Persistence

All data is persisted using Docker volumes:
- `rabbitmq_data` - RabbitMQ data and configuration
- `mongodb_data` - MongoDB database files
- `mongodb_config` - MongoDB configuration files
- `postgresql_data` - PostgreSQL database files
- `elasticsearch_data` - Elasticsearch indices and configuration
- `jaeger_data` - Jaeger traces and temporary data

## � What is RabbitMQ and Why Use It?

**RabbitMQ** is a robust message broker that implements the Advanced Message Queuing Protocol (AMQP). It acts as an intermediary for messaging, allowing applications to communicate asynchronously through message queues.

### 🎯 **Key Benefits:**

1. **📨 Asynchronous Communication**: Decouple services by allowing them to communicate without waiting for responses
2. **⚡ Scalability**: Handle high-throughput message processing with clustering and federation
3. **🔄 Reliability**: Ensure message delivery with persistence, acknowledgments, and clustering
4. **🎛️ Flexible Routing**: Advanced routing capabilities with exchanges, queues, and bindings
5. **📊 Management & Monitoring**: Web-based management interface for monitoring and administration

### 📈 **Perfect for:**
- **Microservices Communication**: Enable loose coupling between services
- **Background Job Processing**: Queue tasks for asynchronous processing
- **Event-Driven Architecture**: Publish/subscribe patterns for real-time updates
- **Load Distribution**: Distribute workload across multiple workers
- **Integration Patterns**: Connect different systems and applications

### 💡 **Real-world Examples:**
- **E-commerce**: Order processing, inventory updates, email notifications
- **Social Media**: Real-time notifications, feed updates, content processing
- **IoT Applications**: Device data collection and processing
- **Financial Systems**: Transaction processing, audit logging

## 🍃 What is MongoDB and Why Use It?

**MongoDB** is a NoSQL document database that stores data in flexible, JSON-like documents. It's designed for modern applications that need to store and query data in a natural, intuitive way.

### 🎯 **Key Benefits:**

1. **📄 Flexible Schema**: Store documents with different structures in the same collection
2. **🚀 Rapid Development**: Natural mapping to objects in programming languages
3. **📈 Horizontal Scaling**: Built-in sharding for distributed data storage
4. **🔍 Rich Queries**: Support for complex queries, indexing, and aggregation
5. **⚡ High Performance**: Optimized for read and write operations with in-memory storage

### 📈 **Perfect for:**
- **Content Management**: Store articles, blogs, user-generated content
- **User Profiles**: Flexible user data with varying attributes
- **Product Catalogs**: E-commerce products with different specifications
- **IoT Data**: Time-series data from sensors and devices
- **Real-time Analytics**: Event tracking and behavioral data

### 💡 **Real-world Examples:**
- **Social Networks**: User profiles, posts, comments, relationships
- **E-commerce**: Product catalogs, user reviews, shopping carts
- **Gaming**: Player profiles, game states, leaderboards
- **Mobile Apps**: User preferences, app data, offline synchronization

## 🐘 What is PostgreSQL and Why Use It?

**PostgreSQL** is an advanced, open-source relational database management system (RDBMS) known for its reliability, feature robustness, and performance. It's often called "the world's most advanced open source database."

### 🎯 **Key Benefits:**

1. **🔒 ACID Compliance**: Guarantees data integrity with Atomicity, Consistency, Isolation, Durability
2. **🔗 Complex Relationships**: Support for foreign keys, joins, and complex relational operations
3. **📊 Advanced Data Types**: JSON, arrays, geometric types, and custom data types
4. **⚡ High Performance**: Query optimization, indexing, and parallel processing
5. **🛡️ Enterprise Features**: Row-level security, advanced authentication, and backup solutions

### 📈 **Perfect for:**
- **Financial Applications**: Banking, accounting, payment processing
- **Enterprise Systems**: ERP, CRM, inventory management
- **Data Warehousing**: Business intelligence and analytics
- **Government Systems**: Public records, compliance, auditing
- **Scientific Applications**: Research data, statistical analysis

### 💡 **Real-world Examples:**
- **Banking**: Account management, transaction processing, regulatory compliance
- **Healthcare**: Patient records, medical history, prescription tracking
- **Supply Chain**: Inventory tracking, order management, supplier relationships
- **Education**: Student records, course management, grading systems

## 🔍 What is Elasticsearch and Why Use It?

**Elasticsearch** is a distributed, RESTful search and analytics engine built on Apache Lucene. It's designed for horizontal scalability, maximum reliability, and real-time search capabilities.

### 🎯 **Key Benefits:**

1. **🔍 Full-Text Search**: Powerful search capabilities with relevance scoring
2. **📊 Real-time Analytics**: Analyze large volumes of data in near real-time
3. **📈 Scalability**: Distribute data across multiple nodes for high availability
4. **🔄 RESTful API**: Simple HTTP-based API for all operations
5. **📋 Schema-free**: Dynamic mapping for flexible document structures

### 📈 **Perfect for:**
- **Search Engines**: Website search, product search, content discovery
- **Log Analytics**: Centralized logging, monitoring, troubleshooting
- **Business Intelligence**: Real-time dashboards, data visualization
- **Security Analytics**: Threat detection, security monitoring
- **Recommendation Systems**: Content recommendations, personalization

### 💡 **Real-world Examples:**
- **E-commerce**: Product search, faceted navigation, recommendations
- **Media**: Content search, article discovery, media asset management
- **DevOps**: Log aggregation, application monitoring, performance analytics
- **Security**: SIEM (Security Information and Event Management)

## �🔍 What is OpenTelemetry and Why Use It?

**OpenTelemetry** is an observability framework that helps you understand what's happening inside your applications and infrastructure. **Jaeger** is a distributed tracing system that implements OpenTelemetry standards.

### 🎯 **Key Benefits:**

1. **🔍 Distributed Tracing**: Track requests as they flow through multiple services
2. **🐛 Debugging**: Quickly identify performance bottlenecks and errors
3. **📊 Performance Monitoring**: Monitor response times, database queries, and API calls
4. **🔗 Service Dependencies**: Visualize how your services interact with each other
5. **📈 Analytics**: Understand usage patterns and system behavior

### 📈 **Perfect for:**
- **Microservices Architecture**: Track requests across multiple services
- **API Development**: Monitor API performance and errors
- **Database Performance**: See which queries are slow
- **Third-party Integrations**: Monitor external service calls
- **Production Debugging**: Quickly find the root cause of issues

## 🎯 User-Friendly Usage Guide

### 🚀 Getting Started (Beginner)

1. **Start all services** (easiest way):
   ```bash
   docker-compose up -d
   ```

2. **Check if everything is running**:
   ```bash
   docker-compose ps
   ```
   You should see all 5 services with "Up" status.

3. **Access the services**:
   - **RabbitMQ Management**: Open http://localhost:15672 in your browser
   - **PostgreSQL**: Use any PostgreSQL client with `localhost:5432`
   - **MongoDB**: Use any MongoDB client with `localhost:27017`
   - **Elasticsearch**: Open http://localhost:9200 in your browser
   - **Jaeger UI**: Open http://localhost:16686 in your browser

### 🔧 Common Development Scenarios

#### Scenario 1: Web Application Development
```bash
# Start databases only
docker-compose up -d postgresql mongodb

# Your app connects to:
# - PostgreSQL: postgresql://admin:postgres@localhost:5432/postgres
# - MongoDB: mongodb://admin:admin@localhost:27017/myapp
```

#### Scenario 2: Message Queue Development
```bash
# Start RabbitMQ and databases
docker-compose up -d rabbitmq postgresql mongodb

# Access RabbitMQ management at: http://localhost:15672
# Login: admin / admin
```

#### Scenario 3: Search and Analytics
```bash
# Start search stack
docker-compose up -d elasticsearch mongodb

# Test Elasticsearch:
curl http://localhost:9200/_cluster/health
```

#### Scenario 4: Full Microservices Stack
```bash
# Start everything
docker-compose up -d

# All services communicate via app_network
```

#### Scenario 5: Observability and Monitoring
```bash
# Start observability stack with databases
docker-compose up -d jaeger postgresql mongodb

# Access Jaeger UI at: http://localhost:16686
# Monitor your application traces and performance
```

### 🛠️ Service-Specific Usage

#### RabbitMQ Usage
```bash
# Start RabbitMQ
docker-compose up -d rabbitmq

# Access Management UI
# URL: http://localhost:15672
# Username: admin
# Password: admin

# Create a queue via management UI or API
curl -u admin:admin -X PUT http://localhost:15672/api/queues/%2F/test-queue

# Send a message
curl -u admin:admin -X POST http://localhost:15672/api/exchanges/%2F/amq.default/publish \
  -H "Content-Type: application/json" \
  -d '{"properties":{},"routing_key":"test-queue","payload":"Hello World","payload_encoding":"string"}'
```

#### MongoDB Usage
```bash
# Start MongoDB
docker-compose up -d mongodb

# Connect using MongoDB shell
docker-compose exec mongodb mongosh -u admin -p admin

# Create a collection and insert data
use myapp
db.users.insertOne({name: "John", email: "john@example.com"})
db.users.find()

# Or connect with MongoDB Compass:
# Connection string: mongodb://admin:admin@localhost:27017/myapp
```

#### PostgreSQL Usage
```bash
# Start PostgreSQL
docker-compose up -d postgresql

# Connect using psql
docker-compose exec postgresql psql -U admin -d postgres

# Create a table and insert data
CREATE TABLE users (id SERIAL PRIMARY KEY, name VARCHAR(100), email VARCHAR(100));
INSERT INTO users (name, email) VALUES ('John', 'john@example.com');
SELECT * FROM users;

# Or connect with pgAdmin/DBeaver:
# Host: localhost, Port: 5432, Database: postgres, User: admin, Password: postgres
```

#### Elasticsearch Usage
```bash
# Start Elasticsearch
docker-compose up -d elasticsearch

# Check cluster health
curl http://localhost:9200/_cluster/health

# Create an index
curl -X PUT "localhost:9200/products" -H 'Content-Type: application/json' -d'
{
  "mappings": {
    "properties": {
      "name": {"type": "text"},
      "price": {"type": "float"},
      "category": {"type": "keyword"}
    }
  }
}'

# Add a document
curl -X POST "localhost:9200/products/_doc/1" -H 'Content-Type: application/json' -d'
{
  "name": "Laptop",
  "price": 999.99,
  "category": "Electronics"
}'

# Search documents
curl -X GET "localhost:9200/products/_search?q=laptop"

# Or use Kibana/Elasticsearch tools with: http://localhost:9200
```

#### Jaeger (OpenTelemetry) Usage
```bash
# Start Jaeger
docker-compose up -d jaeger

# Access Jaeger UI
# URL: http://localhost:16686

# Test Jaeger is working
curl http://localhost:16686/api/services

# Example: Send a test trace (using curl)
curl -X POST http://localhost:14268/api/traces \
  -H "Content-Type: application/json" \
  -d '{
    "data": [{
      "traceID": "1234567890abcdef",
      "spanID": "abcdef1234567890",
      "operationName": "test-operation",
      "startTime": 1642680000000000,
      "duration": 1000000,
      "tags": [
        {"key": "service.name", "value": "test-service"},
        {"key": "http.method", "value": "GET"},
        {"key": "http.url", "value": "/api/test"}
      ]
    }]
  }'
```

### 🚀 **Instrumenting Your Applications**

#### **Node.js Example:**
```javascript
// Install dependencies
// npm install @opentelemetry/api @opentelemetry/node @opentelemetry/exporter-jaeger

const { NodeSDK } = require('@opentelemetry/node');
const { JaegerExporter } = require('@opentelemetry/exporter-jaeger');

// Configure Jaeger exporter
const jaegerExporter = new JaegerExporter({
  endpoint: 'http://localhost:14268/api/traces',
});

// Initialize OpenTelemetry
const sdk = new NodeSDK({
  traceExporter: jaegerExporter,
  serviceName: 'my-node-app',
});

sdk.start();

// Your application code here
const express = require('express');
const app = express();

app.get('/api/users', async (req, res) => {
  // This request will be automatically traced
  res.json({ users: [] });
});

app.listen(3000);
```

#### **Python Example:**
```python
# Install dependencies
# pip install opentelemetry-api opentelemetry-sdk opentelemetry-exporter-jaeger

from opentelemetry import trace
from opentelemetry.exporter.jaeger.thrift import JaegerExporter
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import BatchSpanProcessor

# Configure Jaeger exporter
jaeger_exporter = JaegerExporter(
    agent_host_name="localhost",
    agent_port=6831,
)

# Set up tracing
trace.set_tracer_provider(TracerProvider())
tracer = trace.get_tracer(__name__)

span_processor = BatchSpanProcessor(jaeger_exporter)
trace.get_tracer_provider().add_span_processor(span_processor)

# Example usage
def process_request():
    with tracer.start_as_current_span("process_request") as span:
        span.set_attribute("user.id", "12345")
        span.set_attribute("request.type", "api")
        
        # Your business logic here
        return {"status": "success"}

# Flask example
from flask import Flask
app = Flask(__name__)

@app.route('/api/data')
def get_data():
    with tracer.start_as_current_span("get_data_endpoint"):
        return process_request()
```

#### **Java Spring Boot Example:**
```java
// Add to pom.xml
/*
<dependency>
    <groupId>io.opentelemetry</groupId>
    <artifactId>opentelemetry-api</artifactId>
    <version>1.32.0</version>
</dependency>
<dependency>
    <groupId>io.opentelemetry</groupId>
    <artifactId>opentelemetry-exporter-jaeger</artifactId>
    <version>1.32.0</version>
</dependency>
*/

// Application configuration
import io.opentelemetry.api.OpenTelemetry;
import io.opentelemetry.exporter.jaeger.JaegerGrpcSpanExporter;
import io.opentelemetry.sdk.OpenTelemetrySdk;
import io.opentelemetry.sdk.trace.SdkTracerProvider;
import io.opentelemetry.sdk.trace.export.BatchSpanProcessor;

@Configuration
public class TracingConfig {
    
    @Bean
    public OpenTelemetry openTelemetry() {
        return OpenTelemetrySdk.builder()
            .setTracerProvider(
                SdkTracerProvider.builder()
                    .addSpanProcessor(BatchSpanProcessor.builder(
                        JaegerGrpcSpanExporter.builder()
                            .setEndpoint("http://localhost:14250")
                            .build())
                        .build())
                    .build())
            .build();
    }
}

// Controller example
@RestController
public class ApiController {
    
    private final Tracer tracer = GlobalOpenTelemetry.getTracer("my-spring-app");
    
    @GetMapping("/api/users")
    public ResponseEntity<List<User>> getUsers() {
        Span span = tracer.spanBuilder("get_users").startSpan();
        try (Scope scope = span.makeCurrent()) {
            span.setAttribute("operation", "fetch_users");
            // Your business logic
            return ResponseEntity.ok(userService.findAll());
        } finally {
            span.end();
        }
    }
}
```

### 📊 **Using Jaeger UI**

1. **Open Jaeger UI**: http://localhost:16686

2. **Find Traces**: 
   - Select your service from the dropdown
   - Choose time range
   - Click "Find Traces"

3. **Analyze Performance**:
   - Click on a trace to see detailed timing
   - Identify slow operations
   - Check error rates

4. **Service Dependencies**:
   - Go to "Dependencies" tab
   - See how services interact
   - Identify bottlenecks

### 🔧 **Configuration for Different Languages**

#### **Environment Variables** (Universal):
```bash
export OTEL_EXPORTER_JAEGER_ENDPOINT=http://localhost:14268/api/traces
export OTEL_SERVICE_NAME=my-application
export OTEL_RESOURCE_ATTRIBUTES=service.version=1.0.0
```

#### **Docker Compose Integration** (for your apps):
```yaml
# Add to your application service in docker-compose.yml
your-app:
  image: your-app:latest
  environment:
    - OTEL_EXPORTER_JAEGER_ENDPOINT=http://jaeger:14268/api/traces
    - OTEL_SERVICE_NAME=your-app
  networks:
    - app_network
  depends_on:
    - jaeger
```

### 🔍 Quick Health Checks

```bash
# Check all services status
docker-compose ps

# Quick test all services
echo "Testing RabbitMQ..." && curl -s http://localhost:15672 > /dev/null && echo "✅ RabbitMQ OK"
echo "Testing PostgreSQL..." && docker-compose exec -T postgresql pg_isready -U admin && echo "✅ PostgreSQL OK"
echo "Testing MongoDB..." && docker-compose exec -T mongodb mongosh --eval "db.runCommand('ping')" --quiet && echo "✅ MongoDB OK"
echo "Testing Elasticsearch..." && curl -s http://localhost:9200/_cluster/health > /dev/null && echo "✅ Elasticsearch OK"
echo "Testing Jaeger..." && curl -s http://localhost:16686/api/services > /dev/null && echo "✅ Jaeger OK"
```

### 💡 Pro Tips

1. **Save Resources**: Only run services you need
   ```bash
   # For web development
   docker-compose up -d postgresql mongodb
   
   # For observability testing
   docker-compose up -d jaeger postgresql
   ```

2. **Monitor Resources**: Check resource usage
   ```bash
   docker stats
   ```

3. **Clean Start**: Reset everything
   ```bash
   docker-compose down -v  # ⚠️ This deletes all data
   docker-compose up -d
   ```

4. **Backup Data**: Before major changes
   ```bash
   # PostgreSQL backup
   docker-compose exec postgresql pg_dump -U admin postgres > backup_postgres.sql
   
   # MongoDB backup
   docker-compose exec mongodb mongodump --host localhost --port 27017 --username admin --password admin --out /data/backup
   
   # Export Jaeger traces
   curl "http://localhost:16686/api/traces?service=your-service&start=1642680000000000&end=1642766400000000" > traces_backup.json
   ```

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
docker-compose exec postgresql psql -U admin -d postgres
docker-compose exec jaeger sh
```

### Logs and Debugging
```bash
# View logs for all services
docker-compose logs

# View logs for specific service
docker-compose logs rabbitmq
docker-compose logs mongodb
docker-compose logs postgresql
docker-compose logs elasticsearch
docker-compose logs jaeger

# Follow logs in real-time
docker-compose logs -f --tail=100

# View only recent logs
docker-compose logs --tail=50
```

### Data Management
```bash
# PostgreSQL backup
docker-compose exec postgresql pg_dump -U admin postgres > backup_postgres.sql

# MongoDB backup
docker-compose exec mongodb mongodump --host localhost --port 27017 --username admin --password admin --out /data/backup

# Elasticsearch backup (snapshot)
curl -X PUT "localhost:9200/_snapshot/backup_repo" -H 'Content-Type: application/json' -d'
{
  "type": "fs",
  "settings": {
    "location": "/usr/share/elasticsearch/backup"
  }
}'

# View volume information
docker volume ls
docker volume inspect docker-compose_mongodb_data
docker volume inspect docker-compose_postgresql_data
docker volume inspect docker-compose_elasticsearch_data
docker volume inspect docker-compose_jaeger_data
```

## 🔧 Configuration

### Environment Variables
You can customize the services by modifying the environment variables in `docker-compose.yml`:

**RabbitMQ:**
- `RABBITMQ_DEFAULT_USER` - Default username (current: admin)
- `RABBITMQ_DEFAULT_PASS` - Default password (current: admin)

**MongoDB:**
- `MONGO_INITDB_ROOT_USERNAME` - Root username (current: admin)
- `MONGO_INITDB_ROOT_PASSWORD` - Root password (current: admin)
- `MONGO_INITDB_DATABASE` - Default database name (current: myapp)

**PostgreSQL:**
- `POSTGRES_DB` - Default database name (current: postgres)
- `POSTGRES_USER` - Default username (current: admin)
- `POSTGRES_PASSWORD` - Default password (current: postgres)

**Elasticsearch:**
- `ELASTIC_PASSWORD` - Elastic user password (current: elastic)
- `ES_JAVA_OPTS` - JVM options (current: -Xms512m -Xmx512m)

**Jaeger:**
- `COLLECTOR_OTLP_ENABLED` - Enable OpenTelemetry collector (current: true)
- `COLLECTOR_ZIPKIN_HOST_PORT` - Zipkin compatibility port (current: :9411)

### Port Mapping
- RabbitMQ: `5672` (AMQP), `15672` (Management UI)
- MongoDB: `27017`
- PostgreSQL: `5432`
- Elasticsearch: `9200` (HTTP API), `9300` (Transport)
- Jaeger: `16686` (UI), `14268` (HTTP collector), `14250` (gRPC collector), `6831/6832` (UDP agent)

## 🚨 Troubleshooting

### Common Issues

1. **Port already in use**
   ```bash
   # Check what's using the port
   netstat -an | grep :27017    # MongoDB
   netstat -an | grep :5432     # PostgreSQL
   netstat -an | grep :9200     # Elasticsearch
   netstat -an | grep :15672    # RabbitMQ Management
   netstat -an | grep :16686    # Jaeger UI
   
   # Change port mapping in docker-compose.yml if needed
   ```

2. **Container won't start**
   ```bash
   # Check container logs
   docker-compose logs [service-name]
   
   # Restart specific service
   docker-compose restart [service-name]
   
   # Check system resources
   docker system df
   ```

3. **Data not persisting**
   ```bash
   # Verify volumes exist
   docker volume ls
   
   # Check volume mount points
   docker-compose config
   
   # Inspect specific volume
   docker volume inspect docker-compose_[service]_data
   ```

4. **Can't connect to services**
   ```bash
   # Verify services are running
   docker-compose ps
   
   # Check network connectivity
   docker-compose exec rabbitmq ping mongodb
   docker-compose exec postgresql ping elasticsearch
   
   # Test service endpoints
   curl http://localhost:9200/_cluster/health    # Elasticsearch
   curl http://localhost:15672                   # RabbitMQ Management
   curl http://localhost:16686/api/services      # Jaeger
   ```

5. **Elasticsearch won't start (memory issues)**
   ```bash
   # Increase Docker memory limit to at least 4GB
   # Or reduce Elasticsearch memory in docker-compose.yml:
   # ES_JAVA_OPTS: "-Xms256m -Xmx256m"
   ```

6. **Permission denied errors**
   ```bash
   # Fix volume permissions
   docker-compose down
   sudo chown -R 1000:1000 /var/lib/docker/volumes/
   docker-compose up -d
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

## 🔗 Quick Reference Links

### 🌐 **Management Interfaces**
- **RabbitMQ Management**: http://localhost:15672 (admin/admin)
- **Jaeger Tracing UI**: http://localhost:16686
- **Elasticsearch API**: http://localhost:9200

### 📖 **Documentation Shortcuts**
- [Service Overview Table](#-services-overview) - Compare all services at a glance
- [Quick Start Guide](#-quick-start) - Get up and running in 2 minutes
- [Individual Service Usage](#️-service-specific-usage) - Detailed examples for each service
- [Real-World Examples](#-real-world-application-examples) - Architecture patterns and use cases
- [Troubleshooting Guide](#-troubleshooting) - Fix common issues
- [Configuration Reference](#-configuration) - Customize service settings

### ⚡ **Quick Commands**
```bash
# Start everything
docker-compose up -d

# Check status
docker-compose ps

# View all logs
docker-compose logs -f

# Stop everything
docker-compose down

# Reset all data (⚠️ destructive)
docker-compose down -v
```

---

**Happy Coding!** 🚀

*This README is designed to help you quickly find and understand each service. Use the table of contents above to jump to specific sections, or check the service overview table to compare functionality at a glance.*
