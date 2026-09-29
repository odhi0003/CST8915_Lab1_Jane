# CST8915 Lab 1: Algonquin Pet Store on Azure VM

**Student Name**: Jane Akinyi Odhiambo
**Student ID**: 041268593
**Course**: CST8915 Full-stack Cloud-native Development
**Semester**: Fall 2026

---

## Demo Video

🎥 [Watch Demo Video](https://www.youtube.com/watch?v=_VY6ONsh6TQ)

---

## Technical Explanations

### Order Service (Node.js)

The order service receives new orders through a REST API and puts them on a RabbitMQ queue for processing. The service uses Node.js for a `POST /orders` API endpoint, parses JSON requests, and enables CORS for front-end. The service serializes the orders data into JSON and publishes it to `order_queue`.

The service is like a producer in the microservices system. It separates order submission from order processing. It also communicates asynchronously with other services through RabbitMQ, using AMQP.

### Product Service (Rust)

The product service provides product information. The service exposes a `GET /products` endpoint, that returns a JSON array, which contains product IDs, names, and prices. This service is implemented using Warp web framework.

The Product Service acts as a data provider in the microservices system, for the store front. Communication occurs through REST, where clients send `GET` requests to `/products`. CORS is enabled so that the frontend can request product data from a different origin. The product data is currently hard-coded in the service, instead of fetching dynamically from a database.

### Store Front (Vue.js)

The store front is the user interface that allows users to browse products and place orders. It is built with Vue.js, using components such as `App.vue` and `OrderForm.vue`. The application fetches product data when the component is created, lets users select a product and quantity, calculates the total price, and lets the user submit the completed order.

The Store Front acts as the client that connects the user to the backend services. It communicates with the product services through a `GET` request to `http://localhost:3030/products` to retrieve available products, and also communicates with the order service through a `POST` request to `http://localhost:3000/orders` to submit orders. The CORS on the backend services allows these requests from the frontend.

---

## Challenges and Learnings (Optional)

During setup, I initially left the disk settings at their default values and only configured the basic settings. However, the virtual machine failed to deploy because Microsoft Azure returned a Policy Violation error indicating that my subscription required the use of Standard SSD LRS. I used Microsoft Copilot in Azure to understand why the deployment failed and identify where the disk configuration needed to be changed.

I changed the disk type from Premium SSD LRS to Standard SSD LRS, after which the virtual machine deployed successfully. This experience taught me how resource configurations can affect deployment. It also showed me how troubleshooting tools such as Microsoft Copilot can help identify and resolve configuration issues.

---

## Acknowledgments

I am grateful to Microsoft Copilot in the Azure portal for assisting me in troubleshooting and resolving the policy violation encountered during the virtual machine deployment.