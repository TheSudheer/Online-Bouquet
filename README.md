Here’s the updated project description with the required changes:  

### **Microservices Demo Application**  
This project is a cloud-first microservices demo application designed to showcase the deployment and management of a web-based e-commerce app on Kubernetes. Users can browse items, add them to their cart, and proceed to purchase.  

---

### **Table of Contents**  
- Architecture Overview  
- Microservices  
- Deployment Instructions  
- License  
- Acknowledgements  

---

### **📌 Note**  
🚀 **This project also uses Helm!** To use Helm, navigate to the `charts` directory at the top or click this link:  
👉 [Helm Charts](https://github.com/TheSudheer/Online-Bouquet/tree/main/charts)  

---

### **Architecture Overview**  
The application consists of multiple microservices, each responsible for a specific functionality within the e-commerce platform. These services communicate primarily via gRPC (according to Google) and are deployed on Kubernetes.  

---

### **Microservices**  
The application comprises the following microservices:  
- **Frontend**: Serves the web application to users and handles user interactions.  
- **Product Catalog Service**: Manages the product listings available in the store.  
- **Cart Service**: Manages the items users add to their shopping carts.  
- **Currency Service**: Provides currency conversion rates.  
- **Recommendation Service**: Offers product recommendations to users.  
- **Shipping Service**: Calculates shipping costs based on user selections.  
- **Payment Service**: Processes user payments.  
- **Email Service**: Sends order confirmations and other notifications to users.  
- **Ad Service**: Provides advertising content for the application.  
- **Checkout Service**: Orchestrates the checkout process by interacting with other services.  

---

### **Deployment Instructions**  
To deploy the application on a Kubernetes cluster:  

#### **Clone the Repository**  
```bash
git clone https://github.com/TheSudheer/Online-Bouquet.git
cd Online-Bouquet
```

#### **Deploy Microservices**  
Apply the Kubernetes manifests for each microservice:  
```bash
kubectl apply -f adservice.yaml
kubectl apply -f cartservice.yaml
kubectl apply -f checkoutservice.yaml
kubectl apply -f currencyservice.yaml
kubectl apply -f emailservice.yaml
kubectl apply -f frontend.yaml
kubectl apply -f paymentservice.yaml
kubectl apply -f productcatalogservice.yaml
kubectl apply -f recommendationservice.yaml
kubectl apply -f rediscartservice.yaml
kubectl apply -f shippingservice.yaml
```

#### **Verify Deployment**  
Ensure all pods are running:  
```bash
kubectl get pods
```

#### **Access the Application**  
The frontend service is exposed via a NodePort. Retrieve the NodePort and access the application through your browser:  
```bash
kubectl get service frontend
```
Navigate to `http://<node-ip>:<node-port>` in your web browser.  

---

### **Acknowledgements**  
This project is forked from Google's [microservices-demo](https://github.com/GoogleCloudPlatform/microservices-demo) project.

---

